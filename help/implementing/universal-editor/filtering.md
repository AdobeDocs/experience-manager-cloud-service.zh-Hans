---
title: 筛选组件
description: 了解如何使用组件过滤器限制通用编辑器中每个容器允许使用的组件。
feature: Developing
role: Admin, Developer
exl-id: eeae8d7c-c563-4d9b-8c54-1098a4e98c18
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 100%

---

# 筛选组件 {#filtering-components}

了解如何使用组件过滤器限制通用编辑器中每个容器允许使用的组件。

## 过滤器 {#filters}

使用通用编辑器时，您可以限制每个容器组件允许使用的组件。为此，您必须额外引入一个指向过滤器定义的脚本标记。

```html
<script type="application/vnd.adobe.aue.filter+json" src="/static/filter-definition.json"></script>
```

过滤器定义可能如下所示，它会限制容器只允许添加文本和图像。

```json
[
  {
    "id": "container-filter",
     "components": ["text", "image"]
   }
]
```

然后，您可以通过添加属性 `data-aue-filter` 从容器组件引用过滤器定义，传递您之前已定义的过滤器的 ID。

```html
data-aue-filter="container-filter"
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

>[!TIP]
>
>请参阅以下文档，了解通用编辑器可用的其他自定义和扩展选项：
>
>* [自定义通用编辑器](/help/implementing/universal-editor/customizing.md)
>* [扩展通用编辑器](/help/implementing/universal-editor/extending.md)
