---
title: 图像集
description: 了解如何在Dynamic Media中使用图像集。
feature: Image Sets
role: User
exl-id: 2eb71f24-73d9-4b5c-8605-923a0e3d1505
source-git-commit: a2bbc64051214efa83d74d414e2e5f1407433127
workflow-type: tm+mt
source-wordcount: '2135'
ht-degree: 21%

---

# 图像集 {#image-sets}

借助图像集，用户可以通过单击缩略图来查看项目的不同视图，从而为用户提供集成式查看体验。图像集使您可以展示同一项目的替换视图，并且查看器提供了可用于仔细检查图像的缩放工具。

图像集由带有单词的横幅来指定 `IMAGESET`。 此外，如果图像集已发布，则发布日期(由 **[!UICONTROL 世界]** 图标。 此外，上次修改日期(由 **[!UICONTROL 铅笔]** 图标。

![chlimage_1-133](assets/chlimage_1-339.png)

在图像集中，您还可以通过创建图像集并添加缩略图来创建样本。

当您希望以不同的颜色、模式或外表显示项目时，此应用程序非常有用。 要创建带有颜色色板的图像集，您需要为要向用户呈现的每种不同颜色、模式或外表提供一个图像。 每种颜色、模式或外表还需要有一个颜色、模式或外表样本。

例如，假定您要展示帽檐颜色各异的帽子图像，且帽檐分别为红色、绿色和蓝色。在这种情况下，您需要准备同一款帽子的三张拍照。这三张拍照分别对应红色、绿色和蓝色的帽檐。您还需要准备红色、绿色和蓝色三种颜色的样本。颜色色板用作用户在色板集查看器中单击的缩略图，以查看红色、绿色或蓝色的帽子。

>[!NOTE]
>
>有关Assets用户界面的信息，请参阅 [使用触屏UI管理资产](/help/assets/manage-digital-assets.md).

在创建图像集时，Adobe会推荐以下最佳实践，并实施以下限制：

| 限制类型 | 最佳实践 | 规定的限制 |
| --- | --- | --- |
| 每个集的重复资产数 | 无重复项 | 20 |
| 每组图像的最大数量 | 每组5-10张图像 | 1000 |

另请参阅 [Dynamic Media限制](/help/assets/dynamic-media/limitations.md).

## 快速入门：图像集 {#quick-start-image-sets}

要快速设置并运行图像集，请执行以下操作：

1. 可选。[创建批集预设](/help/assets/dynamic-media/batch-set-presets-dm.md) 并将其应用到上传旋转集图像的新文件夹。

   批集预设可以帮助您自动创建图像集。

   >[!IMPORTANT]
   >
   >批量集由IPS（图像生产系统）作为资产摄取的一部分创建。

1. [为多个视图上传主源图像](#uploading-assets-in-image-sets).

   为图像集上传图像。 请记住，用户可以在图像集查看器中缩放图像。 因此，请仔细选择您的图像。 确保图像的最大大小至少为2000像素。

   请参阅 [Dynamic Media — 支持的栅格图像格式](/help/assets/file-format-support.md#image-support-dynamic-media) ，以获取图像集支持的格式列表。

1. [创建图像集](#creating-image-sets).

   在图像集中，用户在图像集查看器中单击缩略图图像。

   要在资产中创建图像集，请选择 **[!UICONTROL 创建]** > **[!UICONTROL 图像集]**. 然后，添加图像并单击&#x200B;**[!UICONTROL 保存]**。

   请参阅 [准备要上传的图像集资产和上传文件](#uploading-assets-in-image-sets).

   请参阅 [使用选择器](/help/assets/dynamic-media/working-with-selectors.md).

1. 添加 [图像集查看器预设](/help/assets/dynamic-media/managing-viewer-presets.md)，根据需要。

   管理员可以创建或修改图像集查看器预设。要查看带有查看器预设的图像集，请选择图像集，然后在左边栏下拉列表中，选择 **[!UICONTROL 查看器]**.

   要创建或编辑查看器预设，请参阅 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 查看器预设]**.

1. （可选） [查看图像集](/help/assets/dynamic-media/image-sets.md#viewing-image-sets) 批次集预设创建的集合。
1. [预览图像集](/help/assets/dynamic-media/previewing-assets.md).

   选择图像集后，您便可以预览该图像集。要在选定的查看器中检查图像集，请选择缩略图图标。 您可以从 **[!UICONTROL 查看器]** 菜单（可从左边栏下拉列表中找到）。

1. [发布图像集](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

   发布图像集时，将会激活 URL 和嵌入字符串。此外，您还必须 [发布任何自定义查看器预设](/help/assets/dynamic-media/managing-viewer-presets.md) 创建的。 现成的查看器预设已发布。

1. [将 URL 关联到您的 Web 应用程序](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)或者[嵌入视频查看器或图像查看器](/help/assets/dynamic-media/embed-code.md)。

   Experience Manager Assets会为图像集创建URL调用，并在您发布图像集后将其激活。 预览资产时，您可以复制这些 URL。或者，您也可以将它们嵌入到您的网站中。

   选择图像集，然后在左边栏下拉列表中，选择 **[!UICONTROL 查看器]**.

   请参阅 [将图像集关联到网页](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) 和 [嵌入视频查看器或图像查看器](/help/assets/dynamic-media/embed-code.md).

要编辑图像集，请参阅 [编辑图像集](#editing-image-sets). 此外，您还可以查看和编辑 [图像集属性](/help/assets/manage-digital-assets.md#editing-properties).

如果您在创建集时遇到问题，请参阅 [Dynamic Media故障诊断](/help/assets/dynamic-media/troubleshoot-dm.md#images-and-sets).

## 上传图像集的资产 {#uploading-assets-in-image-sets}

首先为图像集上传图像资产。 请记住，用户可以在图像集查看器中缩放图像。 因此，请仔细选择您的图像。 确保图像的最大大小至少为2000像素，以优化缩放详细信息。 Dynamic Media每幅可渲染多达2500万像素的图像。 例如，您可以使用5000x5000万像素图像或任何其他大小组合，最多2500万像素。

<!-- Image Sets supports many image file formats, but lossless TIFF, PNG, and EPS images are recommended. -->

请参阅 [Dynamic Media — 支持的栅格图像格式](/help/assets/file-format-support.md#image-support-dynamic-media) ，以获取图像集支持的格式列表。

为图像集上传图像的方法与[在资产中上传任何其他资产](/help/assets/manage-digital-assets.md#uploading-assets)的方法相同。

### 准备要上传的图像集资产 {#preparing-image-set-assets-for-upload}

在创建图像集之前，请确保图像的大小和格式均合适。

要创建多视图的图像集，您需要多个图像，它们要从不同视角显示一个项目或显示同一项目的不同方面。其目标是突出显示项目的重要功能，以便查看者全面了解项目的显示方式或用途。

由于用户可以缩放图像集中的图像，因此请确保图像的最大大小至少为2000像素。 Experience Manager Assets支持多种图像文件格式，但建议使用无损TIFF、PNG和EPS图像。

>[!NOTE]
>
>如果使用缩略图指示产品色板，请执行以下操作：
>
>创建小角或同一图像的不同拍照，以显示不同的颜色、模式或外表。 您还需要与不同颜色、模式或外表相对应的缩略图文件。例如，要通过显示同一款夹克的黑色、咖色和绿色版的图像集展示缩略图，您需要：
>
>* 同一款夹克的黑色、咖色和绿色版拍照。
>* 黑色、咖色和绿色版的缩略图。


## 创建图像集 {#creating-image-sets}

您可以通过用户界面或API创建图像集。

>[!NOTE]
>
>您还可以通过 [批次集预设](/help/assets/dynamic-media/batch-set-presets-dm.md).
>**重要信息：**&#x200B;批量集由 IPS（图像制作系统）作为资产引入的一部分创建。

在将资产添加到资产集时，资产会按字母数字顺序自动添加。 您可以在添加资产后手动重新排序或排序资产。

>[!NOTE]
>
>文件名中包含“，”（逗号）的资产不支持图像集。

在创建图像集时，Adobe会推荐以下最佳实践，并实施以下限制：

| 限制类型 | 最佳实践 | 规定的限制 |
| --- | --- | --- |
| 每个集的重复资产数 | 无重复项 | 20 |
| 每组图像的最大数量 | 每组5-10张图像 | 1000 |

另请参阅 [Dynamic Media限制](/help/assets/dynamic-media/limitations.md).

**要创建图像集，请执行以下操作：**

1. 在Adobe Experience Manager中，选择Experience Manager徽标以访问全局导航控制台。
1. 点按 **[!UICONTROL 导航]** > **[!UICONTROL 资产]**. 导航到要创建图像集的位置，然后转到 **[!UICONTROL 创建]** > **[!UICONTROL 图像集]** 打开“图像集编辑器”页面。

   您还可以从包含资产的文件夹中创建旋转集。

   ![6_5_imagesets-createpulldown](assets/6_5_imagesets-createpulldown.png)

1. 在“图像集编辑器”页面的 **[!UICONTROL 标题]** 字段，输入图像集的名称。 该名称会显示在图像集的横幅中。（可选）输入说明。

   ![6_5_imageset-createnewset](assets/6_5_imageset-creatingnewset.png)

1. 执行以下操作之一：

   * 在“图像集编辑器”页面的左上角附近，选择 **[!UICONTROL 添加资产]**.

   * 在“图像集编辑器”页面的中间附近，选择 **[!UICONTROL 点按以打开资产选择器]**.
   点按以选择要包含在图像集中的资产。 选定资产上有一个复选标记图标。 完成后，在页面的右上角附近，选择 **[!UICONTROL 选择]**.

   借助资产选择器，您可以通过键入关键字并选择 **[!UICONTROL 返回]**. 您还可以应用过滤器来优化搜索结果。您可以按路径、收藏集、文件类型和标记进行过滤。选择过滤器，然后选择 **[!UICONTROL 过滤器]** 图标。 通过选择“视图”图标并选择 **[!UICONTROL 列视图]**, **[!UICONTROL 卡片视图]**&#x200B;或 **[!UICONTROL 列表视图]**.

   请参阅 [使用选择器](/help/assets/dynamic-media/working-with-selectors.md).

   ![6_5_imageset-addassets](assets/6_5_imageset-addingassets.png)

1. 在将资产添加到资产集时，资产会按字母数字顺序自动添加。 您可以在添加资产后手动重新排序或排序资产。

   如有必要，请将资产的重新排序图标拖动到资产文件名右侧，以在设置列表的上下方对图像重新排序。

   ![6_5_imageset-reorderassets](assets/6_5_imageset-reorderassets.png)

   如果要更改缩略图或色板，请单击图像旁的 **+** **缩略图**&#x200B;图标，然后导航到所需的缩略图或色板。选择完所有图像后，单击&#x200B;**[!UICONTROL 保存]**。

1. （可选）执行以下操作之一：

   * 要删除图像，请选择该图像并选择 **[!UICONTROL 删除资产]**.

   * 要应用预设，请在页面的右上角附近，选择 **[!UICONTROL 预设]**，然后选择要同时应用于所有资产的预设。
   >[!NOTE]
   >
   >创建图像集时，可以更改图像集缩略图。 或者，您也可以让Experience Manager根据图像集中的资产自动选择缩略图。 要选择缩略图，请选择 **[!UICONTROL 更改缩略图]** 在“图像集编辑器”页面的“标题”字段上方。 然后，选择任意图像（您也可以导航到其他文件夹以查找图像）。 如果您选择了缩略图，然后决定让Experience Manager从图像集中生成缩略图，请选择 **[!UICONTROL 切换到]** **[!UICONTROL 自动缩略图]**.

1. 单击&#x200B;**[!UICONTROL 保存]**。您新创建的图像集会显示在创建时所用的文件夹中。

## 查看图像集 {#viewing-image-sets}

您可以在用户界面中创建图像集，也可以使用 [批次集预设](/help/assets/dynamic-media/batch-set-presets-dm.md).

>[!IMPORTANT]
>
>批集由IPS创建 [图像生成系统] 作为资产摄取的一部分。

但是，使用批集预设创建的集，请执行 *not* 显示在用户界面中。 您可以通过三种不同方式查看这些集。 （即使您是在用户界面中创建图像集，这些方法也可用）。

* 打开资产的属性。 属性指示引用选定资产或其成员的集。 要查看整个集，请选择集名称。

   ![6_5_imageset-assetproperties](assets/6_5_imageset-assetproperties.png)

* 来自任何集的成员图像。选择 **[!UICONTROL 集]** 菜单，以显示资产所属的集。

   ![6_5_imageset-setspuldownmenu](assets/6_5_imageset-setspulldownmenu.png)

* 从搜索中，您可以选择 **[!UICONTROL 过滤器]**，然后展开 **[!UICONTROL Dynamic Media]** 选择 **[!UICONTROL 集]**.

   搜索会返回在UI中手动创建的匹配集，或通过批集预设自动创建的匹配集。 对于自动集，使用“开始于”执行搜索查询。 此搜索标准与基于使用“包含”的Experience Manager不同。 将过滤器设置为 **[!UICONTROL 集]** 是搜索自动集的唯一方法。

   ![chlimage_1-134](assets/chlimage_1-134.png)

>[!NOTE]
>
>您可以通过用户界面查看集，如 [编辑图像集](#editing-image-sets).

## 编辑图像集 {#editing-image-sets}

您可以对图像集执行各种编辑任务，如：

* 向图像集中添加图像。
* 对图像集中的图像重新排序。
* 删除图像集中的资产。
* 应用查看器预设。
* 删除图像集。

**要编辑图像集，请执行以下操作：**

1. 执行以下任一操作：

   * 将鼠标悬停在图像集资产上，然后选择 **[!UICONTROL 编辑]** （铅笔图标）。
   * 将鼠标悬停在图像集资产上，选择 **[!UICONTROL 选择]** （复选标记图标），然后选择 **[!UICONTROL 编辑]** 中。
   * 点按图像集资产，然后选择 **[!UICONTROL 编辑]** （铅笔图标）。

1. 要编辑图像集中的图像，请执行以下任意操作：

   * 要对资产重新排序，请将图像拖到新位置（选择重新排序图标以移动项目）。
   * 要按升序或降序对项目进行排序，请单击列标题。
   * 要添加资产或更新现有资产，请单击 **[!UICONTROL 添加资产]**. 导航到资产，选择该资产，然后选择 **[!UICONTROL 选择]** 在页面的右上角附近。

      >[!NOTE]
      >
      >如果您通过将Experience Manager用作缩略图的图像替换为其他图像来删除图像，则仍会显示原始资产。
   * 要删除资产，请选择资产，然后选择 **[!UICONTROL 删除资产]**.
   * 要应用预设，请在页面的右上角附近，选择 **[!UICONTROL 预设]**，然后选择查看器预设。
   * 要添加或更改缩略图，请选择资产右侧的缩略图图标。 导航到新的缩略图或色板资产，将其选中，然后选择 **[!UICONTROL 选择]**.
   * 要删除整个图像集，请导航到图像集，选择该图像集，然后选择 **[!UICONTROL 删除]**.

   >[!NOTE]
   >
   >您可以编辑图像集中的图像。 导航到集并选择 **[!UICONTROL 设置成员]** 中。 要打开编辑窗口，请选择资产上的铅笔图标。

1. 点按 **[!UICONTROL 保存]** 完成编辑后。

## 预览图像集 {#previewing-image-sets}

请参阅 [预览资产](/help/assets/dynamic-media/previewing-assets.md).

## 发布图像集 {#publishing-image-sets}

请参阅 [发布资产](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).
