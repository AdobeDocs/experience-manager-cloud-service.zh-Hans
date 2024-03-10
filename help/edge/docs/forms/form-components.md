---
title: 表单组件和属性
description: 本文档概述了 AEM Forms Edge Delivery Service 中可用的表单组件及其属性。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: 7d087d41-9313-482a-a905-8955b0999781
source-git-commit: 2aa70e78764616f41fe64e324c017873cfba1d5b
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 92%

---

# 表单组件和属性：AEM Forms Edge Delivery Service

AEM Forms Edge交付服务允许您使用各种组件创建用户友好的交互式表单。 这些组件可满足不同类型的数据收集需求，并且可以轻松定制以满足您的特定需求。


![包含某些组件和属性的示例电子表格](/help/edge/assets/sample-form-in-spreadsheet.png)

自适应Forms块会生成 [均匀HTML结构](/help/edge/docs/forms/style-theme-forms.md) 用于所有字段类型和容器（面板），确保一致性。 这种一致性结构让[表单样式设计](/help/edge/docs/forms/style-theme-forms.md)变得更加容易。

## 可用组件

以下是可用组件的概述：

### 输入字段

- 所有有效的 HTML5“[input types](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types)”和“[textarea](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea)”。例如，按钮、复选框、颜色、日期、本地日期时间、电子邮件、文件、隐藏、图像、月份、数字、密码、单选、范围、重置、提交、电话、文本、时间、URL 和星期。

### 选择控件

- [复选框组](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/checkbox)：用于选择多个选项。
- [单选按钮组](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/radio)：用于从一个组中仅选择一个选项。
- [下拉菜单](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select)：显示选项菜单。例如，下拉框。

### 容器

- 面板/容器：将相关的表单元素组合在一起，以便更好地组织。这是[字段集](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset)和[图例](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/legend)的组合。






## 组件属性

每个表单组件都带有各种属性，允许您控制其行为和外观。以下是自适应Forms块组件支持的属性：


| 属性 | 适用组件 | 详细信息 |
|--------------|------------------------------|----------------------------------------------------------------------|
| 类型 | 所有 | 指定组件的类型。该属性决定输入字段的行为和外观。例如，对于文本输入，类型可以是“文本”、对于电子邮件输入来说是“电子邮件”、对于密码输入来说是“密码”。自适应Forms块支持  <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types">所有有效的HTML5输入类型</a>， <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea">文本区域</a>， <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select">选择</a>、和 <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">字段集</a> 作为类型。 |
| 类型 | 所有 | 指定组件的类型。该属性决定输入字段的行为和外观。例如，对于文本输入，类型可以是“文本”、对于电子邮件输入来说是“电子邮件”、对于密码输入来说是“密码”。自适应Forms块支持  <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types">所有有效的HTML5输入类型</a>， <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea">文本区域</a>， <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select">选择</a>、和 <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">字段集</a> 作为类型。 |
| 名称 | 所有 | 标识表单提交的组件。名称属性在将表单数据提交到服务器时使用，将用户输入与特定字段相关联。 |
| 标签 | 所有 | 向用户提供上下文信息。标签是显示在组件旁边的文本，指导用户输入哪些信息。 |
| 价值 | 文本、密码、电子邮件、数字、范围、日期及其变体（本地日期时间、月、周、时间）、复选框、单选、隐藏、提交、按钮 | 指定组件的初始值。对于文本输入、文本区域和选择元素，这是显示的默认文本或选项。对于单选和复选框组件，这是选择它们时提交的值/数据。值属性可选，但对于复选框和单选输入应视为必要属性。 |
| 占位符 | 文本、电话、电子邮件、密码、日期（及其变体，如月、周、时间、本地日期时间）、数字、范围 | 提供预期输入的提示。占位符属性提供一个简短的提示，描述输入字段的预期值。一旦用户开始输入，该提示就会消失。 |
| 描述 | 所有 | 提供有关组件的附加信息并用作帮助文本。描述字段可进一步解释填写该组件的目的或说明。它帮助用户理解输入字段的上下文。 |
| 可见 | 所有 | 控制初始可见性。可见性属性是一个布尔属性，用于确定在加载表单时组件最初是可见还是隐藏状态。如果设置为 true，则显示该字段；否则，字段隐藏。 |
| 必填 | 文本、电话、电子邮件、密码、日期及其变体（本地日期时间、月、周、时间）、数字、复选框、单选、文件、选择（下拉菜单）、文本区域 | 指示提交前是否必须填写该字段。必要属性是一个布尔属性，用于指定用户在提交表单之前是否必须为字段提供输入。 |
| 最小值 | 日期（及其变体，如月、周、时间、本地日期时间）、数字、范围 | 指定允许的最小值。“最小值”属性设置用户可以在字段中输入的最小值。例如，对于数字输入，该属性定义了可接受的最低数字。 |
| 最大值 | 日期（及其变体，如月、周、时间、本地日期时间）、数字、范围 | 指定允许的最大值。“最大值”属性设置用户可以在字段中输入的最小值。例如，对于日期输入，该属性定义可接受的最高日期。 |
| 接受 | 文件 | 定义允许的文件类型。“接受”属性是一个以逗号分隔的唯一文件类型说明符列表，用于限制用户可以在文件输入字段中选择的文件类型。 |
| 多个 | 文件 | 允许多选。“多选”属性是与文件输入字段一起使用的布尔属性。当设置为 true 时，用户可以选择多个文件。 |
| 选项 | 下拉列表 | 指定下拉菜单的选项。“选项”属性是一个以逗号分隔的下拉菜单选项列表，定义向用户显示的可选选项。 |
| 已选中 | 复选框、单选按钮 | 确定默认情况下是否选择该字段。“已选中”属性是与复选框和单选输入一起使用的布尔属性。当设置为 true 时，表示加载表单时默认选择该字段。 |
| 字段集 | 所有 | 对字段进行分组以在表单中创建视觉上不同的部分。“字段集”元素将表单中的相关字段分组，在视觉上将字段分开以改善组织和用户体验。</br>要组织字段集中的一组字段，只需使用 `fieldset` 属性并指定其“名称”属性即可。在下面的示例中，我们演示了如何将单选按钮封装在单个字段集中，以便更好地组织。![字段集示例](/help/edge/assets/fieldset-example.png) |



<!--

## Supported HTML 5 input types in Adaptive Forms Block

The Adaptive Forms Block supports a range of HTML 5 input types, and it also seamlessly renders forms created with AEM core components.
Here is the table which outlines how core components correspond to their HTML-5 input types in Edge Delivery:
<table>
 <tbody>
  <tr>
   <td><b>Core Components</b> </td>
   <td><b>HTML 5 input type</b> </td>
   <td><b>Details</b></td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/form-container.html">Form Container</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#form">form </td>
   <td> Create a form to capture user inputs.
   </td>
  </tr>
  <tr>
   <td><a herf="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/text-input.html">Text Input</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/text">text</a></td>
   <td> Defines a single-line text input field. </td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/number-input.html">Number Input</a></td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/number">number</a></td>
   <td>Lets user  enter a number input. You can also add built-in validation to reject non-numerical inputs. Lets user  enter a number input. You can also add built-in validation to reject non-numerical inputs. Initially, the input field is displayed as a number input. If a user applies a display pattern, it changes to text to allow the author to apply number formatting, since HTML 5 lacks support for display patterns. However, when the user clicks it, it returns to typing numbers.</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/date-picker.html">Date Picker</a></td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/date">date </a></td>
   <td> Create an input field for entering a date. You have the option to input the date either through a text box, which validates the entry, or through a dedicated date picker interface. Initially, the native date input field is displayed. If a user applies a display pattern, it changes to text to allow the user to apply formatting, since HTML 5 lacks support for display patterns. However, when the user clicks it, it returns to typing a date.</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment.html">File Attachment</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/file">file</a></td>
   <td> Allows user to choose one or more files from the device storage. It supports enhanced file input validations, such as accepted file types, file size restrictions, and minimum/maximum file selection limits. </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/drop-down.html"> Dropdown List</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select">select</a></td>
   <td> Allows users to select one or more options from a list of predefined options. The options can be of type String, Number, or Boolean.</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox-group.html">Checkbox Group</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/checkbox">multiple checkbox</a></td>
   <td> Allow users to select one or more options from a list. Multiple checkboxes are generated with identical names, each corresponding to an item in the enum. </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/radio-button.html">Radio Button Group</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/radio">multiple radio</a></td>
   <td> Allows a user to select one option from a group of related options. Multiple radio buttons are generated with identical names, each corresponding to an item in the enum.</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/button.html">Button</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/button">button</a></td>
   <td>A UI element that allows users to trigger an action when clicked. </td>
  </tr>
  <tr>
   <td><a href =""https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel-container.html">Panel</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">fieldset with legend</a></td>
   <td> Group sections within a form, where a nested *legend* element adds a caption for the form.</td>
  </tr>
   <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html">Wizard</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">fieldset</a></td>
   <td>Groups related sections within a form. It also controls the arrangement, supporting display options for positioning them at the top or at the left side. </td>
  </tr>
    <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/text.html">Text</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/p">p</a></td>
   <td>A p tag marks a paragraph. In visual content, paragraphs are chunks of text separated by blank lines or an indented first line</td>
  </tr>
     <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/submit-button.html">Submit button</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/submit">submit</a></td>
   <td> A UI element that enables users to submit a form to the server upon clicking. If a user adds a submit rule to a button, it functions as the submit button. </td>
  </tr>
     <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/reset-button.html">Reset button</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/reset">reset</a></td>
   <td>A UI element that resets a form upon clicking. If a user adds a reset rule to a button, it functions as the reset button. </td>
  </tr>
    <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/email-input.html">Email Input</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/email">email</a></td>
   <td> Allows the user to enter and edit an email address. If the user adds the multiple attributes, a list of email addresses can be added or edited.</td>
  </tr>
   <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/telephone-input.html">Telephone Input</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/tel">tel</a></td>
   <td>Allows user to enter and edit a telephone number.</td>
  </tr>
   <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/header.html">Header</td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/header"> header</a></td>
   <td>It includes introductory content, typically a group of introductory or navigational aids. It is supported outside Form container. </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/footer.html">Footer</td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/footer">footer</a></td>
   <td> Contains information such as copyright data or links to related documents. It is supported outside Form container.</td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html">Accordion<a></td>
   <td><i>Not yet supported in Adaptive Forms Block</i></td>
   <td> Allows user to create expandable and collapsible sections in a form. </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html">Horizontal tabs</a></td>
   <td><i>Not yet supported in Adaptive Forms Block</i></td>
   <td>Organizes multiple sections of a form into separate tabs which are displayed horizontally.</td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/image.html">Image</a></td>
   <td><i>Not yet supported in Adaptive Forms Block</i></td>
   <td> Allows user to include images in a form.</td>
  </tr><tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/title.html">Title</a></td>
   <td><i>Not yet supported in Adaptive Forms Block</i></td>
   <td> Refers to the text that appears at the top of the form. </td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/submit-button.html">Switch</td>
   <td><i>Not yet supported in Adaptive Forms Block</i></td>
   <td> A two-state toggle that allows user to select between two states such as enabling or disabling a feature, setting, or functionality.</td>
  </tr>
 </tbody>
</table> -->

## 查看更多

- [创建并预览表单](/help/edge/docs/forms/create-forms.md)
- [启用表单，以发送数据](/help/edge/docs/forms/submit-forms.md)
- [将表单发布到 Sites 页面](/help/edge/docs/forms/publish-forms.md)
- [向表单字段添加验证](/help/edge/docs/forms/validate-forms.md)
- [改变表单主题和样式](/help/edge/docs/forms/style-theme-forms.md)
