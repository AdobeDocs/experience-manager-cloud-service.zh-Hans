---
title: 适用于 AEM Forms as a Cloud Service 的 Edge Delivery Services 的操作遥测
description: 适用于 AEM Forms as a Cloud Service 的 Edge Delivery Services 的操作遥测涉及对用户与表单交互进行持续跟踪和分析。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
role: Admin, Architect, Developer
exl-id: 184fc7dc-d583-4a63-9e30-80d324ec9d7e
source-git-commit: 8be0a9894bb5b3a138c0ec40a437d6c8e4bc7e25
workflow-type: ht
source-wordcount: '789'
ht-degree: 100%

---

# 适用于 AEM Forms as a Cloud Service 的 Edge Delivery Services 的操作遥测

操作遥测让您能够深入了解访客如何与您的 Adobe Experience Manager（AEM）网站互动。此内置工具提供有价值的数据，用以了解用户行为、诊断性能问题并衡量网站试验的有效性。操作遥测不局限于合成测试，而是通过捕捉实际使用中的交互行为，呈现更为精准的网站性能图像。

然而，操作遥测优先考虑访客的隐私。它利用采样技术从具有代表性的用户子集收集数据，确保不会获取任何个人身份信息 (PII)。此外，操作遥测在设计时考虑了数据最小化，仅收集性能分析所需的基本量度。这种方法允许您优化 AEM Sites 同时保持用户信任。


## 先决条件

您可以通过访问以下 URL 查看适用于 AEM Forms as a Cloud Service 的 Edge Delivery Services Forms 监测仪表板：

https://data.aem.live/?ext=forms

![适用于 Forms 的 Edge Delivery Services 的操作遥测登录屏幕](/help/edge/assets/rum-login-screen.png)

要登录适用于 AEM Forms as a Cloud Service 的 Edge Delivery Services 的监测仪表板，请输入以下内容：

* **URL**：该 URL 特定于用户站点或域。用户可以选择过滤站点或域以根据自己的需求查看仪表板。

* **Domain Key**：用户手动生成域密钥。要获取表单的域密钥，请联系您的 Adobe 代表。

### 适用于 AEM Forms as a Cloud Service 的 Edge Delivery Services 的监测仪表板

在登录屏幕输入 URL 和域密钥后，您就可以访问适用于 AEM Forms as a Cloud Service 的 Edge Delivery Services 的监测仪表板。

下图演示了适用于 AEM Forms as a Cloud Service 的 Edge Delivery Services 的仪表板：

![操作遥测表单仪表板](/help/edge/assets/rum-forms-dashboard.png)

### Forms 仪表板的不同关键量度 {#different-metrics-operational-telemetry-dashboard-forms}

此仪表板提供了有关访客如何与 Adobe Experience Manager (AEM) 网站上的表单交互的重要见解。通过监测这些量度，您可以确定需要改进的领域并优化表单，从而获得更佳用户体验和转化率：

* **表单浏览量**：跟踪表单显示的总次数
* **表单提交**：跟踪已完成提交的总数

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

## 可操作见解

通过分析这些量度，您可以发现以下机会：

* 简化表单，减少字段数量。
* 通过清晰的说明和标签提高表单清晰度。
* 优化表单布局，提高移动端响应速度。
* 解决导致表单加载速度变慢的技术问题。

通过关注这些领域，您可以创建更易于使用的表单并鼓励访客填写表格，最终提高转化率。

## 另请参阅

{{see-more-forms-eds}}
