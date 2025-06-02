---
title: AEM Forms的AI助手(Forms Experience Builder)
description: 使用表单片段更快地制作强大的表单
feature: Edge Delivery Services
hide: true
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: 67416999d068af6350748d610e7c1c7b1d991bc4
workflow-type: tm+mt
source-wordcount: '1657'
ht-degree: 2%

---

# AEM Forms的AI助手(Forms Experience Builder)

>[!NOTE]
>
>
> AEM Forms AI助手(Forms Experience Builder)功能在率先采用者项目中提供。 如果您有兴趣，请通过您的工作地址向mailto:aem-forms-ea@adobe.com发送一封快速电子邮件，请求访问功能。


AEM Forms AI助手(Forms Experience Builder)通过自然语言提示简化常见的表单构建任务，从而增强您的创作体验。 它在Forms Manager、自适应Forms编辑器和通用编辑器中提供，通过支持创建和配置操作，使您能够更智能、更快速地构建。 本指南将帮助您入门并充分利用其功能。

## 快速入门

在深入了解之前，让我们先了解访问和与AI助手交互的基础知识。

### 访问AI助手

您可以从AEM Forms中的三个不同位置访问AI助手：

1. **Forms Manager**
   - 导航到： Adobe Experience Manager > Forms > Forms和文档
   - 在界面左侧查找AI助手图标
   - 单击图标以打开AI助手面板

   ![AI助手图标*](/help/edge/docs/forms/assets/forms-manager.gif)

2. **自适应Forms编辑器**
   - 导航到： Adobe Experience Manager > Forms > Forms和文档
   - 选择并打开表单进行编辑
   - 单击编辑器界面中的AI助手图标

   ![AI助手图标*](/help/edge/docs/forms/assets/adaptive-forms-editor.gif)

3. **Universal Editor**

   - 导航到： Adobe Experience Manager > Forms > Forms和文档
   - 在界面左侧查找AI助手图标
   - 单击编辑器界面中的AI助手图标

AI Assistant会根据您当前的位置和任务调整其功能，为每个上下文提供相关帮助。

### 如何进行交互：

- 只需用自然语言键入您的请求即可。
- 使用`/`查看可用命令或快速操作列表。
- 需要助理配置或更新特定字段时，使用`@fieldName` （例如`@firstName`、`@emailAddress`）引用该特定表单字段。


### 快速入门

通过观看我们的介绍性视频，快速启动并运行：

>[!VIDEO](https://video.tv.adobe.com/v/3463164/)


本视频介绍在所有环境中启动助手、基本交互及其功能概述。

## AI Assistant命令参考

| 命令 | 描述 | 用途 | 使用上下文 | 示例 | 主要功能 |
|---------|-------------|---------|---------------|----------|--------------|
| /create-form | 在Forms Manager或Forms编辑器中启动新表单 | 从头开始创建全新的表单 | Forms Manager，自适应Forms编辑器 | /create-form客户反馈调查 | 提供表单结构的选项并创建表单 |
| /add-form | 在通用编辑器中添加新表单 | 在通用编辑器中添加新的表单块或组件 | Edge Delivery Services通用编辑器 | /add-form包含姓名和电子邮件的联系人表单 | 插入表单块，适用于基于块的编辑 |
| /update-layout | 将表单布局更改为可折叠项、基于选项卡、向导或单页响应式设计 | 修改整体结构布局和导航模式 | 所有编辑环境 | /update-layout向导，共3步 | 折叠、选项卡、向导、单页响应选项 |
| /update字段 | 修改现有表单字段的属性和配置 | 更改字段属性，如标签、验证、格式、行为 | 所有编辑环境 | /update-field@email验证为必填项 | 标签、验证规则、字段类型、默认值、可见性 |
| /create-rule | 为表单创建动态行为和条件逻辑 | 实施业务逻辑、计算、条件交互 | 所有编辑环境 | /create-rule在@maritalStatus等于“已婚”时显示@spouseName | 条件可见性、计算、验证、值设置 |
| /create-panel | 创建新面板（用于对相关字段进行分组的容器） | 添加结构容器以逻辑组织表单字段 | 所有编辑环境 | /create-panel个人信息，包括姓名、电子邮件、电话 | 字段分组、标题、布局选项、可折叠部分 |
| /add-panel | 在通用编辑器中将图像转换为表单面板 | 使用AI分析上传的图像并转换为结构化表单面板 | 通用编辑器 | /add-panel从上传的表单图像 | 图像识别、视觉到功能转换、布局保存 |
| /configure-submit | 设置表单提交操作和数据处理 | 定义用户提交完成的表单时会发生什么情况 | 所有编辑环境 | /configure-submit将电子邮件发送到`support@company.com` | 电子邮件、 REST API 、工作流、电子表格、数据库、 Power Automate |
| /help | 在AI助理中访问协助和文档 | 提供有关AEM Forms的上下文帮助、指导和答案 | 所有编辑环境 | /help如何创建多步表单？ | 功能解释、指南、最佳实践、故障排除 |

### 命令类别

| 类别 | 命令 | 主要用例 |
|----------|----------|-------------------|
| 表格创建 | /create-form， /add-form | 启动新表单，添加表单块 |
| 结构和布局 | /update-layout、/create-panel、/add-panel | 组织窗体结构、可视化设计 |
| 字段管理 | /update字段 | 配置单个表单元素 |
| 逻辑和规则 | /create-rule | 添加动态行为和验证 |
| 提交 | /configure-submit | 设置数据处理和工作流 |
| 支持 | /help | 获取帮助和文档 |

### 语法准则

| 元素 | 格式化 | 示例 | 注释 |
|---------|--------|---------|-------|
| 命令 | /command-name | /create-form | 始终以正斜杠开头 |
| 字段引用 | @fieldName | @email， @firstName | 对现有字段使用@符号 |
| 自然语言 | Command +说明 | /create-rule显示条件字段 | 将命令与描述性文本相结合 |
| 多个操作 | 单独的命令 | /create-panel然后/update-layout | 一次应用一个命令 |


### 特定于环境的功能

| 环境 | 可用命令 | 特殊功能 |
|-------------|-------------------|------------------|
| Forms Manager | /create-form， /help | 表单级创建和管理 |
| 自适应Forms编辑器和通用编辑器 | 所有命令 | 完整功能集，详细配置 |



### 字段引用语法（上下文元素）

使用`@fieldName`引用现有字段：

- `@firstName` — 名字字段
- `@email` — 电子邮件字段
- `@phoneNumber` — 电话号码字段
- `@dateOfBirth` — 出生日期字段

### 组件类型

此列表涵盖常见的组件类型。 AI可能会识别变体或更专业的类型，但使用这些精确术语会产生最佳结果：

- `text input` — 单行文本字段
- `text area` — 多行文本字段
- `dropdown` — 选择列表
- `checkbox` — 单个复选框
- `checkbox group` — 多个复选框
- `radio group` — 单选按钮组
- `date picker` — 日期选择
- `file upload` — 文件附件
- `panel` — 分组字段的容器


## 核心功能和扩展的提示示例

AI Assistant可理解各种命令。 下面是一些例子来说明它的力量。 请记住为组件使用精确的术语，如“面板”、“文本输入”、“复选框”等。

| 功能类别 | 描述 | 示例提示 |
| ------------------------- | --------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **表单创建** | 从头开始新表单或基于说明开始新表单。 | `Create a new form titled 'Employee Onboarding'.` <br> `Generate a customer feedback form with fields for name, email, rating (1-5 stars), and comments.` <br> `Start a simple contact form with name, email, and message fields.` <br> `Design a multi-page registration form for an event.` |
| **导入设计** | 将现有设计(图像、Figma、PDF)转换为AEM表单。 | `Import the form design from this uploaded PDF file.` <br> `Convert the uploaded Figma design into an adaptive form, focusing on the 'User Profile' frame.` <br> `Use this JPEG image of our old paper form to create a new digital version.` <br> `Create a form based on the layout of the attached PNG.` |
| **添加组件和面板** | 添加各种表单字段和结构容器（面板）。 | `Add a text input field for 'First Name'.` <br> `Add a 'Personal Details' panel with fields for full name, date of birth, and phone number.` <br> `Insert a checkbox group for 'Interests' with options: Technology, Sports, Music.` <br> `Add a file upload component for 'Resume'.` <br> `Create a repeatable panel named 'WorkExperience' with fields for company, title, and dates.` |
| **布局调整** | 修改窗体布局的结构和外观。 | `Change the 'Personal Details' panel to a two-column layout.` <br> `Set the overall form layout to a wizard (multi-step) navigation.` <br> `Make the header section span the full width of the form.` <br> `Adjust the spacing between fields in the 'Address' panel to be compact.` <br> `Align all field labels to the left.` |
| **规则创建和逻辑** | 实施动态行为、计算和条件可见性。 | `Make the 'Spouse Name' field visible only if 'Marital Status' is selected as 'Married'.` <br> `Calculate the 'Total Amount' by multiplying @quantity and @price.` <br> `Enable the submit button only when the @termsAndConditions checkbox is checked.` <br> `Set the value of @countryCode to '+1' if @country is 'United States'.` <br> `If @age is less than 18, show a message 'Must be 18 or older'.` |
| **字段属性更新** | 修改特定表单字段（如标签、占位符等）的属性。 | `Change the label of @email to 'Primary Email Address'.` <br> `Set the @comment field to be a multi-line text area.` <br> `Make the @phoneNumber field mandatory.` <br> `Add placeholder text 'Enter your ZIP code' to the @zipCode field.` <br> `Change the @country field to a dropdown and populate it with: USA, Canada, UK, Germany.` <br> `Update the help description for @password to 'Must include an uppercase letter, a number, and be at least 8 characters long.'` <br> `Set the maximum length of the @username field to 15 characters.` <br> `Configure the @dateOfBirth field to use a date picker.` |
| **提交操作** | 定义用户提交表单时将发生的情况。 | `Configure the form to submit data to the REST endpoint /api/v2/application-submit.` <br> `Set up an email submission to hr@example.com and sales@example.com on successful submission.` <br> `Trigger an AEM workflow named 'NewLeadProcessing' when this form is submitted.` <br> `On submit, redirect the user to a thank you page at /content/thankyou.html.` |
| **主题** | 应用现有AEM Forms主题以设置表单样式。 | `Apply the 'Modern Business' theme to this form.` <br> `Switch to the 'Accessible Dark' theme.` <br> `Revert to the default canvas theme.` |
| **导航和结构** | 添加导航元素或重新组织表单的各个部分。 | `Add a 'Next' button to the current panel and a 'Previous' button to the next panel.` <br> `Create a Table of Contents based on the form's panels.` <br> `Move the 'Address' panel to be before the 'Contact Information' panel.` |
| **验证** | 为字段设置特定的验证规则。 | `Set a regex pattern for the @employeeID field to be 'EMP\d{5}'.` <br> `Ensure the @age field only accepts numeric values between 18 and 99.` <br> `Validate the @email field to ensure it is a valid email format.` |
| **审阅计划** （通用编辑器） | 在执行之前预览助理的建议更改。 | `Add a contact form with fields for name, email, subject, and message.` （助理将显示其将创建的组件和属性计划，然后单击“应用”）。 |

## 获得最佳结果的最佳实践

要充分利用AI助手，请记住以下提示：

- **开始简单，增量生成：**&#x200B;开始使用更小的、特定的命令（例如，“为‘名字’添加文本输入”），而不是最初过于复杂的多步骤请求。
- **使用AEM Forms术语：**&#x200B;使用“面板”、“文本输入字段”、“复选框组”、“提交操作”、“规则”等术语，以便助理更好地理解。
- **明确引用字段：**&#x200B;配置现有字段时，请使用`@fieldName`表示法（例如，`Make @firstName mandatory`）。
- **审核计划**&#x200B;始终在单击“应用”之前仔细审核该助理在通用编辑器中提出的更改计划。
- **手动验证：**&#x200B;助理进行更改后，请始终预览和测试您的表单，以确保其行为与外观符合预期。 AI是一个功能强大的工具，但最终验证是关键。
- **迭代并优化：**&#x200B;如果第一个提示不能产生准确的结果，请尝试重新措辞或将请求细分为较小的步骤。
- **提供反馈：**&#x200B;使用内置反馈机制帮助助理学习和改进（请参阅“反馈与支持”部分）。

## AI助手的产品帮助

AEM Forms的AI Assistant不仅用于构建，还可以帮助您学习、理解和使用AEM Forms的各种功能。

### 支持的帮助主题

您可以向助理提问，例如：

- “如何从头开始创建新的自适应表单？”
- “自适应Forms中的面板是什么？如何使用它？”
- “解释如何将主题应用于表单。”
- “表单和面板支持哪些布局类型？”
- “如何配置不同的提交操作，如发送电子邮件？”
- “你能指导我使用菲格玛设计来创建表格吗？”
- “创建多步表单的最佳方法是什么？”

### 如何寻求帮助：

1. 在Forms管理器或自适应Forms编辑器中打开AI助手。
2. 用自然语言键入您的问题（例如，“如何添加可重复面板？”）。
3. 助理将作出以下回应：
   - 分步说明。
   - AEM Forms概念的解释。
   - 相关Adobe Experience League文档的链接（如果适用）。

### 获得更好帮助的提示：

- **具体说明：**&#x200B;一次询问一个明确的问题。
- **使用关键字：**&#x200B;包含与AEM Forms功能或UI元素相关的关键字（例如，“自适应表单编辑器”、“规则编辑器”、“主题”）。
- **如果需要，请改写：**&#x200B;如果助理不理解或无法提供所需信息，请尝试简化问题或使用不同的术语。


## 常见问题疑难解答

- **助理未响应：**
   - 确保在支持的环境(Forms Manager、自适应Forms编辑器或通用编辑器)中积极工作。
   - 检查互联网连接。
   - 尝试关闭AI助手面板并重新打开。

- **不准确或意外的响应：**
   - 重新声明您的请求，使其更具体或更简单。
   - 将复杂的请求划分为更小的单个命令。
   - 确保您使用的是标准的AEM Forms术语。

- **设计导入问题(PDF/Figma/Image)：**
   - 验证设计文件是否清晰、结构良好和可读。
   - 确保文件格式受支持(PDF、Figma链接、常见图像类型，如PNG、JPG)。
   - 对于Figma，请确保您定位的框架已明确定义并可访问。

- 无法识别&#x200B;**字段`@fieldName`：**
   - 双击表单中字段的确切名称。 字段名称区分大小写，且必须精确匹配。
   - 如果您尝试修改该字段，请确保该字段已存在。


## 反馈与支持

您的输入对AI助理的不断改进是无价的。

- **提供反馈：**&#x200B;使用内置的&#x200B;**“提供反馈”命令或AI Assistant界面中的按钮**&#x200B;共享您的体验、报告问题或建议增强功能。 （例如，您可以键入`/feedback`或查找反馈图标）。
- **官方支持：**&#x200B;对于严重问题或进一步的帮助，请通过官方Adobe支持渠道或您组织的指定支持联系人联系。


## 相关内容

[AEM Forms AI助手 — 提示库](/help/edge/docs/forms/ai-assistant-prompt-library.md)
