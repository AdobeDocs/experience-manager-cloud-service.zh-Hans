---
title: 页面创作快速入门指南
description: 这是一个概要性快速指南，可帮助您开始创作页面内容
exl-id: d37c9b61-7382-4bf6-8b90-59726b871264
source-git-commit: 43fe6bdc8534cdc6c9d1b8afee90c647c447bfe1
workflow-type: tm+mt
source-wordcount: '1585'
ht-degree: 100%

---

# 页面创作快速入门指南 {#quick-guide-to-authoring-pages}

本文档旨在作为 AEM 中关键页面创作操作的概要性快速入门指南。本文档：

* 并不提供全面的介绍。
* 但提供了详细文档的链接。

有关使用 AEM 进行创作的完整详细信息，请参阅：

* [创作概念](/help/sites-cloud/authoring/getting-started/concepts.md)
* [基本操作](/help/sites-cloud/authoring/getting-started/basic-handling.md)

## 一些快速提示 {#a-few-quick-hints}

在开始使用快速入门指南之前，请查看下面列出的一些常规提示，您应牢记这些提示，并根据创作系统的各个区域分别使用它们。

### 在“站点”控制台中 {#sites-console}

* 创建按钮

   * 此按钮在许多控制台中可用 - 出现的选项是上下文相关的，因此在不同的情况下可能有所改变。

* 重新排序页面

   * 此操作可在[列表视图](/help/sites-cloud/authoring/getting-started/basic-handling.md#list-view)中完成。更改将在其他视图中应用并可见。

### 页面创作 {#page-authoring}

* 导航链接

   * 当您处于&#x200B;**编辑**&#x200B;模式下时，**链接不可用于导航**。要通过链接导航，您需要使用以下任一方式来[预览页面](/help/sites-cloud/authoring/fundamentals/editing-content.md#previewing-pages)：

      * [预览模式](/help/sites-cloud/authoring/fundamentals/editing-content.md#preview-mode)
      * [以发布的形式查看](/help/sites-cloud/authoring/fundamentals/editing-content.md#view-as-published)

* 无法从页面编辑器启动/创建版本。现在，可以从&#x200B;**站点**&#x200B;控制台完成（通过对所选资源选择&#x200B;**创建**&#x200B;或[时间线](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)）。

>[!NOTE]
>
>有许多键盘快捷键可帮助您更轻松地创作体验。
>
>* [编辑页面时的键盘快捷键](/help/sites-cloud/authoring/fundamentals/keyboard-shortcuts.md)
>* [控制台的键盘快捷键](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)


### 查找页面 {#finding-your-page}

查找页面时存在很多方面；您可以导航和/或搜索：

1. 打开&#x200B;**站点**&#x200B;控制台（使用&#x200B;**全局导航**&#x200B;中的[站点](/help/sites-cloud/authoring/getting-started/basic-handling.md#global-navigation)选项 - 它将在您选择 Adobe Experience Manager（左上方）时以下拉菜单的形式触发）。

1. 通过点按/单击相应的页面，在树中向下导航。页面资源的显示方式取决于您所使用的视图 - [卡片视图、列表视图或列视图](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)：

   ![查看选择下拉列表](/help/sites-cloud/authoring/assets/views.png)

1. 使用[标头中的痕迹导航](/help/sites-cloud/authoring/getting-started/basic-handling.md#the-header)对树进行向上导航，这允许您返回到选定的位置：

   ![痕迹导航下拉列表](/help/sites-cloud/authoring/assets/breadcrumb.png)

1. 您还可以[搜索](/help/sites-cloud/authoring/getting-started/search.md)页面。您可以从所显示的结果中选择页面。

   ![搜索字段](/help/sites-cloud/authoring/assets/search.png)

### 创建新页面 {#creating-a-new-page}

要[创建新的页面](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page)，请执行以下操作：

1. [导航到要创建新页面的位置](#finding-your-page)。
1. 使用&#x200B;**创建**&#x200B;图标，然后从列表中选择&#x200B;**页面**：

   ![“创建”按钮](/help/sites-cloud/authoring/assets/create.png)

1. 这将打开向导，逐步指导您收集[创建新页面](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page)时所需的信息。按照屏幕上的说明操作。

### 选择页面以执行其他操作 {#selecting-your-page-for-further-action}

您可以选择一个页面，以对其执行操作。选择页面后，工具栏将自动更新，以显示与该资源相关的操作。

选择页面的方式取决于您在控制台中所使用的视图：

1. 列视图：

   * 点按/单击所需资源的缩略图 - 缩略图上将覆盖一个勾号，表示已选择该页面。

1. 列表视图：

   * 点按/单击所需资源的缩略图 - 缩略图上将覆盖一个勾号，表示已选择该页面。

1. 卡片视图：

   * 通过[选择所需的资源](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)进入选择模式。具体操作方式取决于您的设备：

      * 在移动设备上：点按并按住卡片
      * 在桌面设备上：使用勾号图标表示的[快速操作](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)：
   * 卡片上将覆盖一个勾号，表示已选择该页面。

   ![示例卡片](/help/sites-cloud/authoring/assets/card.png)

### 快速操作（仅限卡片视图/桌面） {#quick-actions-card-view-desktop-only}

[快速操作](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)可用：

1. [导航](#finding-your-page)到要执行操作的页面。
1. 将鼠标指针悬停在代表所需资源的卡片上方。将会显示快速操作：

   ![卡片操作](/help/sites-cloud/authoring/assets/card-actions.png)

### 编辑页面内容 {#editing-your-page-content}

要编辑您的页面，请执行以下操作：

1. [导航](#finding-your-page)到要编辑的页面。
1. 使用“编辑”（铅笔）图标[打开要编辑的页面](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#opening-a-page-for-editing)：

   ![编辑按钮](/help/sites-cloud/authoring/assets/edit.png)

   可以从以下位置访问该图标：

   * 所需资源的[快速操作（仅限卡片视图/桌面）](#quick-actions-card-view-desktop-only)。
   * [选择页面](#selecting-your-page-for-further-action)后显示的工具栏。

1. 编辑器打开后，您可以：

   * 通过以下方式[向页面中添加新组件](/help/sites-cloud/authoring/fundamentals/editing-content.md#inserting-a-component)：

      * 打开侧面板
      * 选择组件选项卡（[组件浏览器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser)）
      * 将所需组件拖放到页面中。

      可以通过以下图标打开（或关闭）侧面板：

      ![侧面板切换按钮](/help/sites-cloud/authoring/assets/side-panel-toggle.png)

   * [编辑页面中现有组件的内容](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar)：

      * 通过点按或单击打开组件工具栏。使用&#x200B;**编辑**（铅笔）图标打开对话框。
      * 通过点按住或慢速双击打开组件的就地编辑器。此时将显示可用的操作（对于某些组件，该选择将受到限制）。
      * 要查看所有可用的操作，请使用以下图标进入全屏模式：

         ![全屏按钮](/help/sites-cloud/authoring/assets/full-screen.png)
   * [配置现有组件的属性](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-edit-dialog)

      * 通过点按或单击打开组件工具栏。使用&#x200B;**配置**（扳手）图标打开对话框。
   * 通过以下任一方式[移动组件](/help/sites-cloud/authoring/fundamentals/editing-content.md#moving-a-component)：

      * 将所需组件拖动到新位置。
      * 通过点按或单击打开组件工具栏。根据需要依次使用&#x200B;**剪切**&#x200B;和&#x200B;**粘贴**&#x200B;图标。
   * [复制（并粘贴）](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar)组件：

      * 通过点按或单击打开组件工具栏。根据需要依次使用&#x200B;**复制**&#x200B;和&#x200B;**粘贴**&#x200B;图标。
   >[!NOTE]
   >
   >您可以将组件&#x200B;**粘贴**&#x200B;到同一页面或其他页面。如果在剪切/复制操作之前粘贴到已打开的其他页面，则表明该页面需要刷新。

   * [删除](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar)组件：

      * 通过点按或单击打开组件工具栏，然后使用&#x200B;**删除**&#x200B;图标。
   * 向页面[添加注释](/help/sites-cloud/authoring/fundamentals/annotations.md#annotations)：

      * 选择&#x200B;**注释**&#x200B;模式（对话气泡图标）。使用&#x200B;**添加注释**（加号）图标添加注释。使用右上方的 X 退出注释模式。

         ![“注释”按钮](/help/sites-cloud/authoring/assets/annotations.png)
   * [预览页面](/help/sites-cloud/authoring/fundamentals/editing-content.md#preview-mode)（用于查看页面在发布环境中的显示情况）

      * 从工具栏中选择&#x200B;**预览**。
   * 使用&#x200B;**编辑**&#x200B;下拉选择器返回编辑模式（或选择其他模式）。

   >[!NOTE]
   >
   >要使用内容中的链接导航，您必须使用[预览模式](/help/sites-cloud/authoring/fundamentals/editing-content.md#preview-mode)。

### 编辑页面属性 {#editing-the-page-properties}

[编辑页面属性](/help/sites-cloud/authoring/fundamentals/page-properties.md)的方法（主要）有两种：

* 从&#x200B;**站点**&#x200B;控制台中：

   1. [导航](#finding-your-page)到要发布的页面。
   1. 从以下任一位置选择&#x200B;**属性**&#x200B;图标：

      * 所需资源的[快速操作（仅限卡片视图/桌面）](#quick-actions-card-view-desktop-only)。
      * [选择页面](#selecting-your-page-for-further-action)后显示的工具栏。

      ![“属性”按钮](/help/sites-cloud/authoring/assets/properties.png)

   1. 将会显示页面属性。您可以进行需要的更新，然后使用“保存”保留这些更改


* 在[编辑页面](#editing-your-page-content)时：

   1. 打开&#x200B;**页面信息**&#x200B;菜单。
   1. 选择&#x200B;**打开属性**&#x200B;以打开用于编辑属性的对话框。

      ![“页面信息”按钮](/help/sites-cloud/authoring/assets/page-information.png)

### 发布页面（或取消发布） {#publishing-your-page-or-unpublishing}

[发布页面](/help/sites-cloud/authoring/fundamentals/publishing-pages.md)（和取消发布）的方法主要有两种：

* 从&#x200B;**站点**&#x200B;控制台中：

   1. [导航](#finding-your-page)到要发布的页面。
   1. 从以下任一位置选择&#x200B;**快速发布**&#x200B;图标：

      * 所需资源的[快速操作（仅限卡片视图/桌面）](#quick-actions-card-view-desktop-only)。
      * [选择页面](#selecting-your-page-for-further-action)后显示的工具栏（还可以访问[稍后发布](/help/sites-cloud/authoring/fundamentals/publishing-pages.md)）。

      ![“快速发布”按钮](/help/sites-cloud/authoring/assets/quick-publish.png)


* 在[编辑页面](#editing-your-page-content)时：

   1. 打开&#x200B;**页面信息**&#x200B;菜单。
   1. 选择&#x200B;**发布页面**。

* 从控制台取消发布页面只能通过&#x200B;**管理发布**&#x200B;选项完成，该选项仅在工具栏上可用（不能通过快速操作）。

   ![“管理发布”按钮](/help/sites-cloud/authoring/assets/manage-publication.png)

   **取消发布页面**&#x200B;选项仍可通过编辑器中的&#x200B;**页面信息**&#x200B;菜单使用。

   请参阅[发布页面](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#unpublishing-pages)以了解更多信息。

### 移动、复制并粘贴或删除页面 {#move-copy-and-paste-or-delete-your-page}

这些操作全部可以通过以下项触发：

1. [导航](#finding-your-page)到要移动、复制并粘贴或删除的页面。
1. 使用以下任一方式根据需要选择复制（然后粘贴）、移动或删除图标：

   * 所需资源的[快速操作（仅限卡片视图/桌面）](#quick-actions-card-view-desktop-only)。
   * [选择页面](#selecting-your-page-for-further-action)后显示的工具栏。

   然后，取决于您的操作：

   * [复制](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#copying-and-pasting-a-page):

      * 复制后，您将需要导航到新位置并进行粘贴。
   * [移动](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#moving-or-renaming-a-page):

      * 将打开相应的向导来收集移动页面时所需的信息。按照屏幕上的说明操作。
   * [删除](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#deleting-a-page):

      * 系统将要求您确认该操作。
   >[!NOTE]
   >
   >快速操作中并未提供“删除”操作。

### 锁定页面（然后解锁） {#locking-your-page-then-unlocking}

[锁定页面](/help/sites-cloud/authoring/fundamentals/editing-content.md#locking-a-page) ，可阻止其他作者在您处理页面时对其进行处理。 可以找到“锁定”（和“解锁”）图标／按钮：

* [选择页面](#selecting-your-page-for-further-action)后显示的工具栏。
* 编辑页面时显示的[“页面信息”下拉菜单](#editing-the-page-properties)。
* 编辑页面（页面处于锁定状态）时显示的页面工具栏

例如，“锁定”图标如下所示：

![“锁定”按钮](/help/sites-cloud/authoring/assets/lock.png)

### 访问页面引用 {#accessing-page-references}

在“引用”边栏中，可以[快速访问对页面的引用/从页面进行的引用](/help/sites-cloud/authoring/fundamentals/environment-tools.md#references)。

1. 使用工具栏图标选择&#x200B;**引用**（在[选择您的页面](#selecting-your-page-for-further-action)之前或之后）：

   ![引用视图选项](/help/sites-cloud/authoring/assets/references.png)

   此时会显示引用类型列表：

   ![引用视图](/help/sites-cloud/authoring/assets/references-list.png)

1. 点按/单击所需的引用类型，以显示更多详细信息并（视需要）执行进一步操作。

### 创建页面版本 {#creating-a-version-of-your-page}

要创建页面的[版本](/help/sites-cloud/authoring/features/page-versions.md)：

1. 要打开“时间线”边栏，请使用工具栏图标选择&#x200B;**[时间线](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)**（在[选择您的页面](#selecting-your-page-for-further-action)之前或之后）：

   ![时间线视图选项](/help/sites-cloud/authoring/assets/timeline.png)

1. 点按/单击“时间线”列右下方的省略号以显示其他按钮，包括&#x200B;**另存为版本**。

   ![时间线视图](/help/sites-cloud/authoring/assets/timeline-view.png)

1. 选择&#x200B;**另存为版本**，然后再选择&#x200B;**创建**。

### 恢复/比较页面版本 {#restoring-comparing-a-version-of-your-page}

恢复和/或比较页面版本时所使用的机制基本相同：

1. 使用工具栏图标选择&#x200B;**[时间线](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)**（在[选择您的页面](#selecting-your-page-for-further-action)之前或之后）：

   ![时间线视图选项](/help/sites-cloud/authoring/assets/timeline.png)

   如果页面的某个版本已经保存，则会在“时间线”中列出该版本。

1. 点按/单击要恢复的版本 - 这将显示其他操作按钮：

   * **恢复到此版本**

      * 将恢复该版本。
   * **显示差异**

      * 将打开该页面，并突出显示（两个版本之间的）差异。
