---
title: 自定义UI
description: 了解不同的扩展点，通过这些扩展点可自定义通用编辑器的UI以支持内容作者的需求。
source-git-commit: 65893c0c0dee37bed8ecfbb06a12e7c093c4397c
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 0%

---


# 自定义UI {#customizing-ui}

了解不同的扩展点，通过这些扩展点可自定义通用编辑器的UI以支持内容作者的需求。

## 禁用发布 {#disable-publish}

某些创作工作流在发布之前需要审查内容。 在这种情况下，任何作者都不应可以使用发布选项。

此 **Publish** 因此，可以通过添加以下元数据在应用程序中完全禁止显示按钮。

```html
<meta name="urn:adobe:aue:config:disable" content="publish"/>
```
