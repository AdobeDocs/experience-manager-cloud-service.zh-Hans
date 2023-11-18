---
title: 使用 ContextHub 数据预览页面
description: ContextHub 工具栏显示 ContextHub 存储区中的数据，并允许您更改存储区数据，该工具栏可用于预览内容
exl-id: 9c0536c5-900e-4814-9e31-f9fee5adc17c
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 31%

---

# 使用 ContextHub 数据预览页面  {#previewing-pages-using-contexthub-data}

ContextHub工具栏显示ContextHub存储区中的数据，并允许您更改存储区数据。 ContextHub工具栏可用于预览由ContextHub存储区中的数据确定的内容。

工具栏包含一系列用户界面模式，这些模式包含一个或多个UI模块。

* UI模式是显示在工具栏左侧的图标。 选择图标后，工具栏会显示它包含的UI模块。
* UI模块显示来自一个或多个ContextHub存储的数据。 某些UI模块还允许您处理存储数据。

ContextHub安装多个UI模式和UI模块。 您的管理员可能已 [已配置ContextHub](/help/implementing/developing/personalization/configuring-contexthub.md) 以显示不同的标记。

## 显示ContextHub工具栏 {#revealing-the-contexthub-toolbar}

ContextHub工具栏在预览模式下可用。 该工具栏仅在创作实例中且管理员已将其启用后才可用。

![ContextHub 工具栏](/help/sites-cloud/authoring/assets/contexthub-toolbar.png)

1. 在打开页面进行编辑时，在工具栏上选择预览。

   ![“预览”按钮](/help/sites-cloud/authoring/assets/contexthub-preview-button.png)

1. 要显示工具栏，请选择ContextHub图标。

   ![ContextHub 按钮](/help/sites-cloud/authoring/assets/contexthub-button.png)

## 用户界面模块功能 {#ui-module-features}

提供的每个UI模块都是一组不同的功能，但以下类型的功能是通用的。 由于UI模块是可扩展的，因此您的开发人员可以实施所需的其他功能。

### 工具栏内容 {#toolbar-content}

UI 模块可以在工具栏中显示一个或多个 ContextHub 存储区中的数据。UI 模块使用图标和标题来标识自身。

![ContextHub 角色](/help/sites-cloud/authoring/assets/contexthub-persona-button.png)

### 弹出窗口内容 {#popup-content}

某些 UI 模块在单击或点按时，会显示一个弹出覆盖窗口。通常，弹出窗口包含的信息比工具栏上显示的信息要多。

![ContextHub 配置文件信息](/help/sites-cloud/authoring/assets/contexthub-profile.png)

### 弹出Forms {#popup-forms}

模块的弹出叠加图可以包括表单元素，以便您更改ContextHub存储中的数据。 如果页面内容由存储数据决定，则可以使用表单并观察页面内容的变化。

### 全屏模式 {#fullscreen-mode}

弹出窗口叠加图可以包含图标，您选择图标以展开弹出内容以覆盖整个浏览器窗口或屏幕。

![全屏按钮](/help/sites-cloud/authoring/assets/contexthub-fullscreen.png)
