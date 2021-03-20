---
title: ' [!DNL Assets]的开发人员参考'
description: '[!DNL Assets] APIs and developer reference content lets you manage assets, including binary files, metadata, renditions, comments, and [!DNL Content Fragments]。'
contentOwner: AG
translation-type: tm+mt
source-git-commit: 77b4d9f07626419ddab3a7363b06c382447ec982
workflow-type: tm+mt
source-wordcount: '1400'
ht-degree: 2%

---


# [!DNL Adobe Experience Manager Assets] API和开发人员参考资料  {#assets-cloud-service-apis}

本文包含为[!DNL Assets]开发者提供的[!DNL Cloud Service]的建议、参考材料和资源。 它包括新的资产上传模块、API参考以及有关后处理工作流中提供的支持的信息。

## [!DNL Experience Manager Assets] API和操作  {#use-cases-and-apis}

[!DNL Assets] as提供 [!DNL Cloud Service] 了多个API以与数字资产进行编程交互。每个API都支持下表所述的特定用例。 [!DNL Assets]用户界面、[!DNL Experience Manager]桌面应用程序和[!DNL Adobe Asset Link]支持所有或部分操作。

>[!CAUTION]
>
>某些API仍然存在，但不受主动支持（用×表示），因此不得使用。

| 支持级别 | 描述 |
| ------------- | --------------------------- |
| ✓ | 支持 |
| × | 不受支持. 不要使用。 |
| - | 不可用 |

| 用例 | [aem-upload](https://github.com/adobe/aem-upload) | [AEM / Sling / ](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/index.html) JCRJava API | [Asset compute服务](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html) | [[!DNL Assets] HTTP API](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/mac-api-assets.html#create-an-asset) | Sling [GET](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) / [POST](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html) Servlet | [GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) _(预览)_ |
| ----------------|:---:|:---:|:---:|:---:|:---:|:---:|
| **原始二进制** |  |  |  |  |  |  |
| 创建原始 | ✓ | × | - | × | × | - |
| 阅读原件 | - | × | ✓ | ✓ | ✓ | - |
| 更新原始 | ✓ | × | ✓ | × | × | - |
| 删除原始 | - | ✓ | - | ✓ | ✓ | - |
| 复制原始 | - | ✓ | - | ✓ | ✓ | - |
| 移动原始 | - | ✓ | - | ✓ | ✓ | - |
| **元数据** |  |  |  |  |  |  |
| 创建元数据 | - | ✓ | ✓ | ✓ | ✓ | - |
| 读取元数据 | - | ✓ | - | ✓ | ✓ | - |
| 更新元数据 | - | ✓ | ✓ | ✓ | ✓ | - |
| 删除元数据 | - | ✓ | ✓ | ✓ | ✓ | - |
| 复制元数据 | - | ✓ | - | ✓ | ✓ | - |
| 移动元数据 | - | ✓ | - | ✓ | ✓ | - |
| **内容片段(CF)** |  |  |  |  |  |  |
| 创建CF | - | ✓ | - | ✓ | - | - |
| 阅读CF | - | ✓ | - | ✓ | - | ✓ |
| 更新CF | - | ✓ | - | ✓ | - | - |
| 删除CF | - | ✓ | - | ✓ | - | - |
| 复制CF | - | ✓ | - | ✓ | - | - |
| 移动CF | - | ✓ | - | ✓ | - | - |
| **版本** |  |  |  |  |  |  |
| 创建版本 | ✓ | ✓ | - | - | - | - |
| 阅读版本 | - | ✓ | - | - | - | - |
| 删除版本 | - | ✓ | - | - | - | - |
| **文件夹** |  |  |  |  |  |  |
| 创建文件夹 | ✓ | ✓ | - | ✓ | - | - |
| 读取文件夹 | - | ✓ | - | ✓ | - | - |
| 删除文件夹 | ✓ | ✓ | - | ✓ | - | - |
| 复制文件夹 | ✓ | ✓ | - | ✓ | - | - |
| 移动文件夹 | ✓ | ✓ | - | ✓ | - | - |

## 资产上传{#asset-upload-technical}

[!DNL Experience Manager] as提供 [!DNL Cloud Service] 了将资产上传到存储库的新方法。用户可以使用HTTP API直接将资产上传到云存储。 上载二进制文件的步骤有：

1. [提交HTTP请求](#initiate-upload)。它将通知[!DNL Experience Manage]r部署您上传新二进制文件的意图。
1. [将二进制内容](#upload-binary) POST到由启动请求提供的一个或多个URI。
1. [提交HTTP请](#complete-upload) 求以通知服务器二进制内容已成功上载。

![直接二进制上传协议概述](assets/add-assets-technical.png)

该方法为资产上传提供了可扩展且更高性能的处理。 与[!DNL Experience Manager] 6.5相比的差异是：

* 二进制文件不会通过[!DNL Experience Manager]，现在，它只是将上载过程与为部署配置的二进制云存储进行协调。
* 二进制云存储可与内容投放网络(CDN)或Edge网络一起使用。 CDN会选择更靠近客户端的上载端点。 当数据传输到附近端点的距离较短时，上载性能和用户体验会得到改善，对于地理上分布的团队而言尤其如此。

>[!NOTE]
请参阅在开放源[aem-upload库](https://github.com/adobe/aem-upload)中实现此方法的客户端代码。

### 启动上载{#initiate-upload}

将HTTPPOST请求提交到所需的文件夹。 此时会在此文件夹中创建或更新资产。 包含选择器`.initiateUpload.json`，以指示请求将启动二进制文件的上载。 例如，应创建资产的文件夹的路径为`/assets/folder`。 POST请求为`POST https://[aem_server]:[port]/content/dam/assets/folder.initiateUpload.json`。

请求正文的内容类型应为`application/x-www-form-urlencoded`表单数据，包含以下字段：

* `(string) fileName`: 必填. 资产在[!DNL Experience Manager]中显示的名称。
* `(number) fileSize`: 必填. 要上传的资产的文件大小（以字节为单位）。

只要每个二进制文件都包含必填字段，单个请求就可以用于启动多个二进制文件的上载。 如果成功，请求将以`201`状态代码和包含JSON数据的正文进行响应，格式如下：

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

* `completeURI` （字符串）：当二进制文件上载完成时，调用此URI。URI可以是绝对URI或相对URI，客户端应能够处理其中任何一个。 也就是说，该值可以是`"https://author.acme.com/content/dam.completeUpload.json"`或`"/content/dam.completeUpload.json"`请参阅[完整上载](#complete-upload)。
* `folderPath` （字符串）：上载二进制文件夹的完整路径。
* `(files)` （数组）：元素的列表，其长度和顺序与在启动请求中提供的二进制信息的列表的长度和顺序相匹配。
* `fileName` （字符串）：相应二进制的名称，在启动请求中提供。此值应包括在完整请求中。
* `mimeType` （字符串）：相应二进制的MIME类型，在启动请求中提供。此值应包括在完整请求中。
* `uploadToken` （字符串）：对应二进制文件的上载令牌。此值应包括在完整请求中。
* `uploadURIs` （数组）：一个字符串列表，其值是应将二进制内容上载到的完整URI(请参阅上 [载二进制](#upload-binary))。
* `minPartSize` （数）：如果存在多个URI，则可能提供给任何一个uploadURI的数据的最小长度（以字节为单位）。
* `maxPartSize` （数）：如果存在多个URI，则可能提供给任何一个uploadURI的数据的最大长度（以字节为单位）。

### 上传二进制{#upload-binary}

启动上载的输出包括一个或多个上载URI值。 如果提供了多个URI，则客户端将二进制文件拆分为多个部分，并按顺序对每个URI发出每个部分的POST请求。 使用所有URI。 确保每个部件的大小在初始化响应中指定的最小和最大大小范围内。 CDN边缘节点有助于加快二进制文件的请求上传。

实现此目的的一种可能方法是根据API提供的上载URI数计算部件大小。 例如，假设二进制文件的总大小为20,000字节，而上载URI的数量为2。 然后，按照以下步骤操作：

* 通过将总大小除以URI数来计算部件大小：20,000 / 2 = 10,000。
* POST字节范围0-9,999，在上传URI的列表，二进制到第一个URI。
* POST字节范围10,000 — 上载URI列表中二进制到第二个URI的19,999。

如果上载成功，服务器将使用`201`状态代码对每个请求做出响应。

### 完成上载{#complete-upload}

在上载二进制文件的所有部分后，将HTTPPOST请求提交到由启动数据提供的完整URI。 请求正文的内容类型应为`application/x-www-form-urlencoded`表单数据，包含以下字段。

| 字段 | 类型 | 必需或不需要 | 描述 |
|---|---|---|---|
| `fileName` | 字符串 | 必填 | 资产名称，由启动数据提供。 |
| `mimeType` | 字符串 | 必填 | 二进制的HTTP内容类型，由启动数据提供。 |
| `uploadToken` | 字符串 | 必填 | 正如启动数据提供的那样，为二进制上载令牌。 |
| `createVersion` | 布尔型 | 可选 | 如果`True`和具有指定名称的资产存在，则[!DNL Experience Manager]会创建该资产的新版本。 |
| `versionLabel` | 字符串 | 可选 | 如果创建了新版本，则与新版本的资产关联的标签。 |
| `versionComment` | 字符串 | 可选 | 如果创建了新版本，则与该版本关联的注释。 |
| `replace` | 布尔型 | 可选 | 如果`True`和具有指定名称的资产存在，则[!DNL Experience Manager]将删除该资产，然后重新创建该资产。 |

>[!NOTE]
如果资产存在且未指定`createVersion`或`replace`，则[!DNL Experience Manager]会使用新的二进制文件更新资产的当前版本。

与启动过程一样，完整的请求数据可能包含多个文件的信息。

在为文件调用完整URL之前，不会完成上传二进制文件的过程。 资产会在上传流程完成后进行处理。 即使资产的二进制文件上传完全但上传过程未完成，处理也不会开始。

如果成功，服务器将使用`200`状态代码做出响应。

### 开放源上载库{#open-source-upload-library}

要进一步了解上传算法或构建您自己的上传脚本和工具，Adobe提供开放源代码库和工具：

* [开放源aem-upload库](https://github.com/adobe/aem-upload)。
* [开源命令行工具](https://github.com/adobe/aio-cli-plugin-aem)。

### 已弃用的资产上传API {#deprecated-asset-upload-api}

<!-- #ENGCHECK review / update the list of deprecated APIs below. -->

仅[!DNL Adobe Experience Manager]作为[!DNL Cloud Service]支持新上载方法。 [!DNL Adobe Experience Manager] 6.5中的API已弃用。 与上传或更新资产或演绎版（任何二进制上传）相关的方法在以下API中已弃用：

* [Experience Manager资源HTTP API](mac-api-assets.md)
* `AssetManager` Java API，如  `AssetManager.createAsset(..)`

>[!MORELIKETHIS]
* [开放源aem-upload库](https://github.com/adobe/aem-upload)。
* [开源命令行工具](https://github.com/adobe/aio-cli-plugin-aem)。


## 资产处理和后处理工作流{#post-processing-workflows}

在[!DNL Experience Manager]中，资产处理基于使用[asset microservices](asset-microservices-configure-and-use.md#get-started-using-asset-microservices)的&#x200B;**[!UICONTROL 处理用户档案]**&#x200B;配置。 处理不需要开发人员扩展。

对于后处理工作流配置，请使用带有自定义步骤的扩展的标准工作流。

## 支持后处理工作流{#post-processing-workflows-steps}中的工作流步骤

从[!DNL Experience Manager]的先前版本升级的客户可以使用asset microservices处理资产。 云本机资产微服务的配置和使用更简单。 不支持在早期版本的[!UICONTROL DAM更新资产]工作流中使用的几个工作流步骤。

[!DNL Experience Manager] 支持 [!DNL Cloud Service] 以下工作流步骤：

* `com.day.cq.dam.similaritysearch.internal.workflow.process.AutoTagAssetProcess`
* `com.day.cq.dam.core.impl.process.CreateAssetLanguageCopyProcess`
* `com.day.cq.wcm.workflow.process.CreateVersionProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.StartTrainingProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.TransferTrainingDataProcess`
* `com.day.cq.dam.core.impl.process.TranslateAssetLanguageCopyProcess`
* `com.day.cq.dam.core.impl.process.UpdateAssetLanguageCopyProcess`
* `com.adobe.cq.workflow.replication.impl.ReplicationWorkflowProcess`
* `com.day.cq.dam.core.impl.process.DamUpdateAssetWorkflowCompletedProcess`

以下技术工作流模型由资产微服务替换，或者该支持不可用：

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
* [Experience Cloud [!DNL Cloud Service] aSDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)。

