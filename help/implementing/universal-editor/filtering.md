---
title: 筛选组件
description: 了解如何使用组件过滤器在通用编辑器中限制每个容器允许的组件。
feature: Developing
role: Admin, Architect, Developer
exl-id: eeae8d7c-c563-4d9b-8c54-1098a4e98c18
source-git-commit: cdad4954b13f5582bebfd604220da90529231ccd
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 3%

---

# 筛选组件 {#filtering-components}

了解如何使用组件过滤器在通用编辑器中限制每个容器允许的组件。

## 过滤器 {#filters}

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

然后，您可以通过添加属性`data-aue-filter`，传递您之前定义的筛选器的ID，从容器组件中引用筛选器定义。

```html
data-aue-filter="container-filter"
```

将筛选器定义中的`components`属性设置为`null`将允许所有组件，就像没有筛选器一样。

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
>在文档中了解对通用编辑器可用的其他自定义和扩展选项：
>
>* [自定义通用编辑器](/help/implementing/universal-editor/customizing.md)
>* [扩展通用编辑器](/help/implementing/universal-editor/extending.md)
