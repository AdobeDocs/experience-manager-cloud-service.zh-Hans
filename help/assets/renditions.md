---
title: 在Experience Manager Assets中查看和管理节目
description: 了解AEM Assets和Dynamic Media如何通过静态和动态图像演绎版简化有效的图像管理。
exl-id: 006dc493-c400-4d0f-b314-c1978582b7fb
source-git-commit: 4627eb00ba910d1ad2920db15a87761bd7e4a0c0
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---

# 在Experience Manager Assets中查看和管理节目{#renditions}

Adobe Experience Manager (AEM)中的演绎版是数字资源（如图像）的自定义版本，专为不同的设备和平台而设计，可确保实现最佳性能。 AEM有助于轻松地创建和管理这些演绎版，从而增强用户体验。 您可以创建缩略图、针对Web或移动设备优化图像、添加水印、查看和下载动态呈现版本或智能裁剪呈现版本，以及执行更多其他操作。

Dynamic Media图像预设和智能裁切演绎版可促进符合品牌标准的系统化图像管理，从而最大限度地提升品牌凝聚力。 这简化了在无需任何管理员访问权限的情况下根据需要快速定位和使用动态图像演绎版的过程。

演绎版分为静态和动态两种类型，每种类型都具有独特的特性和功能，我们将进一步详细讨论这些特性和功能。

## 静态演绎版 {#static-renditions}

静态演绎版是数字资产的预生成版本，通常在资产摄取或修改期间创建。 这些演绎版针对特定目的和平台进行了优化，例如Web缩略图、适用于移动设备的响应式设计格式或适用于打印的高分辨率版本，从而确保高效且一致的体验。
学习 [如何查看和下载](#view-dynamic-renditions) 中的静态演绎版 [!DNL Experience Manager Assets].

## 动态演绎版 {#dynamic-renditions}

动态演绎版是实时创建的资产的自定义版本，可满足特定需求，例如根据设备分辨率调整图像大小或裁切以适合不同的宽高比。
这些演绎版使组织能够为不同的受众需求提供个性化和优化的体验。 您可以在中查看和下载动态演绎版 [!DNL Experience Manager Assets].

### 开始之前

* 您必须是有许可的AEM Dynamic Media用户。

* 使用 [!UICONTROL 管理员视图] 要设置：
   * [智能裁剪图像配置文件](/help/assets/dynamic-media/image-profiles.md#creating-image-profiles)
   * [图像预设](/help/assets/dynamic-media/managing-image-presets.md)

  您可以 [切换视图](/help/assets/assets-view-introduction.md#how-to-access-assets-view) 以在“资源”视图中预览动态演绎版。

### 查看和下载动态演绎版 {#view-renditions}

要查看或下载图像的动态演绎版，请执行以下操作 [!DNL Experience Manager Assets]，请按照以下步骤操作：

1. 转到 **[!UICONTROL 资产管理]** > **[!UICONTROL 资产]**.

1. 导航到适用的资源文件夹。

1. 单击要查看的图像，然后单击 **[!UICONTROL 详细信息]**.

1. 在右菜单中，单击 **[!UICONTROL 节目]**. <br> 此 **[!UICONTROL 节目]** 此时将打开面板，其中可用 **[!UICONTROL 动态]** 和 **[!UICONTROL 智能裁剪]** 呈现版本。

   ![动态演绎版](assets/preset_smart_crop.png)
   <!-- ![dynamic renditions](assets/preset_smart_crop_view.png) -->

1. 单击要查看或下载的演绎版。

1. 单击 ![下载图标](assets/do-not-localize/download-icon.png) 图标（位于需要下载的动态演绎版旁边）。 <br> 或者，您可以选择图像演绎版，然后单击 **[!UICONTROL 下载节目]** 选项。

   您可以单击 ![下载图标](assets/do-not-localize/download-icon.png) 顶部可用的图标 **[!UICONTROL 智能裁剪]** 呈现版本部分，用于下载该资源的所有可用智能裁剪呈现版本。

>[!NOTE]
>
>仅当从管理员视图上传资产时，动态演绎版才可见。
