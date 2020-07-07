---
title: 将数字资产添加到Adobe Experience Manager
description: 将您的数字资产作为Adobe Experience Manager添加为Cloud Service
translation-type: tm+mt
source-git-commit: 23349f3350631f61f80b54b69104e5a19841272f
workflow-type: tm+mt
source-wordcount: '1358'
ht-degree: 3%

---


# 将数字资产添加到Adobe Experience Manager {#add-assets-to-experience-manager}

Adobe Experience Manager通过丰富的元数据、智能标记、演绎版和其他数字资产管理(DAM)服务丰富了已上传数字文件的二进制内容。 您可以将各种类型的文件(如图像、文档和原始图像文件)从本地文件夹或网络驱动器上传到Experience Manager资产。

提供了许多上传方法。 除了最常用的浏览器上传外，还存在将资产添加到Experience Manager库的其他方法，包括桌面客户端(如Adobe Asset Link或Experience Manager桌面应用程序)、上传和摄取客户将创建的脚本，以及自动摄取作为AEM扩展添加的集成。

我们将重点介绍此处为最终用户上传方法，并提供指向文章的链接，这些文章描述了使用Experience ManagerAPI和SDK进行资产上传和获取的技术方面。

虽然可以以Experience Manager方式上传和管理任何二进制文件，但最常用的文件格式支持其他服务，如元数据提取或预览/再现生成。 有关详细信息， [请参阅支持的](file-format-support.md) 文件格式。

您还可以选择对上传的资产进行其他处理。 您可以在上传资产的文件夹中配置大量资产处理用户档案，以添加特定元数据、演绎版或图像处理服务。 请参 [阅下面的](#additional-processing) “其他处理”以了解更多信息。

>[!NOTE]
>
>Experience Manager作为Cloud Service，利用一种新的资产上传方式——直接二进制上传。 默认情况下，开箱即用的产品功能和客户端（如AEM用户界面、Adobe Asset Link、AEM桌面应用程序）都支持此功能，因此对最终用户是透明的。
>
>上传由技术团队需要使用新上传API和协议的客户自定义或扩展的代码。

## Upload assets {#upload-assets}

要上传文件（或多个文件），您可以在桌面上选择它们，然后拖放到用户界面（Web浏览器）到目标文件夹。 或者，也可以从用户界面启动上传。

1. 在资产用户界面中，导航到要添加数字资产的位置。
1. 要上传资产，请执行以下操作之一：

   * On the toolbar, tap the **[!UICONTROL Create]** icon. 然后，在菜单上，点按文 **[!UICONTROL 件]**。 如果需要，可以重命名显示的对话框中的文件。
   * 在支持HTML5的浏览器中，直接将资产拖动到“资产”用户界面上。 不显示要重命名文件的对话框。
   ![create_menu](assets/create_menu.png)

   要选择多个文件，请按Ctrl或Command键，然后在文件选取器对话框中选择资产。 使用iPad时，一次只能选择一个文件。

<!-- #ENGCHECK do we support pausing? I couldn't get pause to show with 1.5GB upload.... If not, this should be removed#

   You can pause the uploading of large assets (greater than 500 MB) and resume it later from the same page. Tap the **[!UICONTROL Pause]** icon beside progress bar that appears when an upload starts.

   ![chlimage_1-211](assets/chlimage_1-211.png)

   The size above which an asset is considered a large asset is configurable. For example, you can configure the system to consider assets above 1000 MB (instead of 500 MB) as large assets. In this case, **[!UICONTROL Pause]** appears on the progress bar when assets of size greater than 1000 MB are uploaded.

   The Pause button does not show if a file greater than 1000 MB is uploaded with a file less than 1000 MB. However, if you cancel the less than 1000 MB file upload, the **[!UICONTROL Pause]** button appears.

   To modify the size limit, configure the `chunkUploadMinFileSize` property of the `fileupload`node in the CRX repository.

   When you click the **[!UICONTROL Pause]** icon, it toggles to a **[!UICONTROL Play]** icon. To resume uploading, click the **[!UICONTROL Play]** icon.

   ![chlimage_1-212](assets/chlimage_1-212.png)
-->

1. To cancel an ongoing upload, click close (`X`) next to the progress bar. 当您取消上传操作时，AEM Assets会删除资产部分上传的部分。

   如果在上传文件之前取消上传操作，AEM Assets将停止上传当前文件并刷新内容。 但是，不会删除已上传的文件。


<!-- #ENGCHECK do we support pausing? I couldn't get pause to show with 1.5GB upload.... If not, this should be removed#
   The ability to resume uploading is especially helpful in low-bandwidth scenarios and network glitches, where it takes a long time to upload a large asset. You can pause the upload operation and continue later when the situation improves. When you resume, uploading starts from the point where you paused it.
-->

<!-- #ENGCHECK assuming this is not relevant? remove after confirming#
   During the upload operation, AEM saves the portions of the asset being uploaded as chunks of data in the CRX repository. When the upload completes, AEM consolidates these chunks into a single block of data in the repository.

   To configure the cleanup task for the unfinished chunk upload jobs, go to `https://[aem_server]:[port]/system/console/configMgr/org.apache.sling.servlets.post.impl.helper.ChunkCleanUpTask`.
-->


1. AEM Assets中的上传进度对话框显示成功上传的文件和无法上传的文件的计数。

此外，资产用户界面还会显示您上传的最新资产或您首先创建的文件夹。

>[!NOTE]
>
>要将嵌套文件夹层次结构上传到AEM，请参 [阅批量上传资产](#bulk-upload)。

<!-- #ENGCHECK I'm assuming this is no longer relevant.... If yes, this should be removed#

### Serial uploads {#serialuploads}

Uploading numerous assets in bulk consumes significant I/O resources, which may adversely impact the performance of your AEM Assets instance. In particular, if you have a slow internet connection, the time to upload drastically increases due to a spike in disk I/O. Moreover, your web browser may introduce additional restrictions to the number of POST requests AEM Assets can handle for concurrent asset uploads. As a result, the upload operation fails or terminate prematurely. In other words, AEM assets may miss some files while ingesting a bunch of files or altogether fail to ingest any file.

To overcome this situation, AEM Assets ingests one asset at a time (serial upload) during a bulk upload operation, instead of the concurrently ingesting all the assets.

Serial uploading of assets is enabled by default. To disable the feature and allow concurrent uploading, overlay the `fileupload` node in Crx-de and set the value of the `parallelUploads` property to `true`.

### Streamed uploads {#streamed-uploads}

If you upload many assets to AEM, the I/O requests to server increase drastically, which reduces the upload efficiency and can even cause some upload task to time out. AEM Assets supports streamed uploading of assets. Streamed uploading reduces the disk I/O during the upload operation by avoiding asset storage in a temporary folder on the server before copying it to the repository. Instead, the data is transferred directly to the repository. This way, the time to upload large assets and the possibility of timeouts is reduced. Streamed upload is enabled by default in AEM Assets.

>[!NOTE]
>
>Streaming upload is disabled for AEM running on JEE server with servlet-api version lower than 3.1.
-->

### 在资产已存在时处理上传 {#handling-upload-existing-file}

如果您上传的资产名称与您上传资产的位置中已有资产的名称相同，则会显示一个警告对话框。

您可以选择替换现有资产，创建另一个版本，或者重命名上传的新资产以同时保留两个资产。如果您替换现有资产，则资产的元数据以及您对现有资产所做的任何先前修改（例如注释、裁剪等）都将被删除。 如果您选择保留这两个资产，则会重命名新资产，并在其名称 `1` 中附加数字。

>[!NOTE]
>
>在名称冲 **[!UICONTROL 突]** 对话框 [!UICONTROL 中选择替] 换时，将为新资产重新生成资产ID。 此ID与上一个资产的ID不同。
>
>如果启用“资产分析”以通过AdobeAnalytics跟踪展示次数／点击次数，则重新生成的资产ID将使Analytics上为资产捕获的数据无效。

要将重复资产保留在AEM Assets中，请点按／单 **[!UICONTROL 击保留]**。 要删除您上传的重复资产，请点按／单击 **[!UICONTROL 删除]**。

### 文件名处理和禁止字符 {#filename-handling}

AEM Assets可防止您上传文件名中带有禁止字符的资产。 如果您尝试上传包含不允许的字符或更多字符的资产，AEM Assets会显示一条警告消息并停止上传，直到您删除这些字符或上传时使用允许的名称。

为了符合组织的特定文件命名约定，您 [!UICONTROL 可以在“上传资产] ”对话框中为上传的文件指定长名。

但是，不支持以下(以空格分隔的列表)字符：

* 资产文件名不能包含 `* / : [ \\ ] | # % { } ? &`
* 资产文件夹名称不能包含 `* / : [ \\ ] | # % { } ? \" . ^ ; + & \t`

## 批量上传资产 {#bulk-upload}

要上传更多文件，特别是如果这些文件存在于磁盘上的嵌套文件夹层次结构中，可以使用以下方法：

* 使用利用资产上传API的自定义上 [传脚本或工具](developer-reference-material-apis.md#asset-upload-technical)。 此类自定义工具可以根据需要添加对资产的其他处理（例如，翻译元数据或重命名文件）。
* 使用 [Experience Manager桌面应用](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html) ，上传嵌套文件夹层次结构。

>[!NOTE]
>
>在设置内容并部署到Experience Manager时，需要仔细规划、考虑和选择工具，才能将批量上传作为从其他系统迁移内容的一部分。 有关内容迁 [移方法的指](/help/implementing/deploying/overview.md) 导，请参阅部署指南。

## 使用桌面客户端上传资产 {#upload-assets-desktop-clients}

除了Web浏览器用户界面外，Experience Manager还支持桌面上的其他客户端。 它们还提供上传体验，无需转到Web浏览器。

* [Adobe Asset](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html) Link提供从Adobe Photoshop、Adobe Illustrator和Adobe InDesign桌面应用程序中的AEM访问资源的功能。 您可以从这些桌面应用程序中的Adobe Asset Link用户界面直接将当前打开的文档上传到AEM。
* [Experience Manager桌面应用](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html) 程序简化了在桌面上处理资源的工作，它们与文件类型无关，也与处理资源的本机应用程序无关。 从本地文件系统上传嵌套文件夹层次结构中的文件尤为有用，因为浏览器上传仅支持上传平面文件列表。

## 附加处理 {#additional-processing}

为了对上传的资产进行其他处理，您可以对上传资产的文件夹使用资产处理用户档案用户档案。 这些属性位于文件夹属 **[!UICONTROL 性对话框中]** 。

![assets-folder-properties](assets/assets-folder-properties.png)

提供以下用户档案:

* [元数据用户档案](metadata-profiles.md) 允许您将默认元数据属性应用到上传到该文件夹的资产
* [处理用户档案](asset-microservices-configure-and-use.md#processing-profiles) 允许您应用再现处理，除默认的再现外，还可以生成再现

此外，如果Dynamic Media在您的环境中处于启用状态：

* [Dynamic Media图像用户档案](dynamic-media/image-profiles.md) 允许您对上传的资产应&#x200B;**[!UICONTROL 用特定裁剪]** （智能裁剪和像素裁剪）和锐化配置。
* [Dynamic Media视频用户档案](dynamic-media/video-profiles.md) 允许您应用特定的视频编码用户档案（分辨率、格式、参数）。

>[!NOTE]
>
>Dynamic Media对资产进行裁剪和其他操作是无损的，即，它们不会更改上传的原始内容，而是为传送资产时要进行的裁剪或媒体转换提供参数

对于分配了处理用户档案的文件夹，用户档案名显示在卡视图的缩略图上。 在列表视图中，用户档案名称显示在处理 **[!UICONTROL 用户档案列]** 。

## 使用API上传或摄取资产 {#upload-using-apis}

开发人员参考的“资产上传”部分提供了上传API和协议的技术详细信息，以及指向开放源码SDK [和示例客户](developer-reference-material-apis.md#asset-upload-technical) 端的链接。

>[!MORELIKETHIS]
>
>* [Adobe Experience Manager 桌面应用程序](https://docs.adobe.com/content/help/zh-Hans/experience-manager-desktop-app/using/introduction.html)
>* [Adobe Asset Link](https://www.adobe.com/cn/creativecloud/business/enterprise/adobe-asset-link.html)
>* [Adobe Asset Link文档](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html)
>* [资产上传的技术参考](developer-reference-material-apis.md#asset-upload-technical)

