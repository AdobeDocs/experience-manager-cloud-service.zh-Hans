---
title: Forms Experience Builder
description: 使用表单片段更快地制作强大的表单
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: 750674bbd29ec1b29388579d77c7c15bd89335ab
workflow-type: tm+mt
source-wordcount: '1180'
ht-degree: 2%

---


# Forms Experience Builder简介

>[!IMPORTANT]
>
> **文档可能会发生变化**：此文档目前正在针对产品进行测试，因此可能会进行更新和修订。随着Forms Experience Builder在率先采用者计划中的不断演进，功能、命令和示例可能会发生变化。

Forms Experience Builder为Adobe Experience Manager (AEM) Forms引入了人工智能的强大功能。 这一创新的解决方案改变了组织通过自然语言交互和智能自动化来创建、管理和优化其数字表单的方式。

Forms Experience Builder构建于现代Web技术之上，由高级AI服务提供支持，它使技术用户和非技术用户都能够通过对话界面创建完善的专业级表单。 无论您是需要简单的注册表单的业务分析师，还是创建复杂的多步骤工作流的开发人员，Forms Experience Builder都可以简化整个表单创建过程。

## 对话界面

Forms Experience Builder提供了基于聊天的直观界面，使表单创建变得简单，就像聊天：

```
┌─────────────────────────────────────────────────────────┐
│ Forms Experience Builder                               │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  👤 User: Create a customer feedback form              │
│                                                         │
│  🤖 AI: I'll help you create a feedback form. What    │
│       type of feedback do you want to collect?         │
│                                                         │
│  👤 User: Product reviews with ratings and comments    │
│                                                         │
│  🤖 AI: Perfect! I've created a feedback form with:   │
│       * Product rating (1-5 stars)                     │
│       * Comment field                                   │
│       * Customer email (optional)                       │
│       * Submit to email notification                    │
│                                                         │
│  👤 User: Add a field for product category             │
│                                                         │
│  🤖 AI: Added a dropdown field with common categories  │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

## 核心功能

### AI支持的表单创建

**自然语言表单生成**

使用纯英文描述从头开始创建完整的表单。 您只需描述自己的要求，例如“创建一个具有评级尺度和评论字段的客户反馈表单”，Forms Experience Builder即会生成相应的表单结构、字段类型和验证规则。

**动态字段管理**

通过对话式命令添加、修改或删除表单字段。 AI理解上下文，可以根据您的要求智能建议字段类型、验证规则和用户界面改进。

**布局优化**

通过自然语言更新表单布局和配置。 请求更改，如“使表单更便于移动使用”或“在逻辑流中重新组织字段”，Forms Experience Builder将应用适当的样式和布局调整。

### 智能导入和转换

**PDF到表单的转换**

将静态PDF文档转换为交互式动态表单。 上传任意PDF文档，Forms Experience Builder将分析结构以创建具有相应字段类型和验证的相应数字表单。

表单转换的&#x200B;**URL**

将现有Web窗体或页面转换为AEM Forms。 只需提供一个URL，Forms Experience Builder即可提取表单元素，并将其重新创建为具有增强功能的本机AEM Forms。

**多格式文件支持**

处理各种用于表单创建的文件类型，包括PDF、图像、屏幕截图和现有表单模板。 Forms Experience Builder可以处理这些内容并将其转换为功能性AEM Forms。

### 高级表单逻辑和集成

**智能规则生成**

通过自然语言创建复杂的表单验证和业务逻辑规则。 Forms Experience Builder可以生成复杂的条件逻辑、字段依赖项和验证规则，这些通常需要丰富的编码知识。

**完整的提交操作配置**

配置表单提交以与现有业务系统集成：

- **电子邮件集成**：设置自动电子邮件通知和确认
- **REST API端点**：连接到自定义应用程序和服务
- **云存储**：与Azure Blob Storage、SharePoint和OneDrive集成
- **工作流自动化**：连接到Power Automate和Workfront Fusion
- **营销平台**：与Marketo直接集成，用于潜在客户管理
- **AEM工作流**：利用现有AEM工作流功能

**性能分析**

分析表单转化绩效和用户参与模式。 Forms Experience Builder提供了有关表单有效性的见解以及改进完成率和用户体验的优化建议。

## 工作原理

Forms Experience Builder遵循一种简单的对话式方法：

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│  1. Describe    │───▶│  2. AI Creates  │───▶│  3. Refine &    │
│  Your Form      │    │  Initial Form   │    │  Configure      │
│  Requirements   │    │                 │    │                 │
└─────────────────┘    └─────────────────┘    └─────────────────┘
         │                       │                       │
         │                       │                       │
         ▼                       ▼                       ▼
┌─────────────────────────────────────────────────────────────────┐
│  "Create a loan application form"  →  Form with relevant        │
│  "Add conditional logic"           →  fields and basic          │
│  "Connect to CRM system"           →  validation rules          │
└─────────────────────────────────────────────────────────────────┘
```

## 用例示例

### 贷款申请表

```
┌─────────────────────────────────────────────────────────┐
│ Loan Application - Multi-Step Form                    │
├─────────────────────────────────────────────────────────┤
│ Step 1: Personal Information                           │
│  🏠 Property Type: [Primary] [Investment] [Commercial] │
│  💰 Loan Amount: [$_______] (triggers different paths) │
│  📊 Income Verification: [W2] [Self-Employed] [Other]  │
│                                                         │
│ Step 2: Financial Details (conditional based on above) │
│  ↳ If Self-Employed: Show tax returns, profit/loss     │
│  ↳ If W2: Show employment history, pay stubs           │
│  ↳ Complex debt-to-income calculations                 │
│                                                         │
│ Step 3: Compliance & Review                            │
│  📋 Regulatory disclosures, digital signatures         │
│  🔍 Automated eligibility pre-screening                │
└─────────────────────────────────────────────────────────┘
```

### 保险索赔表

```
┌─────────────────────────────────────────────────────────┐
│ Insurance Claim - Adaptive Form                        │
├─────────────────────────────────────────────────────────┤
│ 🚗 Claim Type: [Auto] [Property] [Health] [Business]   │
│                                                         │
│ ↳ Auto Selected: Shows accident details, police report │
│ ↳ Property: Shows damage assessment, repair estimates  │
│ ↳ Health: Shows medical provider network, pre-auth     │
│                                                         │
│ 📎 Dynamic Document Requirements:                       │
│   * Photos/videos of damage                            │
│   * Police reports (auto only)                         │
│   * Medical records (health only)                      │
│   * Repair estimates (property only)                   │
│                                                         │
│ 🔄 Real-time claim status updates                      │
└─────────────────────────────────────────────────────────┘
```

### 迁移和转换方案

通过AI支持的转换，将现有表单转换为强大的数字体验。


### 📄 PDF到Digital

**从静态文档到交互式表单**

通过自动计算和移动响应式设计，将包含50多个字段的PDF forms转换为动态数字体验。

**主要优点：**

- 自动计税和字段依赖关系
- 数字签名和电子归档集成
- 移动响应布局优化
- 处理错误减少95%

**最适合于：**&#x200B;税务表单、政府申请、复杂业务文档

**节省时间：**&#x200B;每个表单2-3小时→15分钟



### 🏛️旧版XFA现代化

**为过时的表单注入新的生命力**

利用实时验证和可访问性合规性，将复杂的XFA应用程序转换为现代的多步向导。

**主要优点：**

- 简化的多步向导界面
- 利用情景式帮助进行实时验证
- 政府数据库集成
- 完全符合WCAG 2.1无障碍要求

**最适合于：**&#x200B;政府许可、企业申请、合规表单

**影响：**&#x200B;完成速度提高70%，错误减少90%




### 📱屏幕快照转为数字

**将任何纸质表单转换为数字体验**

上传任何纸质表单的图像，观看人工智能提取字段、优化布局和创建集成就绪的数字表单。

**主要优点：**

- 智能字段类型检测（99%+准确性）
- 优化响应布局生成
- 在原始纸面文档之外增强了验证
- 集成就绪型架构

**最适合：**&#x200B;纸面应用程序、手写表单、旧文档

**处理时间：** 2小时→5分钟（每个表单）



### 🌐 HTML增强功能

**充实您现有的Web窗体**

在不中断现有功能的情况下，将高级验证、条件逻辑和多渠道提交添加到基本的HTML表单。

**主要优点：**

- 高级验证逻辑和规则
- 条件字段行为和工作流
- 多渠道提交选项
- 内置分析和性能跟踪

**最适合：**&#x200B;联系人表单、注册表单、简单Web应用程序

**转化改进：** +40%且用户体验增强


## Forms Experience Builder与传统开发

| 方面 | 传统表单创建 | Forms Experience Builder |
|--------|---------------------------|----------------------|
| **创建时间** | 2-3天 | 2-3小时 |
| **技术知识** | 必填 | 非必需 |
| **验证规则** | 手动编码 | 自然语言 |
| **移动优化** | 手动CSS/JS | 自动 |
| **辅助功能** | 手动实施 | 内置合规性 |
| **更新** | 需要更改代码 | 自然语言 |


## 为组织带来的好处

### 民主化表单创建

使非技术性用户无需编程知识即可创建复杂的表单。 业务分析员、主题专家和内容创建者可以通过自然语言对话直接将其需求转换为功能形式。

### 缩短实现价值的时间(TTV)

将表单开发速度从数天大幅提升到数小时。 以前需要较长的开发周期现在可以通过对话式人工智能在单个会话中完成，从而加快数字计划的上市速度。

### 界面简化

通过直观的对话界面消除学习曲线。 用户可以使用自然语言创建复杂的表单，而不是学习技术表单构建工具，从而减少培训时间并提高采用率。

### 扩展现代化工作

高效地使旧版表单项目组合符合现代化要求。 将现有PDF、XFA和HTML表单转换为响应式数字体验，同时保留业务逻辑并增强整个表单生态系统的用户体验。

## 快速入门

要开始使用Forms Experience Builder，请访问[Forms Experience Builder文档](forms-ai-assistant-getting-started.md)。 您可以通过Forms编辑器或通用编辑器访问AEM Forms Experience Builder，具体取决于您的首选工作流程。

对于希望转变表单创建过程的组织，Forms Experience Builder提供了一个强大、直观的解决方案，它将对话式人工智能的灵活性与企业级表单管理的强大功能结合起来。

## 载入和抢先体验

Forms Experience Builder目前作为早期访问(EA)计划的一部分提供。 要参与并获得访问权限，请执行以下步骤：

1. 确保您使用的是与组织关联的官方工作电子邮件地址。
2. 向[aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com)发送一封电子邮件，请求访问Forms Experience Builder。
3. 在您的请求中包含您的组织名称和任何相关的项目详细信息，以帮助加快载入流程。

>[!NOTE]
>
> Forms Experience Builder的访问权限仅限于“抢先体验”计划中的已批准参与者。 如果您符合条件，Adobe将审核您的请求并提供入门的进一步说明。

有关提前访问程序及其功能的详细信息，请参阅[AEM Forms提前访问文档](/help/forms/early-access-ea-features.md)。

