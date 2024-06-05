---
title: AEM页面编辑器
description: AEM页面编辑器是一个用于创作内容的强大工具。
exl-id: da7d5933-f6c9-4937-a483-ec4352fba86b
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1431'
ht-degree: 39%

---

# AEM页面编辑器 {#editing-page-content}

在中创建页面后 [**站点** 控制台，](/help/sites-cloud/authoring/sites-console/introduction.md) 您可以使用AEM页面编辑器编辑页面的内容，该编辑器是用于创作内容的强大工具。

>[!NOTE]
>
>在中编辑页面时 [**站点** 控制台，](/help/sites-cloud/authoring/sites-console/introduction.md) 控制台将打开与页面对应的编辑器 [模板：](/help/sites-cloud/authoring/sites-console/templates.md) 本文档中描述的页面编辑器，或者 [通用编辑器。](/help/sites-cloud/authoring/universal-editor/authoring.md)

>[!NOTE]
>
>您的帐户需要拥有适当的访问权限和权限才能编辑页面。 如果您没有权限，请联系您的系统管理员。

## 方向 {#orientation}

AEM页面编辑器主要由三个部分组成：

1. [工具栏](#toolbar)  — 利用工具栏，可快速更改页面模式并访问其他页面设置。
1. [侧面板](#side-panel)  — 利用侧面板，可访问页面组件和资产以及其他创作工具。
1. [编辑器](#editor)  — 在编辑器中，您可以对内容进行更改并进行预览。

![页面编辑器的布局](assets/page-editor-layout.png)

内容使用可拖动到页面上的[组件](/help/sites-cloud/authoring/components-console.md)（适用于内容类型）进行添加。然后，可以就地编辑、移动或删除这些内容。

### 工具栏 {#page-toolbar}

根据页面配置，用户可通过页面工具栏访问与上下文相关的功能。

![页面编辑器工具栏](assets/page-editor-toolbar.png)

#### 侧面板 {#side-panel-button}

这将打开/关闭 [侧面板，](/help/sites-cloud/authoring/page-editor/editor-side-panel.md) ，其中包含资产浏览器、组件浏览器和内容树。

![侧面板切换](assets/page-editor-side-panel-toggle.png)

#### 页面信息 {#page-information}

通过此选项可访问详细的页面信息，包括页面详细信息和可在页面上执行的操作，包括查看和编辑页面信息、查看页面属性以及发布/取消发布页面。

![“页面信息”按钮](assets/page-editor-page-information-icon.png)

**页面信息** 打开一个下拉菜单，提供有关所选页面的最后一次编辑和最后一次发布的详细信息。 根据页面、其站点和实例的特性，其他操作可用。

* [打开属性](/help/sites-cloud/authoring/sites-console/page-properties.md)
* [转出页](/help/sites-cloud/administering/msm/overview.md#msm-from-the-ui)
* [启动工作流](/help/sites-cloud/authoring/workflows/applying.md#starting-a-workflow-from-the-page-editor)
* [锁定页面](/help/sites-cloud/authoring/page-editor/introduction.md#locking-unlocking)
* [发布页面](/help/sites-cloud/authoring/sites-console/publishing-pages.md#publishing-pages-1)
* [取消发布页面](/help/sites-cloud/authoring/sites-console/publishing-pages.md#unpublishing-pages)
* [编辑模板](/help/sites-cloud/authoring/sites-console/templates.md)
* [以发布的形式查看](/help/sites-cloud/authoring/page-editor/introduction.md#view-as-published)
* [以管理员身份查看](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources)
* [帮助](/help/sites-cloud/authoring/basic-handling.md#accessing-help)
* [提升启动项](/help/sites-cloud/authoring/launches/promoting.md)（如果该页面是启动项）

另外，在适当时，**页面信息**&#x200B;还允许访问分析和建议。

#### 模拟器 {#emulator}

这将切换 [模拟器工具栏](/help/sites-cloud/authoring/page-editor/responsive-layout.md#selecting-a-device-to-emulate)，用于模拟页面在其他设备上的外观。 这会在布局模式下自动启用。

![“模拟器”按钮](assets/page-editor-emulator.png)

#### ContextHub {#context-hub}

这将打开 [ContextHub。](/help/sites-cloud/authoring/personalization/contexthub.md) 它仅在 **预览** 模式。

![ContextHub 按钮](assets/page-editor-context-hub.png)

#### 页面标题 {#page-title}

这是页面的标题，以大写字母作为信息呈现。

![页面标题](assets/page-editor-page-title.png)

#### 模式选择器 {#mode-selector}

模式选择器显示当前 [模式](/help/sites-cloud/authoring/page-editor/introduction.md#mode-selector) 并允许您选择其他模式，如编辑、布局、时间扭曲或定位。

![“模式选择器”按钮](assets/page-editor-mode-selector.png)

编辑页面时可以使用多种模式来执行不同的操作：

* [编辑](/help/sites-cloud/authoring/page-editor/edit-content.md)  — 编辑页面内容时使用的模式
* [布局](/help/sites-cloud/authoring/page-editor/responsive-layout.md)  — 允许您创建和编辑依赖于设备的响应式布局（如果页面基于布局容器）
* [定位](/help/sites-cloud/authoring/personalization/targeted-content.md)  — 通过在所有渠道中进行定位和衡量来提高内容相关性
* [时间扭曲](/help/sites-cloud/authoring/sites-console/page-versions.md#timewarp)  — 查看特定时间点的页面状态
* [Live Copy状态](/help/sites-cloud/authoring/page-editor/introduction.md#live-copy-status)  — 允许快速概述Live Copy状态以及哪些组件是/不是继承的
* [开发人员模式](/help/implementing/developing/tools/developer-mode.md)
* [预览](/help/sites-cloud/authoring/page-editor/introduction.md#previewing-pages)  — 查看发布环境中显示的页面；或使用内容中的链接进行导航
* [批注](/help/sites-cloud/authoring/page-editor/annotations.md)  — 在页面上添加或查看注释

>[!NOTE]
>
>* 根据页面的特性，某些模式可能不可用。
>* 某些模式需要相应的许可/权限才能访问。
>* 由于空间限制，“开发人员”模式在移动设备上不可用。
>* 有一个 [键盘快捷键](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md) ( `Ctrl-Shift-M`)以在 **预览** 和当前选择的模式(例如， **编辑**， **布局**，等等)。

#### 预览 {#preview}

此 **预览** 按钮启用 [预览模式。](#preview-mode)，显示发布时显示的页面。

![“预览”按钮](assets/page-editor-preview.png)

#### 批注 {#annotate}

**批注** 模式允许您添加 [注释](/help/sites-cloud/authoring/page-editor/annotations.md) 查看页面时跳转到页面。 添加第一个注释后，该图标将切换为数字，以指示页面上的注释数量。

![“注释”按钮](assets/page-editor-annotations.png)

### 侧面板 {#side-panel}

侧面板提供对三个不同选项卡的访问权限。

* 用于向页面添加新内容的组件浏览器
* 用于向页面添加新资产的资产浏览器
* 用于浏览页面结构的内容树

![页面编辑器的侧面板](assets/page-editor-side-panel.png)

请参阅文档 [页面编辑器侧面板](/help/sites-cloud/authoring/page-editor/editor-side-panel.md) 以了解更多信息。

### 编辑器 {#editor}

在编辑器中，您可以直接对页面内容进行更改。 页面会按照您看到的方式进行渲染，您可以使用侧面板中的资产或组件浏览器拖放新内容以及就地编辑内容。

![页面编辑器的编辑器](assets/page-editor-editor.png)

## 编辑内容 {#editing-content}

现在，您已了解页面编辑器，可以开始编辑内容了。

请参阅文档 [使用AEM页面编辑器编辑内容](/help/sites-cloud/authoring/page-editor/edit-content.md) 以了解更多信息。

## 状态通知 {#status-notification}

如果页面属于 [工作流](/help/sites-cloud/authoring/workflows/overview.md) 或多个工作流时，此信息显示在编辑页面时工具栏下方的通知栏中。

![工作流通知](assets/page-editor-editing-workflow-notification.png)

>[!NOTE]
>
>状态栏仅对具有相应权限的用户帐户可见。

通知会列出正在针对页面运行的工作流。如果用户参与了当前工作流步骤，还可以使用[影响工作流状态](/help/sites-cloud/authoring/workflows/participating.md)和获取更多工作流相关信息的选项，例如：

* **完成** - 打开&#x200B;**完成工作项目**&#x200B;对话框
* **委派** - 打开&#x200B;**完成工作项目**&#x200B;对话框
* **查看详细信息** - 打开工作流的&#x200B;**详细信息**&#x200B;窗口

通过通知栏完成和委派工作流步骤，与从“通知”收件箱中[参与工作流](/help/sites-cloud/authoring/workflows/participating.md)的操作方式相同。

如果页面从属于多个工作流，则在通知的右侧端将显示工作流的数量，并且还提供有箭头按钮以允许您滚动浏览工作流。

![多个工作流通知](assets/page-editor-editing-workflow-notification-multiple.png)

## Live Copy 状态 {#live-copy-status}

此 **Live Copy状态** 页面模式可让您快速概述Live Copy状态以及/不继承哪些组件：

* 绿色边框：已继承
* 粉色边框：继承已被取消

例如：

![显示的 Live Copy 状态示例](assets/page-editor-editing-live-copy-status.png)

## 预览页面 {#previewing-pages}

可通过以下两个选项预览页面：

* [预览模式](#preview-mode)  — 快速就地预览
* [查看已发布的项目](#view-as-published)  — 在新选项卡中打开页面的完整预览

>[!TIP]
>
>* 内容中的链接是可见的，但在中不可访问 **编辑** 模式。
>* 如果您希望使用链接进行导航，请使用任一预览选项。
>* 使用[键盘快捷键](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md) `Ctrl-Shift-M` 可在预览和最后选择的模式之间切换。

>[!NOTE]
>
>这两个预览选项均可设置 WCM 模式 Cookie。

### 预览模式 {#preview-mode}

编辑内容时，您可以使用预览模式预览页面。 此模式：

* 会隐藏各种编辑机制，以便让您快速查看页面在发布时是什么样子。
* 让您使用链接进行导航。
* **不会**&#x200B;刷新页面内容。

创作时，使用页面编辑器右上角的图标即可使用预览模式：

![“预览”按钮](assets/page-editor-preview.png)

### 以发布的形式查看 {#view-as-published}

**查看已发布的项目**&#x200B;选项可从[页面信息](#page-information)菜单中获取。这会在新选项卡中打开页面，刷新内容并准确显示页面在发布环境中呈现的原貌。

## 锁定和解锁页面 {#locking-unlocking}

AEM允许您锁定页面，这样其他人就无法编辑其内容。 在对某个特定页面进行大量编辑时，或者需要冻结页面一段时间时，锁定很有用。

1. 选择&#x200B;**页面信息**&#x200B;图标来打开菜单。
1. 选择&#x200B;**锁定页面**&#x200B;选项。

锁定后，页面编辑器的工具栏中将显示锁定符号。

![锁定页面的示例](assets/page-editor-editing-locked-page.png)

解锁页面的方法与 [锁定页面](#locking-a-page). 锁定页面后，锁定选项就会被替换为解锁操作。

>[!CAUTION]
>
>* 模拟用户身份时可以执行页面锁定。但是，以这种方式锁定的页面只能由（客户）随后使用被模拟的用户解锁。
>* 无法通过模拟锁定页面的用户的身份来解锁页面。
>* 如果锁定页面的用户无法解锁页面，请联系客户支持以评估解除锁定的选项。

## 撤消和重做页面编辑 {#undoing-and-redoing-page-edits}

通过以下图标可撤消或重做某项操作。这些图标会适时地出现在工具栏中：

![“撤消”和“重做”按钮](assets/page-editor-redo.png)

>[!TIP]
>
>* 也可使用[键盘快捷键](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md) `Ctrl-Z` 撤消页面编辑操作。
>* 也可使用键盘快捷键 `Ctrl-Y` 重做页面编辑操作。

>[!NOTE]
>
>请参阅文档 [撤消和重做限制](/help/sites-cloud/authoring/page-editor/undo-redo.md) 有关撤消和重做页面编辑时可执行操作的完整详细信息。
