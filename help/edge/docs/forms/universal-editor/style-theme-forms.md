---
title: 自定义 Edge Delivery Services for AEM Forms 的主题和样式
description: 有效地自定义通过 Edge Delivery Services 交付的 AEM Forms 的主题和样式，确保具有凝聚力和品牌化的用户体验。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: ac780399-34fe-457d-aaf4-b675656c024d
source-git-commit: 3b6d75b13730e920a10bc623947bc8b2d46dc5a9
workflow-type: tm+mt
source-wordcount: '1916'
ht-degree: 83%

---

# 自定义表单的外观&#x200B;

表单对于网站上的用户交互至关重要，用户可以在其中输入数据。您可以使用级联样式表 (CSS) 来设置表单字段的样式，以增强表单的视觉呈现效果，并改善用户体验。

Adaptive Forms Block 可为所有表单字段生成一致的结构。一致的结构使得开发 CSS 选择器更容易根据字段类型和字段名称来选择和设置表单字段的样式。

本文档概述了各种表单组件的 HTML 结构，有助于您了解如何为各种表单字段创建 CSS 选择器，以便设置 Adaptive Forms Block 的表单字段的样式。

在文章的最后：

- 您可以了解到 Adaptive Forms Block 中包含的默认 CSS 文件的结构。
- 您可以了解到 Adaptive Forms Block 提供的表单组件中的 HTML 结构，其中包括常规组件和特定组件，例如下拉菜单、单选按钮组和复选框组。
- 您将会学习到如何使用 CSS 选择器根据字段类型和字段名称设置表单字段的样式，从而根据需求实现一致或独特的样式。

## 了解表单字段类型

在深入研究样式设置之前，让我们回顾一下 Adaptive Forms Block 支持的常见表单[字段类型](/help/edge/docs/forms/universal-editor/create-custom-component.md#supported-fieldtypes)：

- 输入字段：包括文本输入、电子邮件输入、密码输入等。
- 复选框组：用于选择多个选项。
- 单选按钮组：用于从一个组中仅选择一个选项。
- 下拉菜单：也称为选择框，用于从列表中选择一个选项。
- 面板/容器：用于将相关的表单元素组合在一起。

## 基本样式设置准则

在设置特定表单字段的样式之前，了解[基本的 CSS 概念](https://www.w3schools.com/css/css_intro.asp)至关重要：

- [选择器](https://www.w3schools.com/css/css_selectors.asp)：CSS 选择器可让您针对特定的 HTML 元素进行样式设置。您可以使用元素选择器、类选择器或 ID 选择器。
- [属性](https://www.w3schools.com/css/css_syntax.asp)：CSS 属性定义元素的外观。用于设置表单字段的样式的常见属性包括颜色、背景颜色、边框、间距、边距等。
- [框模型](https://www.w3schools.com/css/css_boxmodel.asp)：CSS 框模型将 HTML 元素的结构描述为由间距、边框和边距包围的内容区域。
- Flexbox/网格：CSS [Flexbox](https://www.w3schools.com/css/css3_flexbox.asp) 和[网格版面](https://www.w3schools.com/css/css_grid.asp)是用于创建响应式和灵活设计的强大工具。


## 为 Adaptive Forms Block 设置表单样式

Adaptive Forms Block 提供了标准化 HTML 结构，简化了选择表单组件并设计其样式的过程：

- **更新默认样式**：您可以通过编辑表单CSS文件来修改表单的默认样式。 项目的GitHub存储库中提供了默认样式，通常位于： `https://github.com/<your-github-username>/<your-repository>/tree/main/blocks/form/form.css`。 此文件为表单提供全面的样式，支持多步向导表单，并重点使用CSS自定义属性以便于自定义。

- **CSS样式模式**： Edge Delivery Services使用基于块的CSS架构。 使用以下推荐的选择器模式：

  **主模式（推荐）：**

  ```css
  /- Block-level styling - Form container */
  .form {
      /- Styles for the entire form block */
      max-width: 600px;
      margin: 0 auto;
  }
  
  /- Form element styling */
  .form form {
      /- Styles for the actual <form> element */
      padding: 2rem;
  }
  
  /- Field wrapper styling by type */
  .form .{Type}-wrapper input {
      /- Styles for input fields */
      padding: 0.75rem;
      border: 1px solid #ccc;
  }
  ```

  **上下文特定的模式（当需要更高特殊性时）：**

  ```css
  /- When you need higher specificity for main content area */
  main .form .{Type}-wrapper input {
      /- More specific targeting */
      border-color: #007cba;
  }
  ```

## 组件结构

Adaptive Forms Block 为各种表单元素提供一致的 HTML 结构，确保更轻松地设置样式和管理。您可以使用 CSS 来操作组件以设置样式。

### 常规组件（下拉菜单、单选按钮组和复选框组除外）：

所有表单字段（下拉菜单、单选按钮组和复选框组除外）都具有以下 HTML 结构：

+++ 通用组件的 HTML 结构

```HTML
  <div class="{Type}-wrapper field-{Name}   field-wrapper" data-required={Required}>
     <label for="{FieldId}" class="field-label">First   Name</label>
     <input type="{Type}" placeholder="{Placeholder}"   maxlength="{Max}" id={FieldId}" name="{Name}"   aria-describedby="{FieldId}-description">
     <div class="field-description" aria-live="polite"  id="{FieldId}-description">
      Hint - First name should be minimum 3 characters  and a maximum of 10 characters.
     </div>
  </div>
```

- 类：div 元素包含几个用于定位特定元素和样式的类。您需要 `{Type}-wrapper` 或 `field-{Name}` 类来开发 CSS 选择器以设置表单字段的样式：
- {Type}：通过字段类型标识组件。例如，文本 (text-wrapper)、数字 (number-wrapper)、日期 (date-wrapper)。
- {Name}：通过名称标识组件。字段名称只能包含字母数字字符，名称中的多个连续破折号将替换为单个破折号 `(-)`，并且字段名称中的开头和结尾破折号将被删除。例如，名字 (field-first-name field-wrapper)。
- {FieldId}：它是自动生成的字段的唯一标识符。
- {Required}：这是一个布尔值，表示该字段是否为必填字段。
- 标签：`label` 元素为字段提供描述性文本，并使用 `for` 属性将它与输入元素关联。
- 输入：`input` 元素定义要输入的数据类型。例如：文本、数字、电子邮件。
- 描述（可选）：带类 `field-description` 的 `div` 为用户提供附加信息或说明。

**HTML 结构示例**

```HTML
<div class="text-wrapper field-first-name field-wrapper" data-required="true">
  <label for="firstName" class="field-label">First Name</label>
  <input type="text" placeholder="Enter your first name" maxlength="50" id="firstName" name="firstName" aria-describedby="firstName-description">
  <div class="field-description" aria-live="polite" id="firstName-description">
    Please enter your legal first name.
  </div>
</div>
```

+++

+++ 常规组件的 CSS 选择器

```CSS
  
  /- Primary Pattern: Target field wrapper by type */
  .form .{Type}-wrapper {
    /- Add your styles here */
    margin-bottom: 1rem;
    border-radius: 4px;
  }
  
  /- Primary Pattern: Target input fields within wrapper */
  .form .{Type}-wrapper input {
    /- Add your styles here */
    border: 1px solid #ccc;
    padding: 8px;
    border-radius: 4px;
    width: 100%;
  }
  
  /- Context-specific: Target element by field name when higher specificity needed */
  .form .field-{Name} input {
    /- Add your styles here */
    /- Use this pattern for specific field customization */
  }
  
```

- `.form .{Type}-wrapper`：基于字段类型定位字段包装器元素。 例如，`.form .text-wrapper`以所有文本字段容器为目标。
- `.form .{Type}-wrapper input`：定位包装器中的实际输入元素。 这是为表单输入设置样式的推荐模式。
- `.form .field-{Name}`：基于特定字段名称的目标元素。 例如，`.form .field-first-name`以“名字”字段容器为目标。 使用`.form .field-{Name} input`专门定向输入元素。
- **避免**： `main .form form .{Type}-wrapper` — 这会创建不必要的CSS特殊性，且更难维护。

**常规组件的示例 CSS 选择器**

```CSS
/- Primary Pattern: Target all text input fields */
.form .text-wrapper input {
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
  width: 100%;
}

/- Context-specific: Target field by name when higher specificity needed */
.form .field-first-name input {
  text-transform: capitalize;
  border-color: #007cba;
}

/- Alternative with main context if needed */
main .form .text-wrapper input {
  /- Use only when you need higher specificity */
  color: #333;
}
```

+++

### 下拉菜单组件

对于下拉菜单，使用 `select` 元素而不是 `input` 元素：

+++ 下拉组件的 HTML 结构

```HTML
<div class="{Type}-wrapper field-{Name} field-wrapper" data-required={Required}>
   <label for="{FieldId}" class="field-label">First Name</label>
   <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id={FieldId}" name="{Name}" aria-describedby="{FieldId}-description">
   <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - First name should be minimum 3 characters and a maximum of 10 characters.
   </div>
</div>
```

**示例 HTML 结构**

```HTML
<div class="drop-down-wrapper field-country field-wrapper" data-required="true">
  <label for="country" class="field-label">Country</label>
  <select id="country" name="country">
    <option value="">Select Country</option>
    <option value="US">United States</option>
    <option value="CA">Canada</option>
  </select>
  <div class="field-description" aria-live="polite" id="country-description">
    Please select your country of residence.
  </div>
</div>
```

+++

+++ 下拉组件的 CSS 选择器

以下 CSS 列出了下拉组件的一些 CSS 选择器示例。

```CSS
/- Primary Pattern: Target the dropdown wrapper */
.form .drop-down-wrapper {
  /- Add your styles here */
  display: flex;
  flex-direction: column;
  margin-bottom: 15px;
}

/- Target the select element */
.form .drop-down-wrapper select {
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
  background-color: #fff;
}

/- Style the label */
.form .drop-down-wrapper .field-label {
  margin-bottom: 5px;
  font-weight: bold;
}
```

- 锁定包装器：第一个选择器 (`.drop-down-wrapper`) 锁定外部包装器元素，确保样式应用于整个下拉组件。
- Flexbox 布局：Flexbox 垂直排列标签、下拉菜单和描述以实现干净布局。
- 标签样式：标签以更粗的字体和微小边距脱颖而出。
- 下拉样式：`select` 元素接收边框、间距和圆角以获得精美外观。
- 背景颜色：设置一致的背景颜色以实现视觉和谐。
- 箭头自定义：可选样式隐藏默认下拉箭头，并使用 Unicode 字符和定位创建自定义箭头。

+++

### 单选按钮组

与下拉组件类似，单选按钮组也拥有自己的 HTML 结构和 CSS 结构：

+++ 单选按钮组的 HTML 结构

```HTML
<fieldset class="radio-group-wrapper field-{Name} field-wrapper" id="{FieldId}" name="{Name}" data-required="{Required}">
   <legend for="{FieldId}" class="field-label">....</legend>
   <% for each radio in Group %>
   <div class="radio-wrapper field-{Name}">
      <input type="radio" value="" id="{UniqueId}" data-field-type="radio-group" name="{FieldId}">
      <label for="{UniqueId}" class="field-label">...</label>
   </div>
   <% end for %>
</fieldset>
```

**示例 HTML 结构**

```HTML
<fieldset class="radio-group-wrapper field-color field-wrapper" id="color_preference" name="color_preference" data-required="true">
  <legend for="color_preference" class="field-label">Favorite Color:</legend>
  <% for each radio in Group %>
    <div class="radio-wrapper field-color">
      <input type="radio" value="red" id="color_red" data-field-type="radio-group" name="color_preference">
      <label for="color_red" class="field-label">Red</label>
    </div>
    <div class="radio-wrapper field-color">
      <input type="radio" value="green" id="color_green" data-field-type="radio-group" name="color_preference">
      <label for="color_green" class="field-label">Green</label>
    </div>
    <div class="radio-wrapper field-color">
      <input type="radio" value="blue" id="color_blue" data-field-type="radio-group" name="color_preference">
      <label for="color_blue" class="field-label">Blue</label>
    </div>
  <% end for %>
</fieldset>
```

+++

+++ 单选按钮组的 CSS 选择器

- 定位字段集

```CSS
  main .form form .radio-group-wrapper {
    border: 1px solid #ccc;
    padding: 10px;
  }
```

此选择器针对具有 radio-group-wrapper 类的任何字段集。这对于将通用样式应用于整个单选按钮组非常有用。

- 定位单选按钮标签

```CSS
main .form form .radio-wrapper label {
    font-weight: normal;
    margin-right: 10px;
  }
```

- 根据名称锁定特定字段集中的所有单选按钮标签

```CSS
main .form form .field-color .radio-wrapper label {
  /- Your styles here */
}
```

+++

### 复选框组

+++ 复选框组的 HTML 结构

```HTML
<fieldset class="checkbox-group-wrapper field-{Name} field-wrapper" id="{FieldId}" name="{Name}" data-required="{Required}">
   <legend for="{FieldId}" class="field-label">....</legend>
   <% for each radio in Group %>
   <div class="checkbox-wrapper field-{Name}">
      <input type="checkbox" value="" id="{UniqueId}" data-field-type="checkbox-group" name="{FieldId}">
      <label for="{UniqueId}" class="field-label">...</label>
   </div>
   <% end for %>
</fieldset>
```

**示例 HTML 结构**

```HTML
<fieldset class="checkbox-group-wrapper field-topping field-wrapper" id="topping_preference" name="topping_preference" data-required="false">
  <legend for="topping_preference" class="field-label">Pizza Toppings:</legend>
  <div class="checkbox-wrapper field-topping">
    <input type="checkbox" value="pepperoni" id="topping_pepperoni" data-field-type="checkbox-group" name="topping_preference">
    <label for="topping_pepperoni" class="field-label">Pepperoni</label>
  </div>
  <div class="checkbox-wrapper field-topping">
    <input type="checkbox" value="mushrooms" id="topping_mushrooms" data-field-type="checkbox-group" name="topping_preference">
    <label for="topping_mushrooms" class="field-label">Mushrooms</label>
  </div>
  <div class="checkbox-wrapper field-topping">
    <input type="checkbox" value="onions" id="topping_onions" data-field-type="checkbox-group" name="topping_preference">
    <label for="topping_onions" class="field-label">Onions</label>
  </div>
</fieldset>
```

+++

+++ 复选框组的 CSS 选择器

- 定位外部包装器：这些选择器定位单选按钮组和复选框组的最外层容器，允许您将常规样式应用于整个组结构。这对于设置间距、对齐方式或其他与布局相关的属性非常有用。

```CSS
  
  /- Primary Pattern: Targets radio group wrappers */
  .form .radio-group-wrapper {
    margin-bottom: 20px; /- Adds space between radio groups */  
    display: flex;
    flex-direction: column;
  }

  /- Primary Pattern: Targets checkbox group wrappers */
  .form .checkbox-group-wrapper {
    margin-bottom: 20px; /- Adds space between checkbox groups */
    display: flex;
    flex-direction: column;
  }
```

- 定位组标签：此选择器定位单选按钮组和复选框组包装器中的 `.field-label` 元素。这使您能够专门为这些组设置标签样式，从而使它们更加突出。

```CSS
/- Primary Pattern: Target group labels */
.form .radio-group-wrapper legend,
.form .checkbox-group-wrapper legend {
  font-weight: bold; /- Makes the group label bold */
  margin-bottom: 0.5rem;
  font-size: var(--form-font-size-base);
}
```

- 定位单个输入和标签：这些选择器提供对单个单选按钮、复选框及其关联标签的更精细控制。您可以使用它们来调整大小、间距或应用更独特的视觉样式。

```CSS
/- Primary Pattern: Styling radio buttons */
.form .radio-group-wrapper input[type="radio"] {
  margin-right: 8px; /- Adds space between the input and its label */
  margin-bottom: 4px;
}

/- Primary Pattern: Styling radio button labels */
.form .radio-group-wrapper label {
  font-size: var(--form-font-size-base); /- Changes the label font size */
  display: flex;
  align-items: center;
}

/- Primary Pattern: Styling checkboxes */
.form .checkbox-group-wrapper input[type="checkbox"] {
  margin-right: 8px; /- Adds space between the input and its label */
  margin-bottom: 4px;
}

/- Primary Pattern: Styling checkbox labels */
.form .checkbox-group-wrapper label {
  font-size: var(--form-font-size-base); /- Changes the label font size */
  display: flex;
  align-items: center;
}
```

- 自定义单选按钮和复选框的外观：此技术隐藏默认输入并使用 `:before` 和 `:after` 伪元素来创建根据“选中”状态更改外观的自定义视觉效果。

```CSS
/- Hide the default radio button or checkbox */
main .form form .radio-group-wrapper input[type="radio"],
main .form form .checkbox-group-wrapper input[type="checkbox"] {
  opacity: 0;
  position: absolute;
}

/- Create a custom radio button */
main .form form .radio-group-wrapper input[type="radio"] + label::before {
  /- ... styles for custom radio button ... */
}

main .form form .radio-group-wrapper input[type="radio"]:checked + label::before {
  /- ... styles for checked radio button ... */
}

/- Create a custom checkbox */
main .form form .checkbox-group-wrapper input[type="checkbox"] + label::before {
  /- ... styles for custom checkbox ... */
}

main .form form .checkbox-group-wrapper input[type="checkbox"]:checked + label::before {
  /- ... styles for checked checkbox ... */
}
```

+++

### 面板/容器组件

+++ 面板/容器组件的 HTML 结构

```HTML
<fieldset class="panel-wrapper field-{PanelName} field-wrapper">
  <legend for="{id}" class="field-label" data-visible="false">bannerComponent</legend>
  <div class="{Type}-wrapper field-{Name} field-wrapper">
    <label for="{FieldId}" class="field-label">First Name</label>
    <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id={FieldId}" name="{Name}">
    <div class="field-description" aria-live="polite" id="{FieldId}-description">
      Hint - First name should be minimum 3 characters and a maximum of 10 characters.
    </div>
  </div>
</fieldset>
```

**示例 HTML 结构**

```HTML
<fieldset class="panel-wrapper field-login field-wrapper">
  <legend for="login" class="field-label" data-visible="false">Login Information</legend>
  <div class="text-wrapper field-username field-wrapper">
    <label for="username" class="field-label">Username</label>
    <input type="text" placeholder="Enter your username" maxlength="50" id="username" name="username">
    <div class="field-description" aria-live="polite" id="username-description">
      Please enter your username or email address.
    </div>
  </div>
  <div class="password-wrapper field-password field-wrapper">
    <label for="password" class="field-label">Password</label>
    <input type="password" placeholder="Enter your password" maxlength="20" id="password" name="password">
    <div class="field-description" aria-live="polite" id="password-description">
      Your password must be at least 8 characters long.
    </div>
  </div>
</fieldset>
```

- Fieldset 元素充当面板容器，具有 panel-wrapper 类和基于面板名称 (field-login) 进行样式设置的附加类。
- 图例元素(`<legend>`)用作包含文本“登录信息”和类字段标签的面板标题。 data-visible=&quot;false&quot; 属性可以与 JavaScript 一起使用来控制标题的可见性。
- 在字段集中，多个。{Type}-wrapper 元素（在本例中为 .text-wrapper 和 .password-wrapper）代表面板中的各个表单字段。
- 每个包装器都包含一个标签、输入字段和描述，与前面的示例类似。

+++

+++ 面板/容器组件的 CSS 选择器示例

1. 定位面板：

```CSS
  /- Target the entire panel container */
  main .form form .panel-wrapper {
    /- Add your styles here (e.g., border, padding, background color) */
    border: 1px solid #ccc;
    padding: 15px;
    border-radius: 4px;
    margin-bottom: 20px;
 }
```

-  `.panel-wrapper` 选择器使用 panel-wrapper 类来设置所有元素的样式，为所有面板创建一致的外观。

1. 定位面板标题：

```CSS
  /- Target the legend element (panel title) */
  .panel-wrapper legend {
    /- Add your styles here (e.g., font-weight, font-size) */
    font-weight: bold;
    font-size: 16px;
    padding-bottom: 5px;
    margin-bottom: 10px;
    border-bottom: 1px solid #ddd; /- Optional: create a separation line */
  }
```

-  `.panel-wrapper legend` 选择器设置面板内图例元素的样式，使标题在视觉上脱颖而出。


1. 定位面板中的各个字段：

```CSS
/- Target all form field wrappers within a panel */
main .form form .panel-wrapper .{Type}-wrapper {
  /- Add your styles here (e.g., margin) */
  margin-bottom: 10px;
}
```

-  `.panel-wrapper .{Type}-wrapper` 选择器针对面板中具有 `.{Type}-wrapper` 类的所有包装器，允许您设置表单字段之间的间距样式。

1. 定位特定领域（可选）：

```CSS
  /- Target the username field wrapper */
  main .form form .panel-wrapper .text-wrapper.field-username {
    /- Add your styles here (specific to username field) */
  }

  /- Target the password field wrapper */
  main .form form .panel-wrapper .password-wrapper.field-password {
    /- Add your styles here (specific to password field) */
  }
```

- 这些可选选择器允许您在面板中锁定特定的字段包装器以实现独特的样式，例如突出显示用户名字段。

+++

### 可重复面板

+++ 可重复面板的 HTML 结构

```HTML
<fieldset class="panel-wrapper field-{PanelName} field-wrapper">
  <legend for="{id}" class="field-label" data-visible="false">bannerComponent</legend>
  <div class="{Type}-wrapper field-{Name} field-wrapper">
    <label for="{FieldId}" class="field-label">First Name</label>
    <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id={FieldId}" name="{Name}">
    <div class="field-description" aria-live="polite" id="{FieldId}-description">
      Hint - First name should be minimum 3 characters and a maximum of 10 characters.
    </div>
</fieldset>
```

**示例 HTML 结构**

```HTML
<fieldset class="panel-wrapper field-contact field-wrapper" data-repeatable="true">
  <legend for="contact-1" class="field-label" data-visible="false">Contact Information</legend>
  <div class="text-wrapper field-name field-wrapper">
    <label for="name-1" class="field-label">Name</label>
    <input type="text" placeholder="Enter your name" maxlength="50" id="name-1" name="contacts[0].name">
    <div class="field-description" aria-live="polite" id="name-1-description">
      Please enter your full name.
    </div>
  </div>
  <div class="email-wrapper field-email field-wrapper">
    <label for="email-1" class="field-label">Email</label>
    <input type="email" placeholder="Enter your email address" maxlength="100" id="email-1" name="contacts[0].email">
    <div class="field-description" aria-live="polite" id="email-1-description">
      Please enter a valid email address.
    </div>
  </div>
</fieldset>

<fieldset class="panel-wrapper field-contact field-wrapper" data-repeatable="true">
  <legend for="contact-2" class="field-label" data-visible="false">Contact Information</legend>
  <div class="text-wrapper field-name field-wrapper">
    <label for="name-2" class="field-label">Name</label>
    <input type="text" placeholder="Enter your name" maxlength="50" id="name-2" name="contacts[1].name">
    <div class="field-description" aria-live="polite" id="name-2-description">
      Please enter your full name.
    </div>
  </div>
  <div class="email-wrapper field-email field-wrapper">
    <label for="email-2" class="field-label">Email</label>
    <input type="email" placeholder="Enter your email address" maxlength="100" id="email-2" name="contacts[1].email">
    <div class="field-description" aria-live="polite" id="email-2-description">
      Please enter a valid email address.
    </div>
  </div>
</fieldset>
```

每个面板具有与单个面板示例相同的结构，并具有附加属性：

- data-repeatable=&quot;true&quot;：此属性指示可以使用 JavaScript 或框架动态重复面板。

- 唯一 ID 和名称：面板中的每个元素都有一个唯一 ID（例如 name-1、email-1）和基于面板索引的名称属性（例如 name=&quot;contacts[0 ].name”）。这样可以在提交多个面板时进行正确的数据收集。

+++

+++ 可重复面板的 CSS 选择器

- 定位所有可重复面板：

```CSS
  /- Target all panels with the repeatable attribute */
 main .form form .panel-wrapper[data-repeatable="true"] {
    /- Add your styles here (e.g., border, margin) */
    border: 1px solid #ccc;
    padding: 15px;
    border-radius: 4px;
    margin-bottom: 20px;
  }
```

选择器对所有可重复的面板进行样式设置，确保一致的外观和感觉。


- 定位面板中的各个字段：

```CSS
/- Target all form field wrappers within a repeatable panel */
main .form form .panel-wrapper[data-repeatable="true"] .{Type}-wrapper {
  /- Add your styles here (e.g., margin) */
  margin-bottom: 10px;
}
```

此选择器对可重复面板中的所有字段包装器进行样式设置，从而保持字段之间的间距一致。

- 定位特定领域（在面板内）：

```CSS
/- Target the name field wrapper within the first panel */
main .form form .panel-wrapper[data-repeatable="true"][data-index="0"] .text-wrapper.field-name {
  /- Add your styles here (specific to first name field) */
}

/- Target all
```

+++

### 文件附件

+++ 文件附件的 HTML 结构

```HTML
<div class="file-wrapper field-{FileName} field-wrapper">
  <legend for="{id}" class="field-label" data-visible="false"> File Attachment </legend>
  <div class="file-drag-area">
    <div class="file-dragIcon"></div>
    <div class="file-dragText">Drag and Drop To Upload</div>
    <button class="file-attachButton" type="button">Attach</button>
    <input type="file" accept="audio/*, video/*, image/*, text/*, application/pdf" id="{id}" name="{FileName}" autocomplete="off" multiple="" required="required">
  </div>
  <div class="files-list">
    <div data-index="0" class="file-description">
      <span class="file-description-name">ClaimForm.pdf</span>
      <span class="file-description-size">26 kb</span>
      <button class="file-description-remove" type="button"></button>
    </div>
  </div>
</div>
```

**示例 HTML 结构**


```HTML
<div class="file-wrapper field-claim_form field-wrapper">
  <legend for="claim_form" class="field-label" data-visible="false">File Attachment</legend>
  <div class="file-drag-area">
    <div class="file-dragIcon"></div>
    <div class="file-dragText">Drag and Drop To Upload</div>
    <button class="file-attachButton" type="button">Attach</button>
  </div>
  <input type="file" accept="audio/*, video/*, image/*, text/*, application/pdf" id="claim_form"
         name="claim_form" autocomplete="off" multiple="" required="required" data-max-file-size="2MB">
  <div class="files-list">
    </div>
</div>
```

- 类属性使用为文件附件提供的名称（claim_form）。
- 输入元素的 id 和名称属性与文件附件名称 (claim_form) 匹配。
- 文件列表部分最初是空的。当文件上传时，它会用 JavaScript 动态填充。

+++

+++ 文件附件组件的 CSS 选择器

- 定位整个文件附件组件：

```CSS
/- Target the entire file attachment component */
main .form form .file-wrapper {
  /- Add your styles here (e.g., border, padding) */
  border: 1px solid #ccc;
  padding: 15px;
  border-radius: 4px;
  margin-bottom: 20px;
}
```

该选择器设置整个文件附件组件的样式，包括图例、拖动区域、输入字段和列表。

- 定位特定元素：

```CSS
/- Target the drag and drop area */
main .form form .file-wrapper .file-drag-area {
  /- Add your styles here (e.g., background color, border) */
  background-color: #f0f0f0;
  border: 1px dashed #ddd;
  padding: 10px;
  text-align: center;
}

/- Target the file input element */
main .form form .file-wrapper input[type="file"] {
  /- Add your styles here (e.g., hide the default input) */
  display: none;
}

/- Target individual file descriptions within the list (populated dynamically) */
main .form form .file-wrapper .files-list .file-description {
  /- Add your styles here (e.g., margin, display) */
  display: flex;
  justify-content: space-between;
  margin-bottom: 5px;
}

/- Target the file name within the description */
main .form form .file-wrapper .files-list .file-description .file-description-name {
  /- Add your styles here (e.g., font-weight) */
  font-weight: bold;
}
```

这些选择器允许您单独设置文件附件组件各个部分的样式。您可以调整样式以符合您的设计偏好。

+++


## 设置组件的样式

您还可以根据表单字段的特定类型 (`{Type}-wrapper`) 或单个名称 (`field-{Name}`) 来设置其样式。这允许更精细地控制和自定义表单外观。

### 基于字段类型的样式设置

您可以使用 CSS 选择器来锁定特定字段类型并一致地应用样式。

+++ HTML 结构

```HTML
<div class="{Type}-wrapper field-{Name} field-wrapper" data-required={Required}>
   <label for="{FieldId}" class="field-label">First Name</label>
   <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id={FieldId}" name="{Name}" aria-describedby="{FieldId}-description">
   <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - First name should be minimum 3 characters and a maximum of 10 characters.
   </div>
</div>
```

**示例 HTML 结构**

```HTML
<div class="text-wrapper field-name field-wrapper" data-required="true">
  <label for="name" class="field-label">Name</label>
  <input type="text" placeholder="Enter your name" maxlength="50" id="name" name="name">
</div>

<div class="number-wrapper field-age field-wrapper" data-required="true">
  <label for="age" class="field-label">Age</label>
  <input type="number" placeholder="Enter your age" id="age" name="age">
</div>

<div class="email-wrapper field-email field-wrapper" data-required="true">
  <label for="email" class="field-label">Email Address</label>
  <input type="email" placeholder="Enter your email" id="email" name="email">
</div>
```

- 每个字段都包含在具有多个类的 `div` 元素中：
   - `{Type}-wrapper`：标识字段的类型。例如，`form-text-wrapper`、`form-number-wrapper`、`form-email-wrapper`。
   - `field-{Name}`：通过名称标识字段。例如，`form-name`、`form-age`、`form-email`。
   - `field-wrapper`：所有字段包装器的通用类。
- `data-required` 属性指示该字段是必填字段还是可选字段。
- 每个字段都有相应的标签、输入元素和潜在的附加元素（例如占位符和描述）。


+++


+++ 示例 CSS 选择器

```CSS
/- Primary Pattern: Target all text input fields */
.form .text-wrapper input {
  /- Add your styles here */
  width: 100%;
  padding: var(--form-input-padding);
}

/- Primary Pattern: Target all number input fields */
.form .number-wrapper input {
  /- Add your styles here */
  letter-spacing: 2px; /- Example for adding letter spacing to all number fields */
  text-align: center;
}
```

+++

### 基于字段名称的样式设置

您还可以按名称锁定各个字段以应用唯一样式。

+++ HTML 结构

```HTML
<div class="{Type}-wrapper field-{Name} field-wrapper" data-required={Required}>
   <label for="{FieldId}" class="field-label">First Name</label>
   <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id="{FieldId}" name="{Name}" aria-describedby="{FieldId}-description">
   <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - Enter the 6 digit number sent to your mobile number.
   </div>
</div>
```

**示例 HTML 结构**

```HTML
<div class="number-wrapper field-otp field-wrapper" data-required="true">
  <label for="otp" class="field-label">OTP</label>
  <input type="number" placeholder="Enter your OTP" maxlength="6" id="otp" name="otp" aria-describedby="otp-description">
  <div class="field-description" aria-live="polite" id="otp-description">
    Hint - Enter the 6 digit number sent to your mobile number.
   </div>
</div>
```

+++

+++ 示例 CSS 选择器

```CSS
/- Primary Pattern: Target specific field by name */
.form .field-otp input {
   letter-spacing: 2px;
   text-align: center;
   font-family: monospace;
}

/- Context-specific: Use higher specificity when needed */
main .form .field-otp input {
   /- Use only when you need to override other styles */
   font-weight: bold;
}
```

此 CSS 针对位于具有类 `field-otp` 的元素内的所有输入元素。Edge Delivery Services表单结构遵循自适应Forms块惯例，其中容器使用特定于字段的类进行标记，例如“field-otp”用于名为“otp”的字段。

+++

## CSS文件结构和引用

### **默认样式位置**

默认表单样式位于：

```
https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/blocks/form/form.css
```

### **本地项目结构**

在您的Edge Delivery Services项目中：

```
/blocks/form/form.css          // Main form block styles
/styles/styles.css             // Global site styles
/styles/lazy-styles.css        // Additional component styles
```

### **自定义CSS集成**

1. **项目级自定义**：将样式添加到`/styles/styles.css`
2. **特定于表单的自定义**：修改`/blocks/form/form.css`
3. **组件覆盖**：在自定义CSS中使用适当的特定性选择器

## CSS问题疑难解答

### **CSS特殊性问题**

```css
/- ❌ Problem: Styles not applying */
.text-wrapper input {
  color: red;
}

/- ✅ Solution: Match or exceed existing specificity */
.form .text-wrapper input {
  color: red;
}

/- ✅ Alternative: Use higher specificity when needed */
main .form .text-wrapper input {
  color: red;
}
```

### **CSS变量覆盖问题**

```css
/- ❌ Problem: Variables not working */
.form {
  --form-border-color: blue; /- Local scope only */
}

/- ✅ Solution: Define in root scope */
:root {
  --form-border-color: blue; /- Global scope */
}
```

### **常见选择器错误**

```css
/- ❌ Incorrect: Assumes direct nesting */
.form form input {
  /- This might miss inputs in wrappers */
}

/- ✅ Correct: Target actual structure */
.form .text-wrapper input {
  /- Targets actual HTML structure */
}

/- ❌ Avoid: Unnecessary specificity */
main .form form .text-wrapper input {
  /- Too specific, harder to override */
}

/- ✅ Preferred: Balanced specificity */
.form .text-wrapper input {
  /- Easier to maintain and override */
}
```

### **表单状态样式**

```css
/- Validation states */
.form .field-wrapper.error input {
  border-color: var(--form-error-color);
}

.form .field-wrapper.success input {
  border-color: var(--form-success-color);
}

/- Loading state */
.form[data-submitting="true"] {
  opacity: 0.7;
  pointer-events: none;
}

/- Disabled state */
.form input:disabled {
  background-color: var(--form-input-disabled-background);
  cursor: not-allowed;
}
```

### **特定于组件的最佳实践**

#### **按钮样式**

```css
/- Primary buttons */
.form .button-wrapper button[type="submit"] {
  background-color: var(--form-focus-color);
  color: white;
  border: none;
  padding: var(--form-input-padding);
  border-radius: var(--form-border-radius);
}

/- Secondary buttons */
.form .button-wrapper button[type="reset"] {
  background-color: transparent;
  color: var(--form-text-color);
  border: 1px solid var(--form-border-color);
}
```

#### **响应表单设计**

```css
/- Mobile-first approach */
.form {
  width: 100%;
  padding: 1rem;
}

/- Tablet and up */
@media (min-width: 768px) {
  .form {
    max-width: var(--form-max-width);
    padding: var(--form-padding);
  }
}
```

## 最佳实践摘要

1. **使用CSS自定义属性**：利用变量设置一致的主题
2. **遵循基于块的架构**：使用`.form`作为主块选择器
3. **避免过度特异性**：除非必要，否则不要使用`main .form form`
4. **目标包装器**：使用`.{Type}-wrapper`模式进行组件定位
5. **保持一致性**：在整个项目中使用相同的选择器模式
6. **跨设备测试**：确保表单在移动设备、平板电脑和桌面上正常运行
7. **验证辅助功能**：确保样式不会干扰屏幕阅读器或键盘导航


