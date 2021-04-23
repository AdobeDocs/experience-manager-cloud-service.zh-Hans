---
title: 可选 — 如何使用AEM创建单页应用程序(SPA)
description: 在AEM无外设开发人员历程的这一可选延续中，您将了解AEM如何将无外设投放与传统的全堆栈CMS功能结合在一起，以及如何使用AEM SPA Editor框架创建可编辑的SPA。
hide: true
hidefromtoc: true
index: false
translation-type: tm+mt
source-git-commit: 3fd695cbe77873fa57373d91249b71d8c4be8a08
workflow-type: tm+mt
source-wordcount: '1301'
ht-degree: 0%

---


# 如何使用AEM {#create-spa}创建单页应用程序(SPA)

>[!CAUTION]
>
>正在进行中的工作 — 此文档的创建正在进行中，不应理解为完整或明确，也不应将其用于生产目的。

在此可选的[AEM无外设开发者历程的延续中，](#overview.md)您将学习AEM如何将无外设投放与传统的全栈CMS功能结合在一起，以及如何使用SPA  Editor框架创建可编辑的SPA，以及集成外部SPA，从而根据需要启用编辑功能。

## 迄今为止的故事{#story-so-far}

此时，您应已完成整个[AEM无头开发者历程](overview.md)并了解AEM中无头投放的基础知识，包括对以下方面的了解：

* 无头和无头内容投放之间的区别。
* AEM无外设功能。
* 如何组织和AEM无头项目。
* 如何在AEM中创建无外设内容。
* 如何在AEM中检索和更新无头内容。
* 如何与AEM Headless项目实时协作。

因此，您现在要么已开始使用您的第一个AEM无头项目，要么已具备执行此操作所需的全部知识。 恭喜！

那么，你为什么要阅读这段额外的，可选的旅程的延续呢？ 您可能会回想到，在[入门](getting-started.md#integration-levels)中，我们简要地讨论了AEM如何不仅支持无头投放和传统的全栈模型，还支持结合两者优点的混合模型。 尽管不是传统的无外设模型，但这种混合模型可以为某些项目优惠前所未有的灵活性。

本文以您对AEM Headless的了解为基础，深入探索如何创建您自己的单页应用程序(SPA)，这些应用程序实际上可在AEM中编辑。 这样，您可以创建内容并将其直接投放到SPA，但SPA仍可在AEM中编辑。

## 目标 {#objective}

此文档可帮助您了解如何使用AEM SPA Editor框架开发单页应用程序。 阅读此文档后，您应：

* 了解SPA Editor的基本功能。
* 了解构建完全可编辑的AEM for SPA的要求。
* 了解外部SPA如何集成到AEM中。
* 了解应该或不应该如何实现服务器端渲染。

## 要求和先决条件{#requirements-prerequisites}

在开始使用AEM中的SPA之前，有许多要求。

### 知识{#knowledge}

* 使用React或Angular框架创建SPA的开发经验
* AEM创建内容片段和使用编辑器的基本技能
* 请务必查看AEM](/help/implementing/developing/headful-headless.md)中的文档[Headful和Headless，以了解可能的SPA集成的各个级别。

### 工具 {#tools}

* 用于测试部署项目的沙箱访问
* 用于数据建模和测试的本地开发实例
* 现有外部SPA（可选，取决于选择的集成模型）
* AEM 项目原型

## 什么是SPA?{#what-is-a-spa}

单页应用程序(SPA)与传统页面不同，其特点是它以客户端形式呈现，并且主要由Javascript驱动，它依赖Ajax调用加载数据和动态更新页面。 大多数或所有内容在单页加载中检索一次，并根据用户与页面的交互情况根据需要异步加载其他资源。

这减少了页面刷新的需求，并为用户提供了无缝、快速且更像原生App体验的体验。

AEM SPA Editor允许前端开发人员创建可集成到AEM站点的SPA，使内容作者能够像编辑任何其他AEM内容一样轻松地编辑SPA内容。

## 为什么是SPA?{#why-spa}

SPA更快、更流畅，更像本机应用程序，不仅对于网页的访客，而且由于SPA工作方式的性质，它对营销人员和开发人员都极具吸引力。

有关SPA的完整说明以及您使用它们的原因，请参阅[其他资源](#additional-resources)部分，以获取更多部门内文档的链接。

## AEM如何处理SPA

在AEM上开发单页应用程序时，假定前端开发人员在创建SPA时遵守标准最佳做法。 作为前端开发人员，如果您遵循这些一般最佳做法以及一些特定于AEM的原则，您的SPA将能够与AEM及其内容创作功能一起发挥作用。

* **可移植**  — 与任何组件一样，SPA组件应构建为尽可能可移植。SPA应使用可移植、可重用的组件构建。
* **AEM驱动站点结构**  — 前端开发人员创建组件并拥有其内部结构，但依赖AEM定义站点的内容结构。
* **动态渲染**  — 所有渲染应为动态渲染。
* **动态路由** - SPA负责路由,AEM侦听它并基于它获取。任何路由也应是动态的。

有关AEM如何处理SPA的完整说明，请参阅[其他资源](#additional-resources)部分，以获取更多部门内文档的链接。

## AEM SPA Editor {#aem-spa-editor}

使用通用SPA框架(如React和Angular)构建的站点通过动态JSON加载其内容，并且不提供AEM页面编辑器必须的HTML结构才能放置编辑控件。

要在AEM中启用SPA的编辑，需要在SPA的JSON输出与AEM存储库中的内容模型之间进行映射，以保存对内容所做的更改。

AEM中的SPA支持引入了一个精简JS层，当在页面编辑器中加载事件时，该层会与SPA JS代码交互，可通过该层发送并激活编辑控件的位置以允许进行上下文编辑。 此功能基于Content Services API端点概念构建，因为SPA中的内容需要通过Content Services加载。

有关AEM SPA Editor的完整说明，请参阅[其他资源](#additional-resources)部分，以获取更多部门内文档的链接。

## 调整现有SPA {#existing-spas}

如果您有现有的SPA,AEM支持将其嵌入到AEM中，这样内容作者就可以在AEM编辑器中看到它。 这对于视图他们通过内容片段创建的内容非常有用，这些内容是在最终应用程序的上下文中使用的。

此外，只需进行少量更改，您就可以在AEM编辑器中对外部SPA启用特定编辑功能。

RemotePage组件允许在AEM中呈现外部SPA。

有关如何使外部SPA在AEM中可编辑的完整说明，请参阅[其他资源](#additional-resources)部分，以获取更多部门内文档的链接。

## 下一步是什么{#what-is-next}

要开始开发您自己的SPA for AEM，请查看以下文档:

* [SPA WKND教程](/help/implementing/developing/hybrid/wknd-tutorial.md)
* [使用React快速入门](/help/implementing/developing/hybrid/getting-started-react.md)
* [使用Angular](/help/implementing/developing/hybrid/getting-started-angular.md)

如果您需要改编现有SPA以在AEM中使用它，请查看以下文档:

* [RemotePage组件](/help/implementing/developing/hybrid/remote-page.md)
* [在AEM中编辑外部SPA](/help/implementing/developing/hybrid/editing-external-spa.md)

请参见下面的[其他资源](#additional-resources)，了解这些资源可以帮您深入了解AEM中的SPA主题。

## 其他资源 {#additional-resources}

以下是一些其他资源，可以更深入地了解本文档中提到的一些概念。

* [AEM中的Headful和Headless](/help/implementing/developing/headful-headless.md)  — 介绍AEM中提供的不同投放型号
* [SPA简介和演练。](/help/implementing/developing/hybrid/introduction.md) - AEM的SPA简介
* [开发SPA for AEM](/help/implementing/developing/hybrid/developing.md)  — 关于如何开发AEM for SPA的指南
* [SPA Editor概述](/help/implementing/developing/hybrid/editor-overview.md) - SPA Editor工作方式的详细信息
* [服务器端渲染](/help/implementing/developing/hybrid/ssr.md)  — 如何为AEM SPA配置SSR
* [SPA参考文档](/help/implementing/developing/hybrid/reference-materials.md) - JavaScript API参考和指向开放源SPA AEM GitHub项目的链接
* [内容片段](/help/assets/content-fragments/content-fragments.md)  — 如何创建内容片段
* [AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)  - Maven模板，可创建基于最小、最佳实践的Adobe Experience Manager(AEM)项目作为网站的起点
