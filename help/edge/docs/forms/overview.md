---
title: 适用于 AEM Forms 的 Edge Delivery Services 概述
description: 适用于AEM Forms的Edge Delivery Services专为实现卓越性能而构建，使您能够预见未来简化数据收集和用户参与。
feature: Edge Delivery Services
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
role: Admin, Architect, Developer
source-git-commit: 67fe933807f8a1bca681a6bcee7164f7c117bcac
workflow-type: tm+mt
source-wordcount: '1874'
ht-degree: 7%

---


# AEM Edge Delivery Services上的Forms快速入门

<span class="preview">这是一项预发行功能，可通过我们的[预发行渠道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=zh-Hans#new-features)访问。</span>

本指南可帮助您使用Adobe Experience Manager (AEM) Edge Delivery Services (EDS)了解和实施表单。 无论您是创建简单的联系人表单还是复杂的数据收集工具，本页都会向您介绍您的选项。

## 了解Edge Delivery Services中的Forms

Edge Delivery Services是Adobe的现代化解决方案，用于以卓越的性能和灵活性交付Web内容（包括表单）。 通过在表单中使用Edge Delivery Services，您可以：

* **提供更快的体验：** Forms加载速度惊人，因为它们是从邻近用户的边缘服务器的全局网络(CDN)中提供的。 这提高了用户满意度，并可提高表单完成率。
* **更轻松地更新Forms：** Edge Delivery Services方法通常允许更快的开发周期和内容更新，因此您可以快速调整表单。
* **构建响应式新式Forms：**&#x200B;创建外观出众、可在任何设备上无缝工作的表单。
* **从可扩展性和可靠性中获益：**&#x200B;您的表单将像基础边缘基础架构一样强大且可扩展。

本指南将：

* 解释您可以为Edge Delivery Sites创建（创作）表单的各种方式。
* 向您说明如何配置用户提交表单后发生的情况（提交操作）。
* 帮助您根据特定需求和团队技能选择最佳方法。
* 提供架构图和最佳实践。

## 您应了解的关键术语

* **Edge Delivery Services (EDS)：** Adobe通过CDN提供AEM内容的性能优先的架构。 也称为富兰克林计划。
* **AEM Forms：** Adobe用于创建、管理和处理表单的解决方案。
* **通用编辑器(UE)：**&#x200B;用于AEM内容（包括表单）的可视WYSIWYG编辑器。
* **基于文档的创作：**&#x200B;使用Microsoft Word或Google Docs/工作表创建表单。
* **文档创作(DA)：** Adobe托管的服务，用于为Edge Delivery Services创作内容（包括可以托管表单的页面）。
* **Forms提交服务(FSS)：**&#x200B;一种Adobe服务，可简化将表单数据发送到电子表格或电子邮件的过程。
* **AEM发布实例：**&#x200B;可处理复杂表单提交的实时AEM环境。
* **CORS（跨源资源共享）：**&#x200B;一种浏览器安全功能，在嵌入来自不同域的表单时需要配置此功能。
* **CDN （内容分发网络）：**&#x200B;服务器网络，可根据用户的地理位置快速为其提供Web内容。


**Edge Delivery Services表单交互的概念图**

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
此图显示了用户与通过CDN快速投放的表单进行交互的情况。 然后它们提交的数据由后端系统处理。

## Forms如何在Edge上运行？

使用EDS，您的网站内容（包括表单结构）可以源自各种来源，如AEM as a Cloud Service、SharePoint、Google Drive或文档创作(DA)服务。 然后，将此内容发布到全局CDN。 当用户访问您的网站时，将从最近的CDN边缘服务器直接提供内容，从而确保实现最高速度。

<!--*   **Where AEM Forms Fit In**
    Forms in an EDS architecture are designed to be:
    *   **Fast Loading:** Form structures are often simple HTML rendered client-side.
    *   **Decoupled:** The visual part of the form (frontend) is separate from where the data goes after submission (backend).
    *   **Flexible to Create:** You have different tools to build your forms.
    *   **Configurable for Submission:** You can send data to simple services or powerful AEM backends.-->

**简化的Forms Edge Delivery Services架构**

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

![架构](/help/forms/assets/eds-simplified-architecture.png)
此图显示了历程：表单在创作系统中定义，发布到边缘，提供给用户，提交的数据由后端处理。

## 选择表单创作方法

您可以通过三种主要方式为Edge Delivery Services站点创建表单。 您的选择将取决于您团队的技能、表单的复杂性和项目需求。

### 哪种创作方法适合您？

使用此决策树帮助您选择：

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

![选择正确的平台](/help/forms/assets/eds-authoring-selection.png)

此决策树可帮助您根据团队和表单需求选择创作方法。

### 使用文档创建Forms (Word/Google Docs)

如果您的团队熟悉Microsoft Word或Google Docs/工作表[，则此方法非常适用于快速](/help/edge/docs/forms/create-forms.md)创建表单。

**工作方式：从文档到Web窗体**

您可以使用特殊表格格式或“表单块”直接在Word文档或Google工作表中定义表单的字段、标签和类型。 发布此文档时，Edge Delivery Services会自动将其转换为用户可在您的网站上与之交互的适用于Web的HTML表单。

**功能和特性**

* 在熟悉的工具中创作：Word、Google Docs、Google Sheets。
* 定义字段：文本输入、电子邮件、下拉列表、复选框、单选按钮、文本区域。
* 添加标签、占位符和帮助消息。
* 设置基本验证规则：必填字段、电子邮件格式。
* 集成reCAPTCHA以保护垃圾邮件。
* 允许文件上传。
* 立即发布：文档中的更改会快速反映在实时网站上。
* 使用自定义代码扩展：高级用户可以通过GitHub添加自定义表单组件和样式。

**注意事项**

* 您的团队会定期使用Word或Google Docs/Sheets获取内容。
* 您需要快速创建从简单到中等复杂的表单。
* 您希望通过最少的设置将表单数据直接发送到电子表格或电子邮件地址。

**提交的工作方式(主要是Forms提交服务)**

Forms以此方式创建，通常会[将其数据发送到AEM Forms提交服务](/help/forms/forms-submission-service.md)。 您将配置此项（通常在源文档本身）以将数据发送到Google工作表、OneDrive/SharePoint上的Excel文件或电子邮件。

**基于文档的创作概念**
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
此图显示了文档中定义的表单如何变成实时Web表单。

### 使用通用编辑器以可视方式显示Forms

[通用编辑器](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)提供了一个现代化的拖放界面，可直接在Web浏览器中构建表单。

**工作方式：拖放表单生成**

您可以使用可视化界面将表单组件（如输入字段、按钮、下拉列表）拖动到页面上。 然后，您可以通过属性面板配置每个组件的属性（标签、验证等）。 通用编辑器可让您实时预览表单。

**功能和特性**

* 使用预建组件库创建可视化表单。
* 配置实时验证和业务逻辑（例如，根据选择显示/隐藏字段）。
* 查看不同设备（桌面、移动设备）的实时预览。
* 与AEM功能(如内容片段、AEM工作流和用户权限)集成。
* 使用“Experience Builder”获得使用提示创建或编辑表单的AI帮助。

**注意事项**

* 您需要使用条件逻辑、多步骤面板或个性化来构建复杂表单。
* 您的团队（例如，营销人员、企业用户）更喜欢可视化工具。
* 您需要与AEM as a Cloud Service紧密集成，以便在表单中进行治理、工作流或使用AEM资源。

**提交的工作方式(Forms提交服务或AEM发布)**

使用通用编辑器构建的Forms可以：

* 使用简单的[Forms提交服务](/help/forms/forms-submission-service.md)（用于将数据发送到电子表格或电子邮件）。
* 将数据提交到AEM Publish实例以进行更高级的处理(例如，启动AEM工作流、使用表单数据模型或与其他企业系统集成)。

**通用编辑器概念**

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

![通用编辑器](/help/forms/assets/eds-ue-based.png)

此图显示了用于构建表单的通用编辑器的主要部分。

### 将Forms用于文档创作(DA)

[Document Authoring (DA)](https://www.aem.live/developer/da-tutorial)是一项由Adobe托管的服务，用于创建和管理将通过Edge Delivery Services交付的主要网站内容（页面、文章）。 它是使用SharePoint或Google Drive作为Edge Delivery Services源内容的替代方法。

**了解Edge Delivery Services内容的文档创作(DA)**

文档创作使用Adobe的设计系统(Spectrum)和AEM的文档模型(Blocks， Sections)，提供了一个企业级创作环境。 它专为EDS的结构化内容管理而设计。

**DA如何处理Forms（嵌入，而非直接创作）**

DA本身&#x200B;**不是从头开始构建表单的工具**。 相反，您使用DA创建网页，然后将&#x200B;*嵌入*&#x200B;表单（使用基于文档的创作或通用编辑器创建的）到这些DA创作的页面中。

**将Forms嵌入到DA页面的步骤**

1. **创建表单：**&#x200B;使用以下任一方式生成表单：
   * 基于文档的创作(Word/Google Docs)
   * 通用编辑器

1. **发布您的表单：**&#x200B;请确保此表单已发布，并且可通过其自己的Edge Delivery URL访问（例如，`https://your-eds-project.hlx.page/forms/contact-us`）。
1. **在DA中创作您的页面：**&#x200B;在“文档创作”中创建或编辑您希望在其中显示表单的页面。
1. **嵌入表单：**&#x200B;在DA页面中使用特定的“块”或组件引用并嵌入其URL中的表单。 然后，DA页面将获取并显示此外部创建的表单。

**嵌入表单的文档创作**
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

此图显示您首先使用UE或文档创建表单，然后将其嵌入到在“文档创作”中构建的页面。


### 比较创作选项

| 标准 | 基于文档的创作 | 通用编辑器(WYSIWYG) | 文档创作(DA)中的Forms |
|----------------------------------|---------------------------------------|-----------------------------------------|-------------------------------------------|
| **主要创作工具** | Word/Google Docs/工作表 | 浏览器(AEM通用编辑器) | 不适用(Forms为&#x200B;*嵌入式*) |
| **团队技能级别** | 熟悉文档编辑器 | 熟悉可视化Web工具 | 将DA用于页面内容 |
| **典型表单复杂性** | 从简单到适中 | 中等到复杂，企业级 | 取决于嵌入的形式 |
| **提交选项1 （简单）** | Forms提交服务（至工作表/电子邮件） | Forms提交服务（至工作表/电子邮件） | 遵循嵌入式表单的设置 |
| **提交选项2 （高级）** | 不适用 | AEM Publish（工作流、FDM等） | 遵循嵌入式表单的设置 |
| **AEM后端集成** | 最小 | 高(使用AEM发布提交) | 通过嵌入的通用编辑器表单间接进行 |
| **最适合……** | 内容团队快速创建简单表单，快速捕获数据。 | 需要可视化控制、复杂表单或深度AEM集成的营销人员、业务用户。 | 在DA中管理主要内容的站点，需要来自其他来源的表单。 |

**增强决策树**
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

## 创作方法的功能比较

下表详细比较了不同 AEM 表单创作方法的主要功能，帮助您选择最适合您需求的方法。&#x200B;

| **功能** | **通用编辑器（所见即所得）** | **基于文档的创作** | **文档创作(DA)** |
|-----------------------------------------|-------------------------------|-----------------------------|-----------------------------|
| **统一构成网站** | ✅ |                              | ✅ （含嵌入表单） |
| **嵌入表单支持** | ✅ | ✅ | ✅ （从通用编辑器或文档嵌入） |
| **规则（动态行为）** | 带有自定义函数的高级规则编辑器 | 有限制：显示/隐藏、计算值、自定义函数 | 取决于嵌入的形式 |
| **附件支持** | ✅ | ℹ️（早期访问） | 取决于嵌入的形式 |
| **验证码支持** | reCAPTCHA Enterprise | reCAPTCHA Enterprise | 取决于嵌入的形式 |
| **提交功能** | REST、电子邮件、FDM、工作流、SharePoint、OneDrive、Azure Blob、Power Automate、Workfront Fusion (EA) | 仅限电子表格 | 遵循嵌入式表单的设置 |
| **数据架构** | FDM，自定义 | 自定义 | 基于嵌入式表单 |
| **预填充** | 💡 （通过向导） | ✅ | 取决于嵌入的形式 |
| **片段** | ✅ | ✅ | 取决于嵌入的形式 |
| **可视化规则编辑器** | ✅ |                              |                              |
| **本地化** | 💡 （通过站点） | ℹ️ （Excel/Sheets手册） | 取决于嵌入的形式 |
| **数据架构（数据树）** | 💡 （通过UI扩展） |                              |                              |
| **模板支持** | 仅初始内容 |                              |                              |
| **门户** |                               |                              |                              |
| **主题** | ℹ️（在项目层面） | ℹ️（在项目层面） | ℹ️（基于托管站点） |
| **自定义组件** | ✅ | ✅ | ✅ （如果嵌入的组件支持它） |
| **OOTB 与自定义函数** | ✅ | ✅ | ✅（嵌入形式） |
| **片段引用** |                               |                              |                              |
| **Sign 集成** |                               |                              |                              |
| **试验** | ✅ | ✅ | 取决于嵌入上下文 |
| **通过 Workfront 进行任务管理** | ✅ |                              |                              |
| **个性化扩展** | 💡 |                              |                              |
| **编辑器自定义** | ✅ （通过UI扩展） |                              |                              |
| **提交操作** | ✅ | 仅限电子表格 | 基于嵌入式表单 |

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

为了在您所学知识的基础上再接再厉，您可以采取以下措施：

[选择您的提交策略](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)决定您的项目是需要Forms提交服务的简单性（适用于电子表格/电子邮件输出），还是需要AEM发布提交操作提供的灵活性和后端集成。

请参阅[创建Forms的最佳实践](/help/edge/docs/forms/universal-editor/best-pratices-eds-forms.md)一文，了解如何设计有效、可访问且用户友好的表单。

## 后续步骤

本指南概述了如何将表单与AEM Edge Delivery Services结合使用。 有关特定配置的更多详细分步说明，请参阅Adobe Experience Manager官方文档：

* [使用Edge Delivery Services Forms进行基于文档的创作](/help/edge/docs/forms/tutorial.md)
* [带有Edge Delivery Services Forms的通用编辑器](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
* [文档创作(DA)和嵌入内容](https://www.aem.live/developer/da-tutorial)
* [AEM Forms提交服务](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)


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
