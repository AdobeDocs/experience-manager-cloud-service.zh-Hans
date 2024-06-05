---
title: 了解 CMS Headless 开发
description: 在 AEM Headless 开发人员历程的这一部分中，了解 Headless 技术以及使用它的原因。
exl-id: 8c1fcaf7-1551-4133-b363-6f50af681661
solution: Experience Manager
feature: Headless
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '1626'
ht-degree: 100%

---

# 了解 CMS Headless 开发 {#learn-about}

在 [AEM Headless 开发人员历程](overview.md)的这一部分中，了解 Headless 技术以及使用它的原因。

## 目标 {#objective}

本文档可帮助您了解 Headless 内容交付以及应使用它的原因。阅读本文档后，您应：

* 了解 Headless 内容交付的基本概念和术语。
* 了解为什么需要以及何时需要 Headless
* 从较高层面了解如何使用 Headless 概念以及如何将它们相互关联

## 全栈内容交付 {#full-stack}

自易于使用的大型内容管理系统 (CMS) 兴起以来，组织便已将其用作管理消息、品牌化和通信的中心位置。通过将 CMS 用作管理体验的中心点，消除了在不同的系统中重复任务的需求，从而提高了效率。

![经典全栈 CMS](assets/full-stack.png)

在全栈 CMS 中，用于操作内容的功能在 CMS 中。该系统的各种功能构成了 CMS 堆栈的不同组件。全栈解决方案有许多优点。

* 您需要维护一个系统。
* 集中管理内容。
* 系统的所有服务都是集成的。
* 内容创作是无缝进行的。

因此，如果您想添加一个新渠道或支持新类型的体验，可以将一个（或多个）新组件插入堆栈中，并且您只能在一个位置进行更改。

![向堆栈添加新渠道](assets/adding-channel.png)

当您发现堆栈中的其他项目可能需要调整才能适应更改时，堆栈中依赖项的复杂性很快就会变得明显。

## 全栈交付的限制 {#limits}

全栈方法本身会创建一个容器，所有体验都集中在一个系统中。对容器的一个组件进行更改或添加需要更改其他组件，这可能会使更改成为一项耗时且成本高昂的工作。

对于呈现系统尤为如此，在传统设置中，该系统通常已密切捆绑到 CMS。通常，任何新渠道意味着对呈现系统的更新，这会影响所有其他渠道。

![在将渠道添加到堆栈时，复杂性将增加](assets/presentation-complexity.png)

当您花费更多精力来协调堆栈的所有组件的更改时，此天然容器的限制就会变得明显。

无论平台或接触点如何，用户都应参与其中，这就要求您灵活地运用交付体验的方式。此多渠道方法是数字体验的标准，而全栈方法已被证实在某些情况下是不可改变的。

## Headless 中的头 {#the-head}

任何系统的头通常都是该系统的输出呈现器，通常采用 GUI 或其他图形输出的形式。

例如，Headless 服务器可能位于服务器机房某处的机架中，并且未连接监视器。要访问该服务器，您必须远程连接到它。在此情况下，监视器是头，因为它负责呈现服务器的输出。作为服务消费者，您在远程连接到服务器时提供自己的头（监视器）。

就 Headless CMS 而言，CMS 将管理内容并继续将内容交付给消费者。但是，通过仅以标准化方式交付&#x200B;**内容**，Headless CMS 会省略最终的输出呈现，而只保留要&#x200B;**呈现**&#x200B;给消费服务的内容。

![Headless CMS](assets/headless-cms.png)

消费服务，无论是 AR 体验、网上商店、移动体验、渐进式 Web 应用程序 (PWA) 等，都从 Headless CMS 摄入内容并提供其自己的呈现方式。它们负责为您的内容提供它们自己的头。

忽略头将消除复杂性，从而简化 CMS。这样做还会将呈现内容的责任转移到实际需要内容且通常更适合此类呈现的服务。

## 分离 {#decoupling}

通过公开一组可靠且灵活的应用程序编程接口 (API) 来供所有体验使用，可以实施 Headless 交付。API 充当服务之间的通用语言，通过标准化内容交付在内容级别将它们捆绑起来，但允许它们灵活地实施自己的解决方案。

Headless 是从内容的呈现中分离内容的示例。或者，从更通用的意义上讲，将前端与服务堆栈的后端分离。在 Headless 设置中，呈现系统（头）与内容管理（尾）分离。两者仅通过 API 调用进行交互。

此分离意味着每个消费服务（前端）都可以基于通过 API 交付的相同内容来构建自己的体验，从而确保内容可重用且一致。之后，消费服务可以实施自己的呈现系统，从而使内容管理堆栈（后端）能够轻松地水平扩展。

## 技术基础 {#technology}

Headless 方法让您构建一个技术堆栈，从而轻松快速地适应未来的数字体验需求。

过去的适用于 CMS 的 API 通常基于 REST。代表性状态传输 (REST) 采用无状态方式以文本形式提供资源。这允许使用一组预定义的操作来读取和修改资源。通过确保内容的无状态表示形式，REST 允许各种 Web 服务之间进行良好的互操作。

仍然需要可靠的 REST API。不过，REST 请求可能大而冗长。如果您的多个消费者对您所有的渠道进行 REST 调用，那么这种冗长的情况就会加重，性能也会受到影响。

Headless 内容交付通常会使用 GraphQL API。GraphQL 既允许类似的无状态传输，又允许更有针对性的查询，从而减少所需查询的总数并提高性能。通常会看到混合使用 REST 和 GraphQL 的解决方案，基本上是选择最适用于手头工作的工具。

无论您选择哪个 API，都可以通过定义基于通用 API 的 Headless 系统，来利用最新的浏览器和其他 Web 技术（例如，渐进式 Web 应用程序 (PWA)）。API 会创建一个易于扩展且适应性强的标准接口。

通常，内容在客户端上呈现。这通常意味着，某人在移动设备上调用您的内容，您的 CMS 将交付内容，然后移动设备（客户端）负责呈现您提供的内容。如果设备较旧或速度较慢，您的数字体验也会较慢。

将内容与呈现分离意味着可以更好地控制此类客户端性能问题。服务器端呈现 (SSR) 将呈现内容的责任从客户端浏览器转交到了服务器。这使您（作为内容提供者）能够在需要时向受众提供一定程度的有保障的性能。

## 组织挑战 {#organization}

Headless 展示了交付数字体验方面的灵活度。但这种灵活度本身也带来了挑战。

拥有许多不同的渠道可能意味着它们均有自己的呈现系统。尽管它们通过相同的 API 使用相同内容，但由于呈现方式不同，体验可能会有所不同。必须给予关注以确保客户体验的一致性。

通过实施精心设计的系统、共享模式库、使用可重用的设计组件以及已建立的开放式客户端框架，可以确保提供一致体验，但必须规划这些工作。

## 未来是 Headless，未来即在眼前 {#future}

数字体验将继续定义品牌与客户互动的方式。Headless 设计令人兴奋的地方在于，它使我们能够灵活地响应不断变化的客户期望。

虽然未来是无法预测的，但 Headless 可让您灵活地应对未来发生的一切。

## AEM 和 Headless {#aem-and-headless}

在您继续此开发人员历程时，您将了解 AEM 如何支持 Headless 投放及其全栈投放功能。

作为数字体验管理领域的行业领导者，Adobe 意识到应对体验创建者所面临的实际挑战的理想解决方案很少是一个二选一的选择。正因为这一点，AEM 不仅支持这两个模型，而且唯一允许将两者无缝混合（融合 Headless 和全栈的优势）来帮助您向内容消费者提供最出色的服务，而无论他们身在何处。

此历程专注于仅限 Headless 的内容交付模型。不过，在您掌握这些基础知识后，便能进一步探究如何发挥这两个模型的力量。

## 后续内容 {#what-is-next}

感谢您开始 AEM Headless 历程！现在您已阅读本文档，您应：

* 了解 Headless 内容交付的基本概念和术语。
* 了解为什么需要以及何时需要 Headless。
* 从较高层面了解如何使用 Headless 概念以及如何将它们相互关联。

在此知识的基础上继续您的 AEM Headless 历程，接下来查看文档 [AEM Headless as a Cloud Service 快速入门](getting-started.md)，其中您将了解如何设置必要的工具以及如何开始考虑 AEM 处理 Headless 内容投放的方式及其先决条件。

## 其他资源 {#additional-resources}

我们建议您查看文档 [AEM Headless as a Cloud Service 快速入门](getting-started.md)来继续 Headless 开发历程的下一部分，以下是一些其他可选资源，这些资源对本文档中提到的一些概念进行了更深入的探究，但并非继续 Headless 历程所必需的。

* [Adobe Experience Manager as a Cloud Service 的架构简介](/help/overview/architecture.md) – 了解 AEM as a Cloud Service 的结构
* [AEM as a Headless CMS 简介](/help/headless/introduction.md)
* [AEM 开发人员门户](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=zh-Hans)
* [AEM Headless 教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=zh-Hans) – 使用这些动手实践教程探索如何使用通过 AEM 将内容投放到 Headless 端点的各种选项并选择适合您的选项。
