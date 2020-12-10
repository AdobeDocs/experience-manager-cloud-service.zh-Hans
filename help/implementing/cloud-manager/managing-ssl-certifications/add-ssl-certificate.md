---
title: 添加SSL证书——管理SSL证书
description: 添加SSL证书——管理SSL证书
translation-type: tm+mt
source-git-commit: 88ef9265b40f64f2229e37e5f8ca02959e8d9ce2
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 0%

---


# 添加SSL证书{#adding-an-ssl-certificate}

>[!NOTE]
>AEM作为Cloud Service将仅接受OV（组织验证）或EV（扩展验证）证书。 将不接受DV（域验证）证书。

配置证书需要几天时间，建议提前数月配置证书。 有关详细信息，请参阅[获取SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/get-ssl-certificate.md)。

## 证书格式{#certificate-format}

SSL文件必须采用PEM格式，才能安装在云管理器上。 PEM格式中的常见文件扩展名包括`.pem,`。`crt`、 `.cer`和 `.cert`。

请按照以下步骤将SSL文件的格式转换为PEM:

1. 将PFX转换为PEM

`openssl pkcs12 -in certificate.pfx -out certificate.cer -nodes`

1. 将P7B转换为PEM

`openssl pkcs7 -print_certs -in certificate.p7b -out certificate.cer`

1. 将DER转换为PEM

`openssl x509 -inform der -in certificate.cer -out certificate.pem`

## 添加证书{#adding-certificate}

>[!NOTE]
>* 要在云管理器中安装SSL证书，用户必须处于业务所有者或部署管理器角色。
>* 在任何给定时间，云管理器将允许最多10个SSL证书，这些证书可以与您项目内的一个或多个环境关联，即使证书已过期也是如此。 但是，云管理器UI允许在具有此约束的项目中安装最多50个SSL证书。


请按照以下步骤添加证书：

1. 登录Cloud Manager。
1. 从&#x200B;**概述**&#x200B;页面导航到&#x200B;**环境**&#x200B;屏幕。
1. 单击左侧导航菜单中的&#x200B;**SSL证书**。 此屏幕上将显示包含任何现有SSL证书详细信息的表。

   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-1.png)
1. 选择&#x200B;**添加证书**&#x200B;按钮以打开&#x200B;**添加SSL证书**&#x200B;对话框。

   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-2.png)
   1. 在&#x200B;**证书名称**&#x200B;中输入证书的名称。 这可以是帮助您轻松引用证书的任何名称。
   1. 将&#x200B;**证书**、**私钥**&#x200B;和&#x200B;**证书链**&#x200B;粘贴到各自的字段中。 使用输入框右侧的粘贴图标。

      >[!NOTE]
      >这三个字段都不是可选字段，必须包括在内。
1. 单击&#x200B;**保存**&#x200B;以提交您的证书。 您将在表中看到它显示为新行。
   >[!NOTE]
   >将显示检测到的任何错误。 在保存证书之前，必须解决所有错误。 请参阅[证书错误](#certificate-errors)，进一步了解如何解决常见错误。

## 证书错误{#certificate-errors}

### 正确的证书顺序{#correct-certificate-order}

证书部署失败的最常见原因是中间或链证书的顺序不正确。 具体而言，中间证书文件必须以最接近根的根证书或证书结尾，并以从`main/server`证书到根证书的降序排列。

您可以使用以下命令确定中间文件的顺序：

`openssl crl2pkcs7 -nocrl -certfile $CERT_FILE | openssl pkcs7 -print_certs -noout`

您可以使用以下命令验证私钥和`main/server`证书是否匹配：

`openssl x509 -noout -modulus -in certificate.pem | openssl md5`

`openssl rsa -noout -modulus -in ssl.key | openssl md5`

>[!NOTE]
>这两个命令的输出必须完全相同。 如果找不到与`main/server`证书匹配的私钥，则需要通过生成新的CSR和／或从SSL供应商请求更新的证书来重新键入证书。

### 证书有效日期{#certificate-validity-dates}

Cloud Manager预计SSL证书在将来至少90天内有效

检查证书链的有效性。
