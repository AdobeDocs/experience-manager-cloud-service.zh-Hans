---
title: Forms Experience Builder
description: 使用表单片段更快地制作强大的表单
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Developer
exl-id: 183e999c-9896-49a2-b29b-7c77da380df9
source-git-commit: 1d378e6c8ac714779e77314d3457a14d40cd222f
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 32%

---

# 概述

AEM Forms Experience Builder利用Generative AI通过自然语言加速数字表单的创建。 这一功能强大的工具使技术用户和非技术用户均可使用简单的对话式界面来设计、修改和优化专业级别的表单。

Forms Experience Builder支持通过对话式人工智能快速创建表单，同时使非技术用户无需编码知识即可创建复杂表单。 您可以通过简单的对话命令来设计复杂的布局、实施验证规则以及配置提交操作。

## 核心功能

Forms 体验构建器提供了两种用于创建强大数字表单的主要工作流：

### AI支持的表单创建

**使用自然语言生成表单**

使用简单的英语描述从头开始创建完整的表单。只需描述您的要求，例如“创建一个带有评分量表和评论字段的客户反馈表”，Forms 体验构建器就会生成适当的表单结构。您可以使用可视化编辑器的体验生成器来添加更多字段、验证规则和提交逻辑。

**动态字段管理**

通过对话式命令添加、修改或移除表单字段。AI 会理解上下文，并根据您的要求智能地提出字段类型、验证规则和用户界面改进方面的建议。

**布局优化**

通过自然语言更新表单布局和配置。要求进行更改，例如“将表单布局改为向导式布局”， Forms 体验构建器就会应用适当的样式调整布局。

### 智能导入和转换

将现有文档转换为交互式数字体验。 Forms Experience Builder支持各种格式，可以分析上传的内容以检测字段类型、保留布局以及通过响应式设计和高级逻辑增强表单。 支持的格式包括：

- **Acroforms**：具有现有字段结构的交互式 PDF 表单
- **XFA PDF**：基于 XML 的复杂表单架构
- **扁平化 PDF**：将静态文档转换为交互式表单
- **图像和屏幕快照**：JPG、PNG格式
- **手绘表单**：草图和纸质照片


## Forms Experience Builder演示 {#forms-experience-builder-demo}

>[!VIDEO](https://video.tv.adobe.com/v/3463164/)

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



<!--
**Comprehensive Submit Action Configuration**

Configure form submissions to integrate with your existing business systems:

- **Email Integration**: Set up automated email notifications and confirmations
- **REST API Endpoints**: Connect to custom applications and services
- **Cloud Storage**: Integrate with Azure Blob Storage, SharePoint, and OneDrive
- **Workflow Automation**: Connect to Power Automate and Workfront Fusion
- **Marketing Platforms**: Direct integration with Marketo for lead management
- **AEM Workflows**: Leverage existing AEM workflow capabilities
-->


## 开始探索

以下是您可以开始探索Forms Experience Builder的一些方法：

- **增量生成表单**：从简单的表单开始，逐步增加复杂性。 例如，创建基本联系人表单，然后添加验证规则、占位符文本和条件逻辑。 [了解详情](/help/forms/experience-builder/forms-experience-builder-prompt-examples-library.md#incremental-development-examples)。

- **创建智能字段**：利用AI知识创建具有预填充的上下文感知选项的字段，例如包含所有国家/地区、主要机场或行业标准职称的下拉列表。 [了解详情](/help/forms/experience-builder/forms-experience-builder-prompt-examples-library.md#llm-enhanced-smart-fields)。

- **实施复杂的业务逻辑**：定义根据用户输入显示或隐藏表单节的条件规则。 例如，创建一个规则，仅在用户的婚姻状态为“已婚”时显示“配偶信息”部分。 [了解详情](/help/forms/experience-builder/forms-experience-builder-prompt-examples-library.md#rule-creation--business-logic)。

- **与您的系统集成**：配置表单提交以与现有业务工作流连接，无论该工作流是将数据发送到REST API、在您的CRM中创建新的潜在客户，还是将文档保存到云存储。 [了解详情](/help/forms/experience-builder/forms-experience-builder-prompt-examples-library.md#data-integration--submission)。

<!-- ## Onboarding

The Forms Experience Builder is currently available through an Early Access Program. To request access, follow these steps:

1. **Gather your information**: You will need the following details:
    - IMS Organization ID
    - Program ID
    - Project Details (timeline, scope, use cases)
    - Your Official Work Email

   If you need help finding your IMS Organization ID and Program ID, refer to the [Adobe Experience Cloud Organization Setup Guide](/help/onboarding/cloud-manager-introduction.md) and the [Program and Environment Management](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) documentation.

2. **Send an access request**: Email [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) with all the information gathered in the previous step. 

    Access to the Forms Experience Builder is limited and subject to approval based on program capacity and alignment with early access criteria. 

## Getting started

To get started with the Forms Experience Builder, visit the [Forms Experience Builder documentation](/help/forms/experience-builder/forms-experience-builder-getting-started.md).

-->
