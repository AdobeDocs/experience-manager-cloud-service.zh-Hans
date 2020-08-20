---
title: 数字资产管理的开发人 [!DNL Adobe Experience Manager] 员参考是Cloud Service。
description: '[!DNL资产] API和开发人员参考内容可让您管理资产，包括二进制文件、元数据、演绎版、注释 [!DNL Content Fragments]。'
contentOwner: AG
translation-type: tm+mt
source-git-commit: cfcb9fb85cffeabc5d5af94c30bd8ace8039ac83
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 1%

---


# [!DNL Assets] API和开发人员参考资料 {#assets-cloud-service-apis}

本文包含作为Cloud Service的开发者的参考 [!DNL Assets] 材料和资源。 它包括新的上传方法、API参考以及有关在后处理工作流中提供的支持的信息。

## 资产上传 {#asset-upload-technical}

[!DNL Experience Manager] 因为Cloud Service提供了一种将资产上传到存储库的新方法。 用户可以使用HTTP API直接将资产上传到云存储。 上传二进制文件的步骤有：

1. [提交HTTP请求](#initiate-upload)。 它通知 [!DNL Experience Manage]或部署您上传新二进制文件的意图。
1. [将二进制内容POST](#upload-binary) 到由启动请求提供的一个或多个URI。
1. [提交HTTP请求](#complete-upload) ，通知服务器二进制内容已成功上传。

![直接二进制上传协议概述](assets/add-assets-technical.png)

该方法提供了可伸缩、更高效的资产上传处理。 与6.5相比 [!DNL Experience Manager] 的区别是：

* 二进制文件不会 [!DNL Experience Manager]执行，现在只需将上传过程与为部署配置的二进制云存储进行协调。
* 二进制云存储可与内容投放网络(CDN)或边缘网络一起使用。 CDN会选择更接近客户端的上传端点。 当数据传输到附近端点的距离较短时，上传性能和用户体验会得到改善，尤其对于地理上分布的团队而言。

>[!NOTE]
>
>请参阅在开源aem上传库中实现此方 [法的客户端代码](https://github.com/adobe/aem-upload)。

### 启动上传 {#initiate-upload}

将HTTPPOST请求提交到所需的文件夹。 资产会在此文件夹中创建或更新。 包括选择 `.initiateUpload.json` 器以指示请求是启动二进制文件的上传。 例如，应创建资产的文件夹的路径为 `/assets/folder`。 POST请求为 `POST https://[aem_server]:[port]/content/dam/assets/folder.initiateUpload.json`。

请求主体的内容类型应为表 `application/x-www-form-urlencoded` 单数据，其中包含以下字段：

* `(string) fileName`: 必填. 资产在中显示的名称 [!DNL Experience Manager]。
* `(number) fileSize`: 必填. 要上传的资产的文件大小（以字节为单位）。

只要每个二进制文件都包含必填字段，单个请求就可以用于启动多个二进制文件的上载。 如果请求成功，则请求将以 `201` 下格式以状态代码和包含JSON数据的正文进行响应：

```json
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

* `completeURI` （字符串）:二进制文件完成上传时调用此URI。 URI可以是绝对URI或相对URI，客户端应能处理其中任何一个URI。 即，该值可以是或查 `"https://author.acme.com/content/dam.completeUpload.json"` 看完 `"/content/dam.completeUpload.json"` 成 [上传](#complete-upload)。
* `folderPath` （字符串）:上载二进制文件的文件夹的完整路径。
* `(files)` （阵列）:元素列表，其长度和顺序与初始化请求中提供的二进制信息列表的长度和顺序相匹配。
* `fileName` （字符串）:相应二进制的名称，如启动请求中提供。 此值应包括在完整请求中。
* `mimeType` （字符串）:相应二进制的MIME类型，如启动请求中提供。 此值应包括在完整请求中。
* `uploadToken` （字符串）:相应二进制文件的上传令牌。 此值应包括在完整请求中。
* `uploadURIs` （阵列）:字符串的列表，其值为应将二进制内容上载到的完整URI(请参阅上 [载二进制](#upload-binary))。
* `minPartSize` （数字）:如果存在多个URI，则可能提供给任何一个uploadURI的数据的最小长度（以字节为单位）。
* `maxPartSize` （数字）:如果存在多个URI，则可能提供给任何一个uploadURI的数据的最大长度（以字节为单位）。

### 上传二进制文件 {#upload-binary}

启动上传的输出包括一个或多个上传URI值。 如果提供了多个URI，则客户端将二进制文件拆分为多个部分，并按顺序对每个URI发出POST请求。 使用所有URI。 确保每个部件的大小都在初始化响应中指定的最小和最大大小范围内。 CDN边缘节点有助于加速请求的二进制文件上传。

实现此目的的一种可能方法是根据API提供的上传URI数计算部件大小。 例如，假定二进制文件的总大小为20,000字节，上传URI的数量为2。 然后，按照以下步骤操作：

* 通过将总大小除以URI数计算部件大小：20,000 / 2 = 10,000。
* POST字节范围0-9,999到上传URI列表中的第一个URI。
* POST字节范围10,000 —— 在上传URI列表中，二进制到第二个URI的19,999。

如果上载成功，服务器将使用状态代码对每个请求 `201` 做出响应。

### 完成上传 {#complete-upload}

在上载二进制文件的所有部分后，将HTTPPOST请求提交到由启动数据提供的完整URI。 请求主体的内容类型应为表 `application/x-www-form-urlencoded` 单数据，包含以下字段。

| 字段 | 类型 | 必需或不需要 | 描述 |
|---|---|---|---|
| `fileName` | 字符串 | 必填 | 资产的名称，由初始数据提供。 |
| `mimeType` | 字符串 | 必填 | 二进制的HTTP内容类型，由启动数据提供。 |
| `uploadToken` | 字符串 | 必填 | 二进制的上传令牌，由启动数据提供。 |
| `createVersion` | 布尔型 | 可选 | 如果 `True` 资产存在且具有指定名称，则 [!DNL Experience Manager] 会创建该资产的新版本。 |
| `versionLabel` | 字符串 | 可选 | 如果创建了新版本，则与新版本的资产关联的标签。 |
| `versionComment` | 字符串 | 可选 | 如果创建了新版本，则与该版本关联的注释。 |
| `replace` | 布尔型 | 可选 | 如果 `True` 资产存在且具有指定名称， [!DNL Experience Manager] 则删除该资产，然后重新创建它。 |

>!![NOTE]
如果资产存在且 `createVersion` 未指定 `replace` 或未指定， [!DNL Experience Manager] 则使用新的二进制文件更新资产的当前版本。

与启动过程一样，完整请求数据可能包含多个文件的信息。

直到为文件调用完整URL后，才会完成上传二进制文件的过程。 资产会在上传流程完成后进行处理。 即使资产的二进制文件上传完毕，但上传过程未完成，处理也不会开始。

如果成功，服务器将使用状态 `200` 代码做出响应。

### 开源上传库 {#open-source-upload-library}

要进一步了解上传算法或构建您自己的上传脚本和工具，Adobe提供开放源码库和工具：

* [开放源aem上传库](https://github.com/adobe/aem-upload)。
* [开源命令行工具](https://github.com/adobe/aio-cli-plugin-aem)。

### 已弃用的资产上传API {#deprecated-asset-upload-api}

<!-- #ENGCHECK review / update the list of deprecated APIs below. -->

新的上传方法仅支持 [!DNL Adobe Experience Manager] 作为Cloud Service。 不建议使 [!DNL Adobe Experience Manager] 用6.5中的API。 与上传或更新资产或演绎版（任何二进制上传）相关的方法在以下API中已弃用：

* [Experience Manager资产HTTP API](mac-api-assets.md)
* `AssetManager` Java API，如 `AssetManager.createAsset(..)`

>[!MORELIKETHIS]
* [开放源aem上传库](https://github.com/adobe/aem-upload)。
* [开源命令行工具](https://github.com/adobe/aio-cli-plugin-aem)。


## 资产处理和后处理工作流 {#post-processing-workflows}

在中 [!DNL Experience Manager]，资产处理基于使用资 **[!UICONTROL 产微服务的]** 处理用户档案 [](asset-microservices-configure-and-use.md#get-started-using-asset-microservices)配置。 处理不需要开发人员扩展。

对于后处理工作流配置，请使用带有自定义步骤的扩展的标准工作流。

## 后处理工作流中的工作流步骤支持 {#post-processing-workflows-steps}

从旧版本升级的客户可 [!DNL Experience Manager] 以使用资产微服务处理资产。 云本机资产微服务的配置和使用更简单。 不支持在先前版本的DAM [!UICONTROL 更新资产工作流中使用] 的几个工作流步骤。

[!DNL Experience Manager] 作为Cloud Service，支持以下工作流步骤：

* `com.day.cq.dam.similaritysearch.internal.workflow.process.AutoTagAssetProcess`
* `com.day.cq.dam.core.impl.process.CreateAssetLanguageCopyProcess`
* `com.day.cq.wcm.workflow.process.CreateVersionProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.StartTrainingProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.TransferTrainingDataProcess`
* `com.day.cq.dam.core.impl.process.TranslateAssetLanguageCopyProcess`
* `com.day.cq.dam.core.impl.process.UpdateAssetLanguageCopyProcess`
* `com.adobe.cq.workflow.replication.impl.ReplicationWorkflowProcess`
* `com.day.cq.dam.core.impl.process.DamUpdateAssetWorkflowCompletedProcess`

以下技术工作流模型将替换为资产微型服务，或者该支持不可用：

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

>[!MORELIKETHIS]
* [Experience Cloud作为Cloud ServiceSDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)。

