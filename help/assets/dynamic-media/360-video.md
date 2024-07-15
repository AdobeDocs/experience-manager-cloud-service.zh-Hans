---
title: 360/VR视频
description: 了解如何在Dynamic Media中使用360和虚拟现实(VR)视频。
contentOwner: Rick Brough
feature: 360 VR Video
role: User
exl-id: ffd092d3-2188-47b0-a475-8bfa660c03c1
source-git-commit: 8ed477ec0c54bb0913562b9581e699c0bdc973ec
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 0%

---

# 360/VR视频 {#vr-video}

360°视频同时记录每个方向的视图。 它们使用全方位相机或一系列相机来拍摄。 在播放期间，在平面显示器上，用户可控制视角；在移动设备上播放通常应用其内置的陀螺仪控制。

Dynamic Media包含对360个视频资源交付的本机支持。 默认情况下，查看或播放无需其他配置。 您可以使用标准视频扩展名(如.mp4、.mkv和.mov)来交付360视频。 最常见的编解码器是H.264。

您可以使用360/VR视频查看器渲染等矩形视频。 结果是对房间、财产、位置、景观、医疗程序等的沉浸式观看体验。

当前不支持空间音频；如果音频混入立体声，则平衡(L/R)不会随着客户改变相机视角而改变。

请参阅[在AEM Assets中使用Dynamic Media 360视频和自定义视频缩略图](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-360-video-custom-thumbnail-feature-video-use.html#dynamic-media)。

另请参阅[管理查看器预设](/help/assets/dynamic-media/managing-viewer-presets.md)。

## 360视频的实际效果 {#video-in-action}

选择[空间站360](https://s7d1.scene7.com/s7viewers/html5/Video360Viewer.html?asset=Viewers/space_station_360-AVS)打开浏览器窗口并观看360°视频。 在视频播放过程中，将指针拖动到新位置以更改视角。

来自空间站360视频的![视频帧](assets/6_5_360videoiss_simplified.png)
来自空间站360*的*&#x200B;视频帧

## 360/VR视频和Adobe Premiere Pro {#vr-video-and-adobe-premiere-pro}

您可以使用AdobePremier Pro查看和编辑360/VR素材。 例如，您可以在场景中正确放置徽标和文本，并应用专门为等矩形介质设计的效果和过渡。

查看[编辑360/VR视频](https://helpx.adobe.com/premiere-pro/how-to/edit-360-vr-video.html)。

## 上传资产以用于360视频查看器 {#uploading-assets-for-use-with-the-video-viewer}

上传到[!DNL Experience Manager]的360个视频资源在资源页面上标记为&#x200B;**多媒体**，与普通视频资源类似。

![在卡片视图中看到的已上传360视频资产](assets/6_5_360video-selecttopreview.png)
*在卡片视图中看到的已上传360视频资产。 该资产标记为多媒体。*

**上传资源以用于360视频查看器：**

1. 创建了一个专用于您的360视频资产的文件夹。
1. [将自适应视频配置文件应用到文件夹](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders)。

   与标准的非360视频内容相比，渲染360视频内容对源视频分辨率和编码呈现版本分辨率提出了更高的要求。

   您可以使用随Dynamic Media提供的现成自适应视频配置文件。 但是，对于使用非360视频查看器渲染的相同设置进行编码的非360视频，它导致360视频质量明显降低。 因此，如果需要高品质360视频，请执行以下操作：

   * 理想情况下，您的原始的360视频内容具有以下分辨率之一：

      * 1080p - 1920 x 1080，称为全高清或全高清分辨率，或
      * 2160p - 3840 x 2160，称为4k、UHD或Ultra高清分辨率。 这种大屏幕分辨率通常出现在高端电视机和计算机显示器上。 2160p分辨率通常称为“4k”，因为宽度接近4000像素。 换句话说，它提供的像素是1080p的四倍。

   * [创建具有更高演绎版的自定义自适应视频配置文件](/help/assets/dynamic-media/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming)。 例如，您可以创建包含以下三个设置的自适应视频配置文件：

      * 宽度=自动；高度=720；比特率=2500 kbps
      * 宽度=自动；高度=1080；比特率=5000 kbps
      * 宽度=自动；高度=1440；比特率=6600 kbps

   * 在专门用于360个视频资产的文件夹中处理360个视频内容。

   这种方法给用户的网络和CPU提出了更高的要求。

1. [将视频上传到文件夹](/help/assets/manage-video-assets.md#upload-and-preview-video-assets)。

<!--

## Overriding the default aspect ratio of 360 videos  {#overriding-the-default-aspect-ratio-of-videos}

For an uploaded asset to qualify as a 360 video that you intend to use with the 360 Video viewer, the asset must have an aspect ratio of 2.

By default, AEM detects video as "360" if its aspect ratio (width/height) is 2.0. If you are an Administrator, you can override the default aspect ratio setting of 2 by setting the optional `s7video360AR` property in CRXDE Lite at the following:

* `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

  * **Property type**: Double
  * **Value**: floating-point aspect ratio, default 2.0.

After you set this property, it takes effect immediately on both existing videos and newly uploaded videos.

The aspect ratio applies to 360 video assets for the asset details page and the [Video 360 Media WCM component](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#dynamic-media-components).

Start by uploading 360 Videos.

-->

## 预览360视频 {#previewing-video}

您可以使用预览功能查看向客户显示的360视频效果，并确保其行为符合预期。

另请参阅[编辑查看器预设](/help/assets/dynamic-media/managing-viewer-presets.md#editing-viewer-presets)。

如果对360视频满意，则可发布该视频。

请参阅[在网页上嵌入视频查看器或图像查看器](/help/assets/dynamic-media/embed-code.md)。
请参阅[将URL链接到您的Web应用程序](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)。 如果您的交互式内容具有带有相对URL的链接，尤其是指向[!DNL Experience Manager Sites]页面的链接，则无法基于URL的链接方法。
请参阅[将Dynamic Media Assets添加到页面](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)。

**预览360个视频：**

1. 在&#x200B;**[!UICONTROL Assets]**&#x200B;中，导航到您创建的现有360视频。 要在预览模式下将其打开，请选择360视频资产。

   ![在Experience Manager的卡片视图中看到的已上传360视频资源的屏幕截图。](assets/6_5_360video-selecttopreview-1.png)

   要预览视频，请选择包含360个视频的资产。

1. 在预览页面左上角附近，选择下拉列表，然后选择&#x200B;**[!UICONTROL 查看器]**。

   ![选择查看器以查看可用视频查看器列表的屏幕截图。](assets/6_5_360video-preview-viewers.png)

   从“查看器”列表中，选择&#x200B;**[!UICONTROL Video360_social]**，然后执行以下操作之一：

   * 要改变静态场景的视角，请将指针拖动到视频上。
   * 要开始播放，请选择视频的&#x200B;**[!UICONTROL 播放]**&#x200B;按钮。 在播放视频时，拖动指针以改变视频视角。

   ![用户选择Video360_Social查看器预览360度视频的屏幕截图。](assets/6_5_360video-preview-video360-social.png)*360视频截图。*

   * 从查看器列表中，选择&#x200B;**[!UICONTROL Video360VR]**。

     虚拟现实(VR)视频是使用虚拟现实头戴式耳机访问的沉浸式视频内容。 与普通视频一样，使用360°摄像机录制或捕获视频时，您首先会创建VR视频。

   ![将鼠标指针悬停在Video360VR Viewer选项上的用户屏幕截图。](assets/6_5_360video-preview-video360vr.png)
   *一个360 VR视频截图。*

1. 在预览页面的右上角附近，选择&#x200B;**[!UICONTROL 关闭]**。

## 发布360视频 {#publishing-video}

要使用360视频，您必须发布它。 发布360视频将激活URL和嵌入代码。 它还将360视频发布到Dynamic Media云，该云与CDN集成以实现可扩展的高性能交付。

有关如何发布360视频的详细信息，请参阅[发布Dynamic Media Assets](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)。
另请参阅[在网页上嵌入视频查看器或图像查看器](/help/assets/dynamic-media/embed-code.md)。
另请参阅[将URL链接到您的Web应用程序](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)。 如果您的交互式内容具有带有相对URL的链接，尤其是指向[!DNL Experience Manager Sites]页面的链接，则无法基于URL的链接方法。
另请参阅[将Dynamic Media Assets添加到页面](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)。
