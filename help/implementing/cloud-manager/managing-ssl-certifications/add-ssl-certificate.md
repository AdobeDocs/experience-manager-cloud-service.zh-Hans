---
title: 添加SSL证书
description: 了解如何使用Cloud Manager的自助服务工具添加您自己的SSL证书或DV（域验证）证书。
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: fcde1f323392362d826f9b4a775e468de9550716
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 27%

---


# 添加SSL证书

了解如何使用Cloud Manager的自助服务工具添加客户管理的SSL证书或Adobe生成和管理的DV（域验证）证书。


## 添加SSL或DV证书 {#adding-an-ssl-certificate}

提供证书可能需要几天时间。因此，Adobe建议在任何截止日期或上线日期之前提前配置证书。

请查看[管理SSL证书简介](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md#requirements)中的&#x200B;**证书要求**，以确保AEM as a Cloud Service支持您要添加的证书。

用户必须是&#x200B;**业务负责人**&#x200B;或&#x200B;**部署管理器**&#x200B;角色的成员才能完成此任务。

>[!NOTE]
>
>不允许客户上传DV（域验证）证书。

**添加SSL或DV证书：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台上，选择该程序。

1. 从&#x200B;**概述**&#x200B;页面，导航到&#x200B;**环境**&#x200B;屏幕。

1. 从左侧导航面板的&#x200B;**服务**&#x200B;下，单击&#x200B;**SSL证书**。 如果您看不到下图所示的左侧导航面板，则可能需要单击左上角的汉堡图标。

   ![添加SSL证书](/help/implementing/cloud-manager/assets/ssl/ssl-cert-add.png)

1. 在页面的右上角附近，单击&#x200B;**添加SSL证书**。

1. 在&#x200B;**添加SSL证书**&#x200B;对话框中，根据您的特定用例，执行以下操作之一：

   | 用例 | 步骤 |
   | --- | --- |
   | **添加Adobe托管证书(DV)** | **添加Adobe托管证书(DV)：**<br> a。选择证书类型&#x200B;**托管(DV)** Adobe。<br>![添加DV证书](/help/implementing/cloud-manager/assets/ssl/add-dv-certificate.png)<br>b。在&#x200B;**选择域**&#x200B;下拉列表中，选择要与DV证书关联的一个或多个域。<br>没有域可供选择？ 如果是这样，这意味着您必须添加自定义域。 请参阅[添加自定义域](#add-custom-domain)。 添加完自定义域名后，请返回到本主题并再次从步骤1开始。<br>天。继续执行步骤7。 |
   | **添加客户管理的证书(OV/EV)** | **要添加客户管理的证书(OV/EV)：**<br> a。选择证书类型&#x200B;**客户托管(OV/EV)**。<br>b。在&#x200B;**证书名称**&#x200B;字段中，输入证书的名称。 此字段仅供参考，可以是任何有助于您轻松引用证书的名称。<br>c。在&#x200B;**证书**、**私钥**&#x200B;和&#x200B;**证书链**&#x200B;字段中，将所需值粘贴到各自的字段中。<br>![添加SSL证书对话框](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)<br>显示值中检测到的任何错误。 在保存证书之前，必须解决所有错误。 请参阅[证书错误](#certificate-errors)，了解有关常见错误疑难解答的更多信息。<br>天。继续执行步骤7。 |

<!--
    **Add an SSL certificate:**
    1. Select the certificate type **Customer managed (OV/EV)**.
    1. In **Certificate name** field, enter a name for your certificate. This field is for informational purposes only and can be any name that helps you reference your certificate easily.
    1. In the **Certificate**, **Private key**, and **Certificate chain** fields, paste the required values into their respective fields.

        ![Add SSL certificate dialog box](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)
  
    Any detected errors in values are displayed. Before you can save your certificate, you must address all errors. See [Certificate errors](#certificate-errors) to learn more about troubleshooting common errors.

    **Add a DV certificate:**
    1. Select the certificate type **Adobe managed (DV)**.

        ![Adding a DC certificate](/help/implementing/cloud-manager/assets/ssl/add-dv-certificate.png)

    1. In the **Select domains** drop-down list, select one or more domains that you want associated with the DV certificate.

        No domains to select? If so, it means that you must add a custom domain. See [Add a custom domain](#add-custom-domain). When you are finished, resume the steps from the beginning again. -->

1. 在对话框的右下角，点击&#x200B;**保存**。

   证书成功颁发后，将显示一个绿色复选标记，如上图所示

   ![颁发的DV证书](assets/issued-dv-certificate.png)

### 添加自定义域 {#add-custom-domain}

在添加Adobe生成并管理的域验证(DV)证书之前，必须先添加自定义域。 此操作过程与[自定义域名简介](/help/implementing/cloud-manager/custom-domain-names/introduction.md)和[添加自定义域名](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)中详述的过程几乎相同。 但是，此功能现在略有扩展，如下所述。

1. 添加自定义域名时，在&#x200B;**验证域**&#x200B;对话框中，选择&#x200B;**Adobe托管证书**。

   ![选择Adobe托管](assets/verify-domain-dialog.png)

1. 在&#x200B;**验证域**&#x200B;对话框中，将CNAME验证记录添加到您的DNS。

   ![添加CNAME条目](assets/verify-domain-dialog-adobe-managed.png)

1. 创建域后，单击域列表中的省略号按钮，然后选择&#x200B;**验证**&#x200B;以验证域。

   ![验证域](assets/verify-domain.png)

1. 继续执行任务[添加DV证书](#adding-an-ssl-certificate)。

### 证书错误疑难解答 {#certificate-errors}

如果证书安装不正确或不符合Cloud Manager的要求，则可能会出现某些错误。

+++

* **正确的证书顺序**

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

+++

+++

* **删除客户端证书**

  添加证书时，如果收到类似于以下内容的错误：

  ```text
  The Subject of an intermediate certificate must match the issuer in the previous certificate. The SKI of an intermediate certificate must match the AKI of the previous certificate.
  ```

  您可能已将客户端证书包含在证书链中。 请确保该链不包含客户端证书，然后重试。

+++

+++

* **证书策略**

  如果您看到以下错误，请检查证书的策略。

  ```text
  Certificate policy must conform with EV or OV, and not DV policy.
  ```

  嵌入的OID值通常标识证书策略。 将证书输出到文本并搜索OID将显示证书的策略。

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

+++

+++

* **证书有效日期**

  Cloud Manager 希望 SSL 证书自当前日期起至少 90 天有效。检查证书链的有效性。

+++

## 后续步骤 {#next-steps}

您现在已为项目添加了一个有效的SSL证书。 此步骤通常是第一个设置自定义域名的步骤。

* 要设置自定义域名，请参阅[添加自定义域名](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)。
* 要了解如何在Cloud Manager中更新和管理SSL证书，请参阅[管理SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)。
