---
title: 自定义通用编辑器创作体验
description: 了解不同的扩展点和其他功能，这些功能允许您自定义通用编辑器的UI以支持内容作者的需求。
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
source-git-commit: 11a244b7dd4810fbfec92b3effc362102e7322dc
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 0%

---


# 自定义通用编辑器创作体验 {#customizing-ue}

了解不同的扩展点和其他功能，这些功能允许您自定义通用编辑器的创作体验，以支持内容作者的需求。

## 禁用发布 {#disable-publish}

某些创作工作流在发布之前需要审查内容。 在这种情况下，任何作者都不应可以使用发布选项。

此 **Publish** 因此，可以通过添加以下元数据在应用程序中完全禁止显示按钮。

```html
<meta name="urn:adobe:aue:config:disable" content="publish"/>
```

## 筛选组件 {#filtering-components}

使用通用编辑器时，您可以限制每个容器组件允许的组件。 为此，必须引入额外的脚本标记，该标记指向过滤器定义。

```html
<script type="application/vnd.adobe.aue.filter+json" src="/static/filter-definition.json"></script>
```

过滤器定义可能如下所示，这将限制容器仅允许添加文本和图像。

```json
[
  {
    "id": "container-filter",
     "components": ["text", "image"]
   }
]
```

然后，您可以通过添加属性来引用容器组件中的过滤器定义 `data-aue-filter`，传递您之前定义的过滤器的ID。

```html
data-aue-filter="container-filter"
```

设置 `components` 过滤器定义中的属性 `null` 允许所有组件，就像没有过滤器一样。

```json
[
  {
    "id": "another-container-filter",
     "components": null
   }
]
```

## 有条件地显示和隐藏属性边栏中的组件 {#conditionally-hide}

尽管一个或多个组件通常可供您的作者使用，但在某些情况下可能没有意义。 在这种情况下，您可以通过添加 `condition` 归因于 [组件模型的字段。](/help/implementing/universal-editor/field-types.md#fields)

可以使用定义条件 [JsonLogic架构。](https://jsonlogic.com/) 如果条件为true，则会显示字段。 如果条件为false，则字段将隐藏。

### 示例模型 {#sample-model}

```json
 {
    "id": "conditionally-revealed-component",
    "fields": [
      {
        "component": "boolean",
        "label": "Shall the text field be revealed?",
        "name": "reveal",
        "valueType": "boolean"
      },
      {
        "component": "text-input",
        "label": "Hidden text field",
        "name": "hidden-text",
        "valueType": "string",
        "condition": { "===": [{"var" : "reveal"}, true] }
      }
    ]
 }
```

#### 条件False {#false}

![隐藏的文本字段](assets/hidden.png)

#### 条件True {#true}

![显示的文本字段](assets/shown.png)

