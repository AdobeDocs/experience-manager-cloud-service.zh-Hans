---
title: 添加 SSL 证书
description: 了解如何使用Cloud Manager的自助服务工具添加您自己的SSL证书或Adobe托管的DV（域验证）证书。
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: fa99656e0dd02bb97965e8629d5fa657fbae9424
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 4%

---


# 添加SSL证书 {#add-ssl-cert}

了解如何使用Cloud添加您自己的SSL证书或Adobe托管的DV（域验证）证书

>[!NOTE]
>
>如果您使用客户管理的(OV/EV) SSL证书和客户管理的CDN提供程序，则可以跳过添加SSL证书，并在准备就绪后直接转到[添加CDN配置](/help/implementing/cloud-manager/cdn-configurations/add-cdn-config.md)。

配置证书可能需要几天时间。 因此，Adobe建议在任何截止日期或上线日期之前提前配置您自己的证书，以避免延迟。

要了解如何在Cloud Manager中更新和管理SSL证书，请参阅[管理SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)。

如果在添加或管理证书时遇到问题，请参阅[SSL证书错误疑难解答](/help/implementing/cloud-manager/managing-ssl-certifications/troubleshoot-ssl-cert.md)。


## 先决条件 {#prerequisites}

* 用户必须是&#x200B;**业务负责人**&#x200B;或&#x200B;**部署管理器**&#x200B;角色的成员才能添加SSL证书。
* 如果您正在安装自己的证书，请参阅[管理SSL证书简介](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md#requirements)中的&#x200B;**证书要求**。

## 选择要添加的SSL证书 {#which-ssl-to-add}

在AEM Cloud Manager中[添加自定义域名](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)后，下一步取决于您是选择使用Adobe托管(DV) SSL证书（推荐）还是客户托管(OV/EV) SSL证书。

* **对于Adobe托管(DV) SSL证书：**
   * 添加自定义域并在Cloud Manager中验证后，将完成域验证过程。
   * 现在，您必须[添加托管(DV) SSL证书](#add-adobe-managed-ssl-cert)Adobe。
添加到Cloud Manager后，请等待Adobe代表您颁发并安装DV SSL证书。
   * 当证书处于活动状态时，您的自定义域即可使用。

* **对于客户管理的(OV/EV) SSL证书：**

   * 从证书颁发机构获取OV/EV SSL证书。 有关更多详细信息，请查看客户管理的OV/EV SSL证书的[要求](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md#requirements)。
   * 获取证书后，[在Cloud Manager中添加您的客户托管(OV/EV) SSL证书的](#add-customer-manage-ssl-cert)详细信息。
   * 添加后，自定义域名将标记为已验证，并应用SSL证书。

无论属于哪种情况，在验证并安装证书后，都可以在环境中安全使用自定义域。 请务必[在Cloud Manager界面中定期检查域状态](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)，以确认一切都按预期运行。

另请参阅[SSL证书简介](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md)。

## 添加Adobe托管(DV) SSL证书 {#add-adobe-managed-ssl-cert}

需要帮助您选择在您的域中使用Adobe托管的SSL证书（推荐）还是客户托管的SSL证书？ 请参阅[选择要添加的SSL证书](#which-ssl-to-add)

**添加Adobe托管(DV) SSL证书：**

1. 在[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)登录Cloud Manager并选择适当的程序。
1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台上，选择该程序。
1. 在页面的左上角，单击![显示菜单图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg)以显示侧菜单。

1. 在&#x200B;**服务**&#x200B;标题下，单击![锁定已关闭图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) **SSL证书**。

   ![添加SSL证书](/help/implementing/cloud-manager/assets/ssl/ssl-cert-add.png)

1. 在“SSL证书”页面的右上角附近，单击&#x200B;**添加SSL证书**。

1. 在&#x200B;**添加SSL证书**&#x200B;对话框中，根据[您的特定用例](#which-ssl-to-add)，选择&#x200B;**托管Adobe(DV)**。

   ![添加DV证书](/help/implementing/cloud-manager/assets/ssl/add-dv-certificate.png)

1. 在&#x200B;**证书名称**&#x200B;字段中，输入要与DV SSL证书关联的名称。

1. 在&#x200B;**选择域**&#x200B;下拉列表中，选择要与DV SSL证书关联的一个或多个验证域。
   * 没有域可供选择？ 如果是这样，您必须首先添加自定义域名，并确保在添加SSL证书之前验证域名。
   * 请参阅[添加自定义域名](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)。
   * 添加完自定义域名后，请返回到本主题并再次从步骤1开始。

1. 在对话框的右下角，点击&#x200B;**保存**。

   成功颁发SSL证书后，**SSL证书**&#x200B;表中将显示绿色的有效复选标记。

您现在已为项目添加了一个有效的Adobe托管DV SSL证书。 此步骤通常是第一个设置自定义域名的步骤。

您现在已准备好添加[CDN配置](/help/implementing/cloud-manager/cdn-configurations/add-cdn-config.md)。

## 添加客户管理的(OV/ED) SSL证书 {#add-customer-managed-ssl-cert}

需要帮助您选择在您的域中使用Adobe托管的SSL证书（推荐）还是客户托管的SSL证书？ 请参阅[选择要添加的SSL证书](#which-ssl-to-add)

**要添加客户管理的(OV/EV) SSL证书：**

1. 在[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)登录Cloud Manager并选择适当的程序。
1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台上，选择该程序。
1. 在页面的左上角，单击![显示菜单图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg)以显示侧菜单。
1. 在&#x200B;**服务**&#x200B;标题下，单击![锁定已关闭图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) **SSL证书**。

   ![添加SSL证书](/help/implementing/cloud-manager/assets/ssl/ssl-cert-add.png)

1. 在“SSL证书”页面的右上角附近，单击&#x200B;**添加SSL证书**。

1. 在&#x200B;**添加SSL证书**&#x200B;对话框中，根据[您的特定用例](#which-ssl-to-add)，选择&#x200B;**客户管理的(OV/EV)**。

1. 在&#x200B;**证书名称**字段中，输入证书的名称。
此字段仅供参考，可以是任何有助于您轻松引用SSL证书的名称。

1. 在&#x200B;**证书**、**私钥**&#x200B;和&#x200B;**证书链**字段中，复制OV或EV SSL证书中的必需值，并将其粘贴到对话框中各自的字段中。
将显示在值中检测到的任何错误。 在保存证书之前，必须解决所有错误。 请参阅[证书错误](#certificate-errors)，了解有关常见错误疑难解答的更多信息。

   ![添加SSL证书对话框](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)|

1. 在对话框的右下角，点击&#x200B;**保存**。

   >[!NOTE]
   >
   >* 如果您在[添加自定义域名](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)时选择了&#x200B;**客户管理的证书**，则在&#x200B;***添加并保存客户管理的(OV/EV) SSL证书后***&#x200B;验证域。 另请参阅[检查自定义域名](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#how-to)的状态。

   成功颁发SSL证书后，**SSL证书**&#x200B;表中将显示绿色验证复选标记。

您现在已为项目添加了一个有效的SSL证书。 此步骤通常是第一个设置自定义域名的步骤。

您现在已准备好添加[CDN配置](/help/implementing/cloud-manager/cdn-configurations/add-cdn-config.md)。























<!--
## Add an SSL certificate {#add-ssl-cert}

1. Log into Cloud Manager at [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) and select the appropriate program.
1. On the **[My Programs](/help/implementing/cloud-manager/navigation.md#my-programs)** console, select the program.
1. In the upper-left corner of the page, click ![Show menu icon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) to reveal the side menu. 
1. Under the **Services** heading, click ![Lock closed icon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) **SSL Certificates**. 

   ![Adding an SSL certificate](/help/implementing/cloud-manager/assets/ssl/ssl-cert-add.png)

1. Near the upper-right corner of the SSL Certificates page, click **Add SSL Certificate**.

1. In the **Add SSL certificate** dialog box, based on [your particular use case](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md), do one of the following:

    | | Use case | Steps |
    | --- | --- | --- |
    | 1 | **Add an Adobe managed (DV) certificate** | **To add an Adobe managed (DV) SSL certificate:**<br>a. In the **Add SSL Certificate** dialog box, select the certificate type **Adobe managed (DV)**.<br>![Add a DV certificate](/help/implementing/cloud-manager/assets/ssl/add-dv-certificate.png)<br>b. In the **Certificate name** field, enter a name you want associated with the certificate.<br>c. In the **Select domains** drop-down list, select one or more domains that you want associated with the DV SSL certificate.<br>No domains to select? If so, it means that you must first add a custom domain name and ensure it is verified before you can add an SSL certificate. See [Add a custom domain name](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). When you are finished adding a custom domain name, return to this topic and begin at step 1 again.<br>d. Continue to step 7. |
    | 2 | **Add a customer managed (OV/EV) certificate** | **To add a customer managed (OV/EV) SSL certificate:**<br>a. In the **Add SSL Certificate** dialog box, select the certificate type **Customer managed (OV/EV)**.<br>b. In the **Certificate name** field, enter a name for your certificate. This field is for informational purposes only and can be any name that helps you reference your SSL certificate easily.<br>c. In the **Certificate**, **Private key**, and **Certificate chain** fields, paste the required values into their respective fields.<br>![Add SSL certificate dialog box](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)<br>Any detected errors in values are displayed. Before you can save your certificate, you must address all errors. See [Certificate Errors](#certificate-errors) to learn more about troubleshooting common errors.<br>d. Continue to step 7. | 

1. In the lower-right corner of the dialog box, click **Save**.

    >[!NOTE]
    >
    >* If you selected **Adobe managed certificate** while [adding a custom domain name](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md), the domain is verified with the added certificate when the custom domain is added. 
    >
    >* If you selected **Customer managed certificate** while [adding a custom domain name](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md), the domain is verified ***after*** the customer managed (OV/EV) SSL certificate is added and saved. See also [Check the status of a custom domain name](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#how-to).

    After the SSL certificate is successfully issued, it is displayed with a green verified check mark in the **SSL Certificates** table. 

    You now have added a working SSL certificate for your project. This step is often the first to set up a custom domain name. 
    

* To learn about updating and managing your SSL certificates in Cloud Manager, see [Manage SSL certificates](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md).

* If you are having issues adding or managing your certificates, see [Troubleshoot SSL certificate errors](/help/implementing/cloud-manager/managing-ssl-certifications/troubleshoot-ssl-cert.md). -->
