---
title: 通用编辑器用例和学习路径
description: 了解通用编辑器的主要用例、如何最佳了解它的使用方法以及如何在您自己的项目中实施它。
exl-id: 398ad0e2-c299-4c49-9784-05c84c67bec2
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 100%

---

# 通用编辑器用例和学习路径 {#use-cases-learning-paths}

了解通用编辑器的主要用例、如何最佳详细了解它的使用方法以及如何在您自己的项目中实施它。

## 概述 {#overview}

通用编辑器是一个多功能可视化编辑器，是 Adobe Experience Manager Sites 的一部分。它使作者能够以所见即所得 (WYSIWYG) 的方式对任何无头或有头体验进行编辑。

本文档详细介绍了两个用例，向您展示如何能深入了解它们，以便您可以在自己的项目中实施通用编辑器。

>[!TIP]
>
>如果您还没有阅读，请查看文档[通用编辑器简介](/help/implementing/universal-editor/introduction.md)，以了解关于通用编辑器的完整概述和业务价值。

## 用例 {#use-cases}

无论内容作者在创建什么样的内容，通用编辑器都能为他们提供一种方便、直观的可视化编辑器。两个主要用例是：

* [所见即所得创作](#wysiwyg-authoring) - 使用 AEM Sites 控制台通过通用编辑器在 AEM 中管理您的内容和作者页面
* [无头创作](#headless-authoring) - 使用通用编辑器在您的自定义无头应用程序中创作内容。

### 所见即所得的创作 {#wysiwyg-authoring}

如果您已很熟悉 AEM，您可以使用 Sites 控制台创建和管理您的页面，然后使用通用编辑器编辑这些页面。

通过这种方式，您不仅可以获益于 Sites 控制台中提供的工具，例如页面管理（复制、粘贴、移动）和工作流，还可以获益于现代通用编辑器。

如果这是您的用例，您可以紧接着参阅以下文档，获得关于如何在 AEM 中开始运行通用编辑器的完整概述。

1. [使用 Edge Delivery Services 进行所见即所得创作的开发人员快速入门指南](https://www.aem.live/developer/ue-tutorial) - 在 AEM 中开始使用您的第一个通用编辑器项目
1. [创建区块并将其适配以便在通用编辑器中编辑](https://www.aem.live/developer/universal-editor-blocks) - 了解如何适配区块，使您可以在通用编辑器中编辑内容
1. [使用 Edge Delivery Services 项目为所见即所得的创作进行内容建模](https://www.aem.live/developer/component-model-definitions) - 详细了解如何构建区块以有效进行内容建模，使内容可在通用编辑器中使用。

阅读这些文档后，您可以返回此页面了解无头创作用例以及通用编辑器的一般工作方法。

### 无头创作 {#headless-authoring}

如果您已经有一个无头应用程序，就可以使用通用编辑器为该应用程序创作内容，并将其内容作为内容片段保留在 AEM 中。唯一的要求是此应用程序已经过适配，允许使用通用编辑器。

如果这是您的用例，您可以紧接着参阅以下文档，了解一个经过适配后能够使用通用编辑器的无头应用程序的示例。

* [用于通用编辑器的 SecurBank 应用程序示例](/help/implementing/universal-editor/securbank.md)

阅读这个文档后，您可以返回此页面了解所见即所得创作用例以及通用编辑器的一般工作方法。

{{ue-headless-auth}}

## 通用编辑器的工作方法 {#how-ue-works}

通用编辑器的强大之处在于它能够让作者就地创作任何内容，无论什么内容，它都能为内容作者提供非常直观、统一的用户界面。

通用编辑器的工作方式如下。

1. 开发人员将应用程序或页面进行适配，以便能使用通用编辑器。适配的作用是告诉编辑器哪些内容是可编辑的以及如何保留它。
   * 如果您遵循[使用 Edge Delivery Services 进行所见即所得创作的开发人员快速入门指南](https://www.aem.live/developer/ue-tutorial)文档，您的页面会自动进行适配。
   * 在无头创作中，您的应用程序可以轻松进行适配。
1. 内容作者加载通用编辑器，后者则加载您的页面进行编辑。因为它已经过适配，所以它知道哪些内容是可编辑的以及如何展示和保留这些内容。
1. 内容作者在一个直观的所见即所得界面中编辑页面内容，进行就地编辑。
1. 通用编辑器会自动将更改放回数据源。

如果您想了解有关通用编辑器架构的更多信息，请参阅文档[通用编辑器架构](/help/implementing/universal-editor/architecture.md)。

## 通用编辑器概念说明 {#concepts}

要使页面或应用程序可在通用编辑器中编辑，必须对其进行正确适配。

* [属性和类型](/help/implementing/universal-editor/attributes-types.md) - 为了使应用程序或页面可在通用编辑器中编辑，必须对其进行正确适配。这包括包含适当的元数据，以便编辑器能够编辑应用程序的内容。
* [模型定义、字段和组件类型](/help/implementing/universal-editor/field-types.md) - 只要存在元数据并启用组件编辑后，您就可以定义在编辑器的属性面板中可以操作哪些字段和组件类型。
* [通用编辑器事件](/help/implementing/universal-editor/events.md) - 您可以使用通用编辑器在内容或 UI 交互时发出的事件来增强应用程序中的编辑体验，从而进一步自定义您的应用。

通用编辑器还可以适应您的项目需求。

* [自定义通用编辑器](/help/implementing/universal-editor/customizing.md) - 可以通过筛选编辑器的不同方面或通过扩展编辑器的功能来调整通用编辑器体验。
* [扩展通用编辑器](/help/implementing/universal-editor/extending.md) - 通用编辑器的用户界面的功能可以扩展，以满足您的项目需求。
