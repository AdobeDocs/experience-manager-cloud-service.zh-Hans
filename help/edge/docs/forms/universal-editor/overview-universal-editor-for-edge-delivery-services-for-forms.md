---
title: 适用于Forms的Edge Delivery Services通用编辑器
description: 使用Universal Editor for Edge Delivery Services for Forms创建自适应Forms。
feature: Edge Delivery Services
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
exl-id: d711e0d1-a2fc-4aa6-af87-6e77a7bc5d2e
source-git-commit: 744f505c8e97b6ca6947b685ddb1eba41b370cfa
workflow-type: tm+mt
source-wordcount: '1077'
ht-degree: 71%

---


# 适用于Forms的Edge Delivery Services通用编辑器

<span class="preview">此功能可通过提前访问计划使用。 要请求访问，请将您的正式地址中的电子邮件发送至<a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a>，其中包含您的GitHub组织名称和存储库名称。 例如，如果存储库URL为https://github.com/adobe/abc，则组织名称为adobe，存储库名称为abc。</span>

通用编辑器通过提供简单、直观的可视What You See Is What You Get (WYSIWYG)界面，彻底变革了Adobe Edge Delivery Services的表单创建方式。 它专为内容创建者和表单作者设计，消除了传统表单构建流程的复杂性，使非技术用户也能使用。

使用通用编辑器，您可以使用预建组件（如文本字段、复选框和单选按钮）快速设计响应式交互表单。其强大的功能集支持动态规则、无缝数据集成和高级个性化，确保每个表单都符合您的需求。

无论您是要管理轻量级客户端渲染、确保跨浏览器兼容性，还是要遵守严格的可访问性标准，通用编辑器都能为创建和管理表单提供简化的解决方案。

![通用编辑器](/help/edge/docs/forms/universal-editor/assets/universal-editor.png){width=80%, align-center} -->

## 适用于Forms的Edge Delivery Services的通用编辑器的主要功能



以下是等宽卡片的布局（使用固定宽度列）：

| ![WYSIWYG界面](/help/edge/docs/forms/universal-editor/assets/generate-forms.svg) | ![规则编辑器](/help/edge/docs/forms/universal-editor/assets/rule-editor.svg) | ![提交操作](/help/edge/docs/forms/universal-editor/assets/submit-actions.svg) |
|:-------------:|:-------------:|:-------------:|
| [**WYSIWYG界面**](/help/edge/docs/forms/universal-editor/universal-editor-user-interface.md) | [**规则编辑器**](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md) | [**提交操作**](/help/edge/docs/forms/universal-editor/submit-action.md) |
| 通用编辑器为表单设计提供了所见即所得的界面，具有预建组件库、响应式设计、基于模板的创建和实时字段修改。 | 规则编辑器允许用户使用事件驱动规则、即时验证和通过轻量级 JavaScript 和 JSON 进行错误处理来创建动态表单交互。 | 提交操作支持后端集成、条件提交逻辑、安全端点和预处理器，简化提交工作流程。 |

| ![发布/取消发布](/help/edge/docs/forms/universal-editor/assets/publish-unpublish.svg) | ![响应模式](/help/edge/docs/forms/universal-editor/assets/responsive.svg) | ![自定义组件](/help/edge/docs/forms/universal-editor/assets/custom-components.svg) |
|:-------------:|:-------------:|:-------------:|
| [**发布/取消发布**](/help/edge/docs/forms/universal-editor/publish-forms.md) | [**响应模式**](/help/edge/docs/forms/universal-editor/responsive-layout.md) | [**自定义组件**](/help/edge/docs/forms/universal-editor/create-custom-component.md) |
| 轻松控制表单的可见性 — 只需单击几下即可直接从编辑器中发布或取消发布表单。 | 设计可跨设备（台式机、平板电脑和移动设备）无缝适应的表单。使用响应式模式预览和测试各种屏幕尺寸的表单。 | 自定义组件允许开发人员通过创建针对特定组织用例定制的独特元素来扩展表单功能。 |

| ![样式](/help/edge/docs/forms/universal-editor/assets/personalization.svg) | ![预填充服务](/help/edge/docs/forms/universal-editor/assets/prefill-services.svg) | ![A/B测试](/help/edge/docs/forms/universal-editor/assets/experimentation-ab-testing.svg) |
|:-------------:|:-------------:|:-------------:|
| [**样式**](/help/edge/docs/forms/universal-editor/style-theme-forms.md) | **预填充服务**（即将推出） | [**A/B测试**](https://github.com/adobe/aem-experimentation/blob/main/documentation/experiments.md) |
| 使用CSS设置样式可让开发人员自定义表单元素的外观，并创建符合网站美学的美观设计。 | 预填服务会自动使用来自各种来源的相关用户数据填充表单字段，从而减少手动输入并增强用户体验。 | A/B测试使组织能够试验不同的表单设计、布局和功能，以识别性能最佳的变体。 |

| ![分析和跟踪](/help/edge/docs/forms/universal-editor/assets/analyticsandtracking.svg) | ![任务管理](/help/edge/docs/forms/universal-editor/assets/adobe-workfront.svg) | ![数据绑定](/help/edge/docs/forms/universal-editor/assets/data-binding.svg) |
|:-------------:|:-------------:|:-------------:|
| [**分析和跟踪**](https://www.aem.live/developer/martech-integration) | **任务管理** （即将推出） | **数据绑定** （即将推出） |
| 通过内置分析和跟踪功能深入了解用户行为、表单交互和提交率，从而实现数据驱动的表单优化。 | 与 Adobe Workfront 集成使团队能够管理表单创建和维护任务，确保简化的工作流程。 | 数据绑定允许在表单字段和后端数据源之间直接连接，支持实时更新和高级数据映射。 |

| ![验证码](/help/edge/docs/forms/universal-editor/assets/captcha.svg) | ![嵌入Forms](/help/edge/docs/forms/universal-editor/assets/embedding-forms.svg) | ![感谢您的配置](/help/edge/docs/forms/universal-editor/assets/thank-you.svg) |
|:-------------:|:-------------:|:-------------:|
| [**验证码**](/help/edge/docs/forms/universal-editor/recaptcha-forms.md) | **嵌入Forms** | [**感谢您的配置**](/help/edge/docs/forms/universal-editor/submit-action.md#show-a-custom-thank-you-message-on-adaptive-form-submission-submit-action-message-ue) |
| 使用reCAPTCHA保护表单免受自动机器人的攻击，确保安全可靠的数据收集。 | 使用通用编辑器的内置嵌入组件将表单直接嵌入到Edge Delivery Services Sites页面中。 | 轻松地自定义成功提交表单后向用户显示的确认信息或页面。 |


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

要启用通用编辑器及其高级功能（如规则编辑器），请使用您的官方电子邮件 ID 写信至 aem-forms-ea@adobe.com。Adobe 团队随时恭候您的光临，协助您改变表单创建体验。

## 常见问题解答（FAQ）

**问：谁可以使用通用编辑器？**
通用编辑器专为广大用户设计，包括：

* 希望创建具有视觉吸引力表单的内容创建者。
* 需要高级自定义和集成功能的开发人员。
* 寻求可扩展、安全和合规表单解决方案的组织。

**问：可以把使用通用编辑器创建的表单集成到我现有的系统中吗？**
绝对可以。通用编辑器支持与后端系统的无缝数据绑定，实现实时更新和高级数据映射。它还与 Adobe Workfront 等工具集成，用于任务管理，并支持用于数据提交工作流的安全端点。

**问：可以自定义表单组件吗？**
可以，通用编辑器允许开发人员创建符合特定组织需求的自定义组件。此外，您还可以通过 UI 扩展和自定义工作流来扩展编辑器的功能。

**问：通用编辑器如何处理可访问性？**
通用编辑器的设计严格遵守可访问性标准，包括 WCAG（Web 内容无障碍准则）。这可确保残障人士也能使用表单，从而提供一种包容性的体验。

**问：可以从表单中获得哪些分析结果？**
通用编辑器包含内置分析和跟踪工具，可监测用户互动、表单提交率和转化量度。这些洞察有助于优化表单，提高性能。


## 开始创建表单

{{universal-editor-see-also}}

