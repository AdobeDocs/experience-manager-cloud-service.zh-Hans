---
title: 将数字资产添加到 [!DNL Adobe Experience Manager]。
description: 将您的数字资产作为 [!DNL Cloud Service]添加到 [!DNL Adobe Experience Manager] 。
translation-type: tm+mt
source-git-commit: 6f5b6ba7da4c0d3161b9f34602b0256c319b191f
workflow-type: tm+mt
source-wordcount: '1903'
ht-degree: 1%

---


# 将数字资产添加到Adobe Experience Manager{#add-assets-to-experience-manager}

[!DNL Adobe Experience Manager] 通过丰富的元数据、智能标记、演绎版和其他数字资产管理(DAM)服务，丰富已上传数字文件的二进制内容。您可以将各种类型的文件(如图像、文档和原始图像文件)从本地文件夹或网络驱动器上传到[!DNL Experience Manager Assets]。

提供了许多上传方法。 除了最常用的浏览器上传外，还存在将资产添加到[!DNL Experience Manager]存储库的其他方法，包括桌面客户端(如Adobe资产链接或[!DNL Experience Manager]桌面应用程序)、上传和摄取客户将创建的脚本以及自动摄取集成（添加为[!DNL Experience Manager]扩展）。

我们将重点介绍此处为最终用户提供的上传方法，并提供指向文章的链接，这些文章描述了使用[!DNL Experience Manager] API和SDK进行资产上传和获取的技术方面。

虽然您可以上传和管理[!DNL Experience Manager]中的任何二进制文件，但最常用的文件格式支持其他服务，如元数据提取或预览/再现生成。 有关详细信息，请参阅[支持的文件格式](file-format-support.md)。

您还可以选择对上传的资产进行其他处理。 您可以在上传资产的文件夹中配置大量资产处理用户档案，以添加特定元数据、演绎版或图像处理服务。 请参阅[上传时处理资产](#process-when-uploaded)。

>[!NOTE]
>
>[!DNL Experience Manager] 这样， [!DNL Cloud Service] 您就可以利用新的上传资产的方式——直接二进制上传。默认情况下，开箱即用的产品功能和客户端（如[!DNL Experience Manager]用户界面、[!DNL Adobe Asset Link]、[!DNL Experience Manager]桌面应用程序）都支持此功能，因此对最终用户是透明的。
>
>上传由技术团队需要使用新上传API和协议的客户自定义或扩展的代码。

资产([!DNL Cloud Service])提供以下上传方法。 Adobe建议您在使用上传选项之前了解其用例和适用性。

| 上传方法 | 何时使用？ | 主要人物 |
|---------------------|----------------|-----------------|
| [资产控制台用户界面](#upload-assets) | 偶尔上传、轻松下载、查找器上传。 请勿用于上传大量资产。 | 所有用户 |
| [上传API](#upload-using-apis) | 用于上传过程中的动态决策。 | 开发人员 |
| [[!DNL Experience Manager] 桌面应用程序](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) | 低容量资产摄取，但用于迁移。 | 管理员、营销人员 |
| [[!DNL Adobe Asset Link]](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/adobe-asset-link.ug.html) | 当创意人员和营销人员从受支持的[!DNL Creative Cloud]桌面应用程序中处理资产时非常有用。 | 创意、营销人员 |
| [资产批量摄取](#asset-bulk-ingestor) | 建议进行大规模迁移和偶尔进行批量迁移。 仅用于支持的数据存储。 | 管理员、开发人员 |

## 上传资产{#upload-assets}

<!-- #ENGCHECK do we support pausing? I couldn't get pause to show with 1.5GB upload.... If not, this should be removed#

   You can pause the uploading of large assets (greater than 500 MB) and resume it later from the same page. Tap the **[!UICONTROL Pause]** icon beside progress bar that appears when an upload starts.

   ![chlimage_1-211](assets/chlimage_1-211.png)

   The size above which an asset is considered a large asset is configurable. For example, you can configure the system to consider assets above 1000 MB (instead of 500 MB) as large assets. In this case, **[!UICONTROL Pause]** appears on the progress bar when assets of size greater than 1000 MB are uploaded.

   The Pause button does not show if a file greater than 1000 MB is uploaded with a file less than 1000 MB. However, if you cancel the less than 1000 MB file upload, the **[!UICONTROL Pause]** button appears.

   To modify the size limit, configure the `chunkUploadMinFileSize` property of the `fileupload`node in the CRX repository.

   When you click the **[!UICONTROL Pause]** icon, it toggles to a **[!UICONTROL Play]** icon. To resume uploading, click the **[!UICONTROL Play]** icon.

   ![chlimage_1-212](assets/chlimage_1-212.png)
-->

<!-- #ENGCHECK do we support pausing? I couldn't get pause to show with 1.5GB upload.... If not, this should be removed#
   The ability to resume uploading is especially helpful in low-bandwidth scenarios and network glitches, where it takes a long time to upload a large asset. You can pause the upload operation and continue later when the situation improves. When you resume, uploading starts from the point where you paused it.
-->

<!-- #ENGCHECK assuming this is not relevant? remove after confirming#
   During the upload operation, [!DNL Experience Manager] saves the portions of the asset being uploaded as chunks of data in the CRX repository. When the upload completes, [!DNL Experience Manager] consolidates these chunks into a single block of data in the repository.

   To configure the cleanup task for the unfinished chunk upload jobs, go to `https://[aem_server]:[port]/system/console/configMgr/org.apache.sling.servlets.post.impl.helper.ChunkCleanUpTask`.
-->

要上传文件（或多个文件），您可以在桌面上选择它们，然后在用户界面（Web浏览器）上拖动到目标文件夹。 或者，也可以从用户界面启动上传。

1. 在[!DNL Assets]用户界面中，导航到要添加数字资产的位置。
1. 要上传资产，请执行以下操作之一：

   * 在工具栏上，单击&#x200B;**[!UICONTROL 创建]** > **[!UICONTROL 文件]**。 如果需要，可以重命名显示的对话框中的文件。
   * 在支持HTML5的浏览器中，直接将资产拖动到[!DNL Assets]用户界面上。 不显示要重命名文件的对话框。

   ![create_menu](assets/create_menu.png)

   要选择多个文件，请选择`Ctrl`或`Command`键，然后在文件选取器对话框中选择资产。 使用iPad时，一次只能选择一个文件。

1. 要取消正在进行的上传，请单击进度栏旁边的关闭(`X`)。 取消上传操作后，[!DNL Assets]将删除资产部分上传的部分。
如果在上传文件之前取消上传操作，[!DNL Assets]将停止上传当前文件并刷新内容。 但是，不会删除已上传的文件。

1. [!DNL Assets]中的上载进度对话框显示成功上载的文件计数以及无法上载的文件。
此外，[!DNL Assets]用户界面还显示您上传的最新资产或您首先创建的文件夹。

>[!NOTE]
>
>要上传嵌套文件夹层次结构，请参阅[批量上传资产](#bulk-upload)。

<!-- #ENGCHECK I'm assuming this is no longer relevant.... If yes, this should be removed#

### Serial uploads {#serialuploads}

Uploading numerous assets in bulk consumes significant I/O resources, which may adversely impact the performance of [!DNL Assets]. In particular, if you have a slow internet connection, the time to upload drastically increases due to a spike in disk I/O. Moreover, your web browser may introduce additional restrictions to the number of POST requests [!DNL Assets] can handle for concurrent asset uploads. As a result, the upload operation fails or terminate prematurely. In other words, [!DNL Assets] may miss some files while ingesting a bunch of files or altogether fail to ingest any file.

To overcome this situation, [!DNL Assets] ingests one asset at a time (serial upload) during a bulk upload operation, instead of the concurrently ingesting all the assets.

Serial uploading of assets is enabled by default. To disable the feature and allow concurrent uploading, overlay the `fileupload` node in Crx-de and set the value of the `parallelUploads` property to `true`.

### Streamed uploads {#streamed-uploads}

If you upload many assets to [!DNL Experience Manager], the I/O requests to server increase drastically, which reduces the upload efficiency and can even cause some upload task to time out. [!DNL Assets] supports streamed uploading of assets. Streamed uploading reduces the disk I/O during the upload operation by avoiding asset storage in a temporary folder on the server before copying it to the repository. Instead, the data is transferred directly to the repository. This way, the time to upload large assets and the possibility of timeouts is reduced. Streamed upload is enabled by default in [!DNL Assets].

>[!NOTE]
>
>Streaming upload is disabled for [!DNL Experience Manager] running on JEE server with servlet-api version lower than 3.1.
-->

### 当资产已存在{#handling-upload-existing-file}时处理上传

您可以上传与现有资产路径相同（名称相同，位置相同）的资产。 但是，将显示一个警告对话框，其中包含以下选项：

* 替换现有资产：如果您替换现有资产，则资产的元数据以及您对现有资产所做的任何先前修改（例如注释、裁剪等）都将被删除。
* 创建另一个版本：现有资产的新版本将在存储库中创建。 您可以视图[!UICONTROL 时间轴]中的两个版本，并可以根据需要还原到先前已有的版本。
* 同时保留：如果您选择保留这两个资产，则会重命名新资产，并在其名称后附加数字`1`。

>[!NOTE]
>
>在[!UICONTROL 名称冲突]对话框中选择&#x200B;**[!UICONTROL 替换]**&#x200B;时，将为新资产重新生成资产ID。 此ID与上一个资产的ID不同。
>
>如果启用“资产分析”以跟踪观感或使用[!DNL Adobe Analytics]进行点击，则重新生成的资产ID将使在[!DNL Analytics]上为资产捕获的数据无效。

要在[!DNL Assets]中保留重复资产，请单击&#x200B;**[!UICONTROL 保留]**。 要删除您上传的重复资产，请点按／单击&#x200B;**[!UICONTROL 删除]**。

### 文件名处理和禁止字符{#filename-handling}

[!DNL Experience Manager Assets] 尝试阻止您上传文件名中带有禁止字符的资产。如果您尝试上传包含不允许的字符或更多字符的资产，[!DNL Assets]会显示一条警告消息并停止上传，直到您删除这些字符或上传时使用允许的名称。 某些上传方法不会阻止您上传文件名中包含禁止字符的资产，但会用`-`替换这些字符。

为了符合组织的特定文件命名约定，[!UICONTROL 上传资产]对话框允许您为上传的文件指定长名称。 不支持以下(以空格分隔的列表)字符：

* 资产文件名`* / : [ \\ ] | # % { } ? &`的字符无效
* 资产文件夹名称`* / : [ \\ ] | # % { } ? \" . ^ ; + & \t`的字符无效

## 批量上传资产{#bulk-upload}

批量资产摄取器可以高效地处理大量资产。 但是，大规模摄取不仅仅是一个广泛的文件转储或临时迁移。 要实现大规模摄取，使其成为符合您业务目的且高效的有意义的项目，请规划迁移并管理资产组织。 所有收入都不同，因此，在细微的信息库构成和业务需求中，不是泛泛的因素。 以下是规划和执行批量摄取的一些总体建议：

* 特选资产：删除DAM中不需要的资产。 考虑删除未使用、过时或重复资产。 这减少了数据传输和资产摄取量，从而加快了摄取速度。
* 组织资产：考虑按照某种逻辑顺序组织内容，例如按文件大小、文件格式、用例或优先级。 通常，大型复杂文件需要更多处理。 您还可以考虑使用文件大小筛选选项（如下所述）单独引入大文件。
* 错开收录：考虑将摄取分解为多个批量摄取项目。 这使您能够更快地查看内容并根据需要更新摄取。 例如，您可以在非高峰时间或以多个区块逐步摄取处理密集型资产。 但是，您可以一次性摄取较小且更简单的资产，而无需进行大量处理。

要上传更多文件，请使用以下方法之一。 另请参阅[用例和方法](#upload-methods-comparison)

* [资产上传API](developer-reference-material-apis.md#asset-upload-technical):使用自定义上传脚本或工具，该脚本或工具根据需要利用API添加对资产的其他处理（例如，翻译元数据或重命名文件）。
* [[!DNL Experience Manager] 桌面应用程序](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html):对于从本地文件系统上传资产的创意专业人士和营销人员非常有用。使用它上传可在本地使用的嵌套文件夹。
* [批量摄取工具](#asset-bulk-ingestor):在部署时，可偶尔或最初用于获取大量资产 [!DNL Experience Manager]。

### 资产批量摄取工具{#asset-bulk-ingestor}

该工具仅提供给管理员组，用于从Azure或S3数据存储中大规模获取资源。 观看配置和摄取的视频演练。

>[!VIDEO](https://video.tv.adobe.com/v/329680/?quality=12&learn=on)

要配置此工具，请执行以下步骤：

1. 导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 批量导入]**。 选择&#x200B;**[!UICONTROL 创建]**&#x200B;选项。

![批量导入程序配置](assets/bulk-import-config.png)

1. 在[!UICONTROL 批量导入配置]页上，提供所需的值。

   * [!UICONTROL 标题]:描述性标题。
   * [!UICONTROL 导入源]:选择适用的数据源。
   * [!UICONTROL 按最小大小筛选]:提供资源的最小文件大小(MB)。
   * [!UICONTROL 按最大大小筛选]:提供资源的最大文件大小(MB)。
   * [!UICONTROL 排除MIME类型]:要从摄取中排除的MIME类型的以逗号分隔的列表。例如，`image/jpeg, image/.*, video/mp4`。
   * [!UICONTROL 包括Mime类型]:要包含在摄取中的MIME类型的逗号分隔列表。请参阅[所有支持的文件格式](/help/assets/file-format-support.md)。
   * [!UICONTROL 导入模式]:选择跳过、替换或创建版本。“跳过”模式是默认模式，在此模式下，如果资产已存在，则会跳过以导入资产。 请参阅[替换和创建版本选项](#handling-upload-existing-file)的含义。
   * [!UICONTROL 资产目标文件夹]:在要导入资产的DAM中导入文件夹。例如，`/content/dam/imported_assets`

1. 您可以删除、修改、执行和执行您创建的登录配置，并执行更多操作。 选择批量导入引擎配置时，工具栏中提供以下选项。

   * [!UICONTROL 编辑]:编辑所选配置。
   * [!UICONTROL 删除]:删除所选配置。
   * [!UICONTROL 检查]:验证与数据存储的连接。
   * [!UICONTROL 练习]:调用批量摄取的测试运行。
   * [!UICONTROL 运行]:执行所选配置。
   * [!UICONTROL 停止]:终止活动配置。
   * [!UICONTROL 作业状态]:视图配置在正在进行的导入作业中或用于已完成作业时的状态。
   * [!UICONTROL 视图资产]:视图目标文件夹（如果存在）。

## 使用桌面客户端{#upload-assets-desktop-clients}上传资产

除了Web浏览器用户界面外，[!DNL Experience Manager]还支持桌面上的其他客户端。 它们还提供上传体验，无需转到Web浏览器。

* [[!DNL Adobe Asset Link]](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html) 提供从Adobe Photoshop、Adobe Illustrator和 [!DNL Experience Manager] Adobe InDesign桌面应用程序访问资源的功能。您可以从这些桌面应用程序内的文档资产链接用户界面直接将当前打开的Adobe上传到[!DNL Experience Manager]。
* [[!DNL Experience Manager] 桌面](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) 应用程序简化了在桌面上处理资源的工作，这些资源独立于其文件类型或处理它们的本机应用程序。从本地文件系统上传嵌套文件夹层次结构中的文件尤为有用，因为浏览器上传仅支持上传平面文件列表。

## 上传{#process-when-uploaded}时处理资产

为了对已上传的资产进行其他处理，您可以对上传文件夹应用处理用户档案。 这些用户档案位于[!DNL Assets]文件夹的&#x200B;**[!UICONTROL 属性]**&#x200B;页面中。

![assets-folder-properties](assets/assets-folder-properties.png)

可以使用以下选项卡：

* [元数据](metadata-profiles.md) 配置文件允许您将默认元数据属性应用到上传到该文件夹的资产
* [处理](asset-microservices-configure-and-use.md) 配置文件允许您生成的演绎版数量超出默认值。

此外，如果部署中启用了[!DNL Dynamic Media]，则可以使用以下选项卡：

* [Dynamic Media图](dynamic-media/image-profiles.md) 像配置文件允许您对上传的资&#x200B;**[!UICONTROL 源应]** 用特定裁剪（智能裁剪和像素裁剪）和锐化配置。
* [Dynamic Media视](dynamic-media/video-profiles.md) 频配置文件允许您应用特定的视频编码用户档案（分辨率、格式、参数）。

>[!NOTE]
>
>Dynamic Media资产裁剪和其他操作是无损的，即它们不会更改上传的原始内容，而是为传送资产时要进行的裁剪或媒体转换提供参数

对于分配了处理用户档案的文件夹，用户档案名显示在卡视图的缩略图上。 在列表视图中，用户档案名显示在&#x200B;**[!UICONTROL 处理用户档案]**&#x200B;列中。

## 使用API {#upload-using-apis}上传或摄取资产

开发人员参考的[asset upload](developer-reference-material-apis.md#asset-upload-technical)部分提供了上传API和协议的技术详细信息，以及到开放源码SDK和示例客户端的链接。

>[!MORELIKETHIS]
>
>* [[!DNL Adobe Experience Manager] 桌面应用程序](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html)
>* [关于 [!DNL Adobe Asset Link]](https://www.adobe.com/cn/creativecloud/business/enterprise/adobe-asset-link.html)
>* [[!DNL Adobe Asset Link] 文档](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)
>* [资产上传的技术参考](developer-reference-material-apis.md#asset-upload-technical)

