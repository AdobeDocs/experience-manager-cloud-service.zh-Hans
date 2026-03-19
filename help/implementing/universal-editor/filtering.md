---
title: 过滤器
description: 了解如何定义过滤器以限制编辑器中可用的选项，例如可用组件、RTE选项和资源选择。
feature: Developing
role: Admin, Developer
exl-id: eeae8d7c-c563-4d9b-8c54-1098a4e98c18
source-git-commit: 8d9d162ec5bba99afb1ae86252a49a9880be4e68
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 15%

---


# 过滤器 {#filters}

了解如何定义过滤器以限制编辑器中可用的选项，例如可用组件、RTE选项和资源选择。

## 配置过滤器 {#configuring-filters}

使用通用编辑器时，您可以通过定义过滤器来限制特定功能允许的选项。 过滤器是适用于特定上下文的项目或操作列表。 例如，您可以筛选可插入容器的组件，可以[筛选RTE中可用的选项，](/help/implementing/universal-editor/configure-rte.md)以及[筛选资产选择器中可用的资产](/help/implementing/universal-editor/configure-assets-selector.md)。

所有筛选器的定义都必须类似。

1. [添加脚本标记以指向筛选器定义](#add-tag)
1. [定义过滤器](#define-filter)
1. [引用过滤器](#reference-filter)

让我们以每个容器组件为单位筛选组件为例。

## 引用筛选器定义 {#add-tag}

首先引入额外的脚本标记，该标记指向过滤器定义。

在我们的示例中，筛选每个容器允许的组件，标记可能如下所示。

```html
<script type="application/vnd.adobe.aue.filter+json" src="/static/filter-definition.json"></script>
```

## 定义过滤器 {#define-filter}

过滤器定义包含的JSON具有过滤器和过滤条件唯一的ID。

例如，我们用于筛选每个容器允许的组件的示例，它可能如下所示，这将限制容器仅允许添加文本和图像。

```json
[
  {
    "id": "container-filter",
    "components": ["text", "image"]
   }
]
```

如果将过滤器定义中的 `components` 属性设置为 `null`，就会允许使用所有组件，就好像没有过滤器。

```json
[
  {
    "id": "another-container-filter",
     "components": null
   }
]
```

## 引用过滤器 {#reference-filter}

要使用过滤器，必须引用过滤器定义。 您可以通过以下方式来实现：

* 通过添加属性`data-aue-filter`并传递筛选器的ID，引用容器组件中的筛选器。

  ```html
  data-aue-filter="container-filter"
  ```

* 引用来自[组件定义的筛选器，](/help/implementing/universal-editor/component-definition.md)传递筛选器的ID。

  ```json
  {
     "title":"My Container",
     "id":"my-container",
     "model": "my-model",
     "filter": "container-filter",
     ...
  }
  ```

## 其他资源 {#additional-resources}

请参阅以下文档，了解通用编辑器可用的其他自定义和扩展选项：

* [为通用编辑器配置RTE](/help/implementing/universal-editor/configure-rte.md)
* [为Assets选择器配置过滤器](/help/implementing/universal-editor/configure-assets-selector.md)
* [自定义通用编辑器](/help/implementing/universal-editor/customizing.md)
* [扩展通用编辑器](/help/implementing/universal-editor/extending.md)
