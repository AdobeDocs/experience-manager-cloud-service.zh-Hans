---
title: AEM Forms 的 AI 助手（表单体验生成器）
description: 使用表单片段更快地制作强大的表单
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1145'
ht-degree: 100%

---


# AEM Forms 的 AI 助手（Forms Experience Builder）快速入门

>[!NOTE]
>
>
> AEM Forms 的 AI 助手 (Forms Experience Builder) 功能可在&#x200B;**早期采用者计划**&#x200B;中使用。如果您有兴趣，请从您的工作地址向 :aem-forms-ea@adobe.com 快速发送一封电子邮件，申请访问该功能。

>[!IMPORTANT]
>
> **文档可能会发生变化**：此文档目前正在针对产品进行测试，因此可能会进行更新和修订。随着 AEM Forms 的 AI 助手在早期采用者计划期间不断发展，其功能、命令和示例可能会发生变化。

AEM Forms 的 AI 助手可改变您创建表单的方式 - 只需用自然语言描述您的需求，即可轻松生成表单。该功能可在表单管理用户界面、自适应表单编辑器和通用编辑器中使用，它能理解您的意图，并精确构建您所需的内容。

## 快速入门：只需与它对话

使用 AI 助手工作，就像与一位知识渊博的同事进行对话。您只需描述您想创建的内容，而无需学习复杂的菜单和设置。

### 快速入门

观看我们的介绍视频，快速上手并开始使用：

>[!VIDEO](https://video.tv.adobe.com/v/3463164/)

### 访问 AI 助手

您可以从 AEM Forms 中的三个不同位置访问 AI 助手：

1. **表单管理用户界面**
   - 导航至：Adobe Experience Manager > 表单 > 表单和文档
   - 在界面左侧找到 AI 助手图标
   - 点击图标打开 AI 助手面板

   ![AI 助手图标*](/help/edge/docs/forms/assets/forms-manager.gif){width="50%"}

2. **自适应表单编辑器**
   - 导航至：Adobe Experience Manager > 表单 > 表单和文档
   - 选择并打开一个表单进行编辑
   - 点击编辑器界面中的 AI 助手图标

   ![AI 助手图标*](/help/edge/docs/forms/assets/adaptive-forms-editor.gif){width="75%"}

3. **通用编辑器**

   - 导航至：Adobe Experience Manager > 表单 > 表单和文档
   - 在界面左侧找到 AI 助手图标
   - 点击编辑器界面中的 AI 助手图标

### 如何开始：简单的对话

开始使用 AI 助手最好的方式是使用自然语言。以下是具体操作方法：

**只需描述您的需求：**

- “为我的网站创建一个联系表单”
- “我需要一份带有评分量表的客户反馈表”
- “为即将举行的活动创建一个注册表”
- “做一个简单的产品满意度调查”

**随时添加详细信息：**

- “创建一个包含姓名、电子邮件、电话和消息字段的联系表单”
- “我需要一份多个步骤的会议报名表”
- “创建一个包含五星评级和评论部分的客户反馈表”

**引用您现有的字段：**

- “将电子邮件字段设为必填项”（针对 @email）
- “为电话号码字段添加验证”（针对 @phoneNumber）
- “只在选择已婚的情况下显示配偶信息”（针对 @spouseInfo 和 @maritalStatus）

### 您还可以做什么

除了自然语言之外，AI 助手还提供其他交互方式：

- **上传文件**：附加图像、PDF 或 Figma 设计，让 AI 了解您的设想
- **使用快捷命令**：输入 `/` 查看可用的常用操作快捷键
- **引用特定字段**：使用 `@fieldName` 更改现有的表单字段（例如，`@firstName`，`@emailAddress`）

## 您可以创建什么：有效的例子

以下是使用简单的自然语言可以达到目的的真实示例：

### 创建一个新表单

**简单方法：**

```
"Create a contact form"
```

**更详细的方法：**

```
"Create a professional contact form for a law firm with fields for name, email, phone, case type, and message. Make it mobile-friendly."
```

**附带设计参考：**

```
"Create a contact form based on the attached design mockup. Include all the fields shown in the layout."
```

### 添加表单元素

**基本补充：**

```
"Add a section for personal information"
"Include a file upload for resume"
"Add a dropdown for country selection"
```

**详细规范：**

```
"Add a personal information panel with fields for full name, date of birth, phone number, and email address"
"Include a secure file upload component for documents, limited to PDF files under 5MB"
"Add a country dropdown with options for USA, Canada, UK, and Germany"
```

### 创建动态行为

**简单的逻辑：**

```
"Show additional fields when 'Other' is selected"
"Make the email field required"
"Calculate the total automatically"
```

**复杂的业务规则：**

```
"Show the spouse information fields only when marital status is set to 'Married'"
"Calculate the total cost by multiplying quantity and price, then add 10% tax"
"Enable the submit button only when all required fields are completed and terms are accepted"
```

### 表单布局和设计

**布局更改：**

```
"Make this a multi-step form"
"Organize fields in two columns"
"Convert to an accordion layout"
```

**设计改进：**

```
"Create a wizard-style form with 3 steps: personal info, preferences, and review"
"Arrange the address fields in a compact two-column layout"
"Update the layout to match the attached wireframe"
```

### 提交和集成

**基本提交：**

```
"Send form data to our email"
"Save responses to a spreadsheet"
"Redirect to a thank you page"
```

**高级集成：**

```
"Send form submissions to hr@company.com and create a case in our CRM system"
"Submit data to our REST API endpoint and trigger the new customer workflow"
"Email responses to the sales team and add the lead to our marketing automation platform"
```

## 使用附件

上传文件以帮助 AI 准确了解您正在寻找的内容：

### 支持的文件类型

| 文件类型 | 最适合 | 用例 |
|-----------|----------|-------------|
| **图像**（PNG、JPG、GIF） | 表单布局、UI 模型、纸质表单扫描件 | “创建一个符合此布局的表单” |
| **PDF 文件** | 待转换的现有表格，规范 | “将此 PDF 表单转换为数字化形式” |
| **Figma 文件** | 设计原型，品牌指南 | “根据我的 Figma 设计构建此表单” |
| **设计文件** | 视觉参考，风格指南 | “采用此设计中的风格” |

### 如何使用附件

1. **点击 AI 助手界面中的附件图标** 
2. **从您的设备中选择文件** 
3. **参考附件文件，描述您想要的内容：**
   - “根据此 PDF 附件创建一个表单”
   - “采用此图像中的布局构建一个联系表单”
   - “将此纸质表单转换为数字化版本”

### 附件最佳实践

- **使用清晰、高质量的图像**，以便进行更好的 AI 分析
- **每个附件只关注一个概念**（布局、样式等）
- **参考附件，描述您想要的内容**
- **请将文件大小控制在 10MB 以内，以确保最佳处理效果**

## 获得最佳效果的建议

### 从简单开始，逐步优化

- 从基本请求开始：“创建一个联系表单”
- 逐步添加详细信息：“为电子邮件字段添加验证”
- 测试并优化：“将电话字段设为可选”

### 在需要的情况下具体说明

- 不要用：“把它设计得好看”
- 尝试：“使用专业的颜色和清晰的排版规则”

### 使用自然语言

- 不要用：“添加文本输入组件”
- 尝试：“添加一个名字字段”

### 引用现有元素

- 对现有字段使用 `@fieldName`：“将 @email 设为必填项”
- 具体说明字段名称：“更新 @phoneNumber 字段”

### 分解复杂请求

- 不要提出一个大的请求，而是尝试提出多个小的请求
- 逐步构建表单
- 在进入下一个步骤之前，先测试每一项更改

## 产品帮助和学习

AI 助手还可以教您有关 AEM Forms 功能的知识：

### 提出如下问题：

- “如何创建多步骤表单？”
- “面板和部分有什么区别？”
- “如何设置电子邮件通知？”
- “适合移动设备的表单的最佳实践是什么？”
- “如何将主题应用到我的表单？”

### 获取以下方面的帮助：

- AEM Forms 概念和术语
- 复杂功能的分步说明
- 最佳实践和推荐
- 常见问题排查

## 高级功能参考

对于想要探索高级功能的用户：

### 快速命令

输入 `/` 查看可用的快捷方式：

| 命令 | 用途 | 示例 |
|---------|---------|---------|
| `/create-form` | 开始一个新表单 | `/create-form customer survey` |
| `/add-form` | 在通用编辑器中添加表单 | `/add-form contact form` |
| `/update-layout` | 更改表单结构 | `/update-layout wizard with 3 steps` |
| `/update-field` | 更改字段属性 | `/update-field @email to be required` |
| `/create-rule` | 添加动态行为 | `/create-rule show @spouse if married` |
| `/create-panel` | 添加字段容器 | `/create-panel Personal Information` |
| `/configure-submit` | 设置表单提交 | `/configure-submit to email support` |
| `/help` | 获取帮助 | `/help multi-step forms` |

### 字段引用语法

使用 `@fieldName` 引用现有字段：

- `@firstName` - 名字字段
- `@email` - 电子邮件字段
- `@phoneNumber` - 电话号码字段
- `@dateOfBirth` - 出生日期字段

### 组件类型

使用这些术语可获得最佳结果：

- `text input` - 单行文本字段
- `text area` - 多行文本字段
- `dropdown` - 选择列表
- `checkbox` - 单个复选框
- `checkbox group` - 多个复选框
- `radio group` - 单选按钮群组
- `date picker` - 日期选择
- `file upload` - 文件附件
- `panel` - 用于对字段进行分组的容器

## 疑难解答

### 常见问题和解决方案

**AI 助手不响应：**

- 检查您的互联网连接
- 确保您处于受支持的环境中
- 关闭并重新打开 AI 助手面板

**意外结果：**

- 尝试更具体地重新表述您的请求
- 将复杂的请求分解成多个小步骤
- 使用标准 AEM Forms 术语

**字段引用不起作用：**

- 检查字段名称的拼写是否与显示完全一致
- 对现有字段使用 `@fieldName` 语法
- 引用该字段之前，请确保该字段存在

**设计导入问题：**

- 验证文件是否清晰且结构良好
- 使用支持的格式（PDF、PNG、JPG、Figma）
- 确保文件小于 10MB

## 反馈和支持

帮助我们改进 AI 助手：

- **提供反馈**：使用 AI 助手界面中的反馈按钮
- **报告问题**：通过官方渠道联系 Adobe 支持部门
- **分享体验**：您的反馈有助于让 AI 助手更好地为每个人服务

## 相关资源

[AEM Forms AI 助手 - 提示词库](/help/forms/experience-builder/forms-experience-builder-prompt-examples-library.md)
