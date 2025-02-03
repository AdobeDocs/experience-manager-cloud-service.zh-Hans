---
title: 表单 Edge Delivery Services 通用编辑器（EDS 表单区块）
description: 使用表单 Edge Delivery Services 通用编辑器（EDS 表单区块）创建自适应表单。
feature: Edge Delivery Services
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
exl-id: d711e0d1-a2fc-4aa6-af87-6e77a7bc5d2e
source-git-commit: 5059437eca1dcfbfb26d1ff7b12d532472951568
workflow-type: tm+mt
source-wordcount: '1114'
ht-degree: 63%

---

# 表单 Edge Delivery Services 通用编辑器（EDS 表单区块）

通用编辑器通过提供简单、直观的可视Adobe Edge (WYSIWYG)界面，彻底变革了What You See Is What You Get Delivery Services (EDS)的表单创建方式。 它专为内容创建者和表单作者而设计，消除了传统表单构建流程的复杂性，使其甚至可供非技术用户访问。

使用通用编辑器，您可以使用预建组件（如文本字段、复选框和单选按钮）快速设计响应式交互式表单。 其强大的功能集支持动态规则、无缝数据集成和高级个性化，确保根据您的需求定制每个表单。

无论您是管理轻量级的客户端渲染、确保跨浏览器兼容性，还是遵循严格的辅助功能标准，通用编辑器都可为创建和管理表单提供简化的解决方案。

![通用编辑器](/help/edge/docs/forms/universal-editor/assets/universal-editor.png){width=80%， align-center} —>

## EDS Forms 通用编辑器的主要功能


<div>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/generate-forms.svg" alt="所见即所得界面"> 
    <h3>所见即所得界面</h3>
    <p>通用编辑器为表单设计提供了所见即所得的界面，具有预建组件库、响应式设计、基于模板的创建和实时字段修改。
 </p>
  </div>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/rule-editor.svg" alt="规则编辑器">
    <h3>规则编辑器</h3>
    <p>规则编辑器允许用户使用事件驱动规则、即时验证和通过轻量级 JavaScript 和 JSON 进行错误处理来创建动态表单交互。</p>
  </div>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/responsive.svg" alt="响应式模式">
    <h3>响应式模式 </h3>
    <p>设计可跨设备（台式机、平板电脑和移动设备）无缝适应的表单。使用响应式模式预览和测试各种屏幕尺寸的表单。</p>
  </div>
</div>
<div>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/personalization.svg" alt="个性化"> 
    <h3>个性化</h3>
    <p>通过个性化使用用户数据来提供量身定制的表单体验，根据用户偏好动态调整内容、布局或选项。</p>
  </div>
    <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/prefill-services.svg" alt="预填服务">
    <h3>预填服务</h3>
    <p>预填服务会自动使用来自各种来源的相关用户数据填充表单字段，从而减少手动输入并增强用户体验。</p>
  </div>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/experimentation-ab-testing.svg" alt="规则编辑器">
    <h3>A/B 测试</h3>
    <p>A/B 测试（实验）使组织能够尝试不同的表单设计、布局和功能，以确定性能最佳的变体。</p>
  </div>
</div>

<div>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/analyticsandtracking.svg" alt="分析与跟踪">
    <h3>分析与跟踪</h3>
    <p>通过内置分析和跟踪功能深入了解用户行为、表单交互和提交率，从而实现数据驱动的表单优化。</p>
  </div>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/adobe-workfront.svg" alt="与 Adobe Workfront 集成 ">
    <h3> 任务管理 </h3>
    <p>与 Adobe Workfront 集成使团队能够管理表单创建和维护任务，确保简化的工作流程。</p>
  </div>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/data-binding.svg" alt="数据绑定">
    <h3>数据绑定</h3>
    <p>数据绑定实现了表单字段和后端数据源的直接连接，支持结构化投诉数据存储的实时更新和高级数据映射。</p>
  </div>
</div>

<div>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/publish-unpublish.svg" alt="国际化/本地化">
    <h3>发布/取消发布</h3>
    <p>轻松控制表单的可见性 — 只需单击几下即可直接从编辑器中发布或取消发布表单，从而允许您实时动态管理可用性和内容更新。</p>
  </div>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/submit-actions.svg" alt="提交操作">
    <h3>提交操作</h3>
    <p>提交操作支持后端集成、条件提交逻辑、安全端点和预处理器，简化提交工作流程。</p>
  </div>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/custom-components.svg" alt="任务管理">
    <h3>自定义组件</h3>
    <p>自定义组件允许开发人员通过创建针对特定组织用例定制的独特元素来扩展表单功能。</p>
  </div>
</div>

<div>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/editor-customization.svg" alt="编辑器自定义">
    <h3>编辑器自定义</h3>
    <p>开发人员可以通过 UI 扩展来扩展编辑器的功能，从而实现符合特定组织需求的定制解决方案。</p>
  </div>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/embedding-forms.svg" alt="嵌入表单">
    <h3>嵌入表单</h3>
    <p>使用通用编辑器的内置嵌入组件将表单直接嵌入到 Edge Delivery Services Sites，实现无缝的用户体验。</p>
  </div>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/thank-you.svg" alt="自定义组件">
    <h3>谢谢配置</h3>
    <p>轻松地自定义成功提交表单后向用户显示的确认信息或页面。
    </p>
  </div>
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

通用编辑器提供以下现成的表单组件：

<table>
  <thead>
    <tr>
      <th></th> 
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
      <td>要求用户使用 Google reCaptcha 或 HCaptcha 完成人工验证任务，从而防止垃圾邮件。</td>
    </tr>
    <tr>
      <td><b>复选框</b></td>
      <td>允许用户配置复选框。</td>
    </tr>
    <tr>
      <td><b>复选框组</b></td>
      <td>允许用户从一个组中选择多个选项。</td>
    </tr>
    <tr>
      <td><b>日期选取器</b></td>
      <td>允许用户使用日程表界面选择日期。</td>
    </tr>
    <tr>
      <td><b>下拉列表</b></td>
      <td>在预定义列表中提供单选或多选选项。</td>
    </tr>
    <tr>
      <td><b>电子邮件</b></td>
      <td>使用基本格式验证捕获电子邮件地址。</td>
    </tr>
    <tr>
      <td><b>文件附件</b></td>
      <td>支持上传文档、图像或其他文件类型。</td>
    </tr>
    <tr>
      <td><b>表单片段</b></td>
      <td>可重复使用的表单组件，用于地址字段或联系详细信息等部分。</td>
    </tr>
    <tr>
      <td><b>图像</b></td>
      <td>支持在表单内上传和显示图像。</td>
    </tr>
    <tr>
      <td><b>模态</b></td>
      <td>显示弹出窗口对话框，通常用于警告、附加信息或确认。</td>
    </tr>
    <tr>
      <td><b>数值字段</b></td>
      <td>捕获数值输入，允许验证数字或范围。</td>
    </tr>
    <tr>
      <td><b>面板</b></td>
      <td>使用可扩展/折叠面板来组织表单部分。</td>
    </tr>
    <tr>
      <td><b>单选按钮</b></td>
      <td>允许从一组选项中进行单选。</td>
    </tr>
    <tr>
      <td><b>评分</b></td>
      <td>允许用户提供星级评分。</td>
    </tr>
    <tr>
      <td><b>重置按钮</b></td>
      <td>将表单字段重置为其默认状态。</td>
    </tr>
    <tr>
      <td><b>提交按钮</b></td>
      <td>触发器表单提交并启动定义的工作流程。</td>
    </tr>
    <tr>
      <td><b>电话号码字段</b></td>
      <td>捕获基于国家/地区格式的电话号码。</td>
    </tr>
    <tr>
      <td><b>文本</b></td>
      <td>通过复选框提供一个专门用于显示法律条款和收集用户协议的分区。</td>
    </tr>
    <tr>
      <td><b>文本字段</b></td>
      <td>捕获单行输入，例如姓名或电子邮件地址。</td>
    </tr>
    <tr>
      <td><b>向导</b></td>
      <td>指导用户逐步完成多部分表单流程。</td>
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


In-addtion to pre-built form components, the Universal editor also provides support for:

* **Embedding Forms in Another Webpage**: The Universal Editor supports embedding forms directly into Edge Deliver Services Sites pages. This can be done using the embed component provided out of the box.

* **Validation Messages**: Validation messages provide real-time feedback to users when they enter incorrect or incomplete data. Features include:
    * Dynamic Error Display: Instantly alerts users to errors, such as invalid email addresses or missing required fields.
    * Customizable Messages: Allows form authors to define user-friendly error texts.
    * Rule-Based Validation: Supports advanced validation logic, such as checking dependencies between fields or implementing conditional rules.

* **Hidden Fields**: Hidden fields store data invisibly within the form, often for backend processing or prefilled values. Use cases include:
    * Passing contextual information (e.g., user ID or session data) to the backend without displaying it to users.
    * Capturing metadata like timestamps or tracking IDs.
    * Hidden fields are not visible to end-users but can be prefilled, updated dynamically, or used in workflows.

* **Custom Components**: Custom components allow developers to extend the functionality of forms by creating specialized or third-party integrations. Features include:
    * Flexibility: Developers can design unique form elements tailored to specific use cases.
    * Third-Party Integration: Embed widgets or tools like payment gateways, analytics trackers, or AI-driven input fields.
    * Seamless Compatibility: Custom components can integrate with the Universal Editor's drag-and-drop interface and existing features like data binding or validation.

* **Thank you Configuration**: Customize the acknowledgment message or page shown after form submission.
-->


## 入门培训

要启用通用编辑器及其高级功能（如规则编辑器），请通过您的正式电子邮件ID向我们发送电子邮件： aem-forms-ea@adobe.com 。 Adobe团队将帮助您转变构建表单的体验。

## 常见问题解答(FAQ)

**Q.谁可以使用通用编辑器？**
通用编辑器专为广泛的受众而设计，包括：

* 希望构建美观表单的内容创建者。
* 需要高级自定义和集成功能的开发人员。
* 寻求可扩展、安全且合规的表单解决方案的组织。

**问：我是否可以将使用通用编辑器创建的表单集成到现有系统中？**
当然。 通用编辑器支持与后端系统的无缝数据绑定，支持实时更新和高级数据映射。 它还与Adobe Workfront等工具集成以便进行任务管理，并支持数据提交工作流的安全端点。

**问：是否可以自定义表单组件？**
是的，通用编辑器允许开发人员创建针对特定组织需求的自定义组件。 此外，您还可以通过UI扩展和自定义工作流扩展编辑器的功能。

**问：通用编辑器如何处理辅助功能？**
通用编辑器在设计中严格遵守辅助功能标准，包括WCAG（Web内容辅助功能准则）。 这可确保残障人士可以使用表单，提供包容性的体验。

**问：我可以从表单中获得什么类型的分析？**
通用编辑器包括内置的分析和跟踪工具，用于监控用户交互、表单提交率和转化量度。 这些见解有助于优化您的表单以获得更好的性能。


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
        width: calc(30% - 10px);;
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
