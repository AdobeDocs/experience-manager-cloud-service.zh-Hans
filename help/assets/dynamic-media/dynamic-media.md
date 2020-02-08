---
title: 使用 Dynamic Media
description: 了解如何使用Dynamic media交付资产以在Web、移动和社交网站上消费。
translation-type: tm+mt
source-git-commit: 6224d193adfb87bd9b080f48937e0af1f03386d6

---


# 使用 Dynamic Media {#working-with-dynamic-media}

[Dynamic Media](https://www.adobe.com/solutions/web-experience-management/dynamic-media.html) 有助于按需提供丰富的产品销售和市场营销可视资产，还能根据 Web、移动设备、社交网站等不同销售渠道的各种需求自动调整资产供应情况。Dynamic Media 依托大量重要资产，能够通过其收放自如、效能卓越的全球网络，实时地生成并传送各式各样的丰富内容。

Dynamic Media 可提供交互式查看体验，包括缩放、360 度旋转和视频。Dynamic Media 以独特的方式整合 Adobe Experience Manager 数字资产管理（资产）解决方案的工作流，从而简化了数字营销活动管理流程。

>[!NOTE]
>
>有关使用Adobe Experience manager和 [Dynamic Media的信息，请参阅社区文章](https://helpx.adobe.com/experience-manager/using/aem_dynamic_media.html)。

## Dynamic Media 的功能 {#what-you-can-do-with-dynamic-media}

通过 Dynamic Media，您可以在发布资产前对其进行管理。[处理数字资产](/help/assets/manage-digital-assets.md)详细介绍了资产的一般处理方式。一般主题包括上传、下载、编辑和发布资产；查看和编辑属性，以及搜索资产。

仅限Dynamic media的功能包括：

* [传送横幅](carousel-banners.md)
* [图像集](image-sets.md)
* [交互式图像](interactive-images.md)
* [交互式视频](interactive-videos.md)
* [混合媒体集](mixed-media-sets.md)
* [全景图像](panoramic-images.md)

* [旋转集](spin-sets.md)
* [视频](video.md)
* [传送 Dynamic Media 资产](delivering-dynamic-media-assets.md)
* [管理资产](managing-assets.md)
* [使用概览创建自定义弹出窗口](custom-pop-ups.md)

另请参 [阅设置Dynamic Media](administering-dynamic-media.md)。

<!-- 

OBSOLETE UNTIL INTEGRATING SCENE7 TOPIC GETS A MAJOR UPDATE
>[!NOTE]
>
>To understand the differences between using Dynamic Media and integrating Dynamic Media Classic with AEM, see [Dynamic Media Classic integration versus Dynamic Media](/help/sites-cloud/administering/integrating-scene7.md#aem-scene-integration-versus-dynamic-media).

-->

## 启用Dynamic Media与禁用Dynamic Media {#dynamic-media-on-versus-dynamic-media-off}

您可以通过以下特征判断是否启用（打开）Dynamic Media:

* 在下载或预览资产时，动态演绎版可用。
* 图像集、旋转集和混合媒体集均可用。
* 创建了 PTIFF 演绎版。

单击图像资产时，在启用Dynamic media的情况下，资产的视图会有所不同。 Dynamic media使用HTML5点播查看器。

### Dynamic renditions {#dynamic-renditions}

当 Dynamic Media 处于启用状态时，可以使用图像和查看器预设等动态演绎版（在&#x200B;**[!UICONTROL 动态]**&#x200B;下）。

![chlimage_1-358](assets/chlimage_1-358.png)

### 图像集、旋转集和混合媒体集 {#image-sets-spins-sets-mixed-media-sets}

当 Dynamic Media 处于启用状态时，可以使用图像集、旋转集和混合媒体集。

![chlimage_1-359](assets/chlimage_1-359.png)

### PTIFF renditions {#ptiff-renditions}

Dynamic media enabled assets include `pyramid.tiffs`.

![chlimage_1-360](assets/chlimage_1-360.png)

### 资产视图更改 {#asset-views-change}

With Dynamic Media enabled, you can zoom in and out by clicking the `+` and `-` buttons. You can also click/tap to zoom into certain area. Revert brings you to the original version and you can make the image full screen by clicking the diagonal arrows. Dynamic Media enabled looks like this:

![chlimage_1-361](assets/chlimage_1-361.png)

禁用Dynamic Media后，您可以放大和缩小并恢复到原始大小：

![chlimage_1-362](assets/chlimage_1-362.png)
