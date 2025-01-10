---
title: Dynamic Media 中的视频
description: 了解如何在Dynamic Media中使用视频。 查看有关视频编码、将视频发布到YouTube、查看视频报表以及向视频添加隐藏式字幕或章节标记的最佳实践。
contentOwner: Rick Brough
feature: Video Profiles,Best Practices
role: User
exl-id: 0d5fbb3e-b763-415f-8c69-ea36445f882b
source-git-commit: 222636f9520c17203df632778d3f60b62369a47b
workflow-type: tm+mt
source-wordcount: '10564'
ht-degree: 2%

---

# 视频 {#video}

本节介绍如何在Dynamic Media中使用视频。

## 快速入门：视频 {#quick-start-videos}

以下分步工作流描述旨在帮助您在Dynamic Media中快速启动和运行自适应视频集。 每一步之后，都会交叉引用主题标题，您可以在其中查找更多信息。

>[!NOTE]
>
>在Dynamic Media中使用视频之前，请确保您的Adobe Experience Manager管理员已启用并配置了Dynamic MediaCloud Service。
>
>* 请参阅“配置Dynamic Media”中的[配置Dynamic MediaCloud Service](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services)和[Dynamic Media疑难解答](/help/assets/dynamic-media/troubleshoot-dm.md)。
>

1. **通过执行以下操作上传Dynamic Media视频**：

   * 创建自己的视频编码配置文件。 或者，您只需使用Dynamic Media附带的预定义&#x200B;_自适应视频编码_&#x200B;配置文件即可。

      * [创建视频编码配置文件](/help/assets/dynamic-media/video-profiles.
      * 最大输出视频编码分辨率为8,192 × 4,320或4,320 × 8,192.md#creating-a-video-encoding-profile-for-adaptive-streaming)。
      * 了解有关[视频编码最佳实践](#best-practices-for-encoding-videos)的更多信息。

   * 将视频处理配置文件关联到一个或多个要上传主源视频的文件夹。

      * [将视频配置文件应用到文件夹](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders)。
      * 了解有关[组织数字资源](/help/assets/organize-assets.md)的详细信息。

   * 将您的主源视频上传到指定的文件夹。 添加后，将根据分配给文件夹的视频处理配置文件对视频进行编码。

      * Dynamic Media主要支持最长30分钟、最小分辨率大于25 × 25的短格式视频。
      * 支持的最大输入视频分辨率为16,384 × 16,384。
      * 您可以上传每个大小最大为15 GB的视频文件。
      * [上传您的视频](/help/assets/manage-video-assets.md#upload-and-preview-video-assets)。
      * 了解有关[支持的输入文件格式](/help/assets/file-format-support.md)的详细信息。

   * 从资源或工作流视图中监视[视频编码进度](#monitoring-video-encoding-and-youtube-publishing-progress)。

1. **通过执行以下任一操作来管理您的Dynamic Media视频**：

   * 组织、浏览和搜索视频资源

      * [组织数字资源](/help/assets/organize-assets.md)
      * [搜索视频资源](/help/assets/search-assets.md#custompredicates)或[搜索资源](/help/assets/manage-digital-assets.md#search-assets)

   * 预览和发布视频资产

      * 查看源视频、视频的编码呈现版本及其关联的缩略图：
        [预览视频](/help/assets/manage-video-assets.md#upload-and-preview-video-assets)或[预览资源](/help/assets/dynamic-media/previewing-assets.md)
        [管理视频演绎版](/help/assets/manage-digital-assets.md#managing-renditions)

      * [管理查看器预设](/help/assets/dynamic-media/managing-viewer-presets.md)
      * [发布资产](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)

   * 使用视频元数据

      * 编辑视频的属性，如标题、描述和标记、自定义元数据字段：
        [编辑视频属性](/help/assets/manage-digital-assets.md#editing-properties)

      * [管理数字资源的元数据](/help/assets/manage-metadata.md)
      * [元数据架构](/help/assets/metadata-schemas.md)

   * 审核、批准和注释视频，并保持完整的版本控制

      * [为视频添加批注](/help/assets/manage-video-assets.md#annotate-video-assets)或[为资产添加批注](/help/assets/manage-digital-assets.md#annotating)

      * [创建一个版本](/help/assets/manage-digital-assets.md#asset-versioning)
      * [在资产上启动工作流](/help/assets/manage-digital-assets.md#starting-a-workflow-on-an-asset)

      * [审核文件夹资产](/help/assets/bulk-approval.md)
      * [项目](/help/sites-cloud/authoring/projects/overview.md)

1. 通过执行以下操作之一，**Publish您的Dynamic Media视频**：

   * 如果您使用Experience Manager作为WCM（Web内容管理）系统，则可以直接将视频添加到网页。

      * [将视频添加到网页](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)。

   * 如果您使用的是第三方WCM系统，则可以将视频链接或嵌入到网页。

      * 使用URL集成视频：
        [将URL链接到您的Web应用程序](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)。

      * 在网页上使用嵌入代码集成视频：
        [在网页上嵌入视频查看器](/help/assets/dynamic-media/embed-code.md)。

   * [生成视频报告](#viewing-video-reports)。

   * [向视频添加多个字幕和音轨](#about-msma)。

## 在Dynamic Media中处理视频 {#working-with-video-in-dynamic-media}

Dynamic Media中的视频是一种端到端解决方案，能够轻松发布高质量自适应视频，以流经多个屏幕，包括台式机、平板电脑和移动设备。 自适应视频集对使用不同比特率和格式（例如400 kbps、800 kbps和1000 kbps）编码的相同视频的版本进行分组。 台式计算机或移动设备检测可用带宽。

例如，在iOS移动设备上，它会检测3G、4G或Wi-Fi等带宽。 然后，它自动从自适应视频集内的各种视频比特率中选择正确的编码视频。 视频将流式传输到台式机、移动设备或平板电脑。

此外，如果桌面或移动设备上的网络状况发生更改，则视频质量会自动进行动态切换。 此外，如果客户在桌面上进入全屏模式，则自适应视频集将使用更好的分辨率进行响应，从而改善客户的观看体验。 对于在多个屏幕和设备上播放Dynamic Media视频的客户，使用自适应视频集为他们提供了最佳可能观看体验。

视频播放器用来确定在播放期间要播放或选择的已编码视频的逻辑基于以下算法：

1. 视频播放器根据比特率加载初始视频片段，该比特率最接近在播放器本身中为“初始比特率”设置的值。
1. 视频播放器根据使用下列条件对带宽速度所做的更改进行切换：

   1. 播放器选择低于或等于估计带宽的最高带宽流。
   1. 播放器仅考虑可用带宽的80%。 然而，如果它正在切换，则更保守的是70%，以避免高估并立即切换回来。

有关算法的详细技术信息，请参阅[https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp](https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp)

在管理单个视频和自适应视频集时，支持以下内容：

* 上传多种受支持的视频格式和音频格式的视频。 将视频编码为MP4 H.264格式，以便跨多个屏幕播放。 您可以使用预定义的自适应视频预设、单个视频编码预设或自定义自己的编码来控制视频的质量和大小。

   * 生成自适应视频集时，该视频集包含MP4视频。
   * **注意**：主/源视频未添加到自适应视频集。

* 所有HTML5视频查看器中的视频字幕。
* 使用完整的元数据支持来组织、浏览和搜索视频，从而高效管理视频资产。
* 将自适应视频集交付到Web和台式机、平板电脑及移动设备。

各种iOS平台支持自适应视频流。 请参阅[Dynamic Media查看器参考指南](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/c-html5-video-reference)。

<!-- OUTDATED 2/28/22 BASED ON CQDOC-18692 Dynamic Media supports mobile video playback for MP4 H.264 video. You can find BlackBerry&reg; devices that support this video format at the following: [Supported video formats on BlackBerry&reg;](https://support.blackberry.com/kb/articleDetail?ArticleNumber=000005482).

OUTDATED 2/28/22 BASED ON CQDOC-18692 You can find Windows&reg; devices that support this video format at the following [Supported video formats on Windows&reg; Phone](https://docs.microsoft.com/en-us/windows/uwp/audio-video-camera/supported-codecs). -->

* 使用Dynamic Media视频查看器预设播放视频，包括以下内容：

   * 单个视频查看器。
   * 混合媒体查看器，将视频和图像内容组合在一起。

* 配置视频播放器以满足您的品牌推广需求。
* 将视频与简单URL或嵌入代码集成到您的网站、移动网站或移动应用程序。

<!-- GIVES a 404 See [Dynamic video playback](https://s7d9.scene7.com/s7/uvideo.jsp?asset=GeoRetail/Mop_AVS&config=GeoRetail/Universal_Video1&stageSize=640,480) sample. -->

另请参阅[Experience Manager Assets查看器参考指南](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources)中的[Experience Manager Assets查看器和Dynamic Media Classic ](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/c-html5-s7-aem-asset-viewers#viewers-aem-assets-dmc)以及[仅用于Dynamic Media的查看器](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers#viewers-for-aem-assets-only)。

## 最佳实践：使用HTML5视频查看器 {#best-practice-using-the-html-video-viewer}

Dynamic MediaHTML5视频查看器预设是可靠的视频播放器。 您可以使用它们来避免与HTML5视频播放相关的许多常见问题以及与移动设备相关的问题。 例如，缺乏自适应比特率流交付以及桌面浏览器访问范围有限。

在播放器的设计方面，您可以使用标准Web开发工具来设计视频播放器的功能。 例如，您可以使用HTML5和CSS设计按钮、控件和自定义海报图像背景，以帮助您通过自定义外观触及客户。

在查看器的播放方面，它将自动检测浏览器的视频功能。 然后，它使用HLS或DASH（也称为自适应视频流）提供视频。 或者，如果不存在这些投放方法，则改用HTML5 progressive。

>[!NOTE]
>
>要在视频中使用DASH，Adobe技术支持必须首先在您的帐户中启用它。 请参阅[在您的帐户上启用DASH](#enable-dash)。

您可以使用HTML5和CSS将设计播放组件的功能组合到单个播放器中。 它可以具有嵌入式播放，并根据浏览器的功能使用自适应流和渐进式流。 所有这些功能意味着您可以将富媒体内容的范围扩展到桌面和移动设备用户，并确保简化的视频体验。

另请参阅[Experience Manager Assets查看器参考指南](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources)中的[仅适用于Dynamic Media的查看器](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers#viewers-for-aem-assets-only)。


### 使用HTML5视频查看器在台式计算机和移动设备上播放视频 {#playback-of-video-on-desktop-computers-and-mobile-devices-using-the-html-video-viewer}

对于桌面和移动设备自适应视频流，用于比特率切换的视频基于自适应视频集中的所有MP4视频。

使用HLS、DASH或渐进式视频下载即可播放视频。 在Experience Manager的先前版本（如6.0、6.1和6.2）中，视频是通过HTTP进行流式传输的。

但是，在Experience Manager6.3及更高版本中，视频现在通过HTTPS(即HLS或DASH)进行流式传输，因为DM网关服务URL也始终使用HTTPS。 此默认行为对客户没有影响。 如果浏览器支持HTTPS，则始终会通过HTTPS进行视频流。 请参阅下表。

因此，

* 如果您的HTTPS网站支持HTTPS视频流，则可以使用流式传输。
* 如果您的HTTP网站采用HTTPS视频流，则流式传输不会有问题，并且Web浏览器不会出现混合内容问题。

DASH是国际标准，HLS是Apple标准。 两者都用于自适应视频流。 而且，这两种技术都会根据网络带宽容量自动调整回放。 它还允许客户在视频中的任意位置“搜寻”，而无需等待下载视频的其余部分。

渐进式视频的传送是通过在用户的桌面系统或移动设备上本地下载并存储视频来实现的。

下表描述了使用[Dynamic MediaHTML5视频查看器](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video#interactive-video)在台式计算机和移动设备上播放视频的设备、浏览器和方法。

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
   <td>在Windows® 8和Windows® 10上 — 每当请求DASH或HLS时，强制使用HTTPS。 已知限制： DASH或HLS上的HTTP在此浏览器/操作系统组合中不起作用<br /> <br /> Windows® 7上的渐进式下载。 对HTTP与HTTPS协议使用标准逻辑。</td>
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
   <td>Chrome</td>
   <td>HLS或DASH*自适应比特率流</td>
  </tr>
  <tr>
   <td>桌面</td>
   <td>Safari (Mac)</td>
   <td>HLS自适应比特率流</td>
  </tr>
  <tr>
   <td>移动设备</td>
   <td>Chrome(Android™ 6或更早版本)</td>
   <td>渐进式下载。</td>
  </tr>
  <tr>
   <td>移动设备</td>
   <td>Chrome (Android™ 7或更高版本)</td>
   <td>HLS或DASH*自适应比特率流/td&gt;
  </tr>
  <tr>
   <td>移动设备</td>
   <td>Android™（默认浏览器）</td>
   <td>渐进式下载。</td>
  </tr>
  <tr>
   <td>移动设备</td>
   <td>Safari (iOS)</td>
   <td>HLS自适应比特率流</td>
  </tr>
  <tr>
   <td>移动设备</td>
   <td>Chrome (iOS)</td>
   <td>HLS自适应比特率流</td>
  </tr>
 </tbody>
</table>

>[!IMPORTANT]
>
>要在视频中使用DASH，Adobe技术支持必须首先在您的帐户中启用它。 请参阅[在您的帐户上启用DASH](#enable-dash)。

<!--  THIS LINE WAS REMOVED FROM THE TABLE ABOVE ON FEB 28, 2022 BASED ON CQDOC 18692 -RSB <tr>
   <td>Mobile</td>
   <td>BlackBerry&reg;</td>
   <td>HLS or DASH</td>
  </tr>
 -->

## Dynamic Media视频解决方案的架构 {#architecture-of-dynamic-media-video-solution}

下图显示了通过DMGateway(在Dynamic Media混合模式下)上传和编码并可供公众使用的视频的整体创作工作流。

![chlimage_1-427](assets/chlimage_1-427.png)

## 视频的混合发布架构 {#hybrid-publishing-architecture-for-videos}

![chlimage_1-428](assets/chlimage_1-428.png)

## 视频编码最佳实践 {#best-practices-for-encoding-videos}

如果您已启用Dynamic Media并设置了视频Cloud Service，则&#x200B;**Dynamic Media编码视频**&#x200B;工作流会对视频进行编码。 此工作流会捕获工作流进程历史记录和失败信息。如果您已启用Dynamic Media并设置了视频Cloud Service，则在您上传视频时，**[!UICONTROL Dynamic Media编码视频]**&#x200B;工作流将自动生效。 (如果您未使用Dynamic Media，则&#x200B;**[!UICONTROL DAM更新资产]**&#x200B;工作流将生效。)

以下是编码源视频文件的最佳实践提示。

<!-- For advice about video encoding, see the following:

* [Streaming 101: The Basics — Codecs, Bandwidth, Data Rate, and Resolution](https://www.adobe.com/go/learn_s7_streaming101_en).
* [Video Encoding Basics](https://www.adobe.com/go/learn_s7_encoding_en). -->

### Source视频文件 {#source-video-files}

编码视频文件时，请使用可能具有最高质量的源视频文件。 避免使用以前编码的视频文件，因为这些文件已压缩，进一步编码会创建质量不佳的视频。

* Dynamic Media主要支持最长30分钟、最小分辨率大于25 × 25的短格式视频。
* 您可以上载每个大小最大为15 GB的主源视频文件。

下表描述了编码源视频文件之前必须具有的建议大小、长宽比和最小比特率：

| 大小 | 宽高比 | 最小比特率 |
|--- |--- |--- |
| 1024 × 768 | 4:3 | 大多数视频为4500 kbps。 |
| 1280 × 720 | 16:9 | 3000 - 6000 kbps，具体取决于视频中的移动量。 |
| 1920 × 1080 | 16:9 | 6000 - 8000 kbps，具体取决于视频中的运动量。 |

### 获取文件的元数据 {#obtaining-a-file-s-metadata}

您可以通过以下方式获取文件的元数据：使用视频编辑工具查看其元数据，或使用专为获取元数据而设计的应用程序。 以下是使用第三方应用程序MediaInfo获取视频文件元数据的说明：

1. 转到[MediaInfo下载](https://mediaarea.net/en/MediaInfo/Download)。
1. 选择并下载GUI版本的安装程序，然后按照安装说明进行操作。
1. 安装后，右键单击视频文件(仅限Windows®)并选择MediaInfo，或者打开MediaInfo并将视频文件拖到应用程序中。 您会看到与视频文件关联的所有元数据，包括其宽度、高度和fps。

### 宽高比 {#aspect-ratio}

当为主源视频文件选择或创建视频编码预设时，请确保预设具有相同的纵横比。 此方法可确保与主源视频文件的一致性。 长宽比是视频的宽高比。

要确定视频文件的纵横比，请获取该文件的元数据。 请注意文件的宽度和高度（请参阅以上获取文件的元数据）。 然后使用此公式来确定纵横比：

宽度/高度=纵横比

下表描述了公式结果如何转换为常见的宽高比选项：

| 公式结果 | 宽高比 |
|--- |--- |
| 1.33 | 4:3 |
| 0.75 | 3:4 |
| 1.78 | 16:9 |
| 0.56 | 9:16 |

例如，宽度为1440×高度为1080的视频的长宽比为1440/1080，即1.33。在这种情况下，您可以选择宽高比为4:3的视频编码预设来编码视频文件。

### 比特率 {#bitrate}

比特率是经过编码以构成视频播放一秒的数据量。 比特率以千位/秒(Kbps)为测量单位。

>[!NOTE]
>
>由于所有的编解码器都使用有损压缩，因此比特率是决定视频质量的最重要因素。 有损压缩越是压缩视频文件，质量就越低。 因此，如果所有其他特性（分辨率、帧速率和编解码器）相等，则比特率越低，压缩文件的质量就越低。

在选择比特率编码时，您可以选择两种类型：

* **[!UICONTROL 恒定比特率编码]** (CBR) — 在CBR编码过程中，比特率或每秒比特数在整个编码过程中保持不变。 CBR编码会在整个视频中将设置的数据速率保留到您的设置。 此外，CBR编码不会优化媒体文件的质量，但会节省存储空间。
如果您的视频在整个视频中包含类似的运动级别，请使用CBR。 CBR最常用于流视频内容。 另请参阅[使用自定义添加的视频编码参数](/help/assets/dynamic-media/video-profiles.md#using-custom-added-video-encoding-parameters)。

* **[!UICONTROL 可变比特率编码]** (VBR) - VBR编码会根据压缩程序所需的数据来向下调整数据速率，并将其调整到您设置的上限。 此功能意味着在VBR编码过程中，媒体文件的比特率会根据媒体文件的比特率需求动态增加或减少。
VBR编码时间较长，但产生的结果最理想；媒体文件的质量更好。 VBR最常用于http渐进式视频内容交付。

何时使用VBR而非CRB？
在选择VBR与CBR时，几乎总是建议您为媒体文件使用VBR。 VBR以具有竞争力的比特率提供更高质量的文件。 使用VBR时，请确保使用两遍编码，并将最大比特率设置为目标视频比特率的1.5倍。

选择视频编码预设时，请确保将目标用户的连接速度考虑在内。 选择数据速率为该速度80%的预设。 例如，如果目标用户的连接速度为1000 Kbps，则最佳预设为视频数据速率为800 Kbps的预设。

此表描述了典型连接速度的数据速率。

| 速度(Kbps) | 连接类型 |
|--- |--- |
| 256 | 拨号连接。 |
| 800 | 典型的移动连接。 对于此连接，请将3G体验的数据速率目标定在400到800之间。 |
| 2000 | 典型的宽带台式机连接。 对于这种连接，数据速率目标在800-2000 Kbps范围内，大多数目标平均为1200-1500 Kbps。 |
| 5000 | 典型的高宽带连接。 不建议在此上限范围内进行编码，因为大多数消费者无法以这种速度进行视频交付。 |

### 解决方法 {#resolution}

**分辨率**&#x200B;描述视频文件的高度和宽度（以像素为单位）。 大多数源视频都以高分辨率存储(例如，1920 × 1080)。 为了流传输目的，源视频被压缩成较小的分辨率(640 × 480或更小)。

分辨率和数据速率是决定视频质量的两个相互关联的因素。 要保持相同的视频质量，视频文件中的像素数越高（分辨率越高），数据速率必须越高。 例如，假定分辨率为320×240的视频文件和640×480分辨率的视频文件中每帧的像素数：

| 解决方法 | 每帧的像素 |
|--- |--- |
| 320 × 240 | 76,800 |
| 640 × 480 | 307,200 |

640 × 480文件的每帧像素是其他像素的四倍。 要获得这两个示例分辨率的相同数据速率，对640 × 480文件应用四倍压缩，这会降低视频质量。 因此，250 Kbps的视频数据速率在320 × 240分辨率下产生高质量观看，而不是在640 × 480分辨率下产生高质量观看。

通常，您使用的数据速率越高，视频的显示效果就越好，而且您使用的分辨率越高，则必须保持较高的数据速率（与较低的分辨率相比）。

由于分辨率和数据速率是相互关联的，因此在对视频进行编码时，您有两个选项：

* 选择数据速率，然后以最高分辨率进行编码，该分辨率在您选择的数据速率下显示良好。
* 选择分辨率，然后按照您选择的分辨率进行编码，以获得高质量视频。

当为主源视频文件选择（或创建）视频编码预设时，请使用此表定位正确的分辨率：

| 解决方法 | 高度(像素) | 屏幕大小 |
|--- |--- |--- |
| 240p | 240 | 小屏幕 |
| 300p | 300 | 通常用于移动设备的小屏幕 |
| 360p | 360 | 小屏幕 |
| 480p | 480 | Medium屏幕 |
| 720p | 720 | 大屏幕 |
| 1080p | 1080 | 高清大屏幕 |

支持的最大输入视频分辨率为16,384 × 16,384。 最大输出视频编码分辨率为8,192 × 4,320或4,320 × 8,192。

### Fps（每秒帧数） {#fps-frames-per-second}

在美国和日本，大多数视频的拍摄速度为29.97 fps；在欧洲，大多数视频的拍摄速度为25 fps。 电影的拍摄速度为24 fps。

选择与主源视频文件的fps速率匹配的视频编码预设。 例如，如果主源视频为25 fps，请选择具有25 fps的编码预设。 默认情况下，所有自定义编码都使用主源视频文件的fps。 因此，在创建视频编码预设时，无需明确指定fps设置。

### 视频编码维度 {#video-encoding-dimensions}

要获得最佳结果，请选择编码维度，以便源视频是所有已编码视频的整数倍。

要计算此比率，请将源宽度除以编码宽度以获得宽度比率。 然后，将源高度除以编码后的高度，以获得高度比。

如果生成的比例是整数，则表示视频得到最佳缩放。 如果生成的比例不是整数，则会通过在显示器上留下多余的像素伪像而影响视频质量。 当视频包含文本时，这种效果最为明显。

例如，假设源视频为1920 × 1080。 在下表中，三个编码的视频提供了要使用的最佳编码设置。

| 视频类型 | 宽度×高度 | 宽度比例 | 高宽比 |
|--- |--- |--- |--- |
| 源 | 1920 × 1080 | 1 | 1 |
| 已编码 | 960 × 540 | 2 | 2 |
| 已编码 | 640 × 360 | 3 | 3 |
| 已编码 | 480 × 270 | 4 | 4 |

### 编码视频文件格式 {#encoded-video-file-format}

Dynamic Media建议使用MP4 H.264视频编码预设。 由于MP4文件使用H.264视频编解码器，因此它以压缩文件大小提供高品质视频。

## 查看视频报表 {#viewing-video-reports}

>[!NOTE]
>
>视频报表仅在运行Dynamic Media — 混合模式时可用。

视频报表显示指定时间段内的多个聚合量度，以帮助您监视&#x200B;*已发布*&#x200B;个别和聚合视频是否按预期执行。 系统会汇总您整个网站中所有已发布视频的以下热门量度数据：

* 视频开始
* 完成率
* 视频平均逗留时间
* 视频花费的总时间
* 每次访问的视频数

还列出了所有&#x200B;*已发布*&#x200B;视频的表，以便您可以根据视频总开始次数跟踪网站上最常查看的视频。

在列表中选择视频名称时，会以折线图的形式显示视频的受众维系（流失）报表。 此图表显示在视频播放期间任何给定时间的查看次数。 播放视频时，垂直条与播放器中的时间指示器同步跟踪。 折线图数据中的下降指示受众从无兴趣状态下降的位置。

如果视频是在Adobe Experience Manager Dynamic Media之外进行编码，则表中的受众维系（流失）图表和播放百分比数据将不可用。

>[!NOTE]
>
>跟踪和报表数据仅基于Dynamic Media自身视频播放器及相关视频播放器预设的使用。 因此，您无法跟踪和报告其他视频播放器播放的视频。

默认情况下，首次输入视频报表时，报表显示从当前月份的第一天开始到当前月份日期结束的视频数据。 但是，您可以通过指定自己的日期范围来覆盖默认日期范围。 下次在视频报表中，将使用您指定的日期范围。

为了使视频报表正常工作，在配置Dynamic MediaCloud Service时会自动创建报表包ID。 同时，报表包ID会推送到Publish服务器，以便您在预览资源时可用于复制URL功能。 但是，此功能要求已设置Publish服务器。 如果未设置Publish服务器，您仍可以发布以查看视频报表。 但是，您必须返回到Dynamic Media云配置并选择&#x200B;**[!UICONTROL 确定]**。

**要查看视频报告：**

1. 在Experience Manager的左上角，选择Experience Manager徽标。 在左边栏中，单击![锤子图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Hammer_18_N.svg) > **[!UICONTROL Assets]** > **[!UICONTROL 视频报表]**。
1. 在“视频报表”页面上，执行以下操作之一：

   * 在右上角附近，选择&#x200B;**[!UICONTROL 刷新视频报告]**图标。
仅当报表的结束日期为当天时，才能使用刷新。 此功能可确保您能够查看自上次运行报表以来发生的视频跟踪。

   * 在右上角附近，选择&#x200B;**[!UICONTROL 日期选取器]**图标。
指定要获取其视频数据的开始和结束日期范围，然后选择**[!UICONTROL 运行报表]**。

   “排名最前的量度”组框标识了您网站上所有&#x200B;*已发布*&#x200B;视频的各种聚合量度。

1. 在列出最热门发布的视频的表中，选择要播放视频的视频名称，还可以查看视频的受众维系（流失）报表。

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


## 在您的Dynamic Media帐户中启用DASH、多字幕和多音频曲目以及人工智能生成的字幕支持 {#enable-dash}

您可以在Dynamic Media中启用对以下各项的支持：

* 短划线
* 多字幕和音轨
* AI生成的字幕（限量发布）

创建并提交Adobe客户支持案例。

启用以上三种功能中的任意一项，即启用所有功能。 因此，如果只希望启用DASH，则实际上将启用上面列出的全部三个功能。

| 功能 | 描述 |
| --- | --- |
| 短划线 | DASH(Digital Adaptive Streaming over HTTP)是视频流的国际标准，被广泛地应用于不同的视频观看者中。 在您的帐户上启用DASH后，您可以选择使用DASH或HLS进行自适应视频流传输。 或者，当在查看器预设中选择&#x200B;**[!UICONTROL auto]**&#x200B;作为播放类型时，您可以选择在播放器之间自动切换。<br>在帐户中启用DASH的一些主要优势包括：<ul><li>将DASH流视频打包用于自适应比特率流。 这种方法可以提高投放效率。 自适应流管理可确保为客户提供最佳观看体验。</li><li>使用Dynamic Media播放器优化浏览器流会在HLS和DASH流之间切换，以确保最佳服务质量。 在使用Safari浏览器时，视频播放器会自动切换到HLS。</li><li>您可以通过编辑视频查看器预设来配置首选的流方法(HLS或DASH)。</li><li>优化的视频编码可确保在启用DASH功能时不会使用额外的存储。 为HLS和DASH创建一组视频编码，以优化视频存储成本。</li><li>帮助让您的客户更容易访问视频交付。</li><li>也通过API获取流URL。</li></ul> |
| 多字幕和音轨 | 自动启用多个字幕和音轨支持将使您受益。 启用后，您上传的所有后续视频都将采用新的后端架构进行处理，该架构支持向视频添加多个字幕和音频轨道。 |
| AI生成的字幕（限量发布） | 为由AI支持的视频创建字幕。 利用人工智能，它创建视频的文字记录并将其转换为字幕。 甚至时间线也被定义了。 |

>[!IMPORTANT]
>
>在&#x200B;*之前*&#x200B;上传的任何视频在您的Dynamic Media帐户[上启用多个字幕和音轨支持都必须重新处理](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets)。 此视频重新处理步骤是必需的，这样他们才能使用多个字幕和音频跟踪功能。 重新处理之后，视频URL可继续像往常一样正常工作和播放。

**要在您的Dynamic Media帐户中启用DASH、多字幕和多声道以及人工智能生成的字幕支持，请执行以下操作：**

1. [使用该Admin Console开始创建新的支持案例](https://helpx.adobe.com/cn/enterprise/using/support-for-experience-cloud.html)。
1. 要创建支持案例，请按照说明操作，同时确保提供以下信息：

   * 主要联系人姓名、电子邮件、电话。
   * 您的Cloud Service环境（项目ID和环境ID）。
   * 您的Dynamic Media公司帐户名称。
   * 您的Dynamic Media地区：北美(NA)、亚太(APAC)或欧洲 — 中东 — 亚洲(EMEA)。
   * 指定您希望在AEM as a Cloud Service的Dynamic Media帐户中启用DASH、多字幕和多声道以及人工智能生成的字幕（有限可用性）支持。

1. Adobe客户支持根据提交请求的顺序将您添加到客户等待列表中。
1. 当Adobe准备好处理您的请求时，客户支持联系您以协调并设置目标启用日期。
1. Adobe客户支持会在完成后通知您。
1. 现在，执行以下一项或多项操作：

   * 照常创建[视频查看器预设](/help/assets/dynamic-media/managing-viewer-presets.md#creating-a-new-viewer-preset)。
   * 照常创建[视频配置文件](/help/assets/dynamic-media/video-profiles.md)。
   * [向视频中添加多个字幕和音轨](#add-msma)。


<!-- HIDDEN AS OF OCTOBER 7, 2024 AS PER EMAIL REQUEST FROM RIYA MIDHA ON SAME DATE 

## About multiple caption and audio track support for videos in Dynamic Media{#about-msma}

With multiple caption and audio track capability in Dynamic Media, you can easily add multiple captions and audio tracks to a primary video. This capability means that your videos are accessible to a global audience. You can customize a single, published primary video to a global audience in multiple languages and adhere with accessibility guidelines for different geographical regions. Authors can also manage the captions and audio tracks from a single tab in the user interface.

   ![Captions and audio tracks tab in Dynamic Media along with a table showing uploaded .VTT caption files and uploaded .MP3 audio track files for a video.](/help/assets/dynamic-media/assets/msma-caption-audiotracks-tab2.png)


Some of the use cases to consider for adding multiple captions and audio tracks to your primary video include the following:


| Type | Use case | 
| --- | --- |
| Captions | Multiple language support<br>Descriptive text for accessibility |
|Audio tracks | Multiple language support<br>Commentary tracks<br>Descriptive audio |


All [video formats supported in Dynamic Media](/help/assets/file-format-support.md) and all Dynamic Media video viewers-except the Dynamic Media Video_360 viewer-are supported for use with multiple captions and audio tracks.

Multi-caption and multi-audio track capability is available for your Dynamic Media account by way of a feature toggle that must be enabled (turned on) by Adobe Customer Support.

### Add multiple captions and audio tracks to your video {#add-msma}

Before you add multiple caption and audio tracks to your video, be sure you already have the following in-place:

* Dynamic Media is set up in an AEM environment.
* A [Dynamic Media Video profile is applied to the folder where your videos are ingested](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders).
* [Multi-caption, and multi-audio track is enabled on your Dynamic Media account](/help/assets/dynamic-media/video.md#enable-dash).

Added captions and captions are supported with WebVTT and Adobe VTT formats. And, added audio track files are supported with MP3 format.

>[!IMPORTANT]
>
>Any videos that you uploaded before enabling multiple caption and audio track support on your Dynamic Media account, [must be reprocessed](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). This video reprocessing step is necessary so that multiple caption and audio track capability is available to them. The video URLs continue to work and play as usual, after reprocessing.

**To add multiple captions and audio tracks to your video:**

1. [Upload your primary video to a folder](/help/assets/manage-video-assets.md#upload-and-preview-video-assets) that already has a video profile assigned to it.
1. Navigate to the uploaded video asset that you want to add multiple caption and audio tracks.
1. In asset selection mode, either from the List View or the Card View, select the video asset.
1. On the toolbar, select the Properties icon (a circle with an "i" in it). 

   ![Asset properties button.](/help/assets/dynamic-media/assets/msma-selectedasset-propertiesbutton.png)*Selected video asset in Card View.*

1. On the video's Properties page, select the **[!UICONTROL Captions & Audio Tracks]** tab.


   >[!TIP]
   >If you do not see the [!UICONTROL Captions & Audio Tracks] tab, it means either one of two things:
   >* The folder in which the selected video resides does not have a video profile assigned to it. In which case, see [Apply a video profile to the folder](/help/assets/dynamic-media/video-profiles.md#applying-video-profiles-to-specific-folders)
   >* Or, Dynamic Media must reprocess the video. In which case, see [Reprocess Dynamic Media assets in a folder](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

    When you have completed either one of the above tasks, return to these steps.

   ![Asset properties](/help/assets/dynamic-media/assets/msma-audiotracks.png)*Captions and audio tracks tab on the video's Properties page.*

1. (Optional) To add one or more caption files to a video, do the following:

    * Select **[!UICONTROL Upload Captions]**.
    * Navigate to, and select, one or more `.vtt` (Video Text Tracks) files and open them.
    * For captions to be visible on the media player, you must add required details (metadata) about each caption file that you uploaded. Select the pencil icon to the right of a caption file name. In the Edit Caption dialog box, enter the following required details about the file, then select **[!UICONTROL Save]**. Repeat this process for each caption file that you uploaded:


    | Caption metadata | Description | 
    | --- | --- | 
    Filename | The default filename is derived from the original filename. The filename can be changed only while uploading and cannot be changed later. Filename character requirements are the same as for AEM Assets.<br>The same filename cannot be used for additional caption files and audio track files. |
    | Language | Select the language of the caption. |
    | Type | Select the type of caption that you are using.<br>**Subtitle** - The caption text displayed with the video that translates or transcribes the dialogue.<br>**Caption** - The caption text includes background noises and speaker identification. It also includes other relevant details alongside the translation or transcription of dialogue. This functionality makes the content more accessible to individuals who are deaf or hard of hearing. |
    | Label | The text that is displayed for the caption's name in the **[!UICONTROL Select audio or caption]** pop-up list in the media player. The label is what a customer sees that corresponds to a subtitle or caption track. For example, English (CC). |

    You can change or edit caption metadata later, if necessary. When the video is published, these details are reflected on public URLs in published videos.

1. (Optional) To add one or more audio tracks to a video, do the following:

    * Select **[!UICONTROL Upload Audio Tracks]**.
    * Navigate to, and select, one or more .mp3 files and open them.
    * To make audio tracks visible in the **[!UICONTROL Select audio or caption]** pop-up list on the media player, add the required details for each audio track file. Ensure you include all necessary information for proper display. Select the pencil icon to the right of an audio track file name. In the Edit Audio Track dialog box, enter the following required details, then select **[!UICONTROL Save]**. Repeat this process for each audio track file that you uploaded.

    | Audio Track metadata | Description |
    | --- | --- |
    | Filename | The default filename is derived from the original filename. The filename can be changed only while uploading and cannot be changed later. Filename character requirements are the same as for AEM Assets.<br>The same filename cannot be used for additional audio track files or caption files.| 
    | Language | Select the language of the audio track. |
    | Type | Select the type of audio track that you are using.<br>**Original** - The audio track originally attached to the video and represented as `[Original]` in the label with English language selected by default. While **[!UICONTROL Label]** and **[!UICONTROL Language]** can be changed in the **[!UICONTROL Edit Audio Track]** dialog box, it defaults to the original values if the primary video is reprocessed.<br>**Standard** - An add-on audio track for a language other than the original.<br>**Audio description** - An audio track that also includes a descriptive narration of non-verbal actions and gestures in the video, making content more accessible for individuals who are visually impaired. |
    | Label | The text that is displayed as the audio track's name in the **[!UICONTROL Select audio or caption]** pop-up list in the media player. The label is what a customer sees that corresponds to an audio track. For example, `English [Original]`. The label of audio attached to a video is set to `[Original]` by default. |

    You can change or edit this audio track metadata later, if necessary. When the video is published, these details are reflected on public URLs in published videos.

1. In the upper-right corner of the page, from the **[!UICONTROL Save & Close]** drop-down list, select **[!UICONTROL Save]**. The files are uploaded and metadata processing begins, as seen in the Status column of the interface.

    >[!NOTE]
    >
    >Based on the caching settings of your instance, the metadata processing can take several minutes before it is reflected in preview and in published URLs.

1. (Optional) If you selected **[!UICONTROL Save & Close]** in the previous step, instead of selecting **[!UICONTROL Save]**, you can still view the processing status of the uploaded files. See [View the lifecycle status of uploaded caption and audio track files](/help/assets/dynamic-media/video.md#lifecycle-status-video).

1. (Optional) Preview the video before publishing to ensure the captions and audio work as expected. See [Preview a video that has multiple captions and audio tracks](/help/assets/dynamic-media/video.md#preview-video-audio-subtitle).

1. Publish the video. See [Publish assets](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md). -->



## 关于Dynamic Media中对视频的多个字幕和音轨支持{#about-msma}

借助Dynamic Media中的多个字幕和音轨功能，您可以轻松添加多个音轨。 您还可以使用自己的`.vtt`（视频字幕）文件或AI生成的字幕文件添加多个字幕文件。 Dynamic Media中的AI生成字幕旨在通过自动生成准确且同步的字幕来增强视频可访问性和参与度。 该技术使用高级人工智能算法将口语内容转录为文本，然后作为字幕显示在视频上。 此技术的一些关键功能包括：

* **自动转录：**&#x200B;人工智能系统将口语文字实时转录为文本，确保快速准确地生成字幕。
* **多语言支持：**&#x200B;可以自动以60多种语言提供字幕，从而更易于联系全球受众。
* **增强辅助功能：**&#x200B;通过提供字幕，使耳聋或听力缺佳的观众或喜欢关机看视频的人更容易访问视频。
* **更好的参与度：**&#x200B;字幕有助于保持查看者的注意力并提高理解力，尤其是在嘈杂的环境中或当查看者的母语与视频的语言不同时。

这些功能使AI支持的字幕成为内容创作者寻求提高其视频内容可访问性和参与度的宝贵工具。

![Dynamic Media中的“字幕和音轨”选项卡，以及显示视频的上传.VTT字幕文件和上传.MP3音轨文件的表。](/help/assets/dynamic-media/assets/msma-caption-audiotracks-tab2.png)

向主视频添加多个字幕和音频轨道需要考虑的一些用例包括：

| 类型 | 用例 |
|--- |--- |
| **字幕** | 多语言支持 |
|  | 用于辅助功能的描述性文本 |
| **曲目** | 多语言支持 |
|  | 评论轨道 |
|  | 描述性音频 |

除Dynamic Media *Video_360*&#x200B;查看器外，所有Dynamic Media ](/help/assets/file-format-support.md)和所有Dynamic Media视频查看器都支持所有[视频格式以便与多个字幕和音轨一起使用。

通过必须由Adobe客户支持启用（打开）的功能切换，您的Dynamic Media帐户可以使用多字幕和多音频跟踪功能。

### 为视频添加多个字幕和音轨 {#add-msma}

在将多个字幕和音频轨道添加到视频之前，请确保已具备以下功能：

* Dynamic Media是在AEM环境中设置的。
* [Dynamic Media视频配置文件已应用于从中摄取视频的文件夹](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders)。
* [已在您的Dynamic Media帐户中启用多字幕/音轨和人工智能生成的字幕](#enable-dash)。

WebVTT和AdobeVTT格式支持添加的字幕。 此外，添加的MP3格式音频轨道文件也受支持。

>[!IMPORTANT]
>
>对于在&#x200B;*之前*&#x200B;在您的Dynamic Media帐户上启用多个字幕/音轨支持或人工智能生成的字幕上传的视频，[您需要重新处理它们](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets)。 此重新处理步骤确保这些视频可以使用多个字幕/音频轨道和AI生成的字幕功能。 在重新处理之后，视频URL将继续正常工作并播放。

**要向视频添加多个字幕和音轨：**

1. [将主视频上传到已分配了视频配置文件的文件夹](/help/assets/manage-video-assets.md#upload-and-preview-video-assets)。
1. 导航到要添加多个字幕和音频轨道的上传视频资产。
1. 在资源选择模式下，从![查看卡片图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewCard_18_N.svg) （卡片视图）或![查看列表图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewList_18_N.svg) （列表视图）中选择视频资源。
1. 在工具栏上，单击![信息图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Info_18_N.svg)属性。
   ![所选的视频资产在视频缩略图图像上带有复选标记，并且工具栏上突出显示了“查看属性”。](/help/assets/dynamic-media/assets/msma-selectedasset-propertiesbutton.png)*在卡片视图中选择的视频资产。*
1. 在视频的“属性”页面上，选择&#x200B;**[!UICONTROL 字幕和音轨]**&#x200B;选项卡。

   >[!TIP]
   >如果您看不到&#x200B;**[!UICONTROL 字幕和音轨]**&#x200B;选项卡，则表示以下两种情况之一：
   >
   >* 所选视频所在的文件夹没有分配视频配置文件。 在这种情况下，请参阅[将视频配置文件应用到文件夹](/help/assets/dynamic-media/video-profiles.md#applying-video-profiles-to-specific-folders)
   >* 或者，Dynamic Media必须重新处理视频。 在这种情况下，请参阅[重新处理文件夹](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets)中的Dynamic Media资源。
   >
   >完成以上任一任务后，请返回这些步骤。

   ![属性页面上的字幕和音轨选项卡。](/help/assets/dynamic-media/assets/msma-audiotracks.png)
   在视频的“属性”页面上，*字幕和音频曲目选项卡。*

1. 要将一个或多个音频轨道添加到视频，请执行以下操作：
   1. 选择&#x200B;**[!UICONTROL 上传音轨]**。
   1. 导航到一个或多个.mp3文件并将其打开。
   1. 要使音轨在媒体播放器上的&#x200B;**[!UICONTROL 选择音频或题注]**&#x200B;弹出列表中可见，必须添加有关每个音轨文件的所需详细信息。 这样做可确保正确列出并访问所有音频轨道。 单击音频轨道文件名右侧的![绘制图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Draw_18_N.svg)。 在&#x200B;**编辑音轨**&#x200B;对话框中，输入以下必需的详细信息：

      | 音轨元数据 | 描述 |
      |--- |--- |
      | 文件名 | 默认文件名是从原始文件名派生的。 只能在上传时更改文件名，以后不能更改。 文件名字符要求与AEM Assets相同。<br>不能对附加的音轨文件或字幕文件使用相同的文件名。 |
      | 语言 | 选择正确的音轨语言。 |
      | 类型 | 选择您正在使用的音轨类型。<br>**原始** — 音频曲目最初附加到视频，并在标签中以`[Original]`形式表示，默认情况下选择`English`语言。 虽然&#x200B;**[!UICONTROL 标签]**&#x200B;和&#x200B;**[!UICONTROL 语言]**&#x200B;可以在&#x200B;**[!UICONTROL 编辑音轨]**&#x200B;对话框中更改，但如果重新处理主视频，则默认为原始值。<br>**标准** — 用于原始语言以外的语言的附加音频轨道。<br>**音频描述** — 一个音频轨道，其中还包括视频中非语言操作和手势的描述性叙述，使视障人士更容易访问内容。 |
      | 标签 | 在媒体播放器的&#x200B;**[!UICONTROL 选择音频或题注]**&#x200B;弹出列表中显示为音频轨道名称的文本。 该标签是客户看到的与音轨对应的内容。 例如，`English [Original]`。默认情况下，附加到视频的音频标签设置为`[Original]`。 |

      您可以稍后更改或编辑此音频轨道元数据（如有必要）。 发布视频时，这些详细信息会反映在已发布视频的公共URL上。

   1. 在页面的右上角附近，在&#x200B;**[!UICONTROL 保存并关闭]**&#x200B;下拉列表中，单击&#x200B;**[!UICONTROL 保存]**。
   1. 执行下列操作之一：
      * 对上传的每个音频轨道文件重复此过程。
      * 继续下一步以向视频添加字幕。

1. 要将一个或多个字幕文件添加到视频，请选择以下哪个用例最适合您的场景：

   |  | 用例 | 创建要使用的题注选项 |
   | --- | --- | --- |
   | **选项1** | 我有自己以前存在的字幕文件，这些文件使用我想要使用的语言。<br>请参阅下面的&#x200B;**选项1**。 | **[!UICONTROL 上载文件]** |
   | **选项2** | 我希望人工智能能生成多种语言的字幕文件。<br>请参阅下面的&#x200B;**选项2**。 | **[!UICONTROL 转换音轨]** |
   | **选项3** | 题注文件(`.vtt`)中的文本需要更正，重新上传以替换旧的`.vtt`文件，然后让AI翻译更正后的文件。<br>请参阅下面的&#x200B;**选项3**。 | **[!UICONTROL 翻译字幕]** |

   ![创建字幕选项。](/help/assets/dynamic-media/assets/msma-createcaption.png)
   *创建字幕下拉菜单为您提供三个选项：上传文件、转换音轨和翻译字幕。*

+++**选项1：** *我拥有自己预先存在的描述文件，这些文件使用我要使用的语言* （**[!UICONTROL 上传文件]**&#x200B;选项）

   1. 在页面的右上角附近，单击&#x200B;**[!UICONTROL 创建题注]** > **[!UICONTROL 上传文件]**。
   1. 导航到一个或多个预先存在的`.vtt`文件并将其打开，并选择这些文件。
   1. 为了在媒体播放器上显示字幕，您&#x200B;*必须*&#x200B;添加有关您上传的&#x200B;*每个*&#x200B;字幕文件的所需详细信息。 单击标题文件名右侧的![绘制图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Draw_18_N.svg)。 在&#x200B;**编辑题注**&#x200B;对话框中，输入有关文件的以下必需详细信息：

      | 题注元数据 | 描述 |
      |--- |--- |
      | 文件名 | 默认文件名是从原始文件名派生的。 只能在上传时更改文件名，以后不能更改。 文件名字符要求与AEM Assets相同。<br>不能将同一文件名用于其他字幕文件和音轨文件。 |
      | 语言 | 选择题注的语言。 处理字幕文件后，此语言字段将变为不可编辑（灰显） |
      | 类型 | 选择您正在使用的字幕类型。<br>**子标题** — 与翻译或转录此对话框的视频一起显示的标题文本。<br>**字幕** — 字幕文本包括背景噪音、说话人辨别和其他相关细节，以及对话翻译或转录，增强了耳聋或听力缺佳者的可访问性。 |
      | 标签 | 在媒体播放器的&#x200B;**[!UICONTROL 选择音频或题注]**&#x200B;弹出列表中为题注名称显示的文本。 标签是客户看到的与字幕或描述跟踪对应的内容。 例如 `English (CC)`。 |

      您可以稍后更改或编辑字幕元数据（如有必要）。 发布视频时，这些详细信息会反映在已发布视频的公共URL上。

   1. 在页面的右上角附近，在&#x200B;**[!UICONTROL 保存并关闭]**&#x200B;下拉列表中，单击&#x200B;**[!UICONTROL 保存]**。 文件已上载，元数据处理开始，如界面的&#x200B;**状态**&#x200B;列中所示。

      >[!NOTE]
      >
      >根据实例的缓存设置，元数据处理可能需要几分钟时间，然后才能反映在预览和已发布的URL中。

   1. 如果您在上一步中选择了&#x200B;**[!UICONTROL 保存并关闭]**，而不是选择&#x200B;**[!UICONTROL 保存]**，您仍可以查看已上载文件的处理状态。 请参阅[查看已上传的字幕和音轨文件的生命周期状态](#lifecycle-status-video)。
   1. 继续执行步骤8。

+++

+++**选项2：** *我希望AI生成多种语言的字幕文件* （**[!UICONTROL 转换音轨]**&#x200B;选项）

   1. 在页面的右上角附近，单击&#x200B;**[!UICONTROL 创建字幕]** > **[!UICONTROL 转换音轨]**。

      ![转换音轨对话框。](/help/assets/dynamic-media/assets/msma-convertaudiotracks.png)
      *“转换音轨”对话框使用AI生成多种语言的字幕文件。*

   1. 在&#x200B;**转换音轨**&#x200B;对话框中，设置以下选项：

      | 选项 | 描述 |
      |--- |--- |
      | 要转换的音轨 | 单击![向下V形图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg)，然后选择上载的音频轨道文件，您希望使用AI从中生成字幕。 |
      | 输出语言 | 单击![向下V形图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg)，然后选择您希望字幕文件显示的一个或多个语言。<br>要删除选定的语言，请单击![关闭图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Close_18_N.svg)。<br>在视频播放期间，媒体播放器中会按照您在此处选择它们的顺序显示语言列表。 |

   1. 单击&#x200B;**[!UICONTROL 完成]**。
   1. 在页面的右上角附近，在&#x200B;**[!UICONTROL 保存并关闭]**&#x200B;下拉列表中，单击&#x200B;**[!UICONTROL 保存]**。
   1. 再次单击&#x200B;**[!UICONTROL 字幕和音轨]**&#x200B;选项卡。 已创建一个或多个字幕文件并开始处理，如界面的&#x200B;**状态**&#x200B;列中所示。 另请参阅[查看上传的字幕和音轨文件的生命周期状态](#lifecycle-status-video)。

      >[!NOTE]
      >
      >根据实例的缓存设置，元数据处理可能需要几分钟时间，然后才能反映在预览和已发布的URL中。

   1. （可选）单击题注文件名右侧的![绘制图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Draw_18_N.svg)。 在&#x200B;**编辑标题**&#x200B;对话框中，可以编辑有关文件的以下详细信息：

      | 题注元数据 | 描述 |
      | --- | --- |
      | 类型 | 选择您正在使用的字幕类型。<br>**子标题** — 与翻译或转录此对话框的视频一起显示的标题文本。<br>**字幕** — 字幕文本包含背景噪音和说话人辨别。 其中还包括其他相关信息，以及对话的翻译或转录。 这种方法使耳聋或听力缺佳的用户更容易访问内容。 |
      | 标签 | 在媒体播放器的&#x200B;**[!UICONTROL 选择音频或题注]**&#x200B;弹出列表中为题注名称显示的文本。 标签是客户看到的与字幕或描述跟踪对应的内容。 例如 `English (CC)`。 |

      如果需要，您可以稍后更改或编辑某些字幕元数据。 发布视频时，这些元数据详细信息会反映在已发布视频中的公共URL上。
   1. 继续执行步骤8。

+++

+++**选项3：** *需要更正字幕文件(`.vtt`)中的文本，重新上传以替换旧的`.vtt`文件，然后让AI翻译更正后的文件* （**[!UICONTROL 翻译字幕]**&#x200B;选项）

   1. 单击&#x200B;**[!UICONTROL 创建标题]** > **[!UICONTROL 翻译标题]**。 如果已经添加并处理了一个或多个描述文件，则此选项可用。

      ![翻译字幕对话框。](/help/assets/dynamic-media/assets/msma-translate-captions.png)
      *通过“翻译字幕”对话框，您可以使用现有的字幕文件让AI生成多种语言的新字幕文件。*

   1. 在&#x200B;**翻译字幕**&#x200B;对话框中，设置以下选项：

      | 选项 | 描述 |
      |--- |--- |
      | 要翻译的题注 | 单击![向下V形图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg)，然后选择一个需要使用AI生成字幕的字幕文件。 |
      | 输出语言 | 单击![向下V形图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg)，然后选择您希望字幕文件显示的一个或多个语言。<br>要删除选定的语言，请单击![关闭图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Close_18_N.svg)。<br>在视频播放期间，媒体播放器中会按照您在此处选择它们的顺序显示语言列表。 |

   1. 单击&#x200B;**[!UICONTROL 完成]**。
   1. 在页面的右上角附近，在&#x200B;**[!UICONTROL 保存并关闭]**&#x200B;下拉列表中，单击&#x200B;**[!UICONTROL 保存]**。
   1. 再次单击&#x200B;**[!UICONTROL 字幕和音轨]**&#x200B;选项卡。 已创建一个或多个字幕文件并开始处理，如界面的&#x200B;**状态**&#x200B;列中所示。 另请参阅[查看上传的字幕和音轨文件的生命周期状态](#lifecycle-status-video)。

      >[!NOTE]
      >
      >根据实例的缓存设置，元数据处理可能需要几分钟时间，然后才能反映在预览和已发布的URL中。

   1. （可选）单击题注文件名右侧的![绘制图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Draw_18_N.svg)。 在&#x200B;**编辑标题**&#x200B;对话框中，可以编辑有关文件的以下详细信息：

      | 题注元数据 | 描述 |
      | --- | --- |
      | 类型 | 选择您正在使用的字幕类型。<br>**子标题** — 与翻译或转录此对话框的视频一起显示的标题文本。<br>**字幕** — 字幕文本还包括背景噪音、说话人辨别。 其中还包括其他相关信息，以及对话的翻译或转录。 这种方法使耳聋或听力缺佳的用户更容易访问内容。 |
      | 标签 | 在媒体播放器的&#x200B;**[!UICONTROL 选择音频或题注]**&#x200B;弹出列表中为题注名称显示的文本。 标签是客户看到的与字幕或描述跟踪对应的内容。 例如 `English (CC)`。 |

      如果需要，您可以稍后更改或编辑某些字幕元数据。 发布视频时，这些元数据详细信息会反映在已发布视频中的公共URL上。

   1. 继续执行步骤8。

+++

1. （可选）在发布之前预览视频，以确保字幕和音频按预期工作。 查看[预览具有多个字幕和音轨的视频](#preview-video-audio-subtitle)。
1. Publish视频。 查看[Publish资源](publishing-dynamicmedia-assets.md)。

#### 关于将字幕和音频跟踪文件添加到已发布的视频

在将其他字幕或音频轨道文件上传到已发布的视频后，这些文件在准备就绪后具有`Processed`状态。 然后，您可以在Dynamic Media中预览视频以查看或收听新文件。

但是，在预览后，您必须&#x200B;*再次发布*&#x200B;视频，才能同时发布新添加的字幕或音轨文件。 发布后，字幕或音频将随公共Dynamic Media URL一起提供。

>[!NOTE]
>
>根据实例的缓存设置，元数据更新可能需要几分钟才能反映在预览和已发布的URL中。

在您已将Dynamic Media配置为立即发布的情况下，上传其他字幕或音频文件会立即触发上传字幕或音频文件后的视频发布。

>[!CAUTION]
>
>将字幕文件或音频文件上传到已发布或已取消发布的视频时，如果您&#x200B;[*重新处理*](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets)&#x200B;该视频，文件将被删除。 只有视频的原始音频保持不变。 在这种情况下，必须再次将字幕文件和音频跟踪文件重新上传到视频。

#### 向具有带标题修饰符的现有URL的视频添加多个标题

Dynamic Media支持通过URL修饰符添加带有视频的单个字幕。 请参阅[向视频添加字幕](#adding-captions-to-video)。

对已发布的视频所做的多个字幕更改优先于通过URL修饰符添加的字幕。

**要向具有带标题修饰符的现有URL的视频添加多个标题，请执行以下操作：**

1. 上传已作为视频修饰符添加的字幕文件，以便您明确管理文件。
1. 根据需要上传任何其他字幕文件。
1. 像往常一样Publish视频。
现在，带标题修饰符的现有URL可以加载多个标题。

### 查看上传的字幕和音轨文件的生命周期状态 {#lifecycle-status-video}

您可以观察上传到主视频的任何字幕或音频跟踪文件的生命周期状态。 您可以在&#x200B;**属性**&#x200B;的&#x200B;**字幕和音轨**&#x200B;选项卡中执行此操作。

**要查看视频的生命周期状态：**

1. 导航到要查看其生命周期状态的视频资源。
1. 在资源选择模式下，从![查看卡片图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewCard_18_N.svg) （卡片视图）或![查看列表图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewList_18_N.svg) （列表视图）中选择视频资源。
1. 在工具栏上，单击![信息图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Info_18_N.svg)属性。
1. 在&#x200B;**属性**&#x200B;页面上，选择&#x200B;**[!UICONTROL 字幕和音轨]**&#x200B;选项卡。
1. 在&#x200B;**[!UICONTROL 状态]**&#x200B;列中，记下每个字幕或音频文件的状态。

| 字幕和音轨的状态 | 描述 |
| --- | --- |
| 正在处理 | 添加并保存新的字幕或音轨文件时，它进入“正在处理”状态。 Dynamic Media通过将流清单附加到主视频来处理该文件。 |
| 已处理 | 处理完成后，字幕或音轨文件，或与主视频相关的原始音轨将显示为“已处理”状态。 在&#x200B;*发布实时视频之前，您可以预览显示为“已处理”的字幕和音轨文件*。 |
| 发布时间 | “已发布”状态表示与主视频的“已发布”状态类似。 Assets会在主视频发布后发布，并且可在公共Dynamic Media URL上使用。 |
| 失败 | “失败”状态表示字幕或音频轨道文件的处理未完成。 请删除字幕或音轨文件，然后重新上传。 |
| 已取消发布 | 明确取消发布已发布的主视频时，您添加到该视频的任何字幕或音频跟踪文件也会被取消发布。 |


### 为具有多个音频轨道的视频设置默认音频

默认情况下，视频的原始音频设置为要播放的默认音频。

但是，可以将任何上传的音频轨道文件设置为将视频加载到查看器后播放的默认音频。 在“属性”用户界面的&#x200B;**字幕和音轨**&#x200B;选项卡下，`Default`标签将应用于音频音轨文件的右侧，以便播放视频。

>[!NOTE]
>
>默认音频的播放还取决于以下浏览器中的设置：
>
>* Chrome — 播放视频中设置的默认音频。
>* Safari — 如果在Safari中设置默认语言，则使用设置的默认语言播放音频（如果视频清单中有的话）。 否则，将播放设置为视频属性一部分的默认音频。

**要为具有多个音频轨道的视频设置默认音频：**

1. 导航到要设置其默认音频轨道的视频资产。
1. 在资源选择模式下，从![查看卡片图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewCard_18_N.svg) （卡片视图）或![查看列表图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewList_18_N.svg) （列表视图）中选择视频资源。
1. 在工具栏上，单击![信息图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Info_18_N.svg)属性。
1. 在“属性”页面上，选择&#x200B;**[!UICONTROL 字幕和音轨]**&#x200B;选项卡。
1. 在&#x200B;**音轨**&#x200B;标题下，选择要设置为视频的默认音轨文件。
1. 单击![音频图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Audio_18_N.svg) **[!UICONTROL 设置为默认值]**。
1. 在&#x200B;**设置为默认值**&#x200B;对话框中，单击&#x200B;**[!UICONTROL 替换]**。

   ![声道标题具有选定的声道文件名并突出显示“设置为默认值”按钮。](/help/assets/dynamic-media/assets/msma-defaultaudiotrack.png)*正在设置视频的默认音轨。*

1. 单击右上角的&#x200B;**[!UICONTROL 保存并关闭]**。
1. Publish视频。 查看[Publish资源](publishing-dynamicmedia-assets.md)。

### 预览具有多个字幕和音频轨道的视频 {#preview-video-audio-subtitle}

将字幕文件和音轨文件上传到视频并进行处理后，您可以使用Dynamic Media视频查看器预览所有不同的音轨。 这样做有助于您了解视频在客户心目中的外观和声音，并确保视频按预期运行。

如果对视频感到满意，则可以使用以下任意一种方法[发布视频](publishing-dynamicmedia-assets.md)。

请参阅[在网页上嵌入视频查看器或图像查看器](/help/assets/dynamic-media/embed-code.md)。
查看[将URL链接到您的Web应用程序](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)。 如果您的交互式内容包含具有相对URL的链接，尤其是指向Experience Manager Sites页面的链接，则基于URL的链接方法不可用。
请参阅[将Dynamic Media Assets添加到页面](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)。

>[!NOTE]
>
>默认的“Experience Manager预览”选项卡不显示多个字幕和音轨。 原因是这些磁道与Dynamic Media相关联，并且只能使用Dynamic Media查看器预览查看。

**要预览具有多个字幕和音轨的视频，请执行以下操作：**

1. 在&#x200B;**[!UICONTROL Assets]**&#x200B;中，导航到已添加多个字幕和音轨的现有视频。
1. 单击视频资产可在预览模式下将其打开。
1. 在预览页面的左上角附近，单击![左边栏图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_RailLeft_18_N.svg) ![V形向下图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg)，然后选择&#x200B;**[!UICONTROL 查看器]**。

   ![显示“查看者”选项的下拉列表。](/help/assets/dynamic-media/assets/msma-selectviewers.png)

1. 在页面的左上角附近，单击![左边栏图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_RailLeft_18_N.svg)查看器![向下V形图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg)，然后选择要用于视频预览的查看器。

1. 在页面的右下角附近，单击语音泡泡图标，然后选择要听到的音频或字幕/字幕，或者同时选择两者。

   ![视频查看器中的“音频和字幕”弹出列表。](/help/assets/dynamic-media/assets/msma-selectaudiosubtitle.png)*模拟用户选择音频和字幕进行视频播放。*

1. 要开始播放，请单击![PLay图标](https://spectrum.adobe.com/static/icons/workflow_22/Smock_PlayCircle_22_N.svg)。
如有需要，请单击![最大化图标](https://spectrum.adobe.com/static/icons/workflow_22/Smock_Maximize_22_N.svg)以最大化查看窗口。
请注意页面左下角附近的**[!UICONTROL URL]**&#x200B;和&#x200B;**[!UICONTROL Embed]**&#x200B;按钮。 使用这些按钮分别[将视频的URL链接到您的Web应用程序](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)或[将视频嵌入网页](/help/assets/dynamic-media/embed-code.md)。
1. 在预览页面的右上角附近，单击&#x200B;**[!UICONTROL 关闭]**。

### 从视频中删除字幕或音频跟踪文件

您可以从视频中删除字幕或音频跟踪文件。 删除已发布的字幕或音频轨道文件会自动反映在视频的已发布URL中。

无法删除从主视频中提取的原始音频轨道。

**要从视频中删除字幕或音频轨道文件：**

1. 导航到要设置其默认音频轨道的视频资产。
1. 在资源选择模式下，从![查看卡片图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewCard_18_N.svg) （卡片视图）或![查看列表图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewList_18_N.svg) （列表视图）中选择视频资源。
1. 在工具栏上，单击![信息图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Info_18_N.svg)属性。
1. 在“属性”页面上，选择&#x200B;**[!UICONTROL 字幕和音轨]**&#x200B;选项卡。
1. 执行以下任一操作：

   * 字幕 — 在&#x200B;**字幕**&#x200B;标题下，选择一个或多个要从视频中删除的字幕文件，然后单击![删除图标](https://spectrum.adobe.com/static/icons/workflow_22/Smock_Delete_22_N.svg)**[!UICONTROL 删除]**。
   * 音轨 — 在&#x200B;**音轨**&#x200B;标题下，选择一个或多个要从视频中删除的音轨文件，然后单击![删除图标](https://spectrum.adobe.com/static/icons/workflow_22/Smock_Delete_22_N.svg) **[!UICONTROL 删除]**。

1. 在“删除”对话框中，单击&#x200B;**[!UICONTROL 确定]**。
1. Publish视频。

### 下载已上传到视频的字幕或音频跟踪文件

您可以下载为视频上传的任何字幕或音频跟踪文件。 您可以选择将所有选定的文件下载为`.zip`，或者为每个文件创建单独的下载文件夹。

无法下载从主视频文件提取的原始音轨。

**用例：**&#x200B;如果在`.vtt`文件中发现错误，则可能需要下载字幕文件。 只需下载不正确的`.vtt`文件，在纯文本编辑器中打开它，然后进行更正。 保存`.vtt`文件后，再次上传。 然后，使用&#x200B;**[!UICONTROL 翻译字幕]**&#x200B;选项重新翻译更正的`.vtt`文件。

**要下载上载到视频的字幕或音轨文件：**

1. 导航到要设置其默认音频轨道的视频资产。
1. 在资源选择模式下，从![查看卡片图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewCard_18_N.svg) （卡片视图）或![查看列表图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewList_18_N.svg) （列表视图）中选择视频资源。
1. 在工具栏上，单击![信息图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Info_18_N.svg)属性。
1. 在&#x200B;**属性**&#x200B;页面上，选择&#x200B;**[!UICONTROL 字幕和音轨]**&#x200B;选项卡。
1. 执行以下任一操作：

   * 字幕 — 在&#x200B;**字幕**&#x200B;标题下，选择要从视频下载的一个或多个字幕文件，然后单击![下载图标](https://spectrum.adobe.com/static/icons/workflow_22/Smock_Download_22_N.svg)**[!UICONTROL 下载]**。
   * 音轨 — 在&#x200B;**音轨**&#x200B;标题下，选择要从视频下载的一个或多个音轨文件，然后单击![下载图标](https://spectrum.adobe.com/static/icons/workflow_22/Smock_Download_22_N.svg) **[!UICONTROL 下载]**。

1. 在“下载”对话框中，设置以下选项：

   | 下载选项 | 描述 |
   |--- |--- |
   | 另存为 | 使用在“另存为”文本字段中指定的默认文件名，或指定您自己的名称。 |
   | 为每个资源创建单独的文件夹 | 为您选择下载的每个字幕文件或音轨文件创建一个文件夹。 |
   | 电子邮件 | 使用默认电子邮件程序将.zip文件发送到指定的电子邮件地址。 |
   | 资源 | 指定正在下载的文件数以及所有选定文件的组合总大小。 取消选择此选项会使&#x200B;**[!UICONTROL 下载]**&#x200B;按钮变暗（关闭），从而阻止您下载任何文件。 |
   | 演绎版 | 演绎版是指原始文件的替代版本或预览，通常是较小或分辨率较低的版本。 如果显示为0 B，则可能意味着没有可用的替代版本，或者它太小而无法注册大小。 |

1. 选择&#x200B;**[!UICONTROL 下载]**。
1. Publish视频。 查看[Publish资源](publishing-dynamicmedia-assets.md)。

<!-- ## About AI-generated captions for videos in Dynamic Media

AI-powered captions in Dynamic Media are designed to enhance video accessibility and engagement by automatically generating accurate and synchronized subtitles. This technology uses advanced AI algorithms to transcribe spoken content into text, which is then displayed as captions on the video. Here are some key features.

* **Automatic Transcription:** The AI system transcribes spoken words from an existing audio file into text in real-time, ensuring that captions are generated quickly and accurately.
* **Multilingual Support:** It supports more than 60 languages, making it easier to reach a global audience. You can even translate your existing captions to different languages.
* **Enhanced Accessibility:** By providing captions, videos become more accessible to viewers who are deaf or hard of hearing, as well as those who prefer to watch videos with the sound off.
* **Improved Engagement:** Captions can help retain viewer attention and improve comprehension, especially in noisy environments or when the viewer's native language is different from the video's language.

These features in Dynamic Media make AI-powered video aptions a valuable tool for content creators looking to enhance their video content's accessibility and engagement. -->

## 向视频添加隐藏式字幕 {#adding-captions-to-video}

>[!IMPORTANT]
>
>Adobe建议您在您的Dynamic Media帐户上[启用多个字幕和音轨功能](#enable-dash)。 这样，您就可以利用最新的Dynamic Media后端架构和简化的工作流程，向视频添加字幕、字幕和音轨。

通过将隐藏式字幕添加到单个视频或自适应视频集，您可以将视频扩展到全球市场。 通过添加隐藏式字幕，您无需对音频进行配音，也无需使用母语人士重新录制每种语言的音频。 视频以所录制的语言播放。 出现外语字幕是为了让不同语言的人仍然能够理解音频部分。

隐藏式字幕还为耳聋或听力缺佳的用户提供了更好的辅助功能。

>[!NOTE]
>
>您使用的视频播放器必须支持隐藏式字幕的显示。

另请参阅Dynamic Media中的[辅助功能](/help/assets/dynamic-media/accessibility-dm.md)。

Dynamic Media可以将字幕文件转换为JSON(JavaScript对象表示法)格式。 这种转换意味着，您可以将JSON文本作为隐藏但完整的视频转录内容嵌入到网页中。 然后，搜索引擎可以对内容进行爬网/索引，以使视频更容易被发现，并为客户提供有关视频内容的更多详细信息。

有关在URL中使用JSON函数的更多信息，请参阅[提供静态（非图像）内容](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/c-serving-static-nonimage-contents#image-serving-api)。

**要向视频添加字幕：**

1. 使用第三方应用程序或服务创建视频字幕文件。

   确保您创建的文件遵循WebVTT（Web视频文本跟踪）标准。 字幕文件扩展名为`.vtt`。 您可以了解有关WebVTT字幕标准的更多信息。

   请参阅[WebVTT： Web视频字幕格式](https://w3c.github.io/webvtt/)。

   有许多网站同时提供免费和高级的工具和服务，可用于在Dynamic Media之外创作WebVTT描述文件。<!-- THE FOLLOWING LINK IS NO LONGER LIVE. CHECKED DECEMBER 13, 2023 For example, to create a simple video caption file with no styling, you can use the following free online caption authoring and editing tool: -->

   <!-- [WebVTT Caption Maker](https://testdrive-archive.azurewebsites.net/Graphics/CaptionMaker/Default.html)

   For best results, use the tool in Internet Explorer 9 or above, Google Chrome, or Safari.

   In the tool, in the **[!UICONTROL Enter URL of video file]** field, paste the copied URL of your video file and then select **[!UICONTROL Load]**. See [Obtain a URL for an Asset](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset) to get the URL to the video file itself which you can then paste into the **[!UICONTROL Enter URL of video file field]**. Internet Explorer, Chrome, or Safari can then natively play back the video. -->

按照站点中的屏幕说明创作和保存WebVTT文件。 完成后，复制字幕文件内容并将其粘贴到纯文本编辑器中，并以VTT文件扩展名保存。

>[!NOTE]
>
>为了全局支持多种语言的视频字幕，WebVTT标准要求您为要支持的每种语言创建单独的`.vtt`文件和调用。

通常，您希望将标题`.vtt`文件命名为与视频文件相同的名称，并将其附加到语言区域设置，如 — EN、-FR或 — DE。 这样，它就可以帮助您使用现有WCM系统自动生成视频URL。

1. 在Experience Manager中，将您的WebVTT描述文件上传到DAM。
1. 导航到&#x200B;*已发布*&#x200B;视频资产，以将其与您上传的字幕文件相关联。

   请注意，只有在首次&#x200B;*发布*&#x200B;资产&#x200B;*后*，才可复制 URL。

   查看[Publish资源](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)。

1. 执行下列操作之一：

   * 若要获取弹出式视频查看器体验，请单击&#x200B;**[!UICONTROL URL]**&#x200B;按钮。 在“URL”对话框中，选择URL并将其复制到剪贴板，然后将URL粘贴到简单的文本编辑器中。 使用以下语法附加复制的视频的URL：

     `&caption=<server_path>/is/content/<path_to_caption.vtt_file,1>`

     记下描述路径末尾的`,1`。 紧跟路径中的VTT文件扩展名之后，您可以选择分别设置为`,1`或`,0`来启用（打开）或禁用（关闭）视频播放器栏上的隐藏式字幕按钮。

   * 要获得嵌入的视频查看器体验，请单击&#x200B;**[!UICONTROL 嵌入代码]**。 在“嵌入代码”对话框中，选择嵌入代码，并将其复制到剪贴板，然后将该代码粘贴到简单的文本编辑器中。 使用以下语法附加复制的嵌入代码：

     `videoViewer.setParam("caption","<path_to_caption.vtt_file,1>");`

     请注意题注路径末尾的`,1`。 紧跟路径中的VTT文件扩展名之后，您可以选择分别设置为`,1`或`,0`来启用（打开）或禁用（关闭）视频播放器栏上的隐藏式字幕按钮。

## 向视频添加章节标记 {#adding-chapter-markers-to-video}

您可以通过将章节标记添加到单个视频或自适应视频集，使长格式视频更易于观看和导航。 当用户播放视频时，可以选择视频时间轴上的章节标记（也称为视频洗刷）。 他们可以轻松导航到兴趣点，或立即跳转到新内容、培训和演示。

>[!NOTE]
>
>使用的视频播放器必须支持使用章节标记。 Dynamic Media视频播放器不支持章节标记，但是使用第三方视频播放器可能不支持。

<!-- OBSOLETE CONTENT OBSOLETE CONTENT If desired, you can create and brand your own custom video viewer with chapters instead of using a video viewer preset. For instructions on creating your own HTML5 viewer with chapter navigation, in the Adobe Scene7 Viewer SDK for HTML5 guide, reference the heading "Customizing Behavior Using Modifiers" under the classes `s7sdk.video.VideoPlayer` and `s7sdk.video.VideoScrubber`. The Adobe Scene7 Viewer SDK is available as a download from [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html). -->

您可以像创建字幕一样为视频创建章节列表。 即，创建一个WebVTT文件。 但请注意，此文件必须与任何WebVTT描述文件分开。 不能将字幕和章节合并到一个WebVTT文件中。

您可以使用以下示例作为创建具有章节导航的WebVTT文件时所使用的格式示例：

### 包含视频章节导航的WebVTT文件 {#webvtt-file-with-video-chapter-navigation}

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

在上述示例中，`Chapter 1`是提示标识符，是可选的。 `00:00:000 --> 01:04:364`的提示时间以`00:00:000`格式指定章节的开始时间和结束时间。 最后三位数为毫秒，可保留为`000`（如果首选）。 `The bicycle store behind it all`的章节标题是章节内容的实际描述。 当用户将鼠标指针悬停在时间轴中的可视提示点上时，提示标识符、开始提示时间和章节标题都会显示在视频播放器的弹出窗口中。

由于您使用的是HTML5视频查看器，因此请确保您创建的章节文件遵循WebVTT（Web视频文本跟踪）标准。 章节文件扩展名为`.vtt`。 您可以了解有关WebVTT字幕标准的更多信息。

请参阅[WebVTT： Web视频字幕格式](https://w3c.github.io/webvtt/)。

**向视频添加章节标记：**

1. 将`.vtt`文件保存为UTF8编码，以避免章节标题文本中的字符呈现出现问题。

   通常，您希望将章节VTT文件的名称与视频文件相同，并将其附加到章节中。 这样，它就可以帮助您使用现有WCM系统自动生成视频URL。
1. 在Experience Manager中，上传WebVTT章节文件。

   查看[上传资源](/help/assets/manage-digital-assets.md#uploading-assets)。

1. 执行下列操作之一：

   <table>
     <tbody>
      <tr>
       <td>对于弹出视频查看器体验，</td>
       <td>
       <ol>
       <li>导航到<i>已发布的</i>视频资产，以将其与您上传的章节文件相关联。 请注意，只有在首次<i>发布</i>资产<i>后</i>，才可复制 URL。请参阅<a href="/help/assets/dynamic-media/publishing-dynamicmedia-assets.md">发布Assets。</a></li>
       <li>从下拉菜单中选择<strong>查看器</strong>。</li>
       <li>在左边栏中，选择视频查看器预设名称。 视频预览会在单独的页面中打开。</li>
       <li>在左边栏的底部，单击<strong>URL</strong>按钮。</li>
       <li>在“URL”对话框中，选择URL并将其复制到剪贴板，然后将URL粘贴到简单的文本编辑器中。</li>
       <li>使用以下语法附加复制的视频的URL，以便将其与章节文件的复制URL关联：<br /> <br /> <code>&navigation=<<i>full_copied_URL_path_to_chapter_file</i>.vtt></code><br /> </li>
       </ol> </td>
      </tr>
      <tr>
       <td>对于嵌入的视频查看器体验，<br /> </td>
       <td>
       <ol>
       <li>导航到<i>已发布的</i>视频资产，以将其与您上传的章节文件相关联。 请注意，只有在首次<i>发布</i>资产<i>后</i>，才可复制 URL。请参阅<a href="/help/assets/dynamic-media/publishing-dynamicmedia-assets.md">发布Assets。</a></li>
       <li>从下拉菜单中选择<strong>查看器</strong>。</li>
       <li>在左边栏中，选择视频查看器预设名称。 视频预览会在单独的页面中打开。</li>
       <li>在左边栏的底部，选择<strong>嵌入</strong>。</li>
       <li>在“嵌入代码”对话框中，选择并将整个代码复制到剪贴板，然后将其粘贴到简单的文本编辑器中。</li>
       <li>使用以下语法附加视频的嵌入代码，以便将其与复制的URL关联到章节文件：<br /> <br /> <code>videoViewer.setParam("navigation","&lt;<i>full_copied_URL_path_to_chapter_file</i>.vtt>"</code></li>
       </ol> </td>
      </tr>
     </tbody>
   </table>


## 关于视频缩略图 {#about-video-thumbnails}

视频缩略图是视频帧的缩减版本，或者向客户表示视频的图像资产。 缩略图应当用于鼓励客户选择视频。

Experience Manager中的所有视频都必须具有关联的缩略图。 默认情况下，上传视频到Experience Manager时，第一帧将用作缩略图。 但是，您可以自定义缩略图以用于品牌推广或视觉搜索。 自定义视频缩略图时，可以播放视频并在要使用的帧上暂停。 或者，您可以选择已在数字资产管理器中上传并&#x200B;*发布*&#x200B;的图像资产。

当视频的缩略图发生更改时，将跳过通过Asset compute服务在重新处理视频时生成缩略图。

自定义视频缩略图的功能仅在您将视频配置文件应用到视频所在的文件夹之后才可用。

### 添加自定义视频缩略图 {#adding-a-custom-video-thumbnail}

1. 确保您已完成以下操作：

   * 已为您的视频资产创建文件夹。
   * [已将视频配置文件应用到文件夹](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders)。

   * [已将视频上传到文件夹](/help/assets/manage-video-assets.md#upload-and-preview-video-assets)。


1. 导航到要更改其缩略图图像的已上传视频资产。
1. 在资源选择模式下，从![查看卡片图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewCard_18_N.svg) （卡片视图）或![查看列表图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewList_18_N.svg) （列表视图）中选择视频资源。
1. 在工具栏上，单击![信息图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Info_18_N.svg)属性。
1. 在视频的“属性”页面上，单击&#x200B;**[!UICONTROL 更改缩略图]**。
1. 在“更改缩略图”对话框中，执行以下操作之一：

   * 要将视频中的帧用作新缩略图，请执行以下操作：

      * 在工具栏上，单击&#x200B;**[!UICONTROL 从视频中选择帧]**&#x200B;选项卡。
      * 单击![播放图标](https://spectrum.adobe.com/static/icons/workflow_22/Smock_PlayCircle_22_N.svg)。
      * 在要捕获为视频新缩略图的帧上单击![暂停图标](https://spectrum.adobe.com/static/icons/workflow_22/Smock_PauseCircle_22_N.svg)。

   * 要将图像资产用作新缩略图，请执行以下操作：

      * 在工具栏上，单击&#x200B;**[!UICONTROL 从Assets中选择缩略图]**&#x200B;选项卡。
      * 单击&#x200B;**[!UICONTROL 选择缩略图]**&#x200B;按钮。
      * 导航到要使用的之前上传和发布的图像资产。 资源会自动调整大小以用作视频的缩略图。
      * 选择图像资源，然后单击&#x200B;**[!UICONTROL 选择]**。

1. 在“更改缩略图”对话框中，单击&#x200B;**[!UICONTROL 保存更改]**。
1. 在视频的“属性”页面的右上角，单击&#x200B;**[!UICONTROL 保存并关闭]**&#x200B;或&#x200B;**[!UICONTROL 保存]**。



<!--

## About video thumbnails in Dynamic Media Hybrid mode{#about-video-thumbnails-in-dynamic-media-hybrid-mode}

You can choose from one of ten thumbnail images automatically generated by Dynamic Media to add to your video. The video player displays your selected thumbnail when a video asset is used with the Dynamic Media component in the authoring environment of Experience Manager Sites, Experience Manager Mobile, or Experience Manager Screens. The thumbnail serves as a static picture that best represents the contents of your entire video and further encourages users to select the Play button.

Based on the total time of the video, Dynamic Media captures ten (default) thumbnail images at 1%, 11%, 21%, 31%, 41%, 51%, 61%, 71%, 81%, and 91% into the video. The ten thumbnails persist meaning that if you decide to choose a different thumbnail later on, you do not need to regenerate the series. You preview the ten thumbnail images and then select the one you want to use with your video. If you want to change to default you can use CRXDE Lite to configure the time interval that thumbnail images are generated. For example, if you only wanted to generate a series of four evenly spaced thumbnail images from your video, you can configure the interval time at 24%, 49%, 74%, and 99%.

Ideally, you can add a video thumbnail anytime after you upload your video but before you publish the video on your website.

If you prefer, you can choose to upload a custom thumbnail to represent your video instead of using a thumbnail generated by Dynamic Media. For example, you could create a custom thumbnail image that has the title of your video, an eye-catching opening image, or a very specific image captured from your video. The custom video thumbnail image that you upload should have a maximum resolution of 1280 &times; 720 pixels (minimum width of 640 pixels) and be no larger than 2MB.

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

   If you configured new default time intervals, or you uploaded a new video to replace the existing video, you need to have Dynamic Media regenerate the thumbnails.

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

1. On the lower-right panel, in the Properties tab, double-select `thumbnailtime`.
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

## 更改Dynamic Media资源的Dynamic Media URL

开箱即用的查看器可以播放在Dynamic Media中处理的视频。 您还可以通过直接访问清单URL并使用您自己的自定义查看器来播放它们。 以下是获取视频清单URL的API。

### 关于getVideoManifestURI API

`getVideoManifestURI`API通过c`q-scene7-api:com.day.cq.dam.scene7.api`公开，可用于生成以下清单URL：

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
| `resource` | 与Dynamic Media已摄取的视频对应的资源。 |
| `manifestType` | 可以是`ManifestType.DASH`或`ManifestType.HLS` |
| `onlyIfPublished` | 如果清单URI仅在投放层上发布且可用的情况下生成，则设置为true。 |

要使用上述方法获取视频的清单URL，请将[视频编码配置文件](/help/assets/dynamic-media/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming)添加到“上传视频”文件夹。 Dynamic Media会根据在分配给文件夹的视频编码文件中找到的编码来处理这些视频。 现在，您可以调用上述API以获取已上传视频的清单URL。

### 错误方案

如果出现错误，则API返回空值。 异常记录在Experience Manager错误日志中。 所有此类记录错误以`Could not generate Video Manifest URI`开头。 以下情况可能会导致发生此类错误：

* `IllegalArgumentException`被记录为以下任意项：

   * 传递的`resource`参数为null。
   * 传递的`resource`参数不是视频。
   * 传递的`manifestType`参数为null。
   * `onlyIfPublished`参数作为true传递，但视频未发布。
   * 未使用Dynamic Media中的自适应视频集摄取视频。

* 在连接到Dynamic Media时出现问题时，`IOException`将被记录。
* 当传递的`manifestType`参数为`ManifestType.DASH`且未使用DASH格式处理视频时，将记录`UnsupportedOperationException`。

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





