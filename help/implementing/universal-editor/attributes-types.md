---
title: 属性和项类型
description: 了解通用编辑器所需的数据属性和项类型。
exl-id: 02795a31-244a-42b4-8297-2649125d7777
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 79%

---


# 属性和类型 {#attributes-types}

了解通用编辑器所需的数据属性和项类型。

## 简介 {#introduction}

为了使应用程序可由 Universal Editor 编辑，必须对其进行适当的检测。这包括包含适当的元数据，以便编辑器能够编辑应用程序的内容。本文档详细介绍了这些元数据的属性和项目类型。

>[!NOTE]
>
>在服务器端执行内容验证。Universal Editor 仅使用数据属性。必须在API级别验证它们是否适合模型/结构。

## 数据属性 {#data-properties}

| 数据属性 | 描述 |
|---|---|
| `data-aue-resource` | 资源的 URN，请参阅[检测文档“AEM Universal Editor 快速入门”页面](getting-started.md#instrument-thepage)部分 |
| `data-aue-prop` | 资源的属性，请参阅[检测文档“AEM Universal Editor 快速入门”页面](getting-started.md#instrument-thepage)部分 |
| `data-aue-type` | [可编辑项的类型](#item-types)（例如，文本、图像和引用） |
| `data-aue-filter` | 定义可以使用哪些参考 |
| `data-aue-label` | 为编辑器中显示的可选项目定义自定义标签<br>如果设置了 `data-aue-model`，则会通过模型检索标签 |
| `data-aue-model` | 定义一个模型，该模型会用于属性边栏中基于表单的编辑 |
| `data-aue-behavior` | 定义检测工具](#behaviors)的[行为，例如，独立文本或图像也可以模拟组件使其可移动或可删除 |

## 项目类型 {#item-types}

| `data-aue-type` | 描述 | `data-aue-resource` | `data-aue-prop` | `data-aue-filter` | `data-aue-label` | `data-aue-model` | `data-aue-behavior` |
|---|---|---|---|---|---|---|---|
| `text` | 文本在 HTML 标记内是可编辑的，但只能采用简单的文本格式，没有可用的富文本格式，例如，这通常用于标题组件 | 可选 | 必填 | 不适用 | 可选 | 不适用 | 可选 |
| `richtext` | 文本是可编辑的，具有完整的富文本功能。RTE 会显示在右面板中 | 可选 | 必填 | 不适用 | 可选 | 不适用 | 可选 |
| `media` | 可编辑的是资源，例如图像或视频 | 可选 | 必填 | 可选<br>传递到资源选择器的图像或视频筛选条件列表 | 可选 | 不适用 | 可选 |
| `container` | 可编辑的行为与组件的容器（也就是段落系统）的行为类似。 | 取决于<br>见下文 | 取决于<br>见下文 | 可选<br>允许的组件列表 | 可选 | 不适用 | 不适用 |
| `component` | 可编辑项是一个组件。它不添加额外功能。指示 DOM 的可移动/可删除部分以及打开属性边栏及其字段需要用到它 | 必填 | 不适用 | 不适用 | 可选 | 可选 | 不适用 |
| `reference` | 可编辑是一个引用，例如内容片段、体验片段或产品 | 取决于<br>见下文 | 取决于<br>见下文 | 可选<br>传递到参考选择器的内容片段、产品或体验片段筛选条件列表 | 可选 | 可选 | 不适用 |

根据使用案例，可能需要也可能不需要 `data-aue-prop` 或 `data-aue-resource`。例如：

* 如果您通过 GraphQL 查询内容片段并且希望使列表在上下文中可编辑，则需要 `data-aue-resource`。
* 如果您有一个组件呈现已参考内容片段的内容并且您想更新组件中的参考，则需要 `data-aue-prop`。

## 行为 {#behaviors}

| `data-aue-behavior` | 描述 |
|---|---|
| `component` | 用于允许独立文本、富文本和媒体模仿组件，以便它们也能够在页面上移动和被删除 |
| `container` | 用于允许容器被视为自己的组件，以便它们可以在页面上移动和删除 |
