---
title: 在Experience Manager Assets中查看和管理节目
description: 了解AEM Assets和Dynamic Media如何通过静态和动态图像演绎版简化有效的图像管理。
exl-id: 006dc493-c400-4d0f-b314-c1978582b7fb
feature: Renditions
role: User
source-git-commit: eb5886b5ed6a6f5b52303b4fccf5c266178b36f8
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 在Experience Manager Assets中查看和管理节目{#renditions}

| [搜索最佳实践](/help/assets/search-best-practices.md) | [元数据最佳实践](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [具有 OpenAPI 功能的 Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 开发人员文档](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

Adobe Experience Manager (AEM)中的演绎版是数字资源（如图像）的自定义版本，专为不同的设备和平台而设计，可确保实现最佳性能。 AEM有助于轻松地创建和管理这些演绎版，从而增强用户体验。 您可以创建缩略图、针对Web或移动设备优化图像、添加水印、查看和下载动态演绎版或智能裁剪演绎版，以及执行更多操作。

Dynamic Media图像预设和智能裁切演绎版可促进符合品牌标准的系统化图像管理，从而最大限度地提升品牌凝聚力。 这简化了在无需任何管理员访问权限的情况下根据需要快速定位和使用动态图像演绎版的过程。

演绎版分为静态和动态两种类型，每种类型都具有独特的特性和功能，我们将进一步详细讨论这些特性和功能。

## 静态演绎版 {#static-renditions}

静态演绎版是数字资产的预生成版本，通常在资产摄取或修改期间创建。 这些演绎版针对特定目的和平台进行了优化，例如Web缩略图、适用于移动设备的响应式设计格式或适用于打印的高分辨率版本，从而确保高效且一致的体验。
了解如何在Experience Manager Assets中[查看和下载静态呈现版本](#view-and-download-static-renditions)。

### 查看和下载静态演绎版{#view-and-download-static-renditions}

要查看并下载资源演绎版，请执行以下步骤：

1. 在Assets视图中，单击&#x200B;**Assets**，导航到文件夹，选择一个资源，然后单击&#x200B;**详细信息**。
1. 单击右窗格中可用的演绎版图标。
1. 选择要预览的演绎版，然后单击![下载图标](/help/assets/assets/download-icon.svg)进行下载。

   ![查看和下载动态演绎版](/help/assets/assets/view-download-static-rendition.png)

## 动态演绎版 {#dynamic-renditions}

动态演绎版是实时创建的资产的自定义版本，可满足特定需求，例如根据设备分辨率调整图像大小或裁切以适合不同的宽高比。
这些演绎版使组织能够为不同的受众需求提供个性化和优化的体验。 您可以在Experience Manager Assets中查看和下载动态演绎版。

## Dynamic Media演绎版 {#dynamic-media-renditions}

### 开始之前

* 您必须是有许可的AEM Dynamic Media用户。
* 使用[!UICONTROL 管理员视图]进行设置：
   * [智能裁剪图像配置文件](/help/assets/dynamic-media/image-profiles.md#creating-image-profiles)
   * [图像预设](/help/assets/dynamic-media/managing-image-presets.md)

  您可以[稍后切换视图](/help/assets/assets-view-introduction.md#how-to-access-assets-view)以在Assets视图中预览动态演绎版。
* 将Publish资源重命名为Dynamic Media ，以便在Assets视图中提供Dynamic Media演绎版。 有关详细信息，请参阅[Publish Assets到AEM和Dynamic Media](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/publish-assets-to-aem-and-dm)。


### 查看和下载Dynamic Media呈现版本 {#view-download-dm-renditions}

要在Experience Manager Assets中查看或下载图像的动态演绎版，请执行以下步骤：

1. 转到&#x200B;**[!UICONTROL Assets管理]** > **[!UICONTROL Assets]**。

1. 导航到适用的资源文件夹。

1. 单击需要查看的资产，然后单击&#x200B;**[!UICONTROL 详细信息]**。

1. 在右菜单中，单击&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;图标。 **[!UICONTROL Dynamic Media]**&#x200B;面板显示Dynamic Media和智能裁剪演绎版。

   ![动态演绎](/help/assets/assets/dm-scene7-renditions.png)
   <!-- ![dynamic renditions](assets/preset_smart_crop_view.png) -->

1. 选择要预览的演绎版，然后单击&#x200B;**复制URL**&#x200B;以复制所选演绎版的URL。 单击&#x200B;**下载演绎版**&#x200B;可下载图像资源的演绎版。
1. 选择要预览的智能裁剪演绎版，然后单击&#x200B;**复制URL**&#x200B;以复制所选演绎版的URL。
1. 单击![下载图标](assets/do-not-localize/download-icon.png)可将所有可用的智能裁剪演绎版下载为单个zip文件。
   ![下载图标](/help/assets/assets/smartcrop-rendition.png)

   >[!NOTE]
   >
   >这些演绎版仅适用于图像资源。

## 带有OpenAPI功能呈现的Dynamic Media {#dm-with-openapi-renditions}

### 开始之前

* 您必须是有许可的AEM Dynamic Media用户。
* 必须批准Assets才能显示具有OpenAPI功能呈现的Dynamic Media。 有关详细信息，请参阅[在Experience Manager中批准资源](/help/assets/approve-assets.md#copy-delivery-url-approved-assets)
* 必须在您的AEM as a Cloud Service实例上启用具有OpenAPI功能的Dynamic Media。

### 查看具有OpenAPI功能呈现的Dynamic Media {#view-download-dm-with-openapi-renditions}

1. 选择资产并单击&#x200B;**详细信息**。
1. 单击右侧窗格中可用的Dynamic Media图标。 Dynamic Media面板为所有资源类型显示具有OpenAPI功能的Dynamic Media。
   ![下载图标](/help/assets/assets/dm-with-open-api-copy-url.png)
1. 选择&#x200B;**带有OpenAPI的Dynamic Media**&#x200B;选项，然后单击&#x200B;**复制URL**&#x200B;以复制资源的投放URL。


