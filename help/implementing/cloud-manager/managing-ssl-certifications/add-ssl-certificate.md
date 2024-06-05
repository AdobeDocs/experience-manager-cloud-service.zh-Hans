---
title: 添加 SSL 证书
description: 了解如何使用 Cloud Manager 的自助服务工具添加您自己的 SSL 证书。
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 80%

---

# 添加 SSL 证书 {#adding-an-ssl-certificate}

了解如何使用 Cloud Manager 的自助服务工具添加您自己的 SSL 证书。

>[!TIP]
>
>提供证书可能需要几天时间。因此，Adobe 建议提前提供证书。

## 证书要求 {#certificate-requirements}

查看部分 **证书要求** 文档的 [管理SSL证书简介](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md#requirements) 以确保AEMas a Cloud Service支持您要添加的证书。

## 添加证书 {#adding-a-cert}

按照以下步骤使用 Cloud Manager 添加证书。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台上，选择该程序。

1. 从&#x200B;**概述**&#x200B;页面导航到&#x200B;**环境**&#x200B;屏幕。

1. 单击 **SSL证书** 从左侧导航面板中。 主屏幕上显示一个包含任何现有 SSL 证书详细信息的表。

   ![添加 SSL 证书](/help/implementing/cloud-manager/assets/ssl/ssl-cert-1.png)

1. 单击 **添加SSL证书** 以打开 **添加SSL证书** 对话框。

   * 在&#x200B;**证书名称**&#x200B;中输入证书名称。
      * 这仅供参考，可以是任何有助于您轻松引用证书的名称。
   * 将&#x200B;**证书**、**私钥**&#x200B;和&#x200B;**证书链**&#x200B;值粘贴到各自的字段中。这三个字段都是必填字段。
   * 在某些情况下，最终用户证书可能会包含在链中，并且必须在将链粘贴到字段之前将其清除。

   ![添加“SSL 证书”对话框](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)

   * 显示检测到的任何错误。
      * 在保存证书之前，必须解决所有错误。
      * 请参阅[证书错误](#certificate-errors)部分，了解有关解决常见错误的更多信息。

1. 单击&#x200B;**保存**，保存您的证书。

保存后，您将看到证书在表中显示为新行。

![保存的 SSL 证书](/help/implementing/cloud-manager/assets/ssl/ssl-cert-3.png)

>[!NOTE]
>
>用户必须是&#x200B;**业务负责人**&#x200B;或&#x200B;**部署管理员**&#x200B;角色成员，才能在 Cloud Manager 中安装 SSL 证书。

>[!NOTE]
>
>如果您收到类似于的错误 `The Subject of an intermediate certificate must match the issuer in the previous certificate. The SKI of an intermediate certificate must match the AKI of the previous certificate.`中，您可能已将客户端证书包含在证书链中。 请确保该链不包含客户端证书，然后重试。

## 证书错误 {#certificate-errors}

如果证书安装不正确或不符合 Cloud Manager 的要求，则可能会出现某些错误。

### 证书策略 {#certificate-policy}

如果您看到以下错误，请检查证书的策略。

```text
Certificate policy must conform with EV or OV, and not DV policy.
```

通常，证书策略由嵌入的 OID 值标识。将证书输出到文本并搜索 OID 将显示证书的策略。

您可以使用以下示例作为指导，将证书详细信息输出为文本。

```text
openssl x509 -in 9178c0f58cb8fccc.pem -text
certificate:
    Data:
        Version: 3 (0x2)
        Serial Number:
            91:78:c0:f5:8c:b8:fc:cc
        Signature Algorithm: sha256WithRSAEncryption
        Issuer: C = US, ST = Arizona, L = Scottsdale, O = "GoDaddy.com, Inc.", OU = http://certs.godaddy.com/repository/, CN = Go Daddy Secure Certificate Authority - G2
        Validity
            Not Before: Nov 10 22:55:36 2021 GMT
            Not After : Dec  6 15:35:06 2022 GMT
        Subject: C = US, ST = Colorado, L = Denver, O = Alexandra Alwin, CN = adobedigitalimpact.com
        Subject Public Key Info:
...
```

文本中的 OID 模式定义证书的策略类型。

| 图案 | 策略 | 在 Cloud Manager 中可接受 |
|---|---|---|
| `2.23.140.1.1` | EV | 是 |
| `2.23.140.1.2.2` | OV | 是 |
| `2.23.140.1.2.1` | DV | 否 |

通过 `grep`ping 输出证书文本中的 OID 模式，您可以确认您的证书策略。

```shell
# "EV Policy"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.1" -B5

# "OV Policy"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.2.2" -B5

# "DV Policy - Not Accepted"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.2.1" -B5
```

### 正确的证书顺序 {#correct-certificate-order}

证书部署失败的最常见原因是中间证书或链证书的顺序不正确。

中间证书文件必须以根证书或最接近根的证书结尾。它们必须从 `main/server` 证书降序到根目录。

可以使用以下命令确定中间文件的顺序。

```shell
openssl crl2pkcs7 -nocrl -certfile $CERT_FILE | openssl pkcs7 -print_certs -noout
```

您可以使用以下命令验证私钥和 `main/server` 证书是否匹配。

```shell
openssl x509 -noout -modulus -in certificate.pem | openssl md5
```

```shell
openssl rsa -noout -modulus -in ssl.key | openssl md5
```

>[!NOTE]
>
>这两个命令的输出必须完全相同。如果您找不到 `main/server` 证书的匹配私钥，您需要通过生成新的 CSR 和/或向 SSL 供应商请求更新的证书来重新键入证书。

### 证书有效日期 {#certificate-validity-dates}

Cloud Manager 希望 SSL 证书自当前日期起至少 90 天有效。您应该检查证书链的有效性。
