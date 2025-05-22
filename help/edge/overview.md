---
title: Edge Delivery Services 概述
description: 了解 AEM as a Cloud Service 如何从 Edge Delivery Services 提供的性能和优异 Lighthouse 分数中获益。
feature: Edge Delivery Services
exl-id: 03a1aa93-d2e6-4175-9cf3-c7ae25c0d24e
role: Admin, Architect, Developer
source-git-commit: bf0e840fb3cd1ea5bc832823c522415c066f0018
workflow-type: ht
source-wordcount: '1286'
ht-degree: 100%

---


# Edge Delivery Services 概述 {#edge-delivery-services}

利用 Edge Delivery Services，AEM 能够提供可提高参与和转化的卓越体验。AEM 通过投放可快速创作并开发且极具影响力的体验实现这一点。这是一组可组合的服务，这些服务构成一个快速开发环境，以使作者可快速更新和发布，并且快速推出新站点。因此，借助 Edge Delivery Services，可提高转化率、降低成本并为内容大幅提速。

通过使用 Edge Delivery Services，您可以：

* 快速创建 Lighthouse 分数优异的网站，并通过实际使用监控 (RUM) 持续监控网站性能。
* 通过分离内容来源而提高创作效率。开箱即用，您可以使用通用编辑器进行 AEM 创作，也可以使用基于文档的创作。这样即可在同一网站上使用多个内容源。
* 使用一个内置的试验框架，通过该框架，可快速地创建测试、不影响性能地执行测试并快速地发布到测试获胜方的生产环境。

## 敏捷响应业务需求 {#agile-reaction}

作为长期公认的行业领导者，Adobe 知道能够为客户快速创建和发布新的、有意义的内容是多么重要。市场已经明确了扩大内容创作规模所面临的常见挑战，包括：

1. **对内容的需求持续增长。**
   * 需要培养新的内容作者来满足这一需求。
   * 内容创建过程必须在整个业务范围内有效扩展。
   * 作者必须能够对不断变化的趋势做出快速反应。
1. **需要全渠道内容。**
   * 无论内容传递如何，都需要布局控制。
   * 作者需要被授权直接更改内容布局。
1. **提高内容投资回报率的压力越来越大。**
   * 作者本身需要有优化自己创作的内容的能力。

事实证明，这些趋势在整个行业都是一致的。但是，每个项目的个体要求必然会有所不同。任何 Edge Delivery Services 项目的目标都是专注于找到适合您的用户的解决方案。

1. **注重价值而不是功能。** - 确定最优化的工作流程来为您的作者服务，而不是迷失在 AEM 的扩展功能集中。
1. **充分利用 AEM 的灵活性。** - AEM 功能不需要在真空中使用。根据用例使用您需要的功能。
1. **利用作者的专业知识。** - 从一开始就让真正的内容作者参与到项目中，以确保通过实现合理的功能来提供他们所需的价值。

通过关注作者的价值，您的 Edge Delivery Services 项目可以满足内容创建者面临的现代行业需求，并快速提供内容以取悦您的客户。

## 为内容创作者提供灵活的创作工具 {#overview}

Edge Delivery Services 是一组可组合的服务，通过这些服务，可非常灵活地在网站上创作内容。您既可以使用[通用编辑器](/help/sites-cloud/authoring/universal-editor/authoring.md)进行 [AEM 内容管理](/help/sites-cloud/authoring/author-publish.md)和内容创作，也可以使用[基于文档的创作。](https://www.aem.live/docs/authoring)

下图展示了如何在 Microsoft Word（基于文档的创作）中编辑内容并将其发布到 Edge Delivery Services，以及如何使用通用编辑器进行 AEM 内容创作。

![Edge Delivery 架构](assets/AEM-with-EDS-publishing-simple2.png)

Edge Delivery Services 使用 GitHub，因此您可直接从您的 GitHub 存储库管理和部署代码。新内容可立即添加，而不经过重建过程。

### 基于文档的创作 {#document-based}

通过基于文档的创作，您可以直接使用 Microsoft Word 或 Google Docs 中的内容，以便这些来源成为您网站上的页面。此外，标题、列表、图像、字体元素都可以从初始源转移到网站中。

* 通过基于文档的创作，每个营销人员都可以使用已知的创作工具（Microsoft Word, Google Docs 等）快速创建内容。
* 通过允许直接在源文档中创作、审查和发布，简化了内容创建。
* 由于使用已知工具，内容作者无需任何入职培训，从而提高了内容速度。
* 您可以使用 GitHub 中的 CSS 和 JavaScript 开发您网站的功能。

![基于文档的创作](assets/document-based-authoring.png)

基于文档的创作文档中的进一步阅读内容：

* 有关如何开始使用 Edge Delivery 的详细信息，请参阅 [aem.live 文档的“构建”部分。](https://www.aem.live/docs/#build)
* 要了解如何使用 Edge Delivery 创作和发布内容，请参阅 [aem.live 文档的“发布”部分。](https://www.aem.live/docs/authoring)
* 要了解如何正确启动您的网站项目，请参阅 [aem.live 文档的“启动”部分](https://www.aem.live/docs/#launch)

### 使用通用编辑器进行 AEM 创作{#wysiwyg-authoring}

通用编辑器是一个所见即所得 (WYSIWYG) 的可自定义的一站式场所，可通过视觉预览在上下文中实时编辑内容。

* 使用通用编辑器进行 AEM 创作，您可以提高创作效率，无论是无头还是有头创作。
* 您可以利用 AEM 全面的内容管理功能，包括工作流程和治理。
* 利用众多扩展点来支持您自己的流程和集成。
* 您可以使用 GitHub 中的 CSS 和 JavaScript 开发您网站的功能。

![使用通用编辑器进行 AEM 创作](assets/wysiwyg-authoring.png)

开始使用通用编辑器和 Edge Delivery Services 进行 AEM 创作：

* 有关使用通用编辑器进行 AEM 创作的概述，请参阅 aem.live 文档中的文档[为 Edge Delivery Services 进行 AEM 创作](https://www.aem.live/docs/aem-authoring)。
* 有关开发人员概述，请参阅 aem.live 文档中的文档[快速入门 - 通用编辑器开发人员教程](https://www.aem.live/developer/ue-tutorial)。

### 决定你的创作方法 {#authoring-method}

AEM 的灵活性可确保满足您的创作需求。Adobe 可以帮助您确定最适合您要求的方法。

* 始终让内容作者参与决策。
* 可以实现多种创作方法。
* 事后您可以随时改变您的创作方法。
* 您不需要在实施之前做出决定，而应该将其作为实施的一部分。

## Edge Delivery Services 和其他 Adobe Experience Cloud 产品 {#edge-other-products}

Edge Delivery Services 是 Adobe Experience Manager 的一部分。因此，Edge Delivery Services 和 AEM Sites 可以在同一个域中共存，这是大型网站的常见用例。此外，您的 AEM Sites 页面可以无缝使用来自 Edge Delivery Services 的内容，反之亦然。

请参阅 aem.live 文档中的文档[快速入门 - 通用编辑器开发人员教程](https://www.aem.live/developer/ue-tutorial)，了解如何使用 AEM 和 Edge Delivery Services 启动您自己的项目进行创作。

您还可以将 Edge Delivery Services 与 [Adobe Target](https://www.aem.live/developer/target-integration)、[实际使用监控 (RUM)](https://www.aem.live/developer/rum) 结合使用，以诊断网站的使用情况和性能，还可以与[启动](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/tags/home)结合使用。

## 从 Adobe 获取帮助 {#getting-help}

Adobe 提供三个渠道帮助您使用 Edge Delivery Services：

* 利用[社区资源](#community-resources)进行一般查询。
* 访问您的[产品协作渠道](#collaboration-channel)以解决特定问题。
* [记录支持工单以](#support-ticket)解决重大和关键问题。

### 访问社区资源 {#community-resources}

Adobe 致力于为您提供最佳社区参与度以及有关 Edge Delivery Services、用通用编辑器进行 AEM 创作以及基于文档的创作的大力支持。

* 请在[Experience League 社区](https://adobe.ly/3Q6kTKl)参与提问、分享反馈、发起讨论、向 Adobe 专家和 AEM 顾问/支持者寻求帮助并实时与志同道合的人交流。
* 加入[Discord 频道](https://discord.gg/aem-live)，通过这个更休闲的平台可实时互动和快速交流想法。

### 如何访问您的产品协作渠道 {#collaboration-channel}

考虑到与用户建立的直接沟通渠道的作用，所有 AEM 项目都将在启动时建立一个 Slack 频道以快速获得关键更新和针对体验质量的大规模报告。您会从 Adobe 收到一条加入您组织特有的 Slack 频道的邀请。

有关更多信息，请参阅[使用 Slack 机器人](https://www.aem.live/docs/slack)文档。

您可以通过已配置的产品协作渠道与 Adobe 产品团队互动，回答有关产品使用或最佳实践的问题。没有服务水平目标 (SLT) 与通过该产品协作渠道进行的对话关联。

### 记录支持工单 {#support-ticket}

{{support-ticket}}
