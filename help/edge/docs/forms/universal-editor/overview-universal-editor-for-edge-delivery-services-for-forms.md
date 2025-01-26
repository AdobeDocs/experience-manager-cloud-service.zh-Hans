---
title: 适用于 AEM Forms 的 Edge Delivery Services 概述
description: '适用于 AEM Forms 的 Edge Delivery Services '
feature: Edge Delivery Services
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
source-git-commit: ae31df22c723c58addd13485259e92abb4d4ad54
workflow-type: tm+mt
source-wordcount: '1144'
ht-degree: 11%

---

# FormsEdge Delivery Services的通用编辑器(EDS Forms块)


通用编辑器旨在帮助内容创建者和表单作者轻松构建、管理和编辑表单。 它提供了针对Edge Delivery Services(EDS)的简单、直观且高效的编辑体验。

使用通用编辑器，用户可以拖放表单元素（如文本字段、复选框和单选按钮）以在What You See Is What You Get (WYSIWYG)界面中创建表单。 这种方法使表单创建变得直观且可访问，即使对于没有技术专业知识的人也是如此。

![Universal Editor](/help/edge/docs/forms/universal-editor/assets/universal-editor.png)

通用编辑器允许内容创建者和表单作者以简化且高效的方式构建、管理和编辑表单。 此编辑器专门针对Edge Delivery Services(EDS)。 通用编辑器为创建表单提供了用户友好的可视化编辑体验。 您可以轻松地拖放表单元素（如文本字段、复选框、单选按钮等），并在WYSIWYG (What You See Is What You Get)样式界面中对其进行配置。

通用编辑器的核心优势在于其强大的功能集，其中包括高级表单创建功能、动态规则编辑以及与各种数据源的无缝集成。 用户可以使用预建的组件、可自定义的模板和广泛的表单元素库快速设计响应式表单。

技术功能经过精心设计，可保持轻量级的客户端渲染、跨浏览器兼容以及严格遵守辅助功能标准。 Universal Editor for EDS Forms Block为寻求灵活、强大的表单创建和管理平台的组织提供了一个全面的解决方案。

## EDS Forms通用编辑器的主要功能


<div>
  <div class="card" style="display: inline-block; width: calc(33.33% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/universal-editor.png" alt="WYSIWYG界面"> 
    <h3>WYSIWYG界面</h3>
    <p>通用编辑器为表单设计提供了WYSIWYG界面。 它提供了预建的组件库、响应式设计支持以及基于模板的表单创建。 您可以立即添加或删除表单字段并修改字段属性（如标签、数据绑定、验证）。 您还可以将自定义表单组件插入通用编辑器。</p>
  </div>
  <div class="card" style="display: inline-block; width: calc(33.33% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="https://via.placeholder.com/150" alt="规则编辑器">
    <h3>规则编辑器</h3>
    <p>规则编辑器允许您通过轻量级的JavaScript和基于JSON的定义创建具有事件驱动规则、即时验证和错误处理的复杂表单交互。</p>
  </div>
  <div class="card" style="display: inline-block; width: calc(33.33% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="https://via.placeholder.com/150" alt="提交操作">
    <h3>提交操作</h3>
    <p>提交操作通过后端集成选项、数据预处理器、条件提交逻辑和安全端点连接来简化表单提交工作流。</p>
  </div>
</div>

<div>
  <div class="card" style="display: inline-block; width: calc(33.33% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="https://via.placeholder.com/150" alt="预填充服务">
    <h3>预填充服务</h3>
    <p>预填充服务通过智能地使用来自各种来源的相关数据填充表单字段，从而减少手动数据输入，进而增强用户体验。</p>
  </div>
  <div class="card" style="display: inline-block; width: calc(33.33% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="https://via.placeholder.com/150" alt="数据绑定">
    <h3>数据绑定</h3>
    <p>数据绑定实现了表单字段与后端数据源之间的直接、动态连接，支持实时同步和复杂的数据映射。</p>
  </div>
  <div class="card" style="display: inline-block; width: calc(33.33% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="https://via.placeholder.com/150" alt="国际化/本地化">
    <h3>国际化/本地化</h3>
    <p>国际化支持通过多语言渲染、从右至左的语言兼容性和特定于区域设置的格式来确保全局可访问性。</p>
  </div>
</div>

<div>
  <div class="card" style="display: inline-block; width: calc(33.33% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="https://via.placeholder.com/150" alt="Analytics和Tracking">
    <h3>Analytics和Tracking</h3>
    <p>内置的分析和跟踪机制可深入分析表单交互、提交率和用户行为，从而实现持续优化。</p>
  </div>
  <div class="card" style="display: inline-block; width: calc(33.33% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="https://via.placeholder.com/150" alt="试验（A/B测试）">
    <h3>试验（A/B测试）</h3>
    <p>试验允许组织对表单设计运行A/B测试，以确定性能最佳的布局或功能。</p>
  </div>
  <div class="card" style="display: inline-block; width: calc(33.33% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="https://via.placeholder.com/150" alt="任务管理">
    <h3>任务管理</h3>
    <p>与Adobe Workfront集成允许团队管理与表单创建和维护相关的任务，从而确保简化协作。</p>
  </div>
</div>

<div>
  <div class="card" style="display: inline-block; width: calc(33.33% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="https://via.placeholder.com/150" alt="编辑器自定义">
    <h3>编辑器自定义</h3>
    <p>开发人员可以通过UI扩展来扩展通用编辑器的功能，从而实现符合特定组织需求的定制解决方案。</p>
  </div>
</div>


<!-- ![Universal Editor](/help/edge/docs/forms/universal-editor/assets/generate-forms.svg)  **WYSIWYG interface for Form creation**: Universal Editor provides a WYSIWYG interface for form design. It provides pre-built component library, responsive design support, and template-based form creation. You can instantly add or remove form fields and modify field properties (like label, data binding, validation). You can also plugin custom form components to Universal Editor.


* **Rule editor**: The rule editor stands out as a powerful mechanism for creating sophisticated form interactions. It supports event-driven rules, instant validation, and error handling through lightweight JavaScript and JSON-based definitions. This allows developers to implement complex form logic, such as conditional field visibility, automatic calculations, and dynamic form behaviour without extensive coding.

* **Submit actions**: Submit Actions enable form submission workflows. These actions provide comprehensive backend integration options, supporting protocols like REST API. The system allows you configure data pre-processors for automatic data transformation, conditional submission logic based on form field values, and secure endpoint connections. Organizations can define complex submission rules that validate data, and manage form responses with granular control.

* **Pre-fill services:** Pre-fill Services enhance user experience by intelligently populating form fields with relevant data. These services connect to various data sources, including user profiles, browser local storage, and external databases. The mechanism supports dynamic data population, enabling automatic completion of form fields based on contextual information. Users benefit from reduced manual data entry, while administrators gain flexibility in configuring pre-fill rules across different form types and scenarios. The pre-fill functionality adapts to different authentication methods, including session-based approaches and token-based systems, ensuring both convenience and security.

* **Data binding capabilities**: Data binding in the Universal Editor enables direct, dynamic connections between form fields and backend data sources. This feature allows real-time synchronization of form data, supporting complex data mapping scenarios. The system supports transforming form inputs into structured database records with minimal configuration. Advanced mapping supports nested data structures, allowing complex form designs to interact seamlessly with intricate data models.

* **Internationalization/localization capabilities**: Internationalization support ensures global accessibility, with multi-language rendering, right-to-left language compatibility, and locale-specific formatting.

* **Analytics and tracking mechanisms**: The built-in analytics and tracking mechanisms provide comprehensive insights into form interactions, submission rates, and user behavior, enabling continuous optimization of form design and performance. 

* **Experimentation (A/B Testing)**: The Universal Editor supports experimentation by allowing organizations to run A/B tests on form designs to identify the best-performing layouts or features.

* **Task Management via Adobe Workfront**: Integration with Adobe Workfront allows teams to manage tasks related to form creation and maintenance, ensuring streamlined collaboration and efficient workflows.

* **Editor Customization via UI Extension**: Developers can extend the functionality of the Universal Editor through UI extensions, enabling tailored solutions that fit specific organizational needs. -->

## 预建表单组件

通用编辑器提供了以下现成的表单组件：

<table>
  <thead>
    <tr>
      <th>可爱</th> 
      <th>表单组件</th>
      <th>描述</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="22"><img src="/help/edge/docs/forms/universal-editor/assets/adaptive-forms-components.png" alt="表单组件" style="width: 100%;"></td> 
      <td><b>可折叠项</b></td>
      <td>用于组织内容的可折叠面板结构。</td>
    </tr>
    <tr>
      <td><b>按钮</b></td>
      <td>为导航或自定义逻辑等操作添加交互式元素。</td>
    </tr>
    <tr>
      <td><b>验证码</b></td>
      <td>通过要求用户使用Google reCaptcha或HCaptcha完成人工验证任务来阻止垃圾邮件。</td>
    </tr>
    <tr>
      <td><b>复选框</b></td>
      <td>允许用户配置复选框。</td>
    </tr>
    <tr>
      <td><b>复选框组</b></td>
      <td>允许用户从组中选择多个选项。</td>
    </tr>
    <tr>
      <td><b>日期选取器</b></td>
      <td>允许用户使用日历界面选择日期。</td>
    </tr>
    <tr>
      <td><b>下拉列表</b></td>
      <td>从预定义列表中提供单选或多选选项。</td>
    </tr>
    <tr>
      <td><b>电子邮件</b></td>
      <td>通过基本格式验证捕获电子邮件地址。</td>
    </tr>
    <tr>
      <td><b>文件附件</b></td>
      <td>允许上载文档、图像或其他文件类型。</td>
    </tr>
    <tr>
      <td><b>表单片段</b></td>
      <td>地址字段或联系人详细信息等部分的可重用表单组件。</td>
    </tr>
    <tr>
      <td><b>图像</b></td>
      <td>支持在表单中上传和显示图像。</td>
    </tr>
    <tr>
      <td><b>模态</b></td>
      <td>显示弹出对话框，通常用于警报、其他信息或确认。</td>
    </tr>
    <tr>
      <td><b>数值字段</b></td>
      <td>捕获数字输入，允许验证数字或范围。</td>
    </tr>
    <tr>
      <td><b>面板</b></td>
      <td>使用可展开/可折叠的面板组织表单部分。</td>
    </tr>
    <tr>
      <td><b>单选按钮</b></td>
      <td>从选项组启用单选选择。</td>
    </tr>
    <tr>
      <td><b>评分</b></td>
      <td>允许用户提供基于星级的评级。</td>
    </tr>
    <tr>
      <td><b>“重置”按钮</b></td>
      <td>将表单字段重置为其默认状态。</td>
    </tr>
    <tr>
      <td><b>“提交”按钮</b></td>
      <td>触发表单提交并启动定义的工作流。</td>
    </tr>
    <tr>
      <td><b>电话号码字段</b></td>
      <td>根据国家/地区捕获带有格式的电话号码。</td>
    </tr>
    <tr>
      <td><b>文本</b></td>
      <td>提供一个专用部分，用于显示法律术语并通过复选框收集用户协议。</td>
    </tr>
    <tr>
      <td><b>文本字段</b></td>
      <td>DCaptures单行输入，如名称或电子邮件地址。</td>
    </tr>
    <tr>
      <td><b>向导</b></td>
      <td>指导用户逐步完成多部分表单过程。</td>
    </tr>
  </tbody>
</table>

<!-- * Footer: Adds a footer section for consistent design or additional information.
* Form Container: Wraps all form elements and manages overall form properties.
* Header: Adds a header section for form titles, branding, or instructions.-->
<!-- * 
* Prefillable Fields: Automatically populates form fields with data from predefined sources such as user profiles or APIs. 

* Switches/Toggle Buttons: Provides binary on/off choices for user input.


* Title: Adds a text-based heading or label to improve form clarity and organization.

-->

除了预建表单组件之外，通用编辑器还支持：

* **将Forms嵌入其他网页**：通用编辑器支持将表单直接嵌入到Edge交付服务站点页面。 可使用现成的嵌入组件完成此操作。

* **验证消息**：验证消息会在用户输入不正确或不完整的数据时向其提供实时反馈。 功能包括：
   * 动态错误显示：即时提醒用户存在错误，例如电子邮件地址无效或缺少必填字段。
   * 可自定义的消息：允许表单作者定义用户友好的错误文本。
   * 基于规则的验证：支持高级验证逻辑，例如检查字段之间的依赖关系或实施条件规则。

* **隐藏字段**：隐藏字段在表单中以不可见的方式存储数据，通常用于后端处理或预填充值。 用例包括：
   * 将上下文信息（例如，用户ID或会话数据）传递到后端，而不向用户显示。
   * 捕获元数据，如时间戳或跟踪ID。
   * 隐藏字段对最终用户不可见，但可以预填充、动态更新或在工作流中使用。

* **自定义组件**：自定义组件允许开发人员通过创建专用集成或第三方集成来扩展表单的功能。 功能包括：
   * 灵活性：开发人员可以针对特定用例设计独特的表单元素。
   * 第三方集成：嵌入构件或工具，如支付网关、分析跟踪器或人工智能驱动的输入字段。
   * 无缝兼容性：自定义组件可与通用编辑器的拖放界面以及数据绑定或验证等现有功能集成。

* **感谢配置**：自定义表单提交后显示的确认消息或页面。

## 入门培训

要为您的环境启用通用编辑器和规则编辑器，或请求其他功能，如Forms Portal、记录文档、Adobe Sign集成或从右至左的语言支持，只需发送电子邮件从官方地址向mailto:aem-forms-ea@adobe.com发送请求即可。



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