---
title: 管理视频资产
description: 在 [!DNL Adobe Experience Manager]中上传、预览、批注和发布视频资产。
contentOwner: AG
translation-type: tm+mt
source-git-commit: deab2183447e64e8a98f3072ceab2ef2216c4528
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 10%

---


# 管理视频资产 {#manage-video-assets}

视频格式是组织数字资产的关键部分。 [!DNL Adobe Experience Manager] 优惠可以提供成熟的产品和功能，在视频资产创建后管理其整个生命周期。

了解如何在[!DNL Adobe Experience Manager Assets]中管理和编辑视频资产。 使用处理用户档案和使用[!DNL Dynamic Media]集成，可以进行视频编码和转码（例如FFmpeg转码）。 如果没有[!DNL Dynamic Media]许可证，[!DNL Experience Manager]将为视频提供基本支持，如使用FFmpeg进行转码、提取支持的文件格式的预览缩略图，以及在用户界面中预览支持在浏览器中直接回放的格式。

## 上传和预览视频资产{#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] 为扩展名为MP4的视频资产生成预览。您可以在[!DNL Assets]用户界面中预览再现。

1. 在数字资产文件夹或子文件夹中，导航到要添加数字资产的位置。
1. 要上传资产，请单击工具栏中的&#x200B;**[!UICONTROL 创建]**，然后选择&#x200B;**[!UICONTROL 文件]**。 或者，在用户界面上拖动文件。 有关详细信息，请参阅[上传资产](manage-digital-assets.md#uploading-assets)。
1. 要在卡视图中预览视频，请单击视频资产上的&#x200B;**[!UICONTROL 播放]** ![播放选项](assets/do-not-localize/play.png)选项。 您只能在卡视图中暂停或播放视频。 [!UICONTROL 播放]和[!UICONTROL 暂停]选项在列表视图中不可用。
1. 要预览资产详细信息页面中的视频，请在卡上选择&#x200B;**[!UICONTROL 编辑]**。 视频会在浏览器自带的视频播放器中播放。您可以播放视频，暂停视频，控制视频音量，以及将视频放大到全屏。

## 发布视频资产{#publish-video-assets}

发布后，您可以将视频资产作为URL包含在网页中或直接嵌入资产。 有关详细信息，请参阅[publish [!DNL Dynamic Media] assets](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)。

## 使用处理用户档案{#transcode-video}转码

[!DNL Experience Manager] 这样， [!DNL Cloud Service] 您就可以使用处理用户档案对MP4视频文件进行基本转码。该功能不仅允许您上传，还可以预览和缩放MP4视频文件。

![创建用于在  [!DNL Experience Manager]](assets/video-processing-profile-for-mp4.png)

*图：中用于视频转码的处理用户档案 [!DNL Experience Manager]。*

如果您只提供宽度或仅提供高度，而将其他字段留空，则演绎版将保持宽高比。 H.264视频编解码器可用于转码。

要使用处理用户档案处理资产，请向文件夹添加用户档案。 请参阅[使用处理用户档案处理资产](/help/assets/asset-microservices-configure-and-use.md#use-profiles)。

## 注释视频资产{#annotate-video-assets}

1. 从[!DNL Assets]控制台中，选择资产卡上的&#x200B;**[!UICONTROL 编辑]**&#x200B;以显示资产详细信息页面。
1. 要播放视频，请单击&#x200B;**[!UICONTROL 预览]**。
1. 要对视频添加注释，请单击&#x200B;**[!UICONTROL 注释]**。 注释会在视频中的特定时间（帧）添加。 添加注释时，您可以在画布上绘图，并在绘图中包含注释。 注释将自动保存。 要退出注释向导，请单击&#x200B;**[!UICONTROL 关闭]**。
1. 搜索到视频中的特定点，在&#x200B;**文本**&#x200B;字段中指定时间（以秒为单位），然后单击&#x200B;**跳转**。例如，要跳过视频的前 20 秒，请在文本字段中输入 20。
1. 要在时间轴中视图它，请单击注释。 要从时间轴中删除注释，请单击&#x200B;**[!UICONTROL 删除]**。

## 最佳实践和限制{#tips-limitations}

* 没有[!DNL Dynamic Media]许可证，您只能使用处理用户档案处理MP4文件。
* 使用处理用户档案转码MP4文件时，有以下准则和限制：

   * Apple ProRes文件只能将代码转换为最大分辨率1080p。
   * 如果源文件的比特率大于200 Mbps，则只能将代码转换到最大分辨率1080p。
   * 如果源帧速率>=60 fps，则可以使用的源文件的最大大小为，

      * 400 MB用于4k转码。
      * 1080p转码需要800 MB。
      * 8 GB，用于720p转码。
   * 可转码到4k分辨率的最大文件大小为2.55 GB MP4文件，分辨率为4k、12 Mbps比特率和23 fps。


>[!MORELIKETHIS]
>
>* [Dynamic Media视频文档](/help/assets/dynamic-media/video.md)。
>* [进一步了解处理用户档案的使用、类型和配置](/help/assets/asset-microservices-configure-and-use.md)。

