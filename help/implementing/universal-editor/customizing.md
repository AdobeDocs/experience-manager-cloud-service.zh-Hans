---
title: 自定义 Universal Editor
description: 了解用于自定义通用编辑器的不同选项，以支持内容作者的需求。
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 6976f0c9926fb4cb64b0b2d7f8d2daf004c6b936
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 8%

---


# 自定义 Universal Editor {#customizing}

了解用于自定义通用编辑器的不同选项，以支持内容作者的需求。

>[!TIP]
>
>通用编辑器还提供了许多[扩展点，](/help/implementing/universal-editor/extending.md)允许您扩展其功能以满足您的项目需求。

## 禁用发布 {#disable-publish}

某些创作工作流在发布之前需要审查内容。 在这种情况下，任何作者都不应可以使用发布选项。

因此，可以通过添加以下元数据在应用程序中完全隐藏&#x200B;**发布**&#x200B;按钮。

```html
<meta name="urn:adobe:aue:config:disable" content="publish"/>
```

## 禁用发布以预览 {#publish-preview}

某些创作工作流可能会阻止发布到[预览服务](/help/sites-cloud/authoring/sites-console/previewing-content.md)（如果可用）。

因此，可以通过添加以下元数据在应用程序中完全禁止发布窗口中的&#x200B;**预览**&#x200B;选项。

```html
<meta name="urn:adobe:aue:config:disable" content="publish-preview"/>
```

## 禁用打开页面 {#open-page}

通过添加以下元数据，可以在应用程序中完全隐藏&#x200B;**打开页面**&#x200B;按钮。

```html
<meta name="urn:adobe:aue:config:disable" content="header-open-page" />
```

## 筛选组件 {#filtering-components}

您可以使用组件过滤器在通用编辑器中限制每个容器允许的组件。 有关详细信息，请参阅文档[筛选组件](/help/implementing/universal-editor/filtering.md)。

## 有条件地显示和隐藏属性面板中的组件 {#conditionally-hide}

尽管一个或多个组件通常可供您的作者使用，但在某些情况下可能没有意义。 在这种情况下，可以通过向组件模型[&#128279;](/help/implementing/universal-editor/field-types.md#fields)的字段添加`condition`属性来隐藏属性面板中的组件。

可以使用[JsonLogic架构](https://jsonlogic.com/)定义条件。 如果条件为true，则会显示字段。 如果条件为false，则字段将隐藏。

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

## 自定义预览URL {#custom-preview-urls}

您可以通过`urn:adobe:aue:config:preview`元配置指定自定义预览URL，单击[编辑器右上角工具栏](/help/sites-cloud/authoring/universal-editor/navigation.md#universal-editor-toolbar)中的&#x200B;**打开页面**&#x200B;按钮时，将打开该配置。

这对于具有特定预览要求的应用程序特别有用，例如那些[使用具有所见即所得创作的 Edge Delivery Services 的应用程序](/help/edge/wysiwyg-authoring/authoring.md)。

要实现此目的，只需将所需的预览URL包含在所检测应用程序的meta标记中，如下例所示。

```html
<meta name="urn:adobe:aue:config:preview" content="https://wknd.site"/>
```
