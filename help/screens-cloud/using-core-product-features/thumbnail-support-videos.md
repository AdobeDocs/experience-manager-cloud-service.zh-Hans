---
title: Screensas a Cloud Service的视频缩略图支持
description: 本页介绍如何在Screensas a Cloud Service中为视频添加缩略图支持。
index: true
exl-id: 7b15d7cc-f089-4008-9039-5f48343a0f20
source-git-commit: f5af37bf39ecd5a964a8c94a731111c561c2934e
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 1%

---

# 视频的缩略图支持 {#thumbnail-support-videos}

## 简介 {#introduction}

内容作者可以定义视频的缩略图，以便在适当的团队最终确定实际视频时，将图像用作占位符并正确测试内容播放和定位。 在视频播放失败时，也可以使用该图像。

在视频组件中添加对缩略图图像的支持可让客户在渠道中正确添加包含实际内容的有效组件，并在交付视频之前执行任何定位配置。

>[!NOTE]
>如果在视频组件上设置缩略图图像，则在播放器上播放视频播放失败时会播放该图像。 通过此工作流，您可以向受众投放所需消息（通过播放内容），而不是完全跳过该消息。

缩略图支持允许您执行以下操作：

* 当视频尚未准备就绪，或您不一定希望在播放器上测试大型资产下载时，准备渠道体验

* 设置回退机制，以防设备出现播放问题。

## 在视频中使用缩略图 {#using-thumbnails}

>[!IMPORTANT]
>**前提条件**
>在了解如何使用视频缩略图之前，请确保了解如何在Screensas a Cloud Service项目中为频道创建视频演绎版。 参见 [as a Cloud Service在Screens中创建视频演绎版](/help/screens-cloud/configuring/creating-screens-video-renditions-cloud-service.md).

请按照以下步骤在视频中使用缩略图：

1. 导航到现有Screens频道或创建频道。

   >[!NOTE]
   >要了解如何创建渠道和向渠道添加内容，请参阅 [as a Cloud Service在Screens中创建和管理渠道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/create-content/creating-channels-screens-cloud.html?lang=en).

1. 选择渠道。 在操作栏上，单击 **编辑** 以打开编辑器。


   ![操作栏上的编辑按钮。](/help/screens-cloud/using-core-product-features/assets/thumbnail-1.png)

1. 添加或编辑现有视频组件，如下图所示。

   ![高亮显示的视频资源图像。](/help/screens-cloud/using-core-product-features/assets/thumbnail-2.png)

1. 添加或编辑现有视频组件，如下图所示。

1. 选择视频，然后单击配置(*扳手*)图标以打开视频属性。

   ![选定的视频资源图像，带有指向“配置”图标的箭头，被描绘为扳手。 工具栏上。](/help/screens-cloud/using-core-product-features/assets/thumbnail-3.png)

1. 此 **视频** 对话框打开，您可以在其中查看 **缩略图** 放置区域。

   ![显示视频资源图像的视频对话框和缩略图下拉框。](/help/screens-cloud/using-core-product-features/assets/thumbnail-4.png)

1. 将图像从资产选取器拖放到 **缩略图** 放置区域并单击 **完成**.

   ![资源图像选取器显示在“视频”对话框后面，图像资源显示在缩略图拖放框中。](/help/screens-cloud/using-core-product-features/assets/thumbnail-5.png)

1. 单击 **预览**.

1. 如果已在组件上设置视频，则会播放视频。 如果未设置，并且设置了缩略图，则会播放缩略图。 否则，该组件会被视为未配置并被跳过。

## 在视频中使用缩略图时支持的用例 {#understand-use-case}

视频中的缩略图支持以下用例：

* 跳过未设置视频组件。

* 仅具有缩略图集的视频组件播放缩略图。

* 同时具有视频（如果视频具有正确的演绎版）和缩略图集的视频组件播放视频。

* 如果存在播放错误，包含视频集的视频组件将播放缩略图，如果未配置缩略图，则将跳过下一个项目。
