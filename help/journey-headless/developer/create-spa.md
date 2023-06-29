---
title: 可选 — 如何使用Adobe Experience Manager (SPA)创建单页应用程序(AEM)
description: 在 AEM Headless 开发人员历程的这一可选延续部分中，您将了解 AEM 如何将 Headless 交付与传统的全栈 CMS 功能相结合，以及您如何使用 AEM 的 SPA 编辑器框架来创建可编辑的 SPA。
exl-id: d74848f2-683e-49e1-9374-32596ca5d7d7
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '1266'
ht-degree: 50%

---

# 如何使用 AEM 创建单页应用程序 (SPA) {#create-spa}

在此可选的接续部分中， [AEM Headless开发人员历程](overview.md)，您将了解AEM如何将Headless投放与传统全栈CMS功能相结合。 您还可以了解如何使用AEM SPA Editor框架创建可编辑的SPA，以及集成外部SPA，从而根据需要启用编辑功能。

## 迄今为止的故事 {#story-so-far}

此时，您应已完成整个 [AEM Headless 开发人员历程](overview.md)，并已了解 AEM 中的 Headless 交付的基础知识，包括了解：

* Headless 和 Headful 内容交付之间的区别。
* AEM 的 Headless 功能。
* 如何编排 AEM Headless 项目。
* 如何在 AEM 中创建 Headless 内容。
* 如何在 AEM 中检索和更新 Headless 内容。
* 如何使用 AEM Headless 项目上线。

到目前为止，您或者已经启动了您的第一个AEM Headless项目，或者您知道应该这样做。 恭喜！

那么，为什么你看到这个额外的、可选的旅程延续？ 您还记得在 [快速入门](getting-started.md#integration-levels)，讨论了AEM如何不仅支持headless投放和传统的全栈模型，还支持将两者的优势结合起来的混合模型。 虽然此混合模型不是传统 Headless 模型，但它可以为某些项目提供前所未有的灵活性。

本文基于您对AEM Headless的了解，通过深入探索如何创建自己的可在AEM中编辑的单页应用程序(SPA)。 通过这种方式，您可以创建内容并将其无头交付到SPA，但该SPA在AEM中保持可编辑状态。

## 目标 {#objective}

本文档将帮助您了解如何使用 AEM SPA Editor 框架来开发单页应用程序。阅读本文档后，您应：

* 了解 SPA 编辑器的基本功能。
* 了解为 AEM 构建完全可编辑的 SPA 的要求。
* 了解如何将外部 SPA 集成到 AEM 中。
* 了解如何实现或无法实现服务器端渲染。

## 要求和先决条件 {#requirements-prerequisites}

在AEM中开始使用SPA之前，需要满足几项要求。

### 知识 {#knowledge}

* 有关使用 React 或 Angular 框架创建 SPA 的开发经验
* 有关创建内容片段和使用编辑器的基本 AEM 技能
* 请务必查看文档 [AEM 中的 Headful 和 Headless](/help/implementing/developing/headful-headless.md)，了解可能的 SPA 集成的各种级别。

### 工具 {#tools}

* 用于测试部署项目的沙盒访问
* 用于数据建模和测试的本地开发实例
* 现有的外部 SPA（可选，具体取决于选择的集成模型）
* AEM 项目原型

## 什么是 SPA？ {#what-is-a-spa}

单页应用程序(SPA)与传统页面不同，因为它在客户端渲染，主要由JavaScript驱动，依赖Ajax调用加载数据和动态更新页面。 根据用户与页面的交互，大多数（或全部）内容在单个页面加载中检索一次，并根据需要异步加载其他资源。

此功能降低了页面刷新的需求，为用户提供了无缝、快速的体验，并且感觉更像是本机应用程序体验。

利用 AEM SPA Editor，前端开发人员可以创建可集成到 AEM 站点中的 SPA，从而允许内容作者像编辑任何其他 AEM 内容那样轻松地编辑 SPA 内容。

## 为什么使用 SPA？ {#why-spa}

通过更快、更流畅、更类似于本机应用程序，SPA成为一种有吸引力的体验。 由于SPA的工作方式性质，它不仅对网页访客有益，而且对营销人员和开发人员也有益。

有关 SPA 的完整说明以及使用 SPA 的原因，请参阅[其他资源](#additional-resources)部分，获取指向更深入文档的链接。

## AEM 如何处理 SPA

在 AEM 上开发单页应用程序时，假定前端开发人员在创建 SPA 时遵循标准最佳实践。作为前端开发人员，如果您遵循这些常规最佳实践和一些AEM特定原则，您的SPA将可以利用AEM及其内容创作功能。

* **可移植性** – 与任何组件一样，应构建尽可能可移植的 SPA 组件。应使用可移植且可重用的组件构建 SPA。
* **AEM驱动器站点结构**  — 前端开发人员创建组件并拥有其内部结构，但依赖AEM定义站点的内容结构。
* **动态呈现** – 所有呈现都应是动态的。
* **动态路由** – SPA 负责路由，AEM 负责侦听它并根据它进行提取。任何路由也应是动态的。

有关 AEM 如何处理 SPA 的完整说明，请参阅[其他资源](#additional-resources)部分，获取指向更深入文档的链接。

## AEM SPA Editor {#aem-spa-editor}

使用常用SPA框架(如React和Angular)构建的站点通过动态JSON加载其内容。 它们不提供AEMHTML编辑器放置编辑控件所需的页面结构。

要在AEM中启用SPA编辑，需要在SPA的JSON输出与AEM存储库中的内容模型之间映射，以便您可以保存对内容的更改。

AEM中的SPA支持引入了一个精简JavaScript层，当加载到页面编辑器时，该层会与SPA JavaScript代码交互，从而可发送事件。 可以激活编辑控件的位置，以允许进行上下文内编辑。 此功能以Content Services API端点概念为基础，因为必须通过Content Services加载SPA中的内容。

有关 AEM SPA Editor 的完整说明，请参阅[其他资源](#additional-resources)部分，获取指向更深入文档的链接。

## 适应现有 SPA {#existing-spas}

如果您现有SPA，则AEM支持将其嵌入到AEM中，以便内容作者可以在AEM编辑器中看到它。 此功能对于查看他们通过内容片段在使用内容的最终应用程序上下文中创建的内容非常有用。

此外，只需进行一些小的更改，您就可以在SPA编辑器中对外部AEM启用特定的编辑功能。

RemotePage 组件允许在 AEM 中呈现外部 SPA。

有关如何使外部 SPA 在 AEM 中可编辑的完整说明，请参阅[其他资源](#additional-resources)部分，获取指向更深入文档的链接。

## 后续内容 {#what-is-next}

要开始为 AEM 开发您自己的 SPA，请查看以下文档：

* [SPA WKND 教程](/help/implementing/developing/hybrid/wknd-tutorial.md)
* [使用 React 快速入门](/help/implementing/developing/hybrid/getting-started-react.md)
* [使用 Angular 快速入门](/help/implementing/developing/hybrid/getting-started-angular.md)

如果必须调整现有SPA才能在AEM中使用它，请查看以下文档：

* [RemotePage 组件](/help/implementing/developing/hybrid/remote-page.md)
* [在 AEM 中编辑外部 SPA](/help/implementing/developing/hybrid/editing-external-spa.md)

请参阅下面的[其他资源](#additional-resources)，更深入地了解 AEM 中的 SPA 主题。

## 其他资源 {#additional-resources}

以下是一些附加资源，它们对本文档中提及的一些概念进行了更深入的探讨。

* [AEM 中的 Headful 和 Headless](/help/implementing/developing/headful-headless.md) – AEM 中可用的不同交付模型的描述
* [SPA简介和演练](/help/implementing/developing/hybrid/introduction.md) - AEM中的SPA的简介。
* [为 AEM 开发 SPA](/help/implementing/developing/hybrid/developing.md) – 有关如何为 AEM 开发 SPA 的指南
* [SPA 编辑器概述](/help/implementing/developing/hybrid/editor-overview.md) – SPA 编辑器的工作原理的详细信息
* [服务器端渲染](/help/implementing/developing/hybrid/ssr.md)  — 如何为AEM SPA配置SSR
* [SPA参考文档](/help/implementing/developing/hybrid/reference-materials.md) - JavaScript API引用和开源AEM SPA GitHub项目的链接
* [内容片段](/help/sites-cloud/administering/content-fragments/content-fragments.md) – 如何创建内容片段
* [AEM 项目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=zh-Hans) – Maven 模板，它创建最小的基于最佳实践的 Adobe Experience Manager (AEM) 项目作为您网站的起点
