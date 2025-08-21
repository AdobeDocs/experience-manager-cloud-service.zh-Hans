---
title: Forms Experience Builder快速入门
description: 了解如何使用Forms Experience Builder创建和管理具有适用于所有用户类型的渐进式信息披露的表单
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
exl-id: b8f64082-a23f-4919-ad66-042faad77d30
source-git-commit: 750674bbd29ec1b29388579d77c7c15bd89335ab
workflow-type: tm+mt
source-wordcount: '1720'
ht-degree: 15%

---


# Forms Experience Builder快速入门

>[!NOTE]
>
> Forms Experience Builder功能在&#x200B;**早期采用者计划**&#x200B;下可用。 如果您有兴趣，请从您的工作地址向`aem-forms-ea@adobe.com`发送一封快速电子邮件，以请求访问该功能。

>[!IMPORTANT]
>
> **文档可能会发生变化**：此文档目前正在针对产品进行测试，因此可能会进行更新和修订。随着Forms Experience Builder在率先采用者计划中的不断演进，功能、命令和示例可能会发生变化。

本全面指南可帮助您开始使用对话式AI技术创建和管理表单。 无论您是希望创建第一个表单的初学者，还是希望利用高级功能的高级用户，您都可以找到详细信息和实际示例，以指导您逐步了解Forms Experience Builder的功能。

## 先决条件和设置

### 1.请求访问

如果您无权访问Forms Experience Builder：

1. **请求访问**：从工作电子邮件向[aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com)发送电子邮件
2. **包含信息**：组织名称和项目详细信息
3. **等待批准**： Adobe将审核并提供入门指导

### 2.验证Forms是否已启用

在使用Forms Experience Builder之前，请确保为您的环境启用了[AEM Forms](/help/forms/setup-forms-cloud-service.md)。


### 3.设置环境


* Edge Delivery Services (EDS)的&#x200B;**：**

   * [设置Edge Delivery Services Forms的环境](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)
   * [使用Edge Delivery Forms模板创建新表单](/help/edge/docs/forms/universal-editor/create-forms.md)

* 基于核心组件的表单的&#x200B;**：**

   * 在Adobe Experience Manager实例上，转到Forms > Forms &amp; Documents
   * [使用核心组件模板创建新页面](/help/forms/creating-adaptive-form-core-components.md)

## 快速入门

### 访问Forms Experience Builder

**通用编辑器**

* 在通用编辑器中打开EDS页面
* 在左侧面板中查找Forms Experience Builder图标
* 单击以打开对话界面

**自适应表单编辑器**

* 导航到： AEM > Forms > Forms和文档
* 创建或打开基于核心组件的表单以进行编辑
* 单击编辑器工具栏中的Forms Experience Builder图标

### 您的第一个表单

尝试此简单对话以开始：

```
👤 You: "Create a simple contact form"
🤖 AI: "I'll create a contact form with name, email, and message fields for you."

👤 You: "Make the email field required"
🤖 AI: "Updated the email field to be required with validation."
```

### 基本命令

| 符号 | 用途 | 使用方法 |
|--------|---------|------------|
| `/` | 快速操作和快捷键 | 键入`/create`以创建表单，`/help`以获得帮助 |
| `@` | 引用现有表单字段 | 键入`@fieldName`以修改特定字段（例如，`@email`） |
| 纯文本 | 自然对话 | 描述您想要的内容：“添加必填电话号码字段” |

### 成功提示

* **具体说明**：“添加验证所需的电子邮件字段”的效果比“添加电子邮件”更好
* **引用现有字段**：修改表单时使用`@fieldName`
* **请求帮助**：类型`/help`，后跟您的问题
* **迭代**：一次进行一项更改以获得最佳结果

## 核心功能

### 创建Forms的两种方法

#### 1.从头开始创建

使用自然语言描述您的表单要求，Forms Experience Builder将生成完整的表单结构：

**示例：**

* “创建包含个人信息、财务详细信息和文档上传的贷款申请表单”
* “构建包含评级、评论和产品类别的客户反馈表单”
* “我需要一张多步骤注册表，以便参加具有支付处理功能的会议”

#### 2.导入和转换

将现有表单和文档转换为现代交互式体验：

**支持的源：**

* **PDF forms**：上传静态PDF→交互式数字表单，并进行验证
* **屏幕截图/图像**：纸质表单→功能数字版本的照片
* **HTML Forms**：具有高级功能的基本Web窗体→增强型AEM Forms
* **XFA Forms**：旧版Adobe表单→现代响应式表单
* **URL**：具有改进UX→本机AEM Forms的现有Web窗体

**如何导入：**

1. 单击Forms Experience Builder界面中的附件图标
2. 上传您的文件(PDF、图像、Figma设计等)
3. 描述您的要求：
   * &quot;将此PDF表单转换为数字版本&quot;
   * “创建与此屏幕快照布局匹配的表单”
   * “根据我的 Figma 设计构建此表单”

**支持的文件类型：**

* **图像** (PNG、JPG、GIF)：表单布局、UI模型、扫描的表单
* **PDF文件**：现有表单、规范、文档
* **Figma文件**：设计原型，品牌指南
* **设计文件**：视觉参考、样式指南

### 关键交互

#### 添加表单元素

**基本补充：**

```
👤 You: "Add a section for personal information"
🤖 AI: "Added a personal information panel with standard fields"

👤 You: "Include a file upload for resume"
🤖 AI: "Added a secure file upload component for documents"

👤 You: "Add a dropdown for country selection"
🤖 AI: "Added a country dropdown with common options"
```

**详细规范：**

```
👤 You: "Add a personal information panel with fields for full name, date of birth, phone number, and email address"
🤖 AI: "Created a personal information panel with all requested fields and appropriate validation"

👤 You: "Include a secure file upload component for documents, limited to PDF files under 5MB"
🤖 AI: "Added a file upload field with PDF restriction and 5MB size limit"

👤 You: "Add a country dropdown with options for USA, Canada, UK, and Germany"
🤖 AI: "Added a country dropdown with the specified options"
```

#### 创建动态行为

**简单的逻辑：**

```
👤 You: "Show additional fields when 'Other' is selected"
🤖 AI: "Created a conditional rule that shows additional fields when 'Other' is chosen"

👤 You: "Make the email field required"
🤖 AI: "Updated the email field to be required with validation"

👤 You: "Calculate the total automatically"
🤖 AI: "Added calculation logic to automatically compute totals"
```

**复杂的业务规则：**

```
👤 You: "Show the spouse information fields only when marital status is set to 'Married'"
🤖 AI: "Created a conditional rule that displays spouse fields based on marital status"

👤 You: "Calculate the total cost by multiplying quantity and price, then add 10% tax"
🤖 AI: "Added calculation logic with quantity, price, and tax computation"

👤 You: "Enable the submit button only when all required fields are completed and terms are accepted"
🤖 AI: "Created validation logic that enables submission only when all conditions are met"
```

#### 表单布局和设计

**布局更改：**

```
👤 You: "Make this a multi-step form"
🤖 AI: "Converted the form to a progressive layout with navigation"

👤 You: "Organize fields in two columns"
🤖 AI: "Updated the layout to display fields in a two-column arrangement"

👤 You: "Convert to an accordion layout"
🤖 AI: "Transformed the form to use accordion-style sections"
```

**设计改进：**

```
👤 You: "Create a wizard-style form with 3 steps: personal info, preferences, and review"
🤖 AI: "Created a wizard form with three distinct steps and navigation"

👤 You: "Arrange the address fields in a compact two-column layout"
🤖 AI: "Organized address fields in a compact two-column format"

👤 You: "Update the layout to match the attached wireframe"
🤖 AI: "Modified the layout to match the provided design reference"
```

### 集成设置

Forms Experience Builder可以配置各种提交端点，以将表单与外部系统和服务连接：

| 集成类型 | 设置命令 | 用例 |
|------------------|---------------|----------|
| **电子邮件** | “将表单发送到电子邮件” | 表单提交的通知和确认 |
| **REST API** | “提交到REST端点” | 自定义应用程序和第三方系统 |
| **云存储** | “保存到Azure/SharePoint” | 文档存储和文件管理 |
| **工作流** | “连接到Power Automate” | 业务流程自动化和批准 |
| **营销** | “与Marketo集成” | 商机管理和营销自动化 |

**高级集成示例：**

```
👤 You: "Send form submissions to hr@company.com and create a case in our CRM system"
🤖 AI: "Configured email submission and CRM integration"

👤 You: "Submit data to our REST API endpoint and trigger the new customer workflow"
🤖 AI: "Set up REST API submission with workflow triggers"

👤 You: "Email responses to the sales team and add the lead to our marketing automation platform"
🤖 AI: "Configured multi-channel submission with email and marketing automation"
```





## 高级表单操作


### 复杂规则创建

创建完善的验证和业务逻辑，以响应用户交互并确保数据完整性：

```
👤 You: "Show the address section only if the user selects 'Ship to different address'"
🤖 AI: "Created a conditional rule that shows/hides the address panel based on checkbox selection"
```

### 多步骤表单创建

```
👤 You: "Create a progressive form with 3 steps: personal info, preferences, confirmation"
🤖 AI: "Created a progressive form with navigation between steps and validation at each stage"
```

### 高级字段类型

* 文件上传具有文档管理的验证和大小限制
* 具有用于计划的约束和业务规则的日期选取器
* 包含动态选项（根据用户选择而更改）的下拉列表
* 用于复杂决策树的带条件逻辑的单选按钮


### PDF到表单的转换

```
👤 You: "Convert this PDF into an interactive form"
🤖 AI: "Analyzed the PDF and created a form with appropriate field types and validation"
```

### 表单转换的URL

```
👤 You: "Create a form from this website"
🤖 AI: "Extracted form elements and created a native AEM Form with enhanced functionality"
```

### 性能分析

```
👤 You: "Analyze this form's conversion performance"
🤖 AI: "Provided insights on form effectiveness and suggested optimizations"
```

### 高级自定义

#### 自定义验证规则

* 基于用户输入创建动态表单行为的字段依赖项
* 根据用户需求调整表单体验的复杂条件逻辑
* 为用户提供明确指导的自定义错误消息
* 跨字段验证，确保跨多个输入的数据一致性

#### 布局优化

* 移动响应能力，可确保表单在所有设备上无缝工作
* 无障碍合规性使表单可供残障人士使用
* 改进的可视化设计，可提升用户参与度和完成率
* 减少摩擦并提高满意度的用户体验增强功能

#### 集成工作流

* 通过业务工作流传递表单提交的多步骤审批流程
* 将表单数据转换为外部系统所需格式的数据转换
* 将特定规则和计算应用于表单提交的自定义业务逻辑
* 高级错误处理，提供从系统问题中正常恢复的功能

## 命令引用

### 基本命令

| 符号 | 用途 | 使用方法 |
|--------|---------|------------|
| `/` | 快速操作和快捷键 | 键入`/create`以创建表单，`/help`以获得帮助 |
| `@` | 引用现有表单字段 | 键入`@fieldName`以修改特定字段（例如，`@email`） |
| 纯文本 | 自然对话 | 描述您想要的内容：“添加必填电话号码字段” |

### 斜杠命令

| 命令 | 上下文 | 使用示例 |
|---------|---------|---------------|
| `/create-form` | 所有环境 | `/create-form customer survey` |
| `/add-form` | 通用编辑器 | `/add-form contact form` |
| `/update-layout` | 表单编辑器 | `/update-layout wizard with 3 steps` |
| `/update-field` | 表单编辑器 | `/update-field @email to be required` |
| `/create-rule` | 表单编辑器 | `/create-rule show @spouse if married` |
| `/create-panel` | 表单编辑器 | `/create-panel Personal Information` |
| `/configure-submit` | 表单编辑器 | `/configure-submit to email support` |
| `/help` | 所有环境 | `/help multi-step forms` |

### 字段引用

使用 `@fieldName` 引用现有字段：

* `@firstName`，`@lastName` *名称字段
* `@email`，`@phoneNumber` *联系人字段
* `@address`、`@city`、`@zipCode` *地址字段
* `@dateOfBirth`，`@startDate` *日期字段

### 组件类型

描述表单元素时，请使用以下术语：

* `text input` *单行文本字段
* `text area` *多行文本字段
* `dropdown` *选择包含选项的列表
* `checkbox` *单个复选框
* `checkbox group` *多个复选框
* `radio group` *单选按钮组
* `date picker` *日期选择字段
* `file upload` *文件附件字段
* `panel` *分组字段的容器

### 集成命令

| 服务 | 自然语言命令 | 要求 |
|---------|--------------------------|--------------|
| 电子邮件 | “将提交内容发送到[电子邮件]” | 有效的电子邮件地址 |
| REST API | “提交到REST终结点[URL]” | API端点和凭据 |
| Azure Storage | “将文件保存到Azure存储” | 存储帐户配置 |
| SharePoint | “存储在SharePoint [站点]中” | SharePoint站点访问 |
| Power Automate | &quot;触发Power Automate流程&quot; | 流量配置 |
| Marketo | “将潜在客户添加到Marketo” | Marketo API凭据 |

### 提示

1. **使用自然语言**： AI理解复杂的请求并可以解释详细的要求
2. **具体说明**：详细描述产生更好的结果和更准确的表单生成
3. **迭代**：通过对话优化表单以获得完美的用户体验
4. **利用上下文**：引用现有的表单元素，以基于您现有的表单元素进行构建
5. **彻底测试**：验证所有用户方案以确保表单按预期工作

## 产品帮助和学习

Forms Experience Builder还可以向您讲授AEM Forms的功能：

### 提出如下问题：

* “如何创建多步骤表单？”
* “面板和部分有什么区别？”
* “如何设置电子邮件通知？”
* “适合移动设备的表单的最佳实践是什么？”
* “如何将主题应用到我的表单？”

### 获取以下方面的帮助：

* AEM Forms 概念和术语
* 复杂功能的分步说明
* 最佳实践和推荐
* 常见问题排查

## 最佳实践

### 表单设计

* **保持简单**：从基本字段开始，仅在必要时增加复杂性，以避免用户过多
* **使用清晰的标签**：使用描述性标签引导用户完成表单，以明确字段目的
* **提供帮助文本**：通过上下文帮助和示例引导用户完成复杂的字段
* **彻底测试**：验证所有用户路径，以确保表单在所有情况下都正常工作

### 用户体验

* **渐进式公开**：根据上下文显示相关字段以降低认知负载并提高完成率
* **清除导航**：帮助用户了解他们在表单中的位置以及剩余的步骤
* **响应式设计**：确保表单适用于所有设备和屏幕大小，从而最大限度地提高可访问性
* **辅助功能**：遵循WCAG准则，使残障人士能够使用表单

### 性能

* **优化字段计数**：仅请求必要的信息以减少表单放弃并提高完成率
* **使用适当的验证**：在提交之前避免出现错误，以提供立即反馈和指导
* **测试完成率**：通过分析和用户反馈监控和提高表单有效性
* **定期更新**：使表单与业务需求和用户期望保持同步，以获得最佳性能

### 品牌一致性

* **创建品牌模板**：在开始创建表单之前，使用您组织的颜色、字体和样式准备品牌表单模板
* **定义样式标准**：建立可在提示中引用的一致的按钮样式、字段布局和间距准则
* **使用品牌资产**：准备徽标、颜色代码和品牌准则，以便在创建表单时轻松参考
* **模板库**：为常见用例（联系人、注册、反馈）生成品牌化表单模板集合
* **样式提示**：包含特定于品牌的说明：“将公司蓝(#1234AB)用于按钮和公司字体Helvetica”

### 获得最佳效果的建议

**开始简单，生成**

* 从基本请求开始：“创建一个联系表单”
* 逐步添加详细信息：“为电子邮件字段添加验证”
* 测试并优化：“将电话字段设为可选”

**需要时为特定**

* 不要用：“把它设计得好看”
* 尝试：“使用专业的颜色和清晰的排版规则”

**使用自然语言**

* 不要用：“添加文本输入组件”
* 尝试：“添加一个名字字段”

**引用现有元素**

* 对现有字段使用 `@fieldName`：“将 @email 设为必填项”
* 具体说明字段名称：“更新 @phoneNumber 字段”

**划分复杂请求**

* 不要提出一个大的请求，而是尝试提出多个小的请求
* 逐步构建表单
* 在进入下一个步骤之前，先测试每一项更改

## 疑难解答

| 问题 | 快速修复 |
|-------|-----------|
| **接口未加载** | 刷新浏览器，检查互联网连接 |
| **命令不起作用** | 请尝试`/help`或改用自然语言 |
| **@fieldName无法识别** | 检查拼写，确保字段先存在 |
| **文件上传失败** | 在10MB以下使用PDF/JPG/PNG |
| **表单看起来错误** | 更具体一些：“使其对移动设备友好” |
| **集成失败** | 验证API凭据和权限 |

**仍需要帮助？**&#x200B;键入`/help`，后跟您的特定问题或联系您的系统管理员。

有关其他支持，请参阅主[Forms Experience Builder提示库](ai-assistant-prompt-library.md)，或与系统管理员联系以获得技术帮助。
