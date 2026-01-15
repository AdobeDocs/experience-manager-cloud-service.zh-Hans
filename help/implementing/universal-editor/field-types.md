---
title: 模型定义、字段和组件类型
description: 通过示例了解通用编辑器可以在属性面板中编辑的字段和组件类型。了解如何通过创建模型定义并将其与组件关联来适配您自己的应用程序。
exl-id: cb4567b8-ebec-477c-b7b9-53f25b533192
feature: Developing
role: Admin, Developer
source-git-commit: 08e495b0859e9f0a0378a0fb8bd565bc76c777da
workflow-type: tm+mt
source-wordcount: '1604'
ht-degree: 97%

---


# 模型定义、字段和组件类型 {#field-types}

通过示例了解通用编辑器可以在属性面板中编辑的字段和组件类型。了解如何通过创建模型定义并将其与组件关联来适配您自己的应用程序。

## 概述 {#overview}

如果您想使用通用编辑器编辑您自己的应用程序，您就必须适配组件，定义在编辑器的属性面板中可以操作哪些字段和组件类型。为此，您需要创建一个模型并将组件与该模型关联。

本文档概述了模型定义、可用的字段和组件类型以及几个配置示例。

>[!TIP]
>
>如果您不熟悉如何为通用编辑器适配您的应用程序，请参阅文档[面向 AEM 开发人员的通用编辑器概述](/help/implementing/universal-editor/developer-overview.md)。

## 模型定义结构 {#model-structure}

要在通用编辑器的属性面板中配置组件，必须存在一个模型定义，并将其与该组件关联。

模型定义是一个 JSON 结构，以一个模型数组开头。

```json
[
  {
    "id": "model-id",        // must be unique
    "fields": []             // array of fields which shall be rendered in the properties panel
  }
]
```

有关如何定义 `fields` 数组的更多信息，请参阅本文档的&#x200B;**[字段](#fields)**&#x200B;部分。

您可以通过两种方式将模型与组件关联：使用[组件定义](#component-definition)或[通过适配。](#instrumentation)

### 使用组件定义进行关联 {#component-definition}

这是将模型与组件关联的首选方法。这样您就可以在组件定义中集中保持关联，并允许跨容器拖动组件。

只需将 `model` 属性包含在 `component-definition.json` 文件的 `components` 数组的组件对象中。

有关更多详细信息，请参阅文档[组件定义。](/help/implementing/universal-editor/component-definition.md)

### 通过适配进行关联 {#instrumentation}

要将模型定义与组件关联，可以使用 `data-aue-model` 属性。

```html
<div data-aue-resource="urn:datasource:/content/path" data-aue-type="component"  data-aue-model="model-id">Click me</div>
```

>[!NOTE]
>
>通用编辑器首先检查是否通过适配关联了一个模型，并在检查组件定义之前使用这个适配。这意味着：
>
>* 如果项目已经通过适配实施了与模型的关联，就将继续按原样工作，无需任何更改。
>* 如果您在[组件定义](#component-definition)和适配中都定义了模型，就总是会使用适配。

## 加载模型定义 {#loading-model}

模型创建后，就可以将其作为外部文件引用。

```html
<script type="application/vnd.adobe.aue.model+json" src="<url-of-model-definition>"></script>
```

或者您也可以用内联方式定义模型。

```html
<script type="application/vnd.adobe.aue.model+json">
  { ... model definition ... }
</script>
```

## 字段 {#fields}

字段对象具有以下类型定义。

| 配置 | 值类型 | 描述 | 必需 |
|---|---|---|---|
| `component` | `ComponentType` | 组件的渲染器 | 是 |
| `name` | `string` | 属性[或保留数据的路径](#nesting) | 是 |
| `label` | `FieldLabel` | 字段的标签 | 是 |
| `description` | `FieldDescription` | 字段的描述 | 否 |
| `value` | `FieldValue` | 这是默认值，用作占位符。 如果未设置任何值，则通用编辑器将保留在模型定义中定义为`value`的任何内容。 这可确保您看到的内容与后端中保留的内容相匹配。 | 否 |
| `valueType` | `ValueType` | 标准验证，可以是 `string`、`string[]`、`number`、`date`、`boolean` | 否 |
| `required` | `boolean` | 字段是否必需 | 否 |
| `readOnly` | `boolean` | 字段是否为只读 | 否 |
| `hidden` | `boolean` | 字段是否默认隐藏 | 否 |
| `condition` | `RulesLogic` | 根据[条件](/help/implementing/universal-editor/customizing.md#conditionally-hide)显示或隐藏字段的规则 | 否 |
| `multi` | `boolean` | 字段是否为多字段<br/>请注意，属性面板中的多字段不允许容器嵌套 | 否 |
| `validation` | `ValidationType` | 验证规则或字段的规则 | 否 |
| `raw` | `unknown` | 组件可以使用的原始数据 | 否 |

### 名称字段和嵌套 {#nesting}

`name` 字段可以直接指向当前资源的属性，对于 `cq:Pages` 中的组件，它也可以使用指向嵌套属性的路径。例如：

```json
"name": "teaser/image/fileReference"
```

### 组件类型 {#component-types}

以下是可用于渲染字段的组件类型。

| 描述 | 组件类型 |
|---|---|
| [AEM 标记](#aem-tag) | `aem-tag` |
| [AEM 内容](#aem-content) | `aem-content` |
| [布尔值](#boolean) | `boolean` |
| [复选框组](#checkbox-group) | `checkbox-group` |
| [容器](#container) | `container` |
| [内容片段](#content-fragment) | `aem-content-fragment` |
| [日期时间](#date-time) | `date-time` |
| [体验片段](#experience-fragment) | `aem-experience-fragment` |
| [多选](#multiselect) | `multiselect` |
| [数字](#number) | `number` |
| [单选按钮组](#radio-group) | `radio-group` |
| [引用](#reference) | `reference` |
| [富文本](#rich-text) | `richtext` |
| [选择](#select) | `select` |
| [选项卡](#tab) | `tab` |
| [文本](#text) | `text` |

#### AEM 标记 {#aem-tag}

AEM 标记组件类型会启用 AEM 标记选取器，用于在组件上附加标记。

>[!BEGINTABS]

>[!TAB 示例]

```json
{
  "id": "aem-tag-picker",
  "fields": [
    {
      "component": "aem-tag",
      "label": "AEM Tag Picker",
      "name": "cq:tags",
      "valueType": "string"
    }
  ]
}
```

>[!TAB 屏幕快照]

![AEM 标记组件类型的屏幕快照](assets/component-types/aem-tag-picker.png)

>[!ENDTABS]

>[!TIP]
>
>请参阅文档[管理分类数据](https://www.aem.live/docs/authoring-taxonomy)，详细了解如何使用电子表格管理您的 Edge Delivery Services 项目的分类数据。

#### AEM 内容 {#aem-content}

AEM 内容组件类型会启用 AEM 内容选取器，用于选择任何 AEM 资源。与只能选择资产的[引用组件](#reference)不同，AEM 内容组件可以引用任何 AEM 内容。它提供了一种额外的验证类型。

| 验证类型 | 值类型 | 描述 | 必需 |
|---|---|---|---|
| `rootPath` | `string` | 内容选取器在供用户选择 AEM 内容时所打开的路径，选择限制在这个目录和子目录中 | 否 |

>[!BEGINTABS]

>[!TAB 示例]

```json
{
  "id": "aem-content-picker",
  "fields": [
    {
      "component": "aem-content",
      "name": "reference",
      "value": "",
      "label": "AEM Content Picker",
      "valueType": "string",
      "validation": {
            "rootPath": "/content/refresh"
        }
    }
  ]
}
```

>[!TAB 屏幕快照]

![AEM 内容组件类型的屏幕快照](assets/component-types/aem-content-picker.png)

>[!ENDTABS]

#### 布尔值 {#boolean}

布尔值组件类型存储一个简单的真/假值，显示为一种切换开关。它提供了一种额外的验证类型。

| 验证类型 | 值类型 | 描述 | 必需 |
|---|---|---|---|
| `customErrorMsg` | `string` | 在输入的不是布尔值的情况下显示的消息 | 否 |

>[!BEGINTABS]

>[!TAB 示例 1]

```json
{
  "id": "boolean",
  "fields": [
    {
      "component": "boolean",
      "label": "Boolean",
      "name": "boolean",
      "valueType": "boolean"
    }
  ]
}
```

>[!TAB 示例 2]

```json
{
  "id": "another-boolean",
  "fields": [
    {
      "component": "boolean",
      "label": "Boolean",
      "name": "boolean",
      "valueType": "boolean",
      "validation": {
        "customErrorMsg": "Think, McFly. Think!"
      }
    }
  ]
}
```

>[!TAB 屏幕快照]

![布尔值组件类型的屏幕快照](assets/component-types/boolean.png)

>[!ENDTABS]

#### 复选框组 {#checkbox-group}

与布尔值类似，复选框组组件类型允许选择多个真/假项，显示为多个复选框。

>[!BEGINTABS]

>[!TAB 示例]

```json
{
  "id": "checkbox-group",
  "fields": [
    {
      "component": "checkbox-group",
      "label": "Checkbox Group",
      "name": "checkbox",
      "valueType": "string[]",
      "options": [
        { "name": "Option 1", "value": "option1" },
        { "name": "Option 2", "value": "option2" }
      ]
    }
  ]
}
```

>[!TAB 屏幕快照]

![复选框组组件类型的屏幕快照](assets/component-types/checkbox-group.png)

>[!ENDTABS]

#### 容器 {#container}

容器组件类型允许将组件分组，包括多字段支持。它提供了一种额外的配置。请注意，属性面板中的多字段不允许容器嵌套

| 配置 | 值类型 | 描述 | 必需 |
|---|---|---|---|
| `collapsible` | `boolean` | 容器是否可折叠 | 否 |

>[!BEGINTABS]

>[!TAB 示例]

```json
 {
  "id": "container",
  "fields": [
    {
      "component": "container",
      "label": "Container",
      "name": "container",
      "valueType": "string",
      "collapsible": true,
      "fields": [
        {
          "component": "text-input",
          "label": "Simple Text 1",
          "name": "text",
          "valueType": "string"
        },
        {
          "component": "text-input",
          "label": "Simple Text 2",
          "name": "text2",
          "valueType": "string"
        }
      ]
    }
  ]
}
```

>[!TAB 屏幕快照]

![容器组件类型的屏幕快照](assets/component-types/container.png)

>[!TAB 多字段支持]

```json
{
  "component": "container",
  "name": "test",
  "label": "Multi Text",
  "multi": true,
  "fields": [
    {
      "component": "reference",
      "name": "image",
      "value": "",
      "label": "Sample Image",
      "valueType": "string"
    },
    {
      "component": "text",
      "name": "alt",
      "value": "",
      "label": "Alt Text",
      "valueType": "string"
    }
  ]
}
```

>[!ENDTABS]



#### 内容片段 {#content-fragment}

内容片段选取器可用于选择[内容片段](/help/sites-cloud/authoring/fragments/content-fragments.md)及其变体（必需时）。它提供了一种额外的配置。

| 配置 | 值类型 | 描述 | 必需 |
|---|---|---|---|
| `variationName` | `string` | 用于存储所选变体的变量名称。如果未定义，就不显示变体选取器 | 否 |

它也提供了一种额外的验证类型。

| 验证类型 | 值类型 | 描述 | 必需 |
|---|---|---|---|
| `rootPath` | `string` | 内容选取器在供用户选择内容片段时所打开的路径，选择限制在这个目录和子目录中 | 否 |

>[!NOTE]
>
>通用编辑器[根据模型验证内容片段字段](/help/assets/content-fragments/content-fragments-models.md#validation)，允许您强制执行数据完整性规则，例如正则表达式模式和唯一性约束。
>
>这可确保您的内容在发布之前满足特定的业务要求。

>[!BEGINTABS]

>[!TAB 示例 1]

```json
[
  {
    "id": "aem-content-fragment",
    "fields": [
      {
        "component": "aem-content-fragment",
        "name": "picker",
        "label": "Content Fragment Picker",
        "valueType": "string",
        "variationName": "contentFragmentVariation",
        "validation": {
            "rootPath": "/content/refresh"
        }
      }
    ]
  }
]
```

>[!TAB 屏幕快照]

![内容片段选取器的屏幕快照](assets/component-types/aem-content-fragment.png)

>[!ENDTABS]

#### 日期时间 {#date-time}

日期时间组件类型允许指定一个日期、时间或两者的组合。它提供了额外配置。

| 配置 | 值类型 | 描述 | 必需 |
|---|---|---|---|
| `displayFormat` | `string` | 日期字符串的显示格式 | 是 |
| `valueFormat` | `string` | 日期字符串的存储格式 | 是 |

它也提供了一种额外的验证类型。

| 验证类型 | 值类型 | 描述 | 必需 |
|---|---|---|---|
| `customErrorMsg` | `string` | 在不满足 `valueFormat` 的情况下显示的消息 | 否 |

>[!BEGINTABS]

>[!TAB 示例 1]

```json
{
  "id": "date-time",
  "fields": [
    {
      "component": "date-time",
      "label": "Date & Time",
      "name": "date",
      "valueType": "date"
    }
  ]
}
```

>[!TAB 示例 2]

```json
{
  "id": "another-date-time",
  "fields": [
    {
      "component": "date-time",
       "valueType": "date-time",
      "name": "field1",
      "label": "Date Time",
      "description": "This is a date time field that stores both date and time.",
      "required": true,
      "placeholder": "YYYY-MM-DD HH:mm:ss",
      "displayFormat": null,
      "valueFormat": null,
      "validation": {
        "customErrorMsg": "Marty! You have to come back with me!"
      }
    },
    {
      "component": "date-time",
      "valueType": "date",
      "name": "field2",
      "label": "Another Date Time",
      "description": "This is another date time field that only stores the date.",
      "required": true,
      "placeholder": "YYYY-MM-DD",
      "displayFormat": null,
      "valueFormat": null,
      "validation": {
        "customErrorMsg": "Back to the future!"
      }
    },
    {
      "component": "date-time",
      "valueType": "time",
      "name": "field3",
      "label": "Yet Another Date Time",
      "description": "This is another date time field that only stores the time.",
      "required": true,
      "placeholder": "HH:mm:ss",
      "displayFormat": null,
      "valueFormat": null,
      "validation": {
        "customErrorMsg": "Great Scott!"
      }
    }
  ]
}
```

>[!TAB 屏幕快照]

![日期时间组件类型的屏幕快照](assets/component-types/date-time.png)

>[!ENDTABS]

#### 体验片段 {#experience-fragment}

体验片段选取器可用于选择[体验片段](/help/sites-cloud/authoring/fragments/experience-fragments.md)及其变体（必需时）。它提供了一种额外的配置。

| 配置 | 值类型 | 描述 | 必需 |
|---|---|---|---|
| `variationName` | `string` | 用于存储所选变体的变量名称。如果未定义，就不显示变体选取器 | 否 |

它也提供了一种额外的验证类型。

| 验证类型 | 值类型 | 描述 | 必需 |
|---|---|---|---|
| `rootPath` | `string` | 内容选取器在供用户选择体验片段时所打开的路径，选择限制在这个目录和子目录中 | 否 |

>[!BEGINTABS]

>[!TAB 示例 1]

```json
[
  {
    "id": "experience-fragment",
    "fields": [
      {
        "component": "aem-experience-fragment",
        "valueType": "string",
        "name": "experience-fragment",
        "label": "experience-fragment",
        "variationName": "experienceFragmentVariation",
        "validation": {
            "rootPath": "/content/refresh"
        }
      }
    ]
  }
]
```

>[!TAB 屏幕快照]

![体验片段选取器的屏幕快照](assets/component-types/aem-experience-fragment.png)

>[!ENDTABS]


#### 多选 {#multiselect}

多选组件类型显示为下拉菜单中多个可选择项，包括对可选元素分组的功能。

>[!BEGINTABS]

>[!TAB 示例 1]

```json
{
  "id": "multiselect",
  "fields": [
    {
      "component": "multiselect",
      "name": "multiselect",
      "label": "Multi Select",
      "valueType": "string",
      "options": [
        { "name": "Option 1", "value": "option1" },
        { "name": "Option 2", "value": "option2" }
      ]
    }
  ]
}
```

>[!TAB 示例 2]

```json
{
  "id": "multiselect-grouped",
  "fields": [
    {
      "component": "multiselect",
      "name": "property",
      "label": "Multiselect field",
      "valueType": "string",
      "required": true,
      "maxSize": 2,
      "options": [
        {
          "name": "Theme",
          "children": [
            { "name": "Light", "value": "light" },
            { "name": "Dark",  "value": "dark" }
          ]
        },
        {
          "name": "Type",
          "children": [
            { "name": "Alpha", "value": "alpha" },
            { "name": "Beta", "value": "beta" },
            { "name": "Gamma", "value": "gamma" }
          ]
        }
      ]
    }
  ]
}
```

>[!TAB 屏幕快照]

![多选组件类型的屏幕快照](assets/component-types/multiselect.png)
![带分组的多选组件类型的屏幕快照](assets/component-types/multiselect-group.png)

>[!ENDTABS]

#### 数字 {#number}

数字组件类型允许输入数字。它提供了额外的验证类型。

| 验证类型 | 值类型 | 描述 | 必需 |
|---|---|---|---|
| `numberMin` | `number` | 允许的最小数字 | 否 |
| `numberMax` | `number` | 允许的最大数字 | 否 |
| `customErrorMsg` | `string` | 在不满足 `numberMin` 或 `numberMax` 的情况下显示的消息 | 否 |

>[!BEGINTABS]

>[!TAB 示例 1]

```json
{
  "id": "number",
  "fields": [
    {
      "component": "number",
      "name": "number",
      "label": "Number",
      "valueType": "number",
      "value": 0
    }
  ]
}
```

>[!TAB 示例 2]

```json
{
  "id": "another-number",
  "fields": [
   {
      "component": "number",
      "valueType": "number",
      "name": "field1",
      "label": "Number Field",
      "description": "This is a number field.",
      "required": true,
      "placeholder": null,
      "validation": {
        "numberMin": 0,
        "numberMax": 88,
        "customErrorMsg": "You also need 1.21 gigawatts."
      }
    }
  ]
}
```

>[!TAB 屏幕快照]

![数字组件类型的屏幕快照](assets/component-types/number.png)

>[!ENDTABS]

#### 单选按钮组 {#radio-group}

单选按钮组组件类型允许从多个选项中进行互斥选择，显示为与复选框组类似的一个组。

>[!BEGINTABS]

>[!TAB 示例]

```json
{
  "id": "radio-group",
  "fields": [
    {
      "component": "radio-group",
      "label": "Radio Group",
      "name": "radio",
      "valueType": "string",
      "options": [
        { "name": "Option 1", "value": "option1" },
        { "name": "Option 2", "value": "option2" }
      ]
    }
  ]
}
```

>[!TAB 屏幕快照]

![单选按钮组组件类型的屏幕快照](assets/component-types/radio.png)

>[!ENDTABS]

#### 引用 {#reference}

引用组件类型会启用 AEM 资产选取器，用于选择要引用的任何 AEM 资产。与可以选择任何 AEM 资源的[AEM 内容组件](#aem-content)不同，引用组件只能引用资产。它提供了一种额外的验证类型。

引用组件类型允许从当前对象引用另一个数据对象。

>[!BEGINTABS]

>[!TAB 示例]

```json
{
  "id": "reference",
  "fields": [
    {
      "component": "reference",
      "label": "Reference",
      "name": "reference",
      "valueType": "string"
    }
  ]
}
```

>[!TAB 屏幕快照]

![引用组件类型的屏幕快照](assets/component-types/reference.png)

>[!ENDTABS]

#### 富文本 {#rich-text}

富文本允许多行的富文本输入。

>[!BEGINTABS]

>[!TAB 示例 1]

```json
{
  "id": "richtext",
  "fields": [
    {
      "component": "richtext",
      "name": "rte",
      "label": "Rich Text",
      "valueType": "string"
    }
  ]
}
```

>[!TAB 屏幕快照]

![文本区域组件类型的屏幕快照](assets/component-types/richtext.png)

>[!ENDTABS]

#### 选择 {#select}

选择组件类型允许从下拉菜单中的一个预定义选项列表中选择一个选项。

>[!BEGINTABS]

>[!TAB 示例]

```json
{
  "id": "select",
  "fields": [
    {
      "component": "select",
      "label": "Select",
      "name": "select",
      "valueType": "string",
      "options": [
        { "name": "Option 1", "value": "option1" },
        { "name": "Option 2", "value": "option2" }
      ]
    }
  ]
}
```

>[!TAB 屏幕快照]

![选择组件类型的屏幕快照](assets/component-types/select.png)

>[!ENDTABS]

#### 选项卡 {#tab}

选项卡组件类型允许您将其他输入字段一起分组放在多个选项卡上，以增强作者的布局组织。

`tab` 定义可以被认为是 `fields` 数组中的一种分隔符。`tab` 之后发生的一切都将被放在这个选项卡上，直到出现新的 `tab` 后，接下来的各项将被放在这个新选项卡上。

如果您想让一些项显示在所有选项卡上方，就必须在出现任何选项卡之前定义它们。

>[!BEGINTABS]

>[!TAB 示例]

```json
{
  "id": "tab",
  "fields": [
    {
      "component": "tab",
      "label": "Tab 1",
      "name": "tab1"
    },
    {
      "component": "text-input",
      "label": "Text 1",
      "name": "text1",
      "valueType": "string"
    },
    {
      "component": "tab",
      "label": "Tab 2",
      "name": "tab2"
    },
    {
      "component": "text-input",
      "label": "Text 2",
      "name": "text2",
      "valueType": "string"
    }
  ]
}
```

>[!TAB 屏幕快照]

![选项卡组件类型的屏幕快照](assets/component-types/tab.png)

>[!ENDTABS]

#### 文本 {#text}

文本允许输入单行文字。它包括额外的验证类型。

| 验证类型 | 值类型 | 描述 | 必需 |
|---|---|---|---|
| `minLength` | `number` | 允许的最少字符数 | 否 |
| `maxLength` | `number` | 允许的最多字符数 | 否 |
| `regExp` | `string` | 输入文本必须与之匹配的正则表达式 | 否 |
| `customErrorMsg` | `string` | 在违反了 `minLength`、`maxLength` 和/或 `regExp` 的情况下显示的消息 | 否 |

>[!BEGINTABS]

>[!TAB 示例 1]

```json
{
  "id": "simpletext",
  "fields": [
    {
      "component": "text",
      "name": "text",
      "label": "Simple Text",
      "valueType": "string"
    }
  ]
}
```

>[!TAB 示例 2]

```json
{
  "id": "another simpletext",
  "fields": [
    {
      "component": "text",
      "name": "text",
      "label": "Simple Text",
      "valueType": "string",
      "valueFormat": "regexp",
      "description": "This is a text input with validation.",
      "required": true,
      "validation": {
        "minLength": 1955,
        "maxLength": 1985,
        "regExp": "^foo:.*",
        "customErrorMsg": "Why don't you make like a tree and get outta here?"
      }
    }
  ]
}
```

>[!TAB 屏幕快照]

![文本组件类型的屏幕快照](assets/component-types/simpletext.png)

>[!ENDTABS]
