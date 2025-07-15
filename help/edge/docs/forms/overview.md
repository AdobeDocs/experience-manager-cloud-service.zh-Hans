---
title: 适用于 AEM Forms 的 Edge Delivery Services 概述
description: 适用于 AEM Forms 的 Edge Delivery Services 专为实现最佳性能而构建，让您能够畅想简化数据收集和用户参与的未来。
feature: Edge Delivery Services
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
role: Admin, Architect, Developer
source-git-commit: 67fe933807f8a1bca681a6bcee7164f7c117bcac
workflow-type: tm+mt
source-wordcount: '1874'
ht-degree: 100%

---


# 入门指南：在 AEM Edge Delivery Services 中使用表单

<span class="preview">这是一项预发行功能，可通过我们的[预发行渠道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=zh-hans#new-features)访问。</span>

本指南将帮助您了解并实施 Adobe Experience Manager (AEM) Edge Delivery Services (EDS) 中的表单功能。无论是创建简单的联系表单，还是构建复杂的数据采集工具，此页面都会引导您了解相关选项。

## 了解 Edge Delivery Services 中的表单功能

Edge Delivery Services 是 Adobe 为实现卓越性能和敏捷交付而打造的现代 Web 内容交付方案，其中支持表单等内容类型。使用 Edge Delivery Services 表单，您将获得以下优势：

* **更快的体验交付：**&#x200B;表单加载速度极快，因为它们是通过靠近用户的全球边缘服务器网络（CDN）进行交付的。这有助于提升用户满意度，并可能提高表单完成率。
* **更轻松地更新表单：** Edge Delivery Services 的架构通常支持更快速的开发周期和内容更新，使您能够更灵活地调整表单内容。
* **构建现代化响应式表单：**&#x200B;创建在各类设备上均具有出色外观和顺畅体验的表单。
* **受益于可扩展性与高可靠性：**&#x200B;您的表单将具备与底层边缘架构同等的强大稳定性与可扩展性。

本指南将会：

* 讲解如何为您的 Edge Delivery 站点创建（编写）表单的多种方式。
* 演示如何配置用户提交表单后的处理方式（提交操作）。
* 帮助您根据具体需求和团队技能选择最合适的方法。
* 提供架构图示与最佳实践建议。

## 您应了解的关键术语

* **Edge Delivery Services (EDS):** Adobe 面向性能优先的架构，通过 CDN 交付 AEM 内容。也称为 Project Franklin。
* **AEM Forms:** Adobe 提供的表单创建、管理与处理解决方案。
* **Universal Editor （UE）：**&#x200B;款所见即所得（WYSIWYG）的可视化编辑器，用于创建 AEM 内容，包括表单。
* **Document-Based Authoring：**&#x200B;通过 Microsoft Word 或 Google Docs/Sheets 创建表单的方式。
* **Document Authoring（DA）：** Adobe 托管的内容创作服务，用于为 Edge Delivery Services 创建内容（包括可嵌入表单的页面）。
* **Forms Submission Service（FSS）：** Adobe 提供的一项服务，用于简化将表单数据发送至电子表格或电子邮件的流程。
* **AEM Publish Instance：**&#x200B;用于处理复杂表单提交的线上 AEM 环境。
* **CORS（跨源资源共享）：**&#x200B;一种浏览器安全机制，当从不同域嵌入表单时需要进行相应配置。
* **CDN（内容分发网络）：**&#x200B;由多个服务器组成的网络，根据用户的地理位置快速传输网页内容。


**Edge Delivery Services 表单交互概念图示**

<!--  
```mermaid
graph LR
    User[User on Device] >|Interacts| EdgeForm[Edge-Delivered Form Page]
    EdgeForm >|Loads Instantly| CDN[CDN Edge Server]
    CDN >|Serves Content| User
    EdgeForm >|Submits Data| Backend[Backend Processing - e.g. Forms Submission Service / AEM Publish]
    style User fill:#f9f,stroke:#333,stroke-width:2px
    style EdgeForm fill:#ccf,stroke:#333,stroke-width:2px
    style CDN fill:#9cf,stroke:#333,stroke-width:2px
    style Backend fill:#fca,stroke:#333,stroke-width:2px
``` -->

![表单交互](/help/forms/assets/eds-form-interaction.png)
该图展示了用户与通过 CDN 快速交付的表单之间的交互过程。用户提交的数据随后由后端系统进行处理。

## 表单在 Edge 上如何运行？

借助 EDS，您的网站内容（包括表单结构）可以来自多种来源，如 AEM as a Cloud Service、SharePoint、Google Drive 或 Document Authoring（DA）服务。这些内容随后会发布到全球 CDN 网络中。当用户访问您的网站时，内容将直接从距离最近的 CDN 边缘服务器提供，从而实现极致的加载速度。

<!--*   **Where AEM Forms Fit In**
    Forms in an EDS architecture are designed to be:
    *   **Fast Loading:** Form structures are often simple HTML rendered client-side.
    *   **Decoupled:** The visual part of the form (frontend) is separate from where the data goes after submission (backend).
    *   **Flexible to Create:** You have different tools to build your forms.
    *   **Configurable for Submission:** You can send data to simple services or powerful AEM backends.-->

**简化的 Edge Delivery Services 表单架构图示**

<!--
```mermaid
    graph TD
        UserStart[<img src='https://img.icons8.com/ios-filled/50/000000/user.png' width='30' /> User on Device] >|Interacts| EdgeForm[Edge-Delivered Form Page]
        EdgeForm >|Loads Instantly| CDN[CDN Edge Server]
        CDN >|Serves Content| UserEnd[<img src='https://img.icons8.com/ios-filled/50/000000/user.png' width='30' /> User on Device]
        EdgeForm >|Submits Data| Backend[Backend Processing - Form Submission Service / AEM Publish]

        style UserStart fill:#f9f,stroke:#333,stroke-width:2px
        style UserEnd fill:#f9f,stroke:#333,stroke-width:2px
        style EdgeForm fill:#ccf,stroke:#333,stroke-width:2px
        style CDN fill:#9cf,stroke:#333,stroke-width:2px
        style Backend fill:#fca,stroke:#333,stroke-width:2px
``` -->

![架构说明](/help/forms/assets/eds-simplified-architecture.png)
本图展示了整个流程：表单在创作系统中定义，发布至边缘，传递给用户，提交的数据由后端系统处理。

## 选择表单创作方式

您可以通过三种主要方式为 Edge Delivery Services 站点创建表单。您的选择将取决于团队的技能水平、表单的复杂程度以及项目需求。

### 哪种创作方式最适合您？

请参考以下决策树，帮助您做出选择：

**表单创作决策树**
<!--    
```mermaid
    graph TD
        A{Start: I need to create a form for an Edge Delivery Services site} > B{What are my team's primary content creation tools & skills?}
        B -- "We mainly use Word / Google Docs / Sheets" > C{How complex is the form and where does the data need to go?}
        B -- "We use AEM and prefer visual tools (Marketers or Designers)" > D[Use Universal Editor - WYSIWYG]
        B -- "Our site content is managed in Document Authoring (DA)" > E[Use Document Authoring - Embed Forms]
        C -- "Simple to moderate form, data to a spreadsheet or email" > F[Use Document-Based Authoring]
        C -- "More complex logic or needs AEM backend integration" > D
        E > G[Create form using Document-Based Authoring or Universal Editor, then embed in your DA page]

        style A fill:#f9f,stroke:#333,stroke-width:2px
        style F fill:#ccf,stroke:#333,stroke-width:2px
        style D fill:#ccf,stroke:#333,stroke-width:2px
        style G fill:#ccf,stroke:#333,stroke-width:2px
``` -->

![选择合适的平台](/help/forms/assets/eds-authoring-selection.png)

此决策树可根据您的团队构成与表单需求，帮助您选择合适的创作方式。

### 使用文档（Word/Google Docs）创建表单

如果[您的团队熟悉使用 Microsoft Word 或 Google Docs/Sheets](/help/edge/docs/forms/create-forms.md)，此方法非常适合快速创建表单。

**工作原理：从文档到网页表单**

您可在 Word 文档或 Google Sheets 中，使用特定的表格格式或“表单区块”直接定义表单字段、标签和类型。当您发布该文档后，Edge Delivery Services 会自动将其转换为可在网站中交互使用的 HTML 网页表单。

**功能与特性**

* 可在熟悉的工具中进行创作：Word、Google Docs、Google Sheets。
* 支持定义字段类型：文本输入、电子邮件、下拉菜单、复选框、单选按钮、多行文本框等。
* 添加标签、占位符和帮助信息。
* 设置基本验证规则：必填字段、电子邮件格式等。
* 集成 reCAPTCHA 以防止垃圾提交。
* 支持文件上传功能。
* 即时发布： 您在文档中的修改可快速同步至线上站点。
* 支持自定义代码扩展：高级用户可通过 GitHub 添加自定义表单组件和样式。

**注意事项**

* 您的团队经常使用 Word 或 Google Docs/Sheets 进行内容创作。
* 您需要快速创建简单到中等复杂度的表单。
* 您希望将表单数据直接发送到电子表格或电子邮件地址，且只需最小化配置。

**提交原理（主要使用 Forms Submission Service）**

通过此方式创建的表单通常会[将数据发送至 AEM Forms Submission Service](/help/forms/forms-submission-service.md)。您可在源文档中配置它，以将表单数据发送至 Google Sheets、存储于 OneDrive/SharePoint 的 Excel 文件，或作为电子邮件发送。

**文档式创作概念**
<!--    
```mermaid
    graph LR
        subgraph Authoring["You define your form in a Google Sheet or Word Document"]
        Sheet[Spreadsheet or Document with field definitions:\nField Name - Type - Label\nemail - email - Email Address\nmessage - textarea - Your Message]
    end

        Sheet >|Edge Delivery Services automatically converts it| JSON[Internal Form Definition as JSON]
    JSON >|A 'Form Block' on your page renders it as| HTMLForm[Live HTML Form on Your Website]

        style Sheet fill:#e6ffe6,stroke:#333
        style JSON fill:#e6e6ff,stroke:#333
        style HTMLForm fill:#ffe6e6,stroke:#333
```-->

![基于文档](/help/forms/assets/eds-doc-based.png)
该图示展示了如何将文档中定义的表单转化为可在线使用的网页表单。

### 使用 Universal Editor 进行可视化表单创建

[ Universal Editor ](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)提供了一种现代化的拖放式界面，可直接在网页浏览器中创建表单。

**工作原理：拖放式表单构建**

您可以使用可视化界面，将表单组件（如输入字段、按钮、下拉菜单等）拖放至页面中。随后，您可通过属性面板配置每个组件的属性，如标签、验证规则等。使用 Universal Editor 可实时预览您正在构建的表单。

**功能与特性**

* 提供可视化表单创建界面，内置丰富的预构建组件库。
* 支持配置实时验证和业务逻辑（例如：根据选项显示/隐藏字段）。
* 可实时预览不同设备（桌面端、移动端）上的表单效果。
* 支持与 AEM 功能集成，例如内容片段、AEM 工作流和用户权限管理。
* 借助“Experience Builder”，通过提示词获取 AI 协助来创建或编辑表单。

**注意事项**

* 您需要构建具备条件逻辑、多步骤面板或个性化体验的复杂表单。
* 您的团队成员（如市场营销人员或业务用户）更倾向于使用可视化工具。
* 您需要与 AEM as a Cloud Service 紧密集成，以实现治理、工作流管理，或在表单中使用 AEM 资产。

**提交原理（使用 Forms Submission Service 或 AEM Publish 实例）**

使用 Universal Editor 创建的表单可以：

* 使用简单的 [Forms Submission Service](/help/forms/forms-submission-service.md)，将数据发送至电子表格或电子邮件。
* 将数据提交至 AEM Publish 实例，以进行更高级的处理（例如启动 AEM 工作流、使用表单数据模型，或与其他企业系统集成）。

**Universal Editor 概念说明**

<!--    
```mermaid
    graph TD
    subgraph UE_Interface["Universal Editor Interface in your Browser"]
        Toolbar[Editor Toolbar and Asset Finder]
        Canvas[Your Page with the Form Being Built]
        ComponentPalette[Available Form Components:\nInput / Dropdown / Button\nDrag and drop]
        PropertiesPanel[Configure Selected Component:\nLabel / Validation / Rules]
    end
    ComponentPalette >|Drag & Drop onto| Canvas
    Canvas >|Select a component to edit its| PropertiesPanel
    UE_Interface >|Creates| RenderedForm[Live Form on Your Website]

    style UE_Interface fill:#f0f8ff,stroke:#333
    style RenderedForm fill:#ffe6e6,stroke:#333
```-->

![ Universal Editor ](/help/forms/assets/eds-ue-based.png)

该图展示了 Universal Editor 中用于构建表单的主要部分。

### 在文档创作（DA）中使用表单

[文档创作（DA）](https://www.aem.live/developer/da-tutorial)是 Adobe 托管的服务，用于创建和管理网站主要内容（如页面和文章），这些内容将通过 Edge Delivery Services 进行交付。它是使用 SharePoint 或 Google Drive 来管理 Edge Delivery Services 源内容的替代方案。

**了解用于 Edge Delivery Services 内容的文档创作（DA）**

文档创作采用 Adobe 的设计系统（Spectrum）与 AEM 的文档模型（如 Blocks、Sections），提供企业级的创作环境。该工具专为 EDS 提供结构化内容管理而设计。

**DA 如何处理表单（嵌入，而非直接创作）**

DA 本身并&#x200B;**不是用于从零开始构建表单的工具**。相反，您应使用 DA 创建网页内容，并将表单（这些表单通过文档式创作或 Universal Editor 创建）*嵌入*&#x200B;到这些由 DA 编写的页面中。

**将表单嵌入 DA 页面中的步骤**

1. **创建表单：**&#x200B;使用以下任一方式构建表单：
   * 文档式创作方式（Word/Google Docs）
   *  Universal Editor 

1. **发布表单：**&#x200B;确保该表单已发布，并可通过其独立的 Edge Delivery URL 访问（例如：`https://your-eds-project.hlx.page/forms/contact-us`）。
1. **在 DA 中创建页面：**&#x200B;在文档创作中创建或编辑页面，以指定表单出现的位置。
1. **嵌入表单：**&#x200B;在 DA 页面中使用特定的“区块”或组件，通过表单的 URL 引用并嵌入该表单。DA 页面随后将会获取并显示该外部创建的表单。

**在文档创作中嵌入表单**
<!--
```mermaid
    graph TD
    subgraph FormCreation["1. Create Form using other methods"]
        UE_Form[Universal Editor Form] >|Published to| FormLocation[Form lives at its own Edge Delivery Services URL:\nfor example: /forms/my-contact-form]
        DocBased_Form[Document-Based Form] >|Published to| FormLocation
    end

    subgraph DA_Content["2. Author Page in Document Authoring"]
        DAPage[Your Web Page Authored in DA\nExample: /main-site/landing-page]
        EmbedBlock[On DA Page, add 'Embed Form' Block\nPoints to /forms/my-contact-form]
    end

    DAPage > EmbedBlock
    User[User visits your DA Page] > DAPage
    EmbedBlock >|DA Page fetches and displays| FormLocation[The Form appears on your DA Page]

    style FormCreation fill:#e6ffe6,stroke:#333
    style DA_Content fill:#ffe6cc,stroke:#333
    style FormLocation fill:#ccf,stroke:#333
```-->

![文档创作](/help/forms/assets/eds-da-based.png)

该图示说明您需先使用 Universal Editor 或文档来创建表单，再将其嵌入至通过文档创作构建的页面中。


### 对比不同的创作方式

| 标准 | 文档式创作 |  Universal Editor （所见即所得） | 在文档创作（DA）中使用表单 |
|----------------------------------|---------------------------------------|-----------------------------------------|-------------------------------------------|
| **主要创作工具** | Word/Google Docs/Sheets | 浏览器（AEM  Universal Editor ） | 不适用（表单以&#x200B;*嵌入*&#x200B;形式使用） |
| **团队技能水平** | 熟悉文档编辑器 | 熟练使用可视化网页工具 | 使用 DA 进行页面内容创作 |
| **典型的表单复杂度** | 简单到中等复杂度 | 中等至复杂，支持企业级表单需求 | 取决于所嵌入的表单 |
| **提交方式选项 1（简单）** | 使用 Forms Submission Service（提交至电子表格或电子邮件） | 使用 Forms Submission Service（提交至电子表格或电子邮件） | 遵循嵌入表单的设置方式 |
| **提交方式选项 2（高级）** | 不适用 | AEM Publish（工作流、FDM 等） | 遵循嵌入表单的设置方式 |
| **AEM 后端集成能力** | 最小 | 高度集成（通过 AEM Publish 提交） | 以嵌入的 Universal Editor 表单方式间接集成 |
| **最适合...** | 内容团队快速创建简单表单，实现高效数据采集。 | 营销人员或业务用户需要可视化控制、复杂表单或深入 AEM 集成。 | 主体内容由 DA 管理的网站，需要从其他来源嵌入表单。 |

**增强版决策树**
<!--
```mermaid
    graph TD
    A{Start Here: I need a form on my Edge Delivery Services Site} > B{What's my team's main authoring tool & skill for form content?};
    B -- "Word/Google Docs" > C{How complex is the form & data destination?};
    C -- "Simple form, data to Sheet/Email" > Sol1[CHOOSE: Document-Based Authoring + Forms Submission Service];
    C -- "Needs more logic OR AEM backend\nlike Workflow or FDM" > Sol2[CONSIDER: Can Universal Editor meet this need better?];

    B -- "AEM User / Visual Editor needed\nMarketer or Designer" > D{Where does the form data need to go?};
    D -- "Simple - to Sheet/Email" > Sol3[CHOOSE: Universal Editor + Forms Submission Service];
    D -- "Advanced - AEM Workflow, FDM,\n3rd Party via AEM" > Sol4[CHOOSE: Universal Editor + AEM Publish Submissions\nRequires additional setup];

    B -- "Our main site content is in Document Authoring (DA)" > Sol5[STRATEGY: Author form using Sol1, Sol2, Sol3 or Sol4 first\nTHEN embed that form into your DA page];

    A > F{Will this form be embedded or fetched from another site or domain?};
    F -- "Yes" > G[IMPORTANT: Configure CORS on the site hosting the form.\nEnsure any form JavaScript blocks are available where the form is displayed];

    style Sol1 fill:#90ee90,stroke:#333
    style Sol2 fill:#fffacd,stroke:#333
    style Sol3 fill:#90ee90,stroke:#333
    style Sol4 fill:#90ee90,stroke:#333
    style Sol5 fill:#add8e6,stroke:#333
    style G fill:#ffb6c1,stroke:#333
```-->

![决策树](/help/forms/assets/eds-enhanced-decision.png)

## 创作方式的功能比较

下表详细比较了不同 AEM 表单创作方法的主要功能，帮助您选择最适合您需求的方法。&#x200B;

| **功能** | **Universal Editor （所见即所得）** | **文档式创作** | **文档创作（DA）** |
|-----------------------------------------|-------------------------------|-----------------------------|-----------------------------|
| **与 Sites 的统一构成组合** | ✅ |                              | ✅（支持嵌入表单） |
| **嵌入表单支持** | ✅ | ✅ | ✅（可嵌入来自 Universal Editor 或文档的表单） |
| **规则（动态行为）** | 带有自定义函数的高级规则编辑器 | 有限制：显示/隐藏、计算值、自定义函数 | 取决于所嵌入的表单 |
| **附件支持** | ✅ | ℹ️（抢先体验） | 取决于所嵌入的表单 |
| **验证码支持** | reCAPTCHA Enterprise | reCAPTCHA Enterprise | 取决于所嵌入的表单 |
| **提交功能** | REST、电子邮件、FDM、工作流、SharePoint, OneDrive, Azure Blob、Power Automate、Workfront Fusion (EA) | 仅限电子表格 | 遵循嵌入表单的设置方式 |
| **数据架构** | FDM，自定义 | 自定义 | 遵循所嵌入的表单 |
| **预填充** | 💡（通过向导） | ✅ | 取决于所嵌入的表单 |
| **片段** | ✅ | ✅ | 取决于所嵌入的表单 |
| **可视化规则编辑器** | ✅ |                              |                              |
| **本地化** | 💡（通过 Sites） | ℹ️（Excel/Sheets 手册） | 取决于所嵌入的表单 |
| **数据架构（数据树）** | 💡（通过 UI 扩展） |                              |                              |
| **模板支持** | 仅限初始内容 |                              |                              |
| **门户** |                               |                              |                              |
| **主题** | ℹ️（在项目层面） | ℹ️（在项目层面） | ℹ️（基于托管网站） |
| **自定义组件** | ✅ | ✅ | ✅（如果嵌入式组件支持的话） |
| **OOTB 与自定义函数** | ✅ | ✅ | ✅（在嵌入的表单中） |
| **片段引用** |                               |                              |                              |
| **Sign 集成** |                               |                              |                              |
| **试验** | ✅ | ✅ | 取决于嵌入的上下文 |
| **通过 Workfront 进行任务管理** | ✅ |                              |                              |
| **个性化扩展** | 💡 |                              |                              |
| **编辑器自定义** | ✅（通过 UI 扩展） |                              |                              |
| **提交操作** | ✅ | 仅限电子表格 | 遵循所嵌入的表单 |

<!--

## Best Practices for Creating Forms

Building great forms goes beyond just the technology. Here's how to ensure your forms are user-friendly and achieve their goals:

* **Designing User-Friendly and Accessible Forms**

  *   **Use Clear, Visible Labels:** Every form field needs a `<label>`. Don't rely only on placeholder text (text inside the input field), as it disappears when users type and is bad for accessibility.
        *   *Good:* `<label for="email">Email Address:</label> <input type="email" id="email" placeholder="you@example.com">`
        *   *Bad:* `<input type="email" placeholder="Email Address">`
  *   **Keep it Simple:** Use standard HTML input types (`<input type="date">`, `<input type="tel">`) where possible. They often have better mobile support and accessibility than complex custom widgets.
  *   **Logical Order and Grouping:** Arrange fields in a way that makes sense to the user. Group related fields together using `<fieldset>` and `<legend>`.
  *   **Provide Clear Instructions:** For any fields that might be confusing, offer concise help text or tooltips.
  *   **Keyboard Navigation:** Ensure users can navigate through your entire form using only the keyboard (Tab, Shift+Tab, Enter, Spacebar).
  *   **Error Handling:** Make errors obvious and easy to correct. Display error messages next to the relevant field and explain what needs to be fixed.

* **Ensuring Your Forms Load Quickly and Are Visible**

  *   **Place Forms Prominently:** If a form is important, make sure users can see it easily without too much scrolling ("above the fold" if possible). Adobe's research shows many forms get low interaction because they are hidden.
  *   **Optimize Assets:** Keep any custom JavaScript or CSS for your forms as small as possible to ensure fast load times. Edge Delivery Services helps with the base page load, but heavy form scripts can still slow things down.

* **Handling User Data Responsibly**
  *   **Ask Only What You Need:** The less Personal Identifiable Information (PII) you ask for, the better. Every field is a potential reason for a user to abandon the form.
  *   **Be Transparent:** Clearly explain *why* you need certain information and *how it will be used*. Link to your privacy policy. This builds trust.

* **Improving User Experience: Captcha Alternatives**

  * **Rethink Visible Captchas:** Those "type the wavy text" or "click all the traffic lights" tests can be very frustrating for users, especially those with disabilities, and often lead to high drop-off rates.

*   **Consider Alternatives:**
    *   **Honeypot Fields:** Add a hidden field that only bots would fill out. If it has data, the submission is likely spam.
    *   **Time-Based Checks:** Measure how quickly a form is submitted. Submissions that are too fast are often bots.
    *   **Invisible reCAPTCHA (v3):** This Google service analyzes user behavior in the background and only presents a challenge if the user seems suspicious. This is often a much better user experience.

**Form Design Do's and Don'ts**

```mermaid
    graph LR
subgraph GoodFormUX [Do ✅ - For Better Forms]
    direction LR
    ClearLabels[Use Visible <label> Tags for All Fields]
    SimpleInputs[Prefer Standard HTML Input Types]
    KeyboardNav[Ensure Full Keyboard Navigation]
    ClearErrors[Show Clear, Actionable Error Messages]
    MinimalPII[Ask Only for Necessary Information]
    TransparentUse[Explain How Data is Used - Privacy Info]
    InvisibleCaptcha[Use Invisible or Behavioral CAPTCHA]
    ProminentPlacement[Make Form Easy to Find on Page]
end

subgraph BadFormUX [Don't ❌ - Avoid These]
    direction LR
    PlaceholderOnly[Only Use Placeholder Text for Labels]
    ComplexWidgets[Use Overly Complex Custom Widgets]
    PoorErrors[Vague or Missing Error Messages]
    ExcessivePII[Request Excessive Personal Data]
    VisibleHardCaptcha[Use Hard-to-Solve Visible CAPTCHAs]
    HiddenForm[Hide the Form Deep in the Page]
end

style GoodFormUX fill:#e6ffe6,stroke:#333
style BadFormUX fill:#ffe6e6,stroke:#333
```

## Quick Decision Guide: Choosing the Right Form Strategy

Let's bring it all together to help you decide on the best approach for your forms.

*   **Matching Form Features to Your Project Goals**
    *   **For speed and simplicity with basic data capture (to spreadsheets/email):** Document-Based Authoring with the Forms Submission Service is often your fastest route.
    *   **For visually rich forms with potential for AEM backend integration:** Universal Editor is your tool. You can start with the Forms Submission Service for simple needs and scale to full AEM Publish submissions for complex workflows.
    *   **If your site content is managed in Document Authoring (DA):** You'll create forms using one of the above methods and then embed them into your DA pages. The submission logic will be tied to how the original embedded form was configured.-->

为了进一步实践您所掌握的内容，您可以按以下方式继续推进：

[选择合适的提交策略](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)判断您的项目是需要 Forms Submission Service 的简洁方式（适用于输出至电子表格/邮件），还是 AEM Publish Submit Actions 提供的灵活性与后端集成能力。

请参阅[创建表单的最佳实践](/help/edge/docs/forms/universal-editor/best-pratices-eds-forms.md)文章，了解如何设计高效、可访问且用户友好的表单。

## 后续步骤

本指南概述了如何将表单与 AEM Edge Delivery Services 集成使用。如需更详细的配置步骤和说明，请参阅 Adobe Experience Manager 官方文档。

* [使用 Edge Delivery Services 表单进行文档式创作](/help/edge/docs/forms/tutorial.md)
* [使用 Universal Editor 与 Edge Delivery Services 表单](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
* [文档创作（DA）与内容嵌入](https://www.aem.live/developer/da-tutorial)
* [AEM Forms Submission Service](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)


<!-- 
# Edge Delivery Services for AEM Forms
 

Edge Delivery Services for AEM Forms is a composable set of services that enables a rapid development environment where authors can update, publish, and launch new forms rapidly. These services deliver exceptional and high impact forms experiences that drive engagement and conversions. These forms experiences are easy to author and develop.

These services enable you to:

* **Create enrolment experiences with tools of your choice:** Increase authoring efficiency by decoupling content sources. Out of the box you can use Document-based Authoring (Microsoft SharePoint or Google Drive), WYSIWYG Authoring (Universal Editor or Adaptive Forms Editor). You can work with multiple content sources on the same forms site and use your preferred authoring tools, such as Microsoft Excel, Google Sheets, Universal Editor, or Adaptive Forms Editor.

* **Deliver exceptional Digital Enrolment experiences:** Deliver Digital Enrolment experiences that load and render quickly and continuously monitor your forms performance through Operational Telemetry. Faster loading times and optimized user experience contribute to higher form completion and conversion rates. 

* **Use developer friendly toolset:** Edge Delivery Services for AEM Forms
 uses plain HTML, modern CSS, and vanilla JavaScript to create exceptional experiences, avoiding the steep learning curve of a specific framework. A developer with basic web development skills can customize and easily build form components and experiences. There is no need to wait for a pipeline to run, just check-in your code into GitHub and your changes are live.

## Edge Delivery Services for AEM Forms Overview {#edge-overview}

Edge Delivery Services for AEM Forms allows for a high degree of flexibility in how you author forms on your website. You can author content and forms with [WYSIWYG Authoring](/help/forms/creating-adaptive-form-core-components.md) as well as [Document-based Authoring](/help/edge/docs/forms/create-forms.md). Edge Delivery Services for AEM Forms
 provide a forms block, known as [Adaptive Forms Block](/help/edge/docs/forms/create-forms.md) to add a form to your Edge Delivery Services site.

For example, you author forms directly in Microsoft Excel or Google Sheets and these spreadsheets are transformed into forms for your website. Any new form or form content, such as a new form field, is instantly available on your website without requiring a rebuild process.

The following diagram illustrates how you can edit forms in Microsoft Excel or Google Sheets (Document-based Authoring) and publish to Edge Delivery Services. It also shows the AEM publishing method using the WYSIWYG Authoring (Universal Editor or Adaptive Forms Editor).

![Publish to Edge Delivery Services and AEM](/help/edge/docs/forms/assets/AEM-forms-with-EDS-publishing.png)

Edge Delivery Services for AEM Forms uses GitHub so customers can manage and deploy code directly from their GitHub repository. For example, you can write forms in either [Google Sheets](/help/edge/docs/forms/create-forms.md) or [Microsoft Excel](/help/edge/docs/forms/create-forms.md) and the components of your forms can be developed by using CSS and JavaScript in a GitHub repository.

When your forms are ready, you can use the [AEM Sidekick](/help/edge/docs/forms/tutorial.md#preview-and-publish-your-content), a chrome browser extension, to preview and publish content updates.

![Install AEM SideKick](/help/edge/assets/aem-sidekick-preview-publish-forms.png)

The choice between the [Document-based Authoring ](#document-based-authoring-features) and [WYSIWYG Authoring](#wysiwyg-authoring-features) depends on your specific requirements:

* For simple forms that just collect basic information with a few fields (think contact us forms, lead generation forms, or service request forms), and where you need quick data connectivity using a spreadsheet, the [Document-based Authoring](#document-based-authoring-features) is a good fit. You can build these forms like you would build a document in Google Sheets or Microsoft Excel. 

* For complex forms, like forms requiring multiple panels, complex rules and business logic, data manipulation, integration with external systems, or streamlined workflows using AEM features, then [WYSIWYG Authoring](#wysiwyg-authoring-features) is a better option. 


### Key Features of Document-based Authoring and WYSIWYG Authoring

Document-based Authoring offers a basic set of features and WYSIWYG Authoring unlocks additional capabilities beyond the Document-based Authoring, empowering you to build more complex and interactive forms. The key features of both Document-based Authoring and WYSIWYG Authoring are:

#### Document-based Authoring features

Document-based Authoring  allows you to create forms using familiar tools like Microsoft Excel or Google Sheets. These forms offer the following functionalities:

* Accessible components for a user-friendly experience.
* Standardized HTML structure for consistent rendering.
* Rules and validations to ensure data accuracy.
* File attachment options for collecting additional information.
* Google reCAPTCHA integration for spam protection.
* Ability to create custom form components for specific needs.
* Submit form data directly to Microsoft Excel or Google Sheets or email addresses.
* Monitor your forms performance through Operational Telemetry

#### WYSIWYG Authoring features

WYSIWYG Authoring provides WYSIWYG interfaces (Universal Editor and Adaptive Forms Editor) for building forms and offers all the capabilities of Document-based Authoring, plus a wide range of additional features:

* Advanced rules editor for creating complex logic.
* Server-side extensibility for custom functionalities.
* WYSIWYG editing experience for easy form creation and visualization.
* Document of record functionality to create tamper-proof archives of submitted data.
* Integration with Adobe Sign for electronic signatures.
* Integration with Adobe Workfront Fusion to triggering Adobe Workfront Fusion scenarios upon form submission.
* Integration with various data sources for pre-populating forms and submitting data.
* Form Data Model (FDM) for defining data structure and interactions with various data sources.
* Ability to choose from multiple submit actions for handling form submissions, including submitting data to Microsoft SharePoint, Microsoft OneDrive, Adobe Workfront Fusion, Salesforce, Microsoft Dynamics, many more data sources.

The all above features are also available via Adaptive Forms Editor. 

In essence, WYSIWYG Authoring (Universal Editor and [Adaptive Forms Editor](/help/forms/creating-adaptive-form-core-components.md)) builds upon the foundation of [Document-based Authoring](/help/edge/docs/forms/create-forms.md), providing a more advanced toolkit for creating and managing complex forms. 

>[!NOTE]
>
>
> The WYSIWYG Authoring capability is available under the early-adopter program. If you are interested, send a quick email from your work address to aem-forms-ea@adobe.com to request access to the capability.

### Edge Delivery Services for AEM Forms

: Authoring, Publishing, and Submission of Forms  

The following diagrams illustrate the process of creating, publishing, and submitting forms using Document-based Authoring and WYSIWYG Authoring.

![Document-based Authoring](/help/edge/assets/document-based-authoring-workflow.png)

![WYSIWYG Authoring](/help/edge/assets/wysiwyg-authoring-workflow.png)

## Start creating forms

* [Get started with Edge Delivery Services for AEM Forms](/help/edge/docs/forms/tutorial.md)
* [Create a form using Google Sheets or Microsoft Excel](/help/edge/docs/forms/create-forms.md)
* [Set up your Google Sheets or Microsoft Excel files to start accepting data​](/help/edge/docs/forms/submit-forms.md)
* [Publish your form and start collecting data](/help/edge/docs/forms/publish-forms.md)
* [Customize the look of your forms​](/help/edge/docs/forms/style-theme-forms.md)
* [Add repeatable sections to a form​](/help/edge/docs/forms/repeatable-forms.md)
* [Show a custom thank you message after form submission​](/help/edge/docs/forms/thank-you-page-form.md)
* [Adaptive Form Block components and their properties](/help/edge/docs/forms/form-components.md)
* [Real Use Monitoring](https://www.aem.live/developer/rum#authentication)

<!-- 

## Start creating forms

<div>

  <style>
    .card-container {
        width: calc(33.33% - 10px);;
        margin: 5px;
        border: 1px solid #ccc;
        border-radius: 5px;
        padding: 5px;
        box-sizing: border-box;
        transition: background-color 0.3s ease; /* Adding transition effect */
    }
    .card-container:hover {
        background-color: #f0f0f0; /* Changing background color on hover */
    }
</style>

<div style="display: flex; flex-wrap: wrap; justify-content: space-between; margin: -5px;">
    <div class="card-container">
        <a href="/help/edge/docs/forms/create-forms.md">
            <img src="/help/edge/assets/smock_devices_18_n.svg" alt="Create a form using Edge Delivery Services forms" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Create a form using Google Sheets or Microsoft Excel</b>
        </a>
        <p>Create forms that load and render quickly and automatically reflows on mobile devices.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/create-forms.md#manually-configure-a-spreadsheet-to-accept-data">   
            <img src="/help/edge/assets/smock_platformdatamapping_18_n.svg" alt="Submit form" alt="Use Form Fragments in an Edge Delivery Services Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Submit form to spreadsheet</b>
        </a>
        <p>Submit forms directly to your Microsoft Excel or Google Sheets.</p>
    </div>
     <div class="card-container">
        <a href="/help/edge/docs/forms/style-theme-forms.md">
            <img src="/help/edge/assets/smock_imageautomode_18_N.svg" alt="Apply styles or themes to an Edge Delivery Services form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Customize a theme</b>
        </a>
        <p>Create a consistent brand image by applying the same theme across forms.</p>
    </div>
      <div class="card-container">
        <a href="/help/edge/docs/forms/validate-forms.md">
            <img src="/help/edge/assets/smock_condition_18_n.svg" alt="Add validations to form fields" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Apply field validations</b>
        </a>
        <p>Reduce errors and frustration by checking form inputs for proper formatting.</p>
    </div> 
            <div class="card-container">
        <a href="/help/edge/docs/forms/rules-forms.md">
            <img src="/help/edge/assets/smock_documentfragment_18_n.svg" alt="Use rules to add dynamic behaviour to a form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Use rules to add dynamic behaviour to a form</b>
        </a>
        <p>Reuse preconfigured fragments across multiple forms.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/translate-forms.md">  
            <img src="/help/edge/assets/smock_abc_18_n.svg" alt="Translate an Edge Delivery Services Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Translate a form</b>
        </a>
        <p>Extend the reach of your forms while keeping costs in check.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/repeatable-forms.md">  
            <img src="/help/edge/assets/smock_addto_18_n.svg" alt="Add repeatable sections to an Edge Delivery Services Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Add repeatable sections</b>
        </a>
        <p>Effortlessly create and add repeatable sections to a form.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/custom-components-forms.md"> 
            <img src="/help/edge/assets/smock_userdeveloper_18_n.svg" alt="Create custom forms components using standard JavaScript and CSS"  style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Create custom components</b>
        </a>
        <p>Use standard JavaScript and CSS to create components and themes.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/recaptacha-forms.md">  
            <img src="/help//edge/assets/smock_keyclock_18_n.svg" alt="Use reCAPTCHA in an Edge Delivery Services Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Use reCAPTCHA</b>
        </a>
        <p>Use OOTB reCAPTCHA integration for robust spam and bot protection.</p>
    </div>


</div>


</br>


-->
