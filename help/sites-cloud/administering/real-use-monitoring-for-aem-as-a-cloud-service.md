---
title: AEM as a Cloud Service 的实际使用监控
description: 了解如何使用实时监控(RUM)实时捕获和分析网站或应用程序的数字用户体验。
exl-id: 91fe9454-3dde-476a-843e-0e64f6f73aaf
feature: Administering
role: Admin
source-git-commit: c0b86950e36b936d7d471b5bf7b671df7db5d317
workflow-type: tm+mt
source-wordcount: '1200'
ht-degree: 1%

---

# 适用于AEM as a Cloud Service的Real Use Monitoring服务 {#real-use-monitoring-service-for-aem-as-a-cloud-service}

>[!NOTE]
>
>Real Use Monitoring服务是收集数据的客户端，是一种自动化服务。 无需客户设置。

>[!INFO]
>
>客户端监视仅适用于具有AEM (Adobe Experience Manager)Cloud Service版本&#x200B;**2024.5.16461**&#x200B;及更高版本的客户。

## 概述 {#overview}

RUM（实时监控）服务是一种性能监控技术，可实时捕获和分析网站或应用程序的数字用户体验。 它提供了对Web应用程序实时性能的可视性，并提供了对最终用户体验的更深入洞察。 此服务侧重于通过监控网站参与来优化性能，而不是通过监控用户本身。

使用RUM时，会从URL启动开始一直跟踪关键性能指标，直到将请求发送回浏览器为止。 它有助于开发人员增强应用程序，使其易于最终用户使用。

>[!INFO]
>
>“Real User Monitoring”已更名为“Real Use Monitoring”，因为它更好地反映了服务的真实本质。

## 谁可以从实时监控服务中受益？ {#who-can-benefit-from-rum-service}

AEM开发了RUM以帮助客户和Adobe了解访客如何与AEM站点进行交互。 RUM可用于帮助诊断性能问题以及衡量实验的有效性。 RUM通过取样保护访客的隐私 — 仅监控所有页面查看中的一小部分 — 并且不收集任何个人身份信息(PII)。

## Real Use监控服务和隐私 {#rum-service-and-privacy}

AEM中的“Real Use Monitoring”服务旨在保护访客隐私并最大限度地减少数据收集。 作为访客，这意味着您正在访问或可供访问Adobe的网站不收集任何个人信息。

作为站点操作员，无需其他选择加入即可通过此功能启用监控。 最终用户无需接受额外的弹出窗口或同意表单即可启用RUM。

## Real Use Monitoring服务数据采样 {#rum-service-data-sampling}

传统的Web分析解决方案会尝试收集每位访客的数据。 AEM RUM服务仅从一小部分页面查看中捕获信息。 此服务旨在进行取样和匿名处理，而不是取代分析。 默认情况下，页面的取样比率为1:100。 站点操作员此时无法提高或降低采样率。 为了准确估计总流量，每100次页面查看会从1中收集数据，从而为您提供整体流量的可靠近似值。

在决定是否收集数据时，它是基于逐页查看作出的，几乎不可能跟踪多个页面之间的交互。 从设计角度来看，RUM不了解访客或会话，只了解页面查看次数。

## 会收集哪些数据？ {#what-data-is-being-collected}

Real Use Monitoring服务旨在防止收集个人身份信息。 RUM收集的整套信息如下所示：

* 正在访问的站点的主机名，例如： `experienceleague.adobe.com`
* 用于显示页面的广泛用户代理类型和操作系统，如： `desktop:windows`或`mobile:ios`
* 数据收集的时间，如： `2021-06-26 06:00:02.596000 UTC (in order to preserve privacy, we round all minutes to the previous hour, so that only seconds and milliseconds are tracked)`
* 正在访问的页面的URL，例如： `https://experienceleague.adobe.com/docs`
* 反向链接URL（链接到当前页面的页面的URL，如果用户点击链接）
* 随机生成的页面视图ID，格式类似于： `2Ac6`
* 采样速率的加权或反值，如： `100`。 这意味着仅记录一百分之一的页面查看次数
* 页面加载序列中特定事件的检查点或名称。 或者，以访客身份与其交互
* 用户与上述检查点交互的DOM元素的源或标识符。 例如，它可以是图像
* 针对上述检查点，与用户交互的外部页面或资源的目标或链接。 例如：`https://blog.adobe.com/jp/publish/2022/06/29/media_162fb947c7219d0537cce36adf22315d64fb86e94.png`
* 核心Web虚拟(CWV)性能指标，包括描述访客体验质量的最大内容绘制(LCP)、首次输入延迟(FID)、累积布局偏移(CLS)和到首次字节的时间(TTFB)。

## Real Use Monitoring如何为客户工作 {#how-rum-works-for-a-customer}

Real Use Monitoring可自动监控客户端流量，为您提供有价值的分析。 作为Adobe客户，您无需执行任何其他步骤，因为此服务已无缝集成到您的现有设置中。 通过正式发布(GA)的推出，您将自动从此新功能中受益。

<!-- Alexandru: hiding temporarily, until we figure out where this needs to be linked to 

If you wish to leverage more insights with this new feature to optimize your digital experiences effortlessly, please see here (link to Row 99). -->

## 如何使用实时监控服务数据 {#how-rum-service-data-is-being-used}

RUM数据有利于以下目的：

* 确定并解决客户地点的性能瓶颈
* 简化包括页面查看的自动化流量查找。
* 要了解AEM如何与同一页面上的其他脚本（例如Analytics、Targeting或外部库）交互以提高兼容性。

## 限制和了解页面查看次数和性能量度中的差异 {#limitations-and-understanding-variance-in-page-views-and-performance-metrics}

分析RUM数据时，页面查看次数和其他绩效指标可能存在差异。 这些差异可归因于实时客户端监控固有的几个因素。 以下是客户在解释RUM数据时要牢记的关键注意事项：

1. **跟踪器阻止程序**

   * 最终用户使用跟踪器阻止程序或隐私扩展可能会阻止RUM数据收集，因为这些工具会限制跟踪脚本的执行。 此限制可能会导致报告页面查看次数和用户交互次数不足，从而导致实际网站活动与RUM捕获的数据之间存在差异。

1. **捕获Headless API/JSON调用时的限制**

   * RUM数据服务侧重于客户端体验，目前不捕获从非AEM Headless应用程序发出的后端API或JSON调用。 从RUM服务数据中排除这些调用会与CDN Analytics测量的内容请求产生差异。

## 常见问题解答 {#faq}

<!-- REMOVED THIS FAQ AS PER EMAIL REQUEST FROM SHWETA DUA, SEPTEMBER 4, 2024 TO THE DL-AEM-DOCS GROUP 
1. **Can customers integrate the RUM service scripts with third-party systems like Dynatrace?**

   Yes.
-->

1. **是否正在收集“交互到下一个绘制”、“第一字节的时间”和“第一个内容绘制”Web虚拟量度？**

   收集到下一绘画的交互(INP)和到第一字节的时间(TTFB)。  此时不收集第一个内容绘制。

1. **我的网站上阻止了`/.rum`路径，我应该如何修复？**

   需要`/.rum`路径才能使RUM集合正常工作。 如果您在Adobe的AEM as a Cloud Service之前使用CDN，请确保`/.rum`路径转发到与其他AEM内容相同的AEM源。 并且，确保不会以任何方式对其进行调整。

1. **RUM集合是否计入合同目的的内容请求？**

   RUM库和RUM收藏集不会计为内容请求，也不会增加报告的页面查看次数或API调用数。 此外，对于将现成CDN与AEM as a Cloud Service一起使用的客户，[服务器端收藏集](#serverside-collection)是内容请求的基础。

1. **如何选择退出？**

   Adobe建议您使用实时监控(RUM)，因为它具有显着优势，并且允许您优化数字体验。 它可以提供有价值的分析，从而帮助提高网站性能。 该服务旨在实现无缝连接，对网站的性能没有影响。

   选择退出意味着缺少这些见解。 但是，如果您遇到任何问题，请联系Adobe支持部门。
