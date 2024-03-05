---
title: 自定义 AEM Forms Edge Delivery Service Form 的主题和样式
description: 自定义 AEM Forms Edge Delivery Service Form 的主题和样式
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: e8fbe3efae7368c940cc2ed99cc9a352bbafbc22
workflow-type: tm+mt
source-wordcount: '1275'
ht-degree: 90%

---


# 设置表单字段的样式

表单对于网站上的用户交互至关重要，允许他们输入数据。本指南介绍了在中设计各种表单字段样式的基础知识 [自适应表单块](/help/edge/docs/forms/create-forms.md)，帮助您创建美观且用户友好的表单。

## 了解表单字段类型

在深入研究样式之前，让我们回顾自适应表单块支持的常见表单字段类型：

* 输入字段：包括文本输入、电子邮件输入、密码输入等。
* 复选框组：用于选择多个选项。
* 单选按钮组：用于从一个组中仅选择一个选项。
* 下拉菜单：也称为选择框，用于从列表中选择一个选项。
* 面板/容器：用于将相关的表单元素组合在一起。

## 基本样式设置准则

在设置特定表单字段的样式之前，了解基本 CSS 概念至关重要：

* 选择器：CSS 选择器可让您针对特定的 HTML 元素进行样式设置。您可以使用元素选择器、类选择器或 ID 选择器。
* 属性：CSS 属性定义元素的外观。用于设置表单字段的样式的常见属性包括颜色、背景颜色、边框、间距、边距等。
* 框模型：CSS 框模型将 HTML 元素的结构描述为由间距、边框和边距包围的内容区域。
* Flexbox/网格：CSS Flexbox 和网格布局是用于创建响应式和灵活设计的强大工具。

## 为自适应表单块设置表单样式

自适应表单块提供标准化的HTML结构，从而简化表单组件的选择和样式设置过程：

* **更新默认样式**：您可以通过编辑 `/blocks/form/form.css file` 来修改表单的默认样式。此文件为表单提供全面的样式，并支持多步骤向导表单。它强调使用自定义 CSS 变量来轻松跨表单进行自定义、维护和统一样式设置。有关将自适应表单块添加到项目的说明，请参阅 [创建表单](/help/edge/docs/forms/create-forms.md).

* **自定义**：使用默认值 `forms.css` 作为基础，并对其进行自定义以修改表单组件的外观，使其具有视觉吸引力并且对用户友好。此文件的结构有利于组织和维护表单的样式，从而促进整个网站设计的一致性。

## forms.css 的结构细分

* **全局变量：**&#x200B;在 `:root` 级别进行定义，这些变量 (`--variable-name`) 存储整个样式表中使用的值，以确保一致并简化更新。这些变量定义颜色、字体大小、间距和其他属性。您可以声明自己的全局变量或修改现有变量以更改表单的样式。

* **通用选择器样式：**`*`选择器匹配表单中的每个元素，确保样式默认应用于所有组件，包括将 `box-sizing` 属性设置为 `border-box`。

* **表单样式设置：**&#x200B;此部分重点介绍使用选择器来定位特定 HTML 元素以设置表单组件的样式。它定义输入字段、文本区域、复选框、单选按钮、文件输入、表单标签和描述的样式。

* **向导样式（如果适用）：**&#x200B;此部分专注于设计向导布局的样式，这是一个多步骤表单，其中显示每个步骤（一次显示一个）。它定义向导容器、字段集、图例、导航按钮和响应式布局的样式。

* **媒体查询：**&#x200B;它们提供了针对不同屏幕大小的样式，并相应地调整布局和样式。

* **其他样式：**：此部分介绍了成功或错误消息的样式、文件上传区域以及表单中可能显示的其他元素。


## 组件结构

自适应表单块为各种表单元素提供了一致的HTML结构，确保更易于样式化和管理。 您可以使用 CSS 来操作组件以设置样式。

### 常规组件（下拉菜单、单选按钮组和复选框组除外）：

所有表单字段（下拉列表、单选按钮组和复选框组除外）都具有以下 HTML 结构：

#### HTML 结构

```HTML
<div class="form-{Type}-wrapper form-{Name} field-wrapper" data-required={Required}>
  <label for="{FieldId}" class="field-label">Field Label</label>
  <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id="{FieldId}" name="{Name}" aria-describedby="{FieldId}-description">
  <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - Description of the field.
  </div>
</div>
```

* 类：div 元素包含几个用于定位特定元素和样式的类。您需要 `form-{Type}-wrapper` 或 `form-{Name}` 类来开发 CSS 选择器以设置表单字段的样式：
   * {Type}：通过字段类型标识组件。例如，文本 (form-text-wrapper)、数字 (form-number-wrapper)、日期 (form-date-wrapper)。
   * {Name}：通过名称标识组件。字段名称只能包含字母数字字符，名称中的多个连续破折号将替换为单个破折号 `(-)`，并且字段名称中的开头和结尾破折号将被删除。例如，名字 (form-first-name field-wrapper)。
   * {FieldId}：它是自动生成的字段的唯一标识符。
   * {Required}：它是一个布尔值，指示该字段是否为必填字段。
* 标签：`label` 元素为字段提供描述性文本，并使用 `for` 属性将它与输入元素关联。
* 输入：`input` 元素定义要输入的数据类型。例如，文本、数字、电子邮件。
* 描述（可选）：带类 `field-description` 的 `div` 为用户提供附加信息或说明。

**HTML 结构示例**

```HTML
<div class="form-text-wrapper form-first-name field-wrapper" data-required="true">
  <label for="firstName" class="field-label">First Name</label>
  <input type="text" placeholder="Enter your first name" maxlength="50" id="firstName" name="firstName" aria-describedby="firstName-description">
  <div class="field-description" aria-live="polite" id="firstName-description">
    Please enter your legal first name.
  </div>
</div>
```

**常规组件的 CSS 选择器**

```CSS
.form-{Type}-wrapper input {
  /* Add your styles here */
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}


.form-{Name} input {
  /* Add your styles here */
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}
```

* `.form-{Type}-wrapper`：根据字段类型定位外部 `div` 元素。例如，`.form-text-wrapper` 定位所有文本输入字段。
* `.form-{Name}`：根据特定字段名称进一步选择元素。例如，`.form-first-name` 定位“名字”文本字段。

**常规组件的示例 CSS 选择器**

```CSS
/*Target all text input fields */

.form-text-wrapper input {
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}

/*Target all fields with name first-name*/

.form-first-name input {
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}
```


### 下拉菜单组件

对于下拉菜单，使用 `select` 元素而不是 `input` 元素：


#### HTML 结构

```HTML
<div class="form-drop-down-wrapper form-{Name} field-wrapper" data-required={required}>
  <label for="{FieldId}" class="field-label">First Name</label>
  <select id="{FieldId}" name="{Name}"><option></option><option></option></select>
  <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - First name should be minimum 3 characters and a maximum of 10 characters.
  </div>
</div>
```

**示例 HTML 结构**

```HTML
    <div class="form-drop-down-wrapper form-country field-wrapper" data-required="true">
      <label for="country" class="field-label">Country</label>
      <select id="country" name="country">
         <option value="">Select Country</option>
         <option value="US">United States</option>
         <option value="CA">Canada</option>
    </select>
   <div class="field-description" aria-live="polite" id="country-description">Please select your country of residence.</div>
   </div>
```

#### 下拉组件的示例 CSS 选择器

```CSS
/* Target the outer wrapper */
.form-drop-down-wrapper {
  /* Add your styles here */
  display: flex;
  flex-direction: column;
  margin-bottom: 15px;
}

/* Style the label */
.form-drop-down-wrapper .field-label {
  margin-bottom: 5px;
  font-weight: bold;
}

/* Style the dropdown itself */
.form-drop-down-wrapper select {
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
  background-color: white; /* Ensure a consistent background */
  /* Adjust arrow appearance as needed */
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
}

/* Optional: Style the dropdown arrow */
.form-drop-down-wrapper select::-ms-expand {
  display: none; /* Hide the default arrow for IE11 */
}

.form-drop-down-wrapper select::after {
  content: "\25BC";
  font-size: 12px;
  color: #ccc;
  /* Adjust positioning as needed */
  position: absolute;
  right: 10px;
  top: 50%;
  transform: translateY(-50%);
}
```

* 定位包装器：第一个选择器 (`.form-drop-down-wrapper`) 定位外部包装器元素，确保样式应用于整个下拉组件。
* Flexbox 布局：Flexbox 垂直排列标签、下拉菜单和描述以实现干净布局。
* 标签样式：标签以更粗的字体和微小边距脱颖而出。
* 下拉样式：选择元素接收边框、间距和圆角以获得精美外观。
* 背景颜色：设置一致的背景颜色以实现视觉和谐。
* 箭头自定义：可选样式隐藏默认下拉箭头，并使用 Unicode 字符和定位创建自定义箭头。

### 单选按钮组和复选框组

与下拉组件类似，单选按钮组和复选框组也拥有自己的 HTML 结构和 CSS 注意事项：

#### 单选按钮组 HTML 结构

```HTML
<div class="form-checkbox-group-wrapper form-{Name} field-wrapper" data-required={required}>
  <label class="field-label">{Label Text}</label>
  <div class="checkbox-group">
    <input type="checkbox" id="{FieldId}-1" name="{Name}" value="{Value1}">
    <label for="{FieldId}-1">{Option 1 Text}</label>
    <input type="checkbox" id="{FieldId}-2" name="{Name}" value="{Value2}">
    <label for="{FieldId}-2">{Option 2 Text}</label>
    </div>
  <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - Select multiple options (if applicable).
  </div>
</div>
```


#### 复选框组 HTML 结构

```HTML
<div class="form-checkbox-group-wrapper form-{Name} field-wrapper" data-required={required}>
  <label class="field-label">{Label Text}</label>
  <div class="checkbox-group">
    <input type="checkbox" id="{FieldId}-1" name="{Name}" value="{Value1}">
    <label for="{FieldId}-1">{Option 1 Text}</label>
    <input type="checkbox" id="{FieldId}-2" name="{Name}" value="{Value2}">
    <label for="{FieldId}-2">{Option 2 Text}</label>
    </div>
  <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - Select multiple options (if applicable).
  </div>
</div>
```

**单选按钮组和复选框组的 CSS 选择器示例**

* 定位外部包装器：这些选择器定位单选按钮组和复选框组的最外层容器，允许您将常规样式应用于整个组结构。这对于设置间距、对齐方式或其他与布局相关的属性非常有用。


  ```CSS
     /* Targets all radio group wrappers */
  .form-radio-group-wrapper {
    margin-bottom: 20px; /* Adds space between radio groups */
  }
  
  /* Targets all checkbox group wrappers */
  .form-checkbox-group-wrapper {
    margin-bottom: 20px; /* Adds space between checkbox groups */
  }
  ```


* 定位组标签：此选择器定位单选按钮组和复选框组包装器中的 `.field-label` 元素。这使您能够专门为这些组设置标签样式，从而使它们更加突出。

  ```CSS
  .form-radio-group-wrapper .field-label,
  .form-checkbox-group-wrapper .field-label {
   font-weight: bold; /* Makes the group label bold */
  }
  ```



* 定位单个输入和标签：这些选择器提供对单个单选按钮、复选框及其关联标签的更精细控制。您可以使用它们来调整大小、间距或应用更独特的视觉样式。

  ```CSS
  /* Styling radio buttons */
  .form-radio-group-wrapper input[type="radio"] {
    margin-right: 5px; /* Adds space between the input and its   label */
  } 
  
  /* Styling radio button labels */
  .form-radio-group-wrapper label {
    font-size: 15px; /* Changes the label font size */
  }
  
  /* Styling checkboxes */
  .form-checkbox-group-wrapper input[type="checkbox"] {
    margin-right: 5px;  /* Adds space between the input and its  label */ 
  }
  
  /* Styling checkbox labels */
  .form-checkbox-group-wrapper label {
    font-size: 15px; /* Changes the label font size */
  }
  ```




* 自定义单选按钮和复选框的外观：此技术隐藏默认输入并使用 :before 和 :after 伪元素来创建根据“选中”状态更改外观的自定义视觉效果。

  ```CSS
  /* Hide the default radio button or checkbox */
  .form-radio-group-wrapper input[type="radio"],
  .form-checkbox-group-wrapper input[type="checkbox"] {
    opacity: 0; 
    position: absolute; 
  }
  
  /* Create a custom radio button */
  .form-radio-group-wrapper input[type="radio"] + label::before { 
    content: "";
    display: inline-block;
    width: 16px; 
    height: 16px; 
    border: 2px solid #ccc; 
    border-radius: 50%;
    margin-right: 5px;
  }
  
  .form-radio-group-wrapper input[type="radio"]:checked +  label::before {
    background-color: #007bff; 
  }
  
  /* Create a custom checkbox */
  /* Similar styling as above, with adjustments for a square shape  */
  ```


## 设置组件的样式

您还可以根据表单字段的特定类型或单个名称来设置其样式。这允许更精细地控制和自定义表单外观。

### 基于字段类型的样式设置

您可以使用 CSS 选择器来定位特定字段类型并一致地应用样式。

**示例 HTML 结构**

```HTML
<div class="form-text-wrapper form-name field-wrapper" data-required="true">
  <label for="name" class="field-label">Name</label>
  <input type="text" placeholder="Enter your name" maxlength="50" id="name" name="name">
</div>

<div class="form-number-wrapper form-age field-wrapper" data-required="true">
  <label for="age" class="field-label">Age</label>
  <input type="number" placeholder="Enter your age" id="age" name="age">
</div>

<div class="form-email-wrapper form-email field-wrapper" data-required="true">
  <label for="email" class="field-label">Email Address</label>
  <input type="email" placeholder="Enter your email" id="email" name="email">
</div>
```

* 每个字段都包含在具有多个类的 `div` 元素中：
   * `form-{Type}-wrapper`：标识字段的类型。例如，`form-text-wrapper`、`form-number-wrapper`、`form-email-wrapper`。
   * `form-{Name}`：通过名称标识字段。例如，`form-name`、`form-age`、`form-email`。
   * `field-wrapper`：所有字段包装器的通用类。
* `data-required` 属性指示该字段是必填字段还是可选字段。
* 每个字段都有相应的标签、输入元素和潜在的附加元素（例如占位符和描述）。

**示例 CSS 选择器**

```CSS
/* Target all text input fields */
.form-text-wrapper input {
  /* Add your styles here */
}

/* Target all number input fields */
.form-number-wrapper input {
  /* Add your styles here */
  letter-spacing: 2px; /* Example for adding letter spacing to all number fields */
}
```

### 基于字段名称的样式设置

您还可以按名称定位各个字段以应用唯一样式。

**示例 HTML 结构**

```HTML
<div class="form-number-wrapper form-otp field-wrapper" data-required="true">
  <label for="otp" class="field-label">OTP</label>
  <input type="number" placeholder="Enter your OTP" maxlength="6" id="otp" name="otp">
</div>
```

**示例 CSS 选择器**

```CSS
.form-otp input {
   letter-spacing: 2px
}
```

此 CSS 针对位于具有类 `form-otp` 的元素内的所有输入元素。您的表单HTML结构遵循自适应表单块的约定，这意味着有一个标有“form-otp”类的容器包含名为“otp”的字段。


