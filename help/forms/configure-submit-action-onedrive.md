---
Title: How to submit data from an Adaptive Form to Microsoft® OneDrive?
Description: Explore the streamlined process of connecting AEM Forms with Microsoft® OneDrive using the Submit to OneDrive Submit Action. Learn the step-by-step guide to configure OneDrive and set up submission actions for efficient data storage and retrieval
keywords: AEM Forms OneDrive集成，连接到Microsoft OneDrive，使用AEM Forms设置OneDrive配置
feature: Adaptive Forms, Core Components
source-git-commit: 20458e710502e445cf5c8f582a1d183bdac75c8d
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 68%

---


# 将自适应表单提交到 Microsoft® OneDrive

**[!UICONTROL 提交到 OneDrive]**&#x200B;提交操作将自适应表单与 Microsoft® OneDrive 连接起来。您可以将表单数据、文件、附件或记录文档提交到连接的Microsoft® OneDrive存储。

AEMas a Cloud Service提供了多种现成的提交操作来处理表单提交。 有关这些选项的更多信息，请参阅 [自适应表单提交操作](/help/forms/configure-submit-actions-core-components.md)  文章。

## 优点

AEM Forms与Microsoft® OneDrive无缝集成的一些优势包括：

* OneDrive的跨设备访问功能可确保存储的表单数据在不同平台上随时可用。 用户可以从台式机、笔记本电脑、平板电脑和移动设备访问提交的数据、附件和文档，从而提高可访问性和灵活性。
* OneDrive与AEM Forms的集成提供了可靠且可扩展的解决方案，可实现高效的数据存储。 所有自适应表单提交（如文件、附件和记录文档）都可以方便地保存在OneDrive中，确保数据的组织性和可访问性。

## 将OneDrive连接到自适应表单

>[!VIDEO](https://video.tv.adobe.com/v/3424864/connect-aem-adaptive-form-to-onedrive/?quality=12&learn=on)

为AEM Forms提交配置OneDrive，请执行以下步骤：

1. [创建 OneDrive 配置](#create-a-onedrive-configuration-create-onedrive-configuration)：它将 AEM Forms 连接到 Microsoft® OneDrive 存储。
2. [在自适应表单中使用提交到OneDrive提交操作](#use-onedrive-configuration-in-an-adaptive-form-use-onedrive-configuartion-in-af)：它将您的自适应表单连接到配置的Microsoft® OneDrive。

### 创建 OneDrive 配置 {#create-onedrice-configuration}

要将 AEM Forms 连接到 Microsoft® OneDrive 存储，请执行以下操作：

1. 转到 **AEM Forms 创作**&#x200B;实例 > **[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Microsoft® OneDrive]**。
1. 选定 **[!UICONTROL Microsoft® OneDrive]** 后，您将重定向到 **[!UICONTROL OneDrive 浏览器]**。
1. 选择&#x200B;**配置容器**。配置存储在选定的配置容器中。
1. 单击&#x200B;**[!UICONTROL 创建]**。这将显示 OneDrive 配置向导。

   ![OneDrive 配置屏幕](/help/forms/assets/onedrive-configuration.png)

1. 指定&#x200B;**[!UICONTROL 标题]**、**[!UICONTROL 客户端 ID]**、**[!UICONTROL 客户端密码]**&#x200B;和 **[!UICONTROL OAuth URL]**。有关如何检索 OAuth URL 的客户端 ID、客户端密码、租户 ID 的信息，请参阅 [Microsoft® 文档](https://learn.microsoft.com/en-us/graph/auth-register-app-v2)。
   * 您可以从 Microsoft® Azure 门户检索应用程序的`Client ID` 和`Client Secret`。
   * 在 Microsoft® Azure 门户中，将重定向 URI 添加为 `https://[author-instance]/libs/cq/onedrive/content/configurations/wizard.html`。将 `[author-instance]` 替换为创作实例 URL。
   * 添加 API 权限 `offline_access` 和 `Files.ReadWrite.All` 以提供读/写权限。
   * 使用 OAuth URL：`https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`。将 `<tenant-id>` 替换为 Microsoft® Azure 门户中应用程序的 `tenant-id`。

   >[!NOTE]
   >
   > **客户端密码**&#x200B;字段是必填还是可选字段取决于 Azure Active Directory 应用程序配置。如果应用程序配置为使用客户端密码，则必须提供客户端密码。

1. 单击&#x200B;**[!UICONTROL 连接]**。连接成功后，将显示`Connection Successful`消息。

1. 现在，选择 **[!UICONTROL OneDrive 容器]** > **[OneDrive 文件夹]**&#x200B;以保存数据。

   >[!NOTE]
   >
   >* 默认情况下，`forms-ootb-storage-adaptive-forms-submission` 位于 OneDrive 容器中。
   > * 通过单击&#x200B;**创建文件夹**&#x200B;来创建一个 `forms-ootb-storage-adaptive-forms-submission` 形式的文件夹（如果该文件夹不存在）。

现在，您可以在自适应表单中将此 OneDrive 存储配置用于提交操作。

### 在自适应表单中使用 OneDrive 配置 {#use-onedrive-configuartion-in-af}

您可以在自适应表单中使用创建的 OneDrive 存储配置，将数据或生成的记录文档保存在 OneDrive 文件夹中。在以下情况下，执行以下步骤可在自适应表单中使用 OneDrive 存储配置：
1. 创建[自适应表单](/help/forms/creating-adaptive-form.md)。

   >[!NOTE]
   >
   > * 为自适应表单选择相同的[!UICONTROL 配置容器]，您已在其中创建 OneDrive 存储。
   > * 如果未选择[!UICONTROL 配置容器]，则全局[!UICONTROL 存储配置]文件夹将显示在提交操作属性窗口中。

1. 选择&#x200B;**[!UICONTROL 提交到 OneDrive]** 作为&#x200B;**提交操作**。
   ![OneDrive GIF](/help/forms/assets/onedrive-video.gif)
1. 选择要用于保存数据的&#x200B;**[!UICONTROL 存储配置]**。
1. 单击&#x200B;**[!UICONTROL 保存]**&#x200B;以保存提交设置。

在提交表单时，数据将保存在指定的 Microsoft® OneDrive 存储中。
用于保存数据的文件夹结构是 `/folder_name/form_name/year/month/date/submission_id/data`。

## 相关文章

{{af-submit-action}}