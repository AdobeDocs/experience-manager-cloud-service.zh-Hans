---
title: 使用 ContextHub 数据预览页面
description: ContextHub 工具栏显示 ContextHub 存储区中的数据，并允许您更改存储区数据，该工具栏可用于预览内容
exl-id: 9c0536c5-900e-4814-9e31-f9fee5adc17c
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 89%

---

# 使用 ContextHub 数据预览页面  {#previewing-pages-using-contexthub-data}

ContextHub 工具栏显示 ContextHub 存储区中的数据，并允许您更改存储区数据。ContextHub 工具栏可用于预览由 ContextHub 存储区中的数据决定的内容。

该工具栏由一系列包含一个或多个 UI 模块的 UI 模式组成。

* UI 模式是显示在工具栏左侧的图标。当您单击或点按某个图标时，工具栏会显示该模式包含的 UI 模块。
* UI 模块显示一个或多个 ContextHub 存储区中的数据。某些 UI 模块还允许您处理存储区数据。

ContextHub 安装了多个 UI 模式和 UI 模块。您的管理员可能已[配置 ContextHub](/help/implementing/developing/personalization/configuring-contexthub.md)，使其显示不同的内容。

## 显示 ContextHub 工具栏 {#revealing-the-contexthub-toolbar}

ContextHub 工具栏在“预览”模式下可用。该工具栏仅在创作实例中且管理员已将其启用后才可用。

![ContextHub工具栏](/help/sites-cloud/authoring/assets/contexthub-toolbar.png)

1. 在打开页面以进行编辑时，在工具栏上单击或点按“预览”。

   ![“预览”按钮](/help/sites-cloud/authoring/assets/contexthub-preview-button.png)

1. 要显示工具栏，请单击或点按 ContextHub 图标。

   ![ContextHub按钮](/help/sites-cloud/authoring/assets/contexthub-button.png)

## UI 模块功能 {#ui-module-features}

每个 UI 模块都提供了不同的功能集，但以下类型的功能是通用的。由于 UI 模块是可扩展的，因此您的开发人员可以根据需要实现其他功能。

### 工具栏内容 {#toolbar-content}

UI 模块可以在工具栏中显示一个或多个 ContextHub 存储区中的数据。UI模块使用图标和标题来标识自己。

![ContextHub角色](/help/sites-cloud/authoring/assets/contexthub-persona-button.png)

### 弹出窗口内容 {#popup-content}

某些UI模块在单击或点按时会显示一个弹出式叠加。 通常，弹出窗口包含的信息比工具栏上显示的信息要多。

![ContextHub配置文件信息](/help/sites-cloud/authoring/assets/contexthub-profile.png)

### 弹出窗口表单 {#popup-forms}

模块的弹出覆盖窗口可以包含表单元素，使您能够更改 ContextHub 存储区中的数据。如果页面内容由存储区数据决定，您可以使用表单并观察页面内容的更改。

### 全屏模式 {#fullscreen-mode}

弹出覆盖窗口可以包含一个图标，单击或点按该图标会展开弹出窗口内容以覆盖整个浏览器窗口或屏幕。

![全屏按钮](/help/sites-cloud/authoring/assets/contexthub-fullscreen.png)
