---
title: AEM和Edge Delivery Services
description: 了解AEMas a Cloud Service如何从Edge Delivery Services提供的性能和完美的Lighthouse分数中获益。
feature: Edge Delivery Services
exl-id: 03a1aa93-d2e6-4175-9cf3-c7ae25c0d24e
source-git-commit: 9d26a4835dc331f2ff8b741a4c14847ead611874
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 50%

---


# AEM和Edge Delivery Services {#aem-edge}

利用 Edge Delivery Services，AEM 能够提供可提高参与和转化的卓越体验。AEM 通过投放可快速创作并开发且极具影响力的体验实现这一点。这是一组可组合的服务，这些服务构成一个快速开发环境，以使作者可快速更新和发布，并且快速推出新站点。因此，借助 Edge Delivery Services，可提高转化率、降低成本并为内容大幅提速。

通过使用Edge Delivery Services，您可以：

* 快速创建 Lighthouse 分数优异的站点，并通过真实用户监控 (RUM) 持续监控网站性能。
* 通过分离内容来源而提高创作效率。可直接使用 AEM 创作和基于文档的创作。这样即可在同一网站上使用多个内容源。
* 使用一个内置的试验框架，通过该框架，可快速地创建测试、不影响性能地执行测试并快速地发布到测试获胜方的生产环境。

## Edge Delivery Services概述 {#edge-overview}

下图说明了如何在Microsoft Word（基于文档的编辑）中编辑内容以及如何发布到Edge Delivery Services。 它还显示了使用通用编辑器的AEM发布方法。

![Edge Delivery 架构](assets/AEM-with-EDS-publishing-simple2.png)

Edge Delivery Services是一组可组合的服务，允许您在网站上创作内容的方式具有高度灵活性。 如前所述，您可以使用两者 [AEM内容管理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/getting-started/concepts.html) 替换为 [通用编辑器创作](/help/implementing/universal-editor/introduction.md) 以及 [基于文档的创作。](https://www.aem.live/docs/authoring)

例如，您可以直接从 Microsoft Word 或 Google Docs 中使用内容。这意味着来自这些来源的文档可成为您网站上的页面。此外，标题、列表、图像、字体元素都可以从初始源转移到网站中。新内容可立即添加，而不经历重建过程。

Edge Delivery Services使用GitHub，因此客户可以直接从其GitHub存储库管理和部署代码。 例如，您可以在Google文档或Microsoft Word中编写内容，并且可以在GitHub中使用CSS和JavaScript开发站点的功能。 当您就绪时，您即可使用 Sidekick 浏览器扩展预览和发布内容更新。

进一步阅读Edge Delivery Services文档：

* 有关如何开始使用Edge Delivery的详细信息，请参阅 [生成部分。](https://www.aem.live/docs/#build)
* 要了解如何使用Edge Delivery创作和发布内容，请参阅 [发布部分。](https://www.aem.live/docs/authoring)
* 要了解如何正确启动您的网站项目，请参阅 [Launch部分。](https://www.aem.live/docs/#launch)

## Edge Delivery Services和其他Adobe Experience Cloud产品 {#edge-other-products}

Edge Delivery Services是Adobe Experience Manager的一部分，因此Edge Delivery Services和AEM站点可以共存于同一域中。 这是大型网站的常见用例。此外，Edge Delivery Services中的内容还可以轻松地在AEM Sites页面中消费或反之。

您还可以将 Edge Delivery Services 与 Adobe Target、Analytics 和 Launch 结合使用。

## 获取对 Edge Delivery Services 的访问权限 {#getting-access}

快速入门 Edge Delivery Services 十分容易。要开始操作，请遵循 [快速入门 — 开发人员教程。](https://www.aem.live/developer/tutorial)

## 从 Adobe 获取帮助 {#adobe-gethelp}

您可以通过由您提供的产品协作渠道与 Adobe 产品团队联系（有关访问详情，请参阅下文）以回答有关产品使用或最佳实践的疑问。没有服务水平目标 (SLT) 与通过该产品协作渠道进行的对话关联。如果产品问题需要进行额外的调查和疑难解答，并且必须满足响应SLT，则可以按照以下说明提交支持工单 [支持流程。](https://experienceleague.adobe.com/?support-tab=home#support)

Adobe 提供三个渠道帮助您使用 Edge Delivery Services：

* 利用社区资源进行一般查询
* 访问您的产品协作渠道以解决特定问题
* 记录支持工单以解决重大和关键问题

### 访问社区资源 {#community-resource}

Adobe致力于为您提供最佳社区参与以及对Edge Delivery Services和基于文档的创作支持。

* 参与 [Experience League社区](https://adobe.ly/3Q6kTKl) 提出问题、分享反馈、发起讨论、向Adobe专家和AEM顾问/Champs寻求帮助，以及实时与想法相似的个人保持联系。
* 加入我们的 [不和谐的频道，](https://discord.gg/aem-live) 一个更休闲的实时互动和快速创意交流平台。

### 如何访问您的产品协作渠道 {#collab-channel}

鉴于与客户直接沟通渠道的价值，所有AEM客户在发布时将建立一个Slack渠道，以实现速度、关键更新和体验质量的可扩展报告。 您会从 Adobe 收到一条加入您组织特有的 Slack 频道的邀请。

有关更多信息，请参阅[使用 Slack 机器人](https://www.aem.live/docs/slack)文档。

### 记录支持工单 {#support-ticket}

通过 Admin Console 记录支持工单的步骤：

1. [按照标准支持流程，](https://experienceleague.adobe.com/?support-tab=home#support) 创建票证。
1. 在该工单的标题中添加 **Edge Delivery**。
1. 请在描述中提供以下详细信息：

   * 当前网站的 URL。例如：`www.mydomain.com`。
   * 原始网站的URL (`.hlx` URL)。

## 后续内容 {#whats-next}

首先，请查看[使用 Edge Delivery Services](/help/edge/using.md)。
