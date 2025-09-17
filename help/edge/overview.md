---
title: Edge Delivery Services 概述
description: 了解 AEM as a Cloud Service 如何从 Edge Delivery Services 提供的性能和优异 Lighthouse 分数中获益。
feature: Edge Delivery Services
exl-id: 03a1aa93-d2e6-4175-9cf3-c7ae25c0d24e
role: Admin, Architect, Developer
source-git-commit: 8cbcfbc074c69396980ba930339563d5437d5f17
workflow-type: tm+mt
source-wordcount: '988'
ht-degree: 94%

---


# Edge Delivery Services 概述 {#edge-delivery-services}

>[!TIP]
>
>**想立即亲身体验吗？**
>
>如果要立即动手使用Edge Delivery Services，您有两个选项。
>* [使用预建的教程环境立即开始创作 — 已完全配置并准备就绪。](https://www.aem.live/developer/ue-trial)
>* 通过[在aem.live上查看教程，了解更多详细信息并在30分钟内设置您自己的环境。](https://www.aem.live/developer/ue-tutorial)

## 什么是 Edge Delivery Services？ {#what-is-edge}

Edge Delivery Services 是一套现代化内容传递框架，重新定义了网站的构建与传递方式，旨在优化速度、简化流程，并实现高度可扩展性。它是 Adobe Experience Manager 的核心组成部分，通过将渲染和传递推向网络边缘，更贴近用户，从而加快数字体验的响应速度。

它并非用来取代内容传递网络（CDN），而是可无缝集成至您现有的 CDN，或使用 [Adobe 提供的托管 CDN](/help/implementing/dispatcher/cdn.md)。

## 为何选择 Edge Delivery Services？ {#why-edge}

### 提升可发现性与流量 {#increase-traffic}

Edge Delivery 构建的网站经过搜索引擎优化（SEO）及大型语言模型生成式引擎优化（GEO）。这可确保网站在现有及未来的自然流量来源中具备高度可见性与可发现性。**以性能为优先的端到端架构**&#x200B;确保出色的客户体验，从而有效提升用户参与度。

### 开发效率提升 {#developer-efficientcy}

上线周期从数月甚至数年缩短至数天或数周！Edge Delivery 提供&#x200B;**现代网页开发者**&#x200B;喜爱的全套工具：包括 GitHub、本地开发支持自动重新加载、高性能、简洁性，并摒除所有复杂性——无需转译、无需打包器、无需配置，也没有额外负担。

Edge Delivery 的简洁性无需依赖复杂的框架、工具或流程，非常适合 AI 代码生成。使用纯 HTML、现代 CSS 和原生 JavaScript，即可更快速地构建卓越的用户体验。专注于实际工作，减少花在培训和学习新工具上所花的时间。

借助 Edge Delivery，每位开发者都能轻松实现 Lighthouse 评分满分 100 分。

### 支持多种内容来源 {#multiple-content-sources}

来自多种解决方案的内容可直接与 Edge Delivery 集成，**包括您现有的所有 AEM 实例**。内容创作者可使用他们熟悉的工具（如 SharePoint）**从任意系统中管理并发布内容至 Edge Delivery**，从而加快内容交付速度。

### 可组合架构 {#composable-architeture}

无论是无头架构还是传统架构，您都可以以合适的格式交付合适的内容，并添加恰当的呈现效果，让内容在任意渠道中脱颖而出，打造出众的体验。

## 它的运作方式 {#how-does-it-work}

Edge Delivery Services 是一组可组合的服务组件，可为网站内容创作方式提供高度灵活性。它以多云 SaaS 解决方案和纯前端开发方式，取代了 AEM Publish / Dispatcher 以及传统基于 AEM Core Components 的体验构建方式。

![Edge Delivery 架构](assets/aem-with-eds-architecture.png)

Edge Delivery Services 使用 GitHub，因此您可直接从您的 GitHub 存储库管理和部署代码。新内容可立即添加，而不经过重建过程。

## 创作 {#authoring}

### 上下文编辑 {#in-context-editing}

[通用编辑器](/help/implementing/universal-editor/introduction.md)是一款所见即所得（WYSIWYG）的可自定义编辑器，提供一站式内容实时编辑与视觉预览体验，支持在上下文中直接进行内容修改。

* 结合 AEM 内容创作功能与通用编辑器，无论采用无头架构或传统架构，均可显著提升内容创作者的工作效率。
* 您可以充分利用 AEM 全面的内容管理能力，包括工作流与治理机制。
* 您可以利用众多扩展点来支持自有流程与系统集成需求。
* 您可以通过在 GitHub 中使用 CSS 和 JavaScript 来开发网站功能。

![使用通用编辑器进行 AEM 创作](assets/wysiwyg-authoring.png)

### 基于文档的编辑 {#document-based-editing}

[另一种方式是基于文档的内容创作](https://www.aem.live/docs/authoring)，即以文档形式管理内容。Microsoft Word 是一种广受欢迎的选择，因为许多企业已部署 SharePoint，初始内容通常便是在其中创建的。无需学习新工具，直接从 SharePoint 和 Word 发布内容，可省去将内容复制粘贴到 AEM 的繁琐步骤。未使用 SharePoint 的客户也可选择使用 Google Drive 作为替代方案。

## 运营遥测 {#telemetry}

Adobe Experience Manager 使用[运营遥测](https://www.aem.live/docs/operational-telemetry)功能收集运营数据，仅用于发现并解决基于 Adobe Experience Manager 构建的网站中的功能与性能问题。运营遥测数据可用于诊断性能问题，并评估试验的有效性。运营遥测通过[采样](https://www.aem.live/docs/operational-telemetry#operational-telemetry-data-is-sampled)（仅监测所有页面浏览量的一小部分）以及[严格排除可识别个人身份的信息](https://www.aem.live/docs/operational-telemetry#what-data-is-being-collected)（PII），以保障访客隐私。

## 开始探索 {#start-exploring}

开始使用 AEM 内容创作功能、通用编辑器与 Edge Delivery Services：

* Edge Delivery Services 文档 [Edge Delivery Services](https://www.aem.live)
* 有关使用通用编辑器进行 AEM 创作的概述，请参阅 aem.live 文档中的文档[为 Edge Delivery Services 进行 AEM 创作](https://www.aem.live/docs/aem-authoring)。
* 有关开发人员概述，请参阅 aem.live 文档中的文档[快速入门 - 通用编辑器开发人员教程](https://www.aem.live/developer/ue-tutorial)。

## Edge Delivery Services 和其他 Adobe Experience Cloud 产品 {#edge-other-products}

Edge Delivery Services 是 Adobe Experience Manager 的一部分。因此，Edge Delivery Services 和 AEM Sites 可以在同一个域中共存，这是大型网站的常见用例。此外，您的 AEM Sites 页面可以无缝使用来自 Edge Delivery Services 的内容，反之亦然。

您也可以将 Edge Delivery Services 与 [Adobe Target](https://www.aem.live/developer/target-integration) 和 [Adobe Launch](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/tags/home) 搭配使用。

## 从 Adobe 获取帮助 {#getting-help}

Adobe 提供三大层级支持，助您充分运用 Edge Delivery Services：

* 利用[社区资源](#community-resources)进行一般查询。
* 访问您的[产品协作渠道](#collaboration-channel)以解决特定问题。
* [提交支持工单](#support-ticket)，以&#x200B;**在合同支持服务级别协议（SLA）范围内**&#x200B;解决重大和严重问题。

### 访问社区资源 {#community-resources}

Adobe 致力于为您提供最佳社区参与度以及有关 Edge Delivery Services、用通用编辑器进行 AEM 创作以及基于文档的创作的大力支持。

* 请在[Experience League 社区](https://adobe.ly/3Q6kTKl)参与提问、分享反馈、发起讨论、向 Adobe 专家和 AEM 顾问/支持者寻求帮助并实时与志同道合的人交流。
* 加入[Discord 频道](https://discord.gg/aem-live)，通过这个更休闲的平台可实时互动和快速交流想法。

### 提交支持工单 {#support-ticket}

{{support-ticket}}
