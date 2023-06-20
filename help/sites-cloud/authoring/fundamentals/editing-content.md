---
title: 编辑页面内容
description: 创建页面后，您可以编辑内容以进行所需的更新
exl-id: 8af0f621-14e8-4605-a51a-a3be21f19092
source-git-commit: 635f4c990c27a7646d97ebd08b453c71133f01b3
workflow-type: tm+mt
source-wordcount: '3004'
ht-degree: 58%

---

# 编辑页面内容{#editing-page-content}

创建页面（新页面或者作为启动项或 Live Copy 的一部分）后，您可以编辑内容，以进行所需的更新。

内容添加方式 [组件](/help/sites-cloud/authoring/features/components-console.md) （适用于内容类型）的任意页面加载项。 然后，可以就地编辑、移动或删除这些内容。

>[!NOTE]
>
>您的帐户需要拥有适当的访问权以及相应的权限才能进行编辑。
>
>如果您遇到任何问题，我们建议您与系统管理员联系。
<!--
>Your account needs the [appropriate access rights](/help/sites-administering/security.md) and [permissions](/help/sites-administering/security.md#permissions) to edit pages.
-->

>[!NOTE]
>
>如果您的页面和/或模板进行了适当设置，那么您可以在编辑时使用[响应式布局](/help/sites-cloud/authoring/features/responsive-layout.md)。

>[!TIP]
>
>在&#x200B;**编辑**&#x200B;模式下，内容中的链接是可见的，但是&#x200B;**不可访问**。如果您要使用内容中的链接进行导航，请使用[预览模式](#previewing-pages)。

## 页面工具栏 {#page-toolbar}

根据页面配置，用户可以通过页面工具栏访问相应的功能。

![页面工具栏](/help/sites-cloud/authoring/assets/editing-page-toolbar.png)

通过工具栏可访问多个选项。 根据您当前的上下文和配置，某些选项可能不可用。

* **切换侧面板**

  这将打开/关闭侧面板，侧面板中包含 [资产浏览器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser)， [组件浏览器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser)、和 [内容树](/help/sites-cloud/authoring/fundamentals/environment-tools.md#content-tree).

  ![侧面板切换](/help/sites-cloud/authoring/assets/side-panel-toggle.png)

* **页面信息**

  提供对的访问 [页面信息](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information) 菜单，其中包含页面详细信息以及可在页面上执行的操作，包括查看和编辑页面信息、查看页面属性以及发布/取消发布页面。

  ![“页面信息”按钮](/help/sites-cloud/authoring/assets/page-information-icon.png)

* **模拟器**

  切换 [模拟器工具栏](/help/sites-cloud/authoring/features/responsive-layout.md#selecting-a-device-to-emulate)，用于模拟页面在其他设备上的外观。 在布局模式下会自动切换。

  ![“模拟器”按钮](/help/sites-cloud/authoring/assets/emulator.png)

* **ContextHub**

  打开 [ContextHub](/help/sites-cloud/authoring/personalization/contexthub.md)。仅在预览模式下可用。

  ![ContextHub 按钮](/help/sites-cloud/authoring/assets/context-hub.png)

* **页面标题**

  这仅供参考。

  ![页面标题](/help/sites-cloud/authoring/assets/page-title.png)

* **模式选择器**

  显示当前 [模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) 并允许您选择其他模式，例如编辑、布局、时间扭曲或定位。

  ![“模式选择器”按钮](/help/sites-cloud/authoring/assets/mode-selector.png)

* **预览**

  启用 [预览模式](#preview-mode). 这会显示发布后显示的页面。

  ![“预览”按钮](/help/sites-cloud/authoring/assets/preview.png)

* **批注**

  允许您添加 [批注](/help/sites-cloud/authoring/fundamentals/annotations.md) 查看页面时跳转到页面。 在第一个批注之后，图标将切换到指示页面上批注数量的数字。

  ![“注释”按钮](/help/sites-cloud/authoring/assets/annotations.png)

### 状态通知 {#status-notification}

如果页面是一个[工作流](/help/sites-cloud/authoring/workflows/overview.md)或多个工作流的一部分，则在编辑该页面时，将在屏幕顶部的通知栏中显示此信息。

![工作流通知](/help/sites-cloud/authoring/assets/editing-workflow-notification.png)

>[!NOTE]
>
>状态栏仅对具有适当权限的用户帐户可见。

通知会列出针对页面运行的工作流。 如果当前工作流步骤涉及用户，则选项 [影响工作流状态](/help/sites-cloud/authoring/workflows/participating.md) 和获取有关工作流的更多信息，例如：

* **完成** - 打开&#x200B;**完成工作项目**&#x200B;对话框
* **委派** - 打开&#x200B;**完成工作项目**&#x200B;对话框
* **查看详细信息** - 打开工作流的&#x200B;**详细信息**&#x200B;窗口

通过通知栏完成和委派工作流步骤，与从“通知”收件箱中[参与工作流](/help/sites-cloud/authoring/workflows/participating.md)的操作方式相同。

如果页面从属于多个工作流，则在通知的右侧端将显示工作流的数量，并且还提供有箭头按钮以允许您滚动浏览工作流。

![多个工作流通知](/help/sites-cloud/authoring/assets/editing-workflow-notification-multiple.png)

## 组件占位符 {#component-placeholder}

组件占位符是一个指示器，用于显示组件在放置时的放置位置 — 在当前悬停的组件上方。

* 将新组件添加到页面时（从组件浏览器中拖动）：

  ![向页面添加新组件时的占位符](/help/sites-cloud/authoring/assets/editing-component-placeholder.png)

* 移动现有组件时：

  ![在页面上移动现有组件时的占位符](/help/sites-cloud/authoring/assets/editing-component-placeholder-existing.png)

## 插入组件 {#inserting-a-component}

### 使用组件浏览器插入组件 {#inserting-a-component-from-the-components-browser}

您可以使用添加新组件 [组件浏览器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser). 此 [组件占位符](#component-placeholder) 显示组件的放置位置：

1. 确保页面处于&#x200B;[**编辑**&#x200B;模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)。
1. 打开[组件浏览器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser)。
1. 将所需的组件拖动到[所需位置](#component-placeholder)。
1. [编辑](#edit-content) 组件。

>[!NOTE]
>
>在移动设备上，组件浏览器将填充整个屏幕。 开始拖动组件后，浏览器将关闭以再次显示页面，以便您可以放置组件。

### 使用段落系统插入组件 {#inserting-a-component-from-the-paragraph-system}

您可以使用段落系统的&#x200B;**将组件拖动到此处**&#x200B;框添加新组件：

1. 确保页面处于&#x200B;[**编辑**&#x200B;模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)。
1. 有两种方法可以从段落系统中选择和添加新组件：

   * 选择 **插入组件** 选项(+)(位于现有组件的工具栏或 **将组件拖动到此处** 盒子。

     ![插入组件](/help/sites-cloud/authoring/assets/editing-insert-component.png)

   * 如果您使用的是桌面设备，则可以双击&#x200B;**将组件拖动到此处**&#x200B;框。

   * **插入新组件**&#x200B;对话框将打开以允许您选择需要的组件：

     ![“插入新组件”对话框](/help/sites-cloud/authoring/assets/editing-insert-component-selection.png)

1. 选定的组件将添加到页面底部。 [编辑](#edit-content) 所需的组件。

### 使用资产浏览器插入组件 {#inserting-a-component-using-the-assets-browser}

您还可以通过从以下位置拖动资产，向页面中添加新组件： [资产浏览器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser). 这将自动创建适当类型的新组件（并包含资产）。

可针对您的安装配置此行为。有关更多详细信息，请参阅配置段落系统以便可通过拖动资产创建组件实例。<!--This behavior can be configured for your installation. See [Configuring a Paragraph System so that Dragging an Asset Creates a Component Instance](/help/sites-developing/developing-components.md#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance) for further details.-->

要通过拖动以上某一资产类型创建组件，请执行以下操作：

1. 确保页面处于&#x200B;[**编辑**&#x200B;模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)。
1. 打开 [资产浏览器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser).
1. 将所需的资产拖动到所需位置。 此 [组件占位符](#component-placeholder) 显示组件的放置位置。

   在所需位置创建一个适合该资源类型的组件，该组件包含选定的资源。

1. [编辑](#edit-content) 组件（如果需要）。

>[!NOTE]
>
>在移动设备上，资产浏览器将填充整个屏幕。 开始拖动资产后，浏览器将关闭以再次显示页面，以便您可以放置资产。

如果您在浏览资源时发现需要对某个资源进行快速更改，则可以启动 [资产编辑器](/help/assets/manage-digital-assets.md) 直接从浏览器中单击资产名称旁边的编辑图标。

![资产编辑按钮](/help/sites-cloud/authoring/assets/asset-edit-button.png)

## 组件工具栏 {#component-toolbar}

选择组件后将打开工具栏。通过工具栏可访问能够对组件执行的各种不同操作。

用户可用的实际操作会根据相应的情况显示，此处并非对所有操作都进行了描述。

![组件工具栏](/help/sites-cloud/authoring/assets/editing-component-toolbar.png)

* **编辑**

  [取决于组件类型](/help/sites-cloud/authoring/fundamentals/components.md)，这允许您 [编辑组件的内容](#edit-content). 通常会提供一个工具栏。

  ![编辑按钮](/help/sites-cloud/authoring/assets/editing-component-toolbar-edit.png)

* **配置**

  [取决于组件类型](/help/sites-cloud/authoring/fundamentals/components.md)，可编辑和配置组件的属性。 通常会打开一个对话框。

  ![“配置”按钮](/help/sites-cloud/authoring/assets/editing-component-toolbar-configure.png)

* **复制**

  这会将组件复制到剪贴板。 执行粘贴操作后，原始组件将保留。

  ![“复制”按钮](/help/sites-cloud/authoring/assets/editing-component-toolbar-copy.png)

* **剪切**

  这会将组件复制到剪贴板。 执行粘贴操作后，将删除原始组件。

  ![“剪切”按钮](/help/sites-cloud/authoring/assets/editing-component-toolbar-cut.png)

* **删除**

  这将从页面中删除包含您确认的组件。

  ![“删除”按钮](/help/sites-cloud/authoring/assets/editing-component-toolbar-delete.png)

* **插入组件**

  这将打开对话框，您可以 [添加新组件](/help/sites-cloud/authoring/fundamentals/editing-content.md#inserting-a-component-from-the-paragraph-system).

  ![“插入”按钮](/help/sites-cloud/authoring/assets/editing-component-toolbar-insert.png)

* **粘贴**

  这会将组件从剪贴板粘贴到页面。 原始是否保留，取决于您使用的是复制还是剪切。

   * 您可以粘贴到同一页面或不同页面。
   * 粘贴的项目将粘贴到您选择粘贴操作的项目的上方。
   * 仅当剪贴板上有内容时，才会显示粘贴操作。

  ![“粘贴”按钮](/help/sites-cloud/authoring/assets/editing-component-toolbar-paste.png)

  >[!NOTE]
  >
  >如果在剪切/复制操作之前粘贴到已打开的其他页面，则必须刷新该页面才能查看粘贴的内容。

* **组**

  这允许您同时选择多个组件。 在桌面设备上，可以通过以下方式实现相同目的 **按住Ctrl并单击** 或 **按住Command并单击**.

  ![“组”按钮](/help/sites-cloud/authoring/assets/editing-component-toolbar-group.png)

* **父项**

  此项允许您选择选定组件的父组件。

  ![“父项”按钮](/help/sites-cloud/authoring/assets/editing-component-toolbar-parent.png)

* **布局**

  这允许您修改 [布局](/help/sites-cloud/authoring/fundamentals/editing-content.md#edit-component-layout) 选定组件的ID。 这仅适用于选定的组件，不会激活 [布局模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) 整个页面。

  ![“布局”按钮](/help/sites-cloud/authoring/assets/editing-component-toolbar-layout.png)

* **转换为体验片段变体**

  允许您从选定的组件创建一个新的[体验片段](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)，或将其添加到现有的体验片段中。

  ![“转换为体验片段”按钮](/help/sites-cloud/authoring/assets/editing-component-toolbar-xf.png)

## 编辑内容 {#edit-content}

有两种方法可以在组件中添加和/或编辑内容：

* 打开 [用于编辑的组件对话框](#component-edit-dialog).
* [拖放资产](#drag-and-drop-assets-into-component) 以直接添加内容。

### “组件编辑”对话框 {#component-edit-dialog}

您可以打开组件以使用组件工具栏 [的编辑（铅笔）图标编辑内容](#component-toolbar)。

确切的编辑选项将取决于组件。 对于某些组件 [所有操作仅在全屏模式下可用](#edit-content-full-screen-mode). 例如：

* 文本组件

  ![文本组件的工具栏](/help/sites-cloud/authoring/assets/editing-text-component-toolbar.png)

* 图像组件

  ![图像组件的工具栏](/help/sites-cloud/authoring/assets/editing-image-component-toolbar.png)

  >[!NOTE]
  >
  >无法对空的图像组件执行编辑操作。
  >
  >您必须先将图像拖动或上传到组件，然后才能开始编辑。

* 图像组件 — 全屏

  [进入图像组件的全屏模式](#edit-content-full-screen-mode) ，可以留出更多空间来编辑图像，并显示额外的编辑选项，如“启动映射”和“重 **置缩放”******。 此外，全屏模式还允许选择裁剪预设。

  ![图像组件的全屏模式](/help/sites-cloud/authoring/assets/editing-image-component-full-screen.png)

* 使用多个基本组件构建的组件首先将要求您确认所需的编辑选项集：

### 将资产拖放到组件中 {#drag-and-drop-assets-into-component}

对于特定的组件类型（例如图像），您可以直接从资产浏览器中将资产拖放到组件中，从而更新内容。

## 以全屏模式编辑内容 {#edit-content-full-screen-mode}

对于所有组件，都可以通过以下图标进入（和退出）全屏模式：

![“全屏”按钮](/help/sites-cloud/authoring/assets/editing-full-screen.png)

例如，**文本**&#x200B;组件：

![全屏模式下的文本组件](/help/sites-cloud/authoring/assets/editing-text-full-screen.png)

>[!NOTE]
>
>对于某些组件，全屏模式比基本的就地编辑器具有更多的可用选项。

## 移动组件 {#moving-a-component}

要移动段落组件，请执行以下操作：

1. 通过点按并按或点按并按住选择要移动的段落。
1. 将段落拖动到新位置。 AEM指示可以存放段落的位置。 将其拖放到所需位置。

   ![移动组件](/help/sites-cloud/authoring/assets/editing-moving-component.png)

1. 此时会移动您的段落。

>[!TIP]
>
>您也可以使用[剪切并粘贴](#component-toolbar)来移动组件。

## 编辑组件布局 {#edit-component-layout}

您无需为了调整组件而反复不停地从编辑模式切换到[布局模式](/help/sites-cloud/authoring/features/responsive-layout.md)，而是可以为组件选择&#x200B;**布局**&#x200B;操作来更改该组件的布局，在此过程中，由于不必离开编辑模式，从而节省了大量时间。

1. 在站点控制台的&#x200B;**编辑**&#x200B;模式下，选择某个组件会显示该组件的工具栏。

   ![页面组件的组件工具栏](/help/sites-cloud/authoring/assets/editing-layout-toolbar.png)

   单击或点按&#x200B;**布局**&#x200B;操作可调整组件的布局。

   ![组件工具栏的“布局”按钮](/help/sites-cloud/authoring/assets/editing-component-toolbar-layout.png)

1. 选择“布局”操作后：

   * 组件显示的调整大小手柄。
   * 屏幕顶部将显示模拟器工具栏。
   * 组件工具栏上将显示布局操作，而不是标准编辑操作。

   ![布局模式下的组件](/help/sites-cloud/authoring/assets/editing-layout-mode.png)

   此时，您便可以像在[布局模式](/help/sites-cloud/authoring/features/responsive-layout.md#defining-layouts-layout-mode)中一样修改组件布局。

1. 在进行必要的布局更改后，单击组件操作菜单中的&#x200B;**关闭**&#x200B;按钮以停止修改组件的布局。组件的工具栏会返回到其正常的编辑状态。

   ![页面组件的组件工具栏](/help/sites-cloud/authoring/assets/editing-layout-exit.png)

>[!TIP]
>
>“布局”操作仅限用于选定的组件。例如，如果您正在编辑一个组件的布局，然后又单击另一个组件，则将为新选择的组件显示标准编辑工具栏（而不是布局工具栏），而大小调整手柄以及模拟器工具栏将会消失。
>
>如果需要编辑会影响多个组件的页面整体布局，请切换到 [布局模式](/help/sites-cloud/authoring/features/responsive-layout.md).

## 继承组件 {#inherited-components}

继承是一种机制，通过该机制，可以将内容从一个组件自动推送到另一个组件。继承组件可能是多种情况的产物，包括：

* [多站点管理](/help/sites-cloud/administering/msm/overview.md)
* [启动项](/help/sites-cloud/authoring/launches/overview.md)（当基于 Live Copy 时）。

您可以取消（随后也可以重新启用）继承。根据组件的不同，如果组件位于 Live Copy 或启动项的一个页面（基于 Live Copy）中，则可以从组件工具栏中执行此操作。

![显示继承关系的组件工具栏](/help/sites-cloud/authoring/assets/editing-component-toolbar-inheritance.png)

例如：

* 取消继承

  ![“取消继承”按钮](/help/sites-cloud/authoring/assets/editing-cancel-inheritance.png)

* 重新启用继承（如果继承已取消）

  ![“重新启用继承”按钮](/help/sites-cloud/authoring/assets/editing-reenable-inheritance.png)

* “转出”操作也在 Blueprint 或 Live Copy 源中可用

  ![“转出”按钮](/help/sites-cloud/authoring/assets/editing-rollout.png)

## 编辑页面模板 {#editing-the-page-template}

您可以通过在[“页面信息”菜单](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information)中选择&#x200B;**编辑模板**&#x200B;来轻松切换到[模板编辑器](/help/sites-cloud/authoring/features/templates.md#editing-templates-template-authors)。

在[列视图](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view)或[列表视图](/help/sites-cloud/authoring/getting-started/basic-handling.md#list-view)中选择页面时，您可以轻松查看该页面所基于的模板。

## Live Copy 状态 {#live-copy-status}

此 [Live Copy状态页面模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) 允许您快速概述Live Copy状态以及哪些组件是/不是继承的：

* 绿色边框：继承
* 粉红色边框：继承已被取消

例如：

![显示的 Live Copy 状态示例](/help/sites-cloud/authoring/assets/editing-live-copy-status.png)

## 添加注释 {#adding-annotations}

[批注](/help/sites-cloud/authoring/fundamentals/annotations.md) 允许审阅人和其他作者针对您的内容提供反馈。 它们通常用于审阅和验证。

## 预览页面 {#previewing-pages}

可通过以下两个选项预览页面：

* [预览模式](#preview-mode) - 快速就地预览
* [查看已发布的项目](#view-as-published)  — 可在新选项卡中打开页面的完整预览

>[!TIP]
>
>* 内容中的链接是可见的，但在编辑模式下不可访问。
>* 如果您希望使用链接进行导航，请使用任一预览选项。
>* 使用[键盘快捷键](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) `Ctrl-Shift-M` 可在预览和最后选择的模式之间切换。

>[!NOTE]
>
>这两个预览选项均可设置 WCM 模式 Cookie。

### 预览模式 {#preview-mode}

编辑内容时，您可以使用预览功能预览页面 [模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes). 此模式：

* 会隐藏各种编辑机制，以便让您快速查看页面在发布时是什么样子。
* 允许您使用链接进行导航。
* Do **非** 刷新页面内容。

创作时，使用页面编辑器右上角的图标可使用预览模式：

![“预览”按钮](/help/sites-cloud/authoring/assets/preview.png)

### 以发布的形式查看 {#view-as-published}

此 **查看已发布的项目** 选项可从以下网址获得： [页面信息](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information) 菜单。 这将在新选项卡中打开页面，刷新内容并完全按照其在发布环境中的显示方式显示页面。

## 锁定页面 {#locking-a-page}

AEM 允许您锁定页面，这样其他人就无法修改页面内容。当您要对某个特定页面做出大量编辑，或者需要冻结页面一段时间时，此功能非常有用。

可以从以下任一位置锁定页面：

* **站点** 控制台

   1. 使用以下方式选择页面 [选择模式](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources).
   1. 选择锁图标。

      ![“锁定”按钮](/help/sites-cloud/authoring/assets/lock.png)

* **页面编辑器**

   1. 选择 **页面信息** 图标以打开菜单。
   1. 选择 **锁定页面** 选项。

锁定后，控制台视图信息便会更新；编辑时，工具栏中会出现锁定符号。

![锁定页面的示例](/help/sites-cloud/authoring/assets/editing-locked-page.png)

>[!CAUTION]
>
>模拟用户身份时可以执行页面锁定。但是，以这种方式锁定的页面只能由（客户）使用被模拟的用户解锁。
>
>无法通过模拟锁定页面的用户的身份来解锁页面。
>
>如果锁定页面的用户无法解锁页面，请联系客户支持以评估解除锁定的选项。

## 解锁页面 {#unlocking-a-page}

解锁页面的方法与[锁定页面](#locking-a-page)非常相似。在锁定页面后，锁定选项就会被替换为解锁操作选项。

“页面信息”菜单会将&#x200B;**解锁**&#x200B;列为一个选项，并且站点控制台中的“锁定”图标会被替换为&#x200B;**解锁**&#x200B;图标。

![“解锁”按钮](/help/sites-cloud/authoring/assets/unlock.png)

>[!CAUTION]
>
>模拟用户身份时可以执行页面锁定。但是，以这种方式锁定的页面只能由（客户）随后使用被模拟的用户解锁。
>
>无法通过模拟锁定页面的用户的身份来解锁页面。
>
>如果锁定页面的用户无法解锁页面，请联系客户支持以评估解除锁定的选项。

<!--
>[!CAUTION]
>
>Locking a page can be performed when impersonating a user. However a page locked in this way can only then be unlocked by the user who was impersonated, or by a user with admin rights (a member of AEM Administrator IMS profile).
>
>Pages can not be unlocked by impersonating the user who locked the page.
-->

<!--
>Locking a page can be performed when [impersonating a user](/help/sites-administering/security.md#impersonating-another-user). However a page locked in this way can only then be unlocked by the user who was impersonated or by the admin user.
-->

## 撤消和重做页面编辑 {#undoing-and-redoing-page-edits}

通过以下图标可撤消或重做某项操作。这些图标会适时地出现在工具栏中：

![“撤消”和“重做”按钮](/help/sites-cloud/authoring/assets/redo.png)

>[!TIP]
>
>* 也可使用[键盘快捷键](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) `Ctrl-Z` 撤消页面编辑操作。
>* 也可使用键盘快捷键 `Ctrl-Y` 重做页面编辑操作。

>[!NOTE]
>
>有关撤消和重做页面编辑时可执行操作的完整详细信息，请参阅[撤消和重做页面编辑 - 理论](#undoing-and-redoing-page-edits-the-theory)。

## 撤消和重做页面编辑 – 理论 {#undoing-and-redoing-page-edits-the-theory}

AEM 会按照您执行操作的顺序来存储这些操作的历史记录，这样，您便可以按照执行顺序撤消多个操作，然后在必要时重做它们，以重新应用一个或多个操作。

如果选择了内容页面上的某个元素（例如文本组件），则撤消和重做命令将适用于选定的项目。

撤消和重做命令的行为与其他软件中的类似。在您对内容做出决策时，可使用这些命令恢复网页的最近状态。例如，如果您将文本段落移至页面上的其他位置，可以使用撤消命令移回该段落。如果您随后确定上一个位置更好，请使用redo命令“撤消撤消操作”。

例如，您可以：

* 只要您自使用撤消操作后未进行任何页面编辑，就可以重做操作。
* 撤消最多20个编辑操作（默认设置）。
* 还使用 [键盘快捷键](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) 用于撤消和重做。

可以对以下类型的页面更改使用撤消和重做：

* 添加、编辑、删除和移动段落
* 就地编辑段落内容
* 在页面中复制、剪切和粘贴项目

>[!NOTE]
>
>* 对文件和图像的更改执行撤消和重做操作需要特殊的权限。
>* 文件和图像的更改历史记录至少会持续10小时。 然而，在这段时间之后，这些变化的撤销并非板上钉钉。 您的管理员可以更改10小时的默认时间。
>* 系统管理员可以根据您实例的要求，配置撤消/重做功能的各个方面。
<!--* Your system administrator can [configure various aspects of the Undo/Redo features](/help/sites-administering/config-undo.md) according to the requirements for your instance.-->
