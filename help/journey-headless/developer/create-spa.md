---
title: 可选 — 如何使用AEM创建单页应用程序(SPA)
description: 在AEM无头开发人员历程的这一可选延续中，您将了解AEM如何将无头交付与传统的全栈CMS功能结合使用，以及如何使用AEM SPA编辑器框架创建可编辑的SPA。
source-git-commit: ddd320ae703225584d4a2055d0f882d238d60987
workflow-type: tm+mt
source-wordcount: '1273'
ht-degree: 0%

---


# 如何使用AEM {#create-spa}创建单页应用程序(SPA)

在[AEM无头开发人员历程的这一可选延续中，](overview.md)您将了解AEM如何将无头交付与传统的全栈CMS功能结合使用，以及如何使用AEM SPA编辑器框架创建可编辑的SPA，以及如何集成外部SPA，从而根据需要启用编辑功能。

## 到目前为止{#story-so-far}

此时，您应该已完成整个[AEM Headless Developer历程](overview.md)，并了解AEM中无头投放的基础知识，包括对以下内容的了解：

* 无头内容和有头内容交付之间的区别。
* AEM无头功能。
* 如何组织和AEM Headless项目。
* 如何在AEM中创建无标题内容。
* 如何在AEM中检索和更新无标题内容。
* 如何使用AEM Headless项目进行实时。

因此，您现在要么已开始使用您的第一个AEM Headless项目，要么已拥有执行此操作所需的所有知识。 恭喜！

那么，为什么您要阅读此额外的、可选的历程延续？ 您可能会记得，在[入门](getting-started.md#integration-levels)中，我们简要地讨论了AEM如何不仅支持无头交付和传统的全栈模型，还支持结合两者优势的混合模型。 尽管不是传统的无头模式，但这种混合模式可以为某些项目提供前所未有的灵活性。

本文在您对AEM Headless的了解基础上，深入探讨了如何创建您自己的单页应用程序(SPA)，这些应用程序实际上可以在AEM中编辑。 这样，您便可以创建内容并将其直接交付到SPA，但该SPA仍可在AEM中进行编辑。

## 目标 {#objective}

本文档可帮助您了解单页应用程序是如何使用AEM SPA Editor框架开发的。 阅读本文档后，您应：

* 了解SPA编辑器的基本功能。
* 了解为AEM构建完全可编辑的SPA的要求。
* 了解如何将外部SPA集成到AEM中。
* 了解应该或不应该如何实施服务器端渲染。

## 要求和先决条件{#requirements-prerequisites}

在开始使用AEM中的SPA之前，需要满足一些要求。

### 知识 {#knowledge}

* 使用React或SPA框架创建Angular的开发经验
* 基本AEM技能：创建内容片段和使用编辑器
* 请务必查看AEM](/help/implementing/developing/headful-headless.md)中的文档[Headful和Headless，以了解SPA集成的各种可能级别。

### 工具 {#tools}

* 用于测试部署项目的沙盒访问
* 用于数据建模和测试的本地开发实例
* 现有外部SPA（可选，具体取决于选择的集成模型）
* AEM 项目原型

## 什么是SPA?{#what-is-a-spa}

单页应用程序(SPA)与常规页面的不同之处在于，它在客户端呈现，且主要由Javascript驱动，它依赖Ajax调用来加载数据和动态更新页面。 大多数或所有内容在单页加载中检索一次，并根据用户与页面的交互，根据需要异步加载其他资源。

这减少了页面刷新的需求，并为用户提供了无缝、快速且更像本机应用程序体验的体验。

AEM SPA编辑器允许前端开发人员创建可集成到AEM站点中的SPA，从而允许内容作者像任何其他AEM内容一样轻松地编辑SPA内容。

## 为什么选择SPA?{#why-spa}

通过更快、更流畅、更像本机应用程序，SPA不仅对网页的访客非常有吸引力，而且对营销人员和开发人员也非常有吸引力，因为SPA的工作方式很有吸引力。

有关SPA的完整说明以及使用它们的原因，请参阅[其他资源](#additional-resources)部分，以获取更多部门内文档的链接。

## AEM如何处理SPA

在AEM上开发单页应用程序时，假定前端开发人员在创建SPA时遵循标准的最佳实践。 如果您作为前端开发人员，遵循以下一般最佳实践以及一些特定于AEM的原则，则您的SPA将能够与AEM及其内容创作功能结合使用。

* **可移植性**  — 与任何组件一样，SPA组件应构建为尽可能便携。SPA应使用可移植且可重复使用的组件构建。
* **AEM驱动站点结构**  — 前端开发人员创建组件并拥有其内部结构，但依赖AEM来定义站点的内容结构。
* **动态渲染**  — 所有渲染应为动态。
* **动态路由**  - SPA负责路由，AEM侦听该路由并基于该路由获取。任何路由都应是动态的。

有关AEM如何处理SPA的完整说明，请参阅[其他资源](#additional-resources)部分，以获取指向更多部门内文档的链接。

## AEM SPA编辑器{#aem-spa-editor}

使用常用SPA框架(如React和Angular)构建的站点通过动态JSON加载其内容，并且不提供AEM页面编辑器必须的HTML结构才能放置编辑控件。

要在AEM中启用SPA的编辑功能，需要SPA的JSON输出与AEM存储库中的内容模型之间的映射，才能保存对内容所做的更改。

AEM中的SPA支持引入了一个精简JS层，当该层在页面编辑器中加载时，会与SPA JS代码交互，通过该层可以发送事件，并且可以激活编辑控件的位置以允许进行上下文编辑。 此功能基于Content Services API端点概念，因为SPA中的内容需要通过Content Services加载。

有关AEM SPA Editor的完整说明，请参阅[其他资源](#additional-resources)部分，以获取指向更多部门内文档的链接。

## 调整现有SPA {#existing-spas}

如果您现有SPA, AEM支持将其嵌入到AEM中，以便内容作者可以在AEM编辑器中看到该内容。 在将在其中使用内容片段的最终应用程序上下文中，通过内容片段查看他们正在创建的内容时，此选项非常有用。

此外，只需进行少量更改，您就可以在AEM编辑器中启用对外部SPA的某些编辑功能。

RemotePage组件允许在AEM中渲染外部SPA。

有关如何在AEM中使外部SPA可编辑的完整说明，请参阅[其他资源](#additional-resources)部分，以获取更多部门内文档的链接。

## 下一步是什么{#what-is-next}

要开始开发您自己的SPA for AEM，请查看以下文档：

* [SPA WKND教程](/help/implementing/developing/hybrid/wknd-tutorial.md)
* [开始使用React](/help/implementing/developing/hybrid/getting-started-react.md)
* [开始使用Angular](/help/implementing/developing/hybrid/getting-started-angular.md)

如果您需要调整现有SPA以在AEM中使用它，请查看以下文档：

* [RemotePage组件](/help/implementing/developing/hybrid/remote-page.md)
* [在AEM中编辑外部SPA](/help/implementing/developing/hybrid/editing-external-spa.md)

请参阅下文，了解可让您更深入地了解AEM中SPA主题的[其他资源](#additional-resources)。

## 其他资源 {#additional-resources}

以下是一些其他资源，可更深入地了解本文档中提到的一些概念。

* [AEM中的Headful和Headless](/help/implementing/developing/headful-headless.md)  — 对AEM中可用的不同交付模型的描述
* [SPA简介和演练。](/help/implementing/developing/hybrid/introduction.md) - AEM中的SPA简介
* [开发SPA for AEM](/help/implementing/developing/hybrid/developing.md)  — 有关如何开发SPA for AEM的准则
* [SPA编辑器概述](/help/implementing/developing/hybrid/editor-overview.md)  — 有关SPA编辑器工作方式的详细信息
* [服务器端渲染](/help/implementing/developing/hybrid/ssr.md)  — 如何为AEM SPA配置SSR
* [SPA参考文档](/help/implementing/developing/hybrid/reference-materials.md)  - JavaScript API引用和指向开源AEM SPA GitHub项目的链接
* [内容片段](/help/assets/content-fragments/content-fragments.md)  — 如何创建内容片段
* [AEM项目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)  - Maven模板，可创建基于最佳实践的、最小的Adobe Experience Manager(AEM)项目，以作为网站的起点
