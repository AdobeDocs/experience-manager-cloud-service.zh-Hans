---
title: 属性和项类型
description: 了解通用编辑器所需的数据属性和项类型。
exl-id: 02795a31-244a-42b4-8297-2649125d7777
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 100%

---


# 属性和类型 {#attributes-types}

了解通用编辑器所需的数据属性和项类型。

## 简介 {#introduction}

为了使应用程序可由 Universal Editor 编辑，必须对其进行适当的检测。这包括包含适当的元数据，以便编辑器能够编辑应用程序的内容。本文档详细说明了这些元数据的属性和项类型。

>[!NOTE]
>
>在服务器端执行内容验证。Universal Editor 仅使用数据属性。必须在 API 级别处理它们是否适合模型/结构的验证。

## 数据属性 {#data-properties}

| 数据属性 | 描述 |
|---|---|
| `data-aue-resource` | 资源的 URN，请参阅[检测文档“AEM Universal Editor 快速入门”页面](getting-started.md#instrument-thepage)部分 |
| `data-aue-prop` | 资源的属性，请参阅[检测文档“AEM Universal Editor 快速入门”页面](getting-started.md#instrument-thepage)部分 |
| `data-aue-type` | [可编辑项的类型](#item-types)（例如文本、图像和引用） |
| `data-aue-filter` | 定义：<br>- 启用了哪些 RTE 功能<br>- 哪些组件可以添加到容器中<br>- 哪些资产可以添加到一个媒体类型 |
| `data-aue-label` | 为编辑器中显示的可选项定义一个自定义标签 |
| `data-aue-model` | 定义一个用于在属性面板中进行基于表单的编辑的模型 |
| `data-aue-behavior` | 已淘汰。它曾经定义过一种适配行为，允许独立文本、富文本和媒体模仿组件，也可以在页面上被移动和删除，提供 `component` 的一种潜在价值。这个属性现已忽略，如果带有 `data-aue-resource` 的项是容器的一个直接子项时，它会自动被视为组件。 |

## 项目类型 {#item-types}

| `data-aue-type` | 描述 | `data-aue-resource` | `data-aue-prop` | `data-aue-filter` | `data-aue-label` | `data-aue-model` |
|---|---|---|---|---|---|---|
| `text` | 文本在 HTML 标记内是可编辑的，但只能采用简单的文本格式，没有可用的富文本格式，例如，这通常用于标题组件 | 可选 | 必填 | 不适用 | 可选 | 不适用 |
| `richtext` | 文本是可编辑的，具有完整的富文本功能。RTE 会显示在右面板中 | 可选 | 必填 | 不适用 | 可选 | 不适用 |
| `media` | 可编辑项是一种资产，例如图像或视频 | 可选 | 必填 | 可选<br>传递到资源选择器的图像或视频筛选条件列表 | 可选 | 不适用 |
| `container` | 可编辑的行为与组件的容器（也就是段落系统）的行为类似。 | 取决于<br>见下文 | 取决于<br>见下文 | 可选<br>允许的组件列表 | 可选 | 不适用 |
| `component` | 可编辑项是一个组件。它不添加额外功能。必须通过它才能表示 DOM 的可移动/可删除部分，以及才能打开属性面板及其字段 | 必填 | 不适用 | 不适用 | 可选 | 可选 |
| `reference` | 可编辑项是一个引用，例如内容片段、体验片段或产品 | 取决于<br>见下文 | 取决于<br>见下文 | 可选<br>传递到参考选择器的内容片段、产品或体验片段筛选条件列表 | 可选 | 可选 |

`data-aue-resource` 始终是必需的，因为它是表示将内容更改写入哪里的主键。

* 在设置了 `data-aue-type` 的标记上不需要它。
* 如果未设置，就会使用距离最近的父项的 `data-aue-resource` 属性。

每当您要在上下文中编辑就需要 `data-aue-prop`，除非容器是可选的（如果设置，则容器是一个内容片段，prop 指向一个多引用字段）。

* `data-aue-prop` 属性用于为 `data-aue-resource` 的主键进行更新。
