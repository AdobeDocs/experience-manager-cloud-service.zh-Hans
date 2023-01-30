---
title: 预览 3D 资源
description: 了解如何在Experience Manager中预览3D资产。
contentOwner: Rick Brough
feature: 3D Assets
role: User
exl-id: e873bd25-f841-4063-824f-7e48f40bb678
source-git-commit: 35caac30887f17077d82f3370f1948e33d7f1530
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 10%

---

# 在Adobe Experience Manager中预览3D资产{#previewing-3d-assets}

Experience Manager支持在创作过程中上传、交付和交互式预览3D资产。

交互式3D查看器可从资产详细信息页面中Experience Manager。 该查看器提供了各种控件，其中包括一组交互式相机控件，可让您对 3D 资产执行绕行、缩放和平移操作。

<!-- See also [Working with 3D assets in Dynamic Media](/help/assets/dynamic-media/assets-3d.md). -->

## 支持的3D预览格式(Experience Manager){#supported-3d-previewing-assets}

Experience Manager中的交互式3D预览支持以下文件格式：

| 3D文件扩展名 | 文件格式 | MIME类型 | 注释 |
|---|---|---|---|
| GLB | 二进制GL传输 | model/gltf-binary |  |
| GLTF | GL传输格式 | model/gltf+json | 请参阅 **注意** 下。 |
| OBJ | WaveFront 3D对象文件 | application/x-tgif |  |
| STL | 立体成形 | application/vnd.ms-pki.stl |  |
| DN | Adobe Dimension | model/x-adobe-dn | 仅支持摄取；预览不可用。 |
| USDZ | 通用场景描述Zip存档 | model/vnd.usdz+zip | 仅支持摄取；预览不可用。 |

>[!NOTE]
>
>如果在gLTF模型的预览中未呈现材料，请确保它们的名称正确，并且在 `textures` 文件夹，与模型相同，如下所示：

    资产（文件夹）
    model.gltf
    model.bin
    纹理（文件夹）
    material_0_baseColor.jpeg
    material_0_normal.jpeg

## 在预览3D资产时的性能注意事项Experience Manager{#performance-3d-previewing-assets}

在资产详细信息视图页面中打开3D资产所花费的时间取决于多个因素，例如带宽、图像复杂性和服务器延迟。

此外，在以交互方式操作相机时，客户端计算机的功能（如工作站、笔记本或移动触控设备）也很重要。 具备良好图形功能的相当强大的系统可以使交互式 3D 查看体验更流畅、更舒适。

**要在Experience Manager中预览3D资产，请执行以下操作：**

1. 确保已将3D资产上传到Experience Manager。
请参阅 [支持的3D预览格式](#supported-3d-previewing-assets) 和 [上传资产](/help/assets/manage-digital-assets.md#uploading-assets).
1. 从Experience Manager，在 **[!UICONTROL 导航]** 页面，转到 **[!UICONTROL 资产]** > **[!UICONTROL 文件]**.

   ![导航页面](/help/assets/dynamic-media/assets/navigation-assets.png)

1. 在页面的右上角附近，从“视图”下拉列表中，选择 **[!UICONTROL 卡片视图]**，然后导航到要预览的3D资产。

   ![3D卡的选择](/help/assets/dynamic-media/assets/3d-card-select.png)
   _在卡片视图中，选择要预览的3D资产的卡片。_

1. 选择3D资产的卡片。

   ![交互式3D预览](/help/assets/dynamic-media/assets/3d-preview.png)
   _在资产详细信息视图页面中交互式预览3D资产。_
1. 在3D资产的资产详细信息视图页面上，执行以下任一操作：

   | 查看 | 描述 | 鼠标操作 | 触屏操作 |
   | --- | --- | --- | --- |
   | **转动相机** | 围绕 3D 场景和对象旋转视图。 | 左键单击并拖动。 | 单指按住并拖动。 |
   | **平移相机** | 向左、向右、向上或向下平移视图。 | 右键单击并拖动。 | 双指按并拖动。 |
   | **缩放相机** | 进出3D场景的区域。 | 滚轮。 | 双指捏。 |
   | **重新输入相机** | 将相机重新调到3D场景中对象上的某个点。 | 双击. | 双击。 |
   | **重置** | 在页面的右下角附近，选择重置图标以将视图目标点恢复到3D资产的中心。 重置还会使相机更近或更远地移开，以便以合理的查看大小完整地显示资产。 |  |  |
   | **全屏模式** | 要进入全屏模式，请在页面的右下角选择全屏图标。 |  |  |

1. 完成后，在页面的右上角附近，选择 **[!UICONTROL 关闭]**.
