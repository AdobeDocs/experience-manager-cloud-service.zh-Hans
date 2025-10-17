---
title: 自定义通用编辑器
description: 了解如何通过不同的选项自定义通用编辑器，以满足内容作者的需求。
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
feature: Developing
role: Admin, Architect, Developer
source-git-commit: a72b4b7921a1a379bcd089682c02b0519fe3af8a
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 85%

---


# 自定义通用编辑器 {#customizing}

了解如何通过不同的选项自定义通用编辑器，以满足内容作者的需求。

>[!TIP]
>
>通用编辑器还提供了许多[扩展点](/help/implementing/universal-editor/extending.md)，允许您扩展其功能，以满足您的项目需求。

## 禁用发布 {#disable-publish}

某些创作工作流程要求在内容发布之前进行审阅。在这种情况下，任何作者都不应有发布选项。

因此，通过添加以下元数据可以在应用程序中完全抑制&#x200B;**发布**&#x200B;按钮。

```html
<meta name="urn:adobe:aue:config:disable" content="publish"/>
```

## 禁用发布到预览 {#publish-preview}

某些创作工作流程可能会阻止发布到[预览服务](/help/sites-cloud/authoring/sites-console/previewing-content.md)（如果可用）。

因此，通过添加以下元数据可以在应用程序中完全抑制发布窗口中的&#x200B;**预览**&#x200B;选项。

```html
<meta name="urn:adobe:aue:config:disable" content="publish-preview"/>
```

## 禁用发布以使其上线 {#publish-live}

某些创作工作流可能会阻止将内容发布到实时服务。

因此，可以通过添加以下元数据在应用程序中完全禁止发布窗口中的&#x200B;**Live**&#x200B;选项。

```html
<meta name="urn:adobe:aue:config:disable" content="publish-live"/>
```

## 禁用取消发布 {#unpublish}

某些创作工作流在取消发布内容之前需要审批流程。 在这种情况下，任何作者都不应可以使用取消发布选项。

因此，可以通过添加以下元数据在应用程序中完全隐藏&#x200B;**取消发布**&#x200B;按钮。

```html
<meta name="urn:adobe:aue:config:disable" content="unpublish"/>
```

## 禁用打开页面 {#open-page}

通过添加以下元数据可以在应用程序中完全抑制&#x200B;**打开页面**&#x200B;按钮。

```html
<meta name="urn:adobe:aue:config:disable" content="header-open-page" />
```

## 禁用重复按钮 {#duplicate-button}

某些创作工作流程可能需要限制内容作者复制组件的能力。您可以通过添加以下元数据禁用[重复图标](/help/sites-cloud/authoring/universal-editor/navigation.md#duplicate)。

```html
<meta name="urn:adobe:aue:config:disable" content="duplicate"/>
```

## 禁用复制和粘贴 {#copy-paste}

某些创作工作流可能需要限制内容作者的组件复制和粘贴功能。您可以通过添加以下元数据禁用[复制和粘贴图标](/help/sites-cloud/authoring/universal-editor/authoring.md#copy-paste)的功能。

```html
<meta name="urn:adobe:aue:config:disable" content="copy"/>
```

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
