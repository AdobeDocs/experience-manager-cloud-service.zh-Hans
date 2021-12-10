---
title: 如何使用布局模式调整自适应Forms的组件大小？
description: 使用布局模式中可用的响应式网格定义组件的位置。 了解如何访问布局模式、调整组件大小、调整面板大小、为面板定义多列布局、为旧响应式布局启用新的响应式网格，以及为具有旧响应式布局的表单禁用布局模式。
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: 53896a8e-4568-460b-bca7-994baea0c8eb
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1080'
ht-degree: 0%

---

# 使用布局模式调整组件大小 {#use-layout-mode-to-resize-components}

自适应表单创作界面允许您使用布局模式调整组件大小。 拖动列中的蓝色圆点，以定义用于放置组件的起点和终点。 点按响应式网格中的组件后，将显示蓝色圆点。 响应式网格由12个相等的列组成。 替代列中的白色和蓝色底纹将一列与另一列区分开。

您可以使用布局模式调整所有设备类型（如台式机、平板电脑、手机和其他较小设备）的组件大小。 平板电脑自动从桌面版本导出布局配置，而较小的设备从手机导出布局配置。 但是，您可以覆盖自动派生的配置，以便为每种设备类型定义不同的配置。

## 访问布局模式 {#access-layout-mode}

选择 **[!UICONTROL 布局]** 下拉列表(位于“自适应表单”创作界面的顶部，位于 **[!UICONTROL 预览]** 选项。 表单将在布局模式下显示。

1. 登录到 [!DNL Adobe Experience Manager] 创作实例，导航到 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**.
1. 创建新页面或打开现有页面 [自适应表单](creating-adaptive-form.md).
1. 选择 **[!UICONTROL 布局]** 的 **[!UICONTROL 预览]** 选项。 表单将在布局模式下显示。

   ![布局模式](assets/layout_mode_ic_new.png)

## 调整组件大小 {#resize-components}

1. 在布局模式下，点按组件以调整大小。 蓝色圆点显示在响应式网格的开始和结束处。
1. 拖放蓝色圆点以定义组件在响应式网格中的位置。

   ![使用布局模式调整大小](assets/layout_mode_resize_new_updated1.png)

   点按组件后显示的工具栏包含以下选项：

   * **[!UICONTROL 父项]**:选择组件的父项。
   * **[!UICONTROL 还原断点布局]**:撤消所有调整大小的更改，并将默认布局应用于组件。
   * **[!UICONTROL 浮动到新行]**:如果同一行中存在多个组件，请将组件移至下一行。

   您还可以使用 **[!UICONTROL 还原断点布局]** ( ![还原断点](assets/reverttopreviouslypublishedversion.png))选项来撤消所有调整大小的更改。

   >[!NOTE]
   >
   >无法使用布局模式调整表列、工具栏、工具栏按钮和目标区域组件的大小。 使用样式模式调整这些组件的大小。

### 示例 {#example}

**目标：** 要插入表组件和图像组件，并在自适应表单中将它们彼此平行放置。

1. 使用 [!UICONTROL 编辑] 模式。 图像组件在表组件之后显示。
1. 切换到 [!UICONTROL 布局] 模式并点按 [!UICONTROL 表] 组件。 用于调整组件大小的蓝色圆点显示在第1列和第12列。
1. 将响应式网格的第12列蓝色圆点拖到第6列。

   ![定义表的端点](assets/layout_mode_end_point_table_new.png)

1. 同样，选择 [!UICONTROL 图像] 组件，并将响应式网格的列1处的蓝色圆点拖到列7中。 表和图像组件彼此平行显示。

   ![在“布局”模式下并行的表和图像](assets/table_image_parallel_new.png)

   您可以选择图像组件，然后点按 **[!UICONTROL 浮动到新行]** 选项来将图像组件移至下一行。

## 调整面板大小 {#resize-panels-layout-mode}

如果要调整整个面板的大小而不是单个组件的大小，请执行以下步骤：

1. 点按面板中要调整大小的任何组件，选择 ![选择父项](assets/select_parent_icon.svg)，如果面板是组件的直接父组件，则在下拉列表中选择第一个选项。

   蓝色圆点显示在响应式网格的开始和结束处。

1. 拖放蓝色圆点以定义面板在响应式网格中的位置。
您可以重复步骤1和2，然后选择 ![选择父项](assets/float_to_new_line_icon.svg) 将调整大小的面板移到下一行。

## 为面板定义多列布局

执行以下步骤以定义面板的列数：

1. 在 **[!UICONTROL 编辑]** 模式，点按面板，选择 ![配置](assets/configure-icon.svg)，然后选择 **[!UICONTROL 响应 — 页面上的所有内容（无需导航）]** 选项 **[!UICONTROL 面板布局]** 下拉列表。

1. 点按 ![保存](assets/save_icon.svg) 以保存属性。

1. 在 **[!UICONTROL 布局]** 模式，点按面板中的任意组件，选择 ![选择父项](assets/select_parent_icon.svg)，然后选择面板。

1. 点按 ![多列](assets/multi-column.svg) ，然后从下拉列表中选择列数。 列数可以介于1到12之间。 该面板将分为多列布局。

![布局模式中的多列](assets/multi-column-layout.png)

## 为旧的响应式布局启用新的响应式网格 {#enableresponsivegrid}

为使用创建的表单启用新的响应式网格 [!DNL Adobe Experience Manager] Forms 6.4或更低版本，可调整组件大小。

>[!NOTE]
>
>切换到新的响应式网格会丢弃已为表单中使用的组件定义的布局属性。

执行以下步骤以启用新的响应式网格：

1. 选择 **[!UICONTROL 布局]** 的 **[!UICONTROL 预览]** 选项。 此时会显示一条确认消息，用于启用“布局”模式。
1. 点按 **[!UICONTROL 是]** 启用 **[!UICONTROL 布局]** 模式。

### 使用新的响应式布局在自适应表单中嵌入旧片段 {#embed-an-old-fragment-in-an-adaptive-form-with-new-responsive-layout}

自适应表单的新响应式布局允许您向表单添加具有旧响应式布局的自适应表单片段。 但是，新布局会丢弃已为片段中使用的组件定义的布局属性。 您可以切换到布局模式，以定义片段中使用的组件的布局属性。

### 在旧的自适应表单中嵌入具有新响应式布局的片段 {#embed-a-fragment-with-new-responsive-layout-in-an-old-adaptive-form}

如果您在具有旧响应式布局的自适应表单中嵌入了具有新响应式布局的片段，则系统会提示您为表单启用布局模式并重新嵌入该片段。

要启用布局模式，请选择 **[!UICONTROL 布局]** 的 **[!UICONTROL 预览]** 选项，点按 **[!UICONTROL 是]** 确认。 选择 **[!UICONTROL 编辑]** 模式重新嵌入片段。

## 对于具有旧响应式布局的表单，禁用布局模式 {#disable-layout-mode-for-forms-with-old-responsive-layout}

您可以通过编辑表单中所用模板的属性，来禁用具有旧响应式布局的表单的布局模式。

执行以下步骤以禁用布局模式：

1. 选择 **[!UICONTROL 工具]** > **[!UICONTROL 常规]** > **[!UICONTROL 模板]** 并在 **[!UICONTROL 编辑]** 模式。
1. 在左窗格中选择表单容器，然后点按 **[!UICONTROL 策略。]**

   ![禁用布局模式](assets/policy_disable_layout_mode.png)

1. 点按 **[!UICONTROL 布局设置]** 选项卡，选择 **[!UICONTROL 禁用布局模式]**.
1. 点按 ![保存更改](assets/save_icon.svg) 以保存模板属性。
