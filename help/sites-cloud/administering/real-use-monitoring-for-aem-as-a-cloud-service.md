---
title: Real Use Monitoring for AEMas a Cloud Service
description: 了解如何使用实时监控(RUM)实时捕获和分析网站或应用程序的数字用户体验。
exl-id: 91fe9454-3dde-476a-843e-0e64f6f73aaf
source-git-commit: 948eb304c17ad86dcbab2b0685428ae51f38f488
workflow-type: tm+mt
source-wordcount: '1409'
ht-degree: 0%

---

# 适用于AEM的Real Use Monitoring Serviceas a Cloud Service {#real-use-monitoring-service-for-aem-as-a-cloud-service}

>[!NOTE]
>
>我们很高兴地宣布 [GA推出](/help/release-notes/release-notes-cloud/release-notes-current.md#real-use-monitoring) 对于Real Use Monitoring服务，为客户端收集数据。 这是一项自动化服务，无需客户设置。

>[!INFO]
>
>客户端监视仅适用于具有AEM Cloud Service版本的客户 **2024.5.16461** 及更高版本。

## 概述 {#overview}

实时监控(RUM)服务是一种性能监控技术，可实时捕获和分析网站或应用程序的数字用户体验。 它提供了对Web应用程序实时性能的可视性，并提供了对最终用户体验的更深入洞察。 “Real User Monitoring”已更名为“Real Use Monitoring”，因为它更好地反映了服务的真正本质，其侧重于通过监控网站参与而优化性能，而不是用户本身。

使用RUM时，会从启动URL一直跟踪关键性能指标，直到将请求反馈给浏览器，所有这些功能都有助于开发人员增强应用程序，使其易于最终用户使用。

## 谁能从实时监控服务中受益？ {#who-can-benefit-from-rum-service}

Real Use Monitoring服务对所有客户都有好处。 它提供了用户交互的有代表性的反映方式，通过捕获客户端页面查看次数来确保可靠衡量网站参与度。

对于所有Adobe客户，此服务提供了有关用户交互的有价值见解。 使用自己CDN的客户可以从简化的流量报表中受益，因为Adobe现在直接集成了数据收集，从而无需在续订周期期间单独显示报表。

您是否希望使用Adobe的率先采用者RUM Explorer可视化工具来获取有关您网站参与情况的有用见解，从而释放您网站的全部潜力？ 此工具可提供有关页面性能的见解，包括点击次数、核心Web虚拟(CWV)、转化和客户历程图的量度。 通过使用这些强大的见解，您可以优化数字体验以更有效地满足用户的需求。 如果您想了解更多信息并获取访问权限，请发送电子邮件至 `rum-explorer@adobe.com`.

## 了解实际使用情况监控服务的工作方式 {#understand-how-the-rum-service-works}

Adobe Experience Manager使用实时监控(RUM)来帮助客户和Adobe了解访客如何与Adobe Experience Manager站点进行交互、诊断性能问题以及衡量实验的有效性。 RUM通过取样保护访客的隐私 — 仅监控所有页面查看中的一小部分 — 并且不收集任何个人身份信息(PII)。

## Real Use监控服务和隐私 {#rum-service-and-privacy}

Adobe Experience Manager中的实时监控服务旨在保护访客隐私并最大程度地减少数据收集。 作为访客，这意味着您访问的网站不会收集任何个人信息或不会提供Adobe使用。

作为站点操作员，无需其他选择加入即可通过此功能启用监控。 最终用户无需接受额外的弹出窗口或同意表单即可启用RUM。

## Real Use监控服务数据采样 {#rum-service-data-sampling}

传统的Web分析解决方案会尝试收集每位访客的数据。 Adobe Experience Manager的RUM服务仅从一小部分页面查看中捕获信息。 此服务旨在进行取样和匿名处理，而不是取代分析。 默认情况下，页面的取样比率为1:100。 站点操作员此时无法提高或降低采样率。 为了准确估计总流量，每100次页面查看会从1中收集数据，从而为您提供整体流量的可靠近似值。

由于是否按页面查看次数决定是否要收集数据，因此实际上不可能跟踪多个页面上的交互。 从设计角度来看，RUM不了解访客或会话，只了解页面查看次数。

## 正在收集哪些数据 {#what-data-is-being-collected}

Real Use Monitoring服务旨在防止收集个人身份信息。 下面列出了RUM可以收集的整套信息：

* 被访问站点的主机名，例如： `experienceleague.adobe.com`
* 用于显示页面的广泛用户代理类型和操作系统，例如： `desktop:windows` 或 `mobile:ios`
* 数据收集的时间，例如： `2021-06-26 06:00:02.596000 UTC (in order to preserve privacy, we round all minutes to the previous hour, so that only seconds and milliseconds are tracked)`
* 所访问页面的URL，例如： `https://experienceleague.adobe.com/docs`
* 反向链接URL（链接到当前页面的页面的URL，如果用户点击链接）
* 随机生成的页面视图ID，格式类似于： `2Ac6`
* 采样率的加权或反比，例如： `100`. 这意味着仅记录一百分之一的页面查看次数
* 检查点，或加载页面或作为访客与页面交互序列中特定事件的名称
* 用户与上述检查点交互的DOM元素的源或标识符。 例如，这可能是图像
* 针对上述检查点，与用户交互的外部页面或资源的目标或链接。 例如：`https://blog.adobe.com/jp/publish/2022/06/29/media_162fb947c7219d0537cce36adf22315d64fb86e94.png`
* 核心Web虚拟(CWV)性能指标，包括描述访客体验质量的最大内容绘制(LCP)、首次输入延迟(FID)、累积布局偏移(CLS)和到首次字节的时间(TTFB)。

## Real Use监控如何为客户工作 {#how-rum-works-for-a-customer}

Real Use Monitoring可自动监控客户端流量，为您提供有价值的分析。 作为Adobe客户，您无需执行任何其他步骤，因为此服务已无缝集成到您的现有设置中。 通过正式发布(GA)的推出，您将自动从此新功能中受益。

<!-- Alexandru: hiding temporarily, until we figure out where this needs to be linked to 

If you wish to leverage more insights with this new feature to optimize your digital experiences effortlessly, please see here (link to Row 99). -->

## 如何使用实时监控服务数据 {#how-rum-service-data-is-being-used}

RUM数据有利于以下目的：

* 确定并解决客户地点的性能瓶颈
* 简化包括页面查看的自动化流量查找。
* 了解Adobe Experience Manager如何与同一页面上的其他脚本（例如Analytics、Targeting或外部库）进行交互以提高兼容性。

## 限制和了解页面查看次数和性能量度中的差异 {#limitations-and-understanding-variance-in-page-views-and-performance-metrics}

由于您将分析RUM数据，因此页面查看次数和其他性能量度可能存在差异。 这些差异可归因于实时客户端监控固有的几个因素。 以下是客户在解释RUM数据时要牢记的关键注意事项：

1. **跟踪器阻止程序**

   * 最终用户使用跟踪器阻止程序或隐私扩展可能会阻止RUM数据收集，因为这些工具会限制跟踪脚本的执行。 此限制可能会导致报告页面查看次数和用户交互次数不足，从而导致实际网站活动与RUM捕获的数据之间存在差异。

1. **捕获Headless API/JSON调用时的限制**

   * RUM数据服务侧重于客户端体验，目前不捕获从非AEM Headless应用程序发出的后端API或JSON调用。 从RUM服务数据中排除这些调用将会与CDN Analytics测量的内容请求产生差异。

## 常见问题解答 {#faq}


1. **客户能否将RUM服务脚本与Dynatrace等第三方系统集成？**

   是的。

1. **是否正在收集“交互到下一幅绘画”、“第一字节所用时间”和“首次内容绘画”Web虚拟量度？**

   收集到下一绘画的交互(INP)和到第一字节的时间(TTFB)。  此时不收集第一个内容绘制。

1. **此 `/.rum` 我的网站上的路径被阻止，我应该如何修复？**

   此 `/.rum` 需要Path才能使RUM集合正常工作。  如果您的AEMas a Cloud Service中包含的Adobe之前有一个CDN，则您需要确保 `/.rum` 路径将转发到与AEM内容的其余部分相同的AEM源。

1. **RUM收藏集是否计入合同目的的内容请求？**

   RUM库和RUM收藏集都不会计为内容请求，也不会增加报告的页面查看次数或API调用数。 此外，对于将现成CDN与AEMas a Cloud Service结合使用的客户， [服务器端收藏集](#serverside-collection) 是内容请求的基础。

1. **如何选择退出？**

   我们强烈建议使用实时监控(RUM)，因为它具有显着优势，并且可让您优化数字体验。 它可以提供有价值的见解，从而帮助提高网站性能。该服务旨在实现无缝连接，对您网站的性能没有影响。

   选择退出意味着错过这些洞察。 但是，如果您遇到任何问题，请联系Adobe支持。
