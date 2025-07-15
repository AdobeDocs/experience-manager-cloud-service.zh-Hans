---
title: 适用于 AEM Forms 的 Edge Delivery Services 概述
description: 在Adobe Experience Manager Edge Delivery Services上创建并提供高性能表单，重点使用通用编辑器创作方法。
feature: Edge Delivery Services
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
role: Admin, Architect, Developer
source-git-commit: e1ead9342fadbdf82815f082d7194c9cdf6d799d
workflow-type: tm+mt
source-wordcount: '919'
ht-degree: 48%

---


# 适用于 AEM Forms 的 Edge Delivery Services 


适用于 AEM Forms 的 Edge Delivery Services 是一组可组合的服务，可用于实现快速开发环境，作者可以在其中快速更新、发布和启动新表单。这些服务提供卓越且具有高影响力的表单体验，从而推动参与度和转化率。这些表单体验很容易创作和开发。

这些服务使您能够：

* **使用选定工具创建注册体验**：通过分离内容来源而提高创作效率。您可以使用开箱即用、基于文档的创作功能（Microsoft SharePoint 或 Google Drive）和所见即所得的创作功能（通用编辑器或自适应表单编辑器）。您可以在同一个表单网站上使用多个内容源，并使用首选的创作工具，如 Microsoft Excel、Google Sheets、通用编辑器或自适应表单编辑器。

* **提供卓越的数字注册体验：**&#x200B;提供快速加载和渲染的数字注册体验，并通过操作遥测持续监测表单性能。更快的加载时间和优化的用户体验有助于提高表单完成率和转化率。

* **使用易于开发人员使用的工具集：** 适用于 AEM Forms 的 Edge Delivery Services 使用纯 HTML、现代 CSS 和普通 JavaScript 来创建卓越的体验，避免特定框架所需的陡峭学习曲线。具有基本 Web 开发技能的开发人员可以自定义并轻松构建表单组件和体验。无需等待管道运行，只需将代码签入 GitHub，所做的更改就会生效。

## 选择创作方法


Adobe Experience Manager (AEM) Edge Delivery Services (EDS)让您可以从边缘提供超快、高度可扩展的Web体验。 本指南介绍&#x200B;**如何为那些体验构建和发布表单** — 具有明确的推荐层次结构：

1. **通用编辑器(UE) — 大多数团队的最佳选择**
2. **基于文档的创作（文档/工作表） — 非常适用于快速、简单的表单**
3. **文档创作(DA) — 用于将表单嵌入到DA创作的页面**

到最后，您将能够选择正确的创作方法、了解提交选项，并遵循后续步骤以生成可用于生产的表单。





| 团队和要求 | 推荐的方法 | 原因 |
|--------------------|--------------------|-----|
| 营销人员/设计人员需要可视化控制、条件逻辑或AEM集成 | **Universal Editor** | 拖放、高级规则，提交到FSS或AEM Publish |
| 内容作者已在Word/Google Docs/Sheets中工作；简单的数据捕获到电子表格/电子邮件 | **基于文档的创作** | 熟悉的工具，适用于基本表单的最快路径 |
| 在&#x200B;**文档创作(DA)**&#x200B;中内置的网页 | **将UE或基于Doc的表单嵌入** DA页面 | DA不会构建表单本身 |


## 详细创作方法

###  Universal Editor 

<span class="preview">这是通过我们的<a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=zh-hans#new-features">预发行渠道</a>提供的预发行功能。</span>

通用编辑器是面向营销人员和设计人员的可视化拖放创作工具，将速度和企业级功能相结合：

* 实时WYSIWYG编辑和设备预览。
* 与AEM资源、工作流和表单数据模型(FDM)的直接集成。
* 将vanilla JS/CSS中的自定义组件无缝移交给开发人员。
* 用于创建复杂逻辑的高级规则编辑器。
* 自定义功能的服务器端可扩展性。
* WYSIWYG 的编辑体验，可轻松创建表单和可视化。
* 记录文档功能可创建提交数据的防篡改档案。
* 与 Adobe Sign 集成以进行电子签名。
* 与 Adobe Workfront Fusion 集成，在提交表单时触发 Adobe Workfront Fusion 场景。
* 与各种数据源集成以预填充表单和提交数据。
* 表单数据模型 (FDM)，用于定义数据结构和与各种数据源的交互。
* 能够从多个提交操作中进行选择来处理表单提交，包括将数据提交到 Microsoft SharePoint、Microsoft OneDrive、Adobe Workfront Fusion、Salesforce、Microsoft Dynamics 以及更多数据源。
* 使用Forms提交服务(FSS)或AEM Publish提交操作提交

> **推荐**：使用通用编辑器启动每个新表单项目，除非您的团队完全以文档为中心，并且表单非常基本。


### 基于文档的创作(使用Microsoft文档或Google工作表)

基于文档的创作最适合使用熟悉的工具(如Microsoft Word、Google Docs或Google Sheets)创建简单、低复杂度的表单。 此方法非常适合需要快速而直接构建表单的内容团队。

* 可访问的组件可提供用户友好的体验。
* 标准化 HTML 结构，实现一致的渲染。
* 确保数据准确性的规则和验证。
* 用于收集附加信息的文件附件选项。
* Google reCAPTCHA 集成用于垃圾邮件防护。
* 能够根据特定需求创建自定义表单组件。
* 直接将表单数据提交到 Microsoft Excel 或 Google Sheets 或电子邮件地址。
* 通过操作遥测监测表单性能


### 在文档创作(DA)中嵌入Forms

文档创作(DA)专为创建结构化页面内容而设计，不支持原生表单创建。 要将表单添加到DA创作的页面，您可以使用&#x200B;**通用编辑器**（推荐）或基于文档的创作来创建表单，并将表单嵌入到文档创作页面。

## 发布Edge Delivery Services Forms {#edge-overview}

下图说明如何在 Microsoft Excel 或 Google Sheets（基于文档的创作）中编辑表单并将其发布到 Edge Delivery Services。它还显示了使用AEM创作（通用编辑器）的WYSIWYG发布方法。

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

1. **从通用编辑器开始：**&#x200B;请参阅[通用编辑器快速入门指南](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)开始创作表单。
1. **使用基于文档的创作：**&#x200B;使用Microsoft Excel或Google工作表创建表单，请遵循[基于文档的创作教程](/help/edge/docs/forms/tutorial.md)。
1. **在文档创作中嵌入Forms：**&#x200B;如果您在文档创作中构建页面，请使用&#x200B;**通用编辑器**（推荐）或基于文档的创作创建表单，并将表单嵌入到[DA页面](https://www.aem.live/developer/da-tutorial)。

您现在可以使用AEM Edge Delivery Services创建您的第一个高性能表单了。


<!-- 

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