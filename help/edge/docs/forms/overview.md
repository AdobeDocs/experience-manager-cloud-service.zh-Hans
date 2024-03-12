---
title: AEM FormsEdge Delivery Services概述
description: AEM FormsEdge Delivery Services专为实现卓越性能而构建，使您能够预见简化数据收集和用户参与的未来。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
source-git-commit: 8ff0363fbb97aac85733fc9444819fa4d6f12805
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 0%

---

# AEM FormsEdge Delivery Services

AEM FormsEdge Delivery Services是一组可组合的服务，能够实现快速开发环境，以供作者快速更新、发布和启动新表单。 这些服务提供卓越且影响力高的表单体验，可促进参与和转化。 这些表单体验易于创作和开发。

这些服务使您能够：

* **使用您选择的工具创建注册体验：** 通过分离内容源提高创作效率。 开箱即用地您可以使用基于文档的创作(Microsoft SharePoint或Google Drive)和AEM创作(自适应Forms编辑器)。 您可以在同一个表单网站上使用多个内容源并使用首选创作工具，如Microsoft Excel、Google Sheets或自适应Forms编辑器。

* **提供卓越的数字注册体验：** 提供可快速加载和渲染的数字注册体验。 更快的加载时间和优化的用户体验有助于提高表单完成率和转化率。

* **使用开发人员友好的工具集：** AEM FormsEdge Delivery Services使用纯HTML、新式CSS和vanilla JavaScript创建卓越的体验，避免特定框架的陡峭学习曲线。 具有基本Web开发技能的开发人员可以自定义并轻松构建表单组件和体验。 无需等待管道运行，只需将您的代码签入到GitHub中，即可实时进行更改。

## AEM FormsEdge Delivery Services概述 {#edge-overview}

AEM Forms Edge Delivery服务允许您在网站上创作表单的方式具有高度灵活性。 您可以通过以下方式创作内容和表单 [AEM创作](/help/forms/creating-adaptive-form-core-components.md) 以及 [基于文档的创作](/help/edge/docs/forms/create-forms.md). AEM FormsEdge Delivery Services提供表单块，称为 [自适应Forms块](/help/edge/docs/forms/create-forms.md) 以将表单添加到Edge Delivery Services站点。

例如，您直接在Microsoft Excel或Google工作表中创作表单，这些电子表格将转换为您网站的表单。 任何新表单或表单内容（如新表单字段）均可在您的网站上立即使用，而无需重新构建过程。

下图说明了如何在Microsoft Excel或Google Sheets（基于文档的创作）中编辑表单并发布到Edge Delivery Services。 它还显示了使用自适应Forms编辑器(AEM创作)的AEM发布方法。

![Edge Delivery 架构](/help/edge/assets/AEM-forms-with-EDS-publishing.png)

AEM FormsEdge Delivery Services使用GitHub，因此客户可以直接从其GitHub存储库管理和部署代码。 例如，您可以用以下方式编写表单 [Google工作表](/help/edge/docs/forms/create-forms.md) 或 [Microsoft Excel](/help/edge/docs/forms/create-forms.md) 并且可以在GitHub存储库中使用CSS和JavaScript来开发表单的组件。

当您的表单准备就绪后，您可以使用 [AEM Sidekick](/help/edge/docs/forms/tutorial.md#preview-and-publish-your-content)，一种chrome浏览器扩展，用于预览和发布内容更新。

![安装AEM Sidekick](/help/edge/assets/aem-sidekick-preview-publish-forms.png)

选择 [基于文档的创作](#document-based-authoring-features) 和 [AEM创作](#aem-authoring-features) 具体取决于您的特定要求：

* 对于只是通过几个字段收集基本信息的简单表单（例如，联系我们表单、潜在客户生成表单或服务请求表单），以及您需要使用电子表格快速连接数据的表单， [基于文档的创作](#document-based-authoring-features) 非常适合。 您可以像在Google Sheets或Microsoft Excel中构建文档一样构建这些表单。

* 对于复杂表单，例如需要多个面板、复杂规则和业务逻辑、数据操作、与外部系统集成，或使用AEM功能简化工作流的表单， [AEM创作](#aem-authoring-features) 是一个更好的选择。


### 基于文档的创作和AEM创作的主要功能

基于文档的创作提供了一系列基本功能，AEM创作解锁了基于文档的创作之外的其他功能，让您能够构建更复杂且交互式的表单。 基于文档的创作和AEM创作的主要功能包括：

#### 基于文档的创作功能

基于文档的创作允许您使用熟悉的工具(如Microsoft Excel或Google Sheets)创建表单。 这些表单提供以下功能：

* 无障碍组件，提供用户友好的体验。
* 标准化HTML结构以实现一致的呈现。
* 规则和验证以确保数据准确性。
* 用于收集其他信息的文件附件选项。
* Google reCAPTCHA集成用于垃圾邮件保护。
* 能够根据特定需求创建自定义表单组件。
* 将表单数据直接提交到Microsoft Excel、Google工作表或电子邮件地址。

#### AEM创作功能

AEM创作提供了用于构建表单的WYSIWYG界面(自适应Forms编辑器)，并提供了基于文档创作的所有功能以及大量其他功能：

* 用于创建复杂逻辑的高级规则编辑器。
* 自定义功能的服务器端可扩展性。
* 所见即所得编辑体验，可轻松创建表单和可视化图表。
* 记录文档功能，用于创建已提交数据的防篡改存档。
* 与Adobe Sign集成以提供电子签名。
* 与Adobe Workfront Fusion集成，以便在提交表单时触发Adobe Workfront Fusion场景。
* 与各种数据源集成，用于预填充表单和提交数据。
* 表单数据模型，用于定义数据结构和与各种数据源的交互。
* 能够从多个提交操作中进行选择，用于处理表单提交，包括将数据提交到Microsoft SharePoint、Microsoft OneDrive、Adobe Workfront Fusion、Salesforce、Microsoft Dynamics以及更多数据源。

本质上， [AEM创作](/help/forms/creating-adaptive-form-core-components.md) 构建在 [基于文档的创作](/help/edge/docs/forms/create-forms.md)，提供了更高级的工具包来创建和管理复杂的表单。

### AEM FormsEdge Delivery Services：创作。 Forms的发布和提交

下图说明了使用基于文档的创作和AEM创作来创建、发布和提交表单的过程。




![基于文档的创作 ](/help/edge/assets/document-based-authoring-workflow.png)

![AEM创作](/help/edge/assets/aem-authoring-workflow.png)


## 开始创建表单

* [AEM FormsEdge Delivery Services入门](/help/edge/docs/forms/tutorial.md)
* [使用Google Sheets或Microsoft Excel创建表单](/help/edge/docs/forms/create-forms.md)
* [设置Google Sheets或Microsoft Excel文件以开始接受数据&#x200B;。](/help/edge/docs/forms/submit-forms.md)
* [发布表单并开始收集数据](/help/edge/docs/forms/publish-forms.md)
* [自定义表单的外观&#x200B;](/help/edge/docs/forms/style-theme-forms.md)
* [向表单添加可重复部分&#x200B;](/help/edge/docs/forms/repeatable-forms.md)
* [在提交表单后显示自定义感谢消息&#x200B;。](/help/edge/docs/forms/thank-you-page-form.md)
* [自适应表单块组件及其属性](/help/edge/docs/forms/form-components.md)




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