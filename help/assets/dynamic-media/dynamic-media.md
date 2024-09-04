---
title: 使用 Dynamic Media
description: 了解Dynamic Media是什么，您可以使用Dynamic Media提供资源以供在Web、移动和社交网站上使用。
contentOwner: Rick Brough
feature: Dynamic Media,Asset Management
role: Admin,User
exl-id: 3ec3cb85-88ce-4277-a45c-30e52c75ed42
source-git-commit: 57fb7a011cb2da853cdca4f3233cd56775f4a459
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 3%

---

# 使用 Dynamic Media {#working-with-dynamic-media}

[Dynamic Media](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html)可帮助按需提供丰富的视觉营销和营销资源，可自动扩展以用于Web、移动和社交网站上的使用。 Dynamic Media使用一组主要源资源，通过其可扩展、性能优化的全球网络实时生成并提供多种丰富内容变体。

Dynamic Media提供交互式查看体验，包括缩放、360°旋转和视频。 Dynamic Media独特地整合了Adobe Experience Manager数字资产管理(Assets)解决方案的工作流，以简化和简化数字营销活动管理流程。

<!-- >[!NOTE]
>
>A Community article is available on [Working with Adobe Experience Manager and Dynamic Media](https://helpx.adobe.com/experience-manager/using/aem_dynamic_media.html). -->

## 什么是Dynamic Media？

Adobe Experience Manager (AEM)中的Dynamic Mediaas a Cloud Service是一款功能强大的解决方案，旨在帮助您跨数字平台管理、交付和优化富媒体资产，如图像和视频。 它通过允许实时修改（例如根据用户的设备或屏幕大小调整大小、裁剪和质量）将静态媒体转换为动态、引人入胜的体验。 通过Dynamic Media，无论用户使用桌面机、移动设备还是平板电脑，您的资产都会自动调整以提供最佳视觉体验。

Dynamic Media的一个主要优势是能够简化媒体管理。 您无需创建多个版本的图像或视频，Dynamic Media可通过针对每种情况提供最合适的格式来处理所有此类图像或视频。 例如，电子商务企业可以利用360度的产品视图或可缩放图像来创造交互式体验，而内容密集型网站则可以确保快速、高质量的视频流。 这导致更快的加载时间和更引人入胜的用户体验，最终导致更高的客户满意度和更好的转化率。

Dynamic Media与AEM中的数字资产管理(DAM)系统无缝集成，为您提供单个平台来存储、组织和部署您的媒体。 这种集中式方法简化了跨团队的协作，并提供了对资产性能的实时洞察。 无论您是专注于提供引人入胜的视觉效果还是增强媒体驱动的用户交互，Dynamic Media都可以帮助您针对任何渠道优化内容，使其成为致力于提升数字影响力的企业不可或缺的工具。

## 使用Dynamic Media可以做什么 {#what-you-can-do-with-dynamic-media}

通过Dynamic Media，您可以在发布资产之前管理资产。 [使用数字Assets](/help/assets/manage-digital-assets.md)中详细介绍了如何使用常规资源。 一般主题包括上传、下载、编辑和发布资源；查看和编辑属性以及搜索资源。

仅限Dynamic Media的功能包括：

* [传送横幅](carousel-banners.md)
* [图像集](image-sets.md)
* [交互式图像](interactive-images.md)
* [交互式视频](interactive-videos.md)
* [混合媒体集](mixed-media-sets.md)
* [全景图像](panoramic-images.md)
* [旋转集](spin-sets.md)
* [视频](video.md)
* [交付Dynamic Media Assets](delivering-dynamic-media-assets.md)
* [管理Assets](managing-assets.md)
* [使用快速视图创建自定义弹出窗口](custom-pop-ups.md)

另请参阅[设置Dynamic Media](administering-dynamic-media.md)。

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

启用Dynamic Media后，可以使用动态演绎版，例如图像和查看器预设（位于&#x200B;**[!UICONTROL Dynamic]**&#x200B;下）。

![chlimage_1-358](assets/chlimage_1-358.png)

### Dynamic Media图像集、旋转集、混合媒体集 {#image-sets-spins-sets-mixed-media-sets}

如果启用了Dynamic Media，则可以使用图像集、旋转集和混合媒体集。

![chlimage_1-359](assets/chlimage_1-359.png)

### 支持Dynamic Media的PTIFF演绎版 {#ptiff-renditions}

启用了Dynamic Media的资源包括`pyramid.tiffs`。

![chlimage_1-360](assets/chlimage_1-360.png)

### Dynamic Media资源视图更改 {#asset-views-change}

启用Dynamic Media后，您可以通过单击`+`和`-`按钮进行放大和缩小。 您还可以选择放大特定区域。 还原将您带入原始版本，您可以通过单击对角线箭头使图像变为全屏。 已启用Dynamic Media如下所示：

![chlimage_1-361](assets/chlimage_1-361.png)

禁用Dynamic Media后，您可以放大、缩小并恢复到原始大小：

![chlimage_1-362](assets/chlimage_1-362.png)
