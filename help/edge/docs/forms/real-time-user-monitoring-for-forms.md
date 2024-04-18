---
title: Edge Delivery Services Forms 的实时用户监控
description: Edge Delivery Services Forms 的实时用户监控涉及对用户与表单交互的持续跟踪和分析。
feature: Edge Delivery Services
exl-id: 184fc7dc-d583-4a63-9e30-80d324ec9d7e
source-git-commit: 2affe155b285986128487043fcc4f2938fc15842
workflow-type: tm+mt
source-wordcount: '701'
ht-degree: 100%

---


# Edge Delivery Services Forms 的实时用户监控

Adobe Experience Manager 使用 Real User Monitoring（RUM）来了解访问者与 Adobe Experience Manager 驱动的网站的互动。它有助于诊断性能挑战并衡量实验效果。Real User Monitoring 使用采样技术来维护访问者的隐私，确保您访问的网站不会收集任何个人信息。不允许将个人数据添加到 RUM 数据收藏中。Adobe Experience Manager 中的 Real User Monitoring 旨在保护访客隐私并最大限度地减少数据收集。

## 对 Edge Delivery Services Forms 使用实时用户监控的优势 {#advantages}

AEM 使用实时用户监控来实现以下功能：

* 识别并修复站点上的性能瓶颈。
* 估算客户网站的页面浏览量
* 理解 Adobe Experience Manager 与同一页面上的分析、定位或外部库的交互，增强兼容性。

## 先决条件

您可以通过访问以下 URL 查看 Edge Delivery Services Forms 的实时用户监控仪表板：
https://data.aem.live/?ext=forms

![Edge Delivery Services Forms 的 RUM 登录屏幕 ](/help/edge/assets/rum-login-screen.png)

要登录 Edge Delivery Services Forms 的实时用户监控仪表板，请输入以下内容：
* **URL**：该 URL 特定于用户站点或域。用户可以选择过滤站点或域以根据自己的需求查看仪表板。
* **Domain Key**：用户手动生成域密钥。如需帮助或咨询，请参阅 [Generate RUM Domain Key](https://aemcs-workspace.adobe.com/rum/generate-domain-key) 文档。

### Edge Delivery Services Forms 的实时用户监控仪表板

在登录屏幕输入 URL 和域密钥后，您就可以访问 Edge Delivery Services Forms 的实时用户监控仪表板。

下图演示了 Edge Delivery Services Forms 的 RUM 仪表板：

![RUM Forms Dashboard](/help/edge/assets/rum-forms-dashboard.png)

### 表单 RUM 仪表板的不同关键量度 {#different-metrics-rum-dashboard-forms}

您可以使用以下关键量度评估访客与 Adobe Experience Manager 驱动的网站的互动：

* **Formviews**：它是指定日期范围内为 URL 呈现的表单总数。
* **Formsubmission**：它是指定日期范围内为 URL 提交的表单总数。指定日期范围内为某个 URL 的表单总数
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
