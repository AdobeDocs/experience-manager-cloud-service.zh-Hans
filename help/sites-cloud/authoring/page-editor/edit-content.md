---
title: 使用AEM页面编辑器编辑页面内容
description: AEM页面编辑器是一个用于创作内容的强大工具。
exl-id: eacfda02-ff53-42ed-b5b2-88be3879a5e9
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1612'
ht-degree: 32%

---

# 使用AEM页面编辑器编辑页面内容 {#edit-content}

AEM页面编辑器是一个用于创作页面内容的强大工具。 了解如何使用它来就地拖放内容和编辑内容。

## 概述 {#overview}

您可以在页面编辑器中执行三个基本操作来编辑内容：

1. [通过拖放到页面上来添加新组件](#adding-components)。
1. [通过拖放到页面上来添加新资源](#adding-asset)。
1. [就地编辑页面中已存在的组件](#edit-in-place)。

AEM页面编辑器提供了用于执行这些任务的直观的UI，并且还提供了对更高级功能的访问权限。

此外，该编辑器允许您组织页面上的现有内容，方法是

* [移动组件](#moving-components)
* [编辑组件布局](#editing-component-layout)
* [编辑组件继承](#inherited-components)

## 添加组件 {#adding-components}

您可以从侧面板](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#components-browser)中的[组件浏览器中选择新组件并将它们拖放到组件占位符中，从而将新组件拖放到页面上。

### 组件占位符 {#component-placeholder}

组件占位符是一个指示器，用于显示组件在放置时将放置的位置。 它有两种外观。

* 向页面添加新组件（从组件浏览器中拖动）时，它将显示为灰色框，其中包含您放置的组件的详细信息。

  ![向页面添加新组件时的占位符](assets/edit-content-component-placeholder.png)

* 当[移动现有组件](#movging-components)时，它将显示为蓝色正方形。

  ![在页面上移动现有组件时的占位符](assets/edit-content-move-placeholder.png)

在这两种情况下，所选目标都将在您拖动的组件下显示为蓝色轮廓。 目标（在释放组件时将放置该组件的位置）。

### 从组件浏览器添加组件 {#adding-a-component-from-the-components-browser}

您可以使用[组件浏览器](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#components-browser)添加新组件。[组件占位符](#component-placeholder)显示组件所在的位置。

1. 确保页面编辑器处于&#x200B;[**编辑**&#x200B;模式。](/help/sites-cloud/authoring/page-editor/introduction.md#mode-selector)
1. 打开[组件浏览器。](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#components-browser)
1. 将所需的组件拖动到[所需的位置](#component-placeholder)并释放。
1. [编辑](#edit-content)新放置的组件。

>[!NOTE]
>
>在移动设备上，组件浏览器将填满整个屏幕。在开始拖动组件后，浏览器将关闭以再次显示页面，以便您能够放置组件。

### 从段落系统添加组件 {#adding-a-component-from-the-paragraph-system}

您可以使用段落系统的&#x200B;**将组件拖动到此处**&#x200B;占位符添加新组件：

1. 确保页面编辑器处于&#x200B;[**编辑**&#x200B;模式。](/help/sites-cloud/authoring/page-editor/introduction.md#mode-selector)
1. 可通过以下两种方式在段落系统中选择和添加新组件：

   * 从现有组件的工具栏或&#x200B;**将组件拖动到此处**&#x200B;框中选择&#x200B;**插入组件**&#x200B;选项 (+)。

     ![插入组件](assets/edit-content-drag-components-here.png)

   * 如果您使用的是桌面设备，则可以双击&#x200B;**将组件拖动到此处**&#x200B;框。

1. 打开&#x200B;**插入新组件**&#x200B;对话框，允许您选择所需的组件。 点按或单击要添加的组件。

   * 使用搜索筛选器查找组件。
   * 使用组件名称旁边的信息图标了解有关该组件的更多信息。

   ![“插入新组件”对话框](assets/edit-content-insert-component.png)

1. 所选的组件即添加到您选择的目标中。 根据需要[编辑](#edit-content)组件。

## 添加资产 {#adding-asset}

您还可以通过从[资源浏览器拖动资源来向页面添加新组件。](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#assets-browser)这将自动创建相应类型的组件（并包含资产）。

可针对您的安装配置此行为。有关更多详细信息，请参阅文档[组件参考指南](/help/implementing/developing/components/reference.md#component-placeholders)。

要通过拖动以上某一资源类型创建组件，请执行以下操作：

1. 确保您的页面处于&#x200B;[**编辑**&#x200B;模式。](/help/sites-cloud/authoring/page-editor/introduction.md#mode-selector)
1. 打开[资源浏览器](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#assets-browser)。
1. 将所需的资源拖动到所需位置。[组件占位符](#component-placeholder)显示组件所在的位置，如果插入该组件，将显示目标。
1. 将资产发布到目标上。 在包含选定资产的所需位置创建一个适合该资产类型的组件。
1. 如有必要，请[编辑](#edit-content)该组件。

>[!NOTE]
>
>在移动设备上，资源浏览器将填满整个屏幕。在开始拖动资源后，浏览器将关闭以再次显示页面，以便您能够放置资源。

如果您在浏览资源时发现需要对某个资源进行快速更改，则可以直接从浏览器中单击该资源名称旁边的编辑图标，以启动[资源编辑器](/help/assets/manage-digital-assets.md)。

## 就地编辑组件 {#edit-in-place}

选择组件会打开组件工具栏。 这提供了对可对组件执行的各种操作的访问权限。

![组件工具栏](assets/edit-content-component-toolbar.png)

组件工具栏中可用的操作适用于所选的组件。 您可能会看到更多或更少的内容，具体取决于您选择的组件，此处可能会介绍这些组件，也可能不介绍这些组件。

* **编辑**&#x200B;允许您修改组件的内容，通常是就地修改。 其行为取决于组件。

  ![编辑按钮](assets/edit-content-edit.png)

* **Configure**&#x200B;允许您更改组件的一些与其内容不直接相关的参数，通常是在对话框中。 其行为取决于组件。

  ![“配置”按钮](assets/edit-content-configure.png)

* **复制**&#x200B;将组件复制到剪贴板以粘贴到其他位置。 原始元件保持不变。

  ![“复制”按钮](assets/edit-content-copy.png)

* **剪切**&#x200B;将组件复制到剪贴板。 原始组件将被删除。

  ![“剪切”按钮](assets/edit-content-cut.png)

* **Delete**&#x200B;会从包含您确认的页面中删除该组件。

  ![“删除”按钮](assets/edit-content-delete.png)

* **插入组件**&#x200B;打开对话框以[添加新组件。](#adding-a-component-from-the-paragraph-system)

  ![“插入”按钮](assets/edit-content-insert-component.png)

* **粘贴**&#x200B;将组件从剪贴板粘贴到页面。 原始文件是否保留，取决于您使用的是&#x200B;**副本**&#x200B;还是&#x200B;**剪切**。

   * 您可以粘贴到同一页面或其他页面。
   * 如果粘贴到剪切/复制操作之前已打开的其他页面，则必须刷新该页面才能看到粘贴的内容。
   * 粘贴的项目会被粘贴到选择粘贴操作时所在的项目上方。
   * 仅当剪贴板中含有内容时，才会显示“粘贴”操作。

  ![“粘贴”按钮](assets/edit-content-paste.png)

* **组**&#x200B;允许您同时选择多个组件。 在桌面设备上&#x200B;**按住 Ctrl 并单击**&#x200B;或&#x200B;**按住 Command 并单击**&#x200B;可实现同样的操作。

  ![“组”按钮](assets/edit-content-group.png)

* **Parent**&#x200B;选择选定组件的父组件。

  ![“父项”按钮](assets/edit-content-parent.png)

* **布局**&#x200B;允许您修改所选组件的[布局](#editing-component-layout)。

   * 此操作仅适用于选定组件，而不会激活整个页面的[布局模式](/help/sites-cloud/authoring/page-editor/introduction.md#mode-selector)。

  ![“布局”按钮](assets/edit-content-layout.png)

* **转化为体验片段变体**&#x200B;允许您从选定的组件创建[体验片段](/help/sites-cloud/authoring/fragments/content-fragments.md)，或将其添加到现有的体验片段中。

  ![“转换为体验片段”按钮](assets/edit-content-convert.png)

### 组件编辑对话框 {#component-edit-dialog}

某些组件提供了就地可用内容以外的其他编辑选项。 您可以打开组件的“编辑”对话框，即组件工具栏](#component-toolbar)的[编辑（铅笔）图标以访问其他配置选项。

确切的编辑选项取决于组件。对于某些组件[，某些操作将仅在全屏模式](#edit-content-full-screen-mode)下可用。 例如：

* 文本组件

  ![文本组件的工具栏](assets/edit-content-text-component.png)

* 图像组件

  ![图像组件的工具栏](assets/edit-content-image-component.png)

### 以全屏模式编辑组件 {#edit-content-full-screen-mode}

许多组件提供了用于编辑的全屏模式，可通过此按钮访问这些模式。

![“全屏”按钮](/help/sites-cloud/authoring/assets/editing-full-screen.png)

全屏编辑允许显示比就地编辑器（如图像组件）更多的编辑选项。

![全屏模式下的图像组件](assets/edit-content-image-component-full-screen.png)

使用&#x200B;**最小化**&#x200B;按钮以存在全屏模式。

![最小化按钮](assets/edit-content-minimize.png)

## 移动组件 {#moving-components}

要移动组件，请执行以下操作：

1. 通过长按或长按选择要移动的组件。
1. 将组件拖动到新位置。

   * 页面编辑器指示具有[占位符](#component-placeholder)的组件的位置，以及可以使用目标放置段落的位置。

   ![移动组件](assets/edit-content-move-placeholder.png)

1. 将其拖放到所需位置。

>[!TIP]
>
>您也可以使用[剪切并粘贴](#component-toolbar)来移动组件。

## 编辑组件布局 {#editing-component-layout}

您无需为了调整组件而反复不停地从编辑模式切换到[布局模式](/help/sites-cloud/authoring/page-editor/responsive-layout.md)，而是可以为组件选择&#x200B;**布局**&#x200B;操作来更改该组件的布局，在此过程中，由于不必离开编辑模式，从而节省了大量时间。

1. 在站点控制台的&#x200B;**编辑**&#x200B;模式下，选择一个组件以显示该组件的工具栏。

1. 选择&#x200B;**布局**&#x200B;操作以调整组件的布局。

   ![组件工具栏的“布局”按钮](assets/edit-content-layout.png)

1. 在选择Layout操作后，您可以像在[布局模式下一样修改组件的布局。](/help/sites-cloud/authoring/page-editor/responsive-layout.md#defining-layouts-layout-mode)

   * 将显示用于调整组件大小的手柄。
   * 在屏幕的顶部将显示模拟器工具栏。
   * 在组件工具栏中将显示布局操作而不是标准编辑操作。

   ![布局模式下的组件](assets/edit-content-layout-mode.png)

1. 在进行必要的布局更改后，点按或单击组件操作菜单中的&#x200B;**关闭**&#x200B;按钮以停止修改组件的布局，组件工具栏将返回到其正常的编辑状态。

   ![页面组件的组件工具栏](assets/edit-content-layout-close.png)

>[!TIP]
>
>“布局”操作仅限用于选定的组件。例如，如果您正在编辑一个组件的布局，然后单击另一个组件，则将为新选择的组件显示标准编辑工具栏（而不是布局工具栏），并且大小调整手柄和模拟器工具栏将会消失。
>
>如果您需要编辑影响到多个组件的总体页面布局，请切换到[布局模式](/help/sites-cloud/authoring/page-editor/responsive-layout.md)。

## 编辑组件继承 {#inherited-components}

继承是一种机制，通过该机制，可以链接内容，以便更改一个内容会自动更改另一个内容。 继承组件可能是多种情况的产物，包括：

* [多站点管理](/help/sites-cloud/administering/msm/overview.md)
* [启动项](/help/sites-cloud/authoring/launches/overview.md)

您可以取消并重新启用继承。 根据组件的不同，如果组件是Live Copy或启动项的一部分，则可以从组件工具栏中使用这些选项。

* **取消继承**

  ![“取消继承”按钮](assets/edit-content-cancel-inheritance.png)

* 如果继承已取消，则&#x200B;**重新启用继承**

  ![“重新启用继承”按钮](assets/edit-content-re-enable-inheritance.png)

* **转出**&#x200B;也在Blueprint或Live Copy源中可用

  ![“转出”按钮](assets/edit-content-rollout.png)
