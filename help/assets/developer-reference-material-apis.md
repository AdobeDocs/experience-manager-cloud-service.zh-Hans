---
title: 'Adobe Experience Manager作为云服务中用于数字资产管理的资产API '
description: 资产API允许执行基本的创建——读取——更新——删除(CRUD)操作，以管理资产，包括二进制、元数据、演绎版、注释和内容片段。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 26833f59f21efa4de33969b7ae2e782fe5db8a14

---


# Assets as a Cloud Service APIs {#assets-cloud-service-apis}

<!-- 
Give a list of and overview of all reference information available.
* New upload method
* Javadocs
* Assets HTTP API documented at [https://helpx.adobe.com/experience-manager/6-5/assets/using/mac-api-assets.html](https://helpx.adobe.com/experience-manager/6-5/assets/using/mac-api-assets.html)

-->

## 资产上传 {#asset-upload-technical}

Experience Manager作为云服务，提供了将资产上传到存储库的新方式——将二进制上传到二进制云存储。 本节提供其技术概述。

### 直接二进制上传概述 {#overview-binary-upload}

上传二进制文件的高级算法是：

1. 提交HTTP请求，通知AEM上传新二进制文件的意图。
1. 将二进制内容发布到由启动请求提供的一个或多个URI。
1. 提交HTTP请求，通知服务器二进制内容已成功上传。

![直接二进制上传协议概述](assets/add-assets-technical.png)

与AEM的早期版本相比，重要的区别包括：

* 二进制文件不会通过AEM,AEM现在只是将上传过程与为部署配置的二进制云存储进行协调
* 二进制云存储由内容投放网络(CDN, Edge Network)提供，该网络使上传端点更接近客户端，从而有助于提高上传性能和用户体验，尤其是对于分布式团队上传资产

此方法应提供对资产上传的可扩展性和性能更高的处理。

> !![NOTE]
要查看实现此方法的客户端代码，请参阅开放源 [aem-upload库](https://github.com/adobe/aem-upload)

### 启动上传 {#initiate-upload}

第一步是将HTTP POST请求提交到资产应创建或更新的文件夹；包括选择 `.initiateUpload.json` 器以指示请求将开始二进制上传。 例如，应创建资产的文件夹的路径是 `/assets/folder`:

```
POST https://[aem_server]/content/dam/assets/folder.initiateUpload.json
````

请求主体的内容类型应为表单数 `application/x-www-form-urlencoded` 据，其中包含以下字段：

* `(string) fileName`: 必填. 资产在实例中显示的名称。
* `(number) fileSize`: 必填. 要上传的二进制文件的总长度（以字节为单位）。

只要每个二进制文件都包含必填字段，单个请求就可用于启动多个二进制文件的上载。 如果请求成功，则请求会以状态 `201` 代码和包含以下格式JSON数据的正文作出响应：

```
{
    "completeURI": "(string)",
    "folderPath": (string)",
    "files": [
        {
            "fileName": "(string)",
            "mimeType": "(string)",
            "uploadToken": "(string)",
            "uploadURIs": [
                "(string)"
            ]
        }
    ]
}
```

* `completeURI` （字符串）:在二进制完成上传时调用此URI。 URI可以是绝对URI或相对URI，客户端应能够处理其中任何一个。 即，该值可以是或查 `"https://author.acme.com/content/dam.completeUpload.json"` 看完 `"/content/dam.completeUpload.json"` 成 [上传](#complete-upload)。
* `folderPath` （字符串）:上传二进制文件的文件夹的完整路径。
* `(files)` （阵列）:元素列表，其长度和顺序将与初始化请求中提供的二进制信息列表的长度和顺序相匹配。
* `fileName` （字符串）:相应二进制的名称，在启动请求中提供。 此值应包括在完整请求中。
* `mimeType` （字符串）:相应二进制的MIME类型，如initiate请求中提供。 此值应包括在完整请求中。
* `uploadToken` （字符串）:相应二进制文件的上传令牌。 此值应包括在完整请求中。
* `uploadURIs` （阵列）:字符串的列表，其值为应将二进制内容上传到的完整URI(请参阅上 [传二进制](#upload-binary))。
* `minPartSize` （数字）:如果存在多个URI，则可能提供给uploadURI中任何一个的数据的最小长度（以字节为单位）。
* `maxPartSize` （数字）:如果存在多个URI，则可能提供给uploadURI中任何一个的数据的最大长度（以字节为单位）。

### 上传二进制文件 {#upload-binary}

启动上传的输出将包括一个或多个上传URI值。 如果提供了多个URI，则客户端有责任按顺序将二进制文件“拆分”为多个部分，并将每个部分的POST分为多个URI。 必须使用所有URI，并且每个部分必须大于最小大小并小于初始化响应中指定的最大大小。 这些请求将由CDN边缘节点作为前端，以加速二进制文件的上传。

实现此目的的一种潜在方法是根据API提供的上传URI数计算部件大小。 示例假定二进制文件的总大小为20,000字节，上传URI的数量为2:

* 通过将总大小除以URI的数量来计算部件大小：20,000 / 2 = 10,000
* 上传URI列表中二进制到第一个URI的POST字节范围0-9,999
* 在上传URI的列表中，二进制到第二个URI的POST字节范围为10,000-19,999

如果成功，服务器将使用状态代码对每个请求做出 `201` 响应。

### 完成上传 {#complete-upload}

上载二进制文件的所有部分后，最后一步是将HTTP POST请求提交到由启动数据提供的完整URI。 请求主体的内容类型应为应用程序／表单数据`x-www-form-urlencoded` ，其中包含以下字段：

* `(string) fileName`: 必填. 资产的名称，由初始数据提供。
* `(string) mimeType`: 必填. 二进制的HTTP内容类型，由启动数据提供。
* `(string) uploadToken`: 必填. 如启动数据所提供的，为二进制文件上传令牌。
* `(bool) createVersion`: 可选. 如果为true且具有指定名称的资产已存在，则该实例将创建该资产的新版本。
* `(string) versionLabel`: 可选. 如果创建了新版本，则与该版本关联的标签。
* `(string) versionComment`: 可选. 如果创建了新版本，则将与该版本关联的注释。
* `(bool) replace`:可选：如果为true且具有指定名称的资产已存在，则实例将删除该资产，然后重新创建它。

>!![NOTE]
>
> 如果资产已存在且未指定createVersion或replace，则实例将使用新的二进制文件更新资产的当前版本。

与启动过程一样，完整的请求数据可能包含多个文件的信息。

在为文件调用完整URL之前，不会完成上传二进制文件的过程。 即使文件的二进制文件全部上传，资产在完成上传过程之前也不会由实例进行处理。

如果成功，服务器将用状态代码 `200` 做出响应。

### 开放源码上传库 {#open-source-upload-library}

要进一步了解上传算法或构建您自己的上传脚本和工具，Adobe提供开放源代码库和工具作为起点：

* [开放源aem上传库](https://github.com/adobe/aem-upload)
* [开放源代码命令行工具](https://github.com/adobe/aio-cli-plugin-aem)

### 已弃用的资产上传API {#deprecated-asset-upload-api}

<!-- #ENGCHECK review / update the list of deprecated APIs below -->

>[!NOTE]
对于Experience Manager作为云服务，仅支持新的上传API。 已弃用Experience Manager 6.5中的API。

与上传或更新资产或演绎版（任何二进制上传）相关的方法在以下API中已弃用：

* [AEM Assets HTTP API](mac-api-assets.md)
* `AssetManager` Java API，如 `AssetManager.createAsset(..)`

>[!MORELIKETHIS]
* [开放源aem上传库](https://github.com/adobe/aem-upload)
* [开放源代码命令行工具](https://github.com/adobe/aio-cli-plugin-aem)


## 资产处理和后期处理工作流 {#post-processing-workflows}

大多数资产处理都基于资产微服务 **[!UICONTROL 的处理用户档案]**[配置执行](asset-microservices-configure-and-use.md#get-started-using-asset-microservices)，并且不需要开发人员扩展。

对于后处理工作流配置，请使用扩展的标准AEM工作流（例如，可以使用自定义步骤）。 查看以下子节以了解可在资产后期处理工作流中使用的工作流步骤。

### 后处理工作流中的工作流步骤 {#post-processing-workflows-steps}

>[!NOTE]
本节主要适用于从先前版本的AEM以云服务的形式更新到AEM的客户。

由于Experience Manager作为云服务引入了新的部署模型，因此在引入资产微服务之前在工作流中使用的某些工作流步骤可能不再支持后处理工作流。 `DAM Update Asset` 请注意，大多数服务被更简单的资产微服务配置和使用所取代。

以下是AEM中作为云服务的技术工作流模型及其支持级别的列表:

### 支持的工作流步骤 {#supported-workflow-steps}

云服务支持以下工作流步骤。

* `com.day.cq.dam.similaritysearch.internal.workflow.process.AutoTagAssetProcess`
* `com.day.cq.dam.core.impl.process.CreateAssetLanguageCopyProcess`
* `com.day.cq.wcm.workflow.process.CreateVersionProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.StartTrainingProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.TransferTrainingDataProcess`
* `com.day.cq.dam.core.impl.process.TranslateAssetLanguageCopyProcess`
* `com.day.cq.dam.core.impl.process.UpdateAssetLanguageCopyProcess`
* `com.adobe.cq.workflow.replication.impl.ReplicationWorkflowProcess`
* `com.day.cq.dam.core.impl.process.DamUpdateAssetWorkflowCompletedProcess`

### 不支持或替换的型号 {#unsupported-replaced-models}

以下技术工作流模型由资产微型服务取代，或者该支持不可用。

* `com.day.cq.dam.core.impl.process.DamMetadataWritebackWorkflowCompletedProcess`
* `com.day.cq.dam.core.process.DeleteImagePreviewProcess`
* `com.day.cq.dam.s7dam.common.process.DMEncodeVideoWorkflowCompletedProcess`
* `com.day.cq.dam.core.process.GateKeeperProcess`
* `com.day.cq.dam.core.process.AssetOffloadingProcess`
* `com.day.cq.dam.core.process.MetadataProcessorProcess`
* `com.day.cq.dam.core.process.XMPWritebackProcess`
* `com.adobe.cq.dam.dm.process.workflow.DMImageProcess`
* `com.day.cq.dam.s7dam.common.process.S7VideoThumbnailProcess`
* `com.day.cq.dam.scene7.impl.process.Scene7UploadProcess`
* `com.day.cq.dam.s7dam.common.process.VideoProxyServiceProcess`
* `com.day.cq.dam.s7dam.common.process.VideoThumbnailDownloadProcess`
* `com.day.cq.dam.s7dam.common.process.VideoUserUploadedThumbnailProcess`
* `com.day.cq.dam.core.process.CreatePdfPreviewProcess`
* `com.day.cq.dam.core.process.CreateWebEnabledImageProcess`
* `com.day.cq.dam.video.FFMpegThumbnailProcess`
* `com.day.cq.dam.core.process.ThumbnailProcess`
* `com.day.cq.dam.cameraraw.process.CameraRawHandlingProcess`
* `com.day.cq.dam.core.process.CommandLineProcess`
* `com.day.cq.dam.pdfrasterizer.process.PdfRasterizerHandlingProcess`
* `com.day.cq.dam.core.process.AddPropertyWorkflowProcess`
* `com.day.cq.dam.core.process.CreateSubAssetsProcess`
* `com.day.cq.dam.core.process.DownloadAssetProcess`
* `com.day.cq.dam.word.process.ExtractImagesProcess`
* `com.day.cq.dam.word.process.ExtractPlainProcess`
* `com.day.cq.dam.video.FFMpegTranscodeProcess`
* `com.day.cq.dam.ids.impl.process.IDSJobProcess`
* `com.day.cq.dam.indd.process.INDDMediaExtractProcess`
* `com.day.cq.dam.indd.process.INDDPageExtractProcess`
* `com.day.cq.dam.core.impl.lightbox.LightboxUpdateAssetProcess`
* `com.day.cq.dam.pim.impl.sourcing.upload.process.ProductAssetsUploadProcess`
* `com.day.cq.dam.core.process.ScheduledPublishBPProcess`
* `com.day.cq.dam.core.process.ScheduledUnPublishBPProcess`
* `com.day.cq.dam.core.process.SendDownloadAssetEmailProcess`
* `com.day.cq.dam.core.impl.process.SendTransientWorkflowCompletedEmailProcess`

<!-- PPTX source: slide in add-assets.md - overview of direct binary upload section of 
https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->
