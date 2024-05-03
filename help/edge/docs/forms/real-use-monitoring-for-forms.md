---
title: AEM Formsas a Cloud Service的实时监控(RUM)Edge Delivery Services
description: AEM Formsas a Cloud Service的Edge Delivery Services实时监控(RUM)涉及持续跟踪和分析用户与表单的交互。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: 184fc7dc-d583-4a63-9e30-80d324ec9d7e
source-git-commit: 6c56f753d2a32de6fe11fd47843cee5bcb8cac4e
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 45%

---


# AEM Formsas a Cloud Service的实时监控(RUM)Edge Delivery Services

实时监控(RUM)功能允许您深入了解访客与您的Adobe Experience Manager (AEM)网站的交互情况。 此内置工具提供了宝贵的数据来了解用户行为、诊断性能问题以及衡量网站实验的有效性。 RUM不局限于合成测试，它捕获了真实使用的交互，从而更准确地了解您网站的性能。

但是，RUM会优先考虑访客隐私。 它利用取样技术从具有代表性的用户子集中收集数据，确保从未捕获任何个人身份信息(PII)。 此外，RUM在设计时考虑到了数据最小化，只收集性能分析所需的基本指标。 此方法允许您优化AEM站点，同时维护用户信任。


## 先决条件

您可以通过访问以下URL来查看AEM Formsas a Cloud ServiceEdge Delivery Services的监视功能板：

https://data.aem.live/?ext=forms

![FormsEdge Delivery Services的RUM登录屏幕](/help/edge/assets/rum-login-screen.png)

要登录到AEM Formsas a Cloud ServiceEdge Delivery Services的监视功能板，请输入以下内容：

* **URL**：该 URL 特定于用户站点或域。用户可以选择过滤站点或域以根据自己的需求查看仪表板。

* **Domain Key**：用户手动生成域密钥。要获取表单的域密钥，请联系您的Adobe代表。

### 适用于AEM Formsas a Cloud Service的Edge Delivery Services监控功能板

在登录屏幕中输入URL和域键后，您将获得对AEM Formsas a Cloud ServiceEdge Delivery Services监控仪表板的访问权限。

下图演示了AEM Formsas a Cloud Service的Edge Delivery Services功能板：

![RUM Forms Dashboard](/help/edge/assets/rum-forms-dashboard.png)

### Forms功能板的其他关键指标 {#different-metrics-rum-dashboard-forms}

该功能板提供了有关访客如何与Adobe Experience Manager (AEM)网站上表单交互的关键见解。 通过监控这些指标，您可以确定需要改进的方面并优化表单，以获得更好的用户体验和转化率：

* **表单视图**：跟踪表单显示的总次数
* **表单提交**：跟踪已完成的提交总数

* **Largest Contentful Paint**：显示 URL 的加载速度，表示从用户请求 URL 到呈现视口中可见的最大内容元素所需的时间。这个最大的内容元素可以是图像、视频或大量的块级文本元素。URL 加载速度的性能评级分类如下：
   * **Good**：如果加载时间为 2.5 秒或更短。
   * **Okay**：如果加载时间大于 2.5 秒但小于或等于 4 秒。
   * **Bad**：如果加载时间超过 4 秒

* **Cumulative Layout Shift**：它测量页面整个生命周期内发生的每个意外布局偏移的所有单独布局偏移分数的总和。它在确定页面性能方面起着至关重要的作用，因为当用户尝试与页面元素交互时，页面元素发生移动会导致糟糕的用户体验。该分数范围从零到任何正数：零表示没有偏移，而数字越大表示页面上的布局偏移越多。用于评估布局移位分数的性能指标分类如下：

   * **Good**：如果布局偏移分数为 0.1 或更低。
   * **Okay**：如果布局偏移分数大于 0.1 但小于或等于 0.25。
   * **Bad**：如果布局偏移分数超过 0.25。

* **交互到下一次绘制**：它评估页面对用户交互的反应速度，考虑到用户访问页面期间页面响应点击、轻触和键盘输入所需的时间。最终值是观察到的最长的相互作用，忽略任何异常。从交互到下一次绘制的性能指标分类如下：
   * **Good**：如果用户操作之间的持续时间为 200 毫秒（ms）或更短。
   * **Okay**：如果持续时间大于 200 毫秒但小于或等于 500 毫秒。
   * **Bad**：如果持续时间超过 500 毫秒。

## 可操作分析

通过分析这些指标，您可以发现以下机会：

* 简化表单并减少字段数。
* 通过明确的说明和标签提高表单清晰度。
* 优化表单布局以提高移动响应能力。
* 解决会降低表单加载速度的技术问题。

通过专注于这些方面，您可以创建更易于使用的表单并鼓励访客完成这些表单，最终导致更高的转化率。

## 另请参阅

{{see-more-forms-eds}}