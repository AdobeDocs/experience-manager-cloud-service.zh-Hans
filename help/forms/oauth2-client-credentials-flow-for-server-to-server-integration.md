---
title: 如何使用OAuth 2.0客户端凭据流将Salesforce与AEM Forms集成？
seo-title: Salesforce integration with AEM Forms using OAuth 2.0 client credential flow
description: 使用OAuth 2.0客户端凭据流将Salesforce集成与AEM Forms集成的步骤
seo-description: Steps to integrate Salesforce integration with AEM Forms using OAuth 2.0 client credential flow
Keywords: Integration of Salesforce using OAuth 2.0 client credential flow, salesforce integration with oauth2 using client credential flow, salesforce and client credential integration
source-git-commit: 2c0a816b61cfc17a83b24b28be1f317e9681c6c5
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 5%

---


# 使用OAuth 2.0客户端凭据流集成Salesforce应用程序 {#configure-salesforce-with-ouath-2.0-client-credential}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/oauth2-client-credentials-flow-for-server-to-server-integration.html) |
| AEM as a Cloud Service | 本文 |

您可以使用OAuth 2.0客户端凭据将AEM Forms与Salesforce应用程序集成。 OAuth 2.0客户端凭据是一种无需用户参与的直接通信的标准和安全方法。

![在AEM Forms和Salesforce应用程序之间设置通信时的工作流](/help/forms/assets/salesforce-workflow.png)
AEM Forms交换在Salesforce连接的应用程序中定义的客户端凭据（使用者密钥和使用者密钥）以获取访问令牌。

使用OAuth 2.0客户端凭据对授权代码流身份验证进行身份验证具有多种好处：

* OAuth 2.0客户端凭据身份验证允许每个用户有五个以上的连接。
* AEM数据源配置将继续用于AEM用户的停用、访问更改和密码更新。

## 前提条件 {#prerequisites}

在Salesforce应用程序和AEM环境之间设置通信之前：

* 创建 [使用OAuth 2.0客户端凭据流连接的Salesforce应用程序](https://help.salesforce.com/s/articleView?id=sf.connected_app_client_credentials_setup.htm&amp;type=5) 和贵组织的仅API用户，并获取应用程序的使用者密钥和使用者密钥。

* 确保您的Swagger文件已正确配置为与组织的API匹配。 或者，您可以选择 [创建Swagger文件](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/forms/integrate-with-salesforce/describe-rest-api.html) 从头开始，为在AEM环境中使用而定制。


## 使用OAuth 2.0客户端凭据流配置Salesforce应用程序 {#steps-to-create-aem-datasource-configuration}

要使用OAuth 2.0客户端凭据身份验证设置将Salesforce应用程序与自适应表单集成，请执行以下步骤：

1. 登录到  创作实例。
1. 转到 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL 数据源]**.
1. 选择配置文件夹。
1. 单击 **[!UICONTROL 创建]** 和 **[!UICONTROL 创建数据源配置]** 显示。
1. 指定 **[!UICONTROL 标题]** 并选择 **[!UICONTROL 服务类型]** 作为 **[!UICONTROL RESTful服务]**.
1. 单击&#x200B;**[!UICONTROL 下一步]**。
1. 选择 **[!UICONTROL Swagger源]** 作为 **[!UICONTROL 文件].**

   >[!NOTE]
   >
   > 选择swagger文件后，将自动填充Scheme 、 Host name和Base路径。

1. 通过单击从本地计算机上传创建的swagger文件 **[!UICONTROL 浏览]**.
1. 选择 **[!UICONTROL 身份验证类型]** 作为 **[!UICONTROL OAuth 2.0]** 和 **[!UICONTROL 身份验证设置]** 面板。
1. 选择 **[!UICONTROL 授权类型]** 作为 **[!UICONTROL 客户端凭据]**.
1. 指定 **[!UICONTROL 客户端ID]** 和 **[!UICONTROL 客户端密码]** 从Salesforce连接的应用程序中获取。
1. 指定 **[!UICONTROL 访问令牌URL]** 格式
   `https://[MyDomainName].my.salesforce.com/services/oauth2/token`。

   >[!NOTE]
   >
   > 每个组织都有其自己的特定域名。

1. 单击 **[!UICONTROL 测试连接]**.
1. 如果连接成功，请单击 **[!UICONTROL 创建]** 按钮。

现在，您可以 [创建表单数据模型](/help/forms/create-form-data-models.md) 将配置的数据源与您的自适应表单集成。
