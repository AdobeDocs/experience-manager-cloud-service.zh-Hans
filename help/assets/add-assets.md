---
title: 将您的数字资产添加到 [!DNL Adobe Experience Manager]。
description: 将您的数字资产作为 [!DNL Cloud Service]添加到 [!DNL Adobe Experience Manager] 。
feature: Asset Ingestion, Asset Management, Asset Processing, Upload
role: User, Admin
exl-id: 0e624245-f52e-4082-be21-13cc29869b64
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '3162'
ht-degree: 9%

---

# 将数字资产作为[!DNL Cloud Service]添加到[!DNL Adobe Experience Manager][!DNL Assets] {#add-assets-to-experience-manager}

| [搜索最佳实践](/help/assets/search-best-practices.md) | [元数据最佳实践](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | 具有OpenAPI功能的[Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets开发人员文档](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

[!DNL Adobe Experience Manager Assets]接受来自多个来源的多种数字资源。 它存储二进制文件和创建的演绎版，可以使用各种工作流和[!DNL Adobe Sensei]服务进行资产处理，允许跨多个表面通过多个渠道进行分发。

[!DNL Adobe Experience Manager]使用富元数据、智能标记、演绎版和其他数字资产管理(DAM)服务丰富了已上传数字文件的二进制内容。 您可以从本地文件夹或网络驱动器将各种类型的文件（如图像、文档和原始图像文件）上载到[!DNL Experience Manager Assets]。

除了最常用的浏览器上载之外，还存在将资产添加到[!DNL Experience Manager]存储库的其他方法。 这些其他方法包括桌面客户端(如AdobeAsset Link或[!DNL Experience Manager]桌面应用程序)、上传和客户将创建的引入脚本，以及添加为[!DNL Experience Manager]扩展的自动引入集成。

虽然您可以上传和管理[!DNL Experience Manager]中的任何二进制文件，但最常用的文件格式支持其他服务，如元数据提取或预览/演绎版生成。 有关详细信息，请参阅[支持的文件格式](file-format-support.md)。

您还可以选择对上传的资源执行其他处理。 可以在上传资源的文件夹上配置多个资源处理配置文件，以添加特定的元数据、演绎版或图像处理服务。 请参阅上传时[处理资源](#process-when-uploaded)。

[!DNL Assets]提供以下上载方法。 Adobe建议您在使用上传选项之前了解其用例和适用性。

| 上载方法 | 何时使用？ | 主要角色 |
|---------------------|----------------|-----------------|
| [Assets控制台用户界面](#upload-assets) | 偶尔上传、轻松按压和拖动、查找器上传。 请勿使用上传许多资源。 | 所有用户 |
| [上传API](#upload-using-apis) | 用于上传期间的动态决策。 | 开发人员 |
| [[!DNL Experience Manager] 桌面应用程序](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) | 低流量资产摄取，但不适用于迁移。 | 管理员、营销人员 |
| [[!DNL Adobe Asset Link]](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html) | 当创意人员和营销人员从支持的[!DNL Creative Cloud]桌面应用程序中处理资产时非常有用。 | 创意、营销人员 |
| [资源批量引入器](#asset-bulk-ingestor) | 建议进行大规模迁移和偶尔进行批量引入。 仅适用于支持的数据存储。 | 管理员、开发人员 |

## 上传资产 {#upload-assets}

<!-- #ENGCHECK do we support pausing? I couldn't get pause to show with 1.5GB upload.... If not, this should be removed#

   You can pause the uploading of large assets (greater than 500 MB) and resume it later from the same page. Select the **[!UICONTROL Pause]** icon beside progress bar that appears when an upload starts.

   The size above which an asset is considered a large asset is configurable. For example, you can configure the system to consider assets above 1000 MB (instead of 500 MB) as large assets. In this case, **[!UICONTROL Pause]** appears on the progress bar when assets of size greater than 1000 MB are uploaded.

   The [!UICONTROL Pause] option does not show if a file greater than 1000 MB is uploaded with a file less than 1000 MB. However, if you cancel the less than 1000 MB file upload, the **[!UICONTROL Pause]** option appears.

   To modify the size limit, configure the `chunkUploadMinFileSize` property of the `fileupload` node in the CRX repository.

   When you click the **[!UICONTROL Pause]** icon, it toggles to a **[!UICONTROL Play]** icon. To resume uploading, click **[!UICONTROL Play]** option.
-->

<!-- #ENGCHECK do we support pausing? I couldn't get pause to show with 1.5GB upload.... If not, this should be removed#
   The ability to resume uploading is especially helpful in low-bandwidth scenarios and network glitches, where it takes a long time to upload a large asset. You can pause the upload operation and continue later when the situation improves. When you resume, uploading starts from the point where you paused it.
-->

<!-- #ENGCHECK assuming this is not relevant? remove after confirming#
   During the upload operation, [!DNL Experience Manager] saves the portions of the asset being uploaded as chunks of data in the CRX repository. When the upload completes, [!DNL Experience Manager] consolidates these chunks into a single block of data in the repository.

   To configure the cleanup task for the unfinished chunk upload jobs, go to `https://[aem_server]:[port]/system/console/configMgr/org.apache.sling.servlets.post.impl.helper.ChunkCleanUpTask`.
-->

要上传文件（或多个文件），您可以在桌面上选择它们，然后在用户界面（Web浏览器）上将其拖到目标文件夹中。 或者，您可以从用户界面启动上传。

>[!IMPORTANT]
>
>您上传到Experience Manager的Assets如果文件名超过100个字符，则在Dynamic Media中使用这些字符时，其名称会缩短。
>
>文件名中的前100个字符按原样使用；其余任何字符都替换为字母数字字符串。 此重命名方法可确保在Dynamic Media中使用资产时具有唯一的名称。 它还旨在适应Dynamic Media中允许的最大资源文件名长度。


1. 在[!DNL Assets]用户界面中，导航到要添加数字资产的位置。
1. 要上传资源，请执行以下操作之一：

   * 在工具栏上，单击&#x200B;**[!UICONTROL 创建]** > **[!UICONTROL 文件]**。 如果需要，可以在呈现的对话框中重命名文件。
   * 在支持HTML5的浏览器中，将资源直接拖动到[!DNL Assets]用户界面上。 不显示重命名文件的对话框。

   ![create_menu](assets/create_menu.png)

   要选择多个文件，请选择`Ctrl`或`Command`键，然后在文件选取器对话框中选择资源。 使用iPad时，一次只能选择一个文件。

1. 要取消正在进行的上载，请单击进度条旁边的关闭(`X`)。 取消上传操作时，[!DNL Assets]将删除部分上传的资产部分。
如果在上载文件之前取消上载操作，[!DNL Assets]将停止上载当前文件并刷新内容。 但是，不会删除已上载的文件。

1. [!DNL Assets]中的上传进度对话框显示已成功上传的文件数和无法上传的文件数。
此外，[!DNL Assets]用户界面会显示您上传的最新资源或您首先创建的文件夹。

>[!NOTE]
>
>要上传嵌套文件夹层次结构，请参阅[批量上传资产](#bulk-upload)。

<!-- #ENGCHECK I'm assuming this is no longer relevant.... If yes, this should be removed#

### Serial uploads {#serialuploads}

Uploading numerous assets in bulk consumes significant I/O resources, which may adversely impact the performance of [!DNL Assets]. In particular, if you have a slow internet connection, the time to upload drastically increases due to a spike in disk I/O. Moreover, your web browser may introduce additional restrictions to the number of POST requests [!DNL Assets] can handle for concurrent asset uploads. As a result, the upload operation fails or terminate prematurely. In other words, [!DNL Assets] may miss some files while ingesting a bunch of files or altogether fail to ingest any file.

To overcome this situation, [!DNL Assets] ingests one asset at a time (serial upload) during a bulk upload operation, instead of the concurrently ingesting all the assets.

Serial uploading of assets is enabled by default. To disable the feature and allow concurrent uploading, overlay the `fileupload` node in CRX-DE and set the value of the `parallelUploads` property to `true`.

### Streamed uploads {#streamed-uploads}

If you upload many assets to [!DNL Experience Manager], the I/O requests to server increase drastically, which reduces the upload efficiency and can even cause some upload task to time out. [!DNL Assets] supports streamed uploading of assets. Streamed uploading reduces the disk I/O during the upload operation by avoiding asset storage in a temporary folder on the server before copying it to the repository. Instead, the data is transferred directly to the repository. This way, the time to upload large assets and the possibility of timeouts is reduced. Streamed upload is enabled by default in [!DNL Assets].

>[!NOTE]
>
>Streaming upload is disabled for [!DNL Experience Manager] running on JEE server with servlet-api version lower than 3.1.
-->

### 处理现有资源的上传 {#handling-upload-existing-file}

您可以上传与现有资产具有相同路径（相同名称和相同位置）的资产。 但是，会显示一个警告对话框，其中包含下列选项：

* 替换现有资源：如果替换现有资源，则将删除资源的元数据以及您之前对现有资源所做的任何修改（例如，注释和裁切）。

  >[!NOTE]
  >
  >如果资产已锁定或签出，则用于替换资产的选项将不可用。

* 创建其他版本：在存储库中创建现有资源的新版本。 您可以在[!UICONTROL 时间线]中查看这两个版本，如有必要，还可以还原到以前的现有版本。
* 保留两者：如果选择保留两个资源，则新资源将重命名。

若要在[!DNL Assets]中保留重复的资产，请单击&#x200B;**[!UICONTROL 保留]**。 要删除您上传的重复资源，请单击&#x200B;**[!UICONTROL 删除]**。

### 文件名处理和禁止使用的字符 {#filename-handling}

[!DNL Experience Manager Assets]阻止您上传其文件名中包含禁止使用的字符的资产。 如果您尝试上载文件名中包含不允许的字符或更多字符的资产，[!DNL Assets]将显示一条警告消息并停止上载，直到您删除这些字符或使用允许名称上载为止。

为了适合您所在组织的特定文件命名约定，可以使用[!UICONTROL 上传Assets]对话框为上传的文件指定长名称。 不支持以下（以空格分隔的）字符：

* 资源名称的字符无效：`* / : [ \\ ] | # % { } ? &`
* 资产文件夹名称的字符无效： `* / : [ \\ ] | # % { } ? \" . ^ ; + & \t`

## 批量上传资产 {#bulk-upload}

批量资源引入器可以高效地处理许多资源。 但是，大规模摄取并不仅仅是一种广泛的文件转储或临时迁移。 要使大规模引入成为满足您的业务目的并且高效的有意义项目，请规划迁移并策划资源组织。 所有引入都不同，因此，这里考虑的因素不是概括，而是存储库的细微构成和业务需求。 以下是计划和执行批量摄取的一些总体建议：

* 策划资源：删除DAM中不需要的资源。 考虑删除未使用、过时或重复的资源。 此类内务管理可减少传输的数据和引入的资产，从而加快引入速度。
* 组织资产：考虑按某种逻辑顺序组织内容，例如按文件大小、文件格式、用例或优先级。 通常，大型复杂文件需要更多的处理。 您还可以考虑使用文件大小过滤选项（如下所述）单独摄取大文件。
* 交错摄取：考虑将摄取分组为多个批量摄取项目。 q可让您更快地看到内容，并根据需要更新引入。 例如，您可以在非高峰时间摄取处理密集型资产，或逐渐摄取多个块中的资产。 但是，您可以一次性摄取不需要太多处理的更小、更简单的资产。

要上传更多文件，请使用以下方法之一。 另请参阅[用例和方法](#upload-methods-comparison)

* [资源上传API](developer-reference-material-apis.md#asset-upload)：如有必要，请使用自定义上传脚本或使用API添加其他资源处理（例如，翻译元数据或重命名文件）的工具。
* [[!DNL Experience Manager] 桌面应用程序](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)：对于从本地文件系统上传资产的创意专业人员和营销人员非常有用。 使用它可上载本地可用的嵌套文件夹。
* [批量摄取工具](#asset-bulk-ingestor)：在部署[!DNL Experience Manager]时用于偶尔或最初摄取大量资源。

### 资产批量导入工具 {#asset-bulk-ingestor}

此工具仅提供给管理员组，用于从Azure或S3数据存储中大规模摄取资产。 观看配置和摄取的视频演练。

>[!VIDEO](https://video.tv.adobe.com/v/329680/?quality=12&learn=on)

下图说明了从数据存储中摄取资源以Experience Manager时的各个阶段：

![批量摄取工具](assets/bulk-ingestion.png)

**前提条件**

需要来自Azure或AWS的外部存储帐户或存储段才能使用此功能。

>[!NOTE]
>
>创建专用存储帐户容器或存储段，并仅接受来自授权请求的连接。 但是，不支持对入口网络连接的附加限制。

>[!NOTE]
>
>外部存储帐户可能具有与“批量导入”工具不同的文件/文件夹名称规则。 有关不允许/转义名称的更多详细信息，请参阅[在批量导入期间处理文件名](#filename-handling-bulkimport)。


### 配置批量导入工具 {#configure-bulk-ingestor-tool}

要配置批量导入工具，请执行以下步骤：

1. 导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 批量导入]**。 选择&#x200B;**[!UICONTROL 创建]**&#x200B;选项。

1. 在&#x200B;**[!UICONTROL 标题]**&#x200B;字段中指定批量导入配置的标题。

1. 从&#x200B;**[!UICONTROL 导入Source]**&#x200B;下拉列表中选择数据源类型。

1. 提供值以创建与数据源的连接。 例如，如果选择&#x200B;**Azure Blob存储**&#x200B;作为数据源，请指定Azure存储帐户、Azure Blob容器和Azure访问密钥的值。

1. 从下拉列表中选择所需的身份验证模式。 **Azure访问密钥**&#x200B;提供对Azure存储帐户的完全访问，而&#x200B;**Azure SAS令牌**&#x200B;允许管理员使用权限和过期策略限制令牌的功能。

1. 在&#x200B;**[!UICONTROL 源文件夹]**&#x200B;字段中提供包含数据源中资源的根文件夹的名称。

1. （可选）在&#x200B;**[!UICONTROL 按最小大小筛选]**&#x200B;字段中提供要包含在摄取进程中的资源的最小文件大小（以MB为单位）。

1. （可选）在&#x200B;**[!UICONTROL 按最大尺寸过滤]**&#x200B;字段中，以 MB 为单位提供资源的最大文件大小，以将其包括在摄取过程中。

1. （可选）在&#x200B;**[!UICONTROL 排除MIME类型]**&#x200B;字段中指定要从摄取中排除的MIME类型列表（以逗号分隔）。 例如，`image/jpeg, image/.*, video/mp4`。请参阅[所有支持的文件格式](/help/assets/file-format-support.md)。

1. 在&#x200B;**[!UICONTROL 包含MIME类型]**&#x200B;字段中指定要从摄取中包含的MIME类型列表（以逗号分隔）。 请参阅[所有支持的文件格式](/help/assets/file-format-support.md)。

1. 选择&#x200B;**[!UICONTROL 导入后删除源文件]**&#x200B;选项，以在文件导入[!DNL Experience Manager]后从源数据存储中删除原始文件。

1. 选择&#x200B;**[!UICONTROL “导入模式”。]**&#x200B;选择&#x200B;**“跳过”**、**“代替”**，或者&#x200B;**创建版本。**&#x200B;跳过模式是默认模式，在此模式下，引入器会跳过以导入已存在的资产。 查看[替换和创建版本选项](#handling-upload-existing-file)的含义。

1. 要使用&#x200B;**[!UICONTROL 资源目标文件夹]**&#x200B;字段在 DAM 中定义要导入资源的位置，请指定路径。例如：`/content/dam/imported_assets`。

1. （可选）在&#x200B;**[!UICONTROL 元数据文件]**&#x200B;字段中指定要导入的元数据文件（以 CSV 格式提供）。在源Blob位置中指定CSV文件，并在配置批量导入工具时引用路径。 当您[批量导入和导出资产元数据](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/metadata-import-export.html)时，此字段引用的CSV文件格式与CSV文件格式相同。 如果选择&#x200B;**导入后删除源文件**&#x200B;选项，请使用&#x200B;**排除**、**包含MIME类型**&#x200B;或&#x200B;**按路径/文件筛选**&#x200B;字段筛选CSV文件。 您可以使用正则表达式在这些字段中筛选CSV文件。

1. 单击&#x200B;**[!UICONTROL 保存]**&#x200B;以保存配置。

### 管理批量导入工具配置 {#manage-bulk-import-configuration}

创建批量导入工具配置后，您可以先执行任务以评估配置，然后再将资源批量摄取到Experience Manager实例。 要查看用于管理批量导入工具配置的可用选项，请选择位于&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 批量导入]**&#x200B;的配置。

### 编辑配置 {#edit-configuration}

要编辑配置详细信息，请选择配置，然后单击&#x200B;**[!UICONTROL 编辑]**。 执行编辑操作时，无法编辑配置和导入数据源的标题。

### 删除配置 {#delete-configuration}

选择配置并单击&#x200B;**[!UICONTROL 删除]**&#x200B;以删除批量导入配置。

### 验证与数据源的连接 {#validate-connection}

要验证与数据源的连接，请选择配置，然后单击&#x200B;**[!UICONTROL 检查]**。 如果连接成功，Experience Manager将显示以下消息：

![批量导入成功消息](assets/bulk-import-success-message.png)

### 为批量导入作业调用测试运行 {#invoke-test-run-bulk-import}

选择配置并单击&#x200B;**[!UICONTROL 试运行]**&#x200B;以调用批量导入作业的测试运行。 Experience Manager显示有关批量导入作业的以下详细信息：

![练习结果](assets/dry-assets-result.png)

### 批量导入期间处理文件名 {#filename-handling-bulkimport}

当您批量导入资源或文件夹时，[!DNL Experience Manager Assets] 导入在导入源中存在的内容的完整结构。[!DNL Experience Manager] 遵循针对关资源和文件夹名称中特殊字符的内置规则，因此需要净化这些文件名。对于文件夹名称和资源名称，用户定义的标题保持不变并存储在 `jcr:title` 中。

批量导入期间，[!DNL Experience Manager] 查找现有文件夹以避免重复导入资源和文件夹，还验证在发生导入的父文件夹中应用的净化规则。如果在父文件夹中应用了净化规则，则将相同的规则应用于导入源。对于新导入，应用以下净化规则以管理资源的文件名和文件夹名称。

**批量导入中不允许的名称**

文件和文件夹名称中不允许使用以下字符：

* 控制和专用使用字符（0x00到0x1F、\u0081、\uE000）
* 以点(.)结尾的文件或文件夹名称

在导入过程中，会跳过名称符合这些条件的文件或文件夹，并将其标记为失败。

**正在批量导入中处理资源名称**

对于资源文件名，使用API清理JCR名称和路径： `JcrUtil.escapeIllegalJcrChars`。

* 未更改Unicode字符
* 将特殊字符替换为其URL转义代码，例如，`new%asset.png`已更新为`new%25asset.png`：

  ```
                  URL escape code   
  
  "               %22
  %               %25
  '               %27
  *               %2A
  /               %2F
  :               %3A
  [               %5B
  \n              %0A
  \r              %0D
  \t              %09
  ]               %5D
  |               %7C
  ```

**正在处理批量导入中的文件夹名称**

对于文件夹文件名，使用API清理JCR名称和路径： `DamUtil.getSanitizedFolderName`。

* 大写字符转换为小写
* 未更改Unicode字符
* 将特殊字符替换为破折号(“ — ”)，例如，`new folder`已更新为`new-folder`：

  ```
  "                           
  #                         
  %                           
  &                          
  *                           
  +                          
  .                           
  :                           
  ;                          
  ?                          
  [                           
  ]                           
  ^                         
  {                         
  }                         
  |                           
  /         It is used for split folder in cloud storage and is pre-handled, no conversion here.
  \         Not allowed in Azure, allowed in AWS.
  \t
  space     It is the space character.
  ```

<!-- 
[!DNL Experience Manager Assets] manages the forbidden characters in the filenames while you upload assets or folders. [!DNL Experience Manager] updates only the node names in the DAM repository. However, the `title` of the asset or folder remains unchanged.

Following are the file naming conventions that are applied while uploading assets or folders in [!DNL Experience Manager Assets]:

| Characters &Dagger; | When occurring in file names | When occurring in folder names | Example |
|---|---|---|---|
| `. / : [ ] | *` | Replaced with `-` (hyphen). | Replaced with `-` (hyphen). A `.` (dot) in the filename extension is retained as is. | Replaced with `-` (hyphen). | `myimage.jpg` remains as is and `my.image.jpg` changes to `my-image.jpg`. |
| `% ; # , + ? ^ { } "` and whitespaces | Whitespaces are retained | Replaced with `-` (hyphen). | `My Folder.` changes to `my-folder-`. |
| `# % { } ? & .` | Replaced with `-` (hyphen). | NA. | `#My New File.` changes to `-My New File-`. |
| Uppercase characters | Casing is retained as is. | Changed to lowercase characters. | `My New Folder` changes to `my-new-folder`. |
| Lppercase characters | Casing is retained as is. | Casing is retained as is. | NA. |

&Dagger; The list of characters is a whitespace-separated list.
-->

#### 计划一次性或循环批量导入 {#schedule-bulk-import}

要计划一次性或定期批量导入，请执行以下步骤：

1. 创建批量导入配置。
1. 选择配置并从工具栏中选择&#x200B;**[!UICONTROL 计划]**。
1. 设置一次性摄取或安排每小时、每天或每周的摄取计划。单击&#x200B;**[!UICONTROL “提交”。]**

   ![计划批量引入器作业](assets/bulk-ingest-schedule1.png)


#### 查看Assets目标文件夹 {#view-assets-target-folder}

要查看运行批量导入作业后资源导入的Assets目标位置，请选择配置，然后单击&#x200B;**[!UICONTROL 查看Assets]**。

#### 运行批量导入工具 {#run-bulk-import-tool}

在[配置批量导入工具](#configure-bulk-ingestor-tool)并可选[管理批量导入工具配置](#manage-bulk-import-configuration)之后，您可以运行配置作业以开始批量摄取资产。

要启动批量导入流程，请导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 批量导入]**，选择[批量导入配置](#configure-bulk-ingestor-tool)，然后单击&#x200B;**[!UICONTROL 运行]**。 再次单击&#x200B;**[!UICONTROL 运行]**&#x200B;以确认。

Experience Manager在成功完成作业后将作业的状态更新为&#x200B;**正在处理**&#x200B;和&#x200B;**成功**。 若要在Experience Manager中查看导入的资源，请单击&#x200B;**查看Assets**。

当作业正在进行时，您还可以选择配置并单击&#x200B;**停止**&#x200B;以停止批量摄取进程。 再次单击&#x200B;**运行**&#x200B;以继续此进程。 您还可以单击&#x200B;**试运行**&#x200B;以了解仍在等待导入的资产的详细信息。

#### 执行后管理作业 {#manage-jobs-after-execution}

通过Experience Manager，可查看批量导入作业的历史记录。 作业历史记录包括作业的状态、作业创建者、日志以及其他详细信息，如开始日期和时间、创建日期和时间以及完成日期和时间。

要访问配置的作业历史记录，请选择该配置，然后单击&#x200B;**[!UICONTROL 作业历史记录]**。 选择作业并单击&#x200B;**打开**。

![计划批量引入器作业](assets/job-history-bulk-import.png)

Experience Manager显示作业历史记录。 在“批量导入作业历史记录”页面上，您还可以单击&#x200B;**删除**&#x200B;以删除该批量导入配置的作业。


## 使用桌面客户端上传资源 {#upload-assets-desktop-clients}

除了Web浏览器用户界面外，[!DNL Experience Manager]还支持桌面上的其他客户端。 它们还提供了上传体验，无需转至Web浏览器。

* [[!DNL Adobe Asset Link]](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html)提供了从Adobe Photoshop、Adobe Illustrator和Adobe InDesign桌面应用程序中的[!DNL Experience Manager]访问资源的权限。 您可以从这些桌面应用程序中直接从AdobeAsset Link用户界面将当前打开的文档上传到[!DNL Experience Manager]。
* [[!DNL Experience Manager] 桌面应用程序](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)可简化在桌面上使用资产的过程，而与资产的文件类型或处理这些资产的本机应用程序无关。 从本地文件系统上传嵌套文件夹层次结构中的文件很有用，因为浏览器上传仅支持上传平面文件列表。

## 上传时处理资源 {#process-when-uploaded}

要对上传的资源执行其他处理，您可以对上传文件夹应用处理配置文件。 配置文件在[!DNL Assets]中文件夹的&#x200B;**[!UICONTROL 属性]**&#x200B;页面中可用。 扩展名不正确或扩展名不正确的数字资产无法按需要处理。 例如，上传此类资产时，可能没有任何反应，或者资产处理配置文件不正确。 用户仍然可以在DAM中存储二进制文件。

![包含用于添加处理配置文件的选项的资产文件夹属性](assets/assets-folder-properties.png)

可以使用以下选项卡：

* [元数据配置文件](metadata-profiles.md)允许您将默认元数据属性应用于上载到该文件夹中的资源。
* [处理配置文件](asset-microservices-configure-and-use.md)允许您生成的呈现版本比默认情况下可能生成的呈现版本更多。

此外，如果在您的部署中启用了[!DNL Dynamic Media]，则以下选项卡可用：

* [[!DNL Dynamic Media] 图像配置文件](dynamic-media/image-profiles.md)允许您对上传的资源应用特定裁剪（**[!UICONTROL 智能裁剪]**&#x200B;和像素裁剪）和锐化配置。
* [[!DNL Dynamic Media] 视频配置文件](dynamic-media/video-profiles.md)允许您应用特定的视频编码配置文件（分辨率、格式、参数）。

>[!NOTE]
>
>对资源执行[!DNL Dynamic Media]裁剪和其他操作不具有破坏性，也就是说，这些操作不会更改上传的原始文件。 相反，它会在交付资源时提供参数以进行裁切或转换。

对于已分配处理配置文件的文件夹，配置文件名称会显示在卡片视图的缩略图上。 在列表视图中，配置文件名称显示在&#x200B;**[!UICONTROL 处理配置文件]**&#x200B;列中。

## 使用API上传或摄取资源 {#upload-using-apis}

开发人员参考的[资产上传](developer-reference-material-apis.md#asset-upload)部分提供了上传API和协议的技术详细信息，以及指向开源SDK和示例客户端的链接。

## 提示、最佳实践和限制 {#tips-limitations}

* 直接二进制上传是一种上传资产的新方法。 产品功能和客户端（如[!DNL Experience Manager]用户界面、[!DNL Adobe Asset Link]和[!DNL Experience Manager]桌面应用程序）默认支持它。 客户技术团队自定义或扩展的任何自定义代码必须使用新的上传API和协议。

* Adobe建议在[!DNL Experience Manager Assets]的每个文件夹中添加不超过1000个资源。 如果尝试这样做，您可能会收到一条警告消息，显示“此目录包含1000多个项目。 上传和新文件夹创建可能会延迟。” 虽然您仍然可以向一个文件夹添加更多资源，但您可能会遇到性能问题，例如导航到此类文件夹的速度变慢。

* 当您在[!UICONTROL 名称冲突]对话框中选择&#x200B;**[!UICONTROL 替换]**&#x200B;时，将为新资源重新生成资源ID。 此ID与上一个资源的ID不同。 如果启用了[Assets Insights](/help/assets/assets-insights.md)以通过[!DNL Adobe Analytics]跟踪展示次数或单击次数，则重新生成的资源ID将使在[!DNL Analytics]上为资源捕获的数据无效。

* 某些上传方法不会阻止您上传文件名中包含[禁止使用的字符](#filename-handling)的资产。 字符已替换为`-`符号。

* 使用浏览器上传资产仅支持平面文件列表，不支持嵌套文件夹层次结构。 要上传嵌套文件夹中的所有资源，请考虑使用[桌面应用程序](#upload-assets-desktop-clients)。

* 批量导入方法会导入数据源中存在的整个文件夹结构。 但是，在[!DNL Experience Manager]中只创建非空文件夹。


<!-- TBD: Link to file name handling in DA docs when it is documented. 
-->

**另请参阅**

* [翻译资源](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [资源支持的文件格式](file-format-support.md)
* [搜索资源](search-assets.md)
* [连接的资源](use-assets-across-connected-assets-instances.md)
* [资源报告](asset-reports.md)
* [元数据架构](metadata-schemas.md)
* [下载资源](download-assets-from-aem.md)
* [管理元数据](manage-metadata.md)
* [搜索 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [批量元数据导入](metadata-import-export.md)
* [发布资源到 AEM 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [[!DNL Adobe Experience Manager] 桌面应用程序](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html)
>* [关于 [!DNL Adobe Asset Link]](https://www.adobe.com/cn/creativecloud/business/enterprise/adobe-asset-link.html)
>* [[!DNL Adobe Asset Link] 文档](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html)
>* [资产上传的技术参考](developer-reference-material-apis.md#asset-upload)
