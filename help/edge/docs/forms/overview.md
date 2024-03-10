---
title: AEM FormsEdge Delivery Services概述
description: AEM FormsEdge Delivery Services专为实现卓越性能而构建，使您能够预见简化数据收集和用户参与的未来。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
source-git-commit: 2aa70e78764616f41fe64e324c017873cfba1d5b
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 19%

---

# AEM FormsEdge Delivery Services

利用Adobe的AEM FormsEdge Delivery Services，简化表单创建并提高完成率。 这些功能强大、可组合的服务使您能够构建具有卓越性能和视觉吸引力的企业级表单。 AEM会优先处理用户体验和业务目标，从而确保超快的加载时间和更高的表单转化率。

利用该服务，您可以：

* **构建卓越的注册体验**：构建可快速加载和渲染的注册体验，即使在Internet连接速度较慢的情况下也是如此。 缩短加载时间并优化用户体验有助于提高表单完成率和转化率。

* **使用您选择的工具创建注册体验**：通过分离内容源提高创作效率。 开箱即用地您可以使用两者 **基于文档的创作** (Microsoft SharePoint或Google通道)及 **AEM创作** (自适应Forms编辑器)。 因此，您可以在同一表单上使用多个内容源并使用首选创作工具，例如Microsoft Excel、Google Sheets或自适应Forms编辑器。

* **使用开发人员友好的工具集：** AEM Forms使用纯HTML、新式CSS和vanilla JavaScript创建卓越的体验，而不会产生日常开销。 任何具有HTML、CSS和JS基础知识的开发人员都应该能够构建自己的组件，并且无需学习任何特定语言或框架。 无需任何管道或等待，只需将您的代码签入到Github中，即可实时进行更改。 此外，无需任何管道或等待，您可以将代码签入Github并实时进行更改。


## AEM FormsEdge Delivery Services概述 {#edge-overview}

下图说明了如何在Microsoft Excel或Google Sheets中编辑内容（基于文档的编辑）并发布到Edge Delivery Services。 它还显示了使用自适应Forms编辑器的AEM发布方法。

![Edge Delivery 架构](/help/edge/assets/AEM-forms-with-EDS-publishing.png)

Edge Delivery Services 是一组可组合的服务，通过这些服务，可非常灵活地在网站上创作内容。如前所述，您可以使用两者 [AEM内容管理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/getting-started/concepts.html) 替换为 [AEM创作](/help/implementing/universal-editor/introduction.md) 以及 [基于文档的创作](https://www.aem.live/docs/authoring)

例如，您可以直接使用Microsoft Excel或Google工作表中的内容。 这意味着来自这些来源的内容可以成为您网站上的表单。 新内容可立即添加，而不经历重建过程。

Edge Delivery Services 使用 GitHub，因此客户可直接从其 GitHub 存储库管理和部署代码。例如，您可以在Google工作表或Microsoft Excel中编写表单，并且表单的组件可以在GitHub中使用CSS和JavaScript进行开发。 当您就绪时，您即可使用 Sidekick 浏览器扩展预览和发布内容更新。

AEM FormsEdge Delivery Services提供了一个表单块，称为 [自适应Forms块](/help/edge/docs/forms/create-forms.md) 以将表单添加到Edge Delivery Services站点。

### AEM FormsEdge Delivery Services的主要功能

基于文档的创作包含一系列基本功能和AEM创作，可解锁基于文档的创作之外的其他功能，使您能够构建更复杂且交互式的表单。 下表重点说明了这两项功能的主要功能：

<!-- 

>[!BEGINTABS]

>[!TAB Document-based authoring]

Document-based authoring is a versatile option suitable for creating simple forms with essential functionalities. It allows you to integrate various input types like text fields, dropdown menus, and radio buttons, enabling you to collect user data effectively. It offers a basic version of rules to add dynamic behaviour to forms. Key features of Document-based authoring are: 

* **[HTML5-based Form Field components](/help/edge/docs/forms/form-components.md)**: AEM Forms Edge Delivery Services allow you to create user-friendly and interactive forms using form components based on HTML5 [input types](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types), <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea">textarea</a>, <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select">select</a>, and <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">fieldset</a>  elements. These components cater to different types of data collection and can be easily customized to fit your specific needs.  

* **Accessibility**: The fields in the form block are accessible. Each label is linked with its respective input element, and IDs are auto-generated for linking. Descriptions associated with fields are linked via the aria-describedby attribute. Keyboard navigation using the standard Tab/Shift + Tab keys is supported.

* **[Styling](/help/edge/docs/forms/style-theme-forms.md)**: Each form field has a fixed HTML structure that can be easily decorated using custom CSS or JavaScript files. Selectors for targeting fields in CSS and JS are provided based on type and name. You can easily create new selectors due to the standradized structure and style your form. 

* **Basic Rules**: Easily create logic that adjusts field visibility, validation, and behavior based on user input or predefined conditions. Rules offer a flexible and intuitive way to add intelligence to your forms, ensuring they adapt seamlessly based on user inputs.

* **Validations**: Before submission, the form is validated, and invalid fields are appropriately marked with error messages displayed to the user. Adaptive Forms Block support all the HTML form validation, supported by modern browsers, and provide additional validation mechanism like validation script, file size, file type, overall file size, and more. 

* **File Uploads**: You can add file attachment capabilities to your forms. Whether you need to gather documents, images, or other files from your users, file upload functionality serves you effortlessly. With custom handling options available, you can tailor the file upload process to suit your specific requirements.

* **reCAPTCHA**: Benefit from seamless integration of Google reCAPTCHA into your forms with our out-of-the-box (OOTB) support. Safeguard your forms against fraudulent activities, spam, and abuse, while maintaining a smooth and uninterrupted user experience. Adaptive Forms Block supports reCaptcha V3 and reCaptcha Enterprise. 

* **Send email notification on form submission**: Eliminate the hassle of manual follow-ups and ensure timely communication with our built-in email automation for form submissions. This integrated solution lets you effortlessly notify relevant parties, including sending form data, whenever someone fills out a form on your website. No need for complex configurations or additional tools – it's ready to use out of the box.

>[!TAB AEM Authoring]

AEM Authoring unlocks additional capabilities beyond the document-based authoring, empowering you to build more complex and interactive forms. In additon to the features of Document-based authoring, AEM authoring offers the following additional features:  

* Advanced Rules: Define logic-based actions within your forms. You can use rules to conditionally show or hide form sections, pre-populate fields based on user input, and perform various validations to ensure data integrity.

* Server-side extensibility: Extend the functionalities of your forms by integrating them with server-side logic. This allows you to perform complex calculations, interact with external systems, and automate specific tasks based on user actions within the form.
* Streamline workflows and data management: Leverage the power of AEM to:
    * Design user-friendly forms using AEM editors.
    * Generate a "Document of Record" for secure and tamper-proof archiving of submitted data.
    * Facilitate e-signing with Adobe Sign for a smooth and secure signing experience.
    * Automate business processes through AEM workflows, triggering actions based on form submissions.
    * Effortlessly integrate with various data sources, enabling seamless data flow and exchange.

>[!ENDTABS]



## Start creating forms

-->

|                                           | 基于文档的创作 | AEM创作(自适应Forms编辑器) |
| ----------------------------------------- | ------------------------ | ------------------------------------ |
| **表单功能** |                          |                                      |
| 可访问的组件 | ✓ | ✓ |
| 标准化HTML结构 | ✓ | ✓ |
| 规则和验证 | ✓ | ✓ |
| 文件附件（文件上载） | ✓ | ✓ |
| Google reCAPTCHA | ✓ | ✓ |
| 自定义组件 | ✓ | ✓ |
| 提交至电子邮件 | ✓ | ✓ |
| **高级功能** |                          |                                      |
| 带可视规则编辑器的高级规则 |                          | ✓ |
| 服务器端可扩展性 |                          | ✓ |
| 多个提交操作 |                          | ✓ |
| **表单设计与管理** |                          |                                      |
| 用于WYSIWYG编辑的自适应Forms编辑器 |                          | ✓ |
| **集成** |                          |                                      |
| 记录文档 |                          | ✓ |
| 与Adobe Sign集成 |                          | ✓ |
| 与Adobe Analytics集成 |                          | ✓ |
| 与Marketo集成 |                          | ✓ |
| 与多个数据源集成 |                          | ✓ |
| 多个提交操作 |                          | ✓ |


## 开始创建表单

* [快速入门 — 开发人员教程](/help/edge/docs/forms/tutorial.md)
* [使用Google Sheets或Microsoft Excel创建表单](/help/edge/docs/forms/create-forms.md)
* [将表单直接提交到Microsoft Excel或Google工作表](/help/edge/docs/forms/submit-forms.md)
* [更改表单的外观](/help/edge/docs/forms/style-theme-forms.md)


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