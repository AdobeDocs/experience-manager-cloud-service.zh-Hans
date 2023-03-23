---
title: 通用编辑器架构
description: 了解通用编辑器的架构以及数据如何在其服务和层之间流动。
source-git-commit: 0e66c379e10d275610d85a699da272dc0c32a9a8
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 1%

---


# 通用编辑器架构 {#architecture}

了解通用编辑器的架构以及数据如何在其服务和层之间流动。

## 架构构建基块 {#building-blocks}

通用编辑器由四个基本构建块组成，这些构建块可进行交互，以允许内容作者编辑任何实施中任何内容的任何方面，以便提供卓越的体验、提高内容速度，并提供一流的开发人员体验。

1. [编辑者](#editors)
1. [远程应用程序](#remote-app)
1. [API层](#api-layer)
1. [持久层](#persistence-layer)

本文档概述了每个构建基块以及它们如何交换数据。

![通用编辑器的架构](assets/architecture.png)

>[!TIP]
>
>如果您希望看到通用编辑器及其架构的实际运行情况，请参阅此文档 [AEM中通用编辑器快速入门](getting-started.md) 了解如何访问通用编辑器，以及如何开始检测您的第一个AEM应用程序以使用它。

### 编辑者 {#editors}

* **通用编辑器**  — 通用编辑器使用分析的DOM来允许就地编辑内容。 请查看文档 [属性和类型](attributes-types.md) 以了解有关必需元数据的详细信息。 查看文档 [AEM中通用编辑器快速入门](getting-started.md) 例如AEM中的工具示例。
* **属性边栏**  — 组件的某些属性在上下文中无法编辑，例如轮播的旋转时间或始终打开或关闭折叠面板选项卡的时间。 为了允许编辑这种组件信息，在编辑器的侧边栏中提供基于表单的编辑器。

### 远程应用程序 {#remote-app}

要使应用程序在上下文内可在通用编辑器中编辑，必须对DOM进行分析。 远程应用程序必须在DOM中呈现某些属性。 请查看文档 [属性和类型](attributes-types.md) 以了解有关必需元数据的详细信息。 查看文档 [AEM中通用编辑器快速入门](getting-started.md) 例如AEM中的工具示例。

通用编辑器致力于提供最低限度的SDK，因此该工具由远程应用程序实施负责。

### API层 {#api-layer}

* **内容数据**  — 对于通用编辑器，内容数据的源系统和使用方式都不重要。 只有使用上下文内可编辑的数据来定义和提供所需的属性，这一点才很重要。
* **保留数据**  — 对于每个可编辑的数据，都有一个URN标识符。 此URN用于将持久性路由到正确的系统和资源。

### 持久层 {#persistence-layer}

* **内容片段模型**  — 要支持用于编辑内容片段属性的边栏，需要内容片段编辑器和基于表单的编辑器、每个组件的模型以及内容片段。
* **内容**  — 内容可以存储在任何位置，如在AEM、Magento等中。

![持久层](assets/persistence-layer.png)

## 通用编辑器服务和后端系统调度 {#service}

通用编辑器将所有内容更改分派给称为通用编辑器服务的集中服务。 此服务在Adobe I/O Runtime上运行，会根据提供的URN加载扩展注册表中可用的插件。 插件负责与后端通信并返回统一响应。

![通用编辑器服务](assets/universal-editor-service.png)

## 渲染管道 {#rendering-pipelines}

### 服务器端呈现 {#server-side}

![服务器端渲染](assets/server-side.png)

### 静态站点生成 {#static-generation}

![静态站点生成](assets/static-generation.png)

### 客户端渲染 {#client-side}

![客户端渲染](assets/client-side.png)

## 其他资源 {#additional-resources}

要了解有关通用编辑器的更多信息，请参阅这些文档。

* [通用编辑器简介](introduction.md)  — 了解通用编辑器如何允许编辑任何实施中任何内容的任何方面，以便提供卓越的体验、提高内容速度，并提供一流的开发人员体验。
* [使用通用编辑器创作内容](authoring.md)  — 了解内容作者使用通用编辑器创建内容是多么简单、直观。
* [使用通用编辑器发布内容](publishing.md)  — 了解通用可视化编辑器如何发布内容以及您的应用程序如何处理已发布的内容。
* [AEM中通用编辑器快速入门](getting-started.md)  — 了解如何访问通用编辑器，以及如何开始检测您的第一个AEM应用程序以使用它。
* [属性和类型](attributes-types.md)  — 了解通用编辑器所需的数据属性和类型。
* [通用编辑器身份验证](authentication.md)  — 了解通用编辑器如何进行身份验证。
