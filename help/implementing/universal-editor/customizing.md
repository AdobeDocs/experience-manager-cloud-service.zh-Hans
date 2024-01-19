---
title: 自定义 UI
description: 了解不同的扩展点，通过这些扩展点可自定义通用编辑器的UI以支持内容作者的需求。
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
source-git-commit: 7ef3efa6e074778b7b3e3a8159056200b2663b30
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 6%

---


# 自定义 UI  {#customizing-ui}

了解不同的扩展点，通过这些扩展点可自定义通用编辑器的UI以支持内容作者的需求。

## 禁用发布 {#disable-publish}

某些创作工作流在发布之前需要审查内容。 在这种情况下，任何作者都不应可以使用发布选项。

此 **Publish** 因此，可以通过添加以下元数据在应用程序中完全禁止显示按钮。

```html
<meta name="urn:adobe:aue:config:disable" content="publish"/>
```
