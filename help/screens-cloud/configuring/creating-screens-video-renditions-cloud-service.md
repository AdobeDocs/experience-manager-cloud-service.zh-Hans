---
title: 在屏幕中创建屏幕视频演绎版作为Cloud Service
description: 本页介绍如何在Screens中创建Screens视频演绎版作为Cloud Service。
source-git-commit: b8691bb77079eeb7efd141ce89c44c5a312262b3
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 0%

---


# 在屏幕中创建屏幕视频演绎版作为Cloud Service {#creating-screens-video-renditions}

## 简介 {#introduction}

本指南将介绍如何创建在Screens播放器中使用的视频演绎版。

>[!IMPORTANT]
>如果您计划在Screens渠道中使用视频，则必须配置此部分中突出显示的步骤。

## 在Screens中创建Screens视频演绎版作为Cloud Service的步骤 {#steps-creating-screens-video-renditions}

1. 导航到Screens云UI中的渠道。
1. 单击左上角的Adobe Experience Manager ，导航到“屏幕内容提供程序”，即AEM as a ScreensCloud Service。
1. 现在，单击主导航中的工具部分，单击“资产”，然后单击“处理配置文件”

1. 单击“创建”以创建新的处理用户档案
1. 提供“ScreensProcessingProfile”之类的名称
1. 导航到视频选项卡以添加视频编码，然后单击“新增”


   >[!IMPORTANT]
   >请确保使用以“screens — ”开头的编码名称，在Screens As a Seens中，将只考虑使用这些视频演绎版来播放视频体验。 输入适合您的视频的比特率（720px视频为2500 kbps，1080px为5000 kbps）

   >[!NOTE]
   >可以根据您的需求，以不同的宽度/高度/比特率添加多个视频演绎版，但请记住，所有屏幕演绎版都将由Screens设备下载，即使设备仅播放视频演绎版。

1. 单击Save

1. 选择处理配置文件，然后单击“将配置文件应用到文件夹”

1. 选择保留Screens视频的文件夹，然后单击应用

1. 您可以创建多个处理配置文件，并将它们应用到相应的文件夹，以便这些文件夹中的视频获得特定的视频演绎版

1. 当您将任何视频上传到应用了处理配置文件的文件夹后，将会处理视频，并创建配置的演绎版，Screens设备将使用这些演绎版来播放视频。

