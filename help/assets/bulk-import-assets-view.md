---
title: 使用资源视图批量导入资源
description: 了解如何使用新的资源 UI（资源视图）批量导入资源。管理员使用它可以将大量资源从数据源导入到 AEM Assets。
exl-id: 10f9d679-7579-4650-9379-bc8287cb2ff1
source-git-commit: 88198e9333a7f706fc99e487d8cde84647fa111f
workflow-type: tm+mt
source-wordcount: '1747'
ht-degree: 56%

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
| AWS | <ul> <li>AWS 区域 </li> <li> AWS 分段 <li> AWS 访问密钥 </li><li> AWS 访问私钥 </li></ul> |
| Google Cloud | <ul> <li>GCP 桶 </li> <li> GCP 服务帐户电子邮件 <li> GCP 服务帐户私钥</li></ul> |
| Dropbox | <ul> <li>Dropbox 客户端 ID （应用程序密钥） </li> <li> Dropbox的客户端密码（应用程序密码）</li></ul> |
| OneDrive | <ul> <li>OneDrive租户ID  </li> <li> OneDrive客户端ID</li><li> OneDrive客户端密码</li></ul> |

除了基于数据源的这些先决条件之外，您还必须了解数据源中可用的源文件夹名称，其中包含需要导入到 AEM Assets 的所有资源。

## 配置Dropbox开发人员应用程序 {#dropbox-developer-application}

在将资源从Dropbox帐户导入到AEM Assets之前，请创建和配置Dropbox开发人员应用程序。

执行以下步骤：

1. 登录 [Dropbox帐户](https://www.dropbox.com/developers) 并单击 **[!UICONTROL 创建应用程序]**.

1. 在 **[!UICONTROL 选择API]** 部分，选择唯一可用的单选按钮。

1. 在 **[!UICONTROL 选择所需的访问类型]** 部分，选择以下选项之一：

   * 选择 **[!UICONTROL 应用程序文件夹]**，如果您需要访问在应用程序中创建的、位于Dropbox帐户中的单个文件夹。

   * 选择 **[!UICONTROL 完整Dropbox]**，以访问Dropbox帐户中的所有文件和文件夹。

1. 指定应用程序的名称，然后单击 **[!UICONTROL 创建应用程序]**.

1. 在 **[!UICONTROL 设置]** 选项卡，将以下内容添加到 **[!UICONTROL 重定向URI]** 部分：

   * https://exc-unifiedcontent.experience.adobe.net

   * https://exc-unifiedcontent.experience-stage.adobe.net （仅对暂存环境有效）

1. 复制值 **[!UICONTROL 应用程序密钥]** 和 **[!UICONTROL 应用程序密钥]** 字段。 在AEM Assets中配置批量导入工具时需要这些值。

1. 在 **[!UICONTROL 权限]** 选项卡中，添加以下权限 **[!UICONTROL 单个范围]** 部分。

   * account_info.read

   * files.metadata.read

   * files.content.read

   * files.content.write

1. 单击 **[!UICONTROL 提交]** 以保存更改。

## 配置OneDrive开发人员应用程序 {#onedrive-developer-application}

在将资产从OneDrive帐户导入AEM Assets之前，请创建和配置OneDrive开发人员应用程序。

执行以下步骤：

1. 登录 [OneDrive帐户](https://portal.azure.com/#view/Microsoft_AAD_RegisteredApps/ApplicationsListBlade) 并单击 **[!UICONTROL 新注册]**.

1. 指定应用程序的名称，选择 **[!UICONTROL 仅此组织目录中的帐户(仅Adobe — 单个租户)]** 从 **[!UICONTROL 支持的帐户类型]**，然后单击 **[!UICONTROL 注册]**. 已成功创建应用程序。

1. 复制应用程序客户端ID和租户ID字段的值。 在AEM Assets中配置批量导入工具时需要这些值。

1. 执行以下步骤以添加证书：
   1. 在应用程序概述页面上，单击 **[!UICONTROL 添加证书或密码]** 然后单击 **[!UICONTROL 新客户端密码]**.
   1. 指定客户端密钥说明和到期时间，然后单击 **[!UICONTROL 添加]**.
   1. 创建客户端密钥后，复制 **[!UICONTROL 值]** 字段（请勿复制机密ID字段）。 在AEM Assets中配置批量导入时需要此变量。

1. 执行以下步骤以添加重定向URI：
   1. 在应用程序概述页面上，单击 **[!UICONTROL 添加重定向URI]** > **[!UICONTROL 添加平台]** > **[!UICONTROL Web]**.
   1. 将以下内容添加到 **[!UICONTROL 重定向URI]** 部分：

      * https://exc-unifiedcontent.experience.adobe.net

      * https://exc-unifiedcontent.experience-stage.adobe.net （仅对暂存环境有效）

      添加第一个URI并单击 **[!UICONTROL 配置]** 以添加它。 您可以通过单击 **[!UICONTROL 添加URI]** 中提供的选项 **[!UICONTROL Web]** 部分，位于 **[!UICONTROL 身份验证]** 页面。

1. 执行以下步骤可为应用程序添加API权限：
   1. 单击 **[!UICONTROL API权限]** 在左窗格中单击 **[!UICONTROL 添加权限]**.
   1. 单击 **[!UICONTROL Microsoft Graph]** > **[!UICONTROL 已委派权限]**. 此 **[!UICONTROL 选择权限]** 部分显示可用的权限。
   1. 选择 `offline_access` 权限来自 `OpenId permissions` 和 `Files.ReadWrite.All` 权限来自 `Files`.
   1. 单击 **[!UICONTROL 添加权限]** 以保存更新。




## 创建批量导入配置 {#create-bulk-import-configuration}

执行以下步骤创建批量导入配置：

1. 请导航到&#x200B;**[!UICONTROL “设置”]**>**[!UICONTROL “批量导入”]**，然后单击&#x200B;**[!UICONTROL “创建导入”。]**
1. 选择数据源。可用选项包括 Azure、AWS、Google Cloud 和 Dropbox。
1. 在&#x200B;**[!UICONTROL “名称”]**&#x200B;字段中指定批量导入配置的名称。
1. 指定数据源特定的凭据，如[“先决条件”](#prerequisites)中所述。
1. 在的数据源中提供包含资产的文件夹的名称 **[!UICONTROL 源文件夹]** 字段。

   >[!NOTE]
   >
   >如果将Dropbox用作数据源，请根据以下规则指定源文件夹路径：
   >* 如果您选择 **完整Dropbox** 创建Dropbox应用程序时，以及包含资源的文件夹 `https://www.dropbox.com/home/bulkimport-assets`，然后指定 `bulkimport-assets` 在 **[!UICONTROL 源文件夹]** 字段。
   >* 如果您选择 **应用程序文件夹** 创建Dropbox应用程序时，以及包含资源的文件夹 `https://www.dropbox.com/home/Apps/BulkImportAppFolderScope/bulkimport-assets`，然后指定 `bulkimport-assets` 在 **[!UICONTROL 源文件夹]** 字段，其中 `BulkImportAppFolderScope` 指应用程序的名称。 `Apps` 在以下时段后自动添加： `home` 这种情况下。

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
