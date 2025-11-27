---
title: 表单创建技能
description: 了解Experience Production Agent的表单创建技能以及如何使用自然语言从头开始创建表单。
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: 01fce6fcdf1c8ada0422a84fccb9a89f395e2a0e
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 0%

---


# 表单创建技能 {#form-creation-skill}

表单创建技能是Experience Production Agent的一项功能，旨在使用自然语言提示开发表单。 此技能可自动生成适当的表单结构和字段类型。 该技能通过AI助手显现出来。

表单创建技能的一些主要优势包括：

* **加速表单开发**：使用以下方式快速创建表单
简单的自然语言命令，无需学习传统的产品界面。
* **一致的品牌内体验**：使用批准的模板和样式创建遵循您组织的品牌、模板和样式准则的表单。
* **技术壁垒更低**：允许业务用户轻松创建表单，而无需高级技术或深入的产品专业知识。

## 功能 {#capabilitiess}

* **创建具有纯文本提示的新表单**：您可以通过以纯语言提交您的要求来创建表单。 该代理会根据您的自然语言描述和指定的模板自动生成相应的表单结构、字段类型和品牌上体验。 此功能可加快表单创建，同时确保维护品牌和合规性标准。

* **导入PDF文档并将其转换为表单**：您可以将现有PDF文档导入并转换为表单。 代理程序会分析上传的内容以检测字段类型、保留布局并使用响应式设计和验证逻辑增强表单，同时确保维护品牌和合规性标准。

  使用以上任何功能时，系统都会提示您选择要创建的表单类型，指定基于核心组件的自适应表单模板或基于Edge Delivery Services的自适应表单模板，并指示您保存表单的首选路径。 如果您基于Edge Delivery Services创建表单，则还可以指定存储库的GitHub URL。


### 示例提示 {#sample-prompts}

* *创建包含名称、电子邮件和消息字段的反馈集合表单*
* *创建包含产品评级（1-5星）、评论字段和可选电子邮件的客户反馈表单*
* *构建包含姓名、电子邮件、主题下拉列表和消息字段的联系人表单*
* *创建包含个人信息、帐户首选项和条款接受的注册表*
* *通过导入位于“https://[aem-author-url]/path/to/pdf/file*”的PDF文件来创建信用卡申请表
* *使用位于“<https://github.com/wkndforms/wesecure>”的样板创建反馈表单*

## 优化您的表单 {#refine-with-forms-experience-builder}

使用AI助手创建初始表单结构后，您可以使用Forms Experience Builder来：

* **更新表单**：通过可视编辑器添加或修改字段，调整字段类型，并根据需要更新样式。

* **更新布局**：重新排列节、组或字段，调整间距并修改可视层次结构以增强可用性并确保表单对受众清晰直观。

* **添加业务逻辑**：创建条件逻辑、显示/隐藏规则、字段依赖关系，并定义验证规则。

* **配置提交**：配置提交表单数据的位置，包括设置电子邮件通知、与工作流的集成或连接到外部系统。

有关详细信息，请参阅[Forms Experience Builder文档](/help/forms/experience-builder/product-overview.md)。


## 激活 {#activation}

要为贵组织启用Experience Production Agent，必须通过Adobe启动激活。 通过以下方式联系客户以开始此过程：

* 电子邮件： `experience-production-agent@adobe.com`
* 或者，联系您指定的Adobe客户团队。

在联系时，请确保提供您的AEM as a Cloud Service组织ID。


<!-- 
#### Import and convert {#import-and-convert}

Transform existing documents into interactive digital forms. The agent analyzes uploaded content to detect field types, preserve layouts, and enhance forms with responsive design and validation logic. Supported formats include Acroforms, XFA PDFs, flat PDFs, images (JPG, PNG), and hand-drawn form photographs.

>[!VIDEO](https://video.tv.adobe.com/v/3474042)

**Prompt examples:**

* *Convert the attached PDF file to an adaptive form*
* *Transform this scanned form image into an interactive digital form*
* *Import the employee onboarding PDF and create an editable form*
* *Convert this paper form photograph into a digital form with validation*
-->

<!-- 
### Embed an existing form to a sites page {#embed-existing-form}

The form creation skill enables seamless integration of existing forms into any sites page through natural language commands. Rather than manually locating, copying, and embedding form components, users can simply specify which form to add and where to place it. The agent handles the technical implementation, ensuring proper rendering and functionality.

>[!VIDEO](https://video.tv.adobe.com/v/PLACEHOLDER)

**Prompt examples:**

* *Embed the contact form to the homepage*
* *Add the existing customer feedback form to the support page*
* *Insert the newsletter signup form into the footer section*
* *Place the registration form on /content/site/signup*
* *Add form "contact-us-2024" to the current page*
-->

<!-- 
### Build and add a form to an existing sites page {#build-and-add-form}

The form creation skill combines form creation and site integration in a single conversational workflow. Users can describe the form they need and specify where to add it, and the agent creates the form and embeds it into the specified page automatically. This eliminates the traditional multi-step process of creating a form separately and then manually adding it to a page.

>[!VIDEO](https://video.tv.adobe.com/v/PLACEHOLDER)

**Prompt examples:**

* *Create a newsletter signup form with email field and add it to the footer*
* *Build a quick contact form with name, email, and message, then add it to /content/about-us*
* *Add a feedback form with rating stars and comment field to this page*
* *Create a simple survey form with 5 questions and embed it on the customer portal homepage*
* *Build an event registration form with name, email, and date selection, then add it to /content/events/conference-2025*
-->
