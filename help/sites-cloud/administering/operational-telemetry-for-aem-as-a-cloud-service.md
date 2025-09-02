---
title: 用于 AEM as a Cloud Service 的操作遥测
description: 了解操作遥测，它是一项允许监控客户端数据收集的自动服务。
exl-id: 91fe9454-3dde-476a-843e-0e64f6f73aaf
feature: Administering
role: Admin
source-git-commit: d02569f5fcca0e53c8f258be8a193663364ac31f
workflow-type: tm+mt
source-wordcount: '1134'
ht-degree: 1%

---

# AEM as a Cloud Service的操作遥测服务 {#real-use-monitoring-service-for-aem-as-a-cloud-service}

>[!NOTE]
>
>操作遥测服务（客户端的数据收集）是一项自动化服务。 无需客户设置。

>[!INFO]
>
>客户端监视仅适用于具有AEM (Adobe Experience Manager) Cloud Service版本&#x200B;**2024.5.16461**&#x200B;及更高版本的客户。

## 概述 {#overview}

操作遥测服务是一种性能监控技术，用于实时监控网站或应用程序上的客户端流量。 此服务侧重于收集通过监控网站参与度而不是用户本身来优化性能的关键量度和数据。 使用操作遥测，会从URL启动开始一直跟踪关键性能指标，直到将请求提供回浏览器为止。

## 谁可以从操作遥测服务中获益？ {#who-can-benefit-from-operational-telemetry-service}

操作遥测可帮助客户和Adobe了解最终用户如何与AEM Sites交互。 操作遥测通过有限的数据收集和采样保护访客的隐私 — 仅监视所有页面查看的一小部分。

## 操作遥测服务数据采样 {#operational-telemetry-service-data-sampling}

传统的Web分析解决方案会尝试收集每位访客的数据。 AEM的操作遥测服务仅从一小部分页面查看中捕获信息。 此服务旨在进行取样和匿名处理，而不是取代分析。 默认情况下，页面的取样比率为1:100。 站点操作员此时无法提高或降低采样率。 为了准确估计总流量，每100次页面查看会从1中收集数据，从而为您提供整体流量的可靠近似值。

在决定是否收集数据时，它是基于逐页查看作出的，几乎不可能跟踪多个页面之间的交互。 从设计上看，运行遥测不涉及访客或会话，而只涉及页面查看。

## 会收集哪些数据？ {#what-data-is-being-collected}

操作遥测服务旨在最大限度地减少数据收集。 操作遥测收集的整套信息如下所示：

* 正在访问的站点的主机名，例如： `experienceleague.adobe.com`
* 用于显示页面的广泛用户代理类型和操作系统，如： `desktop:windows`或`mobile:ios`
* 数据收集的时间，如： `2021-06-26 06:00:02.596000 UTC (in order to preserve privacy, we round all minutes to the previous hour, so that only seconds and milliseconds are tracked)`
* 正在访问的页面的URL，例如： `https://experienceleague.adobe.com/docs?lang=zh-Hans`
* 反向链接URL（链接到当前页面的页面的URL，如果用户点击链接）
* 随机生成的页面视图ID，格式类似于： `2Ac6`
* 采样速率的加权或反值，如： `100`。 这意味着仅记录一百分之一的页面查看次数
* 页面加载序列中特定事件的检查点或名称。 或者，以访客身份与其交互
* 用户与上述检查点交互的DOM元素的源或标识符。 例如，它可以是图像
* 针对上述检查点，与用户交互的外部页面或资源的目标或链接。 例如：`https://blog.adobe.com/jp/publish/2022/06/29/media_162fb947c7219d0537cce36adf22315d64fb86e94.png`
* [核心Web虚拟(CWV)](https://web.dev/articles/lcp)性能指标[最大内容绘制(LCP)](https://web.dev/articles/lcp)、[交互到下一绘制(INP)](https://web.dev/articles/inp)以及描述访客体验质量的[累积布局偏移(CLS)](https://web.dev/articles/cls)。

## 操作遥测如何为客户工作 {#how-operational-telemetry-works-for-a-customer}

Operational Telemetry自动监视客户端流量。 作为Adobe客户，您无需执行任何其他步骤，因为此服务已无缝集成到您现有的设置中。 使用操作遥测服务后，您将自动从此新功能中获益。 操作遥测服务目前不会公开任何面向客户的指标以进行监视。 我们正在努力尽快为您提供此功能。

<!-- Alexandru: hiding temporarily, until we figure out where this needs to be linked to 

If you wish to leverage more insights with this new feature to optimize your digital experiences effortlessly, please see here (link to Row 99). -->

## Adobe如何使用操作遥测 {#how-operational-telemetry-data-is-being-used}

操作遥测数据用于以下目的：

* 确定并解决客户地点的性能瓶颈
* 要了解AEM如何与同一页面上的其他脚本（例如Analytics、Targeting或外部库）交互以提高兼容性。
<!--
## Limitations and understanding variance in page views and performance metrics {#limitations-and-understanding-variance-in-page-views-and-performance-metrics}

Here are key considerations for customers to keep in mind when interpreting their Operational Telemetry data:

1. **Tracker blockers**

   * End-users employing tracker blockers or privacy extensions can impede Operational Telemetry data collection, as these tools restrict the tracking scripts' execution. This restriction may lead to underreported page views and user interactions, creating a discrepancy between actual site activity and the data captured by Operational Telemetry.

1. **Limitations in capturing headless API/JSON calls**

   * Operational Telemetry data service focuses on the client-side experience and doesn't capture the backend API or JSON calls made from a non-AEM headless app at this time. The exclusion of these calls from Operational Telemetry service data creates variances from the content requests measured by CDN Analytics.
-->

## 常见问题解答 {#faq}

<!-- REMOVED THIS FAQ AS PER EMAIL REQUEST FROM SHWETA DUA, SEPTEMBER 4, 2024 TO THE DL-AEM-DOCS GROUP 
1. **Can customers integrate the Operational Telemetry service scripts with third-party systems like Dynatrace?**

   Yes.
-->

1. **是否正在收集“交互到下一个绘制”、“第一字节的时间”和“第一个内容绘制”量度？**

   收集到下一绘画的交互(INP)和到第一字节的时间(TTFB)。  此时不收集第一个内容绘制。

1. **我的网站上阻止了`/.rum`路径，我应该如何修复？**

   操作遥测收集需要`/.rum`路径才能正常工作。 如果您在Adobe的AEM as a Cloud Service之前使用CDN，请确保`/.rum`路径转发到与其他AEM内容相同的AEM源。 并且，确保不会以任何方式对其进行调整。 或者，您也可以通过`rum.hlx.page`将Cloud Manager[中名为](/help/implementing/cloud-manager/environment-variables.md#add-variables)的环境变量设置为值`AEM_OPTEL_EXTERNAL`，将用于操作遥测的主机更改为`true`。 如果您希望以后更改回相同的域请求，只需再次删除该环境变量即可。

1. **操作遥测集合是否计入合同目的的内容请求？**

   操作遥测库和操作遥测集合不计为内容请求，也不会增加报告的页面查看次数或API调用数。 此外，对于将现成CDN与AEM as a Cloud Service一起使用的客户，[服务器端收藏集](#serverside-collection)是内容请求的基础。

1. **如何禁用操作遥测？**

   Adobe建议您使用操作遥测，因为它具有重大优势，并且可让Adobe通过提高网站性能来帮助您优化数字体验。 该服务旨在实现无缝连接，对网站的性能没有影响。

   选择退出可能意味着错失了改进网站流量参与度的机会。 但是，如果您遇到任何问题，可以通过[将Cloud Manager](/help/implementing/cloud-manager/environment-variables.md#add-variables)中名为`AEM_OPTEL_DISABLED`的环境变量设置为值`true`来禁用操作遥测。 如果以后要再次启用操作遥测，只需再次删除该环境变量即可。

1. **我可以对Nonce使用内容安全策略吗？

   对操作遥测的支持包含一个实验功能，该功能支持使用nonce的内容安全策略。 可以通过[将Cloud Manager](/help/implementing/cloud-manager/environment-variables.md#add-variables)中名为`AEM_OPTEL_NONCE`的环境变量设置为值`true`来启用此功能。 如果您希望稍后再次禁用此功能，只需再次删除该环境变量即可。

   如果您在此功能上遇到任何问题，请联系Adobe支持部门。

1. **如何只为某些页面启用操作遥测？**

   默认情况下，为存储库中`/content`文件夹下的所有页面启用操作遥测。 通过[将Cloud Manager](/help/implementing/cloud-manager/environment-variables.md#add-variables)中名为`AEM_OPTEL_INCLUDED_PATHS`的环境变量设置为存储库中逗号分隔的路径列表，将仅为这些页面启用操作遥测。 此外，您可以将`AEM_OPTEL_EXCLUDED_PATHS`设置为将排除的存储库中的路径列表。 结合这两个设置，您可以根据自己的要求调整包括的操作遥测。

