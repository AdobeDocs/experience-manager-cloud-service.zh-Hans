---
title: 预览 3D 资源
description: 了解如何在Experience Manager中预览3D资源。
contentOwner: Rick Brough
feature: 3D Assets
role: User
exl-id: e873bd25-f841-4063-824f-7e48f40bb678
source-git-commit: d00e1f49438ad36339a09f8914496faeda3d4de6
workflow-type: tm+mt
source-wordcount: '631'
ht-degree: 6%

---

# 在Adobe Experience Manager中预览3D资源{#previewing-3d-assets}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/previewing-3d-assets.html?lang=zh-Hans) |
| AEM as a Cloud Service | 本文 |

Experience Manager Assets支持3D资源的摄取、管理、预览和交付。

您可以使用自动生成的缩略图演绎版或交互式3D查看器预览3D资产。 交互式3D查看器可在Experience Manager的资源详细信息页面中找到。 该查看器包括一系列交互式相机控件，可让您围绕3D场景旋转、缩放和平移。

<!-- See also [Working with 3D assets in Dynamic Media](/help/assets/dynamic-media/assets-3d.md). -->

## Experience Manager中缩略图预览支持的格式{#supported-thumbnail-previewing-assets}

默认情况下，Experience Manager会为以下文件格式生成缩略图：

| 3D文件扩展名 | 文件格式 | MIME类型 | 注释 |
|---|---|---|---|
| GLB | 二进制GL传输 | model/gltf-binary |  |
| FBX | Autodesk FBX | application/octet-stream |  |
| 对象 | WaveFront 3D对象文件 | application/x-tgif |  |
| 3DS | 3D Studio模型 | application/x-3ds |  |
| 美元z | 通用场景描述 | model/vnd.usdz+zip |  |

## Experience Manager中交互式3D预览支持的格式{#supported-3d-previewing-assets}

Experience Manager本身支持以下文件格式的“交互式3D预览”：

| 3D文件扩展名 | 文件格式 | MIME类型 | 注释 |
|---|---|---|---|
| GLB | 二进制GL传输 | model/gltf-binary |  |
| GLTF | GL传输格式 | model/gltf+json | 请参阅 **注释** 下面的。 |
| 对象 | WaveFront 3D对象文件 | application/x-tgif |  |
| STL | 立体光刻 | application/vnd.ms-pki.stl |  |


>[!NOTE]
>
>如果材料未在gLTF模型的预览中渲染，请确保在 `textures` 与模型位于同一根文件夹中的文件夹，如下所示：

    资产（文件夹）
    model.gltf
    model.bin
    纹理（文件夹）
    material_0_baseColor.jpeg
    material_0_normal.jpeg

## 在Experience Manager中预览3D资源时的性能注意事项{#performance-3d-previewing-assets}

在资产详细信息视图页面中打开3D资产所需的时间取决于多种因素，例如带宽、图像复杂性和到服务器的延迟。

此外，在交互操作相机时，客户端计算机的功能（如工作站、笔记本电脑或移动触摸设备）也很重要。 一个功能相当强大、图形功能良好的系统，可以使交互式3D观看体验更顺畅、更顺畅。

**要在Experience Manager中预览3D资源，请执行以下操作：**

1. 确保已将3D资源上传到Experience Manager。
参见 [3D预览支持的格式](#supported-3d-previewing-assets) 和 [上传资产](/help/assets/manage-digital-assets.md#uploading-assets).
1. 从Experience Manager，在 **[!UICONTROL 导航]** 页面，转到 **[!UICONTROL 资产]** > **[!UICONTROL 文件]**.

   ![导航页面](/help/assets/dynamic-media/assets/navigation-assets.png)

1. 在页面的右上角附近，从“视图”下拉列表中选择 **[!UICONTROL 卡片视图]**，然后导航到要预览的3D资产。

   ![选择3D卡](/help/assets/dynamic-media/assets/3d-card-select.png)
   _在卡片视图中，选择要预览的3D资源的卡片。_

1. 选择3D资产的卡。

   ![交互式三维预览](/help/assets/dynamic-media/assets/3d-preview.png)
   _在资源详细信息视图页面中交互式预览3D资源。_
1. 在3D资产的资产详细信息视图页面上，执行以下任一操作：

   | 查看 | 描述 | 鼠标操作 | 触摸屏操作 |
   | --- | --- | --- | --- |
   | **转动相机** | 围绕 3D 场景和对象旋转视图。 | 左键单击+拖动。 | 单指按下+拖动。 |
   | **平移相机** | 向左、向右、向上或向下平移视图。 | 右键单击+拖动。 | 两指按下+拖动。 |
   | **缩放相机** | 移入和移出3D场景区域。 | 滚轮。 | 两指捏合。 |
   | **重新居中相机** | 将相机重新居中到3D场景中对象上的某个点。 | 双击。 | 双击。 |
   | **重置** | 在页面的右下角附近，选择“重置”图标以将视图目标点恢复到3D资产的中心。 重置也会将相机移近或移远一点，以便以合理的查看大小完整地显示资产。 |   |   |
   | **全屏模式** | 要进入全屏模式，请在页面的右下角选择全屏图标。 |   |   |

1. 完成后，在页面的右上角附近，选择 **[!UICONTROL 关闭]**.
