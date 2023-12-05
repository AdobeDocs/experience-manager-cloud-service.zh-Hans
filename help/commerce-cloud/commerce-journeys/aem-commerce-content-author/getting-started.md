---
title: CIF 创作快速入门
description: CIF创作快速入门。
exl-id: 0bef4d8c-0ad3-4ec8-ab08-8c83203b3b68
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '778'
ht-degree: 2%

---

# AEM CIF创作快速入门 {#getting-started}

了解Adobe Experience Manager (AEM) CIF创作。

## 迄今为止的故事 {#story-so-far}

在此AEM Content and Commerce历程的上一个文档中， [了解AEM Content and Commerce](/help/commerce-cloud/introduction.md)您已了解Headless CMS和AEM Content and Commerce的基本理论和概念。

本文基于这些基础之上。

## 目标 {#objective}

本文档可帮助您了解如何使用CIF for Content and Commerce特定创作。 阅读本文档后，您应：

* 了解使用通用编辑器创作CIF的概念
* 如何使用产品和类别选取器访问AEM中的产品目录数据
* 如何使用产品驾驶舱和AEM Omnisearch访问内容和商业数据

## 在通用编辑器中创作CIF {#cif-authoring}

CIF扩展了通用编辑器，使其能够在不离开上下文的情况下访问实时产品数据：

打开侧面板，然后从下拉列表中选择“产品”。
![选择产品类型](assets/asset-finder-overview.png)

您可以浏览产品目录或使用全文搜索字段查找产品。
![产品类型](assets/asset-finder-search.png)

可以将产品直接拖放到支持产品放置的组件（例如产品Teaser、产品轮播）上，这会自动创建产品Teaser组件。

## 产品和类别选取器 {#pickers}

如果商务组件或AEM后台对话框需要产品和类别数据，AEM作者可以使用选取器（即UI元素）来舒适地搜索和选择产品目录数据。

### 产品选取器

单击文件夹图标会打开选取器模式UI（例如，产品Teaser）
![产品选取器](assets/product-picker-open.png)

通过浏览左侧的目录结构或搜索，可以找到产品。 全文搜索遵循所选类别并将搜索结果限制在此类别内。
![产品选取器文件夹](assets/product-picker-folders.png)

具有变体的产品标有一个文件夹图标，单击该图标可显示所有变体。
![产品选取器变体](assets/product-picker-variants.png)
![产品选取器变体已打开](assets/product-picker-variants-open.png)

### 类别选取器

像产品选取器一样工作。 单击文件夹图标会打开选取器模式UI（例如，类别轮播）
![类别选取器](assets/category-picker-open.png)

浏览左侧的目录结构并选择类别。
![类别选取器](assets/category-picker-folders.png)

## 产品 Cockpit {#cockpit}

产品驾驶舱是一个快速访问产品目录及其所有扩充内容的中心位置。 在接下来的模块中，您将学习如何使用内容扩充产品数据。 现在，让我们重点关注访问产品数据。

从主菜单中，单击commerce以查看所有附加的产品目录的列表。
![商务菜单项](assets/commerce-menu-item.png)

这将显示所有连接的产品目录的列表。
![驾驶舱综合目录](assets/cockpit-Integrated-catalogs.png)

产品目录默认显示所有产品的所有第一级类别。 单击某个类别会打开该类别，其中包含所有相关产品和子类别，包括其产品。
![驾驶舱产品目录](assets/cockpit-product-catalog.png)

您可以通过单击资产图标来打开产品资产。 图标通过将鼠标悬停在产品图块上来显示。
![驾驶舱产品属性](assets/cockpit-properties.png)

所有产品属性均为只读，因为数据是从连接的后端实时加载的。 更改产品属性必须在后端系统（记录系统）中完成。 选项卡 **变量** 仅在产品具有变体时显示。 单击选项卡会显示所有变体及其属性。
![驾驶舱产品变型](assets/cockpit-properties-variants.png)

其余选项卡显示与产品关联的所有AEM内容。 这些选项卡将在下一模块中进行讨论。

## AEM Omnisearch {#omnisearch}

使用Omnisearch是一种通过全文搜索查找AEM内容的简单方法。 CIF对Omnisearch进行了扩展，对产品目录及其关联的AEM内容进行了全文搜索。
![商务菜单项](assets/omnisearch.png)

Omnisearch在商务后端运行全文搜索以查找所有相关产品。 结果列在下 **查看所有产品**. Omnisearch还会搜索AEM中与搜索到的产品相关的内容。 结果列在相应的AEM类别下。 在此示例中，一个内容片段与产品相关。

## 后续内容 {#what-is-next}

现在您已完成此历程的这一部分，您应：

* 了解使用通用编辑器创作CIF的概念
* 如何使用产品和类别选取器访问AEM中的产品目录
* 如何使用产品驾驶舱和AEM Omnisearch访问内容和商业数据

在此知识的基础上继续您的历程，接下来查看文档 [管理产品目录页面和模板](catalog-templates.md)，了解如何构建和自定义您的第一个产品目录体验。

## 其他资源 {#additional-resources}

我们建议您继续此历程的下一部分 — [管理产品目录页面和模板](catalog-templates.md) — 以下是一些可选资源，这些资源对这里提到的一些概念进行了更深入的探究。 但是，无需这些可选资源即可继续历程。

* [配置存储和目录](/help/commerce-cloud/getting-started.md#catalog)
