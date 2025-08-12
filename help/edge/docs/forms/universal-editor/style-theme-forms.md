---
title: 自定义 Edge Delivery Services for AEM Forms 的主题和样式
description: 有效地自定义通过 Edge Delivery Services 交付的 AEM Forms 的主题和样式，确保具有凝聚力和品牌化的用户体验。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: ac780399-34fe-457d-aaf4-b675656c024d
source-git-commit: bf35f847f6f00d21915dfedb10cf38ea74344988
workflow-type: tm+mt
source-wordcount: '2493'
ht-degree: 55%

---

# 自定义表单的外观&#x200B;

在适用于AEM Forms的Edge Delivery Services中实施表单样式设置时，需要深入了解CSS自定义属性、基于块的架构和组件特定的定位策略。 与传统表单样式设置方法不同，自适应Forms块实施了一个系统化的设计令牌系统，该系统能够在实现一致主题化的同时维护Edge Delivery Services的性能和可访问性优势。

自适应Forms块架构在所有表单组件中生成标准化的HTML结构，为CSS定位和自定义创建可预测的模式。 这种一致性使开发人员能够实施全面的样式系统，这些系统可以在复杂的表单实施中进行扩展，同时保留基于块的性能优化，这些优化可使Edge Delivery Services变得异常快速。

本全面指南涵盖Edge Delivery Services生态系统中表单样式设置的技术基础，包括CSS自定义属性系统、组件HTML结构模式以及高级样式设置技术。 该文档为创建复杂的品牌表单体验提供了理论理解和实践指导。

## 您将掌握的内容

**CSS自定义属性掌握**：了解控制表单外观的完整变量系统，包括颜色方案、排版比例、间距系统和布局参数。 了解如何覆盖和扩展这些属性以实施全面的品牌主题。

**组件架构了解**：深入了解每个表单组件类型使用的HTML结构模式，从而在不破坏基础功能或辅助功能的情况下实现精确的CSS定位和自定义。

**高级样式设置技术**：实施复杂的样式设置模式，包括基于状态的样式、响应式设计集成以及保持了Edge Delivery Services快速加载特性的性能优化自定义策略。

**专业实施策略**：学习行业标准的表单样式设置方法，包括设计系统集成、可维护的CSS架构和复杂样式设置场景的故障排除技术。

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




## 具有CSS自定义属性的综合表单样式

自适应Forms块利用基于自定义属性（CSS变量）构建的复杂CSS架构，支持在所有表单组件间进行系统化主题化和一致的样式。 了解此结构对于有效的表单自定义和品牌化至关重要。

### 了解forms.css架构

默认表单样式位于位于`/blocks/form/form.css`的项目存储库中，并遵循优先处理可维护性、一致性和自定义灵活性的结构化方法。 该架构包含几个关键组件：

**CSS自定义属性Foundation**：样式系统基于在`:root`级别定义的CSS自定义属性构建，提供了一个跨所有表单组件级联的集中式主题系统。 这些变量可建立颜色、排版规则、间距和布局属性的设计令牌。

**基于块的CSS结构**： Edge Delivery Services采用基于块的架构，其中`.form`类用作所有表单相关样式的主命名空间，从而确保正确的范围隔离并防止CSS与其他页面组件冲突。

**组件特定的样式**：使用一致的包装器模式(`.{Type}-wrapper`)为各个表单组件设置样式，为不同的字段类型提供可预测的定位，同时保持总体设计系统的完整性。

### CSS自定义属性引用和自定义

表单样式系统包含50多种CSS自定义属性，这些属性控制表单外观和行为的各个方面。 了解这些属性可以在保持设计一致性的同时实现全面的自定义。

+++ 颜色和主题设定变量

颜色系统通过精心组织的自定义属性为表单奠定了完整的视觉基础：

```css
:root {
    /* Primary color system */
    --background-color-primary: #fff;
    --label-color: #666;
    --border-color: #818a91;
    --form-error-color: #ff5f3f;
    
    /* Button color system */
    --button-primary-color: #5F8DDA;
    --button-secondary-color: #666;
    --button-primary-hover-color: #035fe6;
    
    /* Form-specific color applications */
    --form-background-color: var(--background-color-primary);
    --form-input-border-color: var(--border-color);
    --form-invalid-border-color: #ff5f3f;
    --form-label-color: var(--label-color);
}
```

**实际自定义示例**：要为表单实施深色主题，请覆盖基色变量：

```css
:root {
    --background-color-primary: #1a1a1a;
    --label-color: #e0e0e0;
    --border-color: #404040;
    --form-error-color: #ff6b6b;
    --button-primary-color: #4a9eff;
}
```

由于系统使用变量引用而不是硬编码值，因此这一更改会传播到所有表单组件。

+++

+++ 排版规则和间距变量

排版样式和间距变量提供对文本表示和布局间距的全面控制：

```css
:root {
    /* Font size system */
    --form-font-size-m: 22px;
    --form-font-size-s: 18px;
    --form-font-size-xs: 16px;
    
    /* Component-specific typography */
    --form-label-font-size: var(--form-font-size-s);
    --form-label-font-weight: 400;
    --form-title-font-weight: 600;
    --form-input-font-size: 1rem;
    
    /* Spacing system */
    --form-field-horz-gap: 40px;
    --form-field-vert-gap: 20px;
    --form-input-padding: 0.75rem 0.6rem;
    --form-padding: 0 10px;
}
```

**实际自定义示例**：若要使用较小的排版规则创建更紧凑的表单布局：

```css
:root {
    --form-font-size-m: 18px;
    --form-font-size-s: 14px;
    --form-font-size-xs: 12px;
    --form-field-horz-gap: 20px;
    --form-field-vert-gap: 15px;
    --form-input-padding: 0.5rem 0.4rem;
}
```

+++

+++ 布局和结构变量

布局变量控制表单维度、网格行为和组件排列：

```css
:root {
    /* Form layout */
    --form-width: 100%;
    --form-columns: 12;
    --form-submit-width: 100%;
    
    /* Card-based components */
    --form-card-border-radius: 4px;
    --form-card-padding: 0.6rem 0.8rem;
    --form-card-shadow: 0 1px 2px rgb(0 0 0 / 3%);
    --form-card-hover-shadow: 0 2px 4px rgb(0 0 0 / 6%);
    
    /* Wizard-specific layout */
    --form-wizard-padding: 0px;
    --form-wizard-padding-bottom: 160px;
    --form-wizard-step-legend-padding: 10px;
}
```

**实际自定义示例**：要创建具有增强视觉深度的卡片样式表单：

```css
:root {
    --form-card-border-radius: 12px;
    --form-card-padding: 1.5rem 2rem;
    --form-card-shadow: 0 4px 12px rgb(0 0 0 / 8%);
    --form-card-hover-shadow: 0 8px 24px rgb(0 0 0 / 12%);
    --form-background-color: #f8f9fa;
}

.form {
    background: var(--form-background-color);
    border-radius: var(--form-card-border-radius);
    box-shadow: var(--form-card-shadow);
    padding: var(--form-card-padding);
    max-width: 600px;
    margin: 2rem auto;
}
```

+++

### css样式模式和最佳实践

自适应Forms块遵循特定的CSS模式，以确保在所有组件间可维护、高性能且一致的样式。

+++ 主要样式模式

**块级表单容器**：针对总体布局和背景样式定位主表单容器：

```css
.form {
    /* Form-wide styles */
    max-width: 800px;
    margin: 0 auto;
    background-color: var(--form-background-color);
    padding: var(--form-padding);
    border-radius: var(--form-card-border-radius);
}
```

**组件包装器模式**：使用一致包装器类的目标特定字段类型：

```css
/* Text input fields */
.form .text-wrapper input {
    padding: var(--form-input-padding);
    border: var(--form-input-border-size) solid var(--form-input-border-color);
    font-size: var(--form-input-font-size);
    border-radius: 4px;
    width: 100%;
}

/* Email input fields */
.form .email-wrapper input {
    padding: var(--form-input-padding);
    border: var(--form-input-border-size) solid var(--form-input-border-color);
    font-size: var(--form-input-font-size);
}

/* Button styling */
.form .button-wrapper button {
    background-color: var(--form-button-background-color);
    color: var(--form-button-color);
    padding: var(--form-button-padding);
    border: var(--form-button-border);
    font-size: var(--form-button-font-size);
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.2s ease;
}

.form .button-wrapper button:hover {
    background-color: var(--form-button-background-hover-color);
}
```

+++

+++ 高级自定义模式

**特定字段的定位**：针对唯一的样式要求，按名称定位各个字段：

```css
/* Style specific fields */
.form .field-email input {
    background-image: url('data:image/svg+xml;...'); /* Email icon */
    background-repeat: no-repeat;
    background-position: right 12px center;
    padding-right: 40px;
}

.form .field-phone input {
    text-align: center;
    letter-spacing: 1px;
    font-family: monospace;
}
```

**基于状态的样式**：实现验证和交互状态：

```css
/* Validation states */
.form .field-wrapper[data-valid="false"] input {
    border-color: var(--form-error-color);
    box-shadow: 0 0 0 2px rgba(255, 95, 63, 0.1);
}

.form .field-wrapper[data-valid="true"] input {
    border-color: #28a745;
    box-shadow: 0 0 0 2px rgba(40, 167, 69, 0.1);
}

/* Focus states */
.form .text-wrapper input:focus,
.form .email-wrapper input:focus {
    outline: none;
    border-color: var(--button-primary-color);
    box-shadow: 0 0 0 2px rgba(95, 141, 218, 0.2);
}
```

+++


## 组件结构

Adaptive Forms Block 为各种表单元素提供一致的 HTML 结构，确保更轻松地设置样式和管理。您可以使用 CSS 来操作组件以设置样式。

+++ 常规组件（下拉菜单、单选按钮组和复选框组除外）：

所有表单字段（下拉菜单、单选按钮组和复选框组除外）都具有以下 HTML 结构：

### 通用组件的 HTML 结构

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

#### 常规组件的 CSS 选择器

```css
/* Primary Pattern: Target field wrapper by type */
.form .{Type}-wrapper {
    /* Container styling for specific field types */
    margin-bottom: 1rem;
    border-radius: 4px;
}

/* Primary Pattern: Target input fields within wrapper */
.form .{Type}-wrapper input {
    /* Input field styling using CSS custom properties */
    border: var(--form-input-border-size) solid var(--form-input-border-color);
    padding: var(--form-input-padding);
    border-radius: 4px;
    width: 100%;
    font-size: var(--form-input-font-size);
}

/* Context-specific: Target element by field name when higher specificity needed */
.form .field-{Name} input {
    /* Field-specific customizations */
    /* Use this pattern for unique styling requirements */
}
```

- `.form .{Type}-wrapper`：基于字段类型定位字段包装器元素。 例如，`.form .text-wrapper`以所有文本字段容器为目标。
- `.form .{Type}-wrapper input`：定位包装器中的实际输入元素。 这是为表单输入设置样式的推荐模式。
- `.form .field-{Name}`：基于特定字段名称的目标元素。 例如，`.form .field-first-name`以“名字”字段容器为目标。 使用`.form .field-{Name} input`专门定向输入元素。
- **避免**： `main .form form .{Type}-wrapper` — 这会创建不必要的CSS特殊性，且更难维护。

**常规组件的示例 CSS 选择器**

```css
/* Primary Pattern: Target all text input fields */
.form .text-wrapper input {
    border: var(--form-input-border-size) solid var(--form-input-border-color);
    padding: var(--form-input-padding);
    border-radius: 4px;
    width: 100%;
    font-size: var(--form-input-font-size);
    background-color: var(--form-input-background-color);
}

/* Context-specific: Target field by name when higher specificity needed */
.form .field-first-name input {
    text-transform: capitalize;
    border-color: var(--button-primary-color);
}

/* Alternative with main context if needed */
main .form .text-wrapper input {
    /* Use only when you need higher specificity */
    color: var(--form-label-color);
}
```

+++

+++ 下拉菜单组件

对于下拉菜单，使用 `select` 元素而不是 `input` 元素：

#### 下拉组件的 HTML 结构

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

#### 下拉组件的 CSS 选择器

以下 CSS 列出了下拉组件的一些 CSS 选择器示例。

```css
/* Primary Pattern: Target the dropdown wrapper */
.form .drop-down-wrapper {
    /* Container layout using flexbox */
    display: flex;
    flex-direction: column;
    margin-bottom: var(--form-field-vert-gap);
}

/* Target the select element */
.form .drop-down-wrapper select {
    border: var(--form-input-border-size) solid var(--form-input-border-color);
    padding: var(--form-input-padding);
    border-radius: 4px;
    background-color: var(--form-input-background-color);
    font-size: var(--form-input-font-size);
    color: var(--form-label-color);
}

/* Style the label */
.form .drop-down-wrapper .field-label {
    margin-bottom: 5px;
    font-weight: var(--form-label-font-weight);
    color: var(--form-label-color);
    font-size: var(--form-label-font-size);
}
```

- 锁定包装器：第一个选择器 (`.drop-down-wrapper`) 锁定外部包装器元素，确保样式应用于整个下拉组件。
- Flexbox 布局：Flexbox 垂直排列标签、下拉菜单和描述以实现干净布局。
- 标签样式：标签以更粗的字体和微小边距脱颖而出。
- 下拉样式：`select` 元素接收边框、间距和圆角以获得精美外观。
- 背景颜色：设置一致的背景颜色以实现视觉和谐。
- 箭头自定义：可选样式隐藏默认下拉箭头，并使用 Unicode 字符和定位创建自定义箭头。

+++

+++ 单选按钮组

与下拉组件类似，单选按钮组也拥有自己的 HTML 结构和 CSS 结构：

#### 单选按钮组的 HTML 结构

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

#### 单选按钮组的 CSS 选择器

- 定位字段集

```css
/* Target radio group container */
.form .radio-group-wrapper {
    border: var(--form-input-border-size) solid var(--form-input-border-color);
    padding: var(--form-input-padding);
    border-radius: 4px;
    margin-bottom: var(--form-field-vert-gap);
}
```

此选择器针对具有 radio-group-wrapper 类的任何字段集。这对于将通用样式应用于整个单选按钮组非常有用。

- 定位单选按钮标签

```css
/* Target radio button labels */
.form .radio-wrapper label {
    font-weight: var(--form-label-font-weight);
    margin-right: 10px;
    color: var(--form-label-color);
    font-size: var(--form-label-font-size);
    cursor: pointer;
}
```

- 根据名称锁定特定字段集中的所有单选按钮标签

```css
/* Target all radio button labels within a specific fieldset based on its name */
.form .field-color .radio-wrapper label {
    /* Field-specific radio label customizations */
    /* Add your custom styles here */
}
```

+++

+++ 复选框组

#### 复选框组的 HTML 结构

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

#### 复选框组的 CSS 选择器

- 定位外部包装器：这些选择器定位单选按钮组和复选框组的最外层容器，允许您将常规样式应用于整个组结构。这对于设置间距、对齐方式或其他与布局相关的属性非常有用。

```css
/* Primary Pattern: Targets radio group wrappers */
.form .radio-group-wrapper {
    margin-bottom: var(--form-field-vert-gap); /* Adds space between radio groups */
    display: flex;
    flex-direction: column;
    border: var(--form-fieldset-border);
    padding: var(--form-input-padding);
}

/* Primary Pattern: Targets checkbox group wrappers */
.form .checkbox-group-wrapper {
    margin-bottom: var(--form-field-vert-gap); /* Adds space between checkbox groups */
    display: flex;
    flex-direction: column;
    border: var(--form-fieldset-border);
    padding: var(--form-input-padding);
}
```

- 定位组标签：此选择器定位单选按钮组和复选框组包装器中的 `.field-label` 元素。这使您能够专门为这些组设置标签样式，从而使它们更加突出。

```css
/* Primary Pattern: Target group labels */
.form .radio-group-wrapper legend,
.form .checkbox-group-wrapper legend {
    font-weight: var(--form-title-font-weight); /* Makes the group label bold */
    margin-bottom: 0.5rem;
    font-size: var(--form-fieldset-legend-font-size);
    color: var(--form-fieldset-legend-color);
    padding: var(--form-fieldset-legend-padding);
    border: var(--form-fieldset-legend-border);
}
```

- 定位单个输入和标签：这些选择器提供对单个单选按钮、复选框及其关联标签的更精细控制。您可以使用它们来调整大小、间距或应用更独特的视觉样式。

```css
/* Primary Pattern: Styling radio buttons */
.form .radio-group-wrapper input[type="radio"] {
    margin-right: 8px; /* Adds space between the input and its label */
    margin-bottom: 4px;
    cursor: pointer;
}

/* Primary Pattern: Styling radio button labels */
.form .radio-group-wrapper label {
    font-size: var(--form-label-font-size); /* Changes the label font size */
    color: var(--form-label-color);
    font-weight: var(--form-label-font-weight);
    display: flex;
    align-items: center;
    cursor: pointer;
}

/* Primary Pattern: Styling checkboxes */
.form .checkbox-group-wrapper input[type="checkbox"] {
    margin-right: 8px; /* Adds space between the input and its label */
    margin-bottom: 4px;
    cursor: pointer;
}

/* Primary Pattern: Styling checkbox labels */
.form .checkbox-group-wrapper label {
    font-size: var(--form-label-font-size); /* Changes the label font size */
    color: var(--form-label-color);
    font-weight: var(--form-label-font-weight);
    display: flex;
    align-items: center;
    cursor: pointer;
}
```

- 自定义单选按钮和复选框的外观：此技术隐藏默认输入并使用 `:before` 和 `:after` 伪元素来创建根据“选中”状态更改外观的自定义视觉效果。

```css
/* Hide the default radio button or checkbox */
.form .radio-group-wrapper input[type="radio"],
.form .checkbox-group-wrapper input[type="checkbox"] {
    opacity: 0;
    position: absolute;
    width: 1px;
    height: 1px;
}

/* Create a custom radio button */
.form .radio-group-wrapper input[type="radio"] + label::before {
    content: '';
    display: inline-block;
    width: 16px;
    height: 16px;
    border: 2px solid var(--form-input-border-color);
    border-radius: 50%;
    margin-right: 8px;
    background-color: var(--form-input-background-color);
    transition: all 0.2s ease;
}

.form .radio-group-wrapper input[type="radio"]:checked + label::before {
    background-color: var(--button-primary-color);
    border-color: var(--button-primary-color);
    box-shadow: inset 0 0 0 3px var(--form-input-background-color);
}

/* Create a custom checkbox */
.form .checkbox-group-wrapper input[type="checkbox"] + label::before {
    content: '';
    display: inline-block;
    width: 16px;
    height: 16px;
    border: 2px solid var(--form-input-border-color);
    border-radius: 2px;
    margin-right: 8px;
    background-color: var(--form-input-background-color);
    transition: all 0.2s ease;
}

.form .checkbox-group-wrapper input[type="checkbox"]:checked + label::before {
    background-color: var(--button-primary-color);
    border-color: var(--button-primary-color);
    background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 16 16"><path fill="white" d="M13.854 3.646a.5.5 0 0 1 0 .708l-7 7a.5.5 0 0 1-.708 0l-3.5-3.5a.5.5 0 1 1 .708-.708L6.5 10.293l6.646-6.647a.5.5 0 0 1 .708 0z"/></svg>');
    background-repeat: no-repeat;
    background-position: center;
}
```

+++

+++ 面板/容器组件

#### 面板/容器组件的 HTML 结构

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


#### 面板/容器组件的 CSS 选择器示例

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

- `.panel-wrapper` 选择器使用 panel-wrapper 类来设置所有元素的样式，为所有面板创建一致的外观。

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

- `.panel-wrapper legend` 选择器设置面板内图例元素的样式，使标题在视觉上脱颖而出。


1. 定位面板中的各个字段：

```CSS
/- Target all form field wrappers within a panel */
main .form form .panel-wrapper .{Type}-wrapper {
  /- Add your styles here (e.g., margin) */
  margin-bottom: 10px;
}
```

- `.panel-wrapper .{Type}-wrapper` 选择器针对面板中具有 `.{Type}-wrapper` 类的所有包装器，允许您设置表单字段之间的间距样式。

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

+++ 可重复面板

#### 可重复面板的 HTML 结构

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


#### 可重复面板的 CSS 选择器

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


+++ 文件附件

#### 文件附件的 HTML 结构

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


#### 文件附件组件的 CSS 选择器

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

+++ 基于字段类型的样式设置

您可以使用 CSS 选择器来锁定特定字段类型并一致地应用样式。

### HTML 结构

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




### 示例 CSS 选择器

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

+++ 基于字段名称的样式设置

您还可以按名称锁定各个字段以应用唯一样式。

#### HTML 结构

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


#### 示例 CSS 选择器

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


## CSS文件结构和实施

### **参考实现**

AEM Forms样板存储库中提供了完整的表单样式引用：

```
https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/blocks/form/form.css
```

此文件用作CSS自定义属性系统的规范实施，并为所有表单样式设置奠定基础。 它包括所有CSS变量、组件样式模式和响应式设计实施的全面定义。

+++

+++ 项目集成

在Edge Delivery Services项目中，通过这种结构化方法实施表单样式：

```
/blocks/form/form.css          // Core form block styles (copied from boilerplate)
/styles/styles.css             // Global site styles and CSS variable overrides
/styles/lazy-styles.css        // Additional component enhancements
```

+++

+++ 实施策略

**CSS自定义属性覆盖**：覆盖全局样式中的表单变量以实施特定于品牌的主题：

```css
/* In /styles/styles.css */
:root {
    /* Brand-specific overrides */
    --button-primary-color: #your-brand-color;
    --form-background-color: #your-background;
    --label-color: #your-text-color;
}
```

**特定于组件的自定义项**：
在维护CSS变量系统的同时添加组件特定的样式：

```css
/* Enhanced component styling */
.form .text-wrapper input {
    border-radius: var(--form-card-border-radius);
    transition: all 0.2s ease;
}

.form .text-wrapper input:focus {
    transform: translateY(-1px);
    box-shadow: 0 0 0 3px rgba(var(--button-primary-color), 0.1);
}
```

**响应式设计集成**：在媒体查询中利用CSS自定义属性实现一致的响应式行为：

```css
@media (max-width: 768px) {
    :root {
        --form-input-padding: 0.875rem;
        --form-field-vert-gap: 1rem;
        --form-padding: 1rem;
    }
}
```

+++

### 完成样式设置实施示例

此部分演示了如何使用CSS自定义属性创建现代的品牌化表单。 为便于理解和导航，将实施划分为清楚的子部分。



+++ 1.品牌主题变量

使用CSS自定义属性定义您品牌的调色板、间距和排版规则。

```css
/* Custom brand theme */
:root {
  /* Brand color system */
  --brand-primary: #2563eb;
  --brand-secondary: #64748b;
  --brand-success: #059669;
  --brand-error: #dc2626;
  --brand-background: #f8fafc;
  
  /* Override form variables */
  --background-color-primary: #ffffff;
  --button-primary-color: var(--brand-primary);
  --button-primary-hover-color: #1d4ed8;
  --form-error-color: var(--brand-error);
  --form-background-color: var(--brand-background);
  --label-color: var(--brand-secondary);
  --border-color: #d1d5db;
  
  /* Enhanced spacing */
  --form-input-padding: 1rem;
  --form-field-vert-gap: 1.5rem;
  --form-padding: 2rem;
  
  /* Modern typography */
  --form-font-size-s: 16px;
  --form-label-font-weight: 500;
}
```


+++

+++ 2.表单容器样式

将现代背景、边框半径和阴影应用于表单容器，以获得美观的布局。


```css
/* Enhanced form container */
.form {
    background: linear-gradient(135deg, #f8fafc 0%, #f1f5f9 100%);
    border-radius: 12px;
    box-shadow: 0 10px 25px rgba(0, 0, 0, 0.05);
    max-width: 600px;
    margin: 2rem auto;
    overflow: hidden;
}
```




+++

+++ 3.输入字段样式

设置文本、电子邮件和数字输入字段的样式，以提供简洁现代的外观。


```css
/* Modern input styling */
.form .text-wrapper input,
.form .email-wrapper input,
.form .number-wrapper input {
    background: white;
    border: 2px solid var(--border-color);
    border-radius: 8px;
    padding: var(--form-input-padding);
    font-size: 16px;
    transition: all 0.2s ease;
    width: 100%;
}
```


+++

+++ 4.其他定制

您可以根据需要定向特定字段、状态或组件，以进一步扩展表单样式。 有关高级模式，请参阅之前的部分。

```css
/* Custom brand theme */
:root {
    /* Brand color system */
    --brand-primary: #2563eb;
    --brand-secondary: #64748b;
    --brand-success: #059669;
    --brand-error: #dc2626;
    --brand-background: #f8fafc;
    
    /* Override form variables */
    --background-color-primary: #ffffff;
    --button-primary-color: var(--brand-primary);
    --button-primary-hover-color: #1d4ed8;
    --form-error-color: var(--brand-error);
    --form-background-color: var(--brand-background);
    --label-color: var(--brand-secondary);
    --border-color: #d1d5db;
    
    /* Enhanced spacing */
    --form-input-padding: 1rem;
    --form-field-vert-gap: 1.5rem;
    --form-padding: 2rem;
    
    /* Modern typography */
    --form-font-size-s: 16px;
    --form-label-font-weight: 500;
}

/* Enhanced form container */
.form {
    background: linear-gradient(135deg, #f8fafc 0%, #f1f5f9 100%);
    border-radius: 12px;
    box-shadow: 0 10px 25px rgba(0, 0, 0, 0.05);
    max-width: 600px;
    margin: 2rem auto;
    overflow: hidden;
}

/* Modern input styling */
.form .text-wrapper input,
.form .email-wrapper input,
.form .number-wrapper input {
    background: white;
    border: 2px solid var(--border-color);
    border-radius: 8px;
    padding: var(--form-input-padding);
    font-size: 16px;
    transition: all 0.2s ease;
    width: 100%;
}

.form .text-wrapper input:focus,
.form .email-wrapper input:focus,
.form .number-wrapper input:focus {
    border-color: var(--brand-primary);
    box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.1);
    transform: translateY(-1px);
}

/* Enhanced button styling */
.form .button-wrapper button[type="submit"] {
    background: linear-gradient(135deg, var(--brand-primary) 0%, #1d4ed8 100%);
    color: white;
    border: none;
    border-radius: 8px;
    padding: 1rem 2rem;
    font-size: 16px;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.2s ease;
    width: 100%;
    box-shadow: 0 4px 12px rgba(37, 99, 235, 0.3);
}

.form .button-wrapper button[type="submit"]:hover {
    transform: translateY(-2px);
    box-shadow: 0 6px 20px rgba(37, 99, 235, 0.4);
}
```

这种全面的方法演示了CSS自定义属性如何在保持自适应Forms块系统的结构完整性和可访问性功能的同时，启用复杂的主题。

+++

## CSS问题疑难解答

+++ CSS特殊性问题

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

+++

+++ CSS变量覆盖问题

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

+++

+++ 表单状态样式

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

+++

+++ 常见选择器错误

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

+++



### **特定于组件的最佳实践**


+++ 按钮样式

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

+++

+++ 响应式表单设计

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

+++

## 最佳实践摘要

1. **使用CSS自定义属性**：利用变量设置一致的主题
2. **遵循基于块的架构**：使用`.form`作为主块选择器
3. **避免过度特异性**：除非必要，否则不要使用`main .form form`
4. **目标包装器**：使用`.{Type}-wrapper`模式进行组件定位
5. **保持一致性**：在整个项目中使用相同的选择器模式
6. **跨设备测试**：确保表单在移动设备、平板电脑和桌面上正常运行
7. **验证辅助功能**：确保样式不会干扰屏幕阅读器或键盘导航


