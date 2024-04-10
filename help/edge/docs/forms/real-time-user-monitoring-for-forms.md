---
title: Forms对Edge Delivery Services的实时用户监控
description: Forms对Edge Delivery Services的实时用户监控涉及持续跟踪和分析用户与表单的交互。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: eadfc3d448bd2fadce08864ab65da273103a6212
workflow-type: tm+mt
source-wordcount: '701'
ht-degree: 0%

---

# Forms对Edge Delivery Services的实时用户监控

Adobe Experience Manager使用Real User Monitoring (RUM)来了解访客与Adobe Experience Manager驱动的网站的交互。 它有助于诊断性能挑战和衡量实验有效性。 Real User Monitoring使用取样技术维护访客的隐私，确保您访问的网站不会收集任何个人信息。 不允许将个人数据添加到RUM数据收集。 Adobe Experience Manager中的“Real User Monitoring”旨在保护访客隐私并最大限度地减少数据收集。

## 对Edge Delivery ServicesForms使用实时用户监控的优势 {#advantages}

AEM对以下内容使用实时用户监控：

* 确定并修复站点上的性能瓶颈。
* 要估计客户地点的页面查看次数，请执行以下操作
* 要理解Adobe Experience Manager与同一页面上的分析、定位或外部库的交互，请增强兼容性。

## 先决条件

您可以通过访问以下URL来查看Edge Delivery ServicesForms的实时用户监控仪表板： https://data.aem.live/?ext=forms

![Edge Delivery ServicesForms的RUM登录屏幕 ](/help/edge/assets/rum-login-screen.png)

要登录到FormsEdge Delivery Services的实时用户监视仪表板，请输入以下内容：
* **URL**：URL特定于用户站点或域。 用户可以根据需要选择筛选网站或域以查看功能板。
* **域密钥**：用户手动生成域密钥。 如需协助或咨询，请参阅 [生成RUM域密钥](https://aemcs-workspace.adobe.com/rum/generate-domain-key) 文档。

### 适用于Edge Delivery ServicesForms的实时用户监控仪表板

在登录屏幕中输入URL和域密钥后，您即可访问Edge Delivery ServicesForms的实时用户监控功能板。

下图演示了Edge Delivery ServicesForms的RUM功能板：

![RUM Forms功能板](/help/edge/assets/rum-forms-dashboard.png)

### Forms的RUM功能板的其他关键量度 {#different-metrics-rum-dashboard-forms}

您可以使用以下关键指标评估访客与Adobe Experience Manager驱动型网站的交互：

* **表单视图**：指定日期范围内为URL呈现的表单总数。
* **表单提交**：在指定日期范围内为URL提交的表单总数。
* **最大内容油漆**：它显示URL加载的速度，指示从用户请求URL时起呈现视区中可见的最大内容元素所用的时间。 这个最大的内容元素可以是图像、视频或实质性的块级文本元素。 URL加载速度的性能评级分类如下：
   * **好**：如果加载时间为2.5秒或更短。
   * **确定**：如果加载时间大于2.5秒但4秒或更短。
   * **不良**：如果加载时间超过4秒

* **累积版面偏移**：它测量在整个页面生命周期内发生的每个意外布局偏移的所有单个布局偏移分数的总和。 它在识别页面性能方面起着至关重要的作用，因为当用户尝试与页面元素进行交互时，页面元素会发生变化，从而导致用户体验不佳。 此分数介于0到任意正数之间：零表示无偏移，数字越大表示页面上的布局偏移越多。 用于评估布局班次分数的性能量度分类如下：

   * **好**：如果布局偏移分数为0.1或更小。
   * **确定**：如果布局偏移得分大于0.1但小于或等于0.25。
   * **不良**：如果布局偏移得分超过0.25。

* **与下一幅绘画的交互**：它评估页面对用户交互做出反应的速度，并考虑页面在用户访问页面期间对点击、点按和键盘输入做出响应所需的时间。 最终值是观察到的相互作用最长的值，不考虑任何异常。 “交互到下一绘画”的性能指标分类如下：
   * **好**：如果用户操作之间的持续时间为200毫秒(ms)或更短。
   * **确定**：如果持续时间超过200毫秒但500毫秒或更短。
   * **不良**：如果持续时间超过500毫秒。

