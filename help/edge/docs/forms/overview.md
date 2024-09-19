---
title: 适用于 AEM Forms 的 Edge Delivery Services 概述
description: 适用于 AEM Forms 的 Edge Delivery Services
feature: Edge Delivery Services
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
role: Admin, Architect, Developer
source-git-commit: 4a8153ffbdbc4da401089ca0a6ef608dc2c53b22
workflow-type: ht
source-wordcount: '1037'
ht-degree: 100%

---

# 适用于 AEM Forms 的 Edge Delivery Services 


适用于 AEM Forms 的 Edge Delivery Services 是一组可组合的服务，可用于实现快速开发环境，作者可以在其中快速更新、发布和启动新表单。这些服务提供卓越且具有高影响力的表单体验，从而推动参与度和转化率。这些表单体验很容易创作和开发。

这些服务使您能够：

* **使用选定工具创建注册体验**：通过分离内容来源而提高创作效率。您可以使用开箱即用、基于文档的创作功能（Microsoft SharePoint 或 Google Drive）和所见即所得的创作功能（通用编辑器或自适应表单编辑器）。您可以在同一个表单网站上使用多个内容源，并使用首选的创作工具，如 Microsoft Excel、Google Sheets、通用编辑器或自适应表单编辑器。

* **提供卓越的数字注册体验：**&#x200B;提供快速加载和渲染的数字注册体验，并通过实际使用监控 (RUM) 持续监控表单性能。更快的加载时间和优化的用户体验有助于提高表单完成率和转化率。

* **使用易于开发人员使用的工具集：** 适用于 AEM Forms 的 Edge Delivery Services 使用纯 HTML、现代 CSS 和普通 JavaScript 来创建卓越的体验，避免特定框架所需的陡峭学习曲线。具有基本 Web 开发技能的开发人员可以自定义并轻松构建表单组件和体验。无需等待管道运行，只需将代码签入 GitHub，所做的更改就会生效。

## 适用于 AEM Forms 的 Edge Delivery Services 概述 {#edge-overview}

适用于 AEM Forms 的 Edge Delivery Services 可让您在网站上创作表单的方式具有高度的灵活性。您可以使用[所见即所得的创作](/help/forms/creating-adaptive-form-core-components.md)功能以及[基于文档的创作](/help/edge/docs/forms/create-forms.md)功能来创作内容和表单。适用于 AEM Forms 的 Edge Delivery Services 提供一个称为 [Adaptive Forms Block](/help/edge/docs/forms/create-forms.md) 的表单区块，以将表单添加到您的 Edge Delivery Services 站点。

例如，您直接在 Microsoft Excel 或 Google Sheets 中创作表单，这些电子表格将转换为您网站的表单。任何新表单或表单内容（例如新表单字段）都可以立即在您的网站上使用，无需重建过程。

下图说明如何在 Microsoft Excel 或 Google Sheets（基于文档的创作）中编辑表单并将其发布到 Edge Delivery Services。它还展示了使用所见即所得的创作（通用编辑器或自适应表单编辑器）功能的 AEM 发布方法。

![发布到 Edge Delivery Services 和 AEM](/help/edge/docs/forms/assets/AEM-forms-with-EDS-publishing.png)

适用于 AEM Forms 的 Edge Delivery Services 使用 GitHub，因此客户可直接从其 GitHub 存储库管理和部署代码。例如，可在 [Google Sheets](/help/edge/docs/forms/create-forms.md) 或 [Microsoft Excel](/help/edge/docs/forms/create-forms.md) 中编写表单，并且可以使用 GitHub 存储库中的 CSS 和 JavaScript 来开发表单的组件。

当表单就绪时，您即可使用 [AEM Sidekick](/help/edge/docs/forms/tutorial.md#preview-and-publish-your-content)（一款 Chrome 浏览器扩展）来预览和发布内容更新。

![安装 AEM SideKick](/help/edge/assets/aem-sidekick-preview-publish-forms.png)

要选择[基于文档的创作](#document-based-authoring-features)还是 [所见即所得的创作](#wysiwyg-authoring-features)，取决于您的具体要求：

* 对于仅通过几个字段收集基本信息的简单表单（例如联系我们表单、商机开发表单或服务请求表单），以及需要使用电子表格进行快速数据连接的情况，[基于文档的创作](#document-based-authoring-features)非常适合。您可以像在 Google Sheets 或 Microsoft Excel 中构建文档一样构建这些表单。

* 对于复杂的表单，例如需要多个面板的表单、复杂的规则和业务逻辑、数据操作、与外部系统的集成或使用 AEM 功能简化的工作流程，那么[所见即所得的创作](#wysiwyg-authoring-features)则是一个更好的选择。


### 基于文档的创作和所见即所得的创作的主要功能

基于文档的创作提供了一组基本功能，所见即所得的创作解锁了基于文档的创作之外的其他功能，使您能够构建更复杂的交互式表单。基于文档的创作和所见即所得的创作的主要功能包括：

#### 基于文档的创作功能

基于文档的创作允许您使用 Microsoft Excel 或 Google Sheets 等熟悉的工具创建表单。这些表单提供以下功能：

* 可访问的组件可提供用户友好的体验。
* 标准化 HTML 结构，实现一致的渲染。
* 确保数据准确性的规则和验证。
* 用于收集附加信息的文件附件选项。
* Google reCAPTCHA 集成用于垃圾邮件防护。
* 能够根据特定需求创建自定义表单组件。
* 直接将表单数据提交到 Microsoft Excel 或 Google Sheets 或电子邮件地址。
* 通过实际使用监控 (RUM) 监控表单性能

#### 所见即所得的创作功能

所见即所得的创作提供用于构建表单的所见即所得界面（通用编辑器以及自适应表单编辑器），并提供基于文档的创作的所有功能，以及一系列其他功能：

* 用于创建复杂逻辑的高级规则编辑器。
* 自定义功能的服务器端可扩展性。
* WYSIWYG 的编辑体验，可轻松创建表单和可视化。
* 记录文档功能可创建提交数据的防篡改档案。
* 与 Adobe Sign 集成以进行电子签名。
* 与 Adobe Workfront Fusion 集成，在提交表单时触发 Adobe Workfront Fusion 场景。
* 与各种数据源集成以预填充表单和提交数据。
* 表单数据模型 (FDM)，用于定义数据结构和与各种数据源的交互。
* 能够从多个提交操作中进行选择来处理表单提交，包括将数据提交到 Microsoft SharePoint、Microsoft OneDrive、Adobe Workfront Fusion、Salesforce、Microsoft Dynamics 以及更多数据源。

所有上述功能也可通过自适应表单编辑器使用。

本质上，所见即所得的创作（通用编辑器和[自适应表单编辑器](/help/forms/creating-adaptive-form-core-components.md)）建立在[基于文档的创作](/help/edge/docs/forms/create-forms.md)的基础之上，为创建和管理复杂表单提供了更高级的工具包。

>[!NOTE]
>
>
> 所见即所得的创作功能可在早期采用者计划中使用。如果您有兴趣，请从您的工作地址向 aem-forms-ea@adobe.com 发送一封快速电子邮件，以请求访问该功能。

### 适用于 AEM Forms 的 Edge Delivery Services 

：编写、发布和提交表单

下图说明了使用基于文档的创作和所见即所得的创作创建、发布和提交表单的过程。

![基于文档的创作](/help/edge/assets/document-based-authoring-workflow.png)

![所见即所得的创作](/help/edge/assets/wysiwyg-authoring-workflow.png)

## 开始创建表单

* [适用于 AEM Forms 的 Edge Delivery Services 快速入门](/help/edge/docs/forms/tutorial.md)
* [使用 Google Sheets 或 Microsoft Excel 创建表单](/help/edge/docs/forms/create-forms.md)
* [设置您的 Google Sheets 或 Microsoft Excel 文件，即可开始接受数据](/help/edge/docs/forms/submit-forms.md)
* [发布您的表单并开始收集数据](/help/edge/docs/forms/publish-forms.md)
* [自定义表单的外观&#x200B;](/help/edge/docs/forms/style-theme-forms.md)
* [将可重复部分添加到表单&#x200B;](/help/edge/docs/forms/repeatable-forms.md)
* [提交表单后显示自定义感谢消息](/help/edge/docs/forms/thank-you-page-form.md)
* [Adaptive Form Block 组件及其属性](/help/edge/docs/forms/form-components.md)
* [实际使用监控](https://www.aem.live/developer/rum#authentication)

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