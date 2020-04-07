---
title: 管理数字资产集合
description: 了解Adobe Experience Manager资产中的集合概念。 了解如何与其他用户一起收藏、管理、编辑和收藏集。
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 26833f59f21efa4de33969b7ae2e782fe5db8a14

---


# 管理收藏集 {#manage-collections}

集合是Adobe Experience Manager资产中的一组资产。 使用收藏集可在用户之间共享资产。该集合可以是静态集合或基于搜索结果的动态集合。

与文件夹不同，收藏集可以包含来自不同位置的资产。 您可以与分配了不同权限级别（包括查看、编辑等）的不同用户共享集合。

您可以与一个用户共享多个收藏集。每个收藏集都包含对资产的引用。收藏集中会保持资产的引用完整性。

根据资产的整理方式，收藏集有以下类型：

* 包含资产、文件夹和其他集合的静态引用列表的集合。

* 基于搜索条件动态包含资产的智能收藏集。

## 访问收藏集控制台 {#navigate-the-collections-console}

要打开“收藏集”控 **[!UICONTROL 制台]** ，请执行以下操作：

要打开收藏 **[!UICONTROL 集]**，请点按或单击Experience Manager徽标。 From the navigation page, go to **[!UICONTROL Assets]** > **[!UICONTROL Collections]**.

## 创建集合 {#create-a-collection}

You can create a collection either with [static references](#create-a-collection-with-static-references) or based on a [search criteria-based filter](#create-a-smart-collection). 您还可以从Lightbox创建收藏集。

### Create a collection with static references {#create-a-collection-with-static-references}

您可以创建包含静态引用的收藏集，例如包含对资产、文件夹、收藏集、旋转集和图像集的引用的收藏集。

1. 导航到&#x200B;**[!UICONTROL 收藏集]**&#x200B;控制台。
1. 在工具栏中，点按／单击 **[!UICONTROL 创建]**。
1. In the **[!UICONTROL Create Collection]** page, enter a title and an optional description for the collection.
1. 向收藏集添加成员并分配相应的权限。或者，选择&#x200B;**[!UICONTROL 公共收藏集]**，以允许所有用户访问该收藏集。

   >[!NOTE]
   >
   >要使成员能够与其他用户共享集合，请在路径 `dam-users` 中提供组读取权限 `home/users`。 为位置的用户授予权 `/content/dam/collections` 限，以允许用户在弹出列表中视图集合。 或者，也可以让用户成为用户组的一 `dam-users` 部分。

1. （可选）为集合添加缩略图。
1. 点按／单 **[!UICONTROL 击创建]**，然后点按／单 **[!UICONTROL 击确定]** ，关闭对话框。 具有指定标题和属性的集合将在“收藏集”控制台中打开。

   >[!NOTE]
   >
   >Experience Manager资产允许您为收藏集创建审核任务，这与为资产文件夹创建审核任务的方式类似。

   要将资产添加到收藏集，请导航到资产用户界面。 有关详细信息，请 [参阅将资产添加到收藏集](#add-assets-to-a-collection)。

### 使用拖放区创建集合 {#create-collections-using-dropzone}

您可以将资产从资产UI拖动到集合。 您还可以创建收藏集的副本，并将资产拖动到该集合。

1. 从“资产”用户界面中，选择要添加到收藏集的资产。
1. 将资产拖至“放 **[!UICONTROL 入收藏集”区域]** 。 或者，点按／单击工 **[!UICONTROL 具栏中的]** “到集合”图标。
1. 在&#x200B;**[!UICONTROL 添加到收藏集]**&#x200B;页面中，点按/单击工具栏中的&#x200B;**[!UICONTROL 创建收藏集]**&#x200B;图标。如果要将资产添加到现有收藏集，请从页面中选择它，然后点按／单击添 **[!UICONTROL 加]**。 默认情况下，将选择最近更新的集合。
1. 在&#x200B;**[!UICONTROL 创建新收藏集]**&#x200B;对话框中，指定收藏集的名称。如果希望所有用户都可以访问该收藏集，请选择&#x200B;**[!UICONTROL 公共收藏集]**。
1. 点按／单击 **[!UICONTROL 继续]** ，以创建集合。

### Create a smart collection {#create-a-smart-collection}

智能收藏集使用搜索条件动态填充资产。 您只能使用文件而不使用文件夹或文件和文件夹来创建智能收藏集。

1. 导航到资产UI，然后点按／单击搜 **[!UICONTROL 索图]** 标。
1. 在“全方位搜索”框中输入搜索关键字，然后按Enter。 点按／单击GlobalNav图标以显示“过滤器”面板，并从“搜索”面板应用搜索筛选器。
1. 从“文件 **[!UICONTROL 和文件夹”列表]** ，选择“ **[!UICONTROL 文件”]**。
1. 点按／单击 **[!UICONTROL 保存智能收藏集]**。
1. 指定集合的名称。 Select **[!UICONTROL Public]** to add the DAM Users group with the Viewer role to the smart collection.

   >[!NOTE]
   >
   >如果选择“ **[!UICONTROL 公共]**”，则创建智能收藏集后，具有所有者角色的每个人都可以使用该智能收藏集。 If you deselect the **[!UICONTROL Public]** option, the DAM user group is no longer associated with the smart collection.

1. 点按/单击&#x200B;**[!UICONTROL 保存]**，以创建智能收藏集，然后关闭消息框以完成该进程。新的智能收藏集也会添加到&#x200B;**[!UICONTROL 保存的搜索]**列表。.
“创建智能选 **[!UICONTROL 择”按钮的标签会变]** 为“编 **[!UICONTROL 辑智能选择”]**。 要编辑智能收藏集的设置，请从“文件和文 **[!UICONTROL 件夹]** ”列 **[!UICONTROL 表中选择“文件]** ”。 然后，点按／单击编辑 **[!UICONTROL 智能选择]** 按钮。

## Add assets to a collection {#add-assets-to-a-collection}

您可以将资产添加到包含一系列引用的资产或文件夹的收藏集中。

>[!NOTE]
>
>智能收藏集可使用搜索查询来填充资产。因此，对资产和文件夹的静态引用不适用于此类收藏集。

1. 在资产UI中，导航到要添加到收藏集的资产所在的位置。
1. 选择资产，然后点按／单击工 **[!UICONTROL 具栏中的]** “到集合”图标。 或者，您也可以将资产拖动到放 **[!UICONTROL 入收藏集区]** 。 当放置区域变为活动状态且其标签变为“放置到添加”时， **[!UICONTROL 松开鼠标按钮]**。
1. 在“添 **[!UICONTROL 加到收藏集]** ”页面中，选择要将资产添加到的收藏集。
1. 点按／单击 **[!UICONTROL 添加]**，然后关闭确认消息。 资产会添加到收藏集。

## 编辑智能收藏集 {#edit-a-smart-collection}

Smart collections are built by saving a search so you can alter their content by modifying the search parameters of the [saved search](#saved-searches).

1. 在资产用户界面中，点按／单击工 **[!UICONTROL 具栏中]** 的搜索图标。
1. 在“Omnisearch”（全局搜索）框中，按Enter键。
1. 点按／单击GlobalNav图标以显示过滤器面板。
1. 从&#x200B;**[!UICONTROL 保存的搜索]**&#x200B;列表中，选择要修改的智能收藏集。“搜索”面板显示为保存的搜索配置的过滤器。
1. 从“文件 **[!UICONTROL 和文件夹”列表]** ，选择“ **[!UICONTROL 文件”]**。
1. 根据需要修改一个或多个过滤器。 点按／单击 **[!UICONTROL 编辑智能收藏集]**。 您还可以编辑智能收藏集的名称。
1. Tap/click **[!UICONTROL Save]**. 此时会出现&#x200B;**[!UICONTROL 编辑智能收藏集]**&#x200B;对话框。
1. 点按／单 **[!UICONTROL 击覆盖]** ，将原始智能收藏集替换为已编辑的收藏集。 或者，选择另 **[!UICONTROL 存为]** ，以单独保存编辑的集合。
1. In the confirmation dialog, tap/click **[!UICONTROL Save]** to complete the process.

## 视图和编辑集合元数据 {#view-and-edit-collection-metadata}

收藏集元数据由与收藏集相关的数据组成，其中包括添加的任何标记。

1. From the Collections console, select a collection and tap/click the **[!UICONTROL Properties]** icon from the toolbar.
1. 在&#x200B;**[!UICONTROL 收藏集元数据]**&#x200B;页面中，从&#x200B;**[!UICONTROL 基本]**&#x200B;和&#x200B;**高级**&#x200B;选项卡中查看收藏集元数据。
1. 根据需要修改元数据，然后点按／单击工 **[!UICONTROL 具栏中的保存并关闭]** ，以保存更改。

### 批量编辑集合元数据 {#edit-collection-metadata-in-bulk}

您可以同时编辑多个集合的元数据。 此功能可帮助您快速复制多个集合中的常见元数据。

1. 在“收藏集”控制台中，选择要编辑其元数据的两个或多个收藏集。
1. 在工具栏中，点按／单击属 **[!UICONTROL 性图]** 标。
1. 在&#x200B;**[!UICONTROL 收藏集元数据]**&#x200B;页面中，根据需要编辑&#x200B;**[!UICONTROL 基本]**&#x200B;和&#x200B;**[!UICONTROL 高级]**&#x200B;选项卡下的元数据。
1. 点按／单 **[!UICONTROL 击工具栏中的保存并关闭]** ，然后关闭确认对话框以完成该过程。
1. 要将新元数据附加到现有元数据，请选择&#x200B;**[!UICONTROL 追加模式]**。如果不选中此选项，则新元数据将替换字段中的现有元数据。点按/单击&#x200B;**[!UICONTROL 提交]**。

   >[!NOTE]
   >
   >“追加模式”仅适用于可包含多个值的字段。对于只能包含单个值的字段，即使选择&#x200B;**[!UICONTROL 追加模式]**，新元数据也不会追加到字段中的现有值中。

## 搜索 {#searching}

The Search feature within Collections supports both [Search for collections](#search-collections) and [Search for assets within a Collection](#search-within-collections).

### 搜索集合 {#search-collections}

您可以从“收藏集”控制台中搜索收藏集。当您在Omnisearch框中使用关键字进行搜索时，AEM资产会搜索集合名称、元数据和添加到集合的标记。

如果您从顶级搜索集合，则搜索结果中只返回单个集合。 收藏集中的资产或文件夹将被排除。 在所有其他情况下（例如，在单个集合或文件夹层次结构中），将返回所有相关的资产、文件夹和收藏集。

### 在集合中搜索 {#search-within-collections}

在收藏集控制台中，点按／单击收藏集以将其打开。

在集合中，AEM资产搜索仅限于您正在查看的集合中的资产（及其标记和元数据）。 在文件夹内搜索时，将返回当前文件夹内所有匹配的资产和子文件夹。 在集合中搜索时，只会返回与资产、文件夹和其他作为集合直接成员的集合相匹配的收藏集。

## 编辑集合设置 {#edit-collection-settings}

您可以编辑集合设置（如标题和说明），或向集合添加成员。

1. 选择一个集合，然后点按／单击工 **[!UICONTROL 具栏中的]** “设置”图标。 或者，也可以使 **[!UICONTROL 用集合缩览图]** 中的设置快速操作。
1. 在&#x200B;**[!UICONTROL 收藏集设置]**&#x200B;页面中修改收藏集设置。例如，按照[添加收藏集](#create-a-collection)中所述修改收藏集标题、描述、成员和权限。
1. Tap/click **[!UICONTROL Save]** to save the changes.

## 删除集合 {#delete-a-collection}

1. 从收藏集控制台中，选择一个或多个收藏集，然后点按／单击工具栏中的删除图标。
1. In the dialog, tap/click **[!UICONTROL Delete]** to confirm the delete action.

   >[!NOTE]
   >
   >You can also delete Smart collections by [delete saved searches](#saved-searches).

## 下载集合 {#download-a-collection}

下载集合时，将下载集合中的整个资产层次结构，包括文件夹和子集合。

1. 从收藏集控制台中，选择一个或多个要下载的收藏集。
1. 在工具栏中，点按／单击下载图标。
1. 在“下 **[!UICONTROL 载]** ”对话框中，点按／单 **[!UICONTROL 击下载]**。 如果要下载集合中资产的演绎版，请选择演 **[!UICONTROL 绎版]**。 <!-- Select the **[!UICONTROL Email]** option to send an email notification to the owner of the collection. -->

   当您选择要下载的集合时，将下载集合下的完整文件夹层次结构。 要将您下载的每个集合（包括嵌套在父集合下的子集合中的资产）包含在单个文件夹中，请为每个资 **[!UICONTROL 产选择创建单独的文件夹]**。

## 编辑多个集合的元数据属性 {#editing-metadata-properties-of-multiple-collections}

Adobe Enterprise Manager(AEM)资产允许您批量编辑许多集合的元数据。 使用“ [!UICONTROL 属性] ”页可对多个集合执行元数据更改，例如，将元数据属性更改为通用值或添加或修改标记。

要自定义元数据 [!UICONTROL 属性页] ，包括添加、修改和删除元数据属性，请使用模式编辑器。

>[!NOTE]
>
>批量编辑方法适用于集合中的可用资产。 对于跨文件夹可用或符合通用标准的资产，可在搜索后 [批量更新元数据](/help/assets/search-assets.md#metadataupdates)。

1. 从收藏集控制台中，选择要编辑的收藏集。
1. 在工具栏中，点按／单 **[!UICONTROL 击属性]** ，以打开选 [!UICONTROL 定集合的] “属性”页面。
1. 修改各个选项卡下选定集合的元数据属性。

   >[!NOTE]
   >
   >您为所选集合添加的元数据将覆盖这些集合的以前元数据，但标记除外。 您在“标记”字段中添 **[!UICONTROL 加的任何标记]** ，都会附加到元数据中标记的现有列表中。

1. 要视图特定集合的元数据属性，请在集合列表中取消选择其余的集合。 元数据编辑器字段会填充特定集合的元数据。

   >[!NOTE]
   >
   >* 在集合属性页面中，可以通过取消选择集合来从集合列表中删除集合。 集合列表默认选中所有集合。 您删除的集合的元数据不会更新。
   >* At the top of the list, select the check box near **[!UICONTROL Title]** to toggle between selecting the collections and clearing the list.


1. 保存更改。

## 创建嵌套集合 {#create-nested-collections}

您可以将一个收藏集添加到另一个收藏集中，从而创建嵌套式收藏集。

1. 从收藏集控制台中，选择所需的收藏集或收藏集组，然后点按或单击工具 **[!UICONTROL 栏中的至收藏]** 。
1. 从“添 **[!UICONTROL 加到收藏集]** ”页面，选择要在其中添加收藏集的收藏集。

   >[!NOTE]
   >
   >默认情况下，最近更新的集合会在“添加到集合 **[!UICONTROL ”页面中处于选中]** 。

1. 点按／单击 **[!UICONTROL 添加]**。 系统会显示一条消息，确认该集合已添加到“选择目标”页面中的 **[!UICONTROL 目标集合]** 。 关闭消息以完成该过程。

>[!NOTE]
>
>无法嵌套智能收藏集。也就是说，智能收藏集不能包含其他任何收藏集。

## 保存的搜索 {#saved-searches}

在“资产”用户界面中，您可以根据某些规则、搜索条件或自定义搜索彩块化来搜索或筛选资产。 如果将这些搜索另存为“保 **[!UICONTROL 存的搜索]**”，则以后可以从“筛选器”面板的“保存的 **[!UICONTROL 搜索]** ”列表中访问它们。 创建保存的搜索也会创建智能收藏集。

创建智能收藏集时将创建保存的搜索。智能收藏集会自动添加到&#x200B;**[!UICONTROL 保存的搜索]**&#x200B;列表。收藏集的“保存的搜索”查询将保存在 `dam:query` CRXDE 的属性中的相对位置`/content/dam/collections/`。

>[!NOTE]
>
>您可以像共享静态集合一样共享智能集合。

编辑保存的搜索与编辑智能收藏集相同。 For details, see [Edit a smart collection](#edit-a-smart-collection).

要删除保存的搜索，请执行以下步骤：

1. 在资产用户界面中，点按／单击工具栏中的搜索图标。

1. 在“Omnisearch”（全搜索）字段中，按Enter键。
1. 单击或点按GlobalNav图标以显示过滤器面板。
1. 从保存 **[!UICONTROL 的搜索列表]** ，点按／单 **** 击要删除的智能收藏集旁边的删除。
1. In the dialog, tap/click **[!UICONTROL Delete]** to delete the saved search.

## 对集合执行工作流 {#run-a-workflow-on-a-collection}

您可以为集合中的资产运行工作流。 如果集合包含嵌套集合，则该工作流也会在嵌套集合中的资产上运行。 但是，如果集合和嵌套集合包含重复资产，则此类资产只运行一次工作流。

1. 从“收藏集”控制台中，选择要运行工作流的收藏集。
1. 点按／单击GlobalNav图标，然后从列表中 **[!UICONTROL 选择]** “时间轴”。
1. 在时间轴中，单击或点按底部的尖角图标，然后点按／单击开始工 **[!UICONTROL 作流]**。
1. 在&#x200B;**[!UICONTROL 启动工作流]**&#x200B;部分，从列表中选择工作流模型。例如，选择 **[!UICONTROL DAM 更新资产]**&#x200B;模型。
1. 输入工作流的标题，然后点按／单击 **[!UICONTROL 开始]**。
1. 在对话框中，点按／单击继 **[!UICONTROL 续]**。 该工作流将在集合中的所有资产上运行。

>[!MORELIKETHIS]
>
>* [为集合创建审阅任务](/help/assets/bulk-approval.md)

