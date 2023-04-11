---
title: Dynamic Media 中的视频
description: 了解如何在Dynamic Media中处理视频。 查看有关对视频进行编码、将视频发布到YouTube、查看视频报表以及向视频添加隐藏式字幕、字幕或章节标记的最佳实践。
contentOwner: Rick Brough
feature: Video Profiles
role: User
exl-id: 0d5fbb3e-b763-415f-8c69-ea36445f882b
source-git-commit: 57666d474cd2ae41048e2d30eb27b0719a447005
workflow-type: tm+mt
source-wordcount: '5899'
ht-degree: 2%

---

# 视频 {#video}

本节介绍如何在Dynamic Media中处理视频。

## 快速入门：视频 {#quick-start-videos}

以下工作流分步描述旨在帮助您在Dynamic Media中快速设置并运行自适应视频集。 在每个步骤之后，都会对主题标题进行交叉引用，您可以在其中找到更多信息。

>[!NOTE]
>
>在Dynamic Media中处理视频之前，请确保Adobe Experience Manager管理员已启用并配置了Dynamic MediaCloud Services。
>
>* 请参阅 [配置Dynamic MediaCloud Services](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services) 配置Dynamic Media和 [Dynamic Media故障诊断](/help/assets/dynamic-media/troubleshoot-dm.md).
>


1. **上传Dynamic Media视频** 通过执行以下操作：

   * 创建您自己的视频编码配置文件。 或者，您只需使用预定义的 _自适应视频编码_ Dynamic Media的个人资料。

      * [创建视频编码配置文件](/help/assets/dynamic-media/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming).
      * 详细了解 [视频编码最佳实践](#best-practices-for-encoding-videos).
   * 将视频处理配置文件关联到一个或多个要在其中上传主要源视频的文件夹。

      * [将视频配置文件应用到文件夹](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders).
      * 详细了解 [组织数字资产](/help/assets/organize-assets.md).
   * 将主源视频上传到文件夹。 将视频添加到文件夹后，这些视频会根据您分配给文件夹的视频处理配置文件进行编码。

      * Dynamic Media主要支持长度最长为30分钟且最小分辨率大于25 x 25的短格式视频。
      * 您可以上传每个最大15 GB的视频文件。
      * [上传视频](/help/assets/manage-video-assets.md#upload-and-preview-video-assets).
      * 详细了解 [支持的输入文件格式](/help/assets/file-format-support.md).
   * 监控方式 [视频编码正在进行中](#monitoring-video-encoding-and-youtube-publishing-progress) 从资产或工作流视图。




1. **管理Dynamic Media视频** 执行以下任一操作：

   * 组织、浏览和搜索视频资产

      * [组织数字资产](/help/assets/organize-assets.md)
      * [搜索视频资产](/help/assets/search-assets.md#custompredicates) 或 [搜索资产](/help/assets/manage-digital-assets.md#search-assets)
   * 预览和发布视频资产

      * 查看源视频以及视频的编码演绎版及其关联的缩略图：
         [预览视频](/help/assets/manage-video-assets.md#upload-and-preview-video-assets) 或 [预览资产](/help/assets/dynamic-media/previewing-assets.md)
         [管理视频演绎版](/help/assets/manage-digital-assets.md#managing-renditions)

      * [管理查看器预设](/help/assets/dynamic-media/managing-viewer-presets.md)
      * [发布资产](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)
   * 使用视频元数据

      * 编辑视频的属性，如标题、描述和标记、自定义元数据字段：
         [编辑视频属性](/help/assets/manage-digital-assets.md#editing-properties)

      * [管理数字资产的元数据](/help/assets/manage-metadata.md)
      * [元数据架构](/help/assets/metadata-schemas.md)
   * 审阅、批准和批注视频，以及维护完全版本控制

      * [对视频添加注释](/help/assets/manage-video-assets.md#annotate-video-assets) 或 [对资产添加注释](/help/assets/manage-digital-assets.md#annotating)

      * [创建版本](/help/assets/manage-digital-assets.md#asset-versioning)
      * [在资产上启动工作流](/help/assets/manage-digital-assets.md#starting-a-workflow-on-an-asset)

      * [审核文件夹资产](/help/assets/bulk-approval.md)
      * [项目](/help/sites-cloud/authoring/projects/overview.md)




1. **发布Dynamic Media视频** 执行下列操作之一：

   * 如果您使用Experience Manager作为WCM（Web内容管理）系统，则可以直接将视频添加到您的网页。

      * [将视频添加到网页](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).
   * 如果您使用的是第三方Web内容管理系统，则可以将视频链接或嵌入到您的网页。

      * 使用URL集成视频：
         [将 URL 关联到您的 Web 应用程序](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md).

      * 使用网页上的嵌入代码集成视频：
         [在网页上嵌入视频查看器](/help/assets/dynamic-media/embed-code.md).
   * [将视频发布到YouTube](#publishing-videos-to-youtube).
   * [生成视频报表](#viewing-video-reports).

   * [在视频中添加字幕](#adding-captions-to-video).



## 在Dynamic Media中处理视频 {#working-with-video-in-dynamic-media}

Dynamic Media中的视频是一种端到端解决方案，可轻松发布高质量自适应视频，以便在包括台式机、平板电脑和移动设备在内的多个屏幕上进行流播放。 自适应视频集是同一视频的一组版本，这些版本以不同的比特率和格式进行编码，如400 kbps、800 kbps和1000 kbps。 台式计算机或移动设备会检测可用带宽。

例如，在iOS移动设备上，它会检测到3G、4G或Wi-Fi等带宽。 然后，它会自动从自适应视频集中的各种视频比特率中选择正确的编码视频。 视频会流式传输到台式机、移动设备或平板电脑。

此外，如果桌面或移动设备上的网络条件发生更改，则会自动动态切换视频质量。 此外，如果客户在桌面上进入全屏模式，自适应视频集将使用更好的分辨率做出响应，从而改善客户的观看体验。 对于在多个屏幕和设备上播放Dynamic Media视频的客户，使用自适应视频集可以为您提供最佳的播放方式。

视频播放器在播放期间用于确定要播放或要选择的编码视频的逻辑，基于以下算法：

1. 视频播放器根据与播放器本身中为“初始比特率”设置的值最接近的比特率来加载初始视频片段。
1. 视频播放器根据带宽速度的更改使用以下条件进行切换：

   1. 播放器会选取低于或等于估计带宽的最高带宽流。
   1. 播放器仅考虑可用带宽的80%。 但是，如果它正在切换，则更为保守，仅为70%，以避免过高估计并立即切换回来。

有关算法的详细技术信息，请参阅 [https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp](https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp)

要管理单个视频和自适应视频集，支持以下操作：

* 从多种支持的视频格式和音频格式上传视频，并将视频编码为MP4 H.264格式，以便在多个屏幕中播放。 您可以使用预定义的自适应视频预设和单个视频编码预设，或自定义您自己的编码以控制视频的质量和大小。

   * 生成自适应视频集时，它将包含MP4视频。
   * **注意**:主/源视频不会添加到自适应视频集。

* 在所有HTML5视频查看器中设置视频字幕。
* 使用完整的元数据支持组织、浏览和搜索视频，以有效管理视频资产。
* 将自适应视频集交付到Web和台式机、平板电脑和移动设备。

各种iOS平台均支持自适应视频流播放。 请参阅 [Dynamic Media查看器参考指南](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/c-html5-video-reference.html).

<!-- OUTDATED 2/28/22 BASED ON CQDOC-18692 Dynamic Media supports mobile video playback for MP4 H.264 video. You can find BlackBerry&reg; devices that support this video format at the following: [Supported video formats on BlackBerry&reg;](https://support.blackberry.com/kb/articleDetail?ArticleNumber=000005482).

OUTDATED 2/28/22 BASED ON CQDOC-18692 You can find Windows&reg; devices that support this video format at the following [Supported video formats on Windows&reg; Phone](https://docs.microsoft.com/en-us/windows/uwp/audio-video-camera/supported-codecs). -->

* 使用Dynamic Media视频查看器预设播放视频，包括以下内容：

   * 单个视频查看器。
   * 结合了视频和图像内容的混合媒体查看器。

* 配置视频播放器以满足您的品牌需求。
* 使用简单的URL或嵌入代码将视频集成到您的网站、移动设备网站或移动设备应用程序。

请参阅 [动态视频播放](https://s7d9.scene7.com/s7/uvideo.jsp?asset=GeoRetail/Mop_AVS&amp;config=GeoRetail/Universal_Video1&amp;stageSize=640,480) 示例。

另请参阅 [Experience Manager Assets和Dynamic Media Classic查看器](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/c-html5-s7-aem-asset-viewers.html#viewers-aem-assets-dmc) 和 [仅Experience Manager Assets查看器](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers.html#viewers-for-aem-assets-only) 在 [Dynamic Media查看器参考指南](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html).

## 最佳实践：使用HTML5视频查看器 {#best-practice-using-the-html-video-viewer}

Dynamic MediaHTML5视频查看器预设是强大的视频播放器。 您可以使用它们来避免许多与HTML5视频播放相关的常见问题以及与移动设备相关的问题。 例如，缺少自适应比特率流传输和桌面浏览器访问限制。

在播放器的设计方面，您可以使用标准Web开发工具来设计视频播放器的功能。 例如，您可以使用HTML5和CSS设计按钮、控件和自定义海报图像背景，以帮助您通过自定义外观联系客户。

在查看器的播放端，查看器会自动检测浏览器的视频功能。 然后，它使用HLS或DASH（也称为自适应视频流）来提供视频。 或者，如果这些投放方法不存在，则改用HTML5渐进式。

>[!NOTE]
>
>要对视频使用DASH，必须先由您帐户上的Adobe技术支持人员启用。 请参阅 [在您的帐户上启用短划线](#enable-dash).)

您可以将使用HTML5和CSS设计播放组件的功能合并到单个播放器中。 它可以具有嵌入式播放，并根据浏览器的功能使用自适应和渐进式流播放。 所有这些功能都意味着您可以将富媒体内容的访问范围扩展到桌面用户和移动设备用户，并确保简化视频体验。

另请参阅 [仅Experience Manager Assets查看器](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers.html#viewers-for-aem-assets-only) 在 [Dynamic Media查看器参考指南](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html).


### 在台式计算机和移动设备上使用HTML5视频查看器播放视频 {#playback-of-video-on-desktop-computers-and-mobile-devices-using-the-html-video-viewer}

对于桌面和移动设备自适应视频流播放，用于比特率切换的视频基于自适应视频集中的所有MP4视频。

使用HLS、DASH或渐进式视频下载进行视频播放。 在以前版本的Experience Manager（如6.0、6.1和6.2）中，视频通过HTTP进行流处理。

但是，在Experience Manager6.3及更高版本中，视频现在通过HTTPS（即HLS或DASH）进行流处理，因为DM网关服务URL也始终使用HTTPS。 此默认行为不会对客户造成任何影响。 也就是说，除非浏览器不支持，否则视频流将始终通过HTTPS进行。 （请参阅下表）。

因此，

* 如果您的HTTPS网站使用HTTPS视频流，则可以进行流播放。
* 如果您的HTTP网站使用HTTPS视频流，则流处理可以正常进行，并且Web浏览器中不会出现混合内容问题。

DASH是国际标准，HLS是Apple标准。 这两种方法都用于自适应视频流播放。 而且，这两种技术都可根据网络带宽容量自动调整播放。 它还允许客户“搜寻”视频中的任意点，而无需等待视频的其余部分下载。

通过在用户的桌面系统或移动设备上本地下载和存储视频来传送渐进式视频。

下表介绍了在台式计算机和移动设备上使用 [Dynamic MediaHTML5视频查看器](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video.html#interactive-video).

<table>
 <tbody>
  <tr>
   <td><strong>设备</strong></td>
   <td><strong>浏览器</strong></td>
   <td><strong>视频播放模式</strong></td>
  </tr>
  <tr>
   <td>桌面</td>
   <td>Internet Explorer 9和10</td>
   <td>渐进式下载。</td>
  </tr>
  <tr>
   <td>桌面</td>
   <td>Internet Explorer 11+</td>
   <td>在Windows® 8和Windows® 10上 — 请求DASH或HLS时，强制使用HTTPS。 已知限制：HTTP on DASH或HLS在此浏览器/操作系统组合中不起作用<br /> <br /> 在Windows® 7上 — 渐进式下载。 使用标准逻辑选择HTTP与HTTPS协议。</td>
  </tr>
  <tr>
   <td>桌面</td>
   <td>Firefox 23-44</td>
   <td>渐进式下载。</td>
  </tr>
  <tr>
   <td>桌面</td>
   <td>Firefox 45或更高版本</td>
   <td>HLS或DASH*自适应比特率流</td>
  </tr>
  <tr>
   <td>桌面</td>
   <td>铬黄</td>
   <td>HLS或DASH*自适应比特率流</td>
  </tr>
  <tr>
   <td>桌面</td>
   <td>Safari(Mac)</td>
   <td>HLS自适应比特率流</td>
  </tr>
  <tr>
   <td>移动设备</td>
   <td>Chrome(Android™ 6或更早版本)</td>
   <td>渐进式下载。</td>
  </tr>
  <tr>
   <td>移动设备</td>
   <td>Chrome(Android™ 7或更高版本)</td>
   <td>HLS或DASH*自适应比特率流/td&gt;
  </tr>
  <tr>
   <td>移动设备</td>
   <td>Android™（默认浏览器）</td>
   <td>渐进式下载。</td>
  </tr>
  <tr>
   <td>移动设备</td>
   <td>Safari(iOS)</td>
   <td>HLS自适应比特率流</td>
  </tr>
  <tr>
   <td>移动设备</td>
   <td>Chrome(iOS)</td>
   <td>HLS自适应比特率流</td>
  </tr>
 </tbody>
</table>

>[!IMPORTANT]
>
>*要对视频使用DASH，必须先由您帐户上的Adobe技术支持人员启用。 请参阅 [在您的帐户上启用短划线](#enable-dash).)

<!--  THIS LINE WAS REMOVED FROM THE TABLE ABOVE ON FEB 28, 2022 BASED ON CQDOC 18692 -RSB <tr>
   <td>Mobile</td>
   <td>BlackBerry&reg;</td>
   <td>HLS or DASH</td>
  </tr>
 -->

## Dynamic Media视频解决方案的架构 {#architecture-of-dynamic-media-video-solution}

下图显示了视频的整体创作工作流程，这些视频通过DMGateway(在Dynamic Media混合模式下)上传和编码，并可供公众使用。

![chlimage_1-427](assets/chlimage_1-427.png)

## 视频的混合发布架构 {#hybrid-publishing-architecture-for-videos}

![chlimage_1-428](assets/chlimage_1-428.png)

## 视频编码最佳实践 {#best-practices-for-encoding-videos}

的 **Dynamic Media编码视频** 如果您已启用Dynamic Media并设置了视频Cloud Services，则工作流会对视频进行编码。 此工作流会捕获工作流进程历史记录和失败信息。请参阅 [监控视频编码和YouTube发布进度](#monitoring-video-encoding-and-youtube-publishing-progress). 如果您已启用Dynamic Media并设置视频Cloud Services，则 **[!UICONTROL Dynamic Media编码视频]** 在您上传视频时，工作流会自动生效。 (如果您没有使用Dynamic Media，则 **[!UICONTROL DAM更新资产]** 工作流生效。)

以下是源视频文件编码的最佳实践提示。

<!-- For advice about video encoding, see the following:

* [Streaming 101: The Basics — Codecs, Bandwidth, Data Rate, and Resolution](https://www.adobe.com/go/learn_s7_streaming101_en).
* [Video Encoding Basics](https://www.adobe.com/go/learn_s7_encoding_en). -->

### 源视频文件 {#source-video-files}

在对视频文件进行编码时，请使用尽可能高质量的源视频文件。 避免使用之前编码的视频文件，因为这些文件已经压缩，而进一步编码会创建质量欠佳的视频。

* Dynamic Media主要支持长度最长为30分钟且最小分辨率大于25 x 25的短格式视频。
* 您可以上载每个最大15 GB的主源视频文件。

下表描述了源视频文件在编码之前必须具有的推荐大小、宽高比和最小比特率：

| 大小 | 宽高比 | 最小比特率 |
|--- |--- |--- |
| 1024 X 768 | 4:3 | 4500 kbps，适用于大多数视频。 |
| 1280 X 720 | 16:9 | 3000 - 6000 kbps，具体取决于视频中的运动量。 |
| 1920 X 1080 | 16:9 | 6000 - 8000 kbps，具体取决于视频中的运动量。 |

### 获取文件的元数据 {#obtaining-a-file-s-metadata}

您可以通过以下方式获取文件的元数据：使用视频编辑工具查看文件的元数据，或使用为获取元数据而设计的应用程序。 以下是有关使用第三方应用程序MediaInfo获取视频文件元数据的说明：

1. 转到 [MediaInfo下载](https://mediaarea.net/en/MediaInfo/Download).
1. 选择并下载GUI版本的安装程序，然后按照安装说明操作。
1. 安装后，右键单击视频文件(仅限Windows®)并选择“MediaInfo”，或打开“MediaInfo”并将视频文件拖到应用程序中。 您会看到与视频文件关联的所有元数据，包括其宽度、高度和fps。

### 宽高比 {#aspect-ratio}

在为主源视频文件选择或创建视频编码预设时，请确保预设的宽高比与主源视频文件的宽高比相同。 宽高比是视频宽度与高度的比率。

要确定视频文件的宽高比，请获取文件的元数据并记下文件的宽度和高度（请参阅上面的获取文件的元数据）。 然后，使用下式确定宽高比：

宽高=宽高比

下表描述了公式结果如何转换为常见的宽高比选项：

| 公式结果 | 宽高比 |
|--- |--- |
| 1.33 | 4:3 |
| 0.75 | 3:4 |
| 1.78 | 16:9 |
| 0.56 | 9:16 |

例如，宽度为1440 x 1080的视频的宽高比为1440/1080或1.33。在这种情况下，请选择宽高比为4:3的视频编码预设，以对视频文件进行编码。

### 比特率 {#bitrate}

比特率是经过编码，构成视频播放一秒的数据量。 比特率以千比特每秒(Kbps)为单位进行测量。

>[!NOTE]
>
>由于所有编解码器都使用有损压缩，因此比特率是视频质量中最重要的因素。 使用有损压缩时，对视频文件的压缩越多，质量就降低得越多。 因此，所有其他特性（分辨率、帧速率和编解码器）均相等，比特率越低，压缩文件的质量就越低。

选择比特率编码时，可以选择以下两种类型：

* **[!UICONTROL 恒定比特率编码]** (CBR) — 在CBR编码期间，比特率或每秒比特数在整个编码过程中保持不变。 CBR编码会在整个视频中将设置的数据速率保留为您的设置。 此外，CBR编码不会为质量优化媒体文件，但会节省存储空间。
如果您的视频在整个视频中包含相似的运动级别，则使用CBR。 CBR最常用于流式传输视频内容。 另请参阅 [使用自定义添加的视频编码参数](/help/assets/dynamic-media/video-profiles.md#using-custom-added-video-encoding-parameters).

* **[!UICONTROL 可变比特率编码]** (VBR)- VBR编码根据压缩程序所需的数据，将数据速率调低并调整到您设置的上限。 此功能意味着在VBR编码过程中，媒体文件的比特率会根据媒体文件的比特率需求动态增加或减少。
VBR需要较长的编码时间，但会产生最有利的结果；媒体文件的质量优于其他文件。 VBR最常用于视频内容的http渐进式交付。

何时使用VBR与CRB?
选择VBR与CBR时，几乎总是建议将VBR用于媒体文件。 VBR以具有竞争力的比特率提供高质量文件。 使用VBR时，请务必对两遍编码进行使用，并将最大比特率设置为目标视频比特率的1.5倍。

选择视频编码预设时，请确保考虑目标最终用户的连接速度。 选择数据率为该速度80%的预设。 例如，如果目标最终用户的连接速度为1000 Kbps，则最佳预设是视频数据率为800 Kbps的预设。

此表描述了典型连接速度的数据率。

| 速度(Kbps) | 连接类型 |
|--- |--- |
| 256 | 拨号连接。 |
| 800 | 典型的移动连接。 对于此连接，为3G体验定位数据率（范围为400到最大800）。 |
| 2000 | 典型的宽带桌面连接。 对于此连接，目标数据率范围为800-2000 Kbps，大多数目标数据率平均为1200-1500 Kbps。 |
| 5000 | 典型的高宽带连接。 不建议在此上限范围内进行编码，因为大多数用户无法以此速度进行视频交付。 |

### 解决方法 {#resolution}

**分辨率** 以像素为单位描述视频文件的高度和宽度。 大多数源视频以高分辨率存储（例如，1920 x 1080）。 出于流播放目的，源视频会压缩为较小的分辨率（640 x 480或更低）。

分辨率和数据率是决定视频质量的两个相互关联的因素。 要保持相同的视频质量，视频文件中的像素数越高（分辨率越高），数据率就必须越高。 例如，请考虑分辨率为320 x 240和分辨率为640 x 480的视频文件中每帧的像素数：

| 解决方法 | 每帧像素数 |
|--- |--- |
| 320 x 240 | 76,800 |
| 640 x 480 | 307,200 |

640 x 480文件的每帧像素数是原来的四倍。 为了使这两个示例分辨率的数据率保持相同，您需要对640 x 480文件应用四倍的压缩，这会降低视频质量。 因此，250 Kbps的视频数据率在320 x 240分辨率下，而在640 x 480分辨率下，会产生高质量的观看效果。

通常，您使用的数据率越高，视频的显示效果越好，您使用的分辨率越高，您必须保持查看质量的数据率就越高（与分辨率较低的数据相比）。

由于分辨率和数据率是相关的，因此在对视频进行编码时有两个选项可供选择：

* 选择一个数据率，然后以在所选数据率中显示良好的最高分辨率进行编码。
* 选择一个分辨率，然后按所需的数据速率进行编码，以便以您选择的分辨率获得高质量视频。

当您为主源视频文件选择（或创建）视频编码预设时，请使用此表来确定正确的分辨率：

| 解决方法 | 高度(像素) | 屏幕大小 |
|--- |--- |--- |
| 240p | 240 | 小屏幕 |
| 300p | 300 | 通常用于移动设备的小屏幕 |
| 360p | 360 | 小屏幕 |
| 480p | 480 | 中型屏幕 |
| 720p | 720 | 大屏幕 |
| 1080p | 1080 | 高清大屏幕 |

### Fps（每秒帧数） {#fps-frames-per-second}

在美国和日本，大多数视频以29.97帧/秒(fps)的速度拍摄；在欧洲，大多数视频以25 fps的速率拍摄。 电影以24 fps的速率拍摄。

选择与主源视频文件的fps速率匹配的视频编码预设。 例如，如果主源视频的帧数为25 fps，请选择25 fps的编码预设。 默认情况下，所有自定义编码都使用主源视频文件的fps。 因此，在创建视频编码预设时，您无需明确指定fps设置。

### 视频编码维度 {#video-encoding-dimensions}

为获得最佳结果，请选择编码维度，以便源视频是所有编码视频的整数倍。

要计算此比率，请将源宽度除以编码宽度，得到宽度比。 然后，将源高度除以编码高度，得到高度比。

如果生成的比率是整数，则表示视频已得到最佳缩放。 如果生成的比率不是整数，则会通过在显示器上留下残留像素伪影来影响视频质量。 当视频包含文本时，此效果最为明显。

例如，假定源视频为1920 x 1080。 在下表中，三个编码视频提供了要使用的最佳编码设置。

| 视频类型 | 宽x高 | 宽度比例 | 高度比 |
|--- |--- |--- |--- |
| 源 | 1920x1080 | 1 | 1 |
| 已编码 | 960 x 540 | 2 | 2 |
| 已编码 | 640 x 360 | 3 | 3 |
| 已编码 | 480 x 270 | 4 | 4 |

### 编码视频文件格式 {#encoded-video-file-format}

Dynamic Media建议使用MP4 H.264视频编码预设。 由于MP4文件使用H.264视频编解码器，因此它提供高质量视频，但文件大小已压缩。

### 在您的帐户上启用短划线 {#enable-dash}

DASH（HTTP上的数字自适应流播放）是视频流播放的国际标准，在不同的视频查看器中得到广泛采用。 在您的帐户上启用短划线后，您可以选择从短划线或HLS中选择自适应视频流播放。 或者，您可以在 **[!UICONTROL 自动]** 在“查看器预设”中选择作为播放类型。

在您的帐户中启用DASH的一些主要优势包括：

* 包含用于自适应比特率流播放的短划线流视频。 这种方法可提高投放效率。 自适应流播放可确保为客户提供最佳的观看体验。
* 使用Dynamic Media播放器优化的流播放在HLS和DASH流之间切换，以确保最佳服务质量。 当使用Safari浏览器时，视频播放器会自动切换到HLS。
* 您可以通过编辑视频查看器预设来配置首选的流播放方法（HLS或DASH）。
* 优化的视频编码可确保在启用短划线功能时不使用额外存储。 为HLS和DASH创建一组视频编码，以优化视频存储成本。
* 帮助让客户更易于访问视频交付。
* 也可以通过API获取流URL。

   >[!IMPORTANT]
   >
   >目前，在您的帐户上启用DASH仅在亚太地区和北美地区提供；即将在欧洲 — 中东 — 非洲推出。

发起使用DASH的请求；它不会在您的帐户上自动启用。

要在您的帐户上启用DASH，请创建客户支持案例，如下所述。 在支持案例中，指定要在Dynamic Media帐户和Experience Manager上启用DASH。

**要在您的帐户上启用DASH，请执行以下操作：**

1. [使用Admin Console开始创建新的支持案例](https://helpx.adobe.com/cn/enterprise/using/support-for-experience-cloud.html).
1. 按照相关说明创建支持案例，同时确保提供以下信息：

   * 主要联系人姓名、电子邮件、电话。
   * 您的Dynamic Media帐户的名称。
   * 指定希望在Dynamic Media帐户和Experience Manager上启用短划线。

1. Adobe客户支持根据请求提交顺序将您添加到DASH客户等待列表。
1. 当Adobe准备好处理您的请求时，客户支持团队会联系您，以协调并设置启用短划线的目标日期。
1. 客户支持部门在完成后会通知您。
1. 创建 [视频查看器预设](/help/assets/dynamic-media/managing-viewer-presets.md#creating-a-new-viewer-preset) 和往常一样。

## 查看视频报表 {#viewing-video-reports}

>[!NOTE]
>
>视频报表仅在运行Dynamic Media — 混合模式时可用。

视频报表显示指定时间段内的多个汇总量度，以帮助您监控 *发布* 单个视频和聚合视频将按预期执行。 以下热门量度数据是针对整个网站中所有已发布视频的汇总数据：

* 视频开始
* 完成率
* 视频平均逗留时间
* 视频播放总时间
* 每次访问视频数

全部表格 *发布* 视频也会列出，以便您可以根据视频开始总数跟踪网站上查看次数最多的视频。

当您在列表中选择视频名称时，它将以折线图形式显示视频的受众保留（下拉）报表。 该图表显示视频播放期间任何给定时刻的查看次数。 播放视频时，垂直条会与播放器中的时间指示器同步跟踪。 折线图数据中的数据显示受众因不感兴趣而停止观看的位置。

如果视频是在Adobe Experience Manager Dynamic Media之外进行编码，则将不提供受众保留（流失）图表和表中的播放百分比数据。

>[!NOTE]
>
>跟踪和报告数据完全基于使用Dynamic Media自己的视频播放器和关联的视频播放器预设。 因此，您无法跟踪和报告通过其他视频播放器播放的视频。

默认情况下，在您首次进入视频报表时，报表会显示从当月的第一个开始到当月日期结束的视频数据。 但是，您可以通过指定您自己的日期范围来覆盖默认日期范围。 下次输入视频报表时，将使用您指定的日期范围。

为了使视频报表正常工作，在配置Dynamic MediaCloud Services时会自动创建报表包ID。 同时，报表包ID会被推送到发布服务器，以便在预览资产时，该ID可用于复制URL功能。 但是，此功能要求发布服务器已经设置。 如果未设置发布服务器，您仍可以通过发布查看视频报表。 但是，您必须返回到Dynamic Media云配置，然后选择 **[!UICONTROL 确定]**.

**要查看视频报表，请执行以下操作：**

1. 在Experience Manager的左上角，选择Experience Manager徽标，然后在左边栏中，导航到 **[!UICONTROL 工具]** （锤子图标）> **[!UICONTROL 资产]** > **[!UICONTROL 视频报表]**.
1. 在“视频报表”页面上，执行以下操作之一：

   * 在右上角附近，选择 **[!UICONTROL 刷新视频报表]** 图标。
仅当报表的结束日期是当天时，才使用“刷新”。 此功能可确保您查看自上次运行报表以来发生的视频跟踪。

   * 在右上角附近，选择 **[!UICONTROL 日期选取器]** 图标。
指定您希望视频数据的开始和结束日期范围，然后选择 **[!UICONTROL 运行报表]**.

   “热门量度”组框标识所有 *发布* 视频。

1. 在列出排名最前的已发布视频的表中，选择要播放视频的视频名称，并查看视频的受众保留（流失）报表。

<!-- OBSOLETE CONTENT OBSOLETE CONTENT - SDK ONLY AVAILABLE INTERNALLY NOW 
### Viewing video reports based on a video viewer that you created using the Dynamic Media HTML5 Viewer SDK {#viewing-video-reports-based-on-a-video-viewer-that-you-created-using-the-scene-hmtl-viewer-sdk}

If you are using an out-of-box video viewer provided by Dynamic Media, or if you created a custom viewer preset based off of an out-of-box video viewer, then no additional steps are required to view video reports. However, if you have created your own video viewer based off the Dynamic Media HTML5 Viewer SDK, then use the following steps to ensure the your video viewer is sending tracking events to Dynamic Media Video Reports.

Use the Dynamic Media Viewers Reference and the Dynamic Media HTML5 Viewers SDK to create your own video viewers.

See [Dynamic Media Viewers Reference Guide](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/home.html).

Download the Scene7 HTML Viewer SDK from Adobe Developer Connection.

See [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html).

**To view Video Reports based on a video viewer that you created using the Dynamic Media HTML5 Viewer SDK:**

1. Navigate to any published video asset.
1. Near the upper-left corner of the asset's page, from the drop-down list, select **[!UICONTROL Viewers]**.
1. Select any video viewer preset and copy the embed code.
1. In the embed code, find the line with the following:

   `videoViewer.setParam("config2", "<value>");`

   The `config2` parameter enables tracking in HTML5 Viewers. It is also a company-specific preset that contains the configuration information for Video Reporting, and for customer-specific Adobe Analytics configurations.

   The correct value for the config2 parameter is found in both the **[!UICONTROL Embed Code]** and in the copy **[!UICONTROL URL]** function. In the URL from the copy **[!UICONTROL URL]** command, the parameter to look for is `&config2=<value>` . The value is almost always `companypreset`, but in some instances it can also be `companypreset-1`, `companypreset-2`, and so forth.

1. In your custom video viewer code, add AppMeasurementBridge .jsp to the viewer page by doing the following:

    * First, determine if you need the `&preset` parameter.
      If the `config2` parameter is `companypreset`, you do *not *need `&preset=parameter`.
      If `config2` is anything else, set the preset parameter the same as the `config2` parameter. For example, if `config2=companypreset-2`, add `&param2=companypreset-2` to the AppMeasurmentBridge.jsp URL.

    * Then, add the AppMeasurementBridge.jsp script:
      `<script language="javascript" type="text/javascript" src="https://s7d1.scene7.com/s7viewers/AppMeasurementBridge.jsp?company=robindallas&preset=companypreset-2"></script>`

1. Create the TrackingManager component by doing the following:

    * After calling `s7sdk.Utils.init();` create a TrackingManager instance to track events by adding the following:
      `var trackingManager = new s7sdk.TrackingManager();`

    * Connect components to TrackingManager by doing the following:
      In the `s7sdk.Event.SDK_READY` event handler, attach the component you want to track to the TrackingManager.
      For example, if the component is `videoPlayer`, add
      `trackingManager.attach(videoPlayer);`
      to attach the component to the trackingManager. To track multiple viewers on a page, use multiple tracking mangaer components.

    * Create the AppMeasurementBridge object by adding the following:

      ```
      var appMeasurementBridge = new AppMeasurementBridge(); appMeasurementBridge.setVideoPlayer(videoPlayer);
      ```

    * Add the tracking function by adding the following:

      ```
      trackingManager.setCallback(appMeasurementBridge.track,
       appMeasurementBridge);
      ```

   The appMeasurementBridge object has a built-in track function. OBSOLETE However, you can provide your own to support multiple tracking systems or other functionality.

   For more information, see *Using the TrackingManager Component* in the *Scene7 HTML5 Viewer SDK User Guide* available for download from [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html).
 -->

## 在视频中添加隐藏式字幕或字幕 {#adding-captions-to-video}

您可以通过向单个视频或自适应视频集添加隐藏式字幕，将视频的覆盖范围扩展到全球市场。 通过添加隐藏式字幕，您无需对音频进行调音，也无需使用母语人士为每个不同语言重新录制音频。 视频以录制的语言播放。 出现外语字幕，使不同语言的人仍然能够理解音频部分。

隐藏式字幕还允许耳聋或听力欠佳的用户更方便地访问。

>[!NOTE]
>
>您使用的视频播放器必须支持隐藏式字幕的显示。

另请参阅 [Dynamic Media中的辅助功能](/help/assets/dynamic-media/accessibility-dm.md).

Dynamic Media可以将题注文件转换为JSON（JavaScript对象表示法）格式。 这种转换意味着您可以将JSON文本作为视频的隐藏但完整的记录嵌入到网页中。 然后，搜索引擎可以爬网/索引内容，以使视频更容易被发现，并为客户提供有关视频内容的更多详细信息。

请参阅 [提供静态（非图像）内容](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/c-serving-static-nonimage-contents.html#image-serving-api) 有关在URL中使用JSON函数的更多信息。

**要在视频中添加字幕或字幕，请执行以下操作：**

1. 使用第三方应用程序或服务创建视频字幕/子标题文件。

   确保您创建的文件遵循WebVTT（Web视频文本跟踪）标准。 字幕文件扩展名为.VTT。 您可以了解有关WebVTT字幕标准的更多信息。

   请参阅 [WebVTT:Web视频文本跟踪格式](https://w3c.github.io/webvtt/).

   在Dynamic Media之外，您可以使用免费和优质的工具和服务来创作字幕/子标题文件。 例如，要创建不带样式的简单视频字幕文件，您可以使用以下免费的在线字幕创作和编辑工具：

   [WebVTT字幕制作器](https://testdrive-archive.azurewebsites.net/Graphics/CaptionMaker/Default.html)

   为获得最佳结果，请使用Internet Explorer 9或更高版本、Google Chrome或Safari中的工具。

   在工具中，在 **[!UICONTROL 输入视频文件的URL]** 字段中，粘贴复制的视频文件的URL，然后选择 **[!UICONTROL 加载]**. 请参阅 [获取资产的URL](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset) 以获取视频文件的URL，然后您可以将其粘贴到 **[!UICONTROL 输入视频文件字段的URL]**. 随后，Internet Explorer、Chrome 或 Safari 可以本机播放视频。

   现在，按照网站上的屏幕说明来创作和保存您的WebVTT文件。 完成后，复制题注文件内容并将其粘贴到纯文本编辑器中，并以VTT文件扩展名进行保存。

   >[!NOTE]
   >
   >为全球支持多种语言的视频字幕，WebVTT标准要求您为要支持的每种语言分别创建单独的.vtt文件和调用。

   通常，您要将字幕VTT文件命名为与视频文件同名，并附加语言区域设置，如 — EN、-FR或 — DE。 这样，您就可以使用现有的Web内容管理系统自动生成视频URL。

1. 在Experience Manager中，将WebVTT字幕文件上传到DAM。
1. 导航到 *发布* 要与您上传的题注文件关联的视频资产。

   请注意，只有在首次&#x200B;*发布*&#x200B;资产&#x200B;*后*，才可复制 URL。

   请参阅 [发布资产](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

1. 执行下列操作之一：

   * 要获得弹出式视频查看器体验，请选择 **[!UICONTROL URL]**. 在“URL”对话框中，选择URL并将其复制到剪贴板，然后将该URL传递到简单的文本编辑器中。 使用以下语法附加复制的视频URL:

      `&caption=<server_path>/is/content/<path_to_caption.vtt_file,1>`

      请注意 `,1` 标题路径的末尾。 在路径中的VTT文件扩展名后，您可以选择启用（打开）或禁用（关闭）视频播放器栏上的隐藏式字幕按钮，方法是将设置为 `,1` 或 `,0`，分别为。

   * 对于嵌入式视频查看器体验，请选择 **[!UICONTROL 嵌入代码]**. 在“嵌入代码”对话框中，选择嵌入代码，并将其复制到剪贴板，然后将该代码粘贴到简单的文本编辑器中。 将复制的嵌入代码附加以下语法：

      `videoViewer.setParam("caption","<path_to_caption.vtt_file,1>");`

      请注意 `,1` 标题路径的末尾。 在路径中的VTT文件扩展名后，您可以选择启用（打开）或禁用（关闭）视频播放器栏上的隐藏式字幕按钮，方法是将设置为 `,1` 或 `,0`，分别为。

## 向视频添加章节标记 {#adding-chapter-markers-to-video}

您可以通过向单个视频或自适应视频集添加章节标记，来更轻松地观看和导航长形视频。 当用户播放视频时，他们可以选择视频时间轴上的章节标记（也称为视频清理器）。 他们可以轻松导航到自己的目标点，或立即跳转到新内容、培训和演示。

>[!NOTE]
>
>使用的视频播放器必须支持使用章节标记。 Dynamic Media视频播放器确实支持章节标记，但使用第三方视频播放器可能不支持。

<!-- OBSOLETE CONTENT OBSOLETE CONTENT If desired, you can create and brand your own custom video viewer with chapters instead of using a video viewer preset. For instructions on creating your own HTML5 viewer with chapter navigation, in the Adobe Scene7 Viewer SDK for HTML5 guide, reference the heading "Customizing Behavior Using Modifiers" under the classes `s7sdk.video.VideoPlayer` and `s7sdk.video.VideoScrubber`. The Adobe Scene7 Viewer SDK is available as a download from [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html). -->

为视频创建章节列表的方式与创建字幕的方式大致相同。 即，创建一个WebVTT文件。 但是，请注意，此文件必须与任何WebVTT标题文件分开。 不能将字幕和章节合并到一个WebVTT文件中。

您可以使用以下示例作为创建包含章节导航的WebVTT文件所使用的格式示例：

### 带有视频章节导航的WebVTT文件 {#webvtt-file-with-video-chapter-navigation}

```xml {.line-numbers}
WEBVTT
Chapter 1
00:00.000 --> 01:04.364
The bicycle store behind it all.
Chapter 2
01:04.364 --> 02:00.944
Creative Cloud.
Chapter 3
02:00.944 --> 03:02.937
Ease of management for a working solution.
Chapter 4
03:02.937 --> 03:35.000
Cost-efficient access to rapidly evolving technology.
```

在上例中， `Chapter 1` 是提示标识符，是可选的。 的提示时间 `00:00:000 --> 01:04:364` 指定章节的开始时间和结束时间(在 `00:00:000` 格式。 最后三位是毫秒，可保留为 `000`，如果首选。 的章节标题 `The bicycle store behind it all` 是章节内容的实际描述。 当用户将鼠标指针悬停在时间轴中的可视提示点上时，提示标识符、开始提示时间和章节标题都会显示在视频播放器的弹出窗口中。

由于您使用的是HTML5视频查看器，因此请确保您创建的章节文件遵循WebVTT（Web视频文本跟踪）标准。 章节文件扩展名为.VTT。 您可以了解有关WebVTT字幕标准的更多信息。

请参阅 [WebVTT:Web视频文本跟踪格式](https://w3c.github.io/webvtt/).

**要向视频添加章节标记，请执行以下操作：**

1. 以UTF8编码格式保存VTT文件，以避免章节标题文本中的字符呈现出现问题。

   通常，您需要使用与视频文件相同的名称命名章节VTT文件，并在其后附加章节。 这样，您就可以使用现有的Web内容管理系统自动生成视频URL。
1. 在Experience Manager中，上传您的WebVTT章节文件。

   请参阅 [上传资产](/help/assets/manage-digital-assets.md#uploading-assets).

1. 执行下列操作之一：

   <table>
     <tbody>
      <tr>
       <td>用于弹出式视频查看器体验</td>
       <td>
       <ol>
       <li>导航到 <i>发布 </i>要与您上传的章节文件关联的视频资产。 请注意，只有在首次<i>发布</i>资产<i>后</i>，才可复制 URL。请参阅 <a href="/help/assets/dynamic-media/publishing-dynamicmedia-assets.md">发布资产。</a></li>
       <li>从下拉菜单中，选择 <strong>查看器</strong>.</li>
       <li>在左边栏中，选择视频查看器预设名称。 视频的预览将在单独的页面中打开。</li>
       <li>在左边栏的底部，选择 <strong>URL</strong>.</li>
       <li>在“URL”对话框中，选择URL并将其复制到剪贴板，然后将该URL传递到简单的文本编辑器中。</li>
       <li>将复制的视频URL附加以下语法，以便将其与复制的URL关联到您的章节文件：<br /> <br /> <code>&navigation=<<i>full_copied_URL_path_to_chapter_file</i>.vtt></code><br /> </li>
       </ol> </td>
      </tr>
      <tr>
       <td>对于嵌入式视频查看器体验<br /> </td>
       <td>
       <ol>
       <li>导航到 <i>发布 </i>要与您上传的章节文件关联的视频资产。 请注意，只有在首次<i>发布</i>资产<i>后</i>，才可复制 URL。请参阅 <a href="/help/assets/dynamic-media/publishing-dynamicmedia-assets.md">发布资产。</a></li>
       <li>从下拉菜单中，选择 <strong>查看器</strong>.</li>
       <li>在左边栏中，选择视频查看器预设名称。 视频的预览将在单独的页面中打开。</li>
       <li>在左边栏的底部，选择 <strong>嵌入</strong>.</li>
       <li>在“嵌入代码”对话框中，选择整个代码，并将其复制到剪贴板，然后将其粘贴到简单的文本编辑器中。</li>
       <li>将视频的嵌入代码附加以下语法，以便将其与复制的URL关联到您的章节文件：<br /> <br /> <code>videoViewer.setParam("navigation","&lt;<i>full_copied_URL_path_to_chapter_file</i>.vtt>"</code></li>
       </ol> </td>
      </tr>
     </tbody>
   </table>

<!--

## About video thumbnails {#about-video-thumbnails}

A video thumbnail is a reduced-size version of a video frame or an image asset representing the video to the customer. The thumbnail should serve to encourage a customer to select the video.

All videos in Experience Manager must have an associated thumbnail; you cannot delete a thumbnail without replacing it. By default, when you upload a video to Experience Manager, the first frame is used as the thumbnail. However, you can customize the thumbnail for branding purposes or visual search, for example. When you customize a video thumbnail, you can either play the video and pause on the frame you want to use, or you can select an image asset that you have already uploaded and *published* in your digital asset manager.

Note that a custom video thumbnail image that you select from a video is not extracted and saved in the DAM as a separate and distinct asset. However, a custom video thumbnail that you select from an existing image asset is saved to the JCR. The path of the selected asset gets stored under the video asset's node as in the following example path:

`/content/dam/*<folder_name*>/<*video_name*>/jcr:content/manualThumbnail`

The ability to customize a video thumbnail is only available after you have applied a video profile to the folder where the video is located.

### Adding a custom video thumbnail {#adding-a-custom-video-thumbnail}

1. Be sure you have already done the following:

    * Created a folder for your video assets.
    * [Applied a video profile to the folder](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders).

    * [Uploaded your videos to the folder](/help/assets/manage-video-assets.md#upload-and-preview-video-assets).

1. Navigate to an uploaded video asset whose thumbnail image you want to change.
1. In asset selection mode either from **[!UICONTROL List View]** or **[!UICONTROL Card View]**, select the video asset.
1. On the toolbar, select the **[!UICONTROL Properties** icon (a circle with an "i" in it).
1. On the video's Properties page, select **[!UICONTROL Change Thumbnail]**.
1. On the Change Thumbnail page, do one of the following:

    * To use a frame from the video as the new thumbnail:

        * On the toolbar, select **[!UICONTROL Select Frame from video]**.
        * Select the Play button, then select the Pause button on the frame you want to capture as the video's new thumbnail.

    * To use an image asset as the new thumbnail:

        * On the toolbar, select **[!UICONTROL Select Thumbnail from Assets]**.
        * Select **[!UICONTROL Select Thumbnail]**.
        * Navigate to a previously uploaded and published image asset you want to use. Note that the asset will automatically be resized to serve as a thumbnail image for the video.
        * Select the image asset, then select **[!UICONTROL Select]**.

1. On the Change Thumbnail page, select **[!UICONTROL Save Change]**.
1. On the video's Properties page, in the upper-right corner, select **[!UICONTROL Save & Close]**.

-->

<!--

## About video thumbnails in Dynamic Media Hybrid mode{#about-video-thumbnails-in-dynamic-media-hybrid-mode}

You can choose from one of ten thumbnail images automatically generated by Dynamic Media to add to your video. The video player displays your selected thumbnail when a video asset is used with the Dynamic Media component in the authoring environment of Experience Manager Sites, Experience Manager Mobile, or Experience Manager Screens. The thumbnail serves as a static picture that best represents the contents of your entire video and further encourages users to select the Play button.

Based on the total time of the video, Dynamic Media captures ten (default) thumbnail images at 1%, 11%, 21%, 31%, 41%, 51%, 61%, 71%, 81%, and 91% into the video. The ten thumbnails persist meaning that if you decide to choose a different thumbnail later on, you do not need to regenerate the series. You preview the ten thumbnail images and then select the one you want to use with your video. If you want to change to default you can use CRXDE Lite to configure the time interval that thumbnail images are generated. For example, if you only wanted to generate a series of four evenly spaced thumbnail images from your video, you can configure the interval time at 24%, 49%, 74%, and 99%.

Ideally, you can add a video thumbnail anytime after you upload your video but before you publish the video on your website.

If you prefer, you can choose to upload a custom thumbnail to represent your video instead of using a thumbnail generated by Dynamic Media. For example, you could create a custom thumbnail image that has the title of your video, an eye-catching opening image, or a very specific image captured from your video. The custom video thumbnail image that you upload should have a maximum resolution of 1280 x 720 pixels (minimum width of 640 pixels) and be no larger than 2MB.

See also [About video thumbnails](/help/assets/dynamic-media/video.md#about-video-thumbnails-in-dynamic-media-scene-mode).

-->

<!--

### Adding a video thumbnail {#adding-a-video-thumbnail}

1. Navigate to an uploaded video asset that you want to add a video thumbnail.
1. In asset selection mode either from the List View or the Card View, select the video asset.
1. On the toolbar, select the **[!UICONTROL View Properties]** icon (a circle with an "i" in it).
1. On the video's Properties page, select **[!UICONTROL Change Thumbnail]**.
1. On the Change Thumbnail page, on the toolbar, select **[!UICONTROL Select Frame]**.

   Dynamic Media generates a series thumbnail images from your video, based on the default time interval or time interval you customized.

1. Preview the generated thumbnail images, then select the one you want to add to your video.
1. Select **[!UICONTROL Save Change]**.

   The video's thumbnail image is updated to use the thumbnail you selected. If you later decide to change the thumbnail image, you can return to the **[!UICONTROL Change Thumbnail]** page and select a new one.

   If you configured new default time intervals, or you uploaded a new video to replace the existing video, you will need to have Dynamic Media regenerate the thumbnails.

   See [Configuring the default time interval that video thumbnails are generated](#configuring-the-default-time-interval-that-video-thumbnails-are-generated).

-->

<!--

#### Configuring the default time interval that video thumbnails are generated {#configuring-the-default-time-interval-that-video-thumbnails-are-generated}

When you configure and save the new default time interval, your change automatically applies only to videos that you upload in the future. It does not automatically apply the new default to videos that you previously uploaded. For existing videos, you must regenerate the thumbnails.

See [Adding a video thumbnail](#adding-a-video-thumbnail).

**To configure the default time interval that video thumbnails are generated,**

1. In Experience Manager, navigate to **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL CRXDE Lite]**.

1. In the CRXDE Lite page, in the directory panel on the left, navigate t `o etc/dam/imageserver/configuration/jcr:content/settings.`

   if the directory panel is not visible, you may need to select the >> icon to the left of the Home tab.

1. On the lower-right panel, in the Properties tab, double-tap `thumbnailtime`.
1. In the Edit thumbnailtime dialog box, use the text fields to enter interval values as percentages.

    * Select the plus sign (+) icon to add one or more interval value fields. You may need to scroll to the bottom of the dialog box to see the icon.
    * Select the minus sign (-) icon to the right of an interval value field to delete it from the list.
    * Select the up arrow icon and the down arrow icon to reorder the interval values.

1. Select **[!UICONTROL OK]** to return to the Properties tab.
1. Near the upper-left corner of the CRXDE Lite page, select **[!UICONTROL Save All]**, then select the Back Home icon in the upper-left corner to return to Experience Manager.

   See [Adding a video thumbnail](#adding-a-video-thumbnail).

-->

<!--

### Adding a custom video thumbnail {#adding-a-custom-video-thumbnail-1}

These steps apply only to Dynamic Media running in Hybrid mode.

T**o add a custom video thumbnail**,

1. Navigate to an uploaded video asset that you want to add a custom video thumbnail.
1. In asset selection mode either from the List View or the Card View, select the video asset.
1. On the toolbar, select the **[!UICONTROL View Properties]** icon (a circle with an "i" in it).
1. On the video's Properties page, select **[!UICONTROL Change Thumbnail]**.
1. On the Change Thumbnail page, on the toolbar, select **[!UICONTROL Upload New Thumbnail]**.
1. Navigate to a thumbnail image you want to use, select it, then select **[!UICONTROL Open]** to begin uploading the image into Experience Manager. Following the upload, be sure you publish the image.
1. After you have successfully uploaded and published the image, in the Change Thumbnail page, select **[!UICONTROL Save Changes]**.

   The custom thumbnail is added to your video.

-->

## 更改Dynamic Media资产的Dynamic Media URL

在Dynamic Media中处理的视频既可以通过现成的查看器使用，也可以通过直接访问清单URL并通过您自己的自定义查看器播放它们。 以下是用于获取视频清单URL的API。

### 关于getVideoManifestURI API

的 `getVideoManifestURI`API通过c公开`q-scene7-api:com.day.cq.dam.scene7.api` 和可用于生成以下清单URL:

```java
/**   
* Returns the manifest url for videos 
* @param resource video resource 
* @param manifestType type of video streaming manifest being requested 
* @param onlyIfPublished return a manifest only if the video is published 
* @return the manifest url for videos 
* 
* @throws Exception 
*/
@Nullable 
String getVideoManifestURI(Resource resource, ManifestType manifestType, boolean onlyIfPublished) throws Exception;
```

#### getVideoManifestURI API参数

此API采用以下三个参数：

| 参数 | 描述 |
| --- | --- |
| `resource` | 与Dynamic Media摄取的视频对应的资源。 |
| `manifestType` | 可以是 `ManifestType.DASH` 或 `ManifestType.HLS` |
| `onlyIfPublished` | 如果清单uri仅在发布后且在投放层上可用时才生成，则设置为true。 |

要使用上述方法获取视频的清单URL，请添加 [视频编码配置文件](/help/assets/dynamic-media/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming) 到“上传视频”文件夹。 Dynamic Media会根据在分配给文件夹的视频编码文件中找到的编码来处理这些视频。 现在，您可以调用上述API来获取上传视频的清单URL。

### 错误方案

如果存在错误，API将返回空值。 Experience Manager错误日志中记录了异常。 所有此类记录错误均以 `Could not generate Video Manifest URI`. 以下情况可能会导致出现此类错误：

* 安 `IllegalArgumentException` 将记录以下任一项：

   * 的 `resource` 传递的参数为null。
   * 的 `resource` 传递的参数不是视频。
   * 的 `manifestType` 传递的参数为null。
   * 的 `onlyIfPublished` 参数将作为true进行传递，但视频未发布。
   * 未使用从Dynamic Media中设置的自适应视频集摄取视频。

* `IOException` 在连接到Dynamic Media时出现问题时被记录。
* `UnsupportedOperationException` 在 `manifestType` 传递的参数 `ManifestType.DASH`，而视频未使用短划线格式进行处理。

<!-- THE REMAINING SECTION IS FOR 6.5 ONLY 

The following is an example of the above API using servlets written in *HTTPWhiteBoard* specification. Select each tab for the code syntax.

>[!BEGINTABS]

>[!TAB Add dependency in pom.xml]

+++**Add dependency in pom.xml** 

```java
dependency> 
     <groupId>com.day.cq.dam</groupId> 
     <artifactId>cq-scene7-api</artifactId> 
     <version>5.12.64</version> 
     <scope>provided</scope> 
</dependency> 
```

+++

>[!TAB Sample servlet]

+++**Sample servlet** 

```java
@Component
        service = Servlet.class 
) 
@HttpWhiteboardServletPattern(value = ManifestServlet.SERVLET_PATTERN) 
@HttpWhiteboardContextSelect(value = Constants.SERVLET_CONTEXT_SELECTOR) 
public class ManifestServlet extends HttpServlet { 

   private static final Logger LOGGER = LoggerFactory.getLogger(ManifestServlet.class); 

   private final ObjectMapper objectMapper; 

    @Reference 
    private Scene7Service scene7Service; 

   public static final String SERVLET_PATTERN = Constants.VIDEO_API_PREFIX + "/manifestUrl"; 

   public ManifestServlet() {
         this.objectMapper = new ObjectMapper(); 
         objectMapper.setSerializationInclusion(JsonInclude.Include.NON_NULL); 
   }

   @Override 

   protected void doGet(HttpServletRequest request, HttpServletResponse response) throws IOException {
        final ResourceResolver resolver = getResourceResolver(request); 
        String assetPath = request.getParameter("assetPath"); 
        String manifest = request.getParameter("manifestType"); 
        String onlyIfPublished = request.getParameter("onlyIfPublished"); 
        Resource resource = resolver.getResource(assetPath); 
        response.setCharacterEncoding(StandardCharsets.UTF_8.toString()); 
        response.setContentType("application/json"); 
        if(resource == null) { 
            LOGGER.info("could not retrieve the resource from JCR"); 
            error("could not retrieve the resource from JCR", response); 
            return; 
        }

        String manifestUri = null; 

        try{ 
            ManifestType manifestType =  ManifestType.DASH; 
            if(manifest != null) { 
                manifestType = ManifestType.valueOf(manifest); 
            } 
            manifestUri = scene7Service.getVideoManifestURI(resource, manifestType, onlyIfPublished != null); 
            objectMapper.writeValue(response.getWriter(), new ManifestUrl(manifestUri)); 
            response.setContentType("application/json"); 
        } catch (Exception e) { 
            LOGGER.error(e.getMessage(), e); 
            error(String.format("Unable to get the manifest url for %s. %s", assetPath, e.getMessage()), response); 
        } 
    } 

    private ResourceResolver getResourceResolver(HttpServletRequest request) { 
        Object rr = request.getAttribute(AuthenticationSupport.REQUEST_ATTRIBUTE_RESOLVER); 
        if (!(rr instanceof ResourceResolver)) { 
            throw new IllegalStateException( 
                    "The request does not seem to have been created via Apache Sling's authentication mechanism."); 
        } else { 
            return (ResourceResolver) rr; 
        } 
    } 

    private void error(String errorMessage, HttpServletResponse response) throws IOException { 
        ManifestUrl errorManifest = new ManifestUrl(null); 
        errorManifest.setErrorMessage(errorMessage); 
        response.setStatus(HttpServletResponse.SC_INTERNAL_SERVER_ERROR); 
        objectMapper.writeValue(response.getWriter(), errorManifest); 
    } 
} 
```

+++

>[!TAB Response Class for servlet]

+++**Response Class for servlet** 

```java
public class ManifestUrl extends VideoResponse { 
     String manifestUrl; 
     public ManifestUrl(String manifestUrl) { 
         this.manifestUrl = manifestUrl; 
     } 
     public String getManifestUrl() { 
         return manifestUrl; 
     } 
} 

public abstract class VideoResponse { 
     String errorString; 

     public String getErrorString() { 
         return errorString; 
     } 

     public void setErrorMessage(String errorString) { 
         this.errorString = errorString; 
     } 
} 
```

+++

>[!TAB Constants file referenced in servlet]

+++**Constants file referenced in servlet** 

```java
public final class Constants { 

     private Constants() { 
     } 

     public static final String VIDEO_API_PREFIX = "/dynamicmedia/video"; 
     public static final String SERVLET_CONTEXT_SELECTOR = "(" + HttpWhiteboardConstants.HTTP_WHITEBOARD_CONTEXT_NAME + "=" + 
             DMSampleApiHttpContext.CONTEXT_NAME + ")"; 

 } 
```

+++

>[!TAB ServletContext]

+++**ServletContext** 

Mount the above servlet using a `servletContext`. The following is an example of `servletContext`. 

```java
public class DMSampleApiHttpContext extends ServletContextHelper { 

 public static final String CONTEXT_NAME = "com.adobe.dmSample"; 
 public static final String CONTEXT_PATH = "/dmSample"; 

 private final MimeTypeService mimeTypeService; 

 private final AuthenticationSupport authenticationSupport; 

 /** 
  * Constructs a new context that will use the given dependencies. 
  * 
  * @param mimeTypeService Used when providing mime type of requests. 
  * @param authenticationSupport Used to authenticate requests with sling. 
  */ 
 @Activate 
 public DMSampleApiHttpContext(@Reference final MimeTypeService mimeTypeService, 
                               @Reference final AuthenticationSupport authenticationSupport) { 
     this.mimeTypeService = mimeTypeService; 
     this.authenticationSupport = authenticationSupport; 
 } 

 // ---------- HttpContext interface ---------------------------------------- 
 /** 
  * Returns the MIME type as resolved by the <code>MimeTypeService</code> or 
  * <code>null</code> if the service is not available. 
  */ 
 @Override 
 public String getMimeType(String name) { 
     MimeTypeService mtservice = mimeTypeService; 
     if (mtservice != null) { 
         return mtservice.getMimeType(name); 
     } 
     return null; 
 } 

 /** 
  * Returns the real context path that is used to mount this context. 
  * @param req servlet request 
  * @return the context path 
  */ 
 public static String getRealContextPath(HttpServletRequest req) { 
     final String path = req.getContextPath(); 
     if (path.equals(CONTEXT_PATH)) { 
         return ""; 
     } 
     return path.substring(CONTEXT_PATH.length()); 
 } 

 /** 
  * Returns a request wrapper that transforms the context path back to the original one 
  * @param req request 
  * @return the request wrapper 
  */ 
 public static HttpServletRequest createContextPathAdapterRequest(HttpServletRequest req) { 
     return new HttpServletRequestWrapper(req) { 

         @Override 
         public String getContextPath() { 
             return getRealContextPath((HttpServletRequest) getRequest()); 
         } 

     }; 

 } 

 /** 
  * Always returns <code>null</code> because resources are all provided 
  * through individual endpoint implementations. 
  */ 
 @Override 
 public URL getResource(String name) { 
     return null; 
 } 

 /** 
  * Tries to authenticate the request using the 
  * <code>SlingAuthenticator</code>. If the authenticator or the Repository 
  * is missing this method returns <code>false</code> and sends a 503/SERVICE 
  * UNAVAILABLE status back to the client. 
  */ 
 @Override 
 public boolean handleSecurity(HttpServletRequest request, 
                               HttpServletResponse response) throws IOException { 

     final AuthenticationSupport authenticator = this.authenticationSupport; 
     if (authenticator != null) { 
         return authenticator.handleSecurity(createContextPathAdapterRequest(request), response); 
     } 

     // send 503/SERVICE UNAVAILABLE, flush to ensure delivery 
     response.sendError(HttpServletResponse.SC_SERVICE_UNAVAILABLE, 
             "AuthenticationSupport service missing. Cannot authenticate request."); 
     response.flushBuffer(); 

     // terminate this request now 
     return false; 
 } 
}
```

+++

>[!ENDTABS]



### Use the sample servlet

You invoke the servlet by performing a `GET` operation at `/dmSample/dynamicmedia/video/manifestUrl`. The following query parameters are passed: 

| Query parameter | Description |
| --- | --- |
| `assetPath` | Mandatory. The path to the video for which `manifestUrl` is generated. |
| `manifestType` | Optional. Parameter can be DASH or HLS. If it is not passed, it defaults to DASH. |
| `onlyIfPublished` | Optional. If passed, the `manifestUrl` is returned only if the video is published.  |

In this example, let us assume the following setup: 

* The company is `samplecompany`.
* The authoring instance is `http://sample-aem-author.com`.
* The folder `/content/dam/video-example` has a video encoding profile applied to it. 
* The video `scenery.mp4` is uploaded to the folder `/content/dam/video-example`.

You can invoke the servlet in following ways: 
     
| Type | Description |
| :--- | --- |
| HLS | `http://sample-aem-author.com/dmSample/dynamicmedia/video/manifestUrl?manifestType=HLS&assetPath=/content/dam/video-example/scenery.mp4`<br><br>In case DASH delivery is enabled:<br>`{"manifestUrl":"https://s7d1.scene7.com/is/content/samplecompany/scenery-AVS.m3u8?packagedStreaming=true"}`<br><br>In case DASH delivery is disabled:<br>`{"manifestUrl":"https://s7d1.scene7.com/is/content/samplecompany/scenery-AVS.m3u8"}` |
| DASH | `http://sample-aem-author.com/dmSample/dynamicmedia/video/manifestUrl?manifestType=DASH&assetPath=/content/dam/video-example/scenery.mp4`<br><br>In case DASH delivery is enabled:<br>`{"manifestUrl":"https://s7d1.scene7.com/is/content/samplecompany/scenery-AVS.mpd"}`<br><br>In case DASH delivery is disabled:<br>`{}` |
| Error: asset path is wrong | `http://sample-aem-author.com/dmSample/dynamicmedia/video/manifestUrl?manifestType=DASH&assetPath=/content/dam/video-example/scennnnnnery.mp4`<br><br>`{"errorString":"could not retrieve the resource from JCR"}` |

-->





