---
title: 高性能表单设计最佳实践
description: 学习使用 AEM Forms 创建用户友好、可访问且高性能表单的关键最佳实践。提升数据质量、用户体验和提交成功率。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 67b6873b-bb93-4d38-963c-2ca65a1a644b
source-git-commit: 75d8ea4f0913e690e3374d62c6e7dcc44ea74205
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 99%

---

# 创建表单的最佳实践

打造优秀表单不仅仅关乎技术本身。以下是确保您的表单具有良好用户体验并能实现其目标的方法：

## 设计用户友好且具备可访问性的表单

* **使用清晰、可见的标签：**&#x200B;每个表单字段都应配有 `<label>`。请勿仅依赖占位符文本（即输入框内的文字），因为在用户开始输入时占位符会消失，且不利于无障碍访问。
   * *推荐：* `<label for="email">Email Address:</label> <input type="email" id="email" placeholder="you@example.com">`
   * *不推荐：* `<input type="email" placeholder="Email Address">`
* **保持简洁：**&#x200B;尽可能使用标准 HTML 输入类型（如 `<input type="date">`、`<input type="tel">`）。它们通常比复杂的自定义控件更支持移动端并具备更好的无障碍访问性。
* **逻辑顺序和字段分组：**&#x200B;按对用户而言合乎逻辑的方式排列字段。可使用 `<fieldset>` 和 `<legend>` 将相关字段进行分组。
* **提供清晰指引：**&#x200B;对于可能引起混淆的字段，提供简洁的帮助文本或提示说明。
* **键盘导航：**&#x200B;确保用户可以仅通过键盘完成整个表单的操作流程（Tab、Shift+Tab、Enter、空格键）。
* **错误处理：**&#x200B;让错误提示明确、易于理解。在相关字段旁边显示错误信息，并说明如何修正。

* **确保表单加载迅速且易于发现**

   * **将表单放在显眼的位置：**&#x200B;如果表单很重要，请确保用户能轻松看见，而无需大量滚动页面（如尽可能放置在“首屏”区域）。Adobe 研究显示，许多表单因隐藏太深而互动率低下。
   * **优化资源体积：**&#x200B;将表单使用的自定义 JavaScript 或 CSS 保持尽可能轻量，以提升加载速度。Edge Delivery Services 可加快基础页面加载，但大型表单脚本仍可能影响性能。

* **负责任地处理用户数据**
   * **只收集必要信息：**&#x200B;请求的个人可识别信息（PII）越少越好。每一个字段都有可能成为用户放弃填写表单的理由。
   * **保持透明：**&#x200B;清晰说明您&#x200B;*为何*&#x200B;需要收集某些信息，以及&#x200B;*这些信息将如何使用*。提供隐私政策链接。这可以建立信任。

* **改善用户体验：验证码替代方案**

   * **重新考虑可见验证码：**&#x200B;让用户输入扭曲字符或点击所有“红绿灯”的验证方式常常令人沮丧，尤其对有障碍的用户更不友好，并且容易导致高流失率。

* **考虑替代方案：**
   * **蜜罐字段（Honeypot Fields）：**&#x200B;添加一个只有机器人会填写的隐藏字段。如果该字段有数据，极可能是垃圾提交。
   * **基于时间的检测：**&#x200B;检测表单提交速度。如果提交过快，往往是机器人操作。
   * **Invisible reCAPTCHA (v3)：** Google 提供的这项服务会在后台分析用户行为，只有在行为可疑时才弹出验证挑战。这通常能带来更好的用户体验。

## 表单设计的注意事项

| ✅推荐 — 优化表单体验 | ❌不推荐 — 应避免的问题 |
|----------------------------------------------------------------------|------------------------------------------------------------------|
| 使用可见的 `<label>` 标记标注所有字段 | 仅使用占位符文字，缺少适当的标签 |
| 优先使用标准 HTML 输入类型（如 `<input type="email">`） | 使用过于复杂的自定义控件 |
| 确保支持完整的键盘导航 | 提示信息模糊或缺失 |
| 显示清晰、可操作的错误提示 | 无正当理由请求过多的个人信息 |
| 仅收集必要的信息 | 使用难以解决的可见 CAPTCHA |
| 说明数据用途（提供隐私说明或链接） | 将表单隐藏在页面较深的位置 |
| 使用不可见或行为型 CAPTCHA 技术 |                                                                  |
| 将表单放置在页面易于发现的位置（显眼的位置） |                                                                  |


## 后续步骤

本指南概述了如何将表单与 AEM Edge Delivery Services 集成使用。如需更详细的配置步骤和说明，请参阅 Adobe Experience Manager 官方文档。

* [使用 Edge Delivery Services 表单进行文档式创作](/help/edge/docs/forms/tutorial.md)
* [使用 Universal Editor 与 Edge Delivery Services 表单](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
* [文档创作（DA）与内容嵌入](https://www.aem.live/developer/da-tutorial)
* [AEM Forms提交服务](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)
