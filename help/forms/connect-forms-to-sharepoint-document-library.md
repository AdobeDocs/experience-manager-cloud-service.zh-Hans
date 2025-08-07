---
Title: How to integrate Adaptive Form to a SharePoint Document Library?
Description: This article explains how to send data from your Adaptive Form to a SharePoint  Document library when you submit the form.
keywords: 如何为自适应表单连接SharePoint文档库、提交到SharePoint、创建SharePoint文档库配置、在自适应表单中使用提交到SharePoint提交操作、AEM Forms数据模型SharePoint文档库、Forms数据模型SharePoint文档库、将Forms数据模型集成到SharePoint文档库
feature: Adaptive Forms, Core Components, Foundation Components, Edge Delivery Services
role: User, Developer
exl-id: a00b4a93-2324-4c2a-824f-49146dc057b0
source-git-commit: dabf8029577c5fb6bb5eebdbf10d77f3d4d95a5d
workflow-type: tm+mt
source-wordcount: '981'
ht-degree: 28%

---

# 将自适应表单连接到Microsoft® SharePoint Document Library {#connect-af-sharepoint-doc-library}

>[!VIDEO](https://video.tv.adobe.com/v/3444368/formautomation-productivitytools-adaptiveforms--sharepointintegration-documentlibrary/?quality=12&learn=on)

<span>此视频仅适用于核心组件。 对于UE/Foundation组件，请参阅文章。</span>


要在自适应表单中使用&#x200B;**[!UICONTROL 提交到SharePoint文档库]**&#x200B;提交操作，请执行以下操作：

1. [创建SharePoint文档库配置](#1-create-a-sharepoint-document-library-configuration)：它将AEM Forms连接到您的Microsoft® Sharepoint存储。
2. [在自适应表单中使用“提交到 SharePoint”提交操作](#2-use-sharepoint-document-library-configuration-in-an-adaptive-form)：它将自适应表单连接到配置的 Microsoft® SharePoint。

## 1.创建SharePoint文档库配置

要将AEM Forms连接到Microsoft®Sharepoint文档库存储，请执行以下操作：

1. 转到您的&#x200B;**AEM Forms作者**&#x200B;实例> **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Microsoft® SharePoint]**。
1. 选择&#x200B;**[!UICONTROL Microsoft® SharePoint]**&#x200B;后，您将被重定向到&#x200B;**[!UICONTROL SharePoint浏览器]**。
1. 选择&#x200B;**配置容器**。配置存储在选定的配置容器中。
1. 从下拉列表中单击&#x200B;**[!UICONTROL 创建]** > **[!UICONTROL SharePoint文档库]**。 这将显示 SharePoint 配置向导。

   ![SharePoint 配置](/help/forms/assets/sharepoint_configuration.png)

1. 指定&#x200B;**[!UICONTROL 标题]**、**[!UICONTROL 客户端 ID]**、**[!UICONTROL 客户端密码]**&#x200B;和 **[!UICONTROL OAuth URL]**。有关如何检索 OAuth URL 的客户端 ID、客户端密码、租户 ID 的信息，请参阅 [Microsoft® 文档](https://learn.microsoft.com/en-us/graph/auth-register-app-v2)。
   * 您可以从 Microsoft® Azure 门户检索应用程序的`Client ID` 和`Client Secret`。
   * 在 Microsoft® Azure 门户中，将重定向 URI 添加为 `https://[author-instance]/libs/cq/sharepoint/content/configurations/wizard.html`。将 `[author-instance]` 替换为创作实例 URL。
   * 添加API权限`offline_access`和`Sites.Manage.All`以提供读/写权限。`Sites.Manage.All`是Microsoft的Graph API中的权限范围，它允许应用程序管理SharePoint Sites的所有方面，例如删除或修改站点。

     >[!NOTE]
     >
     > 您还可以使用SharePoint图形API中的[权限范围](/help/forms/configure-sharepoint-site-limited-access.md)配置具有有限访问权限`Sites.Selected`的Microsoft站点。 `Sites.Selected`是Microsoft的Graph API中的权限范围，它允许对SharePoint站点进行更细粒度和更受限的访问。

   * 使用 OAuth URL：`https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`。将 `<tenant-id>` 替换为 Microsoft® Azure 门户中应用程序的 `tenant-id`。

     >[!NOTE]
     >
     > **客户端密码**&#x200B;字段是必填还是可选字段取决于 Azure Active Directory 应用程序配置。如果应用程序配置为使用客户端密码，则必须提供客户端密码。

1. Microsoft图形API中的`offline_access Sites.Selected`权限范围，允许对SharePoint站点进行更细粒度和更受限的访问。 Microsoft图形API中的`offline_access Sites.Manage.All`权限范围，允许完全访问SharePoint网站。
1. 单击&#x200B;**[!UICONTROL 连接]**。连接成功后，将显示`Connection Successful`消息。

1. 现在，选择&#x200B;**SharePoint站点** > **文档库** > **SharePoint文件夹**&#x200B;以保存数据。

   >[!NOTE]
   >
   >* 默认情况下，`forms-ootb-storage-adaptive-forms-submission`存在于选定的SharePoint站点中。
   >* 通过单击`forms-ootb-storage-adaptive-forms-submission`创建文件夹`Documents`，将文件夹创建为&#x200B;**(如果选定SharePoint站点的**&#x200B;库中尚不存在)。

现在，您可以在自适应表单中将此SharePoint Sites配置用于提交操作。

### 2.在自适应表单中使用SharePoint文档库配置

您可以在自适应表单中使用创建的SharePoint文档库配置，将数据或生成的记录文档保存到SharePoint文件夹中。

>[!NOTE]
>
> * 为自适应表单选择相同的[!UICONTROL 配置容器]，您已在其中创建了SharePoint文档库存储。
> * 如果未选择[!UICONTROL 配置容器]，则全局[!UICONTROL 存储配置]文件夹将显示在提交操作属性窗口中。

>[!BEGINTABS]

>[!TAB 基础组件]

执行以下步骤以在基于基础组件的自适应表单中使用SharePoint文档库存储配置，如下所示：

1. 打开自适应表单进行编辑，然后导航到自适应表单容器属性的&#x200B;**[!UICONTROL 提交]**&#x200B;部分。
1. 从&#x200B;**[!UICONTROL 提交操作]**&#x200B;下拉列表中，选择&#x200B;**提交操作**&#x200B;作为&#x200B;**[!UICONTROL 提交到SharePoint]**。
   ![Sharepoint GIF](/help/forms/assets/submit-to-sharepoint-fc.png){width=50%}
1. 选择要用于保存数据的&#x200B;**[!UICONTROL 存储配置]**。
1. 单击&#x200B;**[!UICONTROL 保存]**&#x200B;以保存提交设置。

>[!NOTE]
>
> * 提交表单时，数据将保存在指定的Microsoft® Sharepoint文档库存储中。 用于保存数据的文件夹结构是 `/folder_name/form_name/year/month/date/submission_id/data`。
> * 附件也存储在`/folder_name/form_name/year/month/date/submission_id/data`目录中。 但是，如果选择&#x200B;**保存具有原始名称的附件**，则附件会使用其原始文件名存储在文件夹中。

>[!TAB 核心组件]

执行以下步骤，在基于核心组件的自适应表单中使用SharePoint文档库存储配置，如下所示：

1. 打开内容浏览器，然后选择自适应表单的&#x200B;**[!UICONTROL 指南容器]**&#x200B;组件。
1. 单击指南容器属性![指南属性](/help/forms/assets/configure-icon.svg)图标。这将打开“自适应表单容器”对话框。
1. 单击&#x200B;**[!UICONTROL 提交]**&#x200B;选项卡。
1. 从&#x200B;**[!UICONTROL 提交操作]**&#x200B;下拉列表中，选择&#x200B;**提交操作**&#x200B;作为&#x200B;**[!UICONTROL 提交到SharePoint]**。
   ![Sharepoint GIF](/help/forms/assets/sharedrive-video.gif)
1. 选择要用于保存数据的&#x200B;**[!UICONTROL 存储配置]**。
1. 单击&#x200B;**[!UICONTROL 保存]**&#x200B;以保存提交设置。

>[!NOTE]
>
> * 提交表单时，数据将保存在指定的Microsoft® Sharepoint文档库存储中。 用于保存数据的文件夹结构是 `/folder_name/form_name/year/month/date/submission_id/data`。
> * 附件也存储在`/folder_name/form_name/year/month/date/submission_id/data`目录中。 但是，如果选择&#x200B;**保存具有原始名称的附件**，则附件会使用其原始文件名存储在文件夹中。

>[!TAB 通用编辑器]

执行以下步骤，使用在Universal Editor中创作的自适应表单中的SharePoint文档库存储配置，如下所示：

1. 打开自适应表单进行编辑。
1. 单击编辑器上的&#x200B;**编辑表单属性**扩展。
出现**表单属性**&#x200B;对话框。

   >[!NOTE]
   >
   > * 如果您在通用编辑器界面中未看到&#x200B;**编辑表单属性**&#x200B;图标，请在Extension Manager中启用&#x200B;**编辑表单属性**&#x200B;扩展。
   > * 请参阅[Extension Manager功能亮点](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)一文，了解如何在通用编辑器中启用或禁用扩展。

1. 单击&#x200B;**提交**&#x200B;选项卡，然后选择&#x200B;**[!UICONTROL 提交到SharePoint]**提交操作。
   ![Sharepoint GIF](/help/forms/assets/submit-to-sharepoint-ue.png)
1. 选择要用于保存数据的&#x200B;**[!UICONTROL 存储配置]**。
1. 单击&#x200B;**[!UICONTROL 保存并关闭]**&#x200B;以保存提交设置。

>[!NOTE]
>
> * 提交表单时，数据将保存在指定的Microsoft® Sharepoint文档库存储中。 用于保存数据的文件夹结构是 `/folder_name/form_name/year/month/date/submission_id/data`。
> * 附件也存储在`/folder_name/form_name/year/month/date/submission_id/data`目录中。 但是，如果选择&#x200B;**保存具有原始名称的附件**，则附件会使用其原始文件名存储在文件夹中。

>[!ENDTABS]

## 相关文章

{{af-submit-action}}
