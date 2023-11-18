---
title: 使用 Dynamic Media
description: 了解如何使用Dynamic Media来提供可在Web、移动和社交网站上使用的资源。
contentOwner: Rick Brough
role: Admin,User
exl-id: 3ec3cb85-88ce-4277-a45c-30e52c75ed42
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 6%

---

# 使用 Dynamic Media {#working-with-dynamic-media}

[Dynamic Media](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html) 帮助按需提供丰富的视觉推销和营销资产，自动针对Web、移动和社交网站上的消费进行扩展。 Dynamic Media使用一组主要源资源，通过其可扩展、性能优化的全球网络实时生成并提供多种丰富内容变体。

Dynamic Media提供交互式查看体验，包括缩放、360°旋转和视频。 Dynamic Media独特地整合了Adobe Experience Manager数字资产管理(Assets)解决方案的工作流，以简化和简化数字营销活动管理流程。

<!-- >[!NOTE]
>
>A Community article is available on [Working with Adobe Experience Manager and Dynamic Media](https://helpx.adobe.com/experience-manager/using/aem_dynamic_media.html). -->

## 使用Dynamic Media可以做什么 {#what-you-can-do-with-dynamic-media}

通过Dynamic Media，您可以在发布资产之前管理资产。 中详细介绍了如何使用一般资产 [使用数字资产](/help/assets/manage-digital-assets.md). 一般主题包括上传、下载、编辑和发布资源；查看和编辑属性以及搜索资源。

仅限Dynamic Media的功能包括：

* [传送横幅](carousel-banners.md)
* [图像集](image-sets.md)
* [交互式图像](interactive-images.md)
* [交互式视频](interactive-videos.md)
* [混合媒体集](mixed-media-sets.md)
* [全景图像](panoramic-images.md)

* [旋转集](spin-sets.md)
* [视频](video.md)
* [交付Dynamic Media资源](delivering-dynamic-media-assets.md)
* [管理资源](managing-assets.md)
* [使用快速视图创建自定义弹出窗口](custom-pop-ups.md)

另请参阅 [设置Dynamic Media](administering-dynamic-media.md).

<!-- 

OBSOLETE UNTIL INTEGRATING SCENE7 TOPIC GETS A MAJOR UPDATE
>[!NOTE]
>
>To understand the differences between using Dynamic Media and integrating Dynamic Media Classic with AEM, see [Dynamic Media Classic integration versus Dynamic Media](/help/sites-cloud/administering/integrating-scene7.md#aem-scene-integration-versus-dynamic-media).

-->

## 启用Dynamic Media与禁用Dynamic Media {#dynamic-media-on-versus-dynamic-media-off}

您可以通过以下特征来判断是否已启用（打开）Dynamic Media：

* 下载或预览资源时，可以使用动态演绎版。
* 图像集、旋转集和混合媒体集均可用。
* 创建PTIFF演绎版。

单击某个图像资源时，启用Dynamic Media后该资源的视图会发生变化。 Dynamic Media使用按需HTML5查看器。

### 动态演绎版 {#dynamic-renditions}

动态演绎版，例如图像和查看器预设(在 **[!UICONTROL 动态]**)在启用Dynamic Media时可用。

![chlimage_1-358](assets/chlimage_1-358.png)

### 图像集、旋转集、混合媒体集 {#image-sets-spins-sets-mixed-media-sets}

如果启用了Dynamic Media，则可以使用图像集、旋转集和混合媒体集。

![chlimage_1-359](assets/chlimage_1-359.png)

### PTIFF演绎版 {#ptiff-renditions}

启用Dynamic Media的资源包括 `pyramid.tiffs`.

![chlimage_1-360](assets/chlimage_1-360.png)

### 资源视图更改 {#asset-views-change}

启用Dynamic Media后，您可以通过单击 `+` 和 `-` 按钮。 您还可以选择放大特定区域。 还原将您带入原始版本，您可以通过单击对角线箭头使图像变为全屏。 已启用Dynamic Media如下所示：

![chlimage_1-361](assets/chlimage_1-361.png)

禁用Dynamic Media后，您可以放大、缩小并恢复到原始大小：

![chlimage_1-362](assets/chlimage_1-362.png)
