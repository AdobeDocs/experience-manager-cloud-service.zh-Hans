---
title: 自定义 UI
description: 了解不同的扩展点，通过这些扩展点可自定义通用编辑器的UI以支持内容作者的需求。
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
source-git-commit: 1bc65e65e6ce074a050e21137ce538b5c086665f
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 3%

---


# 自定义 UI  {#customizing-ui}

了解不同的扩展点，通过这些扩展点可自定义通用编辑器的UI以支持内容作者的需求。

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
