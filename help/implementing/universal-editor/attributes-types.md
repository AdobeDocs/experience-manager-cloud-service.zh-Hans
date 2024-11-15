---
title: 属性和项类型
description: 了解通用编辑器所需的数据属性和项类型。
exl-id: 02795a31-244a-42b4-8297-2649125d7777
feature: Developing
role: Admin, Architect, Developer
source-git-commit: edef86c67becf3b8094196d39baa9e69d6c81777
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 53%

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
| `data-aue-filter` | 定义：<br> — 启用了哪些RTE功能<br> — 可以将哪些组件添加到容器<br> — 可以将哪些资产添加到媒体类型 |
| `data-aue-label` | 为编辑器中显示的可选项目定义自定义标签 |
| `data-aue-model` | 定义用于在属性面板中进行基于表单的编辑的模型 |
| `data-aue-behavior` | 定义检测工具](#behaviors)的[行为，例如，独立文本或图像也可以模拟组件使其可移动或可删除 |

## 项目类型 {#item-types}

| `data-aue-type` | 描述 | `data-aue-resource` | `data-aue-prop` | `data-aue-filter` | `data-aue-label` | `data-aue-model` | `data-aue-behavior` |
|---|---|---|---|---|---|---|---|
| `text` | 文本在 HTML 标记内是可编辑的，但只能采用简单的文本格式，没有可用的富文本格式，例如，这通常用于标题组件 | 可选 | 必填 | 不适用 | 可选 | 不适用 | 可选 |
| `richtext` | 文本是可编辑的，具有完整的富文本功能。RTE 会显示在右面板中 | 可选 | 必填 | 不适用 | 可选 | 不适用 | 可选 |
| `media` | 可编辑的是资源，例如图像或视频 | 可选 | 必填 | 可选<br>传递到资源选择器的图像或视频筛选条件列表 | 可选 | 不适用 | 可选 |
| `container` | 可编辑的行为与组件的容器（也就是段落系统）的行为类似。 | 取决于<br>见下文 | 取决于<br>见下文 | 可选<br>允许的组件列表 | 可选 | 不适用 | 不适用 |
| `component` | 可编辑项是一个组件。它不添加额外功能。需要指示DOM的可移动/可删除部分，并需要它来打开属性面板及其字段 | 必填 | 不适用 | 不适用 | 可选 | 可选 | 不适用 |
| `reference` | 可编辑是一个引用，例如内容片段、体验片段或产品 | 取决于<br>见下文 | 取决于<br>见下文 | 可选<br>传递到参考选择器的内容片段、产品或体验片段筛选条件列表 | 可选 | 可选 | 不适用 |

`data-aue-resource`始终是必需的，因为它是指示内容更改写入位置的主键。

* 不需要直接在设置`data-aue-type`的标记上使用。
* 如果未设置，则使用最接近父级的`data-aue-resource`属性。

当您想要在上下文中编辑时，`data-aue-prop`是必需的，但容器是可选的（如果将该容器设置为内容片段并且prop指向多引用字段）。

* `data-aue-prop`是`data-aue-resource`的主键要更新的属性。

## 行为 {#behaviors}

| `data-aue-behavior` | 描述 |
|---|---|
| `component` | 用于允许独立文本、富文本和媒体模仿组件，以便它们也能够在页面上移动和被删除 |
| `container` | 用于允许容器被视为自己的组件，以便它们可以在页面上移动和删除 |
