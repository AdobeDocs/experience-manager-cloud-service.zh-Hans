---
title: Forms Experience Builder
description: 使用表单片段更快地制作强大的表单
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: de524aeddd5f53cbd713ff0523222966752ebbc0
workflow-type: tm+mt
source-wordcount: '922'
ht-degree: 31%

---




# 概述

AEM Forms Experience Builder利用Generative AI通过自然语言加速数字表单的创建。 这一功能强大的工具使技术用户和非技术用户均可使用简单的对话式界面来设计、修改和优化专业级别的表单。

这一革命性的方法实现了表单创建的民主化，将实现价值的时间从数天大幅缩短到数小时，并扩展了整个表单生态系统的现代化工作。

## Forms Experience Builder演示 {#forms-experience-builder-demo}

>[!VIDEO](https://video.tv.adobe.com/v/3463164/)

## 为什么选择Forms Experience Builder？

Forms Experience Builder具有以下主要优势：

**使用自然语言描述创建表单**

AEM Forms作为单一的真实来源，Forms Experience Builder通过对话式人工智能实现了快速表单创建，将开发时间从数天大幅减少到数小时。

**智能导入和转换功能**

将现有文档转换为交互式数字体验。 Forms Experience Builder支持各种格式，可以分析上传的内容以检测字段类型、保留布局以及通过响应式设计和高级逻辑增强表单。

**授权非技术用户创建专业表单**

Forms Experience Builder允许您在不具备编码知识的情况下创建复杂的表单。 您可以通过简单的对话命令来设计复杂的布局、实施验证规则以及配置提交操作。

## 载入和先决条件

Forms Experience Builder当前可通过提前访问计划获得。 若要请求访问，请通过您的正式电子邮件ID向[aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com)发送电子邮件。

Experience Builder需要具有[自适应AEM Forms as a Cloud Service核心组件](/help/forms/enable-adaptive-forms-core-components.md)的Forms生产创作环境。

## 访问 Forms Experience Builder


1. 导航到&#x200B;**AEM > Forms > Forms和文档**。
1. 单击&#x200B;**创建**&#x200B;并选择&#x200B;**自适应表单**
1. 使用此向导，根据您的要求使用[核心组件模板](/help/forms/creating-adaptive-form-core-components.md)或[Edge Delivery Services](/help/edge/docs/forms/universal-editor/create-forms.md)模板创建新表单并打开表单进行编辑。
1. 在编辑器工具栏中选择&#x200B;**Forms Experience Builder**&#x200B;图标以打开Forms Experience Builder界面以使用自然语言创建表单。


| ![自适应Forms编辑器 — Forms Experience Builder](/help/edge/docs/forms/assets/adaptive-forms-editor.gif "自适应Forms编辑器 — Forms Experience Builder") | ![通用编辑器 — Forms Experience Builder](/help/forms/assets/ue-forms-experience-builder.gif "通用编辑器 — Forms Experience Builder") |
|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| *自适应表单编辑器* | *通用编辑器* |

<!-- >

## Learn more on key capabilities {#key-capabilities-forms-experience-builder}

<table>
<td>
   <a href="/help/forms/experience-builder/forms-experience-builder-getting-started.md">
   <img alt="Getting started with Forms Experience Builder" src="./assets/getting-started.png" />
   </a>
   <div>
      <a href="/help/forms/experience-builder/forms-experience-builder-getting-started.md">
      <strong>Getting started with Forms Experience Builder</strong>
      </a>
   </div>
   <p>
      <em>Learn the basics of creating your first form using AI-powered capabilities.</em>
   </p>
</td>

<td>
   <a href="/help/forms/experience-builder/forms-experience-builder-llm-smart-fields.md">
   <img alt="LLM-enhanced smart fields" src="./assets/llm-smart-fields.png" />
   </a>
   <div>
      <a href="/help/forms/experience-builder/forms-experience-builder-llm-smart-fields.md">
      <strong>LLM-enhanced smart fields</strong>
      </a>
   </div>
   <p>
      <em>Learn how to create fields with pre-populated options using AI knowledge base.</em>
   </p>
</td>

<td>
   <a href="/help/forms/experience-builder/forms-experience-builder-prompt-examples-library.md">
   <img alt="AI-powered form creation" src="./assets/ai-form-creation.png" />
   </a>
   <div>
      <a href="/help/forms/experience-builder/forms-experience-builder-prompt-examples-library.md">
      <strong>AI-powered form creation</strong>
      </a>
   </div>
   <p>
      <em>Learn how to utilize natural language to create and modify forms.</em>
   </p>
</td>
</table>

<table>
<td>
   <a href="/help/forms/experience-builder/intelligent-import-conversion.md">
   <img alt="Intelligent import and conversion" src="./assets/intelligent-import.png" />
   </a>
   <div>
      <a href="/help/forms/experience-builder/intelligent-import-conversion.md">
      <strong>Intelligent import and conversion</strong>
      </a>
   </div>
   <p>
      <em>Learn how to transform existing documents into interactive digital forms</em>
   </p>
</td>

<td>
   <a href="/help/forms/experience-builder/form-submission-integration.md">
   <img alt="Form submission and integration" src="./assets/form-submission.png" />
   </a>
   <div>
      <a href="/help/forms/experience-builder/form-submission-integration.md">
      <strong>Form submission and integration</strong>
      </a>
   </div>
   <p>
      <em>Learn how to configure form submissions to integrate with your business systems.</em>
   </p>
</td>

<td>
   <a href="/help/forms/experience-builder/forms-experience-builder-frequently-asked-questions.md">
   <img alt="Forms Experience Builder frequently asked questions" src="./assets/faq-banner.jpg" />
   </a>
   <div>
      <a href="/help/forms/experience-builder/forms-experience-builder-frequently-asked-questions.md">
      <strong>Frequently asked questions</strong>
      </a>
   </div>
   <p>
      <em>Get responses to common questions about Forms Experience Builder capabilities and usage.</em>
   </p>
</td>
</table> -->

## 核心功能

Forms Experience Builder 提供了两种用于创建强大数字表单的主要工作流：

### AI支持的表单创建

**使用自然语言生成表单**

使用简单的英语描述从头开始创建完整的表单。只需描述您的要求，例如“创建一个带有评分量表和评论字段的客户反馈表”，Forms Experience Builder 就会生成适当的表单结构。您可以使用可视化编辑器的体验生成器来添加更多字段、验证规则和提交逻辑。

**动态字段管理**

通过对话式命令添加、修改或移除表单字段。AI 会理解上下文，并根据您的要求智能地提出字段类型、验证规则和用户界面改进方面的建议。

**布局优化**

通过自然语言更新表单布局和配置。要求进行更改，例如“将表单布局改为向导式布局”， Forms Experience Builder 就会应用适当的样式调整布局。

**全面的提交操作配置**

配置表单提交，与您现有的业务系统集成：

- **电子邮件集成**：设置自动电子邮件通知和确认
- **REST API 端点**：与自定义应用程序和服务连接
- **云存储**：与 Azure Blob 存储、SharePoint 和 OneDrive 集成
- **工作流自动化**：与 Power Automate 和 Workfront Fusion 连接
- **营销平台**：与 Marketo 直接集成，实现潜在客户管理
- **AEM 工作流**：利用现有的 AEM 工作流功能


### 智能导入和转换

将现有文档转换为交互式数字体验。 Forms Experience Builder支持各种格式，可以分析上传的内容以检测字段类型、保留布局以及通过响应式设计和高级逻辑增强表单。 支持的格式包括：

- **Acroforms**：具有现有字段结构的交互式 PDF 表单
- **XFA PDF**：基于 XML 的复杂表单架构
- **扁平化 PDF**：将静态文档转换为交互式表单
- **图像和屏幕快照**：JPG、PNG格式
- **手绘表单**：草图和纸质照片



## Forms Experience Builder与传统开发

| 方面 | 传统表单创建 | Forms Experience Builder |
|--------|---------------------------|----------------------|
| **创建时间** | 2-3 天 | 2-3 小时 |
| **技术知识** | 必需 | 不必需 |
| **验证规则** | 手动编码 | 自然语言 |
| **无障碍访问** | 手动实施 | 内置合规 |

## 开始探索

以下是您可以开始探索Forms Experience Builder的一些方法：

- **增量生成表单**：从简单的表单开始，逐步增加复杂性。 例如，创建基本联系人表单，然后添加验证规则、占位符文本和条件逻辑。 [了解详情](/help/forms/experience-builder/forms-experience-builder-prompt-examples-library.md#incremental-development-examples)。

- **创建智能字段**：利用AI知识创建具有预填充的上下文感知选项的字段，例如包含所有国家/地区、主要机场或行业标准职称的下拉列表。 [了解详情](/help/forms/experience-builder/forms-experience-builder-prompt-examples-library.md#llm-enhanced-smart-fields)。

- **实施复杂的业务逻辑**：定义根据用户输入显示或隐藏表单节的条件规则。 例如，创建一个规则，仅在用户的婚姻状态为“已婚”时显示“配偶信息”部分。 [了解详情](/help/forms/experience-builder/forms-experience-builder-prompt-examples-library.md#rule-creation--business-logic)。

- **与您的系统集成**：配置表单提交以与现有业务工作流连接，无论该工作流是将数据发送到REST API、在您的CRM中创建新的潜在客户，还是将文档保存到云存储。 [了解详情](/help/forms/experience-builder/forms-experience-builder-prompt-examples-library.md#data-integration--submission)。

## 加入

Forms Experience Builder当前可通过提前访问计划获得。 要请求访问权限，请执行以下步骤：

1. **收集您的信息**：您需要以下详细信息：
   - IMS组织ID
   - 项目群 ID
   - 项目详细信息（时间线、范围、用例）
   - 您的正式工作电子邮件

   如果您需要帮助来查找您的IMS组织ID和项目ID，请参阅[Adobe Experience Cloud组织设置指南](/help/onboarding/cloud-manager-introduction.md)和[项目和环境管理](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)文档。

2. **发送访问请求**：电子邮件[aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com)，其中包含上一步中收集的所有信息。

   Forms Experience Builder的访问受到限制，并且需要根据项目容量以及与早期访问标准保持一致进行审批。

## 快速入门

要开始使用Forms Experience Builder，请访问[Forms Experience Builder文档](/help/forms/experience-builder/forms-experience-builder-getting-started.md)。
