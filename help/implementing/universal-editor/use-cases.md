---
title: 通用编辑器用例和学习路径
description: 了解通用编辑器的主要用例，以及如何最好地了解其使用以及如何在您自己的项目中实施它。
exl-id: 398ad0e2-c299-4c49-9784-05c84c67bec2
feature: Developing
role: Admin, Architect, Developer
source-git-commit: bb149cd43158bfd1ceb43b04cc536c8c8291f968
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 0%

---

# 通用编辑器用例和学习路径 {#use-cases-learning-paths}

了解通用编辑器的主要用例，以及如何最好地了解其使用以及如何在您自己的项目上实施它。

## 概述 {#overview}

通用编辑器是一个通用的可视化编辑器，它是Adobe Experience Manager Sites的一部分。 它允许创作者对任何Headless或Headful体验执行“所见即所得”(WYSIWYG)编辑。

本文档详细说明了这两个用例，并说明了如何了解有关它们的更多信息，以便在您自己的项目中实施通用编辑器。

>[!TIP]
>
>如果没有，请查看文档[通用编辑器简介](/help/implementing/universal-editor/introduction.md)，了解通用编辑器的完整概述和价值。

## 用例 {#use-cases}

通用编辑器为您的内容作者提供了一个方便、直观的可视编辑器，而不管他们创建的是什么类型的内容。 两个主要用例包括：

* [WYSIWYG创作](#wysiwyg-authoring) — 使用AEM Sites控制台在AEM中使用通用编辑器管理您的内容和创作页面
* [Headless创作](#headless-authoring) — 使用通用编辑器在您自己的自定义Headless应用程序中创作内容。

### 所见即所得的创作 {#wysiwyg-authoring}

如果您已熟悉AEM，则可以使用站点控制台创建和管理您的页面，然后使用通用编辑器编辑这些页面。

通过这种方式，您可以从Sites控制台中提供的工具(如页面管理（复制、粘贴、移动）和工作流)中受益，也可以从现代的通用编辑器中受益。

如果您有这样的用例，作为紧接着的下一步，请参阅以下文档，全面了解如何在AEM中启动并运行通用编辑器。

1. [使用Edge Delivery Services进行WYSIWYG创作的开发人员快速入门指南](https://www.aem.live/developer/ue-tutorial) — 开始使用AEM中的第一个通用编辑器项目
1. [创建检测为与通用编辑器一起使用的块](https://www.aem.live/developer/universal-editor-blocks) — 了解如何检测块以使您的内容可在通用编辑器中编辑
1. [用于WYSIWYG创作的Edge Delivery Services项目的内容建模](https://www.aem.live/developer/component-model-definitions) — 了解关于如何构建块以有效地对您的内容建模以便与通用编辑器一起使用的详细信息。

阅读这些文档后，您可以返回本页以了解Headless创作用例以及通用编辑器的常规工作方式。

### Headless创作 {#headless-authoring}

如果您已有Headless应用程序，则可以使用通用编辑器为该应用程序创作内容，并将其内容作为AEM中的内容片段保留。 唯一的要求是应用程序必须配置为允许使用通用编辑器。

如果这是您的用例，作为紧接着的步骤，请参阅以下文档来了解使用通用编辑器的Headless应用程序的示例。

* [用于通用编辑器的SecurBank示例应用程序](/help/implementing/universal-editor/securbank.md)

阅读本文档后，您可以返回本页以了解WYSIWYG创作用例以及通用编辑器的常规工作方式。

{{ue-headless-auth}}

## 通用编辑器的工作方式 {#how-ue-works}

通用编辑器的强大功能是能够就地创作任何内容，无论内容是什么，都为内容作者提供完全直观且统一的UI。

通用编辑器的工作方式如下。

1. 开发人员对应用程序或页面进行工具设置，以使用通用编辑器。 此检测告知编辑器哪些内容可编辑以及如何保留内容。
   * 如果您遵循[使用Edge Delivery Services进行WYSIWYG创作的开发人员快速入门指南](https://www.aem.live/developer/ue-tutorial)文档，则您的页面会自动进行检测。
   * 对于Headless创作，可以轻松检测您的应用程序。
1. 内容作者将加载通用编辑器，该编辑器反过来将加载您的页面以进行编辑。 由于它是仪器化的，因此它知道哪些内容可以编辑，以及它如何表示和保留。
1. 内容作者在直观的WYSIWYG界面中编辑页面内容，并就地编辑。
1. 通用编辑器自动将更改保留到数据源。

如果您想了解有关通用编辑器的架构的更多信息，请参阅文档[通用编辑器架构](/help/implementing/universal-editor/architecture.md)。

## 通用编辑器概念 {#concepts}

要使通用编辑器能够编辑某个页面或应用程序，必须正确检测该页面或应用程序。

* [属性和类型](/help/implementing/universal-editor/attributes-types.md) — 为了使通用编辑器能够编辑应用程序或页面，必须正确检测该应用程序或页面。 这包括包含正确的元数据，以便编辑器可以编辑应用程序的内容。
* [模型定义、字段和组件类型](/help/implementing/universal-editor/field-types.md) — 元数据存在以启用组件编辑后，您定义了在编辑器的属性面板中它们可以处理的字段和组件类型。
* [通用编辑器事件](/help/implementing/universal-editor/events.md) — 您可以通过使用通用编辑器在内容或UI交互上发出的事件，来增强应用程序中的编辑体验，从而进一步自定义应用程序。

通用编辑器也可以根据您的项目需求进行调整。

* [自定义通用编辑器](/help/implementing/universal-editor/customizing.md) — 可以通过筛选编辑器的各个方面或扩展编辑器的功能来调整通用编辑器体验。
* [扩展通用编辑器](/help/implementing/universal-editor/extending.md) — 可以扩展通用编辑器的UI以扩展其功能以满足您的项目需求。
