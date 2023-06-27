---
title: as a Cloud Service在Screens中创建视频演绎版
description: 本页介绍如何在Screensas a Cloud Service中创建视频演绎版。
exl-id: a9c46036-cd29-47fa-81d9-c865cf22c98a
source-git-commit: d361ddc9a50a543cd1d5f260c09920c5a9d6d675
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---

# as a Cloud Service在Screens中创建视频演绎版 {#creating-screens-video-renditions}

## 简介 {#introduction}

本节介绍如何创建在Screens播放器中使用的视频演绎版。

>[!IMPORTANT]
>如果您计划在Screens渠道中使用视频，则必须配置本节中突出显示的步骤。

## 在Screens中创建视频呈现形式的步骤as a Cloud Service {#steps-creating-screens-video-renditions}

按照以下步骤在as a Cloud Service于Screens Content Provider的Screens中创建视频演绎版：

1. 在Screens Content Provider中导航到您的渠道。

   >[!NOTE]
   >请参阅 [使用Screens内容提供程序](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/configure-screens-cloud/using-screens-content-provider.html?lang=en#screens-content-provider) 了解更多详细信息。

1. 单击左侧导航栏中的“工具”部分，然后单击 **资产** 然后单击 **处理配置文件**.

   ![单击处理配置文件](/help/screens-cloud/assets/configure/screens-cp-3.png)

1. 单击 **创建** 以创建处理配置文件。

   ![单击“创建”](/help/screens-cloud/assets/configure/screens-video-2.png)

1. 输入 **名称**，例如 **ScreensProcessingProfile**.

   ![](/help/screens-cloud/assets/configure/screens-video-3.png)

1. 导航到 **视频** 选项卡，以便添加视频编码，然后单击 **新增**.

   ![](/help/screens-cloud/assets/configure/screens-video-4a.png)

1. 输入 **编码名称** 例如， **screens-fullhd** 和 **比特率** 作为 **2500**.

   ![](/help/screens-cloud/assets/configure/screens-video-4.png)

   >[!IMPORTANT]
   >使用以“screens — ”开头的编码名称。 只有这些视频演绎版被视为在Screens中以as a Cloud Service方式播放视频体验。 输入适用于您的视频的比特率（720-px视频为2500 kbps，1080 px视频为5000 kbps）。

   >[!NOTE]
   >可以添加具有不同宽度/高度/比特率的多个视频演绎版，以便使用您的视频。 Screens设备会下载所有屏幕和演绎版，即使设备只播放视频演绎版。

1. 单击“**保存**”。

1. 选择处理配置文件，然后单击 **将配置文件应用到文件夹**.

   ![将配置文件应用到文件夹](/help/screens-cloud/assets/configure/screens-video-5.png)

1. 选择保存Screens视频的文件夹并单击 **应用**.

   ![单击应用](/help/screens-cloud/assets/configure/screens-video-6.png)

   >[!NOTE]
   >
   >* 您可以创建多个处理配置文件，并将它们应用到相应的文件夹，以便这些文件夹中的视频获得特定的视频演绎版。
   >* 当您将任何视频上传到应用处理配置文件的文件夹时，将处理视频。 系统会创建配置的演绎版，Screens设备会使用这些演绎版播放视频。
