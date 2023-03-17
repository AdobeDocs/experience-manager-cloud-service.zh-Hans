---
title: 属性和类型
description: 了解通用编辑器所需的数据属性和类型。
source-git-commit: f454475b65da8f410812bbbe30ca5fc393be410a
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 7%

---


# 属性和类型 {#attributes-types}

了解通用编辑器所需的数据属性和类型。

## 简介 {#introduction}

要使通用编辑器能够编辑应用程序，必须正确处理该应用程序。 这包括包含正确的元数据，以便编辑器可以编辑应用程序的内容。 本文档详细介绍了这些元数据的属性和类型。

>[!NOTE]
>
>在服务器端执行内容验证。 通用编辑器只能与数据属性结合使用。 需要在API级别验证它们是否适合模型/结构。

## 数据属性 {#data-properties}

| 数据属性 | 描述 |
|---|---|
| `itemid` | 运行到资源，请参阅部分 [在AEM中设置通用编辑器入门文档的页面](getting-started.md#instrument-thepage) |
| `itemprop` | 资源的属性，请参阅 [在AEM中设置通用编辑器入门文档的页面](getting-started.md#instrument-thepage) |
| `itemtype` | 可编辑项目的类型（例如，文本、图像、引用等） |
| `data-editor-itemfilter` | 定义可以使用的引用 |
| `data-editor-itemlabel` | 为编辑器中显示的可选项目定义自定义标签 <br>以防 `itemmodel` 设置后，标签将通过模型检索 |
| `data-editor-itemmodel` | 定义将在属性边栏中用于基于表单的编辑的模型 |
| `data-editor-behavior` | 定义工具的行为，例如，独立文本或图像也可以模拟组件以使其可移动或可删除 |

## 项目类型 {#item-types}

| `itemtype` | 描述 | `itemid` | `itemprop` | `data-editor-itemfilter` | `data-editor-itemlabel` | `data-editor-itemmodel` | `data-editor-behvior` |
|---|---|---|---|---|---|---|---|
| `text` | 文本可以在HTML标记中编辑，但只能以简单的文本格式编辑，没有可用的富文本格式，这通常用于标题组件，例如 | 可选 | 必填 | 不适用 | 可选 | 不适用 | 可选 |
| `richtext` | 可以使用全富文本功能编辑文本。 RTE将显示在右侧面板中 | 可选 | 必填 | 不适用 | 可选 | 不适用 | 可选 |
| `media` | 可编辑的资产，如图像或视频 | 可选 | 必填 | 可选<br>将传递到资产选择器的图像或视频筛选条件列表 | 可选 | 不适用 | 可选 |
| `container` | 可编辑的行为与组件（即段落系统）的容器相同。 | 取决于 <br>请参阅下文 | 取决于 <br>请参阅下文 | 可选<br>允许的组件列表 | 可选 | 不适用 | 不适用 |
| `component` | 可编辑组件。 不添加其他功能，将需要用于指示DOM的可移动/可删除部分以及打开属性边栏及其字段 | 必填 | 不适用 | 不适用 | 可选 | 可选 | 不适用 |
| `reference` | 可编辑的是引用，例如内容片段、体验片段或产品 | 取决于 <br>请参阅下文 | 取决于 <br>请参阅下文 | 可选<br>内容片段、产品或体验片段筛选条件的列表，这些条件会传递到引用选择器 | 可选 | 可选 | 不适用 |

具体取决于用例 `itemprop` 或 `itemid` 可能是必需的，也可能不是必需的。 例如：

* `itemid` 如果您通过GraphQL查询内容片段，并且希望该列表在上下文中可编辑，则需要使用此参数。
* `itemprop` 如果您有一个组件在渲染引用的内容片段的内容，并且您想要更新组件中的引用，则需要使用此参数。

## 行为 {#behaviors}

| `data-editor-behavior` | 描述 |
|---|---|
| `component` | 可用于让独立文本、富文本和媒体模拟组件，以便它们也可以在页面上移动和删除 |

## 其他资源 {#additional-resources}

要了解有关通用编辑器的更多信息，请参阅这些文档。

* [通用编辑器简介](introduction.md)  — 了解通用编辑器如何允许编辑任何实施中任何内容的任何方面，以便提供卓越的体验、提高内容速度，并提供一流的开发人员体验。
* [使用通用编辑器创作内容](authoring.md)  — 了解内容作者使用通用编辑器创建内容是多么简单、直观。
* [AEM中通用编辑器快速入门](getting-started.md)  — 了解如何访问通用编辑器，以及如何开始检测您的第一个AEM应用程序以使用它。
* [通用编辑器架构](architecture.md)  — 了解通用编辑器的架构以及数据如何在其服务和层之间流动。
* [通用编辑器身份验证](authentication.md)  — 了解通用编辑器如何进行身份验证。
