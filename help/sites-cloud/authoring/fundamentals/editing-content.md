---
title: 编辑页面内容
description: 建立頁面後，您可以編輯內容以進行您所需的更新
exl-id: 8af0f621-14e8-4605-a51a-a3be21f19092
source-git-commit: 81d58f25af8b023774ce8653154597d92a7ac70b
workflow-type: tm+mt
source-wordcount: '3019'
ht-degree: 60%

---

# 编辑页面内容{#editing-page-content}

创建页面（新页面或者作为启动项或 Live Copy 的一部分）后，您可以编辑内容，以进行所需的更新。

內容新增方式： [元件](/help/sites-cloud/authoring/features/components-console.md) （適用於內容型別）可供拖曳至頁面上。 然后，可以就地编辑、移动或删除这些内容。

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

工具列提供許多選項的存取權。 根據您目前的內容和設定，某些選項可能無法使用。

* **切换侧面板**

   這會開啟/關閉側面板，側面板中會包含 [資產瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser)， [元件瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser)、和 [內容樹狀結構](/help/sites-cloud/authoring/fundamentals/environment-tools.md#content-tree).

   ![侧面板切换](/help/sites-cloud/authoring/assets/side-panel-toggle.png)

* **页面信息**

   提供對的存取 [頁面資訊](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information) 功能表，其中包含頁面詳細資訊以及可在頁面上採取的動作，包括檢視和編輯頁面資訊、檢視頁面屬性，以及發佈/取消發佈頁面。

   ![“页面信息”按钮](/help/sites-cloud/authoring/assets/page-information-icon.png)

* **模拟器**

   切換 [模擬器工具列](/help/sites-cloud/authoring/features/responsive-layout.md#selecting-a-device-to-emulate)，用來模擬頁面在其他裝置上的外觀。 這會在版面配置模式中自動切換。

   ![“模拟器”按钮](/help/sites-cloud/authoring/assets/emulator.png)

* **ContextHub**

   打开 [ContextHub](/help/sites-cloud/authoring/personalization/contexthub.md)。仅在预览模式下可用。

   ![ContextHub 按钮](/help/sites-cloud/authoring/assets/context-hub.png)

* **页面标题**

   這僅供參考。

   ![页面标题](/help/sites-cloud/authoring/assets/page-title.png)

* **模式選擇器**

   顯示目前的 [模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) 並可讓您選取其他模式，例如編輯、版面、時間扭曲或定位。

   ![“模式选择器”按钮](/help/sites-cloud/authoring/assets/mode-selector.png)

* **预览**

   啟用 [預覽模式](#preview-mode). 這會顯示發佈時所顯示的頁面。

   ![“预览”按钮](/help/sites-cloud/authoring/assets/preview.png)

* **批注**

   可讓您新增 [註解](/help/sites-cloud/authoring/fundamentals/annotations.md) 在檢閱頁面時跳至頁面。 第一個註解後，圖示會切換為數字，指出頁面上的註解數量。

   ![“注释”按钮](/help/sites-cloud/authoring/assets/annotations.png)

### 状态通知 {#status-notification}

如果页面是一个[工作流](/help/sites-cloud/authoring/workflows/overview.md)或多个工作流的一部分，则在编辑该页面时，将在屏幕顶部的通知栏中显示此信息。

![工作流通知](/help/sites-cloud/authoring/assets/editing-workflow-notification.png)

>[!NOTE]
>
>狀態列僅對具有適當許可權的使用者帳戶可見。

通知會列出針對頁面執行的工作流程。 如果使用者涉及目前的工作流程步驟，則選項 [影響工作流程狀態](/help/sites-cloud/authoring/workflows/participating.md) 並取得更多工作流程的相關資訊，例如：

* **完成** - 打开&#x200B;**完成工作项目**&#x200B;对话框
* **委派** - 打开&#x200B;**完成工作项目**&#x200B;对话框
* **查看详细信息** - 打开工作流的&#x200B;**详细信息**&#x200B;窗口

通过通知栏完成和委派工作流步骤，与从“通知”收件箱中[参与工作流](/help/sites-cloud/authoring/workflows/participating.md)的操作方式相同。

如果页面从属于多个工作流，则在通知的右侧端将显示工作流的数量，并且还提供有箭头按钮以允许您滚动浏览工作流。

![多个工作流通知](/help/sites-cloud/authoring/assets/editing-workflow-notification-multiple.png)

## 组件占位符 {#component-placeholder}

元件預留位置是一個指示器，可顯示將元件拖曳至目前暫留的元件上方時元件的放置位置。

* 將新元件新增至頁面時（從元件瀏覽器拖曳）：

   ![向页面添加新组件时的占位符](/help/sites-cloud/authoring/assets/editing-component-placeholder.png)

* 移动现有组件时：

   ![在页面上移动现有组件时的占位符](/help/sites-cloud/authoring/assets/editing-component-placeholder-existing.png)

## 插入组件 {#inserting-a-component}

### 使用组件浏览器插入组件 {#inserting-a-component-from-the-components-browser}

您可以使用[组件浏览器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser)添加新组件。[组件占位符](#component-placeholder)显示组件在放置时将占据的位置：

1. 确保页面处于&#x200B;[**编辑**&#x200B;模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)。
1. 打开[组件浏览器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser)。
1. 将所需的组件拖动到[所需位置](#component-placeholder)。
1. [編輯](#edit-content) 元件。

>[!NOTE]
>
>在行動裝置上，元件瀏覽器會填滿整個畫面。 開始拖曳元件後，瀏覽器將關閉並再次顯示頁面，以便您放置元件。

### 使用段落系统插入组件 {#inserting-a-component-from-the-paragraph-system}

您可以使用段落系统的&#x200B;**将组件拖动到此处**&#x200B;框添加新组件：

1. 确保页面处于&#x200B;[**编辑**&#x200B;模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)。
1. 有兩種方式可以從段落系統選取和新增元件：

   * 選取 **插入元件** 選項(+)(位於現有元件的工具列或 **將元件拖曳到這裡** 方塊。

      ![插入组件](/help/sites-cloud/authoring/assets/editing-insert-component.png)

   * 如果您使用的是桌面设备，则可以双击&#x200B;**将组件拖动到此处**&#x200B;框。

   * **插入新组件**&#x200B;对话框将打开以允许您选择需要的组件：

      ![“插入新组件”对话框](/help/sites-cloud/authoring/assets/editing-insert-component-selection.png)

1. 選取的元件將新增至頁面底部。 [編輯](#edit-content) 元件視需要。

### 使用「資產瀏覽器」插入元件 {#inserting-a-component-using-the-assets-browser}

您也可以從以下位置拖曳資產，將新元件新增至頁面： [資產瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser). 這會自動建立適當型別的新元件（並包含資產）。

可针对您的安装配置此行为。有关更多详细信息，请参阅配置段落系统以便可通过拖动资产创建组件实例。<!--This behavior can be configured for your installation. See [Configuring a Paragraph System so that Dragging an Asset Creates a Component Instance](/help/sites-developing/developing-components.md#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance) for further details.-->

要通过拖动以上某一资产类型创建组件，请执行以下操作：

1. 确保页面处于&#x200B;[**编辑**&#x200B;模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)。
1. 開啟 [資產瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser).
1. 將所需資產拖曳至所需位置。 此 [元件預留位置](#component-placeholder) 顯示元件將放置的位置。

   將在所需位置建立適合資產型別的元件 — 它將包含所選資產。

1. [編輯](#edit-content) 元件（若有需要）。

>[!NOTE]
>
>在行動裝置上，資產瀏覽器會填滿整個畫面。 開始拖曳資產後，瀏覽器將關閉並重新顯示頁面，以便您放置資產。

如果您在瀏覽資產時發現需要對資產進行快速變更，可以開始 [資產編輯器](/help/assets/manage-digital-assets.md) 直接從瀏覽器按一下資產名稱旁的編輯圖示。

![资产编辑按钮](/help/sites-cloud/authoring/assets/asset-edit-button.png)

## 组件工具栏 {#component-toolbar}

选择组件后将打开工具栏。通过工具栏可访问能够对组件执行的各种不同操作。

用户实际可用的操作将会根据相应的情况来显示，此处并未介绍所有这些操作。

![组件工具栏](/help/sites-cloud/authoring/assets/editing-component-toolbar.png)

* **编辑**

   [根据组件类型](/help/sites-cloud/authoring/fundamentals/components.md)，此操作将允许您[编辑组件的内容](#edit-content)。通常会提供一个工具栏。

   ![编辑按钮](/help/sites-cloud/authoring/assets/editing-component-toolbar-edit.png)

* **配置**

   [根据组件类型](/help/sites-cloud/authoring/fundamentals/components.md)，此操作将允许您编辑和配置组件的属性。通常会打开一个对话框。

   ![“配置”按钮](/help/sites-cloud/authoring/assets/editing-component-toolbar-configure.png)

* **复制**

   這會將元件複製到剪貼簿。 貼上動作後，原始元件將保留。

   ![“复制”按钮](/help/sites-cloud/authoring/assets/editing-component-toolbar-copy.png)

* **剪切**

   這會將元件複製到剪貼簿。 貼上動作後，原始元件將被移除。

   ![“剪切”按钮](/help/sites-cloud/authoring/assets/editing-component-toolbar-cut.png)

* **删除**

   這將會從含有您確認的頁面中刪除元件。

   ![“删除”按钮](/help/sites-cloud/authoring/assets/editing-component-toolbar-delete.png)

* **插入组件**

   這將開啟對話方塊，以 [新增元件](/help/sites-cloud/authoring/fundamentals/editing-content.md#inserting-a-component-from-the-paragraph-system).

   ![“插入”按钮](/help/sites-cloud/authoring/assets/editing-component-toolbar-insert.png)

* **粘贴**

   這會將元件從剪貼簿貼到頁面上。 原始物件是否保留，取決於您是使用複製還是切削。

   * 您可以貼到相同頁面或不同頁面。
   * 貼上的專案將會貼在您選取貼上動作的專案上方。
   * 唯有剪貼簿上有內容時，才會顯示「貼上」動作。

   ![“粘贴”按钮](/help/sites-cloud/authoring/assets/editing-component-toolbar-paste.png)

   >[!NOTE]
   >
   >如果您在剪下/復製作業之前貼到已開啟的其他頁面，則必須重新整理頁面以檢視貼上的內容。

* **组**

   這可讓您一次選取多個元件。 桌上型電腦裝置也可以透過以下步驟達到相同目的： **Control+按一下** 或 **Command+按一下**.

   ![“组”按钮](/help/sites-cloud/authoring/assets/editing-component-toolbar-group.png)

* **父项**

   此项允许您选择选定组件的父组件。

   ![“父项”按钮](/help/sites-cloud/authoring/assets/editing-component-toolbar-parent.png)

* **布局**

   這可讓您修改 [版面](/help/sites-cloud/authoring/fundamentals/editing-content.md#edit-component-layout) 所選元件的ID。 這僅適用於選取的元件，不會啟動 [版面模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) 整個頁面。

   ![“布局”按钮](/help/sites-cloud/authoring/assets/editing-component-toolbar-layout.png)

* **转换为体验片段变体**

   允许您从选定的组件创建一个新的[体验片段](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)，或将其添加到现有的体验片段中。

   ![“转换为体验片段”按钮](/help/sites-cloud/authoring/assets/editing-component-toolbar-xf.png)

## 编辑内容 {#edit-content}

有两种方法可以在组件中添加和/或编辑内容：

* 開啟 [用於編輯的元件對話方塊](#component-edit-dialog).
* [拖放資產](#drag-and-drop-assets-into-component) 從「資產」瀏覽器直接新增內容。

### 元件編輯對話方塊 {#component-edit-dialog}

您可以打开组件以使用组件工具栏 [的编辑（铅笔）图标编辑内容](#component-toolbar)。

確切的編輯選項取決於元件。 針對某些元件 [所有動作僅可在全熒幕模式下使用](#edit-content-full-screen-mode). 例如：

* 文本组件

   ![文本组件的工具栏](/help/sites-cloud/authoring/assets/editing-text-component-toolbar.png)

* 图像组件

   ![图像组件的工具栏](/help/sites-cloud/authoring/assets/editing-image-component-toolbar.png)

   >[!NOTE]
   >
   >无法对空的图像组件执行编辑操作。
   >
   >您必须先将图像拖动或上传到组件，然后才能开始编辑。

* 影像元件 — 全熒幕

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

若要移動段落元件：

1. 使用點選並按住或點選並按住來選取要移動的段落。
1. 將段落拖曳到新位置。 AEM會指出段落可以存放的位置。 將其拖曳至所需位置。

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

1. 選取「配置」動作後：

   * 元件顯示的調整大小操作框。
   * 模擬器工具列會顯示在畫面頂端。
   * 元件工具列上會顯示「配置」動作，而非標準編輯動作。

   ![布局模式下的组件](/help/sites-cloud/authoring/assets/editing-layout-mode.png)

   此时，您便可以像在[布局模式](/help/sites-cloud/authoring/features/responsive-layout.md#defining-layouts-layout-mode)中一样修改组件布局。

1. 在进行必要的布局更改后，单击组件操作菜单中的&#x200B;**关闭**&#x200B;按钮以停止修改组件的布局。组件的工具栏会返回到其正常的编辑状态。

   ![页面组件的组件工具栏](/help/sites-cloud/authoring/assets/editing-layout-exit.png)

>[!TIP]
>
>“布局”操作仅限用于选定的组件。例如，如果您正在编辑一个组件的布局，然后又单击另一个组件，则将为新选择的组件显示标准编辑工具栏（而不是布局工具栏），而大小调整手柄以及模拟器工具栏将会消失。
>
>如果您需要編輯頁面的整體版面，並影響多個元件，請切換至 [版面模式](/help/sites-cloud/authoring/features/responsive-layout.md).

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

此 [即時副本狀態頁面模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) 可讓您快速概略瞭解即時副本狀態以及哪些元件是/不是繼承的：

* 綠色邊框：繼承
* 粉紅色邊框：繼承已取消

例如：

![显示的 Live Copy 状态示例](/help/sites-cloud/authoring/assets/editing-live-copy-status.png)

## 添加注释 {#adding-annotations}

[註解](/help/sites-cloud/authoring/fundamentals/annotations.md) 允許檢閱者和其他作者針對您的內容提供意見回饋。 它們通常用於審查和驗證目的。

## 預覽頁面 {#previewing-pages}

可通过以下两个选项预览页面：

* [预览模式](#preview-mode) - 快速就地预览
* [檢視已發佈](#view-as-published)  — 在新標籤中開啟頁面的完整預覽

>[!TIP]
>
>* 內容中的連結是可見的，但在編輯模式下無法存取。
>* 如果您希望使用链接进行导航，请使用任一预览选项。
>* 使用[键盘快捷键](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) `Ctrl-Shift-M` 可在预览和最后选择的模式之间切换。


>[!NOTE]
>
>这两个预览选项均可设置 WCM 模式 Cookie。

### 预览模式 {#preview-mode}

編輯內容時，您可以使用預覽功能來預覽頁面 [模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes). 此模式：

* 会隐藏各种编辑机制，以便让您快速查看页面在发布时是什么样子。
* 可讓您使用連結來導覽。
* 會 **not** 重新整理頁面內容。

製作時，可使用頁面編輯器右上角的圖示來使用預覽模式：

![“预览”按钮](/help/sites-cloud/authoring/assets/preview.png)

### 以发布的形式查看 {#view-as-published}

此 **檢視已發佈** 選項可從以下網址取得： [頁面資訊](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information) 功能表。 這會在新標籤中開啟頁面、重新整理內容，並完全依照頁面在發佈環境中的顯示方式顯示頁面。

## 锁定页面 {#locking-a-page}

AEM 允许您锁定页面，这样其他人就无法修改页面内容。当您要对某个特定页面做出大量编辑，或者需要冻结页面一段时间时，此功能非常有用。

可從下列任一位置鎖定頁面：

* **網站** 主控台

   1. 選取頁面，並選取 [選擇模式](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources).
   1. 選取鎖定圖示。

      ![“锁定”按钮](/help/sites-cloud/authoring/assets/lock.png)

* **页面编辑器**

   1. 選取 **頁面資訊** 圖示以開啟功能表。
   1. 選取 **鎖定頁面** 選項。

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

撤消和重做命令的行为与其他软件中的类似。在您对内容做出决策时，可使用这些命令恢复网页的最近状态。例如，如果您将文本段落移至页面上的其他位置，可以使用撤消命令移回该段落。如果您認為前一個位置較好，請使用重做指令「復原復原」。

例如，您可以：

* 只要您使用復原後尚未進行頁面編輯，就可以重做動作。
* 最多可復原20個編輯動作（預設設定）。
* 也使用 [鍵盤快速鍵](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) 「復原」和「重做」。

您可以對下列型別的頁面變更使用還原和重做：

* 新增、編輯、移除和移動段落
* 就地編輯段落內容
* 在頁面中複製、剪下和貼上專案

>[!NOTE]
>
>* 对文件和图像的更改执行撤消和重做操作需要特殊的权限。
>* 檔案和影像的變更歷史記錄至少會持續10小時。 然而，在這段時間之後，無法保證會復原變更。 您的管理員可以變更十小時的預設時間。
>* 系统管理员可以根据您实例的要求，配置撤消/重做功能的各个方面。
   <!--* Your system administrator can [configure various aspects of the Undo/Redo features](/help/sites-administering/config-undo.md) according to the requirements for your instance.-->

