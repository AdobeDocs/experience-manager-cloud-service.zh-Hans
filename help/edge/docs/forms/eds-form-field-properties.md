---
title: 掌握自适应表单块字段属性
description: 使用电子表格和自适应表单块字段属性更快地制作功能强大的表单！本指南列出了 EDS 表单块支持的所有属性。
feature: Edge Delivery Services
exl-id: e86ccc36-bda0-4e9d-8d65-ae7cb3fa79b7
source-git-commit: 41dd61425ce3b7536ee805580f3841e32e40ee99
workflow-type: ht
source-wordcount: '930'
ht-degree: 100%

---

# 自适应表单块字段属性

本文档概述了在 `blocks/form/form.js` 中 JSON 架构如何映射到所渲染的 HTML，重点介绍如何识别和渲染字段、常见模式以及字段特有的差异。

## 如何识别字段 (`fieldType`)？

JSON 架构中的每个字段都有一个决定如何渲染该字段的 `fieldType` 属性。`fieldType` 可以是：

- **一个特定类型**\
  例如：`drop-down`、`radio-group`、`checkbox-group`、`panel`、`plain-text`、`image`、`heading` 等。
- **一个有效的 HTML 输入类型**\
  例如：`text`、`number`、`email`、`date`、`password`、`tel`、`range`、`file` 等。
- **带有 `-input` 后缀的类型**\
  例如：`text-input`、`number-input` 等。（标准化为基本类型，如 `text`、`number`）。

如果 `fieldType` 是一个特定类型，就会使用一个&#x200B;**自定义渲染程序**。否则，它会被视为一个&#x200B;**默认的输入类型**。

请参阅以下各节，了解每种字段类型的[完整的 HTML 结构和属性](#common-html-structure)。

## 字段使用的常见属性

以下是大多数字段都使用的属性：

- `id`：指定元素 ID 并支持无障碍性。
- `name`：定义输入、选择或字段集元素的 `name` 属性。
- `label.value`、`label.richText`、`label.visible`：指定标签/图例文本、HTML 内容和可见性。
- `value`：表示字段的当前值。
- `required`：添加 `required` 属性或验证数据。
- `readOnly`、`enabled`：决定这是可编辑的或是禁用的字段。
- `description`：在字段下方显示帮助文本。
- `tooltip`：设置输入的 `title` 属性。
- `constraintMessages`：提供自定义错误消息作为数据属性。

## 常见的 HTML 结构

大多数字段都是包裹在一个包含标签和可选帮助文本的容器中进行渲染。以下代码片段展示了这种结构：

```html
<div class="<fieldType>-wrapper field-wrapper field-<name>" data-id="<id>">
<label for="<id>" class="field-label">Label</label>
<!-- Field-specific input/element here -->
<div class="field-description" id="<id>-description">Description or error
message</div>
</div>
```

对于组（单选按钮/复选框）和面板，会使用 `<legend>` 与 `<fieldset>`，而不是 `<div>/<label>`。帮助文本 <div> 只有在设置了描述的情况下存在。

## 错误消息显示

错误消息显示在 `.field-description` 元素中，这个元素中也显示会动态更新的帮助文本。

**如果一个字段无效**：

- 包装器（例如 `.field-wrapper`）会被指定为 `.field-invalid` 类。
- `.field-description` 内容会被替换为相应的错误消息。

**如果字段变成有效**：

- 就会移除 `.field-invalid` 类。
- `.field-description` 将恢复为原始帮助文本（如有），或者被移除（如果没有帮助文本）。

可以使用 JSON 中的 `constraintMessages` 属性来自定义错误消息。\
这些作为 `data-<constraint>ErrorMessage` 属性添加在包装器上（例如 `data-requiredErrorMessage`）。

## 默认输入类型（HTML 输入或 `*-input`）

如果 `fieldType` 不是特定类型，就会被视为一个标准 HTML 输入类型或者是 `<type>-input`，例如 `text`、`number`、`email`、`date`、`text-input`、`number-input`。

- 后缀 `-input` 会去除，基本类型用作此输入的 `type` 属性。
- 默认情况下，这些类型在 `renderField()` 中处理。
常见的默认输入类型为 `text`、`number`、`email`、`date`、`password`、`tel`、`range`、`file` 等。  它们也接受 `text-input`、`number-input` 等，这些被标准化为基本类型。

## 对默认输入类型的约束

根据 JSON 属性，输入元素中添加了约束属性。

| JSON 属性 | HTML 属性 | 应用到 |
|--------------|---------------|------------|
| maxLength | maxlength | 文本、电子邮件、密码、电话 |
| minLength | minlength | 文本、电子邮件、密码、电话 |
| 模式 | 模式 | 文本、电子邮件、密码、电话 |
| 最大值 | 最大 | 数字、范围、日期 |
| 最小值 | 最小值 | 数字、范围、日期 |
| 步骤 | 步骤 | 数字、范围、日期 |
| 接受 | 接受 | 文件 |
| 多个 | 多个 | 文件 |
| maxOccur | data-max | 面板 |
| minOccur | data-min | 面板 |

>[!NOTE]
>
> `multiple` 是一个布尔值属性。如果为真，就会添加 `multiple` 属性。

表单渲染程序会根据字段的 JSON 定义自动设置这些属性。

## 例如：有约束的 HTML 结构

以下示例展示了如何渲染一个带有验证约束和错误处理属性的数字字段。

```html
<div class="number-wrapper field-wrapper field-age" data-id="age"
data-required="true"
data-minimumErrorMessage="Too small" data-maximumErrorMessage="Too large">
<label for="age" class="field-label">Age</label>
<input type="number"
id="age" name="age"
value="30" required min="18"
max="99" step="1"
placeholder="Enter your age" />
<div class="field-description" id="age-description"> Description or error message
</div>
</div>
```

HTML 结构的每个部分都在数据绑定、验证、显示帮助或错误消息方面起到自己的作用。

## 字段特定的属性及其 HTML 结构

### 下拉面板

**额外的属性：**

- `enum` / `enumNames`：定义下拉面板的可选值及其显示标签。
- `type`：在设为 `array` 的情况下会启用多选。
- `placeholder`：添加一个禁用的占位符选项，在选择之前引导用户。

示例：

```html
<div class="drop-down-wrapper field-wrapper field-<name>" data-id="<id>"
data-required="true"
data-requiredErrorMessage="This field is required">
<label for="<id>" class="field-label">Label</label>
<select id="<id>" name="<name>" required title="Tooltip" multiple>
<option disabled selected value="">Placeholder</option>
<option value="opt1">Option 1</option>
<option value="opt2">Option 2</option>
</select>
<div class="field-description" id="<id>-description"> Description or error message
</div>
</div>
```

### 纯文本

**额外的属性**：

- `richText`：如果为真，就在段落中渲染 HTML。

示例：

```html
<div class="plain-text-wrapper field-wrapper field-<name>" data-id="<id>">
<label for="<id>" class="field-label">Label</label>
<p>Text or <a href="..." target="_blank">link</a></p>
</div>
```

### 复选框

**额外的属性**：

- `enum`：定义复选框的勾选和取消勾选状态的值。
- `properties.variant / properties.alignment`：指定开关样式复选框的外观样式和对齐方式。

示例：

```html
<div class="checkbox-wrapper field-wrapper field-<name>" data-id="<id>"
data-required="true"
data-requiredErrorMessage="Please check this box">
<label for="<id>" class="field-label">Label</label>
<input type="checkbox"
id="<id>"
name="<name>" value="on"
required
data-unchecked-value="off" />
<div class="field-description" id="<id>-description"> Description or error message
</div>
</div>
```

### 按钮

**额外的属性**：

- `buttonType`：通过设置按钮的类型（按钮、提交或重置）来指定按钮的行为。

示例：

```html
<div class="button-wrapper field-wrapper field-<name>" data-id="<id>">
<button id="<id>" name="<name>" type="submit" class="button"> Label
</button>
</div>
```

### 多行输入

**额外的属性**：

- `minLength`：指定在文本或文本区域输入中允许的最小字符数。
- `maxLength`：指定在文本或文本区域输入中允许的最大字符数。
- `pattern`：定义一个正则表达式，输入值必须与其匹配才算有效。
- `placeholder`：输入框或文本区域中显示的占位符文本，直到用户输入一个值。

示例：

```html
<div class="multiline-wrapper field-wrapper field-<name>" data-id="<id>"
data-minLengthErrorMessage="Too short" data-maxLengthErrorMessage="Too long">
<label for="<id>" class="field-label">Label</label>
<textarea id="<id>"
name="<name>" required
minlength="2"
maxlength="100"
pattern="[A-Za-z]+"
placeholder="Type here..."></textarea>
<div class="field-description" id="<id>-description"> Description or error message
</div>
</div>
```

### 面板

**额外的属性**：

- `repeatable`：指定面板是否可以动态重复。
- `minOccur`：设置所必需的最小面板实例数。   maxOccur：设置允许的最大面板实例数。
- `properties.variant`：定义面板的外观样式或变体。
- `properties.colspan`：指定面板在网格布局中包含的列数。
- `index`：指示面板在其父容器中的位置。
- `fieldset`：将相关字段分组到一个带有图例或标签的 `<fieldset>` 元素下。

示例：

```html
<fieldset class="panel-wrapper field-wrapper field-<name>" data-id="<id>"
name="<name>"
data-repeatable="true" data-index="0">
<legend class="field-label">Label</legend>
<!-- Nested fields here -->
<button type="button" class="add">Add</button>
<button type="button" class="remove">Remove</button>
<div class="field-description" id="<id>-description"> Description or error message
</div>
</fieldset>
```

### 单选按钮

**额外的属性**：

- `enum`：定义单选按钮字段允许使用的一组值，被用作每个单选按钮选项的值属性。

示例：

```html
<div class="radio-wrapper field-wrapper field-<name>" data-id="<id>"
data-required="true">
<label for="<id>" class="field-label">Label</label>
<input type="radio" id="<id>" name="<name>" value="opt1" required />
<div class="field-description" id="<id>-description"> Description or error message
</div>
</div>
```

### 单选按钮组

**额外的属性**：

- `enum`：定义单选按钮组的选项值列表，被用作每个单选按钮的值。
- `enumNames`：为单选按钮提供显示标签，与枚举的顺序一致。

示例：

```html
<fieldset class="radio-group-wrapper field-wrapper field-<name>" data-id="<id>"
data-required="true">
<legend class="field-label">Label</legend>
<div>
<input type="radio" id="<id>-0" name="<name>" value="opt1" required />
<label for="<id>-0">Option 1</label>
</div>
<div>
<input type="radio" id="<id>-1" name="<name>" value="opt2" />
<label for="<id>-1">Option 2</label>
</div>
<div class="field-description" id="<id>-description"> Description or error message
</div>
</fieldset>
```

### **复选框组**

**额外的属性**：

- `enum`：定义复选框组的选项值列表，用作每个复选框的值。
- `enumNames`：为复选框提供显示标签，与枚举的顺序一致。
- `minItems`：设置必须为有效性选择的最小复选框数量。
- `maxItems`：设置不会触发错误的可选择的最大复选框数量。

示例：

```html
<fieldset class="checkbox-group-wrapper field-wrapper field-<name>" data-id="<id>"
data-required="true" data-minItems="1"
data-maxItems="3">
<legend class="field-label">Label</legend>
<div>
<input type="checkbox" id="<id>-0" name="<name>" value="opt1" required />
<label for="<id>-0">Option 1</label>
</div>
<div>
<input type="checkbox" id="<id>-1" name="<name>" value="opt2" />
<label for="<id>-1">Option 2</label>
</div>
<div class="field-description" id="<id>-description"> Description or error message
</div>
</fieldset>
```

### 图像

**额外的属性**：

- `value / properties['fd:repoPath']`：定义用于渲染图像的图像源路径或存储库路径。
- `altText`：提供图像的替换文本（alt 属性）以增强无障碍性。

示例：

```html
<div class="image-wrapper field-wrapper field-<name>" data-id="<id>">
<picture>
<img src="..." alt="..." />
<!-- Optimized sources -->
</picture>
</div>
```

### 标题

**额外的属性**：

- `value`：指定标题元素内要显示的文本内容（例如 `<h2>`）。

示例：

```html
<div class="heading-wrapper field-wrapper field-<name>" data-id="<id>">
<h2 id="<id>">Heading Text</h2>
</div>
```

有关更多详细信息，请参阅 `blocks/form/form.js` 和 `blocks/form/util.js` 中的实施。


<!--Each form field is represented as a dedicated row in the spreadsheet, analogous to fields in a database table. The column headers act as labels for the various properties supported by the form field block.

Think of your form as a table in a spreadsheet, where each line represents a different question or piece of information you want to collect. The table headings tell you what kind of answers you can expect for each section.

The below table lists all the properties that are supported by the Adaptive Forms Block.

**Master Your Forms with These Adaptive Forms Block Field Properties:**

This table details all the properties you can use to customize your Adaptive Forms Block fields:

| Property | Description | Example |
|---|---|---|
| **Type** | [HTML input type](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types) (text, email, number, etc.), [textarea](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea), [select](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select), [fieldset](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset) | `text`, `email`, `radio`, `select` |
| **Name** | This defines the unique identifier for submitted data (e.g., 'email' for an email address field).  Choose a clear and unique name for each field, as the name serves as internal field identifier used for data mapping during submission. | `user_name`, `email_address` |
| **Label** | User-friendly field label | `"Full Name"`, `"Choose your country"` |
| **Value** | Default value displayed | `"John Doe"`, `"United States"` |
| **Placeholder** | Hint text within the field | `"Enter your email address"` |
| **Description** | Help text for users | `"Please enter a valid email address"` |
| **Visible** | Show/hide the field initially | `true`, `false` |
| **Mandatory** | Require a value from the user | `true`, `false` |
| **Min/Max** | Set minimum/maximum values (number, date, text length) | `18` (age), `2025-12-31` (date) |
| **Accept** | Allowed file types for file upload | `"image/jpeg,image/png"` |
| **Multiple** | Allow multiple file selections | `true`, `false` |
| **Options** | Comma-separated list for dropdown menus | `"Option 1, Option 2, Option 3"` |
| **Checked** | Default-selected radio button/checkbox | `true`, `false` |
| **Fieldset** | Group fields together | Fieldset name (e.g., `"Personal Information"`) |-->
