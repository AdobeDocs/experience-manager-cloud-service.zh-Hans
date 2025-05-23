---
title: Universal Editor 架构
description: 了解 Universal Editor 的架构以及数据如何在其服务和层之间流动。
exl-id: e6f40743-0f21-4fb6-bf23-76426ee174be
feature: Developing
role: Admin, Architect, Developer
source-git-commit: a7b48559e5bf60c86fecd73a8bcef6c9aaa03b80
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 82%

---


# Universal Editor 架构 {#architecture}

了解 Universal Editor 的架构以及数据如何在其服务和层之间流动。

## 架构构建块 {#building-blocks}

Universal Editor 由四个基本构建块组成，这些构建块将进行交互，使内容作者能够在任意实施中编辑任何内容的任何方面，以提供卓越的体验，提升内容速度并提供最先进的开发人员体验。

1. [编辑器](#editors)
1. [远程应用程序](#remote-app)
1. [API 层](#api-layer)
1. [持久层](#persistence-layer)

本文档概述了所有这些构建块以及它们交换数据的方式。

![Universal Editor 的架构](assets/architecture.png)

>[!TIP]
>
>若要查看 Universal Editor 及其架构，请参阅 [AEM Universal Editor 快速入门](getting-started.md)，了解如何获取 Universal Editor 访问权限以及如何对第一个 AEM 应用程序插桩以使用 Universal Editor。

### 编辑器 {#editors}

* **Universal Editor** – Universal Editor 使用已插桩的 DOM 来允许就地编辑内容。 请参阅[属性和类型](attributes-types.md)，了解有关必要元数据的详细信息。请参阅文档 [AEM Universal Editor 快速入门](getting-started.md)，了解 AEM 中插桩示例。
* **属性面板** — 在上下文中无法编辑组件的某些属性，例如轮播的轮播时间或应始终打开或关闭折叠选项卡。 为了允许编辑此类组件信息，在编辑器的侧面板中提供了一个基于表单的编辑器。

### 远程应用程序 {#remote-app}

要在 Universal Editor 中使应用程序可在上下文中编辑，必须对 DOM 进行插桩。 远程应用程序必须在 DOM 中呈现某些属性。请参阅[属性和类型](attributes-types.md)，了解有关必要元数据的详细信息。请参阅文档 [AEM Universal Editor 快速入门](getting-started.md)，了解 AEM 中插桩示例。

Universal Editor 力求成为最小 SDK，因此，插桩是远程应用程序实施的责任。

### API 层 {#api-layer}

* **内容数据** – 对于 Universal Editor，内容数据的源系统和使用方式都不重要。唯一重要的是使用上下文中可编辑数据来定义和提供所需的属性。
* **持久化数据** – 每个可编辑数据都有一个 URN 标识符。 此 URN 用于将持久性路由到正确的系统和资源。

### 持久层 {#persistence-layer}

* **内容片段模型** — 要支持用于编辑内容片段属性的面板，需要内容片段编辑器和基于表单的编辑器，则需要每个组件的模型和内容片段。
* **Content** — 内容可以存储在任何位置，如AEM、Magento等。

![持久层](assets/persistence-layer.png)

## Universal Editor Service 和后端系统调度 {#service}

Universal Editor 将所有内容更改调度到称为 Universal Editor Service 的集中服务。此服务在 Adobe I/O Runtime 上运行，根据提供的 URN 加载扩展注册表中的可用插件。该插件负责与后端进行通信并返回统一响应。

![Universal Editor Service](assets/universal-editor-service.png)

## 呈现管道 {#rendering-pipelines}

### 服务器端呈现 {#server-side}

![服务器端呈现](assets/server-side.png)

### 静态网站生成 {#static-generation}

![静态网站生成](assets/static-generation.png)

### 客户端呈现 {#client-side}

![客户端呈现](assets/client-side.png)
