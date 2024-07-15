---
title: 构建产品体验
description: 了解如何构建随后可在各种渠道中使用的产品内容，以创建沉浸式购物体验。
exl-id: 4ae70e40-fdf1-4a37-b4dd-0c4882d77908
feature: Commerce Integration Framework
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '1157'
ht-degree: 2%

---

# 构建产品体验 {#building-experiences}

了解如何管理产品体验。

## 迄今为止的故事 {#story-so-far}

在Adobe Experience Manager (AEM)内容和Commerce历程的上一个文档[管理分阶段的产品目录体验](staged-catalog.md)中，您已了解如何管理分阶段的产品目录体验。

## 目标 {#objective}

本文档可帮助您了解如何构建产品内容和体验。

## 产品体验管理 {#management}

产品体验管理是一门学科，用于在AEM中将产品数据（由PIM或商业解决方案拥有）与营销内容进行修饰。 然后，可以将这种包含内容的丰富产品数据用于各种渠道以创建沉浸式购物体验。

在AEM中，您可以创建各种类型的内容，并将它们链接到产品目录。 可以轻松发现和使用相关内容，从而提高工作效率。

### 资源 {#assets}

从较高层面来看，有两种类型的资产与产品相关：产品和营销。 产品资产由商家管理，并专注于显示产品（通常在中性背景前）。 资产在商务解决方案或AEM Assets中进行管理(与Assets集成到商务/pim解决方案)。

营销资产与推广和使用营销所拥有的产品相关。 例如，显示特定上下文中的多个产品(“shop the look”)、“outdoor fall collection”)或操作方法pdf。 CIF提供了一种将任何AEM资源与产品目录对象关联的简单方法。

打开资源属性并切换到&#x200B;**Commerce**&#x200B;选项卡。 利用此选项卡，可管理与产品的关联。 选取器下方的表格提供了有关链接对象的附加信息（仅对选定内容可见）。 单击详细信息图标，以便获取产品驾驶舱的完整视图。 要关联新对象，请单击产品选取器图标（文件夹图标），选择对象并关闭选取器。

![pem资源](assets/pem-assets.png)

### 体验片段 {#experience-fragments}

体验片段是大规模创建可重用或单个产品内容的好方法。 该关联的工作方式与资产类似。 打开属性并切换到&#x200B;**Commerce**&#x200B;选项卡。 利用此选项卡，可管理与产品和类别的关联。 选取器下面的表格提供了有关链接对象的附加信息（仅对选定内容可见）。 单击详细信息图标，以便获取产品驾驶舱的完整视图。 要关联新对象，请单击产品选取器图标（文件夹图标），选择对象并关闭选取器。

![pem xf](assets/pem-xf.png)

### 内容片段 {#content-fragments}

内容片段是任何结构化内容的最佳内容类型。 这可用于通过其他营销数据补充外部产品数据，或以Headless方式创建内容。 内容片段与产品目录对象的关联可通过内容片段模型编辑器中的产品或类别引用类型来实现。 只需将正确的引用类型拖放到模型上并配置字段即可。 这些类型支持单选或多选。

![pem cf模型](assets/pem-cf-model.png)

如果您基于此模型创建内容片段，这些引用类型为您提供了一种简单的方法，即使用相应的选取器来选择正确的对象。

![pem cf](assets/pem-cf.png)

### 产品 Cockpit {#product-cockpit}

在前面的模块中，您被介绍到了产品驾驶舱（或控制台）。 驾驶舱不仅是一种浏览产品目录的简单方法，而且还可以在一个位置查看所有关联的AEM内容。 转到产品控制台，然后打开具有关联内容的产品的属性。 切换到相应的选项卡以查看关联的内容。

![pem驾驶舱](assets/pem-cockpit.png)

单击操作图标将在新的浏览器选项卡中打开该内容。

## 丰富单个产品和类别页面 {#enrich}

在前面的模块中，您已了解如何使用多个产品目录模板。 多个模板是创建不同模板的好方法，但通常不是必需的。 通常，可以将同一模板用于各个内容的占位符。 CIF支持内容片段和体验片段的占位符。

让我们从体验片段占位符开始。 在AEM编辑器中打开产品模板。 将&#x200B;**Commerce Experience Fragment**&#x200B;组件拖放到模板上，然后打开“配置”对话框。

![pem占位符](assets/pem-placeholder.png)

打开组件的对话框，并输入此占位符的名称。 占位符名称为必填，可让您根据需要添加任意数量的占位符。

![pem XF对话框](assets/pem-dialog-xf.png)

打开您在上一步中与产品关联的体验片段。 打开属性并切换到商务选项卡。 在&#x200B;**目录占位符位置**&#x200B;下输入相同的占位符名称。

![pem xf](assets/pem-xf.png)

现在，将&#x200B;**Commerce内容片段**&#x200B;组件拖放到模板上，并打开配置对话框。

![pem CF对话框](assets/pem-dialog-cf.png)

此对话框会重用核心组件内容片段对话框。 在其他资源下查找更多信息。 唯一的区别是配置内容片段模型中的标识符字段（产品SKU或类别UID）的&#x200B;**Link Element**&#x200B;属性。

立即预览具有关联内容片段和/或体验片段的产品页面。 AEM渲染页面时，会根据类型（内容或体验片段）、标识符和体验片段的占位符名称对每个占位符进行查找。 AEM使用URL解析器获取标识符（SKU用于产品，UID用于类别）。 如果返回体验或内容片段，则会将其呈现到占位符位置，否则会忽略占位符。

![pem结果](assets/pem-result.png)

## 使内容可供购买 {#making-shoppable}

也可以通过添加商业组件使常规AEM页面可供购买。 在AEM中创建内容页面，并在编辑器中打开空页面。

![pem空页面](assets/pem-page-empty.png)

首先，将产品详细信息组件拖放到页面上。 然后，切换到Assets侧栏，切换到“产品”并选择产品。 将该产品拖放到产品组件上。 这会在内容页面上显示常规产品组件。

![pem产品页](assets/pem-page-product.png)

如果您已经为该产品创建了关联内容，请在Assets侧边栏中切换到&#x200B;**关联的Commerce内容**。 此选项卡显示与此产品关联的所有AEM内容。 现在，您可以使用任何关联内容快速修饰页面。

![pem扩充页面](assets/pem-page-enriched.png)

## 历程结束？ {#end-of-journey}

恭喜！您已完成AEM Content和Commerce开发人员历程！ 您现在应：

* 了解如何将任何AEM内容关联到产品目录对象
* 使用占位符单独扩充产品和类别页面
* 了解如何使内容可供购买并使用关联的内容选项卡

您现在可以使用AEM Content和Commerce管理产品体验。 但是，AEM Content和Commerce提供了许多其他选项。 查看[其他资源部分](#additional-resources)中提供的其他资源，了解有关此历程中查看的功能的更多信息。

## 其他资源 {#additional-resources}

* [创作Commerce体验](/help/commerce-cloud/authoring/authoring-commerce-experiences.md)
* [产品 Cockpit](/help/commerce-cloud/authoring/product-cockpit.md)
* [内容片段组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=en)
