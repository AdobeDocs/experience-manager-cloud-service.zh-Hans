---
title: Forms Experience Builder 快速入门指南
description: 了解使用Forms Experience Builder创建您的第一个由AI提供支持的表单的基础知识。 包含示例和最佳实践的分步教程。
hide: true
index: false
hidefromtoc: true
role: Admin, Developer
exl-id: c4f838bc-a001-48e7-afaa-c2ff9034f5d4
source-git-commit: 1d378e6c8ac714779e77314d3457a14d40cd222f
workflow-type: tm+mt
source-wordcount: '1048'
ht-degree: 5%

---

# Forms Experience Builder 快速入门指南 {#getting-started-forms-experience-builder}

Forms Experience Builder借助AI将自然语言描述转换为全功能数字表单，彻底改变了表单创建方式。 本指南将帮助您创建第一个表单，并了解使Forms Experience Builder具有强大功能的核心概念。

## 什么是Forms Experience Builder？ {#what-is-forms-experience-builder}

Forms Experience Builder是一款AI支持的表单创建工具，可让您使用对话语言构建复杂的数字表单。 您无需使用传统的拖放界面或复杂的编码，而只需描述您需要的内容，AI将为您创建表单。

**关键功能：**

* **自然语言表单创建** — 用纯英语描述您的表单要求

* **智能导入和转换** — 将现有文档转换为交互式表单

* **智能字段生成** — 具有预填充选项的AI支持的字段

* **业务逻辑自动化** — 通过对话创建条件规则和验证

* **系统集成** — 将表单连接到您现有的业务工作流

## 先决条件 {#prerequisites-getting-started}

在开始之前，请确保您已：

* **访问Forms Experience Builder** — 可通过提前访问计划获得
* **AEM Forms as a Cloud Service** — 具有自适应Forms核心组件的生产创作环境
* **基本了解** — 熟悉表单概念和业务要求

有关详细的技术设置要求和环境配置，请参阅[部署和配置Forms Experience Builder](deploy-forms-experience-builder.md)。

## 创建表单的方法 {#two-ways-to-create-forms}

使用Forms向导选择[核心组件模板](/help/forms/creating-adaptive-form-core-components.md)或[Edge Delivery Services](/help/edge/docs/forms/universal-editor/create-forms.md)模板、主题和其他选项后，Forms Experience Builder提供了两种创建表单的主要方法：

### 1.从头开始创建 {#create-from-scratch}

使用要求的自然语言描述构建表单。

**使用时间：**

* 根据要求构建新表单

* 为新业务流程创建表单

* 当具有明确的规范但没有现有文档时

**示例：**

    创建客户反馈表单，其中包含：
     — 产品评级（1-5星）
     — 详细反馈的评论字段
     — 客户电子邮件（可选）

>[!VIDEO](https://video.tv.adobe.com/v/3473104)



### 2.导入和转换 {#import-and-convert}

将现有文档转换为交互式数字表单。

在使用此选项之前，请上传PDF文件或表单图像。 PDF可以是AcroForm或基于XFA的PDF表单。 对于[其他类型的PDF forms](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/forms/document-services/pdf-forms-and-documents)，使用Adobe Acrobat中的[准备表单](https://helpx.adobe.com/in/acrobat/using/creating-distributing-pdf-forms.html)选项将它们转换为AcroForm

**使用时间：**

* 转换现有PDF forms

* 使基于纸的流程现代化

* 当您有要增强的现有表单设计时

**示例：**

    /create-form将附加的PDF文件转换为自适应表单

>[!VIDEO](https://video.tv.adobe.com/v/3474042)


## 您的第一个表单：分步教程 {#first-form-tutorial}

让我们创建一个简单的联系人表单来了解基本的工作流程。

### 步骤1：从简单的描述开始 {#step-1-simple-description}

从基本的表单描述开始：

    创建一个包含姓名、电子邮件和消息字段的基本联系表

这将创建一个具有三个基本字段的表单。

![具有三个基本字段的表单 — 使用自然语言提示创建](/help/forms/assets/forms-experience-builder-contact-us-form.png)

### 第2步：添加验证和要求 {#step-2-add-validation}

使用验证规则增强表单：

    将 @name 和 @email 设为必填字段并添加适当的验证

`@`符号引用了特定字段以进行目标修改。

![已添加使用自然语言提示的表单Experience Builder验证](/help/forms/assets/forms-experience-builder-contact-us-form-add-validation.png)


### 步骤3：改善用户体验 {#step-3-improve-ux}

添加有用的占位符文本和指导：

    添加占位符文本：@name“您的全名”、@email“your.email@company.com”、@message“告诉我们您需要什么帮助”

![在Forms Experience Builder中使用自然语言提示添加了验证](/help/forms/assets/forms-experience-builder-contact-us-form-add-placeholder.png)

### 步骤4：添加高级功能 {#step-4-advanced-features}

包括附加功能：

    添加两个下拉列表
    
     — 带选项的inquiryType：“一般问题”、“支持请求”、“销售查询”、“合作伙伴”
    
     — 带选项的紧急级别(低、Medium、高)


![在Forms Experience Builder中添加了使用自然语言提示的下拉组件](/help/forms/assets/forms-experience-builder-contact-us-form-add-dropdown.png)


### 步骤5：实施条件逻辑 {#step-5-conditional-logic}

通过添加规则来创建智能的上下文感知行为，例如：

    隐藏表单加载上的@urgencyLevel下拉菜单
    仅当@inquiryType等于“支持请求”时才显示@urgencyLevel下拉菜单(低、Medium、高)

以下是两个单独的规则：一个在加载表单时隐藏紧急级别下拉列表，另一个仅在查询类型为“支持请求”时显示。 您需要使用单独的提示创建每个规则 — 一次只能创建一个规则。

## 了解AI对话方法 {#ai-conversation-approach}

Forms Experience Builder使用对话式界面，您可以在其中执行以下操作：

### 带@符号的引用字段 {#reference-fields}

使用`@fieldName`引用特定字段：

    @email为必填字段
    为US格式向@phoneNumber添加验证
    将@submitButton文本更改为“发送消息”

>[!VIDEO](https://video.tv.adobe.com/v/3474043)


### 使用自然语言命令 {#natural-language-commands}

用简单的英语描述您想要的：

     — 为公司信息添加分区
     — 为部门选择创建下拉列表
     — 包括恢复的文件上传

### 增量构建 {#build-incrementally}

从简单开始，逐步增加复杂性：

1. **基本结构** — 首先创建基本字段
2. **添加验证** — 实施必填字段和格式验证
3. **增强UX** — 添加占位符、帮助文本和样式
4. **实施逻辑** — 添加条件规则和业务逻辑
5. **配置提交** — 设置表单处理和通知


## 常见表单模式 {#common-form-patterns}

### 联系和反馈表单 {#contact-feedback-forms}

**基本联系人表单：**

    创建具有以下特征的联系人表单：
     — 姓名（必需）
     — 电子邮件（必需，已验证）
     — 主题下拉列表（常规、支持、销售、合作）
     — 消息（必需，多行）

**客户反馈表：**

    创建客户反馈表单，其中包含：
     — 产品评级（1-5星）
     — 详细反馈的评论字段
     — 客户电子邮件（可选）

### 注册和载入表单 {#registration-onboarding-forms}

**用户注册：**

    使用以下方式创建用户注册表：
     — 个人信息（姓名、电子邮件、电话）
     — 帐户首选项（新闻稿、通知）
     — 接受条款和条件
     — 密码创建及强度验证

**员工入职：**

    创建员工入门培训表，包含：
     — 个人详细信息和联系信息
     — 雇佣信息和开始日期
     — 文档上传（简历、ID、税单）
     — 福利选择和首选项

### 调查和评估表 {#survey-assessment-forms}

**客户满意度调查：**

    使用以下内容创建客户满意度调查：
     — 总体评分（1-10级）
     — 类别评分（产品、服务、支持）
     — 开放式反馈部分
     — 人口统计信息（可选）

**技能评估：**

    创建技能评估表，该表具有：
     — 熟练程度级别的技能类别
     — 每种技能的体验持续时间
     — 认证和培训信息
     — 自我评估和目标

## 测试和验证 {#testing-validation}

### 始终测试您的表单 {#always-test-forms}

在部署任何表单之前：

1. **测试所有字段** — 确保验证正常工作

2. **验证条件逻辑** — 检查规则是否正确触发

3. **测试提交** — 确认数据已正确处理

4. **在不同设备上验证** — 确保移动设备兼容性

5. **与利益相关者一起审阅** — 从最终用户获得反馈

### 常见验证模式 {#validation-patterns}

**电子邮件验证：**

    将电子邮件格式验证添加到@email字段

**电话号码验证：**

    将美国电话号码格式验证添加到@phoneNumber

**时期验证：**

    添加年龄验证：@dateOfBirth
必须是18岁或以上
**文件上载验证：**

    添加文件类型验证：仅允许PDF、DOC、DOCX用于@resume
    添加文件大小限制：@resume
最大5MB
<!-- 

## Next steps {#next-steps}

Now that you understand the basics, explore these advanced topics:

* **[LLM-enhanced smart fields](forms-experience-builder-llm-smart-fields.md)** - Create fields with pre-populated options using AI knowledge
* **[AI-powered form creation](forms-experience-builder-prompt-examples-library.md)** - Advanced prompt patterns and examples
* **[Intelligent import and conversion](intelligent-import-conversion.md)** - Transform existing documents into forms
* **[Form submission and integration](form-submission-integration.md)** - Connect forms to your business systems

-->


## 相关文章

* [Forms Experience Builder概述](product-overview.md)

<!-- 
* [LLM-enhanced smart fields](forms-experience-builder-llm-smart-fields.md)
* [AI-powered form creation](forms-experience-builder-prompt-examples-library.md)
* [Intelligent import and conversion](intelligent-import-conversion.md)
* [Form submission and integration](form-submission-integration.md)
* [Frequently asked questions](forms-experience-builder-frequently-asked-questions.md)

-->
