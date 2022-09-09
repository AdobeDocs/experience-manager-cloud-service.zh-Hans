---
title: 配置转录服务
seo-title: Configure transcription service
description: Adobe Experience Manager Assets 配置了 [!DNL Azure Media Services] ，它可以自动生成 WebVTT (vtt) 格式的支持音频或视频文件中的口语文本转录。
seo-description: When an audio or video asset is processed in Experience Manager Assets, the AI-based transcription service automatically generates the text transcript rendition of the audio or video asset and stores it at the same location within your Assets repository where the original asset resides. The Experience Manager Assets transcription service allows marketers to effectively manage their audio and video content with added discoverability of the text content as well as increase the ROI of these assets by supporting accessibility and localization.
products: SG_EXPERIENCEMANAGER/ASSETS and Experience Manager as a Cloud Service
sub-product: assets
content-type: reference
contentOwner: Vishabh Gupta
topic-tags: Configuration
feature: Asset Management, Configuration
role: Admin
exl-id: e96c8d68-74a6-4d61-82dc-20e619338d4b
source-git-commit: 4edf66127696ce91466811e2ffdcfbbd73f7cc2c
workflow-type: tm+mt
source-wordcount: '1666'
ht-degree: 100%

---

# 在[!DNL Experience Manager Assets]中配置转录 {#configure-transcription-service}

转录是使用语音识别技术将音频或视频文件中的音频转换为文本（语音到文本）的过程。[!DNL Adobe Experience Manager Assets] 配置了 [!DNL Azure Media Services]，它可以自动生成 WebVTT (vtt) 格式的支持音频或视频文件中的口语文本转录。在[!DNL Experience Manager Assets] 中处理音频或视频资产时，转录服务会自动生成音频或视频资产的文本转录演绎版，并将其存储在原始资产所在的 Assets 存储库中的同一位置。[!DNL Experience Manager Assets] 转录服务允许营销人员通过增加文本内容的可发现性来有效管理其音频和视频内容，并通过支持可访问性和本地化来提高这些资产的 ROI。

转录是口语内容的文本版本；例如，您在任何 OTT 平台上观看的电影通常都包括解说词或字幕，帮助您访问或使用其他语言的内容。或任何用于营销、学习或娱乐目的的音频或视频文件。这些体验从转录开始，然后根据需要进行格式化或翻译。当手动执行时，转录音频或视频是一个很耗时间且容易出错的过程。鉴于对音频视频内容的需求不断增加，扩展手动过程也是一个挑战。[!DNL Experience Manager Assets]使用 Azure 基于人工智能的转录，允许对音频和视频资产进行大规模处理，并生成文本转录（.vtt 文件）以及时间戳细节。除了 Assets，Dynamic Media 也支持转录功能。

转录功能在 [!DNL Experience Manager Assets] 中可以免费使用。但是，管理员需要用户的 Azure 凭据才能在[!DNL Experience Manager Assets]中配置转录服务。您还可以直接从 Microsoft® 获得 [试用凭证](https://azure.microsoft.com/en-us/pricing/details/media-services/)，体验 Assets 中的音频或视频转录功能。

## 转录先决条件 {#prerequisites}

1. 启动并运行的 [!DNL Experience Manager Assets as a Cloud Service] 实例。
1. 在 [!DNL Experience Manager Assets] 中进行配置需要以下 Azure 凭据：

   * 客户端 ID（API 密钥）
   * 客户端密钥
   * 租户端点（域）
   * 媒体帐户
   * 资源组
   * 订阅 ID

   要获取访问 Azure Media Services API 的凭据，请参阅 [Azure 文档](https://docs.microsoft.com/en-us/azure/media-services/latest/access-api-howto?tabs=portal)。

1. 确保 Azure 帐户有足够的信用来处理新请求。

## 在[!DNL Experience Manager Assets]中配置转录 {#configure-transcription}

以下是在 [!DNL Experience Manager Assets] 中启用转录功能所需的配置：

1. [配置 Azure Media Services](#configure-azure-media-service)
1. [配置音频/视频转录的处理配置文件](#configure-processing-profile-for-transcription)


### 配置 Azure Media Services {#configure-azure-media-services}

[!DNL Experience Manager Assets] 使用 [!DNL Azure Media Services]，它可以自动生成 WebVTT (vtt) 格式的[支持音频或视频文件 ](#supported-file-formats-for-transcription)中的口语文本转录。管理员可使用 Azure 凭据在 [!DNL Experience Manager Assets] 中配置 [!DNL Azure Media Services]。[转录先决条件](#transcription-prerequisites)列出配置所需的[!DNL Azure]凭据。如果您没有 [!DNL Azure] 帐户和凭据，请参阅 [Azure Media Services 文档 ](https://azure.microsoft.com/en-us/pricing/details/media-services/) 获取试用凭据。

![configure-transcription-service](assets/configure-transcription-service.png)

转到&#x200B;**[!UICONTROL “工具”]**>**[!UICONTROL “Cloud Service”]**>**[!UICONTROL “Azure Media Services 配置”]**。从左栏选择一个文件夹（位置）并点击[!UICONTROL “创建”]按钮来配置与您的 [!DNL Azure] 帐户的连接。此文件夹是 Experience Manager Assets 中存储您的 [!DNL Azure] 云配置的位置。输入[!DNL Azure]凭据，然后单击&#x200B;**[!UICONTROL “保存并关闭”]**。

### 配置转录的处理配置文件 {#configure-processing-profile}

一旦在 Experience Manager Assets 中配置了[!DNL Azure Media Services]，下一步就是创建一个资产处理配置文件，用于生成音频和视频资产的基于人工智能的转录。基于人工智能的处理配置文件在 Experience Manager Assets 中生成[支持音频或视频资产](#supported-file-formats-for-transcription)的转录文件作为演绎版，并将该演绎版（.vtt 文件）存储在原始资产所在的同一文件夹中。因此，用户更容易搜索和定位资产及其转录演绎版。

转到&#x200B;**[!UICONTROL “工具”]**>**[!UICONTROL “Assets”]**>**[!UICONTROL “处理配置文件”]**，点击&#x200B;**[!UICONTROL “创建”]**&#x200B;按钮以创建基于人工智能的处理配置文件，用于生成音频和视频文件的转录。默认情况下，“处理配置文件”页面仅显示三个选项卡（图像、视频和自定义）。但是，如果您已在[!DNL Experience Manager Assets]实例中配置了[!DNL Azure Media Services]选项卡，则&#x200B;**[!UICONTROL 内容人工智能]**&#x200B;选项卡可见。如果在创建处理配置文件时，您没有看到&#x200B;**[!UICONTROL 内容人工智能]**&#x200B;选项卡，请验证您的 [!DNL Azure] 凭据。

在 **[!UICONTROL 内容人工智能]**&#x200B;选项卡中，单击&#x200B;**[!UICONTROL “新增”]**&#x200B;按钮配置转录。此处，通过从下拉列表中选择文件类型，您可以包括和排除用于生成转录的文件格式（MIME 类型）。在下列插图中，包含所有受支持音频和视频文件，排除文本文件。

启用&#x200B;**[!UICONTROL “在同一目录中创建 VTT 转录文件”]**&#x200B;切换功能，在原始资产所在的同一文件夹中创建和存储转录演绎版（.vtt 文件）。其他演绎版也由默认的 DAM 资产处理工作流生成，与此设置无关。

![configure-transcription-service](assets/configure-transcription-profile.png)

下列插图详细介绍了在 Experience Manager Assets 中创建的自定义视频配置文件。

![configure-transcription-service](assets/video-processing-profile.png)

视频配置文件还包含以下自定义配置。有关如何创建自定义处理配置文件的详细信息，请参阅[处理配置文件文档](/help/assets/asset-microservices-configure-and-use.md)。

![configure-transcription-service](assets/video-processing-profile2.png)

现在，让我们在此视频配置文件中配置转录。导航到&#x200B;**[!UICONTROL 内容人工智能]**&#x200B;选项卡，单击&#x200B;**[!UICONTROL “新增”]**&#x200B;按钮。包括所有音频和视频文件，排除图像和应用程序文件。启用&#x200B;**[!UICONTROL “在同一目录中创建 VTT 转录文件”]**&#x200B;切换功能，并保存配置。

![configure-transcription-service](assets/video-processing-profile1.png)

将处理配置文件配置为音频和视频文件的转录后，您可以使用以下方法之一将此处理配置文件应用于文件夹：

* 在&#x200B;**[!UICONTROL “工具”]**>**[!UICONTROL “Assets”]**>**[!UICONTROL “处理配置文件”]**&#x200B;中选择处理配置文件演绎版，并使用&#x200B;**[!UICONTROL “将配置文件应用到文件夹”]**&#x200B;操作。内容浏览器允许您导航到特定文件夹，选择文件夹并确认配置文件的应用。
* 在 Assets 用户界面中选择一个文件夹，然后单击打开文件夹&#x200B;**[!UICONTROL 属性]**&#x200B;的操作。单击&#x200B;**[!UICONTROL “资产处理”]**&#x200B;选项卡，并从&#x200B;**[!UICONTROL 处理配置文件]**&#x200B;列表中为文件夹选择适当的处理配置文件。要保存更改，请单击&#x200B;**[!UICONTROL “保存并关闭”]**。

   ![configure-transcription-service](assets/video-processing-profile3.png)

* 用户可以在 Assets 用户界面中选择文件夹或特定资产以应用处理配置文件，然后从顶部可用的选项中选择&#x200B;**[!UICONTROL 重新处理资产]**。

>[!TIP]
>一个文件夹只能应用一个处理配置文件。
>
>在处理配置文件应用于文件夹后，该文件夹或其任何子文件夹中上载（或更新）的所有新资产都将使用配置的其他处理配置文件进行处理。这种处理是在标准默认配置文件之外进行的。

>[!NOTE]
>
>应用于文件夹的处理配置文件适用于整个树，但是，可以被应用于子文件夹的另一个配置文件覆盖。
>
>将资产上载到文件夹时，Experience Manager 与包含文件夹的属性进行通信，以确定处理配置文件。如果未应用任何配置文件，则会检查层级中的父文件夹以确定要应用的处理配置文件。


## 生成音频或视频资产的转录 {#generate-transcription}

处理视频资源时，[基于人工智能的处理配置文件](#configure-processing-profile-for-transcription)自动生成转录文件（.vtt 文件），与同一文件夹中的原始资产共同作为演绎版。

![configure-transcription-service](assets/transcript1.png)

您还可以通过访问原始视频资产的演绎版来查看转录演绎版。要访问&#x200B;**[!UICONTROL 演绎版]**&#x200B;面板，请选择原始视频资产并打开左边栏。您可以看到转录演绎版（.vtt 文件）在&#x200B;**[!UICONTROL TRANSCRIPTVTT]**&#x200B;标题下可见。

![configure-transcription-service](assets/transcript.png)

您可以直接从文件夹中下载转录文件（.vtt 文本文件）作为单独的资产演绎版，也可以从原始资产的&#x200B;**[!UICONTROL 演绎版]**&#x200B;面板中下载资产的所有演绎版。

目前，Experience Manager 不支持对 VTT 文件进行本地全文预览或编辑。但是，您可以下载转录演绎版，并使用任何文本编辑器编辑或验证转录文件。转录文件反映了视频中给定时间戳的口语文本以及转录的置信度分数（准确性）。

![configure-transcription-service](assets/transcript-text.png)

## 在 Dynamic Media 中使用转录 {#using-transcription-in-dynamic-media}

如果您已在 Experience Manager Assets 实例中[配置了 Dynamic Media](/help/assets/dynamic-media/config-dm.md)，则可以将资产（音频或视频文件）及其转录文件（.vtt 文件）发布到 Dynamic Media。这样，原始资产（音频或视频文件）及其转录的演绎版（.vtt 文件）将发布到同一文件夹中的 Dynamic Media 中。Dynamic Media 管理员可以使用转录演绎版（.vtt 文件）为音频或视频文件[启用 CC 闭路字幕体验](/help/assets/dynamic-media/video.md#adding-captions-to-video)。

另请参阅：

* [关于如何将 CC 闭路字幕添加到 Dynamic Media 视频的视频教程](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-overview-feature-video-use.html#add-cc-closed-captioning-to-dynamic-media-video)
* [将 Dynamic Media 视频发布到 YouTube](/help/assets/dynamic-media/video.md#publishing-videos-to-youtube)

在下列插图中，URL 反映了引用转录文件（.vtt 文件）的字幕部分。视频在视频中给定的时间戳将口语（转录文本）作为&#x200B;**[!UICONTROL 闭路字幕]**&#x200B;反映出来。用户可以使用 **[!UICONTROL CC]** 按钮启用或禁用字幕。

![configure-transcription-service](assets/transcript-example.png)

## 支持的转录文件格式 {#supported-file-format}

转录支持以下音频和视频文件格式：

| 支持的音频/视频格式 | 扩展名 |
|----|----|
| FLV（含 H.264 和 AAC 编解码器） | (.flv) |
| MXF | (.mxf) |
| MPEG2-PS、MPEG2-TS、3GP | (.ts, .ps, .3gp, .3gpp, .mpg) |
| Windows Media Video (WMV)/ASF | (.wmv, .asf) |
| AVI（未压缩 8 位/10 位） | (.avi) |
| MP4 | (.mp4, .m4a, .m4v) |
| Microsoft® Digital Video Recording (DVR-MS) | (.dvr-ms) |
| Matroska/WebM | (.mkv) |
| WAVE/WAV | (.wav) |
| QuickTime | (.mov) |


>[!NOTE]
>
>应用程序类型的资产（音频或视频文件）不支持转录。

## 已知限制 {#known-limitations}

* 转录功能支持时长不超过 10 分钟的视频。
* 视频标题长度必须少于 80 个字符。
* 支持的文件大小最多为 15 GB。
* 支持的最大处理时间是 60 分钟。
* 在付费 [!DNL Azure] 帐户中，您每分钟最多可以上传 50 部电影。然而，在试用账户中，您每分钟最多可以上传 5 部电影。

## 疑难解答提示 {#troubleshooting}

使用相同的凭据（用于配置）登录 [!DNL Azure Media Services] 帐户以验证请求状态。如果您的请求未成功处理，请联系 [!DNL Azure] 支持。
