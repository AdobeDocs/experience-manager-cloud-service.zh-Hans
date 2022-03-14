---
title: 在屏幕中创建视频演绎版as a Cloud Service
description: 本页介绍如何在Screens中创建视频演绎版as a Cloud Service。
exl-id: a9c46036-cd29-47fa-81d9-c865cf22c98a
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---

# 在屏幕中创建视频演绎版as a Cloud Service {#creating-screens-video-renditions}

## 简介 {#introduction}

本节介绍如何创建在Screens播放器中使用的视频演绎版。

>[!IMPORTANT]
>如果您计划在Screens渠道中使用视频，则必须配置此部分中突出显示的步骤。

## 在Screens中创建视频演绎版的步骤as a Cloud Service {#steps-creating-screens-video-renditions}

请按照以下步骤在Screens中创建与Screens内容提供商as a Cloud Service的视频演绎版：

1. 在Screens内容提供商中导航到您的渠道。

   >[!NOTE]
   >请参阅 [使用Screens内容提供程序](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/configure-screens-cloud/using-screens-content-provider.html?lang=en#screens-content-provider) 以了解更多详细信息。

1. 单击左侧导航栏中的“工具”部分，然后单击 **资产** 然后单击 **处理配置文件**.

   ![](/help/screens-cloud/assets/configure/screens-cp-3.png)

1. 单击 **创建** 创建新处理配置文件。

   ![](/help/screens-cloud/assets/configure/screens-video-2.png)

1. 输入 **名称**，例如 **ScreensProcessingProfile**.

   ![](/help/screens-cloud/assets/configure/screens-video-3.png)

1. 导航到 **视频** 选项卡来添加视频编码，然后单击 **新增**.

   ![](/help/screens-cloud/assets/configure/screens-video-4a.png)

1. 输入 **编码名称** 例如， **screens-fullhd** 和 **比特率** as **2500**.

   ![](/help/screens-cloud/assets/configure/screens-video-4.png)

   >[!IMPORTANT]
   >请确保使用以“screens — ”开头的编码名称，只有这些视频演绎版会被视为在Screensas a Cloud Service播放视频体验。 输入可用于您的视频的比特率（720px视频为2500 kbps，1080px为5000 kbps）。

   >[!NOTE]
   >可以添加多个不同宽度/高度/比特率的视频演绎版，以处理您的视频。 请记住，所有屏幕演绎版都将由Screens设备下载，即使设备只播放视频演绎版。

1. 单击 **保存**.

1. 选择处理配置文件并单击 **将配置文件应用到文件夹**.

   ![](/help/screens-cloud/assets/configure/screens-video-5.png)

1. 选择保留Screens视频的文件夹，然后单击 **应用**.

   ![](/help/screens-cloud/assets/configure/screens-video-6.png)

   >[!NOTE]
   >* 您可以创建多个处理配置文件，并将它们应用到相应的文件夹，以便这些文件夹中的视频获得特定的视频演绎版。
   >* 当您将任何视频上传到应用了“处理”配置文件的文件夹时，会处理视频并创建配置的演绎版，Screens设备会进一步使用这些演绎版来播放视频。

