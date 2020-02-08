---
title: 视频演绎版
description: 视频演绎版
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Video renditions {#video-renditions}

Adobe Experience Manager(AEM)资产可为各种格式（包括OGG、FLV等）的视频资产生成视频演绎版。

AEM 资产支持媒体资产的静态和动态演绎版（DM 编码的演绎版）。

静态演绎版是使用FFMPEG（在系统路径上安装并可用）本机生成的，并存储在内容存储库中。

DM编码的演绎版存储在代理服务器中，并在运行时提供。

AEM资产在客户端为这些演绎版提供播放支持。

要查看特定视频资产的演绎版，请打开其资产页面，然后点按全局导航图标。 然后，从列 **[!UICONTROL 表中选]** 择演绎版。

视频演绎版列表显示在“演绎版” **[!UICONTROL 面板中]** 。

要为DM编码的再现配置代理服务器，请配置Dynamic Media cloud服务。

<!-- To generate video renditions with desired parameters, [create a corresponding video profile](video-profiles.md). -->

配置代理服务器并创建视频配置文件后，您可以将此视频预设包含在处理配置文件中，并将处理配置文件应用到文件夹。

>[!NOTE]
>
>在Internet Explorer 11上，音频播放不适用于OGG和WAV文件。 对于扩展名为OGG或WAV的资产，“源无效”错误显示在资产详细信息页面上。 在MS edge和iPad上，OGG文件不播放并引发“不支持”格式错误。