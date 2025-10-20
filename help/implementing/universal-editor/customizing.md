---
title: 自定义通用编辑器
description: 了解如何通过不同的选项自定义通用编辑器，以满足内容作者的需求。
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
feature: Developing
role: Admin, Architect, Developer
source-git-commit: b32e9b83a761e4f178cddb82b83b31a95a8978f6
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 69%

---


# 自定义通用编辑器 {#customizing}

了解如何通过不同的选项自定义通用编辑器，以满足内容作者的需求。

>[!TIP]
>
>通用编辑器还提供了许多[扩展点](/help/implementing/universal-editor/extending.md)，允许您扩展其功能，以满足您的项目需求。

## 使用Meta配置标记 {#meta-tags}

某些创作工作流可能要求使用通用编辑器的某些功能，而不是其他功能。 为了支持这些不同的情况，meta标记可用于配置或禁用编辑器的某些功能或按钮。

在页面的`<head>`部分使用此标记可禁用一项或多项功能：

```html
<meta name="urn:adobe:aue:config:disable" content="..." />
```

如果要禁用多个功能，请提供以逗号分隔的值列表。

以下是`content`支持的值，即可以使用meta标记禁用的功能。

| 内容值 | 描述 |
|---|---|
| `publish` | 禁用[发布按钮](/help/sites-cloud/authoring/universal-editor/navigation.md#publish) |
| `publish-live` | 禁用实时[发布](/help/sites-cloud/authoring/universal-editor/publishing.md) |
| `publish-preview` | 禁用预览发布（如果[预览服务](/help/sites-cloud/authoring/sites-console/previewing-content.md)可用） |
| `unpublish` | 禁用[取消发布按钮](/help/sites-cloud/authoring/universal-editor/publishing.md#unpublishing-content) |
| `copy` | 禁用[复制和粘贴按钮](/help/sites-cloud/authoring/universal-editor/authoring.md#copy-paste) |
| `duplicate` | 禁用[重复按钮](/help/sites-cloud/authoring/universal-editor/navigation.md#duplicate) |
| `header-open-page` | 禁用[打开页面按钮](/help/sites-cloud/authoring/universal-editor/navigation.md#open-page) |

## 更改您的端点 {#custom-endpoint}

如果您不想使用 Adobe 托管的通用编辑器服务，而是使用您自己的托管版本，您可以在元标记中设置这一点。详细信息请参阅文档[在 AEM 中使用通用编辑器快速入门](/help/implementing/universal-editor/getting-started.md##configuration-settings)。

## 筛选组件 {#filtering-components}

您可以使用组件过滤器限制通用编辑器中每个容器允许使用的组件。有关更多信息，请参阅文档[筛选组件](/help/implementing/universal-editor/filtering.md)。

## 在属性面板中有条件地显示和隐藏组件 {#conditionally-hide}

通常情况下会有一个或多个组件可供作者使用，但在某些情况下可能会不合理。在这种情况下，您可以将一个 `condition` 属性添加到[组件模型的字段中](/help/implementing/universal-editor/field-types.md#fields)，隐藏属性面板中的组件。

可以使用 [JsonLogic 架构](https://jsonlogic.com/)定义条件。如果条件为真，就显示该字段。如果条件为假，就隐藏该字段。

>[!BEGINTABS]

>[!TAB 模型示例]

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

>[!TAB 条件为假]

![隐藏文本字段](assets/hidden.png)

>[!TAB 条件为真]

![显示文本字段](assets/shown.png)

>[!ENDTABS]

## 自定义预览 URL {#custom-preview-urls}

您可以通过 `urn:adobe:aue:config:preview` 元配置指定自定义预览 URL，点击[编辑器右上角工具栏](/help/sites-cloud/authoring/universal-editor/navigation.md#universal-editor-toolbar)中的&#x200B;**打开页面**&#x200B;按钮即可打开这个 URL。

为此，只需将所需的预览 URL 包含在已适配的应用程序的元标记中，如下例所示。

```html
<meta name="urn:adobe:aue:config:preview" content="https://wknd.site"/>
```
