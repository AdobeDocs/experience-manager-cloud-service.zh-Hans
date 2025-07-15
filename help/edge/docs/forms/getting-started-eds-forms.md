---
title: 入门指南：在 AEM Edge Delivery Services 中使用表单
description: 了解如何在Adobe Experience Manager Edge Delivery Services上创建并提供高性能表单，重点使用通用编辑器创作方法。
feature: Edge Delivery Services
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
role: Admin, Architect, Developer
source-git-commit: e1ead9342fadbdf82815f082d7194c9cdf6d799d
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 5%

---


# 入门指南：在 AEM Edge Delivery Services 中使用表单

<span class="preview">这是通过我们的<a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=zh-hans#new-features">预发行渠道</a>提供的预发行功能。</span>

Adobe Experience Manager (AEM) Edge Delivery Services (EDS)让您可以从边缘提供超快、高度可扩展的Web体验。 本指南介绍&#x200B;**如何为那些体验构建和发布表单** — 具有明确的推荐层次结构：

1. **通用编辑器(UE) — 大多数团队的最佳选择**
2. **基于文档的创作（文档/工作表） — 非常适用于快速、简单的表单**
3. **文档创作(DA) — 用于将表单嵌入到DA创作的页面**

到最后，您将能够选择正确的创作方法、了解提交选项，并遵循后续步骤以生成可用于生产的表单。



## 选择创作方法

| 团队和要求 | 推荐的方法 | 原因 |
|--------------------|--------------------|-----|
| 营销人员/设计人员需要可视化控制、条件逻辑或AEM集成 | **Universal Editor** | 拖放、高级规则，提交到FSS或AEM Publish |
| 内容作者已在Word/Google Docs/Sheets中工作；简单的数据捕获到电子表格/电子邮件 | **基于文档的创作** | 熟悉的工具，适用于基本表单的最快路径 |
| 在&#x200B;**文档创作(DA)**&#x200B;中内置的网页 | **将UE或基于Doc的表单嵌入** DA页面 | DA不会构建表单本身 |


## 详细创作方法

###  Universal Editor 

通用编辑器是面向营销人员和设计人员的可视化拖放创作工具，将速度和企业级功能相结合：

* 实时WYSIWYG编辑和设备预览。
* 高级规则和验证UI — 无需代码。
* 与AEM资源、工作流和表单数据模型(FDM)的直接集成。
* 将vanilla JS/CSS中的自定义组件无缝移交给开发人员。
* 灵活的提交目标：使用&#x200B;**Forms提交服务(FSS)**&#x200B;从简单开始，或随着您的需求增长切换到&#x200B;**AEM发布提交操作**。

> **推荐**：使用通用编辑器启动每个新表单项目，除非您的团队完全以文档为中心，并且表单非常基本。


### 基于文档的创作（文档/工作表）

基于文档的创作最适合使用熟悉的工具(如Microsoft Word、Google Docs或Google Sheets)创建简单、低复杂度的表单。 此方法非常适合需要快速而直接构建表单的内容团队。

* 在表（文档）中定义表单字段或定义行（工作表）。
* 支持基本字段验证和Google reCAPTCHA用于垃圾邮件保护。
* 表单提交仅通过Forms提交服务进行处理。
* 即时发布 — 在源文档中所做的任何更改都会立即反映在站点上，而无需部署管道。


### 在文档创作(DA)中嵌入Forms

文档创作(DA)专为创建结构化页面内容而设计，不支持原生表单创建。 要将表单添加到由DA编写的页面，请执行以下步骤：

1. 使用&#x200B;**通用编辑器**（推荐）或基于文档的创作创建表单。
2. 发布表单以生成唯一URL（例如，`/forms/contact-us`）。
3. 在DA页面中，插入&#x200B;**嵌入表单**&#x200B;块并指定已发布表单的URL。

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

1. **从通用编辑器开始：**&#x200B;请参阅[通用编辑器快速入门指南](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)开始创作表单。
2. **配置表单提交：**&#x200B;选择并设置首选提交方法。 有关配置说明，请参阅[Forms提交服务](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)或AEM Publish提交操作。
3. **应用最佳实践：**&#x200B;审查[窗体设计最佳实践](/help/edge/docs/forms/universal-editor/best-practices-eds-forms.md)以确保可访问性和性能。
4. **使用基于文档的创作：**&#x200B;使用Microsoft Excel或Google工作表创建表单，请遵循[基于文档的创作教程](/help/edge/docs/forms/tutorial.md)。
5. **在文档创作中嵌入Forms：**&#x200B;如果您在文档创作中构建页面，请参阅[DA教程](https://www.aem.live/developer/da-tutorial)以了解有关嵌入已发布表单的说明。

> **您现在可以使用AEM Edge Delivery Services创建您的第一个高性能表单。**