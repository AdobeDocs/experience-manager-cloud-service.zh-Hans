---
title: 管理视频资产
description: 在 [!DNL Adobe Experience Manager].
contentOwner: AG
feature: Asset Management,Publishing,Collaboration,Video
role: User
exl-id: 91edce4a-dfa0-4eca-aba7-d41ac907b81e
source-git-commit: 038dbc4b0febfa58f69e05f837760162210f8689
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 9%

---

# 管理视频资产 {#manage-video-assets}

视频格式是组织中数字资产的关键部分。 [!DNL Adobe Experience Manager] 提供了成熟的产品和功能，用于在视频资产创建后管理其整个生命周期。

了解如何在 [!DNL Adobe Experience Manager Assets]. 使用处理配置文件和使用 [!DNL Dynamic Media] 集成。 没有 [!DNL Dynamic Media] 许可证， [!DNL Experience Manager] 为视频提供基本支持，例如使用FFmpeg转码、提取支持的文件格式的预览缩略图，以及在用户界面中预览直接支持在浏览器中播放的格式。

## 上传和预览视频资产 {#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] 为扩展名为MP4的视频资产生成预览。 您可以在 [!DNL Assets] 用户界面。

1. 在数字资产文件夹或子文件夹中，导航到要添加数字资产的位置。
1. 要上传资产，请单击 **[!UICONTROL 创建]** 从工具栏中选择 **[!UICONTROL 文件]**. 或者，在用户界面上拖动文件。 请参阅 [上传资产](manage-digital-assets.md#uploading-assets) 以了解详细信息。
1. 要在卡片视图中预览视频，请单击 **[!UICONTROL 播放]** ![播放选项](assets/do-not-localize/play.png) 选项。 您只能在卡片视图中暂停或播放视频。 的 [!UICONTROL 播放] 和 [!UICONTROL 暂停] 选项在列表视图中不可用。
1. 要在资产详细信息页面中预览视频，请选择 **[!UICONTROL 编辑]** 在卡上。 视频会在浏览器自带的视频播放器中播放。您可以播放视频，暂停视频，控制视频音量，以及将视频放大到全屏。

## 发布视频资产 {#publish-video-assets}

发布后，您可以将视频资产作为URL包含在网页中，或直接嵌入资产。 有关详细信息，请参阅 [发布 [!DNL Dynamic Media] 资产](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

## 使用处理配置文件进行转码 {#transcode-video}

[!DNL Experience Manager] as a [!DNL Cloud Service] 允许您使用处理配置文件对MP4视频文件进行基本转码。 利用功能，不仅可上传，还可预览和缩放MP4视频文件。

![在中为视频转码创建处理配置文件 [!DNL Experience Manager]](assets/video-processing-profile-for-mp4.png)

*图：用于在中进行视频转码的处理用户档案 [!DNL Experience Manager].*

如果您仅提供宽度或仅提供高度，并将另一个字段留空，则演绎版将保持宽高比。 H.264视频编解码器可用于转码。

要使用处理配置文件处理资产，请将配置文件添加到文件夹。 请参阅 [使用处理配置文件处理资产](/help/assets/asset-microservices-configure-and-use.md#use-profiles).

## 在视频资产中添加批注 {#annotate-video-assets}

您可以向视频资产添加注释。 在对视频添加注释时，播放器会暂停，以允许您对帧添加注释。 有关详细信息，请参阅 [管理视频资产](manage-video-assets.md).

>[!NOTE]
>
>视频资产批注尚不支持MXF视频格式。

1. 从 [!DNL Assets] 控制台，选择 **[!UICONTROL 编辑]** ，以显示资产详细信息页面。
1. 要播放视频，请单击 **[!UICONTROL 预览]**.
1. 要在视频中添加批注，请单击 **[!UICONTROL 注释]**. 注释会在视频中的特定时间（帧）添加。 在添加注释时，您可以在画布上绘制图形，并在绘图中包含注释。 注释会自动保存。 要退出注释向导，请单击 **[!UICONTROL 关闭]**.
1. 搜索到视频中的特定点，在&#x200B;**文本**&#x200B;字段中指定时间（以秒为单位），然后单击&#x200B;**跳转**。例如，要跳过视频的前 20 秒，请在文本字段中输入 20。
1. 要在时间轴中查看它，请单击注释。 要从时间轴中删除注释，请单击 **[!UICONTROL 删除]**.

## 最佳实践和限制 {#tips-limitations}

* 没有 [!DNL Dynamic Media] 许可证，则只能使用处理配置文件处理MP4文件。
* 使用处理配置文件转码MP4文件时，需遵循以下准则和限制：

   * Apple ProRes文件只能将代码转换为最大分辨率1080p。
   * 如果源文件的比特率大于200 Mbps，则只能将代码转换到最大分辨率1080p。
   * 如果源帧长>=60 fps，则可使用的源文件的最大大小为：

      * 400 MB用于4k转码。
      * 800 MB用于1080p转码。
      * 8 GB，用于720p转码。
   * 最大文件大小可转码为4k分辨率，为2.55 GB MP4文件，分辨率为4k、12 Mbps比特率和23 fps。


>[!MORELIKETHIS]
>
>* [Dynamic Media视频文档](/help/assets/dynamic-media/video.md).
>* [详细了解处理配置文件的使用、类型和配置](/help/assets/asset-microservices-configure-and-use.md).

