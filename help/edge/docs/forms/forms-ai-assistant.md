---
title: AEM Forms的AI助手(Forms Experience Builder)
description: 使用表单片段更快地制作强大的表单
feature: Edge Delivery Services
hide: true
hidefromtoc: true
role: Admin, Architect, Developer
exl-id: a8d64082-a23f-4919-ad66-042faad77d29
source-git-commit: ab071b9159f3d4db275313080d7c14a46096c4de
workflow-type: tm+mt
source-wordcount: '1141'
ht-degree: 1%

---

# AEM Forms的AI助手(Forms Experience Builder)

>[!NOTE]
>
>
> 适用于AEM Forms的AI助手(Forms Experience Builder)功能在&#x200B;**早期采用者计划**&#x200B;下可用。 如果您有兴趣，请通过您的工作地址向mailto:aem-forms-ea@adobe.com发送一封快速电子邮件，请求访问功能。

>[!IMPORTANT]
>
> **文档可能会发生更改**：此文档当前正在针对产品进行测试，可能会受到更新和修订。 在早期采用者项目中，适用于AEM Forms的AI Assistant会不断演变，因此功能、命令和示例可能会发生变化。

适用于AEM Forms的AI Assistant可改变您创建表单的方式 — 只需以自然语言描述您需要的内容，并观察表单的生动呈现。 它在Forms管理UI、自适应Forms编辑器和通用编辑器中提供，它理解您的意图并构建您正在寻找的确切内容。

## 快速入门：只需与之交谈

AI助手的工作方式就像与知识丰富的同事进行对话。 您无需学习复杂的菜单和设置，只需描述您要创建的内容。

### 快速入门

通过观看我们的介绍性视频，快速启动并运行：

>[!VIDEO](https://video.tv.adobe.com/v/3463164/)

### 访问AI助手

您可以从AEM Forms中的三个不同位置访问AI助手：

1. **Forms管理UI**
   - 导航到： Adobe Experience Manager > Forms > Forms和文档
   - 在界面左侧查找AI助手图标
   - 单击图标以打开AI助手面板

   ![AI助手图标*](/help/edge/docs/forms/assets/forms-manager.gif){width="50%"}

2. **自适应Forms编辑器**
   - 导航到： Adobe Experience Manager > Forms > Forms和文档
   - 选择并打开表单进行编辑
   - 单击编辑器界面中的AI助手图标

   ![AI助手图标*](/help/edge/docs/forms/assets/adaptive-forms-editor.gif){width="75%"}

3. **Universal Editor**

   - 导航到： Adobe Experience Manager > Forms > Forms和文档
   - 在界面左侧查找AI助手图标
   - 单击编辑器界面中的AI助手图标

### 如何开始：简单对话

从AI助手开始的最佳方式是通过自然语言。 方法如下：

**只描述您需要的内容：**

- “为我的网站创建联系人表单”
- “我需要一份具有评级尺度的客户反馈表”
- “为即将举行的活动构建一个注册表”
- “进行简单的产品满意度调查”

**随时添加详细信息：**

- “创建包含姓名、电子邮件、电话和消息字段的联系人表单”
- “我需要一张多步骤会议注册表”
- “构建包含5星级评级和评论部分的客户反馈表单”

**引用现有字段：**

- “将电子邮件字段设为必填”(@email)
- “将验证添加到电话号码字段”(@phoneNumber)
- “仅在已婚的情况下显示配偶信息”(对于@spouseInfo和@maritalStatus)

### 您也可以执行哪些操作

除了自然语言，AI助手还提供其他交互方式：

- **上传文件**：附加图像、PDF或Figma设计以显示AI您所设想的内容
- **使用快速命令**：键入`/`以查看常用操作的可用快捷键
- **引用特定字段**：使用`@fieldName`修改现有表单字段（如`@firstName`、`@emailAddress`）

## 您可以创建的内容：有用的示例

以下是您使用简单自然语言可以完成的任务的实际示例：

### 启动新表单

**简单方法：**

```
"Create a contact form"
```

**更详细的方法：**

```
"Create a professional contact form for a law firm with fields for name, email, phone, case type, and message. Make it mobile-friendly."
```

**设计引用：**

```
"Create a contact form based on the attached design mockup. Include all the fields shown in the layout."
```

### 添加表单元素

**基本添加：**

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

**简单逻辑：**

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

上传文件以帮助AI了解您确切需要什么：

### 支持的文件类型

| 文件类型 | 最适合 | 示例使用 |
|-----------|----------|-------------|
| **图像** (PNG、JPG、GIF) | 表单布局、UI模型、纸质表单扫描 | “创建与此布局匹配的表单” |
| **PDF文件** | 要转换的现有表单，规范 | &quot;将此PDF表单转换为数字&quot; |
| **图形文件** | 设计原型，品牌指南 | “从我的菲格玛设计构建此表单” |
| **设计文件** | 视觉引用、样式参考线 | “匹配此设计中的样式” |

### 如何使用附件

1. **单击AI助手界面中的附件图标**
2. 从设备中&#x200B;**选择文件**
3. **描述所需内容**&#x200B;引用附加文件：
   - “基于此附加的PDF创建表单”
   - “构建与此图像中的布局匹配的联系人表单”
   - “将此纸质表单转换为数字版本”

### 使用附件的最佳实践

- **使用清晰、高质量的图像**&#x200B;以获得更好的AI分析
- **每个附件关注一个概念**（布局、样式等）
- **描述您需要的内容**&#x200B;以及附件
- **将文件保留在10MB以下**&#x200B;以获得最佳处理

## 获得最佳结果的提示

### 从简单开始，逐步构建

- 从基本请求开始：“创建联系人表单”
- 逐步添加详细信息：“向电子邮件字段添加验证”
- 测试和优化：“将电话字段设为可选”

### 需要时具体说明

- 而不是：“使其看起来美观”
- 试用：“使用专业颜色和简洁的排版”

### 使用自然语言

- 而不是“添加文本输入组件”
- 尝试：“添加名字字段”

### 引用现有元素

- 将`@fieldName`用于现有字段：“@email为必填”
- 特定于字段名称：“更新@phoneNumber字段”

### 划分复杂请求

- 请尝试多个较小的请求，而不是一个大型请求
- 逐步构建表单
- 在转到下一个更改之前测试每个更改

## 产品帮助和学习

AI Assistant还可以向您传授AEM Forms的功能：

### 提出以下问题：

- “如何创建多步表单？”
- “面板和部分之间有何区别？”
- “如何设置电子邮件通知？”
- “适用于移动设备的表单的最佳实践是什么？”
- “如何将主题应用于表单？”

### 获取以下方面的帮助：

- AEM Forms概念和术语
- 复杂功能的分步说明
- 最佳实践和建议
- 常见问题疑难解答

## 高级功能参考

对于希望探索高级功能的用户：

### 快速命令

键入`/`以查看可用的快捷键：

| 命令 | 用途 | 示例 |
|---------|---------|---------|
| `/create-form` | 开始新表单 | `/create-form customer survey` |
| `/add-form` | 在通用编辑器中添加表单 | `/add-form contact form` |
| `/update-layout` | 更改窗体结构 | `/update-layout wizard with 3 steps` |
| `/update-field` | 修改字段属性 | `/update-field @email to be required` |
| `/create-rule` | 添加动态行为 | `/create-rule show @spouse if married` |
| `/create-panel` | 添加字段容器 | `/create-panel Personal Information` |
| `/configure-submit` | 设置表单提交 | `/configure-submit to email support` |
| `/help` | 获取帮助 | `/help multi-step forms` |

### 字段引用语法

使用`@fieldName`引用现有字段：

- `@firstName` — 名字字段
- `@email` — 电子邮件字段
- `@phoneNumber` — 电话号码字段
- `@dateOfBirth` — 出生日期字段

### 组件类型

请使用以下术语以获得最佳结果：

- `text input` — 单行文本字段
- `text area` — 多行文本字段
- `dropdown` — 选择列表
- `checkbox` — 单个复选框
- `checkbox group` — 多个复选框
- `radio group` — 单选按钮组
- `date picker` — 日期选择
- `file upload` — 文件附件
- `panel` — 分组字段的容器

## 疑难解答

### 常见问题和解决方案

**AI助手未响应：**

- 检查互联网连接
- 确保您在受支持的环境中
- 关闭并重新打开AI助手面板

**意外结果：**

- 请尝试更明确地更改您的请求
- 将复杂的请求分解为较小的步骤
- 使用标准AEM Forms术语

**字段引用不起作用：**

- 检查字段名称的拼写与显示的完全相同
- 对现有字段使用`@fieldName`语法
- 在引用字段之前确保该字段存在

**设计导入问题：**

- 验证文件是否清晰且结构合理
- 使用支持的格式(PDF、PNG、JPG、Figma)
- 确保文件大小小于10MB

## 反馈和支持

帮助我们改进AI助手：

- **提供反馈**：使用AI助手界面中的反馈按钮
- **报告问题**：通过正式渠道联系Adobe支持部门
- **共享体验**：您的输入有助于使助手对每个人都更好

## 相关资源

[AEM Forms AI助手 — 提示库](/help/edge/docs/forms/ai-assistant-prompt-library.md)
