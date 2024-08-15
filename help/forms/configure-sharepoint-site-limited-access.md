---
Title: How to configure a SharePoint Site with limited access using authorization scope?
Description: Learn how to configure SharePoint Site with limited access using the authorization scope.
keywords: 如何配置具有有限访问权限的SharePoint站点？，配置具有有限访问权限的SharePoint，使用授权范围限制SharePoint站点的访问权限。
feature: Adaptive Forms, Core Components
role: User, Developer
source-git-commit: 85cef99dc7a8d762d12fd6e1c9bc2aeb3f8c1312
workflow-type: tm+mt
source-wordcount: '817'
ht-degree: 16%

---


<span class="preview">该功能在早期采用者计划下可用。 您可以使用官方电子邮件 ID 写信给 aem-forms-ea@adobe.com，加入早期采用者计划并申请使用该功能。</span>

# 使用授权范围配置具有有限访问权限的 SharePoint 网站

受限或受限访问的目的是通过允许管理员控制用户对特定SharePoint站点或一组SharePoint站点的访问来增强安全管理。 当您需要授予用户或组访问特定网站的权限而不允许他们查看任何其他不允许的SharePoint网站时，权限级别非常有用。

## 使用有限访问权限配置SharePoint站点的优势

提供对SharePoint站点的有限访问权限的优势：

* **增强的安全性**：通过限制访问，您可以确保只有授权人员才能查看或处理敏感信息，从而降低未经授权的访问风险。

* **最低权限原则**：它为用户提供了执行其工作功能所需的最低访问级别（或权限）。 这样可最大限度地减少每个用户暴露于网络敏感部分的风险，从而防止潜在的内部威胁。

* **数据保护**：限制访问有助于保护关键数据不被泄露。 它确保只有需要查看数据的用户才能访问数据，这对于遵守数据保护法规至关重要。

* **防止意外数据丢失**：如果能够修改内容的人变少，重要数据被意外删除或更改的可能性就会大大降低。

* **受控数据流**：它有助于控制组织内外的信息流，确保数据不会落入坏人之手。

## 使用授权范围以受限访问权限配置SharePoint

请按照以下步骤使用授权范围配置具有有限访问权限的SharePoint站点：

1. [创建应用程序，使用 ](#create-an-application-with-the-limited-permission-in-the-azure-portal)
1. [在AEM实例中设置授权范围](#set-the-authorization-scope-at-aem-instance)

### 在Azure门户中创建具有有限权限的应用程序

在Microsoft图形API的[Microsoft Azure门户](https://portal.azure.com/#home)中创建具有`Sites.Selected`权限范围的应用程序。

![SharePoint选定的站点](/help/forms/assets/sharepoint-selected-site.png)

有关如何检索`OAuth URL`的`Client ID`、`Client Secret`和`Tenant ID`的信息，请参阅[Microsoft®文档](https://learn.microsoft.com/en-us/graph/auth-register-app-v2)。
* 在 Microsoft® Azure 门户中，将重定向 URI 添加为 `https://[author-instance]/libs/cq/sharepoint/content/configurations/wizard.html`。将 `[author-instance]` 替换为创作实例 URL。
* 在Microsoft的Graph API中添加`offline_access`和`Sites.Selected`权限范围，以提供对站点的受限制访问。
* 对于OAuth URL： `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`。 将 `<tenant-id>` 替换为 Microsoft® Azure 门户中应用程序的 `tenant-id`。

要使用`Sites.Selected` API权限，需要在Azure门户中注册的应用程序，该应用程序具有为SharePoint Online Sites设置的相应权限。 这种设置可确保应用程序拥有在定义的范围内与SharePoint站点交互所需的授权，从而提供所需的有限访问。

请参阅[博客文章 — 开发使用Sites的应用程序。有关开发使用SharePoint Online Sites `Sites.Selected`权限的应用程序的说明，请参阅SPO Sites的选定权限](https://techcommunity.microsoft.com/t5/microsoft-sharepoint-blog/develop-applications-that-use-sites-selected-permissions-for-spo/ba-p/3790476)。

### 在AEM实例中设置授权范围

要提供对Microsoft SharePoint站点的有限访问，必须正确设置授权范围。 要设置授权范围并将AEM Forms连接到您的Microsoft® SharePoint存储，请执行以下操作：

1. 转到您的&#x200B;**AEM Forms创作**&#x200B;实例> **[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Microsoft®SharePoint]**。
1. 选择&#x200B;**[!UICONTROL Microsoft® SharePoint]**&#x200B;后，您将被重定向到&#x200B;**[!UICONTROL SharePoint浏览器]**。
1. 选择&#x200B;**配置容器**。配置存储在选定的配置容器中。
1. 从下拉列表中单击&#x200B;**[!UICONTROL 创建]** > **[!UICONTROL SharePoint文档库]**。 这将显示 SharePoint 配置向导。

   ![SharePoint站点有限站点访问](/help/forms/assets/sharepoint-doc-library-limited-scopes.png)

1. 指定&#x200B;**[!UICONTROL 标题]**、**[!UICONTROL 客户端ID]**&#x200B;和&#x200B;**[!UICONTROL 客户端密钥]**。 有关如何检索客户端ID和客户端密钥的信息，请参阅[Microsoft®文档](https://learn.microsoft.com/en-us/graph/auth-register-app-v2)。

1. 使用OAuth URL作为`https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`。 将 `<tenant-id>` 替换为 Microsoft® Azure 门户中应用程序的 `tenant-id`。

   >[!NOTE]
   >
   > **客户端密码**&#x200B;字段是必填还是可选字段取决于 Azure Active Directory 应用程序配置。如果应用程序配置为使用客户端密码，则必须提供客户端密码。

1. 在`Authorization Scope`字段中添加`offline_access Sites.Selected`。 当您在`Authorization Scope`文本框字段中添加`offline_access Sites.Selected`范围时，`SharePoint Site ID`文本框将出现在屏幕上。

1. 指定SharePoint站点ID。 要了解如何检索SharePoint站点ID，请参阅[额外字节](#extra-bytes)部分。

1. 单击&#x200B;**[!UICONTROL 检查站点连接]**。 连接成功后，将显示`Connection Successful`消息。

1. 现在，选择&#x200B;**SharePoint站点** > **文档库** > **SharePoint文件夹**&#x200B;以保存数据。

   >[!NOTE]
   >
   >* 默认情况下，`forms-ootb-storage-adaptive-forms-submission`存在于选定的SharePoint站点中。
   >* 通过单击&#x200B;**创建文件夹**，将文件夹创建为`forms-ootb-storage-adaptive-forms-submission`(如果选定SharePoint站点的`Documents`库中尚不存在)。

现在，您可以在自适应表单](/help/forms/configure-submit-action-sharepoint.md#use-sharepoint-document-library-configuration-in-an-adaptive-form-use-sharepoint-configuartion-in-af)中将此[SharePoint Sites配置用于提交操作。

## 额外字节

要检索`SharePoint Site ID`的值：
1. 转到[Microsoft Graph Explorer API](https://developer.microsoft.com/en-us/graph/graph-explorer)。
1. 在左窗格的`SharePoint Sites` API下，单击`Search for a SharePoint site by keyword`。
1. 将占位符`contoso`替换为SharePoint网站的实际名称，以获取相应的网站ID。

   ![SharePoint文档库ID](/help/forms/assets/sharepoint-site-id.png)

单击`Run Query`按钮后，屏幕上将显示站点ID。