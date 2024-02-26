---
title: 自定义AEM Forms Edge Delivery Service表单的主题和样式
description: 自定义AEM Forms Edge Delivery Service表单的主题和样式
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 4a3ebcf7985253ebca24e90ab57ae7eaf3e924e9
workflow-type: tm+mt
source-wordcount: '1285'
ht-degree: 0%

---


# 设置表单字段样式

Forms对于用户在网站上的交互至关重要，允许用户输入数据。 本指南介绍了在中设计各种表单字段样式的基础知识 [表单块](/help/edge/docs/forms/create-forms.md)，帮助您创建美观且用户友好的表单。

## 了解表单字段类型

在深入研究样式之前，让我们回顾表单块支持的常见表单字段类型：

* 输入字段：包括文本输入、电子邮件输入、密码输入等。
* 复选框组：用于选择多个选项。
* 单选按钮组：用于从组仅选择一个选项。
* 下拉列表：也称为选择框，用于从列表中选择一个选项。
* 面板/容器：用于将相关的表单元素分组在一起。

## 基本样式设计原则

在为特定表单字段设置样式之前，了解基本CSS概念至关重要：

* 选择器： CSS选择器允许您定位特定的HTML元素以进行样式设置。 可以使用元素选择器、类选择器或ID选择器。
* 属性： CSS属性定义元素的可视外观。 设置表单字段样式的常见属性包括颜色、背景颜色、边框、边距、边距等。
* 方框模型： CSS方框模型将HTML元素的结构描述为一个由边距、边框和边距包围的内容区域。
* Flexbox/Grid：CSS Flexbox和Grid布局是用于创建响应式灵活设计的强大工具。

## 为表单块设置表单样式

表单块提供了一个标准化的HTML结构，从而简化了表单组件的选择和样式设置过程：

* **更新默认样式**：您可以通过编辑 `/blocks/form/form.css file`. 此文件为表单提供全面的样式，支持多步向导表单。 它强调使用自定义CSS变量来轻松进行自定义、维护和跨表单的统一样式。 有关将表单块添加到项目的说明，请参阅 [创建表单](/help/edge/docs/forms/create-forms.md).

* **自定义**：使用默认值 `forms.css` 将其作为基础，并进行自定义以修改表单组件的外观，使其具有视觉吸引力的用户友好性。 文件的结构鼓励组织并维护表单的样式，从而在整个网站中促进一致的设计。

## forms.css结构的细分

* **全局变量：** 定义于 `:root` 级别，这些变量(`--variable-name`)存储样式表中使用的值，以便保持一致性和便于更新。 这些变量定义颜色、字体大小、填充和其他属性。 您可以声明自己的全局变量或修改现有变量以更改表单样式。

* **通用选择器样式：** 此 `*` 选择器匹配表单中的每个元素，确保样式默认应用于所有组件，包括设置 `box-sizing` 属性至 `border-box`.

* **表单样式：** 本节重点介绍如何使用选择器定位特定HTML元素来设置表单组件的样式。 它定义输入字段、文本区域、复选框、单选按钮、文件输入、表单标签和说明的样式。

* **向导样式（如果适用）：** 此部分专门用于设置向导布局的样式，这是一种多步骤表单，每一步显示一个。 它定义向导容器、字段集、图例、导航按钮和响应式布局的样式。

* **媒体查询：** 这些为不同的屏幕大小提供样式，并相应地调整布局和样式。

* **其他样式：**：本节介绍成功或错误消息的样式、文件上传区域以及在表单中可能遇到的其他元素。


## 组件结构

表单块为各种表单元素提供了一致的HTML结构，确保更易于样式化和管理。 您可以使用CSS处理组件以进行样式设置。

### 常规组件（下拉列表、单选按钮组和复选框组除外）：

所有表单字段（下拉列表、单选按钮组和复选框组除外）均具有以下HTML结构：

#### HTML结构

```HTML
<div class="form-{Type}-wrapper form-{Name} field-wrapper" data-required={Required}>
  <label for="{FieldId}" class="field-label">Field Label</label>
  <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id="{FieldId}" name="{Name}" aria-describedby="{FieldId}-description">
  <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - Description of the field.
  </div>
</div>
```

* 类： div元素具有几个用于定位特定元素和样式的类。 您需要 `form-{Type}-wrapper` 或 `form-{Name}` 用于开发CSS选择器以设置表单字段样式的类：
   * {Type}：按字段类型标识组件。 例如，文本(form-text-wrapper)、数字(form-number-wrapper)、日期(form-date-wrapper)。
   * {Name}：按名称标识组件。 字段名称只能包含字母数字字符，名称中的多个连续短划线将替换为单个短划线 `(-)`删除字段名称中的开始和结束短划线。 例如，名字(form-first-name field-wrapper)。
   * {FieldId}：它是自动生成的字段的唯一标识符。
   * {Required}：它是一个布尔值，指示字段是否为必填字段。
* 标签： `label` 要素为字段提供说明性文本，并使用 `for` 属性。
* 输入： `input` 元素定义要输入的数据类型。 例如，文本、数字、电子邮件。
* 描述（可选）： `div` 与类 `field-description` 为用户提供其他信息或说明。

**示例**

```HTML
<div class="form-text-wrapper form-first-name field-wrapper" data-required="true">
  <label for="firstName" class="field-label">First Name</label>
  <input type="text" placeholder="Enter your first name" maxlength="50" id="firstName" name="firstName" aria-describedby="firstName-description">
  <div class="field-description" aria-live="polite" id="firstName-description">
    Please enter your legal first name.
  </div>
</div>
```

#### 常规组件的CSS选择器

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

* `.form-{Type}-wrapper`：定位外部 `div` 元素标识。 例如， `.form-text-wrapper` 定位所有文本输入字段。
* `.form-{Name}`：进一步根据特定字段名称选择元素。 例如， `.form-first-name` 定位“名字”文本字段。

**示例：**

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


### 下拉组件

对于下拉菜单， `select` 元素而不使用 `input` 元素：


#### HTML结构

```HTML
<div class="form-drop-down-wrapper form-{Name} field-wrapper" data-required={required}>
  <label for="{FieldId}" class="field-label">First Name</label>
  <select id="{FieldId}" name="{Name}"><option></option><option></option></select>
  <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - First name should be minimum 3 characters and a maximum of 10 characters.
  </div>
</div>
```

**示例**

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

#### 下拉组件的CSS选择器

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

* 定位包装器：第一个选择器(`.form-drop-down-wrapper`)定位外部包装器元素，确保样式应用于整个下拉组件。
* Flexbox布局：Flexbox垂直排列标签、下拉菜单和说明，以实现简洁的布局。
* 标签样式：标签突出显示，字体粗细而边距较浅。
* 下拉列表样式：选择元素接收边框、内边距和圆角，以提供光亮的外观。
* 背景颜色：为视觉和谐设置一致的背景颜色。
* 箭头自定义：可选样式隐藏默认的下拉箭头，并使用Unicode字符和位置创建自定义箭头。

### 单选框和复选框组

与下拉组件类似，单选框和复选框组也有自己的HTML结构和CSS注意事项：

#### 单选按钮组HTML结构

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


#### 单选按钮组HTML结构

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

#### 单选框和复选框组的CSS选择器

**定位外部包装器**


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

这些选择器定位单选框和复选框组的最外部容器，从而可以将常规样式应用于整个组结构。 此设置可用于设置间距、对齐方式或其他与布局相关的属性。

**定位组标签**

```CSS
.form-radio-group-wrapper .field-label,
.form-checkbox-group-wrapper .field-label {
 font-weight: bold; /* Makes the group label bold */
}
```

此选择器面向 `.field-label` 单选框和复选框组包装器中的元素。 这允许您为这些组设置特定的标签样式，这有可能使它们更加突出。

**定位单个输入和标签**

```CSS
/* Styling radio buttons */
.form-radio-group-wrapper input[type="radio"] {
  margin-right: 5px; /* Adds space between the input and its label */
} 

/* Styling radio button labels */
.form-radio-group-wrapper label {
  font-size: 15px; /* Changes the label font size */
}

/* Styling checkboxes */
.form-checkbox-group-wrapper input[type="checkbox"] {
  margin-right: 5px;  /* Adds space between the input and its label */ 
}

/* Styling checkbox labels */
.form-checkbox-group-wrapper label {
  font-size: 15px; /* Changes the label font size */
}
```

这些选择器对单个单选按钮、复选框及其相关标签提供了更细粒度的控制。 您可以使用这些设置调整大小、间距或应用更多不同的视觉样式。


**自定义单选按钮和复选框的外观**

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

.form-radio-group-wrapper input[type="radio"]:checked + label::before {
  background-color: #007bff; 
}

/* Create a custom checkbox */
/* Similar styling as above, with adjustments for a square shape */
```

此技术会隐藏默认输入，并使用：before和：after伪元素来创建自定义可视化图表，这些可视化图表会根据“选中”状态更改外观。


## 样式字段

除了前面介绍的常规样式设置技术外，您还可以根据表单字段的特定类型或单个名称来设置表单字段的样式。 这允许对表单外观进行更细粒度的控制和自定义。

### 根据字段类型设置样式

您可以使用CSS选择器来定位特定的字段类型，并以一致的方式应用样式。

**示例HTML结构**

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

* 每个字段都封装在 `div` 元素具有以下几个类：
   * `form-{Type}-wrapper`：标识字段类型。 例如， `form-text-wrapper`， `form-number-wrapper`， `form-email-wrapper`.
   * `form-{Name}`：通过名称标识字段。 例如 `form-name`， `form-age`， `form-email`.
   * `field-wrapper`：所有字段包装器的泛型类。
* 此 `data-required` 属性指明字段是必填字段还是可选字段。
* 每个字段都有一个对应的标签、输入元素和潜在的其他元素，如占位符和描述。

例如：

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

### 设置特定字段类型的样式

您还可以按名称定位各个字段以应用唯一样式。

**示例HTML结构**

```HTML
<div class="form-number-wrapper form-otp field-wrapper" data-required="true">
  <label for="otp" class="field-label">OTP</label>
  <input type="number" placeholder="Enter your OTP" maxlength="6" id="otp" name="otp">
</div>
```

**CSS选择器**

```CSS
.form-otp input {
   letter-spacing: 2px
}
```

* 选择器：此CSS定位位于具有类的元素中的所有输入元素 `form-otp`. 您的HTML结构遵循表单块的约定，这意味着有一个标有“form-otp”类的容器包含名为“otp”的字段。

* 属性和值：此代码适用 `letter-spacing: 2px`. 此CSS属性控制输入字段文本内容中各个字母之间的间距。