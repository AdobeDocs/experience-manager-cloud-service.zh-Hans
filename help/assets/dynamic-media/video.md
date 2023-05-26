---
title: Dynamic Media 中的视频
description: 了解如何在Dynamic Media中使用视频。 查看视频编码、将视频发布到YouTube、查看视频报表以及在视频中添加隐藏式字幕、字幕或章节标记的最佳实践。
contentOwner: Rick Brough
feature: Video Profiles
role: User
exl-id: 0d5fbb3e-b763-415f-8c69-ea36445f882b
source-git-commit: 124b363fe341199fdc9b25d25bbf2a9bc8f87d87
workflow-type: tm+mt
source-wordcount: '5868'
ht-degree: 2%

---

# 视频 {#video}

本节介绍如何在Dynamic Media中使用视频。

## 快速入门：视频 {#quick-start-videos}

以下分步工作流描述旨在帮助您快速启动和运行Dynamic Media中的自适应视频集。 每个步骤之后，都有对主题标题的交叉引用，您可以在其中查找更多信息。

>[!NOTE]
>
>在Dynamic Media中使用视频之前，请确保您的Adobe Experience Manager管理员已启用并配置了Dynamic MediaCloud Services。
>
>* 参见 [配置Dynamic MediaCloud Services](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services) 在配置Dynamic Media和 [Dynamic Media疑难解答](/help/assets/dynamic-media/troubleshoot-dm.md).
>


1. **上传Dynamic Media视频** ，方法是：

   * 创建您自己的视频编码配置文件。 或者，您只需使用预定义的 _自适应视频编码_ Dynamic Media随附的资料。

      * [创建视频编码配置文件](/help/assets/dynamic-media/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming).
      * 详细了解 [视频编码的最佳实践](#best-practices-for-encoding-videos).
   * 将视频处理配置文件与一个或多个要上传主源视频的文件夹关联。

      * [将视频配置文件应用到文件夹](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders).
      * 详细了解 [组织数字资源](/help/assets/organize-assets.md).
   * 将您的主源视频上传到文件夹。 将视频添加到文件夹时，会根据您分配给该文件夹的视频处理配置文件对它们进行编码。

      * Dynamic Media主要支持最长30分钟、最小分辨率大于25 x 25的短格式视频。
      * 您可以上传每个大小不超过15 GB的视频文件。
      * [上传您的视频](/help/assets/manage-video-assets.md#upload-and-preview-video-assets).
      * 详细了解 [支持的输入文件格式](/help/assets/file-format-support.md).
   * 监视方式 [视频编码正在进行](#monitoring-video-encoding-and-youtube-publishing-progress) 从资产或工作流视图中。




1. **管理您的Dynamic Media视频** 通过执行以下任一操作：

   * 组织、浏览和搜索视频资产

      * [组织数字资源](/help/assets/organize-assets.md)
      * [搜索视频资产](/help/assets/search-assets.md#custompredicates) 或 [搜索资源](/help/assets/manage-digital-assets.md#search-assets)
   * 预览和发布视频资产

      * 查看源视频、视频的编码演绎版及其相关缩略图：
         [预览视频](/help/assets/manage-video-assets.md#upload-and-preview-video-assets) 或 [预览资源](/help/assets/dynamic-media/previewing-assets.md)
         [管理视频演绎版](/help/assets/manage-digital-assets.md#managing-renditions)

      * [管理查看器预设](/help/assets/dynamic-media/managing-viewer-presets.md)
      * [发布资产](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)
   * 使用视频元数据

      * 编辑视频的属性，如标题、描述和标记、自定义元数据字段：
         [编辑视频属性](/help/assets/manage-digital-assets.md#editing-properties)

      * [管理数字资源的元数据](/help/assets/manage-metadata.md)
      * [元数据架构](/help/assets/metadata-schemas.md)
   * 审查、批准和注释视频，并保持完整的版本控制

      * [为视频添加批注](/help/assets/manage-video-assets.md#annotate-video-assets) 或 [对资产添加注释](/help/assets/manage-digital-assets.md#annotating)

      * [创建版本](/help/assets/manage-digital-assets.md#asset-versioning)
      * [在资产上启动工作流](/help/assets/manage-digital-assets.md#starting-a-workflow-on-an-asset)

      * [查看文件夹资产](/help/assets/bulk-approval.md)
      * [项目](/help/sites-cloud/authoring/projects/overview.md)




1. **发布Dynamic Media视频** 通过执行以下操作之一：

   * 如果您使用Experience Manager作为WCM（Web内容管理）系统，则可以直接将视频添加到网页。

      * [将视频添加到网页](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).
   * 如果您使用的是第三方Web内容管理系统，则可以将视频链接或嵌入到网页。

      * 使用URL集成视频：
         [将 URL 关联到您的 Web 应用程序](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md).

      * 在网页上使用嵌入代码集成视频：
         [在网页上嵌入视频查看器](/help/assets/dynamic-media/embed-code.md).
   * [生成视频报表](#viewing-video-reports).

   * [向视频添加字幕](#adding-captions-to-video).



## 在Dynamic Media中处理视频 {#working-with-video-in-dynamic-media}

Dynamic Media中的视频是一种端到端解决方案，可让您轻松发布高质量的自适应视频，以便在多个屏幕（包括台式机、平板电脑和移动设备）上实现流式传输。 自适应视频集对使用不同比特率和格式（如400 kbps、800 kbps和1000 kbps）编码的相同视频的版本进行分组。 台式计算机或移动设备检测可用带宽。

例如，在iOS移动设备上，它会检测3G、4G或Wi-Fi等带宽。 然后，它自动从自适应视频集内的各种视频比特率中选择正确的编码视频。 视频将流式传输到台式机、移动设备或平板电脑。

此外，如果桌面或移动设备上的网络状况发生变化，则视频质量会自动进行动态切换。 此外，如果客户在桌面上进入全屏模式，自适应视频集将使用更好的分辨率进行响应，从而改善客户的观看体验。 通过使用自适应视频集，客户可以在多个屏幕和设备上播放Dynamic Media视频，您可以获得最佳播放体验。

视频播放器用来确定在播放期间要播放或选择的已编码视频的逻辑基于以下算法：

1. 视频播放器根据比特率加载初始视频片段，该比特率最接近在播放器本身中为“初始比特率”设置的值。
1. 视频播放器根据对带宽速度的更改进行切换，使用的标准如下：

   1. 播放器选择低于或等于估计带宽的最高带宽流。
   1. 播放器只考虑了80%的可用带宽。 然而，如果它调高了，它更保守，只有70%，以避免高估并立即回调。

有关算法的详细技术信息，请参阅 [https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp](https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp)

对于管理单个视频和自适应视频集，支持以下内容：

* 从多种支持的视频格式和音频格式上传视频并将视频编码为MP4 H.264格式以便在多个屏幕上播放。 您可以使用预定义的自适应视频预设、单个视频编码预设或自定义自己的编码来控制视频的质量和大小。

   * 生成自适应视频集时，该视频集包含MP4视频。
   * **注释**：主/源视频未添加到自适应视频集。

* 所有HTML5视频查看器中的视频字幕。
* 组织、浏览和搜索视频，全面支持元数据，以便有效管理视频资产。
* 将自适应视频集交付到Web和台式机、平板电脑和移动设备。

各种iOS平台均支持自适应视频流。 参见 [Dynamic Media查看器参考指南](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/c-html5-video-reference.html).

<!-- OUTDATED 2/28/22 BASED ON CQDOC-18692 Dynamic Media supports mobile video playback for MP4 H.264 video. You can find BlackBerry&reg; devices that support this video format at the following: [Supported video formats on BlackBerry&reg;](https://support.blackberry.com/kb/articleDetail?ArticleNumber=000005482).

OUTDATED 2/28/22 BASED ON CQDOC-18692 You can find Windows&reg; devices that support this video format at the following [Supported video formats on Windows&reg; Phone](https://docs.microsoft.com/en-us/windows/uwp/audio-video-camera/supported-codecs). -->

* 使用Dynamic Media视频查看器预设播放视频，包括以下内容：

   * 单个视频查看器。
   * 结合了视频和图像内容的混合媒体查看器。

* 配置视频播放器以满足您的品牌推广需求。
* 使用简单的URL或嵌入代码将视频集成到您的网站、移动网站或移动应用程序。

参见 [动态视频播放](https://s7d9.scene7.com/s7/uvideo.jsp?asset=GeoRetail/Mop_AVS&amp;config=GeoRetail/Universal_Video1&amp;stageSize=640,480) 示例。

另请参阅 [Experience Manager Assets和Dynamic Media Classic查看器](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/c-html5-s7-aem-asset-viewers.html#viewers-aem-assets-dmc) 和 [仅适用于Experience Manager Assets的查看器](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers.html#viewers-for-aem-assets-only) 在 [Dynamic Media查看器参考指南](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html).

## 最佳实践：使用HTML5视频查看器 {#best-practice-using-the-html-video-viewer}

Dynamic Media HTML5视频查看器预设是可靠的视频播放器。 您可以使用它们来避免与HTML5视频播放相关的许多常见问题以及与移动设备相关的问题。 例如，缺乏自适应比特率流投放和有限的桌面浏览器访问范围。

在播放器的设计方面，您可以使用标准Web开发工具来设计视频播放器的功能。 例如，您可以使用HTML5和CSS设计按钮、控件和自定义海报图像背景，以帮助您通过自定义外观触及客户。

在查看器的播放方面，它会自动检测浏览器的视频功能。 然后，它使用HLS或DASH（也称为自适应视频流）提供视频。 或者，如果不存在这些投放方法，则改用HTML5 progressive。

>[!NOTE]
>
>要在视频中使用DASH，必须首先由您帐户上的Adobe技术支持启用。 参见 [在您的帐户上启用DASH](#enable-dash).

您可以使用HTML5和CSS将设计播放组件的功能组合到单个播放器中。 它可以具有嵌入式播放，并根据浏览器的功能使用自适应流和渐进式流。 所有这些功能意味着，您可以将富媒体内容的范围扩展到桌面和移动设备用户，并确保简化的视频体验。

另请参阅 [仅适用于Experience Manager Assets的查看器](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers.html#viewers-for-aem-assets-only) 在 [Dynamic Media查看器参考指南](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html).


### 使用HTML5视频查看器在桌面计算机和移动设备上播放视频 {#playback-of-video-on-desktop-computers-and-mobile-devices-using-the-html-video-viewer}

对于桌面和移动设备自适应视频流，用于比特率切换的视频基于自适应视频集中的所有MP4视频。

使用HLS或DASH或渐进式视频下载进行视频播放。 在早期版本的Experience Manager（如6.0、6.1和6.2）中，视频是通过HTTP进行流式传输的。

但是，在Experience Manager6.3及更高版本中，视频现在通过HTTPS（即HLS或DASH）进行流式传输，因为DM网关服务URL也始终使用HTTPS。 此默认行为对客户没有影响。 也就是说，除非浏览器不支持HTTPS，否则将始终通过HTTPS进行视频流。 （见下表）。

因此，

* 如果您的HTTPS网站支持HTTPS视频流，则可以使用流式传输。
* 如果您的HTTP网站包含HTTPS视频流，则可以使用流处理，并且Web浏览器中没有出现混合内容问题。

DASH是国际标准，HLS是Apple标准。 两者都用于自适应视频流。 而且，这两种技术都会根据网络带宽容量自动调整播放。 它还允许客户在视频中的任何位置“搜寻”，而无需等待视频的其余部分下载。

渐进式视频是通过将视频下载并存储到用户的桌面系统或移动设备上的方式交付的。

下表介绍了在台式机和移动设备上使用的视频设备、浏览器和播放方法 [Dynamic MediaHTML5视频查看器](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video.html#interactive-video).

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
   <td>在Windows® 8和Windows® 10上 — 只要请求DASH或HLS，就强制使用HTTPS。 已知限制：DASH或HLS上的HTTP在此浏览器/操作系统组合中不起作用<br /> <br /> 在Windows® 7上 — 渐进式下载。 使用标准逻辑选择HTTP与HTTPS协议。</td>
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
   <td>Safari (Mac)</td>
   <td>HLS自适应比特率流</td>
  </tr>
  <tr>
   <td>移动设备</td>
   <td>Chrome (Android™ 6或更低版本)</td>
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
>*要在视频中使用DASH，必须首先由您帐户上的Adobe技术支持启用。 参见 [在您的帐户上启用DASH](#enable-dash).)

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

此 **Dynamic Media编码视频** 如果您已启用Dynamic Media并设置了视频Cloud Services，则工作流会对视频进行编码。 此工作流会捕获工作流进程历史记录和失败信息。如果您已启用Dynamic Media并设置了视频Cloud Services，则 **[!UICONTROL Dynamic Media编码视频]** 上传视频时，工作流会自动生效。 (如果您没有使用Dynamic Media，则 **[!UICONTROL DAM更新资产]** 工作流将生效。)

以下是编码源视频文件的最佳实践提示。

<!-- For advice about video encoding, see the following:

* [Streaming 101: The Basics — Codecs, Bandwidth, Data Rate, and Resolution](https://www.adobe.com/go/learn_s7_streaming101_en).
* [Video Encoding Basics](https://www.adobe.com/go/learn_s7_encoding_en). -->

### 源视频文件 {#source-video-files}

在编码视频文件时，请使用可能具有最高质量的源视频文件。 避免使用以前编码的视频文件，因为这些文件已压缩，进一步编码会创建质量缺佳的视频。

* Dynamic Media主要支持最长30分钟、最小分辨率大于25 x 25的短格式视频。
* 您可以上传每个大小最大为15 GB的主源视频文件。

下表描述了源视频文件在编码之前必须具有的建议大小、长宽比和最小比特率：

| 大小 | 宽高比 | 最小比特率 |
|--- |--- |--- |
| 1024 X 768 | 4:3 | 大多数视频为4500 kbps。 |
| 1280 X 720 | 16:9 | 3000 - 6000 kbps，具体取决于视频中的移动量。 |
| 1920 X 1080 | 16:9 | 6000 - 8000 kbps，具体取决于视频中的移动量。 |

### 获取文件的元数据 {#obtaining-a-file-s-metadata}

您可以通过以下方式获取文件的元数据：使用视频编辑工具查看其元数据，或使用专为获取元数据而设计的应用程序。 以下是使用第三方应用程序MediaInfo获取视频文件元数据的说明：

1. 转到 [MediaInfo下载](https://mediaarea.net/en/MediaInfo/Download).
1. 选择并下载GUI版本的安装程序，然后按照安装说明操作。
1. 安装后，右键单击视频文件(仅限Windows®)并选择MediaInfo，或打开MediaInfo并将视频文件拖到应用程序中。 您可以看到与视频文件关联的所有元数据，包括其宽度、高度和FPS。

### 宽高比 {#aspect-ratio}

当您选择或创建主源视频文件的视频编码预设时，请确保预设具有与主源视频文件相同的纵横比。 宽高比是视频的宽高比。

要确定视频文件的纵横比，请获取文件的元数据并记下文件的宽度和高度（请参阅上面获取文件的元数据）。 然后使用此公式确定纵横比：

宽度/高度=纵横比

下表描述了公式结果如何转换为常见的宽高比选项：

| 公式结果 | 宽高比 |
|--- |--- |
| 1.33 | 4:3 |
| 0.75 | 3:4 |
| 1.78 | 16:9 |
| 0.56 | 9:16 |

例如，1440宽度x 1080高度的视频的长宽比为1440/1080，即1.33。在这种情况下，您可以选择具有4:3纵横比的视频编码预设来编码视频文件。

### 比特率 {#bitrate}

Bitrate是经过编码以构成视频播放一秒的数据量。 比特率以千位/秒(Kbps)为测量单位。

>[!NOTE]
>
>由于所有的编解码器都使用有损压缩，因此比特率是决定视频质量的最重要因素。 有损压缩时，越是压缩视频文件，质量就越低。 因此，所有其他特性（分辨率、帧速率和编解码器）相等，比特率越低，压缩文件的质量就越低。

在选择比特率编码时，可以选择以下两种类型：

* **[!UICONTROL 恒定比特率编码]** (CBR) — 在CBR编码期间，比特率或每秒比特数在整个编码过程中保持不变。 CBR编码会在整个视频中将设置的数据速率保留到您的设置中。 此外，CBR编码不会优化媒体文件的质量，但会节省存储空间。
如果您的视频在整个视频中包含类似的运动级别，请使用CBR。 CBR最常用于流视频内容。 另请参阅 [使用添加自定义的视频编码参数](/help/assets/dynamic-media/video-profiles.md#using-custom-added-video-encoding-parameters).

* **[!UICONTROL 可变比特率编码]** (VBR) - VBR编码根据压缩程序所需的数据来向下调整数据速率，并将其调整到您设置的上限。 此功能意味着在VBR编码过程中，媒体文件的比特率会根据媒体文件的比特率需求动态增加或减少。
VBR的编码时间较长，但产生的结果最理想；媒体文件的质量也更好。 VBR最常用于http渐进式视频内容交付。

您何时使用VBR还是CRB？
在选择VBR与CBR时，几乎总是建议您将VBR用于媒体文件。 VBR以具有竞争力的比特率提供更高质量的文件。 使用VBR时，请确保使用两遍编码，并将最大比特率设置为目标视频比特率的1.5倍。

选择视频编码预设时，请确保将目标最终用户的连接速度考虑在内。 选择数据速率为该速度80%的预设。 例如，如果目标最终用户的连接速度为1000 Kbps，则最佳预设为视频数据速率为800 Kbps的预设。

此表描述了典型连接速度的数据速率。

| 速度(Kbps) | 连接类型 |
|--- |--- |
| 256 | 拨号连接。 |
| 800 | 典型的移动连接。 对于此连接，请将3G体验的数据速率目标定在400到800之间。 |
| 2000 | 典型的宽带台式机连接。 对于这种连接，数据速率目标在800-2000 Kbps范围内，大多数目标平均为1200-1500 Kbps。 |
| 5000 | 典型的高宽带连接。 不建议在此上限范围内进行编码，因为大多数消费者无法使用此速度的视频交付。 |

### 解决方法 {#resolution}

**分辨率** 描述视频文件的高度和宽度（以像素为单位）。 大多数源视频以高分辨率存储（例如，1920 x 1080）。 出于流传输目的，源视频被压缩成较小的分辨率（640 x 480或更小）。

分辨率和数据速率是决定视频质量的两个相互关联的因素。 要保持相同的视频质量，视频文件中的像素数越高（分辨率越高），数据速率必须越高。 例如，假定每帧的像素数在320 x 240分辨率和640 x 480分辨率视频文件中：

| 解决方法 | 每帧的像素 |
|--- |--- |
| 320 x 240 | 76,800 |
| 640 x 480 | 307,200 |

640 x 480文件的每帧像素数是前者的四倍。 要使这两个示例分辨率达到相同的数据速率，可以对640 x 480文件应用四倍的压缩，这会降低视频质量。 因此，250 Kbps的视频数据速率可在320 x 240分辨率下产生高质量观看，但不会在640 x 480分辨率下产生高质量观看。

通常，使用的数据速率越高，视频的显示效果越好，使用的分辨率越高，必须保持查看质量的数据速率越高（与分辨率较低相比）。

由于分辨率和数据速率是相互关联的，因此在编码视频时，您有两个选项：

* 选择一个数据速率，然后以最高分辨率进行编码，该分辨率在您选择的数据速率下显示良好。
* 选择分辨率，然后按照您选择的分辨率进行编码，以获得高质量视频。

当为主源视频文件选择（或创建）视频编码预设时，请使用此表定位正确的分辨率：

| 解决方法 | 高度(像素) | 屏幕大小 |
|--- |--- |--- |
| 240p | 240 | 小屏幕 |
| 300p | 300 | 通常用于移动设备的小屏幕 |
| 360p | 360 | 小屏幕 |
| 480p | 480 | 中屏 |
| 720p | 720 | 大屏幕 |
| 1080p | 1080 | 高清大屏幕 |

### Fps（每秒帧数） {#fps-frames-per-second}

在美国和日本，大多数视频的拍摄速度是每秒29.97帧(fps)；在欧洲，大多数视频的拍摄速度是25帧/秒。 电影的拍摄速度是24帧/秒。

选择与主源视频文件的fps速率匹配的视频编码预设。 例如，如果主源视频为25 fps，请选择一个编码预设为25 fps。 默认情况下，所有自定义编码都使用主源视频文件的fps。 因此，在创建视频编码预设时，无需明确指定fps设置。

### 视频编码维度 {#video-encoding-dimensions}

要获得最佳结果，请选择编码维度，以便源视频是所有已编码视频的整数倍。

要计算此比率，请将源宽度除以编码宽度以获得宽度比率。 然后，将源高度除以编码的高度以获得高度比。

如果生成的比例是整数，则意味着视频得到最佳缩放。 如果生成的比例不是整数，则会通过在显示器上留下多余的像素伪像来影响视频质量。 当视频包含文本时，这种效果最为明显。

例如，假设源视频为1920 x 1080。 在下表中，三个经过编码的视频提供了要使用的最佳编码设置。

| 视频类型 | 宽度x高度 | 宽度比例 | 高度比 |
|--- |--- |--- |--- |
| 源 | 1920x1080 | 1 | 1 |
| 已编码 | 960 x 540 | 2 | 2 |
| 已编码 | 640 x 360 | 3 | 3 |
| 已编码 | 480 x 270 | 4 | 4 |

### 编码的视频文件格式 {#encoded-video-file-format}

Dynamic Media建议使用MP4 H.264视频编码预设。 由于MP4文件使用H.264视频编解码器，因此它以压缩文件大小提供高品质视频。

### 在您的帐户上启用DASH {#enable-dash}

DASH(Digital Adaptive Streaming over HTTP)是视频流的国际标准，被广泛用于各种视频观看者。 在您的帐户上启用DASH后，您可以选择使用DASH或HLS进行自适应视频流。 或者，您可以在以下情况下通过自动在播放器之间切换来选择两者 **[!UICONTROL 自动]** 在查看器预设中选择作为播放类型。

在您的帐户上启用DASH的一些主要优势包括：

* 打包用于自适应比特率流的DASH流视频。 这种方法可以提高投放效率。 自适应流媒体可确保为客户提供最佳观看体验。
* 使用Dynamic Media播放器优化浏览器流会在HLS和DASH流之间切换，以确保最佳服务质量。 使用Safari浏览器时，视频播放器会自动切换到HLS。
* 您可以通过编辑视频查看器预设来配置首选的流方法（HLS或DASH）。
* 优化的视频编码确保在启用DASH功能时不会使用额外的存储。 为HLS和DASH创建一组视频编码，以优化视频存储成本。
* 帮助让您的客户更容易访问视频交付。
* 也通过API获取流URL。

您启动了一个使用DASH的请求；在您的帐户上不会自动启用它。

要在您的帐户上启用DASH，请按照以下所述创建客户支持案例。 在您的支持案例中，指定要在您的Dynamic Media帐户和Experience Manager上启用DASH。

**要在您的帐户上启用DASH，请执行以下操作：**

1. [使用Admin Console开始创建新的支持案例](https://helpx.adobe.com/cn/enterprise/using/support-for-experience-cloud.html).
1. 要创建支持案例，请按照说明操作，同时确保提供以下信息：

   * 主要联系人姓名、电子邮件、电话。
   * 您的Dynamic Media帐户的名称。
   * 指定您希望在Dynamic Media帐户和Experience Manager上启用DASH。

1. Adobe客户支持根据提交请求的顺序将您添加到DASH客户等待列表。
1. 当Adobe准备好处理您的请求时，客户支持将联系您以协调并设置启用DASH的目标日期。
1. 客户支持团队会在完成后通知您。
1. 创建您的 [视频查看器预设](/help/assets/dynamic-media/managing-viewer-presets.md#creating-a-new-viewer-preset) 和往常一样。

## 查看视频报表 {#viewing-video-reports}

>[!NOTE]
>
>视频报表仅在运行Dynamic Media — 混合模式时可用。

视频报表会显示指定时段内的多个聚合量度，以帮助您监控 *已发布* 单个和聚合视频正在按预期执行。 系统会汇总您整个网站中所有已发布视频的以下热门量度数据：

* 视频开始
* 完成率
* 视频平均逗留时间
* 视频花费的总时间
* 每次访问的视频数

全部的表 *已发布* 此外，还列出了视频，以便您可以根据视频总开始次数来跟踪网站上最常查看的视频。

在列表中选择视频名称时，会以折线图的形式显示视频的受众维系（流失）报表。 该图表显示在视频播放期间任何给定时间的查看次数。 在播放视频时，垂直条与播放器中的时间指示器同步跟踪。 折线图数据中的下降指示受众从无兴趣到何时消失。

如果视频是在Adobe Experience Manager Dynamic Media之外进行编码，则受众维系（流失）图表和表中的播放百分比数据将不可用。

>[!NOTE]
>
>跟踪和报告数据完全基于Dynamic Media自己的视频播放器及相关视频播放器预设的使用。 因此，您无法跟踪和报告通过其他视频播放器播放的视频。

默认情况下，首次输入视频报表时，该报表显示从当前月份的第一天开始到当前月份的日期结束的视频数据。 但是，您可以通过指定自己的日期范围来覆盖默认日期范围。 下次输入视频报表时，将使用指定的日期范围。

为了使视频报表正常工作，会在配置Dynamic MediaCloud Services时自动创建报表包ID。 同时，报表包ID会推送到发布服务器，以便在您预览资产时可用于复制URL功能。 但是，此功能要求已设置发布服务器。 如果未设置发布服务器，您仍可以发布以查看视频报表。 但是，您必须返回到Dynamic Media云配置并选择 **[!UICONTROL 确定]**.

**要查看视频报表，请执行以下操作：**

1. 在Experience Manager的左上角，选择Experience Manager徽标，然后在左边栏中导航到 **[!UICONTROL 工具]** （锤子图标）> **[!UICONTROL 资产]** > **[!UICONTROL 视频报表]**.
1. 在“视频报表”页面上，执行以下操作之一：

   * 在右上角附近，选择 **[!UICONTROL 刷新视频报告]** 图标。
仅当报表的结束日期为当天时，才使用刷新。 此功能可确保您查看自上次运行报表以来发生的视频跟踪。

   * 在右上角附近，选择 **[!UICONTROL 日期选取器]** 图标。
指定要获取其视频数据的开始和结束日期范围，然后选择 **[!UICONTROL 运行报告]**.

   “排名最前的量度”组框标识所有量度的各种聚合量度 *已发布* 您网站上的视频。

1. 在列出最热门发布的视频的表中，选择要播放视频的视频名称，并查看视频的受众维系（流失）报表。

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

## 向视频添加隐藏式字幕或字幕 {#adding-captions-to-video}

通过将隐藏式字幕添加到单个视频或自适应视频集，您可以将视频扩展到全球市场。 通过添加隐藏式字幕，您无需对音频进行混音，也无需使用母语人士重新录制每种语言的音频。 视频以所录制的语言播放。 出现外语字幕是为了让不同语言的人仍然能够理解音频部分。

隐藏式字幕还为耳聋或听力缺佳的用户提供了更好的辅助功能。

>[!NOTE]
>
>您使用的视频播放器必须支持隐藏式字幕的显示。

另请参阅 [Dynamic Media中的辅助功能](/help/assets/dynamic-media/accessibility-dm.md).

Dynamic Media可以将字幕文件转换为JSON（JavaScript对象表示法）格式。 此转换意味着，您可以将JSON文本作为隐藏但完整的视频转录内容嵌入到网页中。 然后，搜索引擎可以对内容进行爬网/索引，以使视频更容易被发现，并为客户提供有关视频内容的更多详细信息。

参见 [提供静态（非图像）内容](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/c-serving-static-nonimage-contents.html#image-serving-api) 有关在URL中使用JSON函数的更多信息。

**要在视频中添加字幕或字幕，请执行以下操作：**

1. 使用第三方应用程序或服务创建视频字幕/字幕文件。

   确保您创建的文件遵循WebVTT（Web视频文本跟踪）标准。 字幕文件扩展名为.VTT。 您可以了解有关WebVTT字幕标准的更多信息。

   参见 [WebVTT： Web视频字幕格式](https://w3c.github.io/webvtt/).

   在Dynamic Media之外，您可以使用免费和高级的工具和服务来创作题注/字幕文件。 例如，要创建不带样式的简单视频字幕文件，您可以使用以下免费的在线字幕创作和编辑工具：

   [WebVTT题注生成器](https://testdrive-archive.azurewebsites.net/Graphics/CaptionMaker/Default.html)

   为了获得最佳结果，请在Internet Explorer 9或更高版本、Google Chrome或Safari中使用该工具。

   在工具中， **[!UICONTROL 输入视频文件的URL]** 字段，粘贴复制的视频文件URL，然后选择 **[!UICONTROL 加载]**. 参见 [获取资产的URL](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset) 以获取视频文件本身的URL，然后您可以将其粘贴到 **[!UICONTROL 输入视频文件的URL字段]**. 随后，Internet Explorer、Chrome 或 Safari 可以本机播放视频。

   现在，按照站点中的屏幕说明创作并保存WebVTT文件。 完成后，复制字幕文件内容并将其粘贴到纯文本编辑器中，并以VTT文件扩展名保存。

   >[!NOTE]
   >
   >为了在全球范围内支持多种语言的视频字幕，WebVTT标准要求您创建单独的.vtt文件，并为要支持的每种语言调用。

   通常，您希望将字幕VTT文件的名称与视频文件相同，然后附加语言区域设置，如 — EN、-FR或 — DE。 这样，它可以帮助您使用现有Web内容管理系统自动生成视频URL。

1. 在Experience Manager中，将您的WebVTT字幕文件上传到DAM。
1. 导航到 *已发布* 要与上传的字幕文件关联的视频资源。

   请注意，只有在首次&#x200B;*发布*&#x200B;资产&#x200B;*后*，才可复制 URL。

   参见 [发布资产](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

1. 执行下列操作之一：

   * 要获得弹出式视频查看器体验，请选择 **[!UICONTROL URL]**. 在URL对话框中，选择URL并将其复制到剪贴板，然后将URL粘贴到简单的文本编辑器中。 使用以下语法附加复制的视频URL：

      `&caption=<server_path>/is/content/<path_to_caption.vtt_file,1>`

      请注意 `,1` 标题路径末尾。 紧跟路径中的VTT文件扩展名之后，您可以选择启用（打开）或禁用（关闭）视频播放器栏上的隐藏式字幕按钮，方法是设置为 `,1` 或 `,0`，则不会显示任何内容。

   * 要获得嵌入式视频查看器体验，请选择 **[!UICONTROL 嵌入代码]**. 在“嵌入代码”对话框中，选择，然后将嵌入代码复制到剪贴板，然后将该代码粘贴到简单的文本编辑器中。 使用以下语法附加复制的嵌入代码：

      `videoViewer.setParam("caption","<path_to_caption.vtt_file,1>");`

      请注意 `,1` 标题路径末尾。 紧跟路径中的VTT文件扩展名之后，您可以选择启用（打开）或禁用（关闭）视频播放器栏上的隐藏式字幕按钮，方法是设置为 `,1` 或 `,0`，则不会显示任何内容。

## 向视频添加章节标记 {#adding-chapter-markers-to-video}

您可以通过将章节标记添加到单个视频或自适应视频集，使长格式视频更容易观看和导航。 当用户播放视频时，他们可以在视频时间轴上选择章节标记（也称为视频清理器）。 他们可以轻松导航到目标点，或立即跳转到新内容、培训和演示。

>[!NOTE]
>
>使用的视频播放器必须支持使用章节标记。 Dynamic Media视频播放器支持章节标记，但使用第三方视频播放器可能不支持。

<!-- OBSOLETE CONTENT OBSOLETE CONTENT If desired, you can create and brand your own custom video viewer with chapters instead of using a video viewer preset. For instructions on creating your own HTML5 viewer with chapter navigation, in the Adobe Scene7 Viewer SDK for HTML5 guide, reference the heading "Customizing Behavior Using Modifiers" under the classes `s7sdk.video.VideoPlayer` and `s7sdk.video.VideoScrubber`. The Adobe Scene7 Viewer SDK is available as a download from [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html). -->

您可以像创建字幕一样为视频创建章节列表。 即，创建一个WebVTT文件。 但请注意，此文件必须与任何WebVTT描述文件分开。 不能将字幕和章节合并到一个WebVTT文件中。

您可以使用以下示例作为使用章节导航创建WebVTT文件时所使用的格式示例：

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

在上面的示例中， `Chapter 1` 是提示标识符，并且是可选的。 的提示时间 `00:00:000 --> 01:04:364` 指定章节的开始时间和结束时间，单位为 `00:00:000` 格式。 最后三位数是毫秒，可保留为 `000`（如果首选）。 的章节标题 `The bicycle store behind it all` 是章节内容的实际描述。 当用户将鼠标指针悬停在时间轴中的可视提示点上时，提示标识符、开始提示时间和章节标题都会显示在视频播放器的弹出窗口中。

由于您使用的是HTML5视频查看器，因此请确保您创建的章节文件遵循WebVTT（Web视频文本跟踪）标准。 章节文件扩展名为.VTT。 您可以了解有关WebVTT字幕标准的更多信息。

参见 [WebVTT： Web视频字幕格式](https://w3c.github.io/webvtt/).

**要向视频添加章节标记，请执行以下操作：**

1. 将VTT文件保存为UTF8编码，以避免在章节标题文本中出现字符演绎版问题。

   通常，您希望将章节VTT文件的名称与视频文件相同，并附加章节。 这样，它可以帮助您使用现有Web内容管理系统自动生成视频URL。
1. 在Experience Manager中，上传WebVTT章节文件。

   参见 [上传资产](/help/assets/manage-digital-assets.md#uploading-assets).

1. 执行下列操作之一：

   <table>
     <tbody>
      <tr>
       <td>用于弹出视频查看器体验</td>
       <td>
       <ol>
       <li>导航到 <i>已发布 </i>要与上载的章节文件关联的视频资产。 请注意，只有在首次<i>发布</i>资产<i>后</i>，才可复制 URL。参见 <a href="/help/assets/dynamic-media/publishing-dynamicmedia-assets.md">正在发布资产。</a></li>
       <li>从下拉菜单中，选择 <strong>查看器</strong>.</li>
       <li>在左边栏中，选择视频查看器预设名称。 视频预览在单独的页面中打开。</li>
       <li>在左边栏的底部，选择 <strong>URL</strong>.</li>
       <li>在URL对话框中，选择URL并将其复制到剪贴板，然后将URL粘贴到简单的文本编辑器中。</li>
       <li>使用以下语法附加复制的视频的URL，以便将其与复制的URL关联到章节文件：<br /> <br /> <code>&navigation=<<i>full_copied_URL_path_to_chapter_file</i>.vtt></code><br /> </li>
       </ol> </td>
      </tr>
      <tr>
       <td>用于嵌入式视频查看器体验<br /> </td>
       <td>
       <ol>
       <li>导航到 <i>已发布 </i>要与上载的章节文件关联的视频资产。 请注意，只有在首次<i>发布</i>资产<i>后</i>，才可复制 URL。参见 <a href="/help/assets/dynamic-media/publishing-dynamicmedia-assets.md">正在发布资产。</a></li>
       <li>从下拉菜单中，选择 <strong>查看器</strong>.</li>
       <li>在左边栏中，选择视频查看器预设名称。 视频预览在单独的页面中打开。</li>
       <li>在左边栏的底部，选择 <strong>嵌入</strong>.</li>
       <li>在“嵌入代码”对话框中，选择并将整个代码复制到剪贴板，然后将其粘贴到简单的文本编辑器中。</li>
       <li>使用以下语法附加视频的嵌入代码，以便将其与复制的URL关联到章节文件：<br /> <br /> <code>videoViewer.setParam("navigation","&lt;<i>full_copied_URL_path_to_chapter_file</i>.vtt>"</code></li>
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

## 更改Dynamic Media资源的Dynamic Media URL

在Dynamic Media中处理的视频可以通过现成的查看器使用，也可以直接访问清单URL并通过您自己的自定义查看器播放它们。 以下是获取视频清单URL的API。

### 关于getVideoManifestURI API

此 `getVideoManifestURI`API通过c公开`q-scene7-api:com.day.cq.dam.scene7.api` 和可用于生成以下清单URL：

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
| `manifestType` | 可以是 `ManifestType.DASH` 或 `ManifestType.HLS` |
| `onlyIfPublished` | 如果清单URI仅在投放层上发布且可用时生成，则设置为true。 |

要使用上述方法获取视频的清单URL，请添加 [视频编码配置文件](/help/assets/dynamic-media/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming) 到“上传视频”文件夹。 Dynamic Media会根据在分配给文件夹的视频编码文件中找到的编码来处理这些视频。 现在，您可以调用上述API以获取已上传视频的清单URL。

### 错误方案

如果出现错误，则API返回null。 异常记录在Experience Manager错误日志中。 所有此类记录错误都开始于 `Could not generate Video Manifest URI`. 以下情况可能会导致出现此类错误：

* An `IllegalArgumentException` 因以下任一情况被记录：

   * 此 `resource` 传递的参数为null。
   * 此 `resource` 传递的参数不是视频。
   * 此 `manifestType` 传递的参数为null。
   * 此 `onlyIfPublished` 参数作为true传递，但视频未发布。
   * 未使用Dynamic Media中的自适应视频集摄取视频。

* `IOException` 在连接到Dynamic Media时出现问题时记录。
* `UnsupportedOperationException` 在以下情况下被记录： `manifestType` 传递的参数为 `ManifestType.DASH`，而视频尚未使用DASH格式进行处理。

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





