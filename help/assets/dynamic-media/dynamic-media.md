---
title: 使用 Dynamic Media
description: 了解如何使用Dynamic Media提供资产以在Web、移动和社交网站上消费。
translation-type: tm+mt
source-git-commit: a5e94003a3e9023155dc95ceba1a5531e4f20d8f
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 45%

---


# 使用 Dynamic Media {#working-with-dynamic-media}

[Dynamic Media 有助于按需提供丰富的产品销售和市场营销可视资产，还能根据 Web、移动设备、社交网站等不同销售渠道的各种需求自动调整资产供应情况。](https://www.adobe.com/solutions/web-experience-management/dynamic-media.html)Dynamic Media公司使用一组主要源资产，通过其全球、可扩展、性能优化的网络实时生成和交付多种不同的丰富内容。

Dynamic Media 可提供交互式查看体验，包括缩放、360 度旋转和视频。Dynamic Media 以独特的方式整合 Adobe Experience Manager 数字资产管理（资产）解决方案的工作流，从而简化了数字营销活动管理流程。

>[!NOTE]
>
>[与Adobe Experience Manager和Dynamic Media合作](https://helpx.adobe.com/experience-manager/using/aem_dynamic_media.html)上有社区文章。

## Dynamic Media 的功能 {#what-you-can-do-with-dynamic-media}

通过 Dynamic Media，您可以在发布资产前对其进行管理。[处理数字资产](/help/assets/manage-digital-assets.md)详细介绍了资产的一般处理方式。一般主题包括上传、下载、编辑和发布资产；查看和编辑属性，以及搜索资产。

仅限Dynamic Media的功能包括：

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

另请参阅[设置Dynamic Media](administering-dynamic-media.md)。

<!-- 

OBSOLETE UNTIL INTEGRATING SCENE7 TOPIC GETS A MAJOR UPDATE
>[!NOTE]
>
>To understand the differences between using Dynamic Media and integrating Dynamic Media Classic with AEM, see [Dynamic Media Classic integration versus Dynamic Media](/help/sites-cloud/administering/integrating-scene7.md#aem-scene-integration-versus-dynamic-media).

-->

## Dynamic Media启用与Dynamic Media禁用{#dynamic-media-on-versus-dynamic-media-off}

您可以通过以下特征判断是否启用了Dynamic Media:

* 在下载或预览资产时，可以使用动态演绎版。
* 图像集、旋转集和混合媒体集均可用。
* 创建了 PTIFF 演绎版。

单击图像资产时，启用了Dynamic Media后，资产的视图会有所不同。 Dynamic Media使用点播HTML5查看器。

### 动态演绎版{#dynamic-renditions}

当 Dynamic Media 处于启用状态时，可以使用图像和查看器预设等动态演绎版（在&#x200B;**[!UICONTROL 动态]**&#x200B;下）。

![chlimage_1-358](assets/chlimage_1-358.png)

### 图像集、旋转集和混合媒体集 {#image-sets-spins-sets-mixed-media-sets}

当 Dynamic Media 处于启用状态时，可以使用图像集、旋转集和混合媒体集。

![chlimage_1-359](assets/chlimage_1-359.png)

### PTIFF演绎版{#ptiff-renditions}

启用Dynamic Media的资产包括`pyramid.tiffs`。

![chlimage_1-360](assets/chlimage_1-360.png)

### 资产视图更改 {#asset-views-change}

启用Dynamic Media后，可以单击`+`和`-`按钮进行放大和缩小。您还可以单击／点按以放大特定区域。还原功能可使您恢复到原始版本，并可通过单击对角箭头使图像全屏显示。Dynamic Media启用后，

![chlimage_1-361](assets/chlimage_1-361.png)

禁用Dynamic Media后，您可以放大和缩小并恢复到原始大小：

![chlimage_1-362](assets/chlimage_1-362.png)
