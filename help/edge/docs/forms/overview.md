---
title: 适用于 AEM Forms 的 Edge Delivery Services 概述
description: 了解如何使用Edge Delivery Services通过AEM Forms创建和提供高性能表单，从而实现快速开发和简化数据收集。
feature: Edge Delivery Services
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
role: Admin, Architect, Developer
source-git-commit: 1ddf97f56e5a9b7c95959da47a748f5a6d128e43
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 8%

---


# 适用于 AEM Forms 的 Edge Delivery Services 


适用于 AEM Forms 的 Edge Delivery Services 是一组可组合的服务，可用于实现快速开发环境，作者可以在其中快速更新、发布和启动新表单。这些服务提供卓越且具有高影响力的表单体验，从而推动参与度和转化率。这些表单体验很容易创作和开发。

* **更快的体验：** Forms是从全局内容交付网络(CDN)交付的，确保为用户快速加载这些内容。
* **快速开发：**&#x200B;简化的开发过程允许更快更新。 无需等待较长的管道生成即可发布更改。
* **灵活创作：**&#x200B;从多种工具中进行选择以创建表单，包括基于文档的创作(Microsoft Word、Google Docs/Sheets)或可视化WYSIWYG编辑器（通用编辑器）。

## 工作原理

通过Edge Delivery Services，表单的结构和内容可以驻留在AEM as a Cloud Service、Microsoft SharePoint或Google Drive等源中。 此内容已发布到全局CDN。 当用户访问您的网站时，为了获得最佳性能，会直接从最近的CDN边缘服务器提供表单。

![简化的架构图，其中显示了内容源、CDN和用户。](/help/forms/assets/eds-simplified-architecture.png)
**使用Forms简化的Edge Delivery Services架构**

用户提交的数据可以发送到不同的目标，从简单的电子表格到功能强大的AEM后端以供进一步处理。

## 选择创作方法

您可以通过多种方式为Edge Delivery Services站点创建表单。 最佳方法取决于您团队的技能、表单的复杂性和项目要求。

![帮助选择表单创作方法的决策树。](/help/forms/assets/eds-authoring-selection.png)
**表单创作决策树**

### 基于文档的创作

此方法允许您[使用Microsoft Word或Google Docs/工作表创建表单](/help/edge/docs/forms/create-forms.md)。 您可以使用特定的表格格式在文档中定义表单字段、标签和类型。 Edge Delivery Services将此文档转换为交互式HTML表单。

**功能：**

* 在熟悉的工具(Word、Google Docs或Google Sheets)中创作。
* 定义文本输入、电子邮件、下拉列表、复选框和单选按钮等字段。
* 设置基本验证规则，例如必填字段。
* 集成Google reCAPTCHA以保护垃圾邮件。
* 支持文件上传。
* 将数据直接提交到电子表格或电子邮件地址。
* 通过GitHub使用自定义代码进行扩展，以获取高级组件和样式。

**最适合：**

* 主要使用文档编辑器创建内容的团队。
* 快速创建从简单到中等复杂的表单。
* 将简单的数据收集转换为电子表格或电子邮件。

从基于文档的表单提交通常由[AEM Forms提交服务](/help/forms/forms-submission-service.md)处理，该服务将数据路由到配置的电子表格或电子邮件地址。

### 通用编辑器创作

[通用编辑器提供了一个现代的WYSIWYG界面](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)，用于构建具有拖放体验的表单。

**功能：**

* 使用预建组件库的可视化拖放表单构建。
* 配置实时验证和复杂的业务逻辑（例如，根据用户选择显示/隐藏字段）。
* 不同设备的实时预览。
* 与AEM as a Cloud Service功能(如内容片段、AEM工作流和用户权限)的深度集成。
* 通过“体验生成器”进行人工智能辅助表单创建和编辑。

**最适合：**

* 使用条件逻辑、多步骤面板或个性化构建复杂表单。
* 喜欢可视化工具的团队（例如，营销人员、商业用户）。
* 需要与AEM后端高度集成以便进行数据处理和工作流的项目。

使用Universal Editor构建的Forms可以使用[Forms提交服务](/help/forms/forms-submission-service.md)，也可以配置为使用为OOTB提供的[提交操作进行高级数据处理](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)，例如将数据发送到AEM Workflow、REST端点或数据库。

### 在文档创作页面中嵌入Forms

[文档创作(DA)](https://www.aem.live/developer/da-tutorial)是Adobe托管的服务，用于管理Edge Delivery Services的网站内容。 虽然DA本身并不是表单构建工具，但您可以将其用于创作网页，然后嵌入通过其他方法创建的表单。

**工作方式：**

1. **创建表单：**&#x200B;使用基于文档的创作或通用编辑器构建表单。
2. **发布表单：**&#x200B;确保表单已发布并可在其自己的URL中访问。
3. **嵌入到DA：**&#x200B;在文档创作页面上，添加引用表单URL的块以嵌入它。

这种方法适用于使用文档创作作为其Edge Delivery Services站点的主要内容管理系统的团队。

## 创作方法比较

| 标准 | 基于文档的创作 | 通用编辑器(WYSIWYG) | 文档创作(DA)中的Forms |
|----------------------------------|---------------------------------------|-----------------------------------------|-------------------------------------------|
| **主要创作工具** | Word/Google Docs/工作表 | 浏览器(AEM通用编辑器) | 不适用(Forms为&#x200B;*嵌入式*) |
| **团队技能级别** | 熟悉文档编辑器 | 熟悉可视化Web工具 | 将DA用于页面内容 |
| **典型表单复杂性** | 从简单到适中 | 中等到复杂，企业级 | 取决于嵌入的形式 |
| **提交选项** | Forms提交服务（至工作表/电子邮件） | Forms提交服务、AEM发布（工作流、表单数据模型、第三方集成） | 遵循嵌入式表单的设置 |
| **AEM后端集成** | 最小 | 高(使用AEM发布提交) | 通过嵌入的通用编辑器表单间接进行 |
| **最适合……** | 内容团队快速创建简单表单，快速捕获数据。 | 需要可视化控制、复杂表单或深度AEM集成的营销人员和业务用户。 | 在DA中管理主要内容的网站。 |

<!-- 
## Detailed Feature Comparison

| **Capability**                        | **Universal Editor (WYSIWYG)** | **Document-based Authoring** | **Document Authoring (DA)** |
|-----------------------------------------|-------------------------------|-----------------------------|-----------------------------|
| **Unified Composition with Sites**    | ✅                            |                              | ✅ (with embedded forms)     |
| **Embedding Form Support**            | ✅                            | ✅                          | ✅ (embed from Universal Editor or Docs)   |
| **Rules (Dynamic Behavior)**          | Advanced rules editor with custom functions | Limited: Show/hide, compute value, custom functions | Depends on embedded form     |
| **Attachment Support**                | ✅                            | ℹ️ (Early Access)           | Depends on embedded form     |
| **CAPTCHA Support**                   | reCAPTCHA Enterprise          | reCAPTCHA Enterprise       | Depends on embedded form     |
| **Submission Features**               | REST, Email, FDM, Workflow, SharePoint, OneDrive, Azure Blob, Power Automate, Workfront Fusion (EA) | Only Spreadsheet            | Follows embedded form's setup |
| **Data Schema**                       | FDM, Custom                   | Custom                      | Based on embedded form       |
| **Pre-fill**                          | 💡 (via Wizard)               | ✅                          | Depends on embedded form     |
| **Fragments**                         | ✅                            | ✅                          | Depends on embedded form     |
| **Visual Rule Editor**                | ✅                            |                              |                              |
| **Localization**                      | 💡 (via Sites)                | ℹ️ (Excel/Sheets manual)    | Depends on embedded form     |
| **Template Support**                  | Only Initial Content          |                              |                              |
| **Theme**                             | ℹ️ (at project level)         | ℹ️ (at project level)        | ℹ️ (based on hosting site)    |
| **Custom Component**                  | ✅                            | ✅                          | ✅ (if embedded component supports it) |
| **Experimentation**                   | ✅                            | ✅                          | Depends on embed context     |
| **Submit Action**                     | ✅                            | Only Spreadsheet            | Based on embedded form       |
-->



## 后续步骤

* [使用基于文档的创作创建表单](/help/edge/docs/forms/tutorial.md)
* [了解Forms的通用编辑器](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
* [配置表单提交操作](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)
* [了解文档创作(DA)](https://www.aem.live/developer/da-tutorial)
