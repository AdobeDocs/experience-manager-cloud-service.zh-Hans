---
title: 在Screens中创建视频演绎版as a Cloud Service
description: 本页介绍如何在Screens中创建视频演绎版as a Cloud Service。
exl-id: a9c46036-cd29-47fa-81d9-c865cf22c98a
feature: Administering Screens
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---

# 在Screens中创建视频演绎版as a Cloud Service {#creating-screens-video-renditions}

## 简介 {#introduction}

本节介绍如何在Screens播放器中创建使用的视频演绎版。

>[!IMPORTANT]
>如果您计划在Screens渠道中使用视频，则必须配置本节中重点介绍的步骤。

## 在Screens中创建视频演绎版的步骤as a Cloud Service {#steps-creating-screens-video-renditions}

请按照以下步骤从Screens内容提供程序在Screens as a Cloud Service中创建视频演绎版：

1. 在Screens Content Provider中导航到您的渠道。

   >[!NOTE]
   >有关更多详细信息，请参阅[使用Screens内容提供程序](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/configure-screens-cloud/using-screens-content-provider.html#screens-content-provider)。

1. 单击左侧导航栏中的“工具”部分，然后单击&#x200B;**Assets**，然后单击&#x200B;**处理配置文件**。

   ![单击处理配置文件](/help/screens-cloud/assets/configure/screens-cp-3.png)

1. 单击&#x200B;**创建**&#x200B;以创建处理配置文件。

   ![单击“创建”](/help/screens-cloud/assets/configure/screens-video-2.png)

1. 输入&#x200B;**名称**，如&#x200B;**ScreensProcessingProfile**。

   ![显示高亮显示名称字段的“处理配置文件”对话框。](/help/screens-cloud/assets/configure/screens-video-3.png)

1. 导航到&#x200B;**视频**&#x200B;选项卡，以便添加视频编码，然后单击&#x200B;**新增**。

   ![显示“新增”按钮的“处理配置文件”对话框突出显示。](/help/screens-cloud/assets/configure/screens-video-4a.png)

1. 输入&#x200B;**编码名称**，如&#x200B;**screens-fullhd**&#x200B;和&#x200B;**Bitrate**，作为&#x200B;**2500**。

   ![显示“保存”按钮的“处理配置文件”对话框。](/help/screens-cloud/assets/configure/screens-video-4.png)

   >[!IMPORTANT]
   >使用以“screens — ”开头的编码名称。 在Screensas a Cloud Service中，只会考虑使用这些视频呈现版本来播放视频体验。 输入适用于您的视频的比特率（720-px视频为2500 kbps，1080 px视频为5000 kbps）。

   >[!NOTE]
   >可以添加具有不同宽度/高度/比特率的多个视频演绎版，以使用您的视频。 Screens设备会下载所有屏幕和呈现版本，即使该设备仅播放视频呈现版本。

1. 单击&#x200B;**保存**。

1. 选择处理配置文件，然后单击&#x200B;**将配置文件应用到文件夹**。

   ![将配置文件应用到文件夹](/help/screens-cloud/assets/configure/screens-video-5.png)

1. 选择保留Screens视频的文件夹，然后单击&#x200B;**应用**。

   ![单击应用](/help/screens-cloud/assets/configure/screens-video-6.png)

   >[!NOTE]
   >
   >* 您可以创建多个处理配置文件，并将其应用到相应的文件夹，以便这些文件夹中的视频能够获得特定的视频演绎版。
   >* 将任何视频上传到应用处理配置文件的文件夹时，将处理视频。 系统会创建配置的演绎版，供Screens设备用于播放视频。
