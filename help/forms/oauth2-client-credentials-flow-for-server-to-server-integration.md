---
title: 如何使用 OAuth 2.0 客户端凭据流将 Salesforce 与 AEM Forms 集成？
seo-title: Salesforce integration with AEM Forms using OAuth 2.0 client credential flow
description: 使用 OAuth 2.0 客户端凭据流将 Salesforce 与 AEM Forms 集成的步骤
seo-description: Steps to integrate Salesforce integration with AEM Forms using OAuth 2.0 client credential flow
Keywords: Integration of Salesforce using OAuth 2.0 client credential flow, salesforce integration with oauth2 using client credential flow, salesforce and client credential integration
source-git-commit: 2c0a816b61cfc17a83b24b28be1f317e9681c6c5
workflow-type: ht
source-wordcount: '426'
ht-degree: 100%

---


# 使用 OAuth 2.0 客户端凭据流集成 Salesforce 应用程序 {#configure-salesforce-with-ouath-2.0-client-credential}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/oauth2-client-credentials-flow-for-server-to-server-integration.html) |
| AEM as a Cloud Service | 本文 |

您可以使用 OAuth 2.0 客户端凭据将 AEM Forms 与 Salesforce 应用程序集成。OAuth 2.0 客户端凭据是一种标准且安全的直接通信方法，无需用户参与。

![设置 AEM Forms 和 Salesforce 应用程序之间的通信时的工作流](/help/forms/assets/salesforce-workflow.png)
AEM Forms 交换在 Salesforce 连接的应用程序中定义的客户端凭据（消费方密钥和消费方密码）以获取访问令牌。

与授权代码流身份验证相比，使用 OAuth 2.0 客户端凭据进行身份验证可获得多个好处：

* OAuth 2.0 客户端凭据身份验证允许每个用户拥有超过五个连接。
* AEM 数据源配置继续处理 AEM 用户的停用、访问权限更改、密码更新。

## 前提条件 {#prerequisites}

在设置 Salesforce 应用程序和 AEM 环境之间的通信之前：

* 为您的组织创建[采用 OAuth 2.0 客户端凭据流的 Salesforce 连接的应用程序](https://help.salesforce.com/s/articleView?id=sf.connected_app_client_credentials_setup.htm&amp;type=5)和仅 API 用户，并获取应用程序的消费方密钥和消费方密码。

* 确保已适当配置 Swagger 文件以匹配您组织的 API。或者，您可以选择从头[创建一个 Swagger 文件](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/forms/integrate-with-salesforce/describe-rest-api.html)，该文件专门用于您的 AEM 环境。


## 使用 OAuth 2.0 客户端凭据流配置 Salesforce 应用程序 {#steps-to-create-aem-datasource-configuration}

要使用 OAuth 2.0 客户端凭据身份验证设置将 Salesforce 应用程序与自适应表单集成，请执行以下步骤：

1. 登录您的创作实例。
1. 转到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL 数据源]**。
1. 选择配置文件夹。
1. 单击&#x200B;**[!UICONTROL 创建]**，**[!UICONTROL 创建数据源配置]**&#x200B;随即出现。
1. 指定&#x200B;**[!UICONTROL 标题]**&#x200B;并选择&#x200B;**[!UICONTROL 服务类型]**&#x200B;为 **[!UICONTROL RESTful 服务]**。
1. 单击&#x200B;**[!UICONTROL 下一步]**。
1. 选择 **[!UICONTROL Swagger 源]**&#x200B;作为&#x200B;**[!UICONTROL 文件]。**

   >[!NOTE]
   >
   > 选择 swagger 文件后，将自动填充方案、主机名和基本路径。

1. 通过单击&#x200B;**[!UICONTROL 浏览]**&#x200B;从本地计算机上传创建的 swagger 文件。
1. 选择&#x200B;**[!UICONTROL 身份验证类型]**&#x200B;为 **[!UICONTROL OAuth 2.0]**，**[!UICONTROL 身份验证设置]**&#x200B;面板随即出现。
1. 选择&#x200B;**[!UICONTROL 授权类型]**&#x200B;为&#x200B;**[!UICONTROL 客户端凭据]**。
1. 指定从 Salesforce 连接的应用程序获取的&#x200B;**[!UICONTROL 客户端 ID]**&#x200B;和&#x200B;**[!UICONTROL 客户端密码]**。
1. 用以下格式指定&#x200B;**[!UICONTROL 访问令牌 URL]**
   `https://[MyDomainName].my.salesforce.com/services/oauth2/token`。

   >[!NOTE]
   >
   > 每个组织都有自己特定的域名。

1. 单击&#x200B;**[!UICONTROL 测试连接]**。
1. 如果连接成功，请单击&#x200B;**[!UICONTROL 创建]**&#x200B;按钮。

现在，您可以[创建表单数据模型](/help/forms/create-form-data-models.md)以将配置的数据源与自适应表单集成。
