---
title: 的开发人员参考 [!DNL Assets]
description: '"[!DNL Assets] API和开发人员参考内容允许您管理资产，包括二进制文件、元数据、演绎版、评论和 [!DNL Content Fragments]."'
contentOwner: AG
feature: APIs,Assets HTTP API
role: Developer,Architect,Admin
exl-id: c75ff177-b74e-436b-9e29-86e257be87fb
source-git-commit: 57abdf0198e646719bbb818e2b70d772579ba548
workflow-type: tm+mt
source-wordcount: '1811'
ht-degree: 4%

---

# [!DNL Adobe Experience Manager Assets] 开发人员用例、 API和参考资料 {#assets-cloud-service-apis}

本文包含面向 [!DNL Assets] as a [!DNL Cloud Service]. 它包括新的资产上传模块、API引用，以及有关后处理工作流中提供支持的信息。

## [!DNL Experience Manager Assets] API和操作 {#use-cases-and-apis}

[!DNL Assets] as a [!DNL Cloud Service] 提供了多个API以编程方式与数字资产交互。 每个API都支持特定的用例，如下表所述。 的 [!DNL Assets] 用户界面， [!DNL Experience Manager] 桌面应用程序和 [!DNL Adobe Asset Link] 支持所有或部分操作。

>[!CAUTION]
>
>某些API仍然存在，但不受支持(表示为×)。 请尽量不要使用这些API。

| 支持级别 | 描述 |
| ------------- | --------------------------- |
| ✓ | 支持 |
| × | 不受支持. 请勿使用。 |
| - | 不可用 |

| 用例 | [aem-upload](https://github.com/adobe/aem-upload) | [Experience Manager/ Sling / JCR](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html) Java API | [Asset compute服务](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html) | [[!DNL Assets] HTTP API](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/mac-api-assets.html#create-an-asset) | Sling [GET](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) / [POST](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html) Servlet | [GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html?lang=zh-Hans) |
| ----------------|:---:|:---:|:---:|:---:|:---:|:---:|
| **原始二进制** |  |  |  |  |  |  |
| 创建原始 | ✓ | × | - | × | × | - |
| 读取原始 | - | × | ✓ | ✓ | ✓ | - |
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
| 读取CF | - | ✓ | - | ✓ | - | ✓ |
| 更新CF | - | ✓ | - | ✓ | - | - |
| 删除CF | - | ✓ | - | ✓ | - | - |
| 复制CF | - | ✓ | - | ✓ | - | - |
| 移动CF | - | ✓ | - | ✓ | - | - |
| **版本** |  |  |  |  |  |  |
| 创建版本 | ✓ | ✓ | - | - | - | - |
| 读取版本 | - | ✓ | - | - | - | - |
| 删除版本 | - | ✓ | - | - | - | - |
| **文件夹** |  |  |  |  |  |  |
| 创建文件夹 | ✓ | ✓ | - | ✓ | - | - |
| 读取文件夹 | - | ✓ | - | ✓ | - | - |
| 删除文件夹 | ✓ | ✓ | - | ✓ | - | - |
| 复制文件夹 | ✓ | ✓ | - | ✓ | - | - |
| 移动文件夹 | ✓ | ✓ | - | ✓ | - | - |

## 资产上传 {#asset-upload}

在 [!DNL Experience Manager] as a [!DNL Cloud Service]，您可以使用HTTP API直接将资产上传到云存储。 下面是上载二进制文件的步骤。 在外部应用程序中执行这些步骤，而不是在 [!DNL Experience Manager] JVM。

1. [提交HTTP请求](#initiate-upload). 它会通知 [!DNL Experience Manage]或部署您上传新二进制文件的意图。
1. [PUT二进制文件的内容](#upload-binary) 到由启动请求提供的一个或多个URI。
1. [提交HTTP请求](#complete-upload) 通知服务器二进制文件的内容已成功上传。

![直接二进制上传协议概述](assets/add-assets-technical.png)

>[!IMPORTANT]
在外部应用程序中而不是 [!DNL Experience Manager] JVM。

该方法可以对资产上传进行可伸缩、更高性能的处理。 与 [!DNL Experience Manager] 6.5为：

* 二进制文件不会通过 [!DNL Experience Manager]，现在只需将上传过程与为部署配置的二进制云存储进行协调即可。
* 二进制云存储可与内容交付网络(CDN)或边缘网络配合使用。 CDN会选择更接近客户端的上传端点。 当数据传输到附近端点的距离较短时，上传性能和用户体验会得到改善，尤其是对于地理上分散的团队而言。

>[!NOTE]
请参阅客户端代码以在开源环境中实施此方法 [aem上传库](https://github.com/adobe/aem-upload).

### 启动上传 {#initiate-upload}

将HTTPPOST请求提交到所需的文件夹。 资产会在此文件夹中创建或更新。 包含选择器 `.initiateUpload.json` 以指示请求启动二进制文件的上传。 例如，应创建资产的文件夹的路径是 `/assets/folder`. POST请求为 `POST https://[aem_server]:[port]/content/dam/assets/folder.initiateUpload.json`.

请求正文的内容类型应为 `application/x-www-form-urlencoded` 表单数据，包含以下字段：

* `(string) fileName`: 必填. 资产在中显示的名称 [!DNL Experience Manager].
* `(number) fileSize`: 必填. 上传资产的文件大小（以字节为单位）。

只要每个二进制文件包含必填字段，就可以使用单个请求启动多个二进制文件的上传。 如果成功，请求将以 `201` 状态代码和包含以下格式JSON数据的正文：

```json
{
    "completeURI": "(string)",
    "folderPath": "(string)",
    "files": [
        {
            "fileName": "(string)",
            "mimeType": "(string)",
            "uploadToken": "(string)",
            "uploadURIs": [
                "(string)"
            ],
            "minPartSize": (number),
            "maxPartSize": (number)
        }
    ]
}
```

* `completeURI` （字符串）：在二进制文件完成上传时调用此URI。 URI可以是绝对URI或相对URI，客户端应该能够处理这两个URI。 即，值可以是 `"https://[aem_server]:[port]/content/dam.completeUpload.json"` 或 `"/content/dam.completeUpload.json"` 请参阅 [完成上载](#complete-upload).
* `folderPath` （字符串）：上传二进制文件的文件夹的完整路径。
* `(files)` （数组）：元素列表，其长度和顺序与启动请求中提供的二进制信息列表的长度和顺序相匹配。
* `fileName` （字符串）：相应二进制文件的名称，在启动请求中提供。 此值应包含在完整请求中。
* `mimeType` （字符串）：相应二进制文件的mime类型，在启动请求中提供。 此值应包含在完整请求中。
* `uploadToken` （字符串）：对应二进制文件的上传令牌。 此值应包含在完整请求中。
* `uploadURIs` （数组）：其值是应将二进制内容上传到的完整URI的字符串列表(请参阅 [上载二进制文件](#upload-binary))。
* `minPartSize` （数字）：可提供给任何 `uploadURIs`，如果有多个URI。
* `maxPartSize` （数字）：可提供给 `uploadURIs`，如果有多个URI。

### 上载二进制文件 {#upload-binary}

启动上传的输出包括一个或多个上传URI值。 如果提供了多个URI，则客户端可以将二进制文件拆分为多个部分，并按顺序向提供的上传URI发出每个部分的PUT请求。 如果选择将二进制文件拆分为多个部分，请遵循以下准则：

* 除最后一个部件外，每个部件的大小必须大于或等于 `minPartSize`.
* 每个零件的大小必须小于或等于 `maxPartSize`.
* 如果二进制文件的大小超过 `maxPartSize`，将二进制文件拆分为多个部分以上传。
* 您不必使用所有URI。

如果二进制文件的大小小于或等于 `maxPartSize`，您可以将整个二进制文件上传到单个上传URI。 如果提供了多个上传URI，请使用第一个URI并忽略其余URI。 您不必使用所有URI。

CDN边缘节点有助于加快请求的二进制文件上传。

要实现此目的，最简单的方法是使用 `maxPartSize` 作为零件尺寸。 如果将此值用作部件大小，则API合同可保证有足够的上传URI来上传二进制文件。 要实现此目的，请将二进制文件拆分为部分大小 `maxPartSize`，按顺序为每个部件使用一个URI。 最终零件可以是小于或等于的任意大小 `maxPartSize`. 例如，假定二进制文件的总大小为20,000字节， `minPartSize` 是5,000字节， `maxPartSize` 为8,000字节，上传URI的数量为5。 执行以下步骤：

* 使用第一个上传URI上传二进制文件的前8,000字节。
* 使用第二个上传URI上传二进制文件的第二个8,000字节。
* 使用第三个上传URI上传二进制文件的最后4,000字节。 由于这是最后一部分，因此它不必大于 `minPartSize`.
* 您无需使用最后两个上传URI。 你可以忽略它们。

一个常见错误是，根据API提供的上传URI数量计算部件大小。 API合同不保证此方法有效，实际上可能会产生超出这两种方法之间范围的部件大小 `minPartSize` 和 `maxPartSize`. 这可能会导致二进制上传失败。

同样，最简单、最安全的方法是简单地使用大小等于 `maxPartSize`.

如果上传成功，服务器将使用 `201` 状态代码。

>[!NOTE]
有关上传算法的更多信息，请参阅 [官方功能文档](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html#Upload) 和 [API文档](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/api/binary/BinaryUpload.html) 在Apache Jackrabbit Oak项目中。

### 完成上传 {#complete-upload}

上传二进制文件的所有部分后，将HTTPPOST请求提交到初始数据提供的完整URI。 请求正文的内容类型应为 `application/x-www-form-urlencoded` 表单数据，包含以下字段。

| 字段 | 类型 | 必需或不需要 | 描述 |
|---|---|---|---|
| `fileName` | 字符串 | 必填 | 初始数据提供的资产名称。 |
| `mimeType` | 字符串 | 必填 | 二进制文件的HTTP内容类型，由启动数据提供。 |
| `uploadToken` | 字符串 | 必填 | 初始化数据提供的二进制文件的上载令牌。 |
| `createVersion` | 布尔型 | 可选 | 如果 `True` ，且存在具有指定名称的资产，则 [!DNL Experience Manager] 创建资产的新版本。 |
| `versionLabel` | 字符串 | 可选 | 如果创建了新版本，则会显示与资产新版本关联的标签。 |
| `versionComment` | 字符串 | 可选 | 如果创建了新版本，则与该版本关联的注释。 |
| `replace` | 布尔型 | 可选 | 如果 `True` 并且存在具有指定名称的资产， [!DNL Experience Manager] 删除资产，然后重新创建资产。 |
| `uploadDuration` | 数值 | 可选 | 文件完整上传的总时间（以毫秒为单位）。 如果指定，则上载持续时间将包含在系统的日志文件中，用于传输率分析。 |
| `fileSize` | 数值 | 可选 | 文件的大小（以字节为单位）。 如果指定，则文件大小将包含在系统的日志文件中，用于传输速率分析。 |

>[!NOTE]
如果资产存在且 `createVersion` nor `replace` ，则 [!DNL Experience Manager] 使用新的二进制文件更新资产的当前版本。

与启动过程一样，完整的请求数据可能包含多个文件的信息。

只有在为文件调用完整URL后，才会完成上传二进制文件的过程。 上传过程完成后，会处理资产。 即使资产的二进制文件已完全上传，但上传过程未完成，处理也不会开始。 如果上传成功，服务器将回复 `200` 状态代码。

### 开源上载库 {#open-source-upload-library}

要了解有关上传算法的更多信息或构建您自己的上传脚本和工具，Adobe提供了开源库和工具：

* [开源aem上传库](https://github.com/adobe/aem-upload).
* [开源命令行工具](https://github.com/adobe/aio-cli-plugin-aem).

>[!NOTE]
aem上载库和命令行工具均使用 [node-httptransfer库](https://github.com/adobe/node-httptransfer/)

### 已弃用的资产上传API {#deprecated-asset-upload-api}

<!-- #ENGCHECK review / update the list of deprecated APIs below. -->

仅支持 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service]. 来自的API [!DNL Adobe Experience Manager] 6.5已弃用。 以下API中弃用了与上传或更新资产或演绎版（任何二进制上传）相关的方法：

* [Experience Manager Assets HTTP API](mac-api-assets.md)
* `AssetManager` Java API，例如 `AssetManager.createAsset(..)`

>[!MORELIKETHIS]
* [开源aem上传库](https://github.com/adobe/aem-upload).
* [开源命令行工具](https://github.com/adobe/aio-cli-plugin-aem).
* [Apache Jackrabbit Oak文档，可直接上传](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html#Upload).


## 资产处理和后处理工作流 {#post-processing-workflows}

在 [!DNL Experience Manager]，则资产处理基于 **[!UICONTROL 处理配置文件]** 使用 [资产微服务](asset-microservices-configure-and-use.md#get-started-using-asset-microservices). 处理不需要开发人员扩展。

对于后处理工作流配置，请使用带有自定义步骤的扩展的标准工作流。

## 在后处理工作流中支持工作流步骤 {#post-processing-workflows-steps}

如果您从以前的 [!DNL Experience Manager]，则可以使用资产微服务处理资产。 云原生资产微服务的配置和使用更简单。 在 [!UICONTROL DAM更新资产] 不支持以前版本中的工作流。 有关支持类的更多信息，请参阅 [Java API引用或Javaocs](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html).

以下技术工作流模型已被资产微服务取代，或者无法获得支持：

* `com.day.cq.dam.cameraraw.process.CameraRawHandlingProcess`
* `com.day.cq.dam.core.process.CommandLineProcess`
* `com.day.cq.dam.pdfrasterizer.process.PdfRasterizerHandlingProcess`
* `com.day.cq.dam.core.process.AddPropertyWorkflowProcess`
* `com.day.cq.dam.core.process.CreateSubAssetsProcess`
* `com.day.cq.dam.core.process.DownloadAssetProcess`
* `com.day.cq.dam.word.process.ExtractImagesProcess`
* `com.day.cq.dam.word.process.ExtractPlainProcess`
* `com.day.cq.dam.ids.impl.process.IDSJobProcess`
* `com.day.cq.dam.indd.process.INDDMediaExtractProcess`
* `com.day.cq.dam.indd.process.INDDPageExtractProcess`
* `com.day.cq.dam.core.impl.lightbox.LightboxUpdateAssetProcess`
* `com.day.cq.dam.pim.impl.sourcing.upload.process.ProductAssetsUploadProcess`
* `com.day.cq.dam.core.process.SendDownloadAssetEmailProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.StartTrainingProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.TransferTrainingDataProcess`
* `com.day.cq.dam.switchengine.process.SwitchEngineHandlingProcess`
* `com.day.cq.dam.core.process.GateKeeperProcess`
* `com.day.cq.dam.s7dam.common.process.DMEncodeVideoWorkflowCompletedProcess`
* `com.day.cq.dam.core.process.DeleteImagePreviewProcess`
* `com.day.cq.dam.video.FFMpegTranscodeProcess`
* `com.day.cq.dam.core.process.ThumbnailProcess`
* `com.day.cq.dam.video.FFMpegThumbnailProcess`
* `com.day.cq.dam.core.process.CreateWebEnabledImageProcess`
* `com.day.cq.dam.core.process.CreatePdfPreviewProcess`
* `com.day.cq.dam.s7dam.common.process.VideoUserUploadedThumbnailProcess`
* `com.day.cq.dam.s7dam.common.process.VideoThumbnailDownloadProcess`
* `com.day.cq.dam.s7dam.common.process.VideoProxyServiceProcess`
* `com.day.cq.dam.scene7.impl.process.Scene7UploadProcess`
* `com.day.cq.dam.s7dam.common.process.S7VideoThumbnailProcess`
* `com.day.cq.dam.core.process.MetadataProcessorProcess`
* `com.day.cq.dam.core.process.AssetOffloadingProcess`
* `com.adobe.cq.dam.dm.process.workflow.DMImageProcess`

<!-- Commenting the previous list documented at the time of GA. Replacing it with the updated list via cqdoc-18231.

* `com.day.cq.dam.core.process.DeleteImagePreviewProcess`
* `com.day.cq.dam.s7dam.common.process.DMEncodeVideoWorkflowCompletedProcess`
* `com.day.cq.dam.core.process.GateKeeperProcess`
* `com.day.cq.dam.core.process.AssetOffloadingProcess`
* `com.day.cq.dam.core.process.MetadataProcessorProcess`
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
-->

<!-- PPTX source: slide in add-assets.md - overview of direct binary upload section of
https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

>[!MORELIKETHIS]
* [[!DNL Experience Cloud] as a [!DNL Cloud Service] SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md).

