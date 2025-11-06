---
title: 部署和配置 Forms Experience Builder
description: 了解如何使用 Forms Experience Builder 为所有用户类型创建和管理采用渐进展开方式的表单
hide: true
index: false
hidefromtoc: true
role: Admin, Developer
exl-id: 977f227e-e941-4797-ba74-53d5b8c60ca9
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1404'
ht-degree: 75%

---

# 部署和配置 Forms Experience Builder

>[!NOTE]
>
> Forms Experience Builder可通过提前访问计划获得。 在开始之前，请确保您已请求并获得访问权限。 有关完整说明，请参阅[入门](product-overview.md#onboarding)信息。

>[!IMPORTANT]
>
> **文档可能会发生变化**：此文档目前正在针对产品进行测试，因此可能会进行更新和修订。随着 Forms Experience Builder 在早期访问计划期间不断改进，其功能、命令和示例可能会发生变化。

此综合指南可帮助您开始使用对话式 AI 技术创建和管理表单。无论您是想要创建第一个表单的初学者，还是想要利用复杂功能的高级用户，您都可以找到详细信息和实际示例，指导您了解 Forms Experience Builder 的各种功能。

## 先决条件和设置

### 满足访问权限要求

在使用Forms Experience Builder之前，请确保您已：

* **访问Forms Experience Builder** — 可通过提前访问计划获得
* **AEM Forms as a Cloud Service** — 具有自适应Forms核心组件的生产创作环境
* **基本了解** — 熟悉表单概念和业务要求

### 验证表单是否已启用

在使用 Forms Experience Builder 之前，请确保[您的环境已启用 AEM Forms](/help/forms/setup-forms-cloud-service.md)。

### 设置环境

您的设置过程取决于您的AEM Forms实施。 选择与项目匹配的路径。

用于Edge Delivery Services的&#x200B;****

如果您使用的是Edge Delivery Services Forms，并且主要使用通用编辑器。 [为Edge Delivery Services Forms准备项目](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)。 这是一次性设置，用于启用Forms Experience Builder。

基于核心组件的表单&#x200B;****

如果您在AEM创作环境中使用基于Core Components的自适应Forms，请确保为您的环境启用了[自适应Forms核心组件](/help/forms/enable-adaptive-forms-core-components.md)。



## 快速入门

### 访问表单体验生成器

您可以从三个主要位置访问Forms Experience Builder，具体取决于您的工作流和表单类型。


**1. 自适应Forms编辑器（用于核心组件）**

您可以在编辑特定表单时直接启动生成器。

1. 导航到&#x200B;**AEM > Forms > Forms和文档**。
1. [使用核心组件模板](/help/forms/creating-adaptive-form-core-components.md)创建新表单或打开现有表单。
1. 在编辑器工具栏中选择&#x200B;**Forms Experience Builder**&#x200B;图标以打开对话界面。

   ![AI 助手图标*](/help/edge/docs/forms/assets/adaptive-forms-editor.gif){width="75%"}

**1. 通用编辑器(用于Edge Delivery Services Forms)**

对于通过Edge Delivery Services交付的表单，生成器将集成到通用编辑器中。

1. 在通用编辑器中打开Edge Delivery Services表单。
2. 选择右侧面板中的&#x200B;**Forms Experience Builder**&#x200B;图标以启动对话界面。

### 您的第一个表单

| 对话示例 |   |
|--------------------------------------------------------------------------------------------------------------------------------------------|---|
| **尝试通过此对话创建一个综合联系表（基于 Summit 演示）：**<br><br>**您：**“创建一个用于获取个人信息的联系表，包括全名、电子邮件地址、电话号码、公司名称、职位和一个用于查询的消息字段”<br><br>**AI：**&#x200B;选择一个模板<br>    一个用于选择模板的下拉菜单&#x200B;<br><br>**AI：** 选择一个主题<br>    一个用于选择主题的下拉菜单&#x200B;<br><br>**AI：**&#x200B;创建表单 | ![您的第一个表单](/help/edge/docs/forms/assets/create-form.png) |
| <br>**AI：**&#x200B;打开创建的表单 | </br> 表单已创建并在编辑器中打开 |


### 基本命令

| 符号 | 用途 | 使用示例 |
|--------|---------|---------------|
| `/` | 快速操作和快捷方式 | `/create-form contact form`、`/help validation rules`、`/update-layout wizard` |
| `@` | 引用现有的表单字段 | `@email`、`@firstName`、`Make @phoneNumber required` |
| 纯文本 | 自然对话 | “添加一个必填的电话号码字段”，“创建电子邮件地址的验证方法” |

**具体命令示例：**

* `/create-form customer survey` - 创建一个新的客户意见调查表
* `/add-field @email validation` - 添加对现有电子邮件地址字段的验证
* `/create-rule show @spouse if @maritalStatus equals married` - 创建条件逻辑
* `/configure-submit to email support@company.com` - 设置电子邮件提交
* `/help multi-step forms` - 获取有关多步骤表单创建的帮助

### 成功提示

* **表述具体**：“添加一个必填的电子邮件地址字段和相关验证”比“添加电子邮件地址”效果更好
* **引用现有字段**：更改表格时使用 `@fieldName`
* **请求帮助**：输入 `/help` 后提出您的问题
* **采用迭代方法**：每次只进行一项更改，以获得最佳效果


## 开始创建表单的方法

### 从自然语言提示开始

用自然语言描述您的表单要求，Forms Experience Builder 会生成完整的表单结构：

**示例：**

* “创建一个包含个人信息、财务详细信息和文件上传功能的贷款申请表”
* “创建一个包含评分、评论和产品类别的客户反馈表”
* “我需要一个包含支付处理功能的多步骤会议报名表”


### 关键交互

#### 添加表单元素

**基本补充：**

    👤您：“添加一个个人信息分区”
    👤您：“添加一个简历文件上传功能”
    👤您：“添加一个用于选择国家/地区的下拉菜单”

**详细说明要求：**

    👤您：“添加一个个人信息面板，其中包含全名、出生日期、电话号码和电子邮件地址等字段”
    👤您：“添加一个用于安全上传文档文件的组件，仅限 5MB 以下的 PDF 文件”
    👤您：“添加一个国家/地区下拉菜单，其中包含美国、加拿大、英国和德国等选项”

#### 创建动态行为

**简单的逻辑：**

    👤您：“用户选择了‘其他’时，显示附加字段”
    🤖AI：“创建了一个条件规则，在选择了‘其他’时会显示附加字段”
    
    👤您：“将电子邮件地址字段设为必填项”
    🤖AI：“已将电子邮件地址字段更新为必填项，并添加了验证”
    
    👤 您：“自动计算总和”
    🤖 AI：“添加了自动计算总和的计算逻辑”

**复杂的业务规则：**

    👤您：“只有当婚姻状况被选为‘已婚’时，才显示配偶信息字段”
    🤖AI：“创建了一个根据婚姻状况显示配偶字段的条件规则”
    
    👤您：“通过数量乘以价格来计算总成本，然后加上 10% 的税”
    🤖 AI：“添加了数量、价格和税额计算的计算逻辑”
    
    👤 您：“只有在所有必填字段都填写完整且条款被接受后，才允许使用提交按钮”
    🤖 AI：“创建了只有在满足所有条件后才允许提交的验证逻辑”

#### 表单布局和设计

**布局更改：**

    👤您：“将这个表单做成一个多步骤表单”
    🤖AI：“已将表单转换为一个带导航的渐进展开式布局”
    
    👤您：“将字段排成两列”
    🤖AI：“已更新布局，字段显示为两列排列”
    
    👤您：“转换为一种折叠式布局”
    🤖AI：“已将表单转换为折叠样式的分区”

**设计改进：**

    👤您：“创建一个向导样式的表单，包含以下三个步骤：个人信息、偏好设置和评价”
    🤖AI：“创建了一个包含三个不同步骤和导航的向导式表单”
    
    👤您：“将地址字段排列成一个紧凑的两列布局”
    🤖AI：“已将地址字段组织成一个紧凑的两列格式”
    
    👤您：“更新布局，使其符合附件中的线框”
    🤖AI：“已按照所提供的设计参考更改了布局”

### 提交配置

Forms Experience Builder 可以配置各种提交端点，将您的表单与外部系统和服务连接起来：

| 提交操作类型 | 设置命令 | 用例 |
|------------------|---------------|----------|
| **电子邮件** | “将表单发送到电子邮件地址” | 表单提交的通知和确认 |
| **REST API** | “提交到 REST 端点” | 自定义应用程序和第三方系统 |
| **云存储** | “保存到 Azure/SharePoint” | 文档存储和文件管理 |
| **工作流** | “提交至 Power Automate” | 业务流程自动化和审批 |
| **营销** | “与 Marketo 集成” | 潜在客户管理和营销自动化 |

**高级提交配置示例：**

    👤您：“将表单提交到 hr@company.com，并在我们的 CRM 系统中创建一个案例”
    🤖AI：“已配置电子邮件提交和 CRM 提交操作”
    
    👤您：“将数据提交到我们的 REST API 端点，并触发新客户工作流”
    🤖AI：“已设置 REST API 提交并触发了工作流”
    
    👤您：“将回复用电子邮件发送给销售团队，并将潜在客户添加到我们的营销自动化平台”
    🤖AI：“已配置电子邮件和营销自动化的多渠道提交”





## 高级表单操作


### 复杂规则创建

创建复杂的验证和业务逻辑来响应用户交互以及确保数据完整性：

    👤您：“只有当用户选择了‘运送至另一个地址’后才显示地址分区”
    🤖AI：“创建了一个根据复选框的选择来显示/隐藏地址面板的条件规则”

### 多步骤表单创建

    👤您：“创建一个渐进展开式表单，其中包含 3 个步骤：个人信息、偏好设置、确认”
    🤖AI：“创建了一个包含步骤之间导航和每个阶段进行验证的渐进展开式表单”

### 高级字段类型

* 采取验证和大小限制的文件上传功能，用于文档管理
* 受约束的日期选取器和用于安排计划的业务规则
* 带有动态选项的下拉菜单，可根据用户选择而变化
* 带有条件逻辑的单选按钮，形成复杂的决策树


### PDF到表单的转换

    👤您：“将这个 PDF 转换为一个交互式表单”
    🤖AI：“已分析 PDF，并创建了一个包含适当字段类型和验证的表单”





## 产品帮助和学习

Forms Experience Builder 还可以让您了解有关 AEM Forms 功能的知识：

### 提出以下问题：

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


如需更多支持，请参阅主要 [Forms Experience Builder 提示词库](/help/forms/experience-builder/forms-experience-builder-prompt-examples-library.md)，或者联系您的系统管理员寻求技术帮助。
