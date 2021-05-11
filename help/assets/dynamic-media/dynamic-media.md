---
title: 使用 Dynamic Media
description: 了解如何使用Dynamic Media为在Web、移动和社交网站上消费提供资产。
role: Administrator,Business Practitioner
exl-id: 3ec3cb85-88ce-4277-a45c-30e52c75ed42
translation-type: tm+mt
source-git-commit: 1ad89be4ebddec0705c6f557fed3d697b9f1f3a7
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 37%

---

# 使用 Dynamic Media {#working-with-dynamic-media}

[Dynamic Media 有助于按需提供丰富的产品销售和市场营销可视资产，还能根据 Web、移动设备、社交网站等不同销售渠道的各种需求自动调整资产供应情况。](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html)Dynamic Media使用一组主要源资源，通过其全球、可扩展、性能优化的网络实时生成和交付多种形式的丰富内容。

Dynamic Media提供交互式查看体验，包括缩放、360度旋转和视频。Dynamic Media以独特的方式整合了Adobe Experience Manager数字资产管理（资产）解决方案的工作流，以简化数字活动管理流程。

<!-- >[!NOTE]
>
>A Community article is available on [Working with Adobe Experience Manager and Dynamic Media](https://helpx.adobe.com/experience-manager/using/aem_dynamic_media.html). -->

## Dynamic Media 的功能 {#what-you-can-do-with-dynamic-media}

通过 Dynamic Media，您可以在发布资产前对其进行管理。[处理数字资产](/help/assets/manage-digital-assets.md)详细介绍了资产的一般处理方式。一般主题包括上传、下载、编辑和发布资产；查看和编辑属性，以及搜索资产。

仅Dynamic Media功能包括：

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
* [使用快速视图创建自定义弹出窗口Windows®](custom-pop-ups.md)

另请参阅[设置Dynamic Media](administering-dynamic-media.md)。

<!-- 

OBSOLETE UNTIL INTEGRATING SCENE7 TOPIC GETS A MAJOR UPDATE
>[!NOTE]
>
>To understand the differences between using Dynamic Media and integrating Dynamic Media Classic with AEM, see [Dynamic Media Classic integration versus Dynamic Media](/help/sites-cloud/administering/integrating-scene7.md#aem-scene-integration-versus-dynamic-media).

-->

## Dynamic Media enabled与Dynamic Media disabled {#dynamic-media-on-versus-dynamic-media-off}

您可以通过以下特征判断是否启用了Dynamic Media:

* 在下载或预览资产时，可以使用动态演绎版。
* 图像集、旋转集和混合媒体集均可用。
* 创建了 PTIFF 演绎版。

当您单击图像资产时，启用Dynamic Media后，资产的视图会有所不同。 Dynamic Media使用HTML5点播查看器。

### 动态演绎版{#dynamic-renditions}

当 Dynamic Media 处于启用状态时，可以使用图像和查看器预设等动态演绎版（在&#x200B;**[!UICONTROL 动态]**&#x200B;下）。

![chlimage_1-358](assets/chlimage_1-358.png)

### 图像集、旋转集和混合媒体集 {#image-sets-spins-sets-mixed-media-sets}

当 Dynamic Media 处于启用状态时，可以使用图像集、旋转集和混合媒体集。

![chlimage_1-359](assets/chlimage_1-359.png)

### PTIFF演绎版{#ptiff-renditions}

Dynamic Media启用的资产包括`pyramid.tiffs`。

![chlimage_1-360](assets/chlimage_1-360.png)

### 资产视图更改 {#asset-views-change}

启用Dynamic Media后，可以单击`+`和`-`按钮进行放大和缩小。您还可以单击/点按以放大特定区域。“还原”可使您恢复到原始版本，并可以通过单击对角箭头使图像全屏显示。 已启用Dynamic Media，如下所示：

![chlimage_1-361](assets/chlimage_1-361.png)

禁用Dynamic Media后，您可以放大和缩小并恢复到原始大小：

![chlimage_1-362](assets/chlimage_1-362.png)
