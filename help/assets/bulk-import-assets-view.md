---
title: 使用资源视图批量导入资源
description: 了解如何使用新的资源 UI（资源视图）批量导入资源。管理员使用它可以将大量资源从数据源导入到 AEM Assets。
exl-id: 10f9d679-7579-4650-9379-bc8287cb2ff1
source-git-commit: 88198e9333a7f706fc99e487d8cde84647fa111f
workflow-type: tm+mt
source-wordcount: '1747'
ht-degree: 87%

---

# 使用资源视图批量导入资源  {#bulk-import-assets-view}

AEM Assets 视图中的“批量导入”功能使管理员能够将大量资源从数据源导入到 AEM Assets。管理员不再需要将单个资源或文件夹上传到 AEM Assets。

>[!NOTE]
>
>资源视图批量导入器与管理视图批量导入器使用的后端相同。但是，它提供更多可从其导入的数据源和更简化的用户体验。

您可以从以下数据源导入资源：

* Azure
* AWS
* Google Cloud
* Dropbox
* OneDrive

## 前提条件 {#prerequisites}

| 数据源 | 前提条件 |
|-----|------|
| Azure | <ul> <li>Azure 存储帐户 </li> <li> Azure Blob 容器 <li> 基于身份验证模式的 Azure 访问密钥或 SAS 令牌 </li></ul> |
| AWS | <ul> <li>AWS 区域 </li> <li> AWS 分段 <li> AWS 访问密钥 </li><li> AWS 访问机密 </li></ul> |
| Google Cloud | <ul> <li>GCP 桶 </li> <li> GCP 服务帐户电子邮件 <li> GCP 服务帐户私钥</li></ul> |
| Dropbox | <ul> <li>Dropbox 客户端 ID （应用程序密钥） </li> <li> Dropbox的客户端密码（应用程序密码）</li></ul> |
| OneDrive | <ul> <li>OneDrive 租户 ID  </li> <li> OneDrive 客户端 ID</li><li> OneDrive 客户端机密</li></ul> |

除了基于数据源的这些先决条件之外，您还必须了解数据源中可用的源文件夹名称，其中包含需要导入到 AEM Assets 的所有资源。

## 配置 Dropbox 开发人员应用程序 {#dropbox-developer-application}

在将资源从 Dropbox 帐户导入到 AEM Assets 之前，请先创建并配置 Dropbox 开发人员应用程序。

执行以下步骤：

1. 登录您的 [Dropbox 帐户](https://www.dropbox.com/developers)，然后单击&#x200B;**[!UICONTROL 创建应用程序]**。

1. 在&#x200B;**[!UICONTROL 选择 API]** 部分中，选择唯一可用的单选按钮。

1. 在&#x200B;**[!UICONTROL 选择您需要的访问权限的类型]**&#x200B;部分中，选择以下选项之一：

   * 如果您需要访问您的应用程序内在 Dropbox 帐户中创建的单个文件夹，请选择&#x200B;**[!UICONTROL 应用程序文件夹]**。

   * 如果您需要访问您 Dropbox 帐户中的所有文件和文件夹，请选择&#x200B;**[!UICONTROL 整个 Dropbox]**。

1. 为您的应用程序指定一个名称，然后单击&#x200B;**[!UICONTROL 创建应用程序]**。

1. 在您的应用程序的&#x200B;**[!UICONTROL 设置]**&#x200B;选项卡中，将以下内容添加到&#x200B;**[!UICONTROL 重定向 URI]** 部分：

   * https://exc-unifiedcontent.experience.adobe.net

   * https://exc-unifiedcontent.experience-stage.adobe.net（仅对暂存环境有效）

1. 复制&#x200B;**[!UICONTROL 应用程序密钥]**&#x200B;和&#x200B;**[!UICONTROL 应用程序机密]**&#x200B;字段的值。在 AEM Assets 中配置批量导入工具时需要这些值。

1. 在&#x200B;**[!UICONTROL 权限]**&#x200B;选项卡上的&#x200B;**[!UICONTROL 单独作用域]**&#x200B;部分中添加以下权限。

   * account_info.read

   * files.metadata.read

   * files.content.read

   * files.content.write

1. 单击&#x200B;**[!UICONTROL 提交]**&#x200B;以保存更改。

## 配置 OneDrive 开发人员应用程序 {#onedrive-developer-application}

在将资源从 OneDrive 帐户导入到 AEM Assets 之前，请先创建并配置 OneDrive 开发人员应用程序。

执行以下步骤：

1. 登录到您的 [OneDrive 帐户](https://portal.azure.com/#view/Microsoft_AAD_RegisteredApps/ApplicationsListBlade)，然后单击&#x200B;**[!UICONTROL 新注册]**。

1. 指定应用程序的名称，从&#x200B;**[!UICONTROL 支持的帐户类型]**&#x200B;中选择&#x200B;**[!UICONTROL 仅在此组织目录中的帐户（仅 Adobe - 单一租户）]**，然后单击&#x200B;**[!UICONTROL 注册]**。随后即成功创建该应用程序。

1. 复制应用程序客户端 ID 和租户 ID 字段的值。在 AEM Assets 中配置批量导入工具时需要这些值。

1. 执行以下步骤以添加证书：
   1. 在应用程序概述页面上，单击&#x200B;**[!UICONTROL 添加证书或机密]**，然后单击&#x200B;**[!UICONTROL 新建客户端机密]**。
   1. 指定客户端机密的描述和到期日期，然后单击&#x200B;**[!UICONTROL 添加]**。
   1. 创建客户端机密后，复制&#x200B;**[!UICONTROL 值]**&#x200B;字段（请勿复制机密 ID 字段）。在 AEM Assets 中配置批量导入时需要它。

1. 执行以下步骤以添加重定向 URI：
   1. 在应用程序概览页面上，单击&#x200B;**[!UICONTROL 添加重定向 URI]** > **[!UICONTROL 添加平台]** > **[!UICONTROL Web]**。
   1. 将以下内容添加到&#x200B;**[!UICONTROL 重定向 URI]** 部分：

      * https://exc-unifiedcontent.experience.adobe.net

      * https://exc-unifiedcontent.experience-stage.adobe.net（仅对暂存环境有效）

      添加第一个 URI，然后单击&#x200B;**[!UICONTROL 配置]**&#x200B;以添加它。通过单击可在&#x200B;**[!UICONTROL 身份验证]**&#x200B;页面上的 **[!UICONTROL Web]** 部分中找到的&#x200B;**[!UICONTROL 添加 URI]** 选项可添加更多。

1. 执行以下步骤以添加应用程序的 API 权限：
   1. 在左窗格中单击 **[!UICONTROL API 权限]**，然后单击&#x200B;**[!UICONTROL 添加权限]**。
   1. 单击 **[!UICONTROL Microsoft Graph]** > **[!UICONTROL 委派的权限]**。随后&#x200B;**[!UICONTROL 选择权限]**&#x200B;部分显示可用的权限。
   1. 从 `OpenId permissions` 选择 `offline_access` 权限，从 `Files` 选择 `Files.ReadWrite.All` 权限。
   1. 单击&#x200B;**[!UICONTROL 添加权限]**&#x200B;以保存更新。




## 创建批量导入配置 {#create-bulk-import-configuration}

执行以下步骤创建批量导入配置：

1. 请导航到&#x200B;**[!UICONTROL “设置”]**>**[!UICONTROL “批量导入”]**，然后单击&#x200B;**[!UICONTROL “创建导入”。]**
1. 选择数据源。可用选项包括 Azure、AWS、Google Cloud 和 Dropbox。
1. 在&#x200B;**[!UICONTROL “名称”]**&#x200B;字段中指定批量导入配置的名称。
1. 指定数据源特定的凭据，如[“先决条件”](#prerequisites)中所述。
1. 在的数据源中提供包含资产的文件夹的名称 **[!UICONTROL 源文件夹]** 字段。

   >[!NOTE]
   >
   >如果您使用 Dropbox 作为数据源，请根据以下规则指定源文件夹路径：
   >* 如果在创建 Dropbox 应用程序时选择&#x200B;**整个 Dropbox**，并且包含资源的文件夹存在于 `https://www.dropbox.com/home/bulkimport-assets`，则在&#x200B;**[!UICONTROL 源文件夹]**&#x200B;字段中指定 `bulkimport-assets`。
   >* 如果在创建 Dropbox 应用程序时选择&#x200B;**应用程序文件夹**，并且包含资源的文件夹存在于 `https://www.dropbox.com/home/Apps/BulkImportAppFolderScope/bulkimport-assets`，则在&#x200B;**[!UICONTROL 源文件夹]**&#x200B;字段中指定 `bulkimport-assets`，其中 `BulkImportAppFolderScope` 表示应用程序的名称。这种情况下，自动在 `home` 之后添加 `Apps`。

1. （可选）选择&#x200B;**[!UICONTROL “导入后删除源文件”]**&#x200B;选项，以在文件导入到 Experience Manager Assets 后，从源数据存储中删除原始文件。
1. 选择&#x200B;**[!UICONTROL “导入模式”。]**&#x200B;选择&#x200B;**[!UICONTROL “跳过”]**、**[!UICONTROL “代替”]**，或者&#x200B;**[!UICONTROL 创建版本。]**跳过模式是默认模式，在该模式下，如果资源已经存在，则摄取器会跳过导入该资源。
   ![导入源详细信息](/help/assets/assets/bulk-import-source-details.png)

1. （可选）在“元数据文件”字段中指定以 CSV 格式提供的要导入的元数据文件，然后单击&#x200B;**[!UICONTROL “下一个”]**&#x200B;导航到&#x200B;**[!UICONTROL 位置和筛选器。]**
1. 要使用&#x200B;**[!UICONTROL 资源目标文件夹]**&#x200B;字段在 DAM 中定义要导入资源的位置，请指定路径。例如：`/content/dam/imported_assets`。
1. （可选）在&#x200B;**[!UICONTROL “选择筛选器”]**&#x200B;部分，在&#x200B;**[!UICONTROL 按最小尺寸过滤]**&#x200B;字段中提供资源的最小文件大小（MB），以将其包括在摄取过程中。
1. （可选）在&#x200B;**[!UICONTROL 按最大尺寸过滤]**&#x200B;字段中，以 MB 为单位提供资源的最大文件大小，以将其包括在摄取过程中。
1. （可选）使用&#x200B;**[!UICONTROL 包括 MIME 类型]**&#x200B;字段选择要包含在摄取过程中的 MIME 类型。您可以在此字段中选择多种 MIME 类型。如果您未定义值，则所有 MIME 类型都会包含在摄取过程中。

1. （可选）使用&#x200B;**[!UICONTROL 排除 MIME 类型]**&#x200B;字段选择要排除在摄取过程中的 MIME 类型。您可以在此字段中选择多种 MIME 类型。如果您未定义值，则所有 MIME 类型都会包含在摄取过程中。

   ![批量导入过滤器](assets/bulk-import-location.png)

1. 单击&#x200B;**[!UICONTROL “下一个”。]**&#x200B;选择&#x200B;**[!UICONTROL “保存和运行导入”]**&#x200B;保存配置并运行批量导入。选择&#x200B;**[!UICONTROL “保存导入”]**，暂时保存配置，以便稍后运行。

   ![执行批量导入](assets/bulk-import-run.png)

1. 单击&#x200B;**[!UICONTROL “保存”]**，执行所选选项。

### 批量导入期间处理文件名 {#filename-handling-bulkimport-assets-view}

当您批量导入资源或文件夹时，[!DNL Experience Manager Assets] 导入在导入源中存在的内容的完整结构。[!DNL Experience Manager] 遵循针对关资源和文件夹名称中特殊字符的内置规则，因此需要净化这些文件名。对于文件夹名称和资源名称，用户定义的标题保持不变并存储在 `jcr:title` 中。

批量导入期间，[!DNL Experience Manager] 查找现有文件夹以避免重复导入资源和文件夹，还验证在发生导入的父文件夹中应用的净化规则。如果在父文件夹中应用了净化规则，则将相同的规则应用于导入源。对于新导入，应用以下净化规则以管理资源的文件名和文件夹名称。

有关在批量导入期间不允许使用的名称、处理资源名称和处理文件夹名称的详细信息，请参阅[批量导入期间在管理视图中处理文件名](add-assets.md##filename-handling-bulkimport)。

## 查看现有的批量导入配置 {#view-import-configuration}

如果您在创建配置后选择保存配置，则该配置会显示在&#x200B;**[!UICONTROL “已保存的导入”]**&#x200B;选项卡中。

![保存批量导入配置](assets/bulk-import-save.png)

如果您选择保存并运行导入，则导入配置会显示在&#x200B;**[!UICONTROL “已执行的导入”]**&#x200B;选项卡中。

![保存批量导入配置](assets/bulk-import-executed.png)

计划执行的导入会显示在&#x200B;**[!UICONTROL “已计划的导入”]**&#x200B;选项卡中。

## 编辑批量导入配置 {#edit-import-configuration}

要编辑配置详细信息，请单击与配置名称对应的更多选项(...)，然后单击 **[!UICONTROL 编辑]**. 执行编辑操作时无法编辑配置的标题和导入数据源。您可以使用“已执行”、“已计划”或“已保存的导入”选项卡编辑配置。

![编辑批量导入配置](assets/bulk-import-edit.png)

## 计划一次性或定期导入 {#schedule-imports}

要计划一次性或定期批量导入，请执行以下步骤：

1. 单击与中可用的配置名称对应的更多选项(...) **[!UICONTROL 执行的导入]** 或 **[!UICONTROL 保存的导入]** 选项卡，然后单击 **[!UICONTROL 计划]**. 您也可以通过导航到&#x200B;**[!UICONTROL ”已计划的导入“]**&#x200B;选项卡，并单击&#x200B;**[!UICONTROL ”计划“]**&#x200B;来重新计划当前计划的导入。

1. 设置一次性摄取或安排每小时、每天或每周的摄取计划。单击&#x200B;**[!UICONTROL “提交”。]**

   ![计划批量导入配置](assets/bulk-import-schedule.png)

## 执行导入健康检查 {#import-health-check}

要验证与数据源的连接，请单击与配置名称对应的更多选项(...)，然后单击 **[!UICONTROL Check]**. 如果连接成功，Experience Manager Assets 将会显示以下消息：

![批量导入健康检查](assets/bulk-import-health-check.png)

## 在执行导入之前执行练习 {#dry-run-bulk-import}

单击与配置名称对应的更多选项(...)，然后单击 **[!UICONTROL 练习]** 以调用批量导入作业的测试运行。 Experience Manager Assets 显示有关“批量导入”作业的以下详细信息：

![批量导入健康检查](assets/bulk-import-dry-run.png)

## 运行批量导入 {#run-bulk-import}

如果在创建配置时保存了导入，则可以导航到保存的导入选项卡，单击与配置对应的更多选项(...)，然后单击 **[!UICONTROL 运行]**.

同样，如果需要执行已执行的导入，请导航到已执行的导入选项卡，单击与配置名称对应的更多选项(...)，然后单击 **[!UICONTROL 运行]**.

## 停止或计划正在进行的导入 {#schedule-stop-ongoing-report}

您可以使用导入期间显示在“批量导入”主页上的批量导入状态对话框来计划或停&#x200B;&#x200B;止正在进行的批量导入。

![正在进行的导入](assets/bulk-import-progress.png)

您还可以通过单击&#x200B;**[!UICONTROL “查看资源”]**&#x200B;来查看已导入目标文件夹中的资源。


## 删除批量导入配置 {#delete-bulk-import-configuration}

单击与中存在的配置名称对应的更多选项(...) **[!UICONTROL 执行的导入]**， **[!UICONTROL 计划的导入]**，或 **[!UICONTROL 保存的导入]** 选项卡，然后单击 **[!UICONTROL 删除]** 以删除批量导入配置。

## 执行批量导入后导航到资源 {#view-assets-after-bulk-import}

要查看运行批量导入作业后导入资产的Assets目标位置，请单击与配置名称对应的更多选项(...)，然后单击 **[!UICONTROL 查看资源]**.
