---
title: AEM Sites和Edge Delivery Services
description: 了解Edge Delivery Services如何扩展AEM Sites的创作和发布可能性，从而加快内容创建并以100%的性能交付站点。
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: b3497f87446ca4c1c71d48f29aebcaa882feb898
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 5%

---


# AEM Sites和Edge Delivery Services {#sites-and-edge}

了解Edge Delivery Services如何扩展AEM Sites的创作和发布可能性，从而加快内容创建并以100%的性能交付站点。

## 概述 {#overview}

除了AEM Sites as a Cloud Service](/help/sites-cloud/sites-cloud-changes.md)作为云原生AEM as a Cloud Service平台的一部分提供的所有[功能和特性之外，Edge Delivery Services还提供了额外的创作和发布可能性，可加快内容创建并以100%的性能交付站点。

## 什么是Edge Delivery Services？ {#what-is-edge}

Edge Delivery Services可提供卓越的体验，通过交付能够快速创作和开发的高影响力体验来推动参与和转化。 这是一组可组合的服务，这些服务构成一个快速开发环境，以使作者可快速更新和发布，并且快速推出新站点。在文档[Edge Delivery Services概述中了解有关Edge Delivery Services的更多信息。](/help/edge/overview.md)

将Edge Delivery Services与AEM Sitesas a Cloud Service结合使用，您的项目将从以下方面受益：

* [新的开发人员体验](#developer-experience)
* [新发布层](#publish-tier)
* [其他创作选项](#authoring-options)

## 新的开发人员体验 {#developer-experience}

Edge Delivery Services的核心理念是&#x200B;*速度*。 首先从开发人员体验开始。 如果您的开发人员：

* 了解Git基础知识和
* 了解HTML、CSS和JavaScript的基础知识

不到30分钟，他们就可以启动并运行为Edge Delivery Services自定义自己的项目和组件。 首先，在GitHub上克隆我们的样板项目，然后只需提交更改即可。 您的自定义设置会立即上线！

请参阅文档[快速入门 — 开发人员教程](https://www.aem.live/developer/tutorial)，了解有关为Edge Delivery Services开发的更多信息。

## 新的Publish层 {#publish-tier}

不仅开发时间大大缩短，而且Edge Delivery Services也带来了飞速发展的网站。

## 其他创作选项 {#authoring-options}

Edge Delivery Services还可以通过提供新的创作选项来提高内容创建速度。

### 通用编辑器 {#universal-editor}

通用编辑器提供了无缝的、即席即得(WYSIWYG)创作体验，可用于创作任何内容。

请参阅文档[用于Edge Delivery Services的WYSIWYG内容创作](/help/edge/wysiwyg-authoring/authoring.md)，了解有关使用通用编辑器创作内容的更多信息。

### 基于文档的创作 {#document-authoring}

通过基于文档的创作，任何人都可以借助众所周知的工具(Word和Google文档)在不进行任何培训的情况下创建内容。 使用这些简单的工具，Edge Delivery Services可以立即将更改转换为Word文档以更新您的实时网站内容。

请参阅文档[创作和发布内容](https://www.aem.live/docs/authoring)，了解有关使用基于文档的创作的更多信息。

## Edge适合您吗？ {#decision}

Adobe发现，其客户及其利益相关者从各种规模的项目中的Edge Delivery Services中获得了巨大利益。 因此，Adobe建议将Edge Delivery Services作为任何新项目的起点。

也可以在Edge Delivery上部署网站或页面的子集，同时将其余网站或页面保留在当前栈栈中。 每当需要提高性能、自然流量、客户参与度、开发人员或内容周转率时，建议采用此方法。

如果您不确定Edge Delivery是否适合您，请联系您的Adobe代表。

### Edge Delivery和Headless呢？ (#headless)

Edge Delivery是一个与后端分离的性能第一头。 如果您有一个自定义head，例如React SPA，则Adobe建议AEM headless集成模式。 有关详细信息，请参阅[AEM Headless文档](/help/headless/introduction.md)。

但是，Adobe通常建议使用Edge Delivery作为默认头部，以便从其速度和性能中获益，并通过Headless方法(例如React或SPA)集成项目的Headless部分（通常是业务应用程序）。
