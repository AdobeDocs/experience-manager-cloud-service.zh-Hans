---
title: 自定义和扩展通用编辑器
description: 了解不同的扩展点和其他功能，这些功能允许您自定义通用编辑器的UI以支持内容作者的需求。
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 1%

---


# 自定义和扩展通用编辑器 {#customizing-extending}

了解不同的扩展点和其他功能，这些功能允许您自定义通用编辑器的创作体验，以支持内容作者的需求。

## 概述 {#overview}

通用编辑器允许您根据项目需求进行两种类型的适应。

* [自定义通用编辑器](#customizing)  — 可以通过多个自定义配置调整通用编辑器的标准功能。
* [扩展通用编辑器UI](#extending)  — 还可以使用App Builder扩展通用编辑器的UI，以满足您的项目需求。

以下各节将详细介绍这两种类型。

## 自定义 Universal Editor {#customizing}

通用编辑器提供了多个内置选项以自定义其功能。

### 禁用发布 {#disable-publish}

某些创作工作流在发布之前需要审查内容。 在这种情况下，任何作者都不应可以使用发布选项。

此 **Publish** 因此，可以通过添加以下元数据在应用程序中完全禁止显示按钮。

```html
<meta name="urn:adobe:aue:config:disable" content="publish"/>
```

### 筛选组件 {#filtering-components}

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

### 有条件地显示和隐藏属性边栏中的组件 {#conditionally-hide}

尽管一个或多个组件通常可供您的作者使用，但在某些情况下可能没有意义。 在这种情况下，您可以通过添加 `condition` 归因于 [组件模型的字段。](/help/implementing/universal-editor/field-types.md#fields)

可以使用定义条件 [JsonLogic架构。](https://jsonlogic.com/) 如果条件为true，则会显示字段。 如果条件为false，则字段将隐藏。

>[!BEGINTABS]

>[!TAB 示例模型]

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

>[!TAB 条件False]

![隐藏的文本字段](assets/hidden.png)

>[!TAB 条件True]

![显示的文本字段](assets/shown.png)

>[!ENDTABS]

## 扩展通用编辑器UI {#extending}

作为Adobe Experience Cloud服务，可以使用应用程序生成器和Experience Manager扩展通用编辑器的UI。

UI扩展是使用AdobeApp Builder构建的JavaScript应用程序，可以嵌入到在Adobe Experience Cloud统一外壳下运行的UI应用程序（例如通用编辑器）中。 您可以将自己的按钮和操作添加到标题菜单和属性边栏，并为通用编辑器创建自己的事件。

如果您想探索这些可能性，请参阅以下资源：

1. [UI可扩展性](https://developer.adobe.com/uix/docs/)  — 这是UI扩展的开发人员文档。
1. [UI可扩展性指南](https://developer.adobe.com/uix/docs/guides/)  — 关于如何开发您自己的扩展的分步说明
1. [通用编辑器扩展点](https://developer.adobe.com/uix/docs/services/aem-universal-editor/)  — 特定于通用编辑器的扩展点文档

>[!TIP]
>
>如果您希望通过示例学习，请参见 [AEM用户界面可扩展性教程。](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/developing/extensibility/ui/overview) 虽然它侧重于扩展内容片段控制台，但在通用编辑器中实施UI扩展的概念是相同的。

[使用AEM Sites中的Extension Manager，](https://developer.adobe.com/uix/docs/extension-manager/) 您可以基于每个实例启用或禁用扩展，访问Adobe的第一方扩展（包括通用编辑器的第一方扩展）等等。
