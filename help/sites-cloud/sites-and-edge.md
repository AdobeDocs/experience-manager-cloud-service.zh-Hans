---
title: AEM Sites 和 Edge Delivery Services
description: 了解 Edge Delivery Services 如何扩展 AEM Sites 的创作和发布可能性，以加速内容创建并传递具有 100% 性能的网站。
solution: Experience Manager Sites
feature: Authoring
role: User
exl-id: 7747d6f7-18e4-4713-baea-bcfa94f54934
source-git-commit: a9adbb1886dcfedfc3fccb6f56939c46ba1365ee
workflow-type: ht
source-wordcount: '618'
ht-degree: 100%

---

# AEM Sites 和 Edge Delivery Services {#sites-and-edge}

了解 Edge Delivery Services 如何扩展 AEM Sites 的创作和发布可能性，以加速内容创建并传递具有 100% 性能的网站。

## 概述 {#overview}

除了 AEM Sites as a Cloud Service 作为云原生 AEM as a Cloud Services 平台的一部分提供的[所有功能和特性](/help/sites-cloud/sites-cloud-changes.md)外，Edge Delivery Services 还提供了额外的创作和发布可能性，以加速内容创建并传递具有 100% 性能的网站。

## 什么是 Edge Delivery Services？ {#what-is-edge}

Edge Delivery Services 通过提供可快速创作和开发的高影响力体验，带来卓越的用户体验，从而推动参与度和转化率。它是一组可组合的服务，支持快速开发环境，作者可以在其中快速更新和发布，并快速启动新网站。若要了解有关 Edge Delivery Services 的更多信息，请参阅文档 [Edge Delivery Services 概述。](/help/edge/overview.md)

将 Edge Delivery Services 与 AEM Sites as a Cloud Service 结合使用，您的项目可以从以下方面受益：

* [全新的开发人员体验](#developer-experience)
* [新的发布层](#publish-tier)
* [其他创作选项](#authoring-options)

## 全新的开发人员体验 {#developer-experience}

Edge Delivery Services 的核心理念是&#x200B;*速度*。这始于开发人员体验。如果您的开发人员：

* 了解 Git 基础知识和
* 了解 HTML、CSS 和 JavaScript 的基础知识

他们可以在不到 30 分钟的时间内启动并运行自己的项目和 Edge Delivery Services 的组件。首先在 GitHub 上克隆我们的样板项目，然后提交您的更改。您的定制立即生效！

请参阅文档[快速入门——开发人员教程](https://www.aem.live/developer/tutorial)，了解有关为 Edge Delivery Services 进行开发的更多信息。

## 新的发布层 {#publish-tier}

不仅开发时间大大缩短，而且 Edge Delivery Services 也带来了超快的网站。

## 其他创作选项 {#authoring-options}

Edge Delivery Services 还通过提供新的创作选项来提高您的内容创建速度。

### 通用编辑器 {#universal-editor}

通用编辑器提供了一种无缝的、所见即所得的创作体验，可用于创作任何内容。

请参阅文档 [Edge Delivery Services 所见即所得内容创作](/help/edge/wysiwyg-authoring/authoring.md)，以了解有关使用通用编辑器进行内容创作的更多信息。

### 基于文档的创作 {#document-authoring}

基于文档的创作允许任何人通过利用众所周知的工具（Word 和 Google Docs）来创建内容，而无需任何培训。使用这些简单的工具，Edge Delivery Services 可以立即将 Word 文档的更改转换为您实时网站上的更新内容。

请参阅文档[创作和发布内容](https://www.aem.live/docs/authoring)，了解有关使用基于文档的创作的更多信息。

## Edge 适合您吗？ {#decision}

Adobe 发现，其客户及其利益相关者在各种规模的项目中，都从 Edge Delivery Services 中受益匪浅。因此，Adobe 建议利用 Edge Delivery Services 作为任何新项目的起点。

也可以在 Edge Delivery 上部署一部分网站或页面，同时将其余部分保留在当前堆栈上。每当需要提高性能、自然流量、客户参与度、开发人员或内容速度时，都建议这样做。

如果您不确定 Edge Delivery 是否适合您，请联系您的 Adobe 代表。

### Edge Delivery 和 Headless 呢？(#headless)

Edge Delivery 是与后端分离的性能优先的前端。如果您有一个自定义的前端，比如 React SPA，Adobe 建议使用 AEM headless 集成模式。有关更多信息，请参阅 [AEM Headless 文档](/help/headless/introduction.md)。

然而，Adobe 通常建议使用 Edge Delivery 作为默认前端，以从其速度和性能中受益，并通过 headless 方法（如 React 或 SPA）集成项目的 headless 部分（通常是业务应用程序）。
