---
title: 在Screensas a Cloud Service中创建视频演绎版
description: 本页介绍如何在Screensas a Cloud Service中创建视频演绎版。
exl-id: a9c46036-cd29-47fa-81d9-c865cf22c98a
feature: Administering Screens
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---

# 在Screensas a Cloud Service中创建视频演绎版 {#creating-screens-video-renditions}

## 简介 {#introduction}

本节介绍如何在Screens播放器中创建使用的视频演绎版。

>[!IMPORTANT]
>如果您计划在Screens渠道中使用视频，则必须配置本节中突出显示的步骤。

## 在Screens中创建视频呈现形式的步骤as a Cloud Service {#steps-creating-screens-video-renditions}

执行以下步骤，在as a Cloud Service于Screens Content Provider的Screens中创建视频演绎版：

1. 在Screens Content Provider中导航到您的渠道。

   >[!NOTE]
   >请参阅 [使用Screens内容提供程序](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/configure-screens-cloud/using-screens-content-provider.html#screens-content-provider) 以了解更多详细信息。

1. 单击左侧导航栏中的“工具”部分，然后单击 **资产** 然后单击 **处理配置文件**.

   ![单击处理配置文件](/help/screens-cloud/assets/configure/screens-cp-3.png)

1. 单击 **创建** 以创建处理配置文件。

   ![单击创建](/help/screens-cloud/assets/configure/screens-video-2.png)

1. 输入 **名称**，例如 **ScreensProcessingProfile**.

   ![“处理配置文件”对话框，其中显示高亮显示的“名称”字段。](/help/screens-cloud/assets/configure/screens-video-3.png)

1. 导航到 **视频** 选项卡，以便添加视频编码，然后单击 **新增**.

   ![显示“新增”按钮的“处理配置文件”对话框（高亮显示）。](/help/screens-cloud/assets/configure/screens-video-4a.png)

1. 输入 **编码名称** 例如， **screens-fullhd** 和 **比特率** 作为 **2500**.

   ![显示“保存”按钮的“处理配置文件”对话框。](/help/screens-cloud/assets/configure/screens-video-4.png)

   >[!IMPORTANT]
   >使用以“screens — ”开头的编码名称。 只有这些视频演绎版被视为在Screensas a Cloud Service中播放视频体验。 输入适用于您的视频的比特率（720-px视频为2500 kbps，1080 px视频为5000 kbps）。

   >[!NOTE]
   >可以添加具有不同宽度/高度/比特率的多个视频演绎版，以使用您的视频。 Screens设备会下载所有屏幕和呈现版本，即使该设备仅播放视频呈现版本。

1. 单击&#x200B;**保存**。

1. 选择处理配置文件，然后单击 **将配置文件应用到文件夹**.

   ![将配置文件应用到文件夹](/help/screens-cloud/assets/configure/screens-video-5.png)

1. 选择保留Screens视频的文件夹并单击 **应用**.

   ![单击应用](/help/screens-cloud/assets/configure/screens-video-6.png)

   >[!NOTE]
   >
   >* 您可以创建多个处理配置文件，并将其应用到相应的文件夹，以便这些文件夹中的视频能够获得特定的视频演绎版。
   >* 将任何视频上传到应用处理配置文件的文件夹时，将处理视频。 系统会创建配置的演绎版，供Screens设备用于播放视频。
