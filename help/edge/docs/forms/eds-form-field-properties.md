---
title: 掌握自适应Forms块字段属性
description: 使用电子表格和自适应Forms块字段属性更快地制作功能强大的表单！ 本指南列出了EDS Forms Block支持的所有属性。
feature: Edge Delivery Services
source-git-commit: ccc6439f68d8199154d4cd664b9cdb6428460a64
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 3%

---


# 自适应Forms块字段属性

本文档概述了JSON架构如何映射到在`blocks/form/form.js`中渲染的HTML，重点介绍如何识别和渲染字段、常见模式以及特定于字段的差异。

## 如何识别字段(`fieldType`)？

JSON架构中的每个字段都有一个`fieldType`属性来确定其呈现方式。 `fieldType`可以是：

- **特殊类型**\
  示例： `drop-down`、`radio-group`、`checkbox-group`、`panel`、`plain-text`、`image`、`heading`等。
- **有效的HTML输入类型**\
  示例： `text`、`number`、`email`、`date`、`password`、`tel`、`range`、`file`等。
- **后缀为`-input`的类型**\
  示例： `text-input`、`number-input`等。 （已规范化为基类型，如`text`、`number`）。

如果`fieldType`与特殊类型匹配，则使用&#x200B;**自定义渲染器**。 否则，它被视为&#x200B;**默认输入类型**。

请参阅以下各节，了解每种字段类型的[完整HTML结构和属性](#common-html-structure)。

## 字段使用的通用属性

以下是大多数字段使用的属性：

- `id`：指定元素ID并支持辅助功能。
- `name`：为输入、选择或字段集元素定义`name`属性。
- `label.value`、`label.richText`、`label.visible`：指定标签/图例文本、HTML内容和可见性。
- `value`：表示字段的当前值。
- `required`：添加`required`特性或验证数据。
- `readOnly`，`enabled`：控制该字段是可编辑的还是禁用的。
- `description`：在字段下方显示帮助文本。
- `tooltip`：设置输入的`title`属性。
- `constraintMessages`：提供自定义错误消息作为数据属性。

## 通用HTML结构

大多数字段都呈现在包含标签和可选帮助文本的包装中。 以下代码片段演示了该结构：

```html
<div class="<fieldType>-wrapper field-wrapper field-<name>" data-id="<id>">
<label for="<id>" class="field-label">Label</label>
<!-- Field-specific input/element here -->
<div class="field-description" id="<id>-description">Description or error
message</div>
</div>
```

对于组（单选框/复选框）和面板，使用带`<fieldset>`的`<legend>`而不是`<div>/<label>`。 帮助文本 <div> 仅在设置了描述时存在。

## 错误消息显示

错误消息显示在用于帮助文本（动态更新）的相同`.field-description`元素中。

**当字段无效时**：

- 包装器（例如，`.field-wrapper`）被指定为`.field-invalid`类。
- `.field-description`内容已替换为相应的错误消息。

**字段生效时**：

- 已删除`.field-invalid`类。
- `.field-description`将还原为原始帮助文本（如果可用），如果不存在则删除。

可以使用JSON中的`constraintMessages`属性定义自定义错误消息。\
这些内容在包装上添加为`data-<constraint>ErrorMessage`属性（例如，`data-requiredErrorMessage`）。

## 默认输入类型(HTML输入或`*-input`)

如果`fieldType`不是特殊类型，则会将其视为标准HTML输入类型或作为`<type>-input`，例如`text`、`number`、`email`、`date`、`text-input`、`number-input`。

- 后缀`-input`被去除，基类型被用作输入的`type`属性。
- 这些类型默认在`renderField()`中处理。
常用默认输入类型为`text`、`number`、`email`、`date`、`password`、`tel`、`range`、`file`等。  它们还接受`text-input`、`number-input`等，这些类型被规范化为基类型。

## 默认输入类型的约束

约束将根据JSON属性作为属性添加到输入元素中。

| JSON属性 | HTML属性 | 应用于 |
|--------------|---------------|------------|
| maxLength | maxlength | 文本，电子邮件，密码，电话 |
| minlength | minlength | 文本，电子邮件，密码，电话 |
| 模式 | 模式 | 文本，电子邮件，密码，电话 |
| 最大值 | 最大 | 数字、范围、日期 |
| 最小值 | 最小值 | 数字、范围、日期 |
| 步骤 | 步骤 | 数字、范围、日期 |
| 接受 | 接受 | 文件 |
| 多个 | 多个 | 文件 |
| maxOccure | data-max | 面板 |
| minOccurs | data-min | 面板 |

>[!NOTE]
>
> `multiple`是一个布尔属性。 如果为true，则添加`multiple`属性。

这些属性由表单渲染器根据字段的JSON定义自动设置。

## 示例：带有约束的HTML结构

以下示例演示如何使用验证约束和错误处理属性呈现数字字段。

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

HTML结构的每个部分在数据绑定、验证和显示帮助或错误消息方面都扮演着角色。

## 字段特定的属性及其HTML结构

### 下拉面板

**额外属性：**

- `enum` / `enumNames`：为下拉列表定义选项值及其显示标签。
- `type`：如果设置为`array`，则启用多项选择。
- `placeholder`：添加禁用的占位符选项，以便在选择之前引导用户。

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

**额外属性**：

- `richText`：如果为true，则在段落中呈现HTML。

示例：

```html
<div class="plain-text-wrapper field-wrapper field-<name>" data-id="<id>">
<label for="<id>" class="field-label">Label</label>
<p>Text or <a href="..." target="_blank">link</a></p>
</div>
```

### 复选框

**额外属性**：

- `enum`：定义复选框的选中和取消选中状态的值。
- `properties.variant / properties.alignment`：指定开关样式复选框的可视样式和对齐方式。

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

**额外属性**：

- `buttonType`：通过设置按钮的类型（按钮、提交或重置）来指定按钮的行为。

示例：

```html
<div class="button-wrapper field-wrapper field-<name>" data-id="<id>">
<button id="<id>" name="<name>" type="submit" class="button"> Label
</button>
</div>
```

### 多行输入

**额外属性**：

- `minLength`：指定在文本或文本区域输入中允许的最小字符数。
- `maxLength`：指定文本或文本区域输入中允许的最大字符数。
- `pattern`：定义输入值必须匹配才能被视为有效的正则表达式。
- `placeholder`：在输入值之前在输入或文本区域中显示占位符文本。

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

**额外属性**：

- `repeatable`：指定面板是否可以动态重复。
- `minOccur`：设置所需的最小面板实例数。   maxOccur：设置允许的面板实例的最大数量。
- `properties.variant`：定义面板的可视样式或变量。
- `properties.colspan`：指定面板在网格布局中跨越的列数。
- `index`：指示面板在其父容器中的位置。
- `fieldset`：将相关字段分组到具有图例或标签的`<fieldset>`元素下。

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

### 单选

**额外属性**：

- `enum`：定义单选字段允许的值集，用作每个单选按钮选项的值属性。

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

**额外属性**：

- `enum`：定义单选按钮组的选项值列表，用作每个单选按钮的值。
- `enumNames`：为单选按钮提供显示标签，与枚举的顺序匹配。

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

**额外属性**：

- `enum`：定义复选框组的选项值列表，用作每个复选框的值。
- `enumNames`：为复选框提供显示标签，与枚举的顺序匹配。
- `minItems`：设置必须选择的有效性复选框的最小数目。
- `maxItems`：设置触发错误之前可选择的复选框的最大数目。

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

**额外属性**：

- `value / properties['fd:repoPath']`：定义用于呈现图像的图像源路径或存储库路径。
- `altText`：为图像提供替换文本（alt属性）以提高可访问性。

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

**额外属性**：

- `value`：指定要显示在标题元素内的文本内容（例如，`<h2>`）。

示例：

```html
<div class="heading-wrapper field-wrapper field-<name>" data-id="<id>">
<h2 id="<id>">Heading Text</h2>
</div>
```

有关更多详细信息，请参阅`blocks/form/form.js`和`blocks/form/util.js`中的实现。


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

