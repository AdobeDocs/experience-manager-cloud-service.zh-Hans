---
title: 屏幕中视频的缩略图支持as a Cloud Service
description: 本页介绍如何在Screens中为视频添加缩略图支持as a Cloud Service。
index: true
exl-id: 7b15d7cc-f089-4008-9039-5f48343a0f20
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 1%

---

# 视频的缩略图支持 {#thumbnail-support-videos}

## 简介 {#introduction}

内容作者可以为视频定义缩略图，以便图像可用作占位符，并在相应团队最终确定实际视频时，正确测试内容播放和定位。 在视频播放失败时，也可以使用图像。

通过在视频组件中添加对缩略图图像的支持，客户可以在渠道中正确添加有效组件（包含实际内容），并在视频实际交付之前执行任何定位配置。

>[!NOTE]
>如果在视频组件上设置了缩略图，则在播放器上的视频播放失败时，将会播放缩略图图像。 这样，您就可以向受众交付所需的消息（通过播放内容），而不是完全跳过该消息。

缩略图支持允许您：

* 当视频尚未就绪，或您不一定想在播放器上测试大型资产下载时，准备渠道体验

* 如果设备上存在播放问题，请设置回退机制。

## 在视频中使用缩略图 {#using-thumbnails}

>[!IMPORTANT]
>**前提条件**
>在了解如何使用视频缩略图之前，请确保了解如何在Screensas a Cloud Service项目中为渠道创建视频演绎版。 请参阅 [此处](/help/screens-cloud/configuring/creating-screens-video-renditions-cloud-service.md) 以了解更多详细信息。

请按照以下步骤在视频中使用缩略图：

1. 导航到现有Screens渠道或创建新渠道。

   >[!NOTE]
   >要了解如何创建渠道并将内容添加到渠道，请参阅 [在Screens中创建和管理渠道as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/create-content/creating-channels-screens-cloud.html?lang=en).

1. 选择渠道并单击 **编辑** 从操作栏中打开编辑器。

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-1.png)

1. 添加或编辑现有视频组件，如下图所示。

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-2.png)

1. 选择视频，然后单击 *扳手* 图标以打开视频属性。

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-3.png)

1. 的 **视频** 对话框打开，您将在其中查看 **缩略图** 拖放区域。

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-4.png)

1. 将图像从资产选取器拖放到 **缩略图** 拖放区域，单击 **完成**.

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-5.png)

1. 单击 **预览**.

1. 如果在组件上设置了视频，则将播放视频。 如果没有，且缩略图已设置，则将播放缩略图。 否则，该组件将被视为未配置，将被跳过。

## 在视频中使用缩略图时支持的用例 {#understand-use-case}

视频中的缩略图支持以下用例：

* 将跳过未设置任何内容的视频组件。

* 只有缩略图集的视频组件将播放缩略图。

* 同时设置了视频（如果视频具有正确的演绎版）和缩略图的视频组件将播放视频。

* 如果出现播放错误，则具有视频集的视频组件将播放缩略图，或者在缩略图未配置的情况下，只跳到下一个项目。
