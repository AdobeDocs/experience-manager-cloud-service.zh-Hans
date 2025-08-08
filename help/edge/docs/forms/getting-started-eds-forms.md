---
title: 入门指南：在 AEM Edge Delivery Services 中使用表单
description: 了解如何使用 Adobe Experience Manager Edge Delivery Services 创建并交付高性能表单，重点采用通用编辑器创作方式。
feature: Edge Delivery Services
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
role: Admin, Architect, Developer
source-git-commit: bc422429d4a57bbbf89b7af2283b537a1f516ab5
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 100%

---


# 入门指南：在 AEM Edge Delivery Services 中使用表单

<!--
<span class="preview"> This is a pre-release feature available through our <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=zh-Hans#new-features">pre-release channel</a>. </span>
-->

Adobe Experience Manager (AEM) Edge Delivery Services（EDS）可让您从边缘区域交付极快且高度可扩展的 Web 体验。本指南说明了&#x200B;**如何构建并发布表单来确保提供这样的体验**，并提供明确的推荐层级：

1. **通用编辑器（UE）——大多数团队的首选方式**
2. **基于文档的创作（Docs/Sheets）——适用于快速创建简单表单**
3. **文档创作（DA） —— 用于将表单嵌入由 DA 创作的页面中**

完成本指南后，您将能够选择合适的创作方式，了解不同的提交选项，然后可采取创作生产就绪表单的后续步骤。



## 选择创作方法

| 团队与需求 | 推荐的方式 | 原因 |
|--------------------|--------------------|-----|
| 适用于需要视觉控制、条件逻辑或 AEM 集成功能的市场营销人员/设计师 | **通用编辑器** | 支持拖放操作、高级规则，将数据提交至 FSS 或 AEM Publish 环境 |
| 内容作者已在使用 Word / Google Docs / Sheets，适用于将简单数据捕获至电子表格或通过电子邮件接收 | **基于文档的创作方式** | 使用熟悉的工具，是创建基础表单的最快途径 |
| 由&#x200B;**文档创作（DA）**&#x200B;构建的网站页面 | 可将 UE 表单或基于文档的表单&#x200B;**嵌入**&#x200B;至 DA 页面中 | DA 本身不具备表单构建功能 |


## 创作方式详解

### 通用编辑器

通用编辑器是一款面向市场营销人员和设计师的可视化拖放式创作工具，兼具高速与企业级性能优势：

- 支持实时所见即所得（WYSIWYG）编辑与设备预览。
- 高级规则与验证界面 — 无需代码。
- 可直接集成 AEM 资产、工作流和表单数据模型（FDM）
- 可无缝交接给开发人员，使用原生 JS/CSS 开发自定义组件
- 灵活的提交目标：可从简单的 **Forms Submission Service（FSS）**&#x200B;起步，随着需求增长再切换至 **AEM Publish 环境提交操作**。

> **推荐**：除非您的团队完全以文档为中心，且要创建非常基础的表单，否则建议所有新表单项目均采用通用编辑器开始构建。


### 基于文档的创作方式（Docs/Sheets）

基于文档的创作最适合使用熟悉的工具（如 Microsoft Word、Google Docs 或 Google Sheets）创建结构简单、复杂度较低的表单。此方法非常适合内容团队，以快速且简便的方式构建表单。

- 在 Docs 中以表格形式定义表单字段，或在 Sheets 中以行的方式定义字段。
- 支持基本字段验证，并可集成 Google reCAPTCHA 提供防垃圾信息保护。
- 表单提交操作仅通过 Forms Submission Service 进行处理。
- 即时发布——源文档中的任何更改都会立即反映到网站上，无需经过部署管道。


### 在文档创作（DA）中嵌入表单

文档创作（DA）旨在用于构建结构化页面内容，不支持原生表单创建功能。如需将表单添加至由 DA 创作的页面，请按照以下步骤操作：

1. 使用&#x200B;**通用编辑器**（推荐）或基于文档的创作方式创建表单。
2. 发布表单以生成唯一的 URL（例如，`/forms/contact-us`）。
3. 在您的 DA 页面中插入&#x200B;**嵌入表单**&#x200B;模块，并指定已发布表单的 URL。

<!-- 
## Feature Comparison

| Capability | Universal Editor | Document-Based | Document Authoring |
|------------|-----------------|----------------|--------------------|
| Visual drag-and-drop | ✅ | – | – |
| Advanced rules editor | ✅ | Limited | – |
| Attachments | ✅ | EA | – |
| reCAPTCHA Enterprise | ✅ | ✅ | Depends on embed |
| Submit to spreadsheet/email | ✅ (FSS) | ✅ (FSS) | Via embed |
| Submit to AEM workflows/FDM | ✅ | – | Via UE embed |
| Custom components (JS/CSS) | ✅ | ✅ | Via embed |
| Localization via Sites | ✅ | Manual | Via embed |

-->

## 后续步骤

1. **从通用编辑器开始：**&#x200B;参阅[通用编辑器入门指南](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)开始创作表单。
2. **配置表单提交方式：**&#x200B;选择并设置您偏好的提交方式。请参阅 [Forms Submission Service](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md) 或 AEM Publish 提交操作的配置说明。
3. **应用最佳实践：**&#x200B;请查阅[表单设计最佳实践](/help/edge/docs/forms/universal-editor/best-practices-eds-forms.md)，以确保无障碍访问性与性能优化。
4. **使用基于文档的创作方式：**&#x200B;若需使用 Microsoft Excel 或 Google Sheets 创建表单，请参阅[基于文档的创作教程](/help/edge/docs/forms/tutorial.md)。
5. **在文档创作中嵌入表单：**&#x200B;如果您使用文档创作构建页面，请参考 [DA 教程](https://www.aem.live/developer/da-tutorial)了解如何嵌入已发布的表单。

> **现在，您已准备好使用 AEM Edge Delivery Services 创建首个高性能表单。**