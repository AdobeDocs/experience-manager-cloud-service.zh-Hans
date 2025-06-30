---
title: 管理数字资产收藏集
description: 了解Adobe Experience Manager Assets中的收藏集概念。 了解如何与其他用户一起管理、编辑和编辑收藏集。
contentOwner: AG
mini-toc-levels: 1
feature: Collections, Asset Management
role: User
exl-id: b0798adc-56a4-4577-b4ee-8d1fca3bff09
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '2398'
ht-degree: 19%

---

# 管理收藏集 {#manage-collections}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-collections.html?lang=en) |
| AEM as a Cloud Service | 本文 |

收藏集是Adobe Experience Manager Assets中的一组资源。 使用收藏集可在用户之间共享资源。集合可以是静态集合或基于搜索结果的动态集合。

收藏集与文件夹的不同之处是可包含来自不同位置的资源。您可以与分配了不同级别权限（包括查看、编辑等）的各种用户共享收藏集。

您可以与一个用户共享多个收藏集。每个收藏集都包含对资源的引用。收藏集中会保持资源的引用完整性。

根据收藏集整理资产的方式，这些收藏集属于以下类型：

* 包含资产、文件夹和其他收藏集的静态引用列表的收藏集。

* 根据搜索条件动态包含资产的智能收藏集。

## 访问收藏集控制台 {#navigate-the-collections-console}

要打开&#x200B;**[!UICONTROL 收藏集]**&#x200B;控制台：

要打开&#x200B;**[!UICONTROL 收藏集]**，请选择Experience Manager徽标。 从导航页面，转到&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL 收藏集]**。

## 创建收藏集 {#create-a-collection}

您可以通过[静态引用](#create-a-collection-with-static-references)或基于[基于搜索条件的筛选器](#create-a-smart-collection)创建集合。 您还可以从Lightbox创建收藏集。

### 创建具有静态引用的收藏集 {#create-a-collection-with-static-references}

您可以创建具有静态引用的集合，例如，具有对资产、文件夹、集合、旋转集和图像集的引用的集合。

1. 导航到&#x200B;**[!UICONTROL 收藏集]**&#x200B;控制台。
1. 从工具栏中选择&#x200B;**[!UICONTROL 创建]**。
1. 在&#x200B;**[!UICONTROL 创建收藏集]**&#x200B;页面中，输入收藏集的标题和可选描述。
1. 向收藏集添加成员并分配相应的权限。或者，选择&#x200B;**[!UICONTROL 公共收藏集]**，以允许所有用户访问该收藏集。

   >[!NOTE]
   >
   >若要使成员能够与其他用户共享收藏集，请在路径`home/users`上提供`dam-users`组读取权限。 将权限授予位于`/content/dam/collections`位置的用户以允许这些用户在弹出列表中查看收藏集。 或者，将用户设为`dam-users`组的一部分。

1. （可选）为收藏集添加缩略图图像。
1. 选择&#x200B;**[!UICONTROL 创建]**，然后选择&#x200B;**[!UICONTROL 确定]**&#x200B;以关闭对话框。 具有指定标题和属性的集合将在“收藏集”控制台中打开。

   >[!NOTE]
   >
   >Experience Manager Assets允许您为收藏集创建审阅任务，其方式与为资源文件夹创建审阅任务的方式类似。

   要将资源添加到收藏集，请导航到Assets用户界面。 有关详细信息，请参阅[将资源添加到收藏集](#add-assets-to-a-collection)。

### 使用拖放区域创建收藏集 {#create-collections-using-dropzone}

您可以将资源从Assets UI拖到收藏集中。 您还可以创建收藏集的副本，并将资产拖到该处。

1. 从Assets用户界面中，选择要添加到收藏集的资源。
1. 将资源拖到收藏集&#x200B;**区域中的**&#x200B;拖放位置。 或者，从工具栏中选择&#x200B;**[!UICONTROL 目标收藏集]**&#x200B;图标。
1. 在&#x200B;**[!UICONTROL 添加到收藏集]**&#x200B;页面中，从工具栏中选择&#x200B;**[!UICONTROL 创建收藏集]**&#x200B;图标。 如果要将资源添加到现有收藏集，请从页面中选择它，然后选择&#x200B;**[!UICONTROL 添加]**。 默认情况下，将选择最近更新的集合。
1. 在&#x200B;**[!UICONTROL 创建新收藏集]**&#x200B;对话框中，指定收藏集的名称。如果希望所有用户都可以访问该收藏集，请选择&#x200B;**[!UICONTROL 公共收藏集]**。
1. 选择&#x200B;**[!UICONTROL 继续]**&#x200B;以创建集合。

### 创建智能收藏集 {#create-a-smart-collection}

智能收藏集使用搜索条件动态填充资产。 您可以创建仅使用文件的智能收藏集，而不使用文件夹或文件和文件夹。

1. 导航到Assets UI，然后选择&#x200B;**[!UICONTROL 搜索]**&#x200B;图标。
1. 在“全搜索”框中输入搜索关键字，然后选择`Enter`。 选择GlobalNav图标以显示“筛选器”面板，并从“搜索”面板应用搜索筛选器。
1. 从&#x200B;**[!UICONTROL 文件和文件夹]**&#x200B;列表中选择&#x200B;**[!UICONTROL 文件]**。
1. 选择&#x200B;**[!UICONTROL 保存智能收藏集]**。
1. 指定收藏集的名称。 选择&#x200B;**[!UICONTROL 公共]**&#x200B;以将具有查看器角色的DAM用户组添加到智能收藏集。

   >[!NOTE]
   >
   >如果选择&#x200B;**[!UICONTROL 公共]**，则创建智能收藏集后，所有具有“所有者”角色的人都可以使用该收藏集。 如果取消&#x200B;**[!UICONTROL Public]**&#x200B;选项，则DAM用户组不再与智能收藏集关联。

1. 选择&#x200B;**[!UICONTROL 保存]**&#x200B;以创建智能收藏集，然后关闭消息框以完成该过程。 新的智能收藏集也已添加到&#x200B;**[!UICONTROL 保存的搜索]**&#x200B;列表。
“创建智能选 **[!UICONTROL 择”按钮的标签会变]** 为“编 **[!UICONTROL 辑智能选择”]**。 要编辑智能收藏集的设置，请从“文件和文 **[!UICONTROL 件夹]** ”列 **[!UICONTROL 表中选择“文件]** ”。 然后选择&#x200B;**[!UICONTROL 编辑智能选择]**&#x200B;按钮。

## 将资源添加到收藏集 {#add-assets-to-a-collection}

您可以将资源添加到包含引用的资源或文件夹列表的收藏集。

>[!NOTE]
>
>智能收藏集使用搜索查询来填充资源。 因此，对资源和文件夹的静态引用不适用于它们。

1. 在Assets UI中，导航到要添加到收藏集的资源的位置。
1. 选择资产并从工具栏中选择&#x200B;**[!UICONTROL 到收藏集]**&#x200B;图标。 或者，您可以将资产拖到收藏集&#x200B;**区域中的**&#x200B;放置。 当放置区域变为活动状态并且其标签更改为&#x200B;**[!UICONTROL 放置到“添加”]**&#x200B;时，释放鼠标按钮。
1. 在&#x200B;**[!UICONTROL 添加到收藏集]**&#x200B;页面中，选择要将资产添加到的收藏集。
1. 选择&#x200B;**[!UICONTROL 添加]**，然后关闭确认消息。 资产将会添加到收藏集。

## 编辑智能收藏集 {#edit-a-smart-collection}

智能收藏集是通过保存搜索生成的，因此您可以通过修改[保存的搜索](#saved-searches)的搜索参数来更改其内容。

1. 在Assets用户界面中，从工具栏中选择&#x200B;**[!UICONTROL 搜索]**&#x200B;图标。
1. 将光标置于Omnisearch框中，选择`Enter`键。
1. 选择GlobalNav图标以显示“筛选器”面板。
1. 从&#x200B;**[!UICONTROL 保存的搜索]**&#x200B;列表中，选择要修改的智能收藏集。“搜索”面板显示为保存的搜索配置的过滤器。
1. 从&#x200B;**[!UICONTROL 文件和文件夹]**&#x200B;列表中选择&#x200B;**[!UICONTROL 文件]**。
1. 根据需要修改一个或多个筛选器。 选择&#x200B;**[!UICONTROL 编辑智能收藏集]**。 您还可以编辑智能收藏集的名称。
1. 选择&#x200B;**[!UICONTROL 保存]**。出现&#x200B;**[!UICONTROL 编辑智能收藏集]**&#x200B;对话框。
1. 选择&#x200B;**[!UICONTROL 覆盖]**&#x200B;将原始智能收藏集替换为已编辑的收藏集。 或者，选择&#x200B;**[!UICONTROL 另存为]**&#x200B;以单独保存编辑后的收藏集。
1. 在确认对话框中，选择&#x200B;**[!UICONTROL 保存]**&#x200B;以完成该过程。

## 查看和编辑收藏集元数据 {#view-and-edit-collection-metadata}

收藏集元数据包含有关收藏集的数据，包括添加的任何标记。

1. 从“收藏集”控制台中，选择一个收藏集，然后从工具栏中选择&#x200B;**[!UICONTROL 属性]**&#x200B;图标。
1. 在&#x200B;**[!UICONTROL 收藏集元数据]**&#x200B;页面中，从&#x200B;**[!UICONTROL 基本]**&#x200B;和&#x200B;**高级**&#x200B;选项卡中查看收藏集元数据。
1. 根据需要修改元数据，然后从工具栏中选择&#x200B;**[!UICONTROL 保存并关闭]**&#x200B;以保存更改。

### 批量编辑收藏集元数据 {#edit-collection-metadata-in-bulk}

您可以同时编辑多个收藏集的元数据。 此功能可帮助您在多个收藏集中快速复制常用元数据。

1. 在“收藏集”控制台中，选择要编辑元数据的两个或多个收藏集。
1. 从工具栏中选择&#x200B;**[!UICONTROL 属性]**&#x200B;图标。
1. 在&#x200B;**[!UICONTROL 收藏集元数据]**&#x200B;页面中，根据需要编辑&#x200B;**[!UICONTROL 基本]**&#x200B;和&#x200B;**[!UICONTROL 高级]**&#x200B;选项卡下的元数据。
1. 从工具栏中选择&#x200B;**[!UICONTROL 保存并关闭]**，然后关闭确认对话框以完成该过程。
1. 要将新元数据附加到现有元数据，请选择&#x200B;**[!UICONTROL 追加模式]**。如果不选中此选项，则新元数据将替换字段中的现有元数据。选择&#x200B;**[!UICONTROL 提交]**。

   >[!NOTE]
   >
   >“追加模式”仅适用于可包含多个值的字段。对于只能包含单个值的字段，即使选择&#x200B;**[!UICONTROL 追加模式]**，新元数据也不会追加到字段中的现有值中。

## 搜索 {#searching}

收藏集中的搜索功能支持[搜索收藏集](#search-collections)和[搜索收藏集中的资产](#search-within-collections)。

### 搜索收藏集 {#search-collections}

您可以从“收藏集”控制台中搜索收藏集。 当您在Omnisearch框中搜索关键字时，[!DNL Experience Manager Assets]将搜索收藏集名称、元数据和添加到收藏集的标记。

如果从顶级搜索收藏集，则搜索结果中只返回单个收藏集。 排除收藏集中的Assets或文件夹。 在所有其他情况下（例如，在单个收藏集内或文件夹层次结构中），将返回所有相关资产、文件夹和收藏集。

### 在收藏集中搜索 {#search-within-collections}

在收藏集控制台中，选择一个收藏集以将其打开。

在收藏集中，[!DNL Experience Manager]搜索仅限于您正在查看的收藏集中的资产（及其标记和元数据）。 在文件夹中搜索时，将返回当前文件夹中所有匹配的资源和子文件夹。 在收藏集中搜索时，仅返回匹配的资产、文件夹以及属于该收藏集的直接成员的其他收藏集。

## 编辑收藏集设置 {#edit-collection-settings}

您可以编辑收藏集设置（如标题和描述），也可以将成员添加到收藏集。

1. 选择一个收藏集，然后在工具栏中选择&#x200B;**[!UICONTROL 设置]**&#x200B;图标。 或者，使用收藏集缩略图中的&#x200B;**[!UICONTROL 设置]**&#x200B;快速操作。
1. 在&#x200B;**[!UICONTROL 收藏集设置]**&#x200B;页面中修改收藏集设置。例如，按照[添加收藏集](#create-a-collection)中所述修改收藏集标题、描述、成员和权限。
1. 选择&#x200B;**[!UICONTROL 保存]**&#x200B;以保存更改。

## 删除收藏集 {#delete-a-collection}

1. 从收藏集控制台中，选择一个或多个收藏集，然后选择工具栏中的删除图标。
1. 在对话框中，选择&#x200B;**[!UICONTROL 删除]**&#x200B;以确认删除操作。

   >[!NOTE]
   >
   >您还可以通过[删除保存的搜索](#saved-searches)来删除智能收藏集。

## 下载收藏集 {#download-a-collection}

下载收藏集时，将下载收藏集中资产的整个层次结构，包括文件夹和子收藏集。

1. 从收藏集控制台中，选择要下载的一个或多个收藏集。
1. 从工具栏中选择下载图标。
1. 在&#x200B;**[!UICONTROL 下载]**&#x200B;对话框中，选择&#x200B;**[!UICONTROL 下载]**。 如果要下载收藏集中资产的演绎版，请选择&#x200B;**[!UICONTROL 演绎版]**。<!-- Select the **[!UICONTROL Email]** option to send an email notification to the owner of the collection. -->

   选择要下载的收藏集时，将会下载收藏集下的完整文件夹层次结构。 要将您下载的每个收藏集（包括嵌套在父收藏集下的子收藏集中的资产）包含在单个文件夹中，请选择&#x200B;**[!UICONTROL 为每个资产创建单独的文件夹]**。

## 编辑多个收藏集的元数据属性 {#editing-metadata-properties-of-multiple-collections}

通过Adobe Enterprise Manager Assets，您可以批量编辑许多收藏集的元数据。 使用[!UICONTROL 属性]页面可对多个收藏集执行元数据更改，例如，将元数据属性更改为通用值或者添加或修改标记。

要自定义元数据[!UICONTROL 属性]页面，包括添加、修改和删除元数据属性，请使用架构编辑器。

>[!NOTE]
>
>批量编辑方法适用于收藏集中可用的资产。 对于跨文件夹可用的资源或与通用条件匹配的资源，可在搜索[&#128279;](/help/assets/search-assets.md#metadata-updates)后批量更新元数据。

1. 从收藏集控制台中，选择要编辑的收藏集。
1. 从工具栏中选择&#x200B;**[!UICONTROL 属性]**&#x200B;以打开所选收藏集的[!UICONTROL 属性]页面。
1. 修改各种选项卡下所选收藏集的元数据属性。

   >[!NOTE]
   >
   >为所选收藏集添加的元数据将覆盖这些收藏集的先前元数据，但标记除外。 您在&#x200B;**[!UICONTROL 标记]**&#x200B;字段中添加的任何标记都会附加到元数据中标记的现有列表中。

1. 要查看特定收藏集的元数据属性，请取消选择收藏集列表中剩余的收藏集。 使用特定收藏集的元数据填充元数据编辑器字段。

   >[!NOTE]
   >
   >* 在收藏集属性页中，可以通过取消选择从收藏集列表中删除收藏集。 收藏集列表默认选择了所有收藏集。 您删除的收藏集的元数据不会更新。
   >* 在列表顶部，选中&#x200B;**[!UICONTROL 标题]**&#x200B;附近的复选框，以在选择收藏集和清除列表之间切换。

1. 保存更改。

## 创建嵌套收藏集 {#create-nested-collections}

您可以将一个收藏集添加到另一个收藏集，从而创建嵌套收藏集。

1. 从“收藏集”控制台中，选择所需的收藏集或收藏集组，然后在工具栏中选择&#x200B;**[!UICONTROL 至收藏集]**。
1. 从&#x200B;**[!UICONTROL 添加到收藏集]**&#x200B;页面中，选择要添加收藏集的收藏集。

   >[!NOTE]
   >
   >默认情况下，**[!UICONTROL 添加到收藏集]**&#x200B;页面中会选择最近更新的收藏集。

1. 选择&#x200B;**[!UICONTROL 添加]**。 有一条消息确认该集合已添加到&#x200B;**[!UICONTROL 选择目标]**&#x200B;页的目标集合中。 关闭消息以完成该过程。

>[!NOTE]
>
>无法嵌套智能收藏集。 换句话说，智能收藏集不能包含任何其他收藏集。

## 保存的搜索 {#saved-searches}

在“资产”用户界面中，您可以根据某些规则、搜索条件或自定义搜索彩块化来搜索或筛选资产。 如果将这些搜索另存为&#x200B;**[!UICONTROL 保存的搜索]**，则以后可以从“过滤器”面板的&#x200B;**[!UICONTROL 保存的搜索]**&#x200B;列表中访问它们。 创建保存的搜索也会创建智能收藏集。

创建智能收藏集时将创建保存的搜索。智能收藏集会自动添加到&#x200B;**[!UICONTROL 保存的搜索]**&#x200B;列表。收藏集的“保存的搜索”查询保存在CRXDE的`dam:query`属性中的相对位置`/content/dam/collections/`。 您可以保存的搜索以及列表中显示的已保存搜索没有限制。

>[!NOTE]
>
>您可以使用与共享静态收藏集相同的方式共享智能收藏集。

编辑保存的搜索与编辑智能收藏集相同。 有关详细信息，请参阅[编辑智能收藏集](#edit-a-smart-collection)。

要删除保存的搜索，请执行以下步骤：

1. 在Assets用户界面中，从工具栏中选择搜索图标。

1. 将光标置于Omnisearch字段中，选择`Enter`键。
1. 选择GlobalNav图标以显示“筛选器”面板。
1. 从&#x200B;**[!UICONTROL 保存的搜索]**&#x200B;列表中，选择要删除的智能收藏集旁的&#x200B;**[!UICONTROL 删除]**。
1. 在对话框中，选择&#x200B;**[!UICONTROL 删除]**&#x200B;以删除保存的搜索。

## 对收藏集执行工作流 {#run-a-workflow-on-a-collection}

您可以为收藏集中的资产运行工作流。 如果收藏集包含嵌套收藏集，则工作流也会在嵌套收藏集中的资产上运行。 但是，如果收藏集和嵌套收藏集包含重复的资产，则工作流仅会为此类资产运行一次。

1. 从“收藏集”控制台中，选择要运行工作流的收藏集。
1. 选择GlobalNav图标，然后从列表中选择&#x200B;**[!UICONTROL 时间线]**。
1. 从时间轴中，选择底部的脱字符图标，然后选择&#x200B;**[!UICONTROL 启动工作流]**。
1. 在&#x200B;**[!UICONTROL 启动工作流]**&#x200B;部分，从列表中选择工作流模型。例如，选择 **[!UICONTROL DAM 更新资产]**&#x200B;模型。
1. 输入工作流的标题，然后选择&#x200B;**[!UICONTROL 开始]**。
1. 在对话框中，选择&#x200B;**[!UICONTROL 继续]**。 工作流会在收藏集中的所有资产上运行。

**另请参阅**

* [翻译资源](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [资源支持的文件格式](file-format-support.md)
* [搜索资源](search-assets.md)
* [连接的资源](use-assets-across-connected-assets-instances.md)
* [资源报告](asset-reports.md)
* [元数据架构](metadata-schemas.md)
* [下载资源](download-assets-from-aem.md)
* [管理元数据](manage-metadata.md)
* [搜索 Facet](search-facets.md)
* [批量元数据导入](metadata-import-export.md)
* [发布资源到 AEM 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [为收藏集创建审核任务](/help/assets/bulk-approval.md)
