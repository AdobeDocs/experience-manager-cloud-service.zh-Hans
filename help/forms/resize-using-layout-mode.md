---
title: 如何使用布局模式调整自适应表单组件的大小？
description: 定义AEM Forms组件的位置，了解如何访问布局模式、调整组件大小、调整面板大小以及定义面板的多列布局。
role: User, Developer
level: Intermediate
feature: Adaptive Forms, Foundation Components
exl-id: 53896a8e-4568-460b-bca7-994baea0c8eb
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '1138'
ht-degree: 2%

---

# 使用布局模式调整自适应Forms的组件大小 {#use-layout-mode-to-resize-components}

>[!NOTE]
>
> Adobe建议为[创建新的自适应Forms](/help/forms/creating-adaptive-form-core-components.md)或[将自适应Forms添加到AEM Sites页面](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)使用现代的、可扩展的数据捕获[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)。 这些组件代表有关创建自适应表单的重大改进，确保实现令人印象深刻的用户体验。本文介绍了使用基础组件创作自适应Forms的旧方法。

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/resize-using-layout-mode.html) |
| AEM as a Cloud Service | 本文 |

通过自适应表单创作界面，您可以使用布局模式调整组件大小。 拖动列中的蓝色圆点以定义起点和终点来定位组件。 点按响应式网格中的组件后，会显示蓝点。 响应式网格由12个相等的列组成。 备用列中的白色和蓝色阴影将一列与另一列区分开来。

您可以使用布局模式为所有设备类型（如台式机、平板电脑、手机和其他小型设备）调整组件大小。 平板电脑会自动从台式机版本获取布局配置，较小的设备则从手机获取布局配置。 但是，您可以覆盖自动派生的配置以针对每种设备类型定义不同的配置。

## 访问布局模式 {#access-layout-mode}

从自适应表单创作界面顶部出现在&#x200B;**[!UICONTROL 预览]**&#x200B;选项旁边的下拉列表中选择&#x200B;**[!UICONTROL 布局]**。 该表单将以布局模式显示。

1. 登录到[!DNL Adobe Experience Manager]创作实例并导航到&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**。
1. 创建新或打开现有的[自适应表单](creating-adaptive-form.md)。
1. 从&#x200B;**[!UICONTROL 预览]**&#x200B;选项旁边顶部显示的下拉列表中选择&#x200B;**[!UICONTROL 布局]**。 该表单将以布局模式显示。

   ![布局模式](assets/layout_mode_ic_new.png)

## 调整组件大小 {#resize-components}

1. 在布局模式下，选择要调整大小的组件。 蓝点显示在响应式网格的开头和结尾。
1. 拖放蓝点以定义组件在响应式网格中的位置。

   ![使用布局模式调整大小](assets/layout_mode_resize_new_updated1.png)

   点按组件后显示的工具栏包含以下选项：

   * **[!UICONTROL 父项]**：选择组件的父项。
   * **[!UICONTROL 还原断点布局]**：撤消所有调整大小的更改，并将默认布局应用于组件。
   * **[!UICONTROL 浮动到新行]**：如果同一行中有多个组件，则将组件移动到下一行。

   您还可以在面板级别使用&#x200B;**[!UICONTROL 还原断点布局]** （![还原断点](assets/reverttopreviouslypublishedversion.png)）选项来撤消所有调整大小的更改。

   >[!NOTE]
   >
   >无法使用布局模式调整表格列、工具栏、工具栏按钮和目标区域组件的大小。 使用样式模式调整这些组件的大小。

### 示例 {#example}

**目标：**&#x200B;要插入表组件和图像组件，并在自适应表单中将其相互平行放置。

1. 在自适应表单中使用[!UICONTROL 编辑]模式插入表和图像组件。 图像组件显示在表组件之后。
1. 切换到[!UICONTROL 布局]模式并选择[!UICONTROL 表]组件。 用于调整组件大小的蓝点显示在列1和12。
1. 将响应式网格第12列中的蓝色圆点拖到第6列。

   ![定义表的终结点](assets/layout_mode_end_point_table_new.png)

1. 同样，选择[!UICONTROL Image]组件并将响应式网格第1列中的蓝色圆点拖到第7列。 表格和图像组件彼此平行显示。

   在布局模式下并行![表和图像](assets/table_image_parallel_new.png)

   您可以选择图像组件，然后选择工具栏中可用的&#x200B;**[!UICONTROL 浮动到新行]**&#x200B;选项以将图像组件移动到下一行。

## 调整面板大小 {#resize-panels-layout-mode}

如果要调整整个面板而非单个组件的大小，请执行以下步骤：

1. 选择面板中要调整大小的任何组件，选择![选择父项](assets/select_parent_icon.svg)，然后选择下拉列表中的第一个选项（如果该面板是组件的直接父项）。

   蓝点显示在响应式网格的开头和结尾。

1. 拖放蓝点以定义面板在响应式网格中的位置。
您可以重复步骤1和2，然后选择![选择父项](assets/float_to_new_line_icon.svg)以将调整大小的面板移至下一行。

## 定义面板的多列布局

执行以下步骤可定义面板的列数：

1. 在&#x200B;**[!UICONTROL 编辑]**&#x200B;模式下，选择面板，选择![配置](assets/configure-icon.svg)，然后从&#x200B;**[!UICONTROL 面板布局]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL 响应式 — 页面上的所有内容（不含导航）]**&#x200B;选项。

1. 选择![保存](assets/save_icon.svg)以保存属性。

1. 在&#x200B;**[!UICONTROL 布局]**&#x200B;模式下，选择面板中的任何组件，选择![选择父项](assets/select_parent_icon.svg)，然后选择面板。

1. 选择![多列](assets/multi-column.svg)并从下拉列表中选择列数。 列数可在1到12之间。 面板被分为多列布局。

![布局模式下的多列](assets/multi-column-layout.png)

## 为旧响应布局启用新响应网格 {#enableresponsivegrid}

为您使用[!DNL Adobe Experience Manager] Forms 6.4或更低版本创建的表单启用新响应式网格，以调整组件大小。

>[!NOTE]
>
>切换到新的响应式网格会丢弃已为表单中使用的组件定义的布局属性。

执行以下步骤以启用新响应式网格：

1. 从&#x200B;**[!UICONTROL 预览]**&#x200B;选项旁边顶部显示的下拉列表中选择&#x200B;**[!UICONTROL 布局]**。 显示启用布局模式的确认。
1. 选择&#x200B;**[!UICONTROL 是]**&#x200B;为表单启用&#x200B;**[!UICONTROL 布局]**&#x200B;模式。

### 使用新响应布局在自适应表单中嵌入旧片段 {#embed-an-old-fragment-in-an-adaptive-form-with-new-responsive-layout}

新的自适应表单响应布局允许您向表单添加具有旧响应布局的自适应表单片段。 但是，新布局会丢弃为片段中使用的组件定义的布局属性。 您可以切换到布局模式以定义片段中使用的组件的布局属性。

### 在旧自适应表单中嵌入具有新响应布局的片段 {#embed-a-fragment-with-new-responsive-layout-in-an-old-adaptive-form}

如果在具有旧响应布局的自适应表单中嵌入具有新响应布局的片段，则系统会提示您启用表单的布局模式并重新嵌入片段。

要启用“布局”模式，请从&#x200B;**[!UICONTROL 预览]**&#x200B;选项顶部出现的下拉列表中选择&#x200B;**[!UICONTROL 布局]**，并选择&#x200B;**[!UICONTROL 是]**&#x200B;进行确认。 选择&#x200B;**[!UICONTROL 编辑]**&#x200B;模式以重新嵌入片段。

## 对具有旧响应布局的表单禁用布局模式 {#disable-layout-mode-for-forms-with-old-responsive-layout}

您可以通过编辑表单中使用的模板的属性来禁用具有旧响应布局的表单的布局模式。

执行以下步骤可禁用布局模式：

1. 选择&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 常规]** > **[!UICONTROL 模板]**，并在&#x200B;**[!UICONTROL 编辑]**&#x200B;模式下打开表单中使用的模板。
1. 在左窗格中选择表单容器，然后选择&#x200B;**[!UICONTROL 策略]**。

   ![禁用布局模式](assets/policy_disable_layout_mode.png)

1. 选择&#x200B;**[!UICONTROL 布局设置]**&#x200B;选项卡，然后选择&#x200B;**[!UICONTROL 禁用布局模式]**。
1. 选择![保存更改](assets/save_icon.svg)以保存模板属性。

## 另请参阅 {#see-also}

{{see-also}}