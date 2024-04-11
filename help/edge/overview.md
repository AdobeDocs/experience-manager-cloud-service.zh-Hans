---
title: Edge Delivery Services 概述
description: 了解 AEM as a Cloud Service 如何从 Edge Delivery Services 提供的性能和优异 Lighthouse 分数中获益。
feature: Edge Delivery Services
exl-id: 03a1aa93-d2e6-4175-9cf3-c7ae25c0d24e
source-git-commit: bf6d0ff2f4aebb6620be46704072743578b096d2
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 48%

---


# Edge Delivery Services 概述 {#edge-delivery-services}

利用 Edge Delivery Services，AEM 能够提供可提高参与和转化的卓越体验。AEM 通过投放可快速创作并开发且极具影响力的体验实现这一点。这是一组可组合的服务，这些服务构成一个快速开发环境，以使作者可快速更新和发布，并且快速推出新站点。因此，借助 Edge Delivery Services，可提高转化率、降低成本并为内容大幅提速。

通过使用 Edge Delivery Services，您可以：

* 快速创建 Lighthouse 分数优异的站点，并通过真实用户监控 (RUM) 持续监控网站性能。
* 通过分离内容来源而提高创作效率。可直接使用 AEM 创作和基于文档的创作。这样即可在同一网站上使用多个内容源。
* 使用一个内置的试验框架，通过该框架，可快速地创建测试、不影响性能地执行测试并快速地发布到测试获胜方的生产环境。

## 概述 {#overview}

Edge Delivery Services是一组可组合的服务，允许您在网站上创作内容的方式具有高度灵活性。 您可以同时使用两者 [AEM内容管理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/getting-started/concepts.html) 和基于AEM的创作，使用 [通用编辑器](/help/sites-cloud/authoring/universal-editor/authoring.md) 以及 [基于文档的创作。](https://www.aem.live/docs/authoring)

下图说明了如何在Microsoft Word（基于文档的创作）中编辑内容以及如何发布到Edge Delivery Services。 它还显示了使用通用编辑器进行的基于AEM的编辑。

![Edge Delivery 架构](assets/AEM-with-EDS-publishing-simple2.png)

您可以直接使用Microsoft Word或Google文档中的内容，以便这些源成为您网站上的页面。 此外，标题、列表、图像、字体元素都可以从初始源转移到网站中。新内容可立即添加，而不经历重建过程。

Edge Delivery Services使用GitHub，因此您可以直接从GitHub存储库管理和部署代码。 例如，您可以在Google文档或Microsoft Word中编写内容，并且可以在GitHub中使用CSS和JavaScript开发站点的功能。 准备就绪后，您可以使用Sidekick浏览器扩展来预览和发布内容更新。

更多信息请参阅 Edge Delivery Services 文档：

* 有关如何开始使用 Edge Delivery 的详细信息，请参阅[“生成”部分](https://www.aem.live/docs/#build)。
* 要了解如何使用 Edge Delivery 创作和发布内容，请参阅[“发布”部分](https://www.aem.live/docs/authoring)。
* 要了解如何正确地启动您的网站项目，请参阅[“启动”部分](https://www.aem.live/docs/#launch)。

## Edge Delivery Services和其他Adobe Experience Cloud产品 {#edge-other-products}

Edge Delivery Services是Adobe Experience Manager的一部分，因此Edge Delivery Services和AEM站点可以共存于同一域中，这是大型网站的常见用例。 此外，Edge Delivery Services中的内容可供AEM Sites页面轻松使用，反之亦然。

请参阅[使用 Edge Delivery Services 进行 AEM 创作的开发人员快速入门指南](/help/edge/aem-authoring/edge-dev-getting-started.md)以了解如何开始您自己要使用 AEM 和 Edge Delivery Services 创作的项目。

您还可以将Edge Delivery Services与 [Adobe Target，](https://www.aem.live/developer/target-integration) [Real User Monitoring (RUM)](https://www.aem.live/developer/rum) 诊断站点的使用情况和性能，以及 [启动。](https://experienceleague.adobe.com/en/docs/experience-platform/tags/home)

## Edge Delivery Services 快速入门 {#getting-started}

通过遵循以下步骤，可以轻松开始使用Edge Delivery Services [快速入门 — 开发人员教程。](https://www.aem.live/developer/tutorial)

## 从 Adobe 获取帮助 {#getting-help}

Adobe 提供三个渠道帮助您使用 Edge Delivery Services：

* 与 [社区资源](#community-resources) 进行一般查询。
* 访问 [产品协作渠道](#collaboration-channel) ，以了解具体问题。
* [记录支持票证](#support-ticket) 解决重大和关键问题。

### 访问社区资源 {#community-resources}

Adobe致力于为您提供最佳社区参与度以及对Edge Delivery Services、基于AEM和基于文档的创作支持。

* 请加入 [Experience League 社区](https://adobe.ly/3Q6kTKl)，从中您可提问、分享反馈、发起讨论、向 Adobe 专家和 AEM 顾问/支持者寻求帮助并实时与志同道合的人交流。
* 加入我们的 [Discord 频道](https://discord.gg/aem-live)，通过这个更休闲的平台可实时互动和快速交流想法。

### 如何访问您的产品协作渠道 {#collaboration-channel}

考虑到与用户直接通信渠道的价值，所有AEM项目在启动时将建立一个Slack渠道，以实现速度、关键更新和体验质量的可扩展报告。 您将从 Adobe 收到一条加入您组织特有的 Slack 频道的邀请。

有关详细信息，请参阅文档 [使用Slack机器人](https://www.aem.live/docs/slack) 以了解更多详细信息。

您可以通过预配置的产品协作渠道与Adobe产品团队互动，回答有关产品使用或最佳实践的问题。 没有通过产品协作渠道与对话相关联的服务级别目标(SLT)。

### 记录支持工单 {#support-ticket}

如果产品问题需要进行额外的调查和疑难解答，并且必须满足响应SLT，则可以使用Admin Console按照以下流程提交支持工单：

1. [按照标准支持流程，](https://experienceleague.adobe.com/?support-tab=home#support) 并创建票证。
1. 在该工单的标题中添加 **Edge Delivery**。
1. 在说明中，除了问题描述外，还提供以下详细信息：

   * 当前网站的 URL。例如：`www.mydomain.com`。
   * 原始网站的 URL (`.hlx` URL)。

## 后续内容 {#whats-next}

通过查看开始使用 [使用Edge Delivery Services。](/help/edge/using.md)
