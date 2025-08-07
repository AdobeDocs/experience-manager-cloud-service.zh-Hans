---
title: 适用于 AEM Forms 的 Edge Delivery Services 概述
description: 使用 Adobe Experience Manager Edge Delivery Services 创建并分发高性能表单，重点采用通用编辑器创作方式。
feature: Edge Delivery Services
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
role: Admin, Architect, Developer
source-git-commit: ccfb85da187e828b5f7e8b1a8bae3f483209368d
workflow-type: tm+mt
source-wordcount: '879'
ht-degree: 100%

---


# 适用于 AEM Forms 的 Edge Delivery Services 


适用于 AEM Forms 的 Edge Delivery Services 是一组可组合的服务，可用于实现快速开发环境，作者可以在其中快速更新、发布和启动新表单。这些服务提供卓越且具有高影响力的表单体验，从而推动参与度和转化率。这些表单体验很容易创作和开发。

这些服务使您能够：

- **使用选定工具创建注册体验**：通过分离内容来源而提高创作效率。您可以使用开箱即用、基于文档的创作功能（Microsoft SharePoint 或 Google Drive）和所见即所得的创作功能（通用编辑器或自适应表单编辑器）。您可以在同一个表单网站上使用多个内容源，并使用首选的创作工具，如 Microsoft Excel、Google Sheets、通用编辑器或自适应表单编辑器。

- **提供卓越的数字注册体验：**&#x200B;提供快速加载和渲染的数字注册体验，并通过操作遥测持续监测表单性能。更快的加载时间和优化的用户体验有助于提高表单完成率和转化率。

- **使用易于开发人员使用的工具集：** 适用于 AEM Forms 的 Edge Delivery Services 使用纯 HTML、现代 CSS 和普通 JavaScript 来创建卓越的体验，避免特定框架所需的陡峭学习曲线。具有基本 Web 开发技能的开发人员可以自定义并轻松构建表单组件和体验。无需等待管道运行，只需将代码签入 GitHub，所做的更改就会生效。

## 选择创作方法


Adobe Experience Manager (AEM) Edge Delivery Services（EDS）可让您从边缘区域交付极快且高度可扩展的 Web 体验。本指南说明了&#x200B;**如何构建并发布表单来确保提供这样的体验**，并提供明确的推荐层级：

- **通用编辑器（UE）——大多数团队的首选方式**
- **基于文档的创作（Docs/Sheets）——适用于快速创建简单表单**
- **文档创作（DA） —— 用于将表单嵌入由 DA 创作的页面中**

完成本指南后，您将能够选择合适的创作方式，了解不同的提交选项，然后可采取创作生产就绪表单的后续步骤。


| 团队与需求 | 推荐的方式 | 原因 |
|--------------------|--------------------|-----|
| 适用于需要视觉控制、条件逻辑或 AEM 集成功能的市场营销人员/设计师 | **通用编辑器** | 支持拖放操作、高级规则，将数据提交至 FSS 或 AEM Publish 环境 |
| 内容作者已在使用 Word / Google Docs / Sheets，适用于将简单数据捕获至电子表格或通过电子邮件接收 | **基于文档的创作方式** | 使用熟悉的工具，是创建基础表单的最快途径 |
| 由&#x200B;**文档创作（DA）**&#x200B;构建的网站页面 | 可将 UE 表单或基于文档的表单&#x200B;**嵌入**&#x200B;至 DA 页面中 | DA 本身不具备表单构建功能 |


## 创作方式详解

### 通用编辑器

<!--<span class="preview"> This is a pre-release feature available through our <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=zh-Hans#new-features">pre-release channel</a>. </span>-->

[通用编辑器](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)是一款面向市场营销人员和设计师的可视化拖放式创作工具，兼具高速与企业级性能优势：

- 支持实时所见即所得（WYSIWYG）编辑与设备预览。
- 可直接集成 AEM 资产、工作流和表单数据模型（FDM）。
- 可无缝交接给开发人员，使用原生 JS/CSS 开发自定义组件
- 用于创建复杂逻辑的高级规则编辑器。
- 自定义功能的服务器端可扩展性。
- WYSIWYG 的编辑体验，可轻松创建表单和可视化。
- 记录文档功能可创建提交数据的防篡改档案。
- 与 Adobe Sign 集成以进行电子签名。
- 与 Adobe Workfront Fusion 集成，在提交表单时触发 Adobe Workfront Fusion 场景。
- 与各种数据源集成以预填充表单和提交数据。
- 表单数据模型 (FDM)，用于定义数据结构和与各种数据源的交互。
- 能够从多个提交操作中进行选择来处理表单提交，包括将数据提交到 Microsoft SharePoint、Microsoft OneDrive、Adobe Workfront Fusion、Salesforce、Microsoft Dynamics 以及更多数据源。
- 支持通过 Forms Submission Service（FSS）或 AEM Publish 提交操作完成提交

**推荐**：除非您的团队完全以文档为中心，且要创建非常基础的表单，否则建议所有新表单项目均采用通用编辑器开始构建。


### 基于文档的创作（使用 Microsoft Docs 或 Google Sheets）

[基于文档的创作](/help/edge/docs/forms/tutorial.md)最适合使用熟悉的工具（如 Microsoft Word、Google Docs 或 Google Sheets）创建结构简单、复杂度较低的表单。此方法非常适合内容团队，以快速且简便的方式构建表单。

- 可访问的组件可提供用户友好的体验。
- 标准化 HTML 结构，实现一致的渲染。
- 确保数据准确性的规则和验证。
- 用于收集附加信息的文件附件选项。
- Google reCAPTCHA 集成用于垃圾邮件防护。
- 能够根据特定需求创建自定义表单组件。
- 直接将表单数据提交到 Microsoft Excel 或 Google Sheets 或电子邮件地址。
- 通过操作遥测监测表单性能


### 在文档创作（DA）中嵌入表单

文档创作（DA）旨在用于构建结构化页面内容，不支持原生表单创建功能。若需将表单添加至由 DA 创作的页面，您可以使用&#x200B;**通用编辑器**（推荐）或基于文档的方式创建表单，并将其嵌入到文档创作页面中。

## 发布 Edge Delivery Services 表单 {#edge-overview}

下图说明如何在 Microsoft Excel 或 Google Sheets（基于文档的创作）中编辑表单并将其发布到 Edge Delivery Services。它也说明了如何使用所见即所得创作工具（通用编辑器）进行 AEM 发布。

![发布到 Edge Delivery Services 和 AEM](/help/edge/docs/forms/assets/AEM-forms-with-EDS-publishing.png)


<!-- 
## Feature Comparison

| Capability | Universal Editor | Document-Based | Document Authoring |
|------------|-----------------|----------------|--------------------|
| Visual drag-and-drop | ✅ | – | – |
| Advanced rules editor | ✅ | Limited | – |
| Attachments | ✅ | EA | – |
| reCAPTCHA Enterprise | ✅ | ✅ | Depends on embed |
| Submit to spreadsheet/email | ✅ (FSS) | ✅ (FSS) | Via embed |
| Submit to AEM workflows/FDM | ✅ | – | Via UE embed |
| Custom components (JS/CSS) | ✅ | ✅ | Via embed |
| Localization via Sites | ✅ | Manual | Via embed |

-->

## 后续步骤

- [通用编辑器在 Edge Delivery Services for Forms 中的功能与优势](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
- [使用通用编辑器创建您的首个表单](/help/edge/docs/forms/universal-editor/create-forms.md)
- [使用 Google Sheets 或 Microsoft Excel 创建首个表单](/help/edge/docs/forms/tutorial.md)。
- [在文档创作（DA）中嵌入表单](https://www.aem.live/developer/da-tutorial)


现在，您已准备好使用 AEM Edge Delivery Services 创建首个高性能表单。


<!-- 

## Start creating forms

- [Get started with Edge Delivery Services for AEM Forms](/help/edge/docs/forms/tutorial.md)
- [Create a form using Google Sheets or Microsoft Excel](/help/edge/docs/forms/create-forms.md)
- [Set up your Google Sheets or Microsoft Excel files to start accepting data​](/help/edge/docs/forms/submit-forms.md)
- [Publish your form and start collecting data](/help/edge/docs/forms/publish-forms.md)
- [Customize the look of your forms​](/help/edge/docs/forms/style-theme-forms.md)
- [Add repeatable sections to a form​](/help/edge/docs/forms/repeatable-forms.md)
- [Show a custom thank you message after form submission​](/help/edge/docs/forms/thank-you-page-form.md)
- [Adaptive Form Block components and their properties](/help/edge/docs/forms/form-components.md)
- [Real Use Monitoring](https://www.aem.live/developer/rum#authentication)

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
        transition: background-color 0.3s ease; /- Adding transition effect */
    }
    .card-container:hover {
        background-color: #f0f0f0; /- Changing background color on hover */
    }
</style>

<div style="display: flex; flex-wrap: wrap; justify-content: space-between; margin: -5px;">
    <div class="card-container">
        <a href="/help/edge/docs/forms/create-forms.md">
            <img src="/help/edge/assets/smock_devices_18_n.svg" alt="Create a form using eds forms" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Create a form using Google Sheets or Microsoft Excel</b>
        </a>
        <p>Create forms that load and render quickly and automatically reflows on mobile devices.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/create-forms.md#manually-configure-a-spreadsheet-to-accept-data">   
            <img src="/help/edge/assets/smock_platformdatamapping_18_n.svg" alt="Submit form" alt="Use Form Fragments in an EDS Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Submit form to spreadsheet</b>
        </a>
        <p>Submit forms directly to your Microsoft Excel or Google Sheets.</p>
    </div>
     <div class="card-container">
        <a href="/help/edge/docs/forms/style-theme-forms.md">
            <img src="/help/edge/assets/smock_imageautomode_18_N.svg" alt="Apply styles or themes to an eds form" style="border-radius: 5px;"> </b>
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
            <img src="/help/edge/assets/smock_abc_18_n.svg" alt="Translate an EDS Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Translate a form</b>
        </a>
        <p>Extend the reach of your forms while keeping costs in check.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/repeatable-forms.md">  
            <img src="/help/edge/assets/smock_addto_18_n.svg" alt="Add repeatable sections to an EDS Form" style="border-radius: 5px;"> </b>
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
            <img src="/help//edge/assets/smock_keyclock_18_n.svg" alt="Use reCAPTCHA in an EDS Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Use reCAPTCHA</b>
        </a>
        <p>Use OOTB reCAPTCHA integration for robust spam and bot protection.</p>
    </div>


</div>


</br>


-->