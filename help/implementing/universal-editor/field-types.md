---
title: 字段类型
description: 通过有关如何检测您自己的应用程序的示例，了解通用编辑器可以在组件边栏中编辑的不同类型的字段。
exl-id: cb4567b8-ebec-477c-b7b9-53f25b533192
source-git-commit: 7ef3efa6e074778b7b3e3a8159056200b2663b30
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 7%

---


# 字段类型 {#field-types}

通过有关如何检测您自己的应用程序的示例，了解通用编辑器可以在组件边栏中编辑的不同类型的字段。

{{universal-editor-status}}

## 概述 {#overview}

在调整自己的应用程序以便与通用编辑器一起使用时，必须检测组件并定义它们可以在编辑器的组件边栏中处理的数据类型。

本文档概述了可用的字段类型以及示例配置。

>[!TIP]
>
>如果您不熟悉如何针对通用编辑器检测应用程序，请参阅文档 [面向AEM开发人员的通用编辑器概述。](/help/implementing/universal-editor/developer-overview.md)

## 布尔值 {#boolean}

布尔字段存储呈现为复选框的简单true/false值。

### 样本 {#sample-boolean}

```json
{
  "fields": [   
   {
      "component": "boolean",
      "valueType": "boolean",
      "name": "field1",
      "label": "Boolean Field",
      "description": "This is a boolean field.",
      "required": true,
      "placeholder": null,
      "validation": {
        "customErrorMsg": "This is an error."
      }
    }
  ]
}
```

## 复选框组 {#checkbox-group}

与布尔值类似，复选框组允许选择多个true/false项目。

### 样本 {#sample-checkbox-group}

```json
{
  "fields": [   
   {
      "component": "checkbox-group",
      "valueType": "string-array",
      "name": "field1",
      "label": "Checkbox Group",
      "description": "This is a checkbox group.",
      "required": true,
      "placeholder": null,
      "options": [
        { "name": "First option", "value": "one" },
        { "name": "Second option", "value": "two" },
        { "name": "Third option", "value": "three" }
      ]
    }
  ]
}
```

## 日期时间 {#date-time}

日期时间字段允许指定日期或时间或它们的组合。

### 样本 {#sample-date-time}

```json
{
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

## 数字 {#number}

数字字段允许输入数字。

### 样本 {#sample-number}

```json
{
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
        "numberMin": null,
        "numberMax": null,
        "customErrorMsg": "Please don't do that."
      }
    }
  ]
}
```

## 单选按钮组 {#radio-group}

单选按钮组允许从呈现为类似于复选框组的组的组的多个选项中进行互斥选择。

### 样本 {#sample-radio-group}

```json
{
  "fields": [   
   {
      "component": "radio-group",
      "valueType": "string",
      "name": "field1",
      "label": "Radio Group",
      "description": "This is a radio group.",
      "required": true,
      "placeholder": null,
      "options": [
        { "name": "Option One", "value": "one" },
        { "name": "Option Two", "value": "two" },
        { "name": "Option Three", "value": "three" }
      ]
    }
  ]
}
```

## 引用 {#reference}

引用允许将另一个数据对象指定为来自当前对象的引用。

## 选择 {#select}

选择允许在下拉菜单中选择一个或多个预定义选项。

### 样本 {#sample-select}

```json
{
  "fields": [   
   {
      "component": "select",
      "valueType": "string",
      "name": "field1",
      "label": "Select",
      "description": "This is a select.",
      "required": true,
      "placeholder": null,
      "options": [
        { "name": "Option One", "value": "one" },
        { "name": "Option Two", "value": "two" },
        { "name": "Option Three", "value": "three" }
      ],
      "emptyOption": true
    }
  ]
}
```

## 文本区域 {#text-area}

文本区域允许多行文本输入。

### 样本 {#sample-text-area}

```json
{
  "fields": [   
   {
      "component": "text-area",
      "valueType": "string",
      "name": "field1",
      "label": "Text Area",
      "description": "This is a text area.",
      "required": true,
      "multi": true,
      "placeholder": null,
      "mimeType": "text/x-markdown"
    }
  ]
}
```

## 文本输入 {#text-input}

文本输入允许单行文本输入。

### 样本 {#sample-text-input}

```json
{
  "fields": [   
   {
      "component": "text-input",
      "valueType": "string",
      "name": "field1",
      "label": "Text Input",
      "description": "This is a text input.",
      "required": true,
      "multi": true,
      "placeholder": null
    },
    {
      "component": "text-input",
      "valueType": "string",
      "name": "field2",
      "label": "Another Text Input",
      "description": "This is a text input with validation.",
      "required": true,
      "multi": true,
      "placeholder": null,
      "validation": {
        "minLength": 5,
        "maxLength": 10,
        "regExp": "^foo:.*",
        "customErrorMsg": "I'm sorry, Dave. I can't do that."
      }
    }
  ]
}
```

## 选项卡 {#tab}

使用选项卡，可将其他输入字段分组到多个选项卡上，以改善作者的布局组织。

A `tab` 可以将定义视为数组中的分隔符 `fields`. 之后的一切 `tab` 将被放置在该选项卡上，直到有新的 `tab` 之后，会将以下项目放置到新选项卡上。

如果希望项目出现在所有选项卡上方，则必须在任何选项卡之前定义它们。

### 样本 {#sample-tab}

```json
{
  "id": "title",
  "fields": [
    {
      "component": "tab",
      "label": "Tab",
      "name": "tab1"
    },
    {
      "component": "text-input",
      "name": "tab-response",
      "value": "",
      "placeholder": "Tab? I can't give you a tab unless you order something.",
      "label": "Lou",
      "valueType": "string"
    },
    {
      "component": "tab",
      "label": "Pepsi Free",
      "name": "tab2"
    },
    {
      "component": "text-input",
      "name": "pepsi-free-response",
      "value": "",
      "placeholder": "You want a Pepsi, pal, you're gonna pay for it.",
      "label": "Mr. Carruthers",
      "valueType": "string"
    },
    {
      "component": "select",
      "name": "without-sugar",
      "value": "coffee",
      "label": "Something without sugar",
      "valueType": "string",
      "options": [
        { "name": "Coffee", "value": "coffee" },
        { "name": "Hot Coffee", "value": "hot-coffee" },
        { "name": "Hotter Coffee", "value": "hotter-coffee" }
      ]
    }
  ]
}
```
