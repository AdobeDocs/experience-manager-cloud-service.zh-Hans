---
title: 'Adobe Experience Manager中用作云服务的数字资产管理的资产API '
description: 资产API允许执行基本的创建——读取——更新——删除(CRUD)操作，以管理资产，包括二进制、元数据、演绎版、注释和内容片段。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 27e72bbc0d852eb2c2eb059967c91e6108613965
workflow-type: tm+mt
source-wordcount: '1249'
ht-degree: 1%

---


# Assets as a Cloud Service APIs {#assets-cloud-service-apis}

<!-- 
Give a list of and overview of all reference information available.
* New upload method
* Javadocs
* Assets HTTP API documented at [https://helpx.adobe.com/experience-manager/6-5/assets/using/mac-api-assets.html](https://helpx.adobe.com/experience-manager/6-5/assets/using/mac-api-assets.html)

-->

## 资产上传 {#asset-upload-technical}

Experience Manager作为云服务，提供了一种将资产上传到存储库的新方法——将二进制上传到二进制云存储。 本节提供其技术概述。

### 直接二进制上传概述 {#overview-binary-upload}

上传二进制文件的高级算法是：

1. 提交HTTP请求，通知AEM上传新二进制文件的意图。
1. 将二进制内容发布到由启动请求提供的一个或多个URI。
1. 提交HTTP请求，通知服务器二进制内容已成功上传。

![直接二进制上传协议概述](assets/add-assets-technical.png)

与AEM的早期版本相比，重要区别包括：

* 二进制文件不会通过AEM,AEM现在只是将上传过程与为部署配置的二进制云存储进行协调
* 二进制云存储由内容投放网络(CDN, Edge Network)提供，它使上传端点更接近客户端，从而有助于提高上传性能和用户体验，尤其对于上传资产的分布式团队而言

此方法应提供对资产上传的更具可扩展性和更高性能的处理。

> !![NOTE]
要查看实现此方法的客户端代码，请参阅开放源 [码aem-upload库](https://github.com/adobe/aem-upload)

### 启动上传 {#initiate-upload}

第一步是将HTTP POST请求提交到应创建或更新资产的文件夹； 包括选择 `.initiateUpload.json` 器以指示请求将开始二进制上传。 例如，应创建资产的文件夹的路径为 `/assets/folder`:

```
POST https://[aem_server]/content/dam/assets/folder.initiateUpload.json
```

请求主体的内容类型应为表 `application/x-www-form-urlencoded` 单数据，其中包含以下字段：

* `(string) fileName`: 必填. 资产在实例中显示的名称。
* `(number) fileSize`: 必填. 要上传的二进制文件的总长度（以字节为单位）。

只要每个二进制文件都包含必填字段，单个请求就可以用于启动多个二进制文件的上载。 如果请求成功，则请求将以 `201` 下格式以状态代码和包含JSON数据的正文进行响应：

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

* `completeURI` （字符串）: 当二进制文件完成上传时调用此URI。 URI可以是绝对URI或相对URI，客户端应能处理其中任何一个URI。 即，该值可以是或查 `"https://author.acme.com/content/dam.completeUpload.json"` 看完 `"/content/dam.completeUpload.json"` 成 [上传](#complete-upload)。
* `folderPath` （字符串）: 上载二进制文件的文件夹的完整路径。
* `(files)` （阵列）: 元素列表，其长度和顺序将与初始化请求中提供的二进制信息列表的长度和顺序相匹配。
* `fileName` （字符串）: 相应二进制的名称，如启动请求中提供。 此值应包括在完整请求中。
* `mimeType` （字符串）: 相应二进制的MIME类型，如在启动请求中提供。 此值应包括在完整请求中。
* `uploadToken` （字符串）: 相应二进制文件的上传令牌。 此值应包括在完整请求中。
* `uploadURIs` （阵列）: 字符串的列表，其值为应将二进制内容上载到的完整URI(请参阅上 [载二进制](#upload-binary))。
* `minPartSize` （数字）: 如果存在多个URI，则可能提供给任何一个uploadURI的数据的最小长度（以字节为单位）。
* `maxPartSize` （数字）: 如果存在多个URI，则可能提供给任何一个uploadURI的数据的最大长度（以字节为单位）。

### 上传二进制文件 {#upload-binary}

启动上传的输出将包括一个或多个上传URI值。 如果提供了多个URI，则客户端有责任按顺序将二进制文件“拆分”为各个部分，并对每个URI进行POST。 必须使用所有URI，且每个部件必须大于最小大小并小于启动响应中指定的最大大小。 这些请求将由CDN边缘节点前端，以加速二进制文件的上传。

实现此目的的一种潜在方法是根据API提供的上传URI数计算部件大小。 示例假定二进制文件的总大小为20,000字节，上传URI的数量为2:

* 通过将总大小除以URI数计算部件大小： 20,000 / 2 = 10,000
* 上传URI列表中二进制到第一个URI的POST字节范围0-9,999
* POST字节范围10,000 —— 上载URI列表中二进制到第二个URI的19,999

如果成功，服务器将使用状态代码对每个请求 `201` 做出响应。

### 完成上传 {#complete-upload}

在上载二进制文件的所有部分后，将HTTP POST请求提交到由启动数据提供的完整URI。 请求主体的内容类型应为表 `application/x-www-form-urlencoded` 单数据，包含以下字段。

| 字段 | 类型 | 必需或不需要 | 描述 |
|---|---|---|---|
| `fileName` | 字符串 | 必填 | 资产的名称，由初始数据提供。 |
| `mimeType` | 字符串 | 必填 | 二进制的HTTP内容类型，由启动数据提供。 |
| `uploadToken` | 字符串 | 必填 | 二进制的上传令牌，由启动数据提供。 |
| `createVersion` | 布尔型 | 可选 | 如 `True` 果具有指定名称的资产已存在，则Experience Manager会创建该资产的新版本。 |
| `versionLabel` | 字符串 | 可选 | 如果创建了新版本，则与新版本的资产关联的标签。 |
| `versionComment` | 字符串 | 可选 | 如果创建了新版本，则与该版本关联的注释。 |
| `replace` | 布尔型 | 可选 | 如 `True` 果具有指定名称的资产已存在，Experience Manager会删除该资产，然后重新创建它。 |

>!![NOTE]
>
> 如果资产已存在且未 `createVersion` 指 `replace` 定，则Experience Manager会使用新的二进制文件更新资产的当前版本。

与启动过程一样，完整请求数据可能包含多个文件的信息。

直到为文件调用完整URL后，才会完成上传二进制文件的过程。 即使文件的二进制文件全部上传，资产也不会由实例处理，直到其上传过程完成。

如果成功，服务器将使用状态 `200` 代码做出响应。

### 开源上传库 {#open-source-upload-library}

要进一步了解上传算法或构建您自己的上传脚本和工具，Adobe提供开放源码库和工具作为起点：

* [开放源aem上传库](https://github.com/adobe/aem-upload)
* [开源命令行工具](https://github.com/adobe/aio-cli-plugin-aem)

### 已弃用的资产上传API {#deprecated-asset-upload-api}

<!-- #ENGCHECK review / update the list of deprecated APIs below. -->

对于Adobe Experience Manager作为云服务，仅支持新上传API。 Adobe Experience Manager 6.5中的API已弃用。 与上传或更新资产或演绎版（任何二进制上传）相关的方法在以下API中已弃用：

* [AEM Assets HTTP API](mac-api-assets.md)
* `AssetManager` Java API，如 `AssetManager.createAsset(..)`

>[!MORELIKETHIS]
* [开放源aem上传库](https://github.com/adobe/aem-upload)。
* [开源命令行工具](https://github.com/adobe/aio-cli-plugin-aem)。


## 资产处理和后处理工作流 {#post-processing-workflows}

在Experience Manager中，资产处理基于使用资产 **[!UICONTROL 微服务的]** “处理 [用户档案](asset-microservices-configure-and-use.md#get-started-using-asset-microservices)”配置进行。 处理不需要开发人员扩展。

对于后处理工作流配置，请使用带有自定义步骤的扩展的标准工作流。

## 后处理工作流中的工作流步骤支持 {#post-processing-workflows-steps}

从先前版本的Experience Manager升级为Experience Manager作为云服务的客户可以使用资产微服务处理资产。 云本机资产微服务的配置和使用更简单。 不支持在先前版本的DAM [!UICONTROL 更新资产工作流中使用] 的几个工作流步骤。

Experience Manager作为云服务支持以下工作流步骤。

* `com.day.cq.dam.similaritysearch.internal.workflow.process.AutoTagAssetProcess`
* `com.day.cq.dam.core.impl.process.CreateAssetLanguageCopyProcess`
* `com.day.cq.wcm.workflow.process.CreateVersionProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.StartTrainingProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.TransferTrainingDataProcess`
* `com.day.cq.dam.core.impl.process.TranslateAssetLanguageCopyProcess`
* `com.day.cq.dam.core.impl.process.UpdateAssetLanguageCopyProcess`
* `com.adobe.cq.workflow.replication.impl.ReplicationWorkflowProcess`
* `com.day.cq.dam.core.impl.process.DamUpdateAssetWorkflowCompletedProcess`

以下技术工作流模型将替换为资产微型服务，或者该支持不可用。

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
