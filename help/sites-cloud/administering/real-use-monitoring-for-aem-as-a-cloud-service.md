---
title: AEM as a Cloud Service 的实际使用监控
description: 了解如何使用实际使用监控 （RUM） 实时捕获和分析网站或应用程序的数字用户体验。
exl-id: 91fe9454-3dde-476a-843e-0e64f6f73aaf
feature: Administering
role: Admin
source-git-commit: 8ccef0103ae7fb75171431eeb36f7352f6467d56
workflow-type: tm+mt
source-wordcount: '1302'
ht-degree: 0%

---

# AEM即云服务的实际使用监控服务 {#real-use-monitoring-service-for-aem-as-a-cloud-service}

>[!NOTE]
>
>实际使用监视服务（客户端数据收集）是一种自动化服务。 不需要客户设置。

>[!INFO]
>
>客户端监控仅适用于AEM云服务版本2024.5.16461 **及更高版本的**&#x200B;客户。

## 概述 {#overview}

真实使用监控 （RUM） 服务是一种性能监控技术，可实时捕获和分析网站或应用程序的数字用户体验。 它提供了对 Web 应用程序的实时性能的可见性，并提供了对最终用户体验的更深入洞察。 该服务侧重于通过监控网站参与度而不是用户本身来优化性能。

使用 RUM，从 URL 的启动到将请求服务回浏览器，都会直接跟踪关键性能指标。 它可以帮助开发人员增强应用程序，使其易于最终用户使用。

>[!INFO]
>
>“真实用户监控”已更名为“真实使用监控”，因为它更好地反映了服务的真正本质。

## 谁可以从实际使用的监控服务中受益？ {#who-can-benefit-from-rum-service}

实际使用监控服务对所有客户都有好处。 它提供了用户交互的代表性反映，通过捕获客户端页面浏览量来确保可靠地衡量网站参与度。

对于所有 Adobe 客户，此服务可提供有关用户交互的宝贵见解。 使用自己的 CDN 的客户可以从简化的流量报告中受益，因为 Adobe 现在直接集成了数据收集，从而消除了在续订周期中单独报告的需求。

## 了解实际使用监视服务的工作原理 {#understand-how-the-rum-service-works}

Adobe Experience Manager （AEM） 使用实际使用监控 （RUM） 来帮助客户和 Adobe 了解访问者如何与 AEM 站点交互。 它可以帮助他们诊断性能问题，并衡量实验的有效性。 RUM 通过抽样保护访问者的隐私 - 仅监控所有页面浏览量的一小部分 - 并且不会收集任何个人身份信息 （PII）。

## 真实使用监控服务和隐私 {#rum-service-and-privacy}

AEM 中的实际使用监控服务旨在保护访问者隐私并最大限度地减少数据收集。 作为访问者，这意味着您正在访问或提供给 Adobe 的网站不会收集任何个人信息。

作为站点操作员，无需其他选择加入即可通过此功能启用监视。 最终用户无需接受任何其他弹出窗口或同意表单来启用 RUM。

## 实际使用监控服务数据采样 {#rum-service-data-sampling}

传统的网络分析解决方案试图收集每个访问者的数据。 AEM 的 RUM 服务仅从一小部分页面浏览量中捕获信息。 该服务旨在进行采样和匿名化，而不是替代分析。 默认情况下，页面的采样率为 1：100。 站点运营商目前无法增加或降低采样率。 为了准确估计总流量，每 100 次页面浏览量，都会从 1 次收集数据，从而为您提供总流量的可靠近似值。

作为是否收集数据的决定，它是在逐个页面视图的基础上进行的，并且几乎不可能跟踪跨多个页面的交互。 根据设计，RUM 没有访问者或会话的概念，只有页面浏览量的概念。

## 正在收集哪些数据 {#what-data-is-being-collected}

实际使用监控服务旨在防止收集个人身份信息。 RUM 收集的完整信息如下：

* 正在访问的站点的主机名，例如： `experienceleague.adobe.com`
* 用于显示页面的广泛用户代理类型和操作系统，例如： `desktop:windows` 或 `mobile:ios`
* 数据收集的时间，例如： `2021-06-26 06:00:02.596000 UTC (in order to preserve privacy, we round all minutes to the previous hour, so that only seconds and milliseconds are tracked)`
* 正在访问的页面的 URL，例如： `https://experienceleague.adobe.com/docs`
* 引荐来源网址（如果用户点击了链接，则为链接到当前页面的网页的网址）
* 随机生成的页面视图 ID，格式类似于： `2Ac6`
* 采样率的权重或反数，例如： `100`这意味着只记录了一百个页面浏览量中的一个
* 加载页面序列中特定事件的检查点或名称。 或者，作为访客与之交互
* 用户为上述检查点与之交互的 DOM 元素的源或标识符。 例如，它可以是一个图像
* 目标，或链接到用户为上述检查点与之交互的外部页面或资源。 例如：`https://blog.adobe.com/jp/publish/2022/06/29/media_162fb947c7219d0537cce36adf22315d64fb86e94.png`
* 核心 Web 指标 （CWV） 性能指标，包括描述访问者体验质量的最大内容绘制 （LCP）、首次输入延迟 （FID）、累积布局偏移 （CLS） 和到达第一个字节的时间 （TTFB）。

## 实际使用监视如何为客户工作 {#how-rum-works-for-a-customer}

实际使用监控会自动监控客户端流量，为您提供有价值的见解。 作为 Adobe 客户，您无需执行任何其他步骤，因为此服务已无缝集成到您的现有设置中。 随着正式发布 （GA） 推出，您将自动受益于此新功能。

<!-- Alexandru: hiding temporarily, until we figure out where this needs to be linked to 

If you wish to leverage more insights with this new feature to optimize your digital experiences effortlessly, please see here (link to Row 99). -->

## 如何使用实际使用监视服务数据 {#how-rum-service-data-is-being-used}

RUM 数据可用于以下目的：

* 识别并修复客户站点的性能瓶颈
* 简化包含页面浏览量的自动流量查找。
* 了解AEM如何与同一页面上的其他脚本（例如分析、定位或外部库）进行交互，以提高兼容性。

## 限制和了解页面浏览量和效果指标的差异 {#limitations-and-understanding-variance-in-page-views-and-performance-metrics}

在分析 RUM 数据时，页面浏览量和其他性能指标可能存在差异。 这些差异可归因于实时客户端监视中固有的几个因素。 以下是客户在解释其 RUM 数据时要牢记的关键注意事项：

1. **跟踪器拦截器**

   * 使用跟踪器阻止程序或隐私扩展的最终用户可能会阻碍 RUM 数据收集，因为这些工具会限制跟踪脚本的执行。 此限制可能会导致页面浏览量和用户交互报告不足，从而在实际网站活动与 RUM 捕获的数据之间造成差异。

1. **捕获无外设 API/JSON 调用时的限制**

   * RUM 数据服务专注于客户端体验，目前不捕获从非 AEM 无头应用程序进行的后端 API 或 JSON 调用。 从 RUM 服务数据中排除这些调用会产生与 CDN Analytics 测量的内容请求的差异。

## 常见问题解答 {#faq}


1. **客户能否将 RUM 服务脚本与第三方系统（如 Dynatrace）集成？**

   是的。

1. **是否正在收集“与下一个绘制的交互”、“到第一个字节的时间”和“第一个内容绘制”Web 指标？**

   收集与下一个绘画的交互 （INP） 和到第一个字节的时间 （TTFB）。  此时不会收集第一个内容丰富的绘画。

1. **`/.rum`该路径在我的网站上被阻止，我应该如何解决？**

   该 `/.rum` 路径是 RUM 收集工作所必需的。 如果您在 Adobe 作为 AEM 即云服务的一部分提供的内容前面有一个 CDN，请确保该 `/.rum` 路径转发到与其余 AEM 内容相同的 AEM 源。 并且，请确保不以任何方式对其进行调整。

1. **RUM 收集是否计入用于合同目的的内容请求？**

   RUM 库和 RUM 集合不算作内容请求，也不会增加报告的页面浏览量或 API 调用数。 此外，对于将开箱即用的 CDN 与 AEM 作为云服务结合使用的客户来说， [服务器端收集](#serverside-collection) 是内容请求的基础。

1. **如何选择退出？**

   Adobe 建议使用真实使用监控 （RUM），因为它具有显著的优势，并且可以让您优化数字体验。 它可以提供有价值的见解，有助于提高网站性能。 该服务设计为无缝的，对您网站的性能没有影响。

   选择退出意味着错过这些见解。 但是，如果您遇到任何问题，请联系 Adobe 支持部门。
