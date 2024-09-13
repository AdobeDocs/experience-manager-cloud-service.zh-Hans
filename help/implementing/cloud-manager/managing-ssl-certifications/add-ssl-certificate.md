---
title: 添加SSL证书
description: 了解如何使用Cloud Manager的自助服务工具添加您自己的SSL证书或DV（域验证）证书。
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: d2f05915c0bf0af073db7f070b83f13aeae55252
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 9%

---


# 添加SSL证书 {#add-ssl-cert}

了解如何使用Cloud Manager的自助服务工具添加客户管理的SSL证书或Adobe生成和管理的DV（域验证）证书。

另请参阅[SSL证书错误疑难解答](/help/implementing/cloud-manager/managing-ssl-certifications/troubleshoot-ssl-cert.md)。

## 添加SSL证书 {#adding-an-ssl-certificate}

提供证书可能需要几天时间。因此，Adobe建议在任何截止日期或上线日期之前提前配置证书。

请查看[管理SSL证书简介](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md#requirements)中的&#x200B;**证书要求**，以确保AEM as a Cloud Service支持您要添加的证书。

用户必须是&#x200B;**业务负责人**&#x200B;或&#x200B;**部署管理器**&#x200B;角色的成员才能完成此任务。

>[!NOTE]
>
>不允许客户上传DV（域验证）证书。

**添加SSL证书：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台上，选择该程序。

1. 从&#x200B;**概述**&#x200B;页面，导航到&#x200B;**环境**&#x200B;屏幕。

1. 从左侧导航面板的&#x200B;**服务**&#x200B;下，单击&#x200B;**SSL证书**。 如果您看不到下图所示的左侧导航面板，则可能需要单击左上角的汉堡图标。

   ![添加SSL证书](/help/implementing/cloud-manager/assets/ssl/ssl-cert-add.png)

1. 在页面的右上角附近，单击&#x200B;**添加SSL证书**。

1. 在&#x200B;**添加SSL证书**&#x200B;对话框中，根据[您的特定用例](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)，执行以下操作之一：

   | | 用例 | 步骤 |
   | --- | --- | --- |
   | 1 | **添加Adobe托管证书(DV)** | **添加Adobe托管证书(DV)：**<br> a。选择证书类型&#x200B;**托管(DV)** Adobe。<br>![添加DV证书](/help/implementing/cloud-manager/assets/ssl/add-dv-certificate.png)<br>b。在&#x200B;**选择域**&#x200B;下拉列表中，选择要与DV证书关联的一个或多个域。<br>没有域可供选择？ 如果是这样，这意味着您必须添加自定义域。 请参阅[添加自定义域名](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)。 添加完自定义域名后，请返回到本主题并再次从步骤1开始。<br>天。继续执行步骤7。 |
   | 2 | **添加客户管理的证书(OV/EV)** | **要添加客户管理的证书(OV/EV)：**<br> a。选择证书类型&#x200B;**客户托管(OV/EV)**。<br>b。在&#x200B;**证书名称**&#x200B;字段中，输入证书的名称。 此字段仅供参考，可以是任何有助于您轻松引用证书的名称。<br>c。在&#x200B;**证书**、**私钥**&#x200B;和&#x200B;**证书链**&#x200B;字段中，将所需值粘贴到各自的字段中。<br>![添加SSL证书对话框](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)<br>显示值中检测到的任何错误。 在保存证书之前，必须解决所有错误。 请参阅[证书错误](#certificate-errors)，了解有关常见错误疑难解答的更多信息。<br>天。继续执行步骤7。 |

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

   成功颁发证书后，**SSL证书**&#x200B;表中将显示绿色复选标记。

您现在已为项目添加了一个有效的SSL证书。 此步骤通常是第一个设置自定义域名的步骤。

* 要设置自定义域名，请参阅[添加自定义域名](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)。
* 要了解如何在Cloud Manager中更新和管理SSL证书，请参阅[管理SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)。

<!--
### Add a custom domain {#add-custom-domain}

Before you can add an Adobe generated and managed Domain Validated (DV) certificate, you must first add a custom domain. The process for doing so is nearly the same as detailed in [Introduction to custom domain names](/help/implementing/cloud-manager/custom-domain-names/introduction.md) and [Add a custom domain name](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). However, that functionality is now slightly expanded, as described below.

1. When adding a custom domain name, in the **Verify domain** dialog box, select an **Adobe managed certificate**.

    ![Choose Adobe-managed](assets/verify-domain-dialog.png)

1. In the **Verify domain** dialog box, add a CNAME verification record to your DNS.

    ![Add CNAME entry](assets/verify-domain-dialog-adobe-managed.png)

1. After the domain is created, click the ellipsis button in the list of domains and select **Verify** to verify the domain.

    ![Verify domain](assets/verify-domain.png) 

1. Resume the task [Add a DV certificate](#adding-an-ssl-certificate). -->


