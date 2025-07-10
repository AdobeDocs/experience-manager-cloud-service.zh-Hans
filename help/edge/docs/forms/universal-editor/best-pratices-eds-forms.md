---
title: 设计高性能Forms的最佳实践
description: 了解使用AEM Forms创建用户友好、可访问和高性能表单的基本最佳实践。 提高数据质量、用户体验和提交成功率。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 67b6873b-bb93-4d38-963c-2ca65a1a644b
source-git-commit: 75d8ea4f0913e690e3374d62c6e7dcc44ea74205
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 0%

---

# 创建Forms的最佳实践

构建绝佳的形式不仅仅是技术。 下面是如何确保表单对用户友好并实现其目标的：

## 设计用户友好且易于访问的Forms

* **使用清晰可见的标签：**&#x200B;每个表单字段都需要一个`<label>`。 不要只依赖占位符文本（输入字段内的文本），因为当用户键入内容时，占位符文本会消失，并且不利于访问。
   * *良好：* `<label for="email">Email Address:</label> <input type="email" id="email" placeholder="you@example.com">`
   * *错误：* `<input type="email" placeholder="Email Address">`
* **保持简单：**&#x200B;尽可能使用标准HTML输入类型(`<input type="date">`、`<input type="tel">`)。 与复杂的自定义构件相比，它们通常可提供更好的移动支持和辅助功能。
* **逻辑顺序和分组：**&#x200B;以对用户有意义的方式排列字段。 使用`<fieldset>`和`<legend>`将相关字段分组在一起。
* **提供清晰的说明：**&#x200B;对于任何可能令人困惑的字段，提供简洁的帮助文本或工具提示。
* **键盘导航：**&#x200B;确保用户仅使用键盘（Tab、Shift+Tab、Enter、空格键）即可导航浏览整个表单。
* **错误处理：**&#x200B;使错误明显且易于纠正。 在相关字段旁边显示错误消息，并解释哪些内容需要修复。

* **确保您的Forms加载快速且可见**

   * **突出放置Forms：**&#x200B;如果表单很重要，请确保用户可轻松地查看表单，而无需过度滚动（如果可能，请将“折叠”放在上方）。 Adobe的研究表明，许多表单由于是隐藏的，互动程度很低。
   * **优化Assets：**&#x200B;将表单的任何自定义JavaScript或CSS尽可能的减小以确保快速加载时间。 Edge Delivery Services有助于加载基本页面，但较大的表单脚本仍可能会减慢加载速度。

* **负责任地处理用户数据**
   * **仅询问您需要的内容：**&#x200B;您要求的个人身份识别信息(PII)越少越好。 每个字段都是用户放弃表单的潜在原因。
   * **透明：**&#x200B;清楚地解释&#x200B;*为什么*&#x200B;您需要某些信息以及&#x200B;*如何使用它*。 链接至您的隐私政策。 这会建立信任。

* **改善用户体验：验证码替代方案**

   * **重新思考可见的字幕：**&#x200B;那些“键入波动文本”或“单击所有红绿灯”测试可能会让用户（尤其是残障用户）非常沮丧，并通常会导致高流失率。

* **考虑替代项：**
   * **Honeypot字段：**&#x200B;添加只由机器人填写的隐藏字段。 如果其中包含数据，则提交内容可能是垃圾邮件。
   * **基于时间的检查：**&#x200B;衡量提交表单的速度。 提交太快通常是机器人。
   * **不可见的reCAPTCHA (v3)：**&#x200B;此Google服务在后台分析用户行为，仅当用户看起来可疑时才会提出质询。 这通常是更好的用户体验。

## 窗体设计应该做和不应该做

| ✅可以 — 为了获得更好的Forms | ❌不 — 避免这些 |
|----------------------------------------------------------------------|------------------------------------------------------------------|
| 对所有字段使用可见的`<label>`标记 | 仅使用占位符文本而不是适当的标签 |
| 首选标准HTML输入类型（如`<input type="email">`） | 使用过于复杂的自定义构件 |
| 确保完整的键盘导航 | 提供模糊或缺少的错误消息 |
| 显示清除、可操作的错误消息 | 无正当理由请求过多的个人数据 |
| 仅询问必要信息 | 使用难以解析的可见验证码 |
| 说明如何使用数据（隐私信息或链接） | 在页面内隐藏表单 |
| 使用不可见或行为验证码技术 |                                                                  |
| 使表单易于在页面上找到（突出放置） |                                                                  |


## 后续步骤

本指南概述了如何将表单与AEM Edge Delivery Services结合使用。 有关特定配置的更多详细分步说明，请参阅Adobe Experience Manager官方文档：

* [使用Edge Delivery Services Forms进行基于文档的创作](/help/edge/docs/forms/tutorial.md)
* [带有Edge Delivery Services Forms的通用编辑器](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
* [文档创作(DA)和嵌入内容](https://www.aem.live/developer/da-tutorial)
* [AEM Forms提交服务](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)
