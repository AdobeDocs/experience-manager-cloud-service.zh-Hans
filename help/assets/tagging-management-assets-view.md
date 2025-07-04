---
title: 如何在资源视图中管理标记？
description: 了解如何在资源视图中管理标记。标记帮助您将资源分类，这样可更高效地浏览和搜索资源。
exl-id: 7c5e1212-054f-46ca-9982-30e40b0482e1
feature: Smart Tags
role: User, Admin, Developer
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '1739'
ht-degree: 98%

---

# 在资源视图中管理标记 {#view-assets-and-details}

>[!CONTEXTUALHELP]
>id="assets_taxonomy_management"
>title="管理标记"
>abstract="标记帮助您将资源分类，这样可更高效地浏览和搜索资源。管理员可以使用分层的标记结构，该结构便于应用相关的元数据、为资源分类、支持搜索、重用标记、提高可发现性等。"

标记帮助您将资源分类，这样可更高效地浏览和搜索资源。标记有助于将适当的分类传播给其他用户和工作流程。

随着时间的推移，受控词汇的扁平列表变得难以管理。管理员可以使用分层的标记结构，该结构便于应用相关的元数据、为资源分类、支持搜索、重用标记、提高可发现性等。

您可以在根级别创建命名空间，并在命名空间内创建子标记的层次结构。例如，您可以在根级别创建一个`Activities`命名空间，并在该命名空间中具有 `Cycling`、`Hiking` 和 `Running` 标记。您可以在 `Running` 中有更多的子标记 `Clothing` 和 `Shoes`。

![标记管理](assets/tags-hierarchy.png)

变迁功能可提供许多好处，例如：

* 标记允许作者通过通用的分类法轻松组织不同的资源。作者可以通过常用标记快速搜索和组织资源。

* 分层标记非常灵活，能够很好地以逻辑方式组织术语。通过命名空间、标记和子标记，可以表示整个分类系统。

* 随着组织词汇的变化，标记可能会随着时间的推移而演变。

* 在管理视图中管理的标记与在资源视图中管理的标记保持同步，从而确保元数据得到治理及其完整性。

若要将标记应用于资源，您必须首先创建一个命名空间，然后创建并向其添加标记。您还可以创建标记并将其添加到现有命名空间。您在根级别创建的任何标记都会自动添加到标准标记命名空间。然后，您可以将“标记”字段添加到元数据表单，以便它显示在“资源详细信息”页面上。配置这些设置后，您可以开始将标记应用到资源。

>[!NOTE]
>
>仅当您不使用默认元数据表单时，才需要将“标记”字段添加到元数据表单。

![标记管理](assets/tagging-taxonomy-management.png)

除了本文提到的功能之外，管理视图中还提供了其他功能，包括合并、重命名、本地化和发布标记。

## 创建命名空间 {#create-a-namespace}

命名空间是只能存在于根级别的标记的容器。您可以通过首先为命名空间定义逻辑名称来开始设置标记的层次结构。如果您未将标记添加到任何现有命名空间，该标记将自动移至标准标记部分。

执行以下步骤可创建命名空间：

1. 前往 `Settings` 下的 `Taxonomy Management`，查看现有命名空间的列表。您还可以查看上次修改日期、修改命名空间或其下标记的用户以及标记在资源中使用的次数。
1. 单击 `Create Namespace`.
1. 为命名空间添加 `Title`、`Name` 和 `Description`。您 `Title` 字段中指定的输入内容会显示在层次结构的顶部。例如，在下图中，**活动**&#x200B;指的是命名空间的标题。

   ![标记管理](assets/tags-hierarchy.png)

1. 单击 `Save`.

## 将标记添加到命名空间 {#add-tags-to-namespace}

执行以下步骤以将标记添加到命名空间：

1. 转到&#x200B;**[!UICONTROL 分类管理]**。
1. 选择命名空间并单击`Create`，在命名空间下的顶层创建标记。如果您需要在命名空间中存在的标记下创建子标记，请选择该标记，然后单击 `Create`。
   ![标记的层次结构](assets/hierarchy-of-tags.png)

   在本例中，左侧的图像表示 `Path` 字段中显示的命名空间`automobile-four-wheeler`正下方的标记。右图是标记内添加的子标记的示例，因为除了命名空间之外，`Path` 字段中还显示了更多的标记名称、`jeep` 和 `jeep-meridian`。
1. 指定标记的标题、名称和描述，然后单击 `Save`。


   >[!NOTE]
   >
   >* `Title` 和 `Name` 字段是强制性的，而 `Description` 字段是可选的。
   >* 默认情况下，该工具会复制您在“标题”字段中键入的文本，删除空格或特殊字符 (.&amp; / \ : * ? [ ] | &quot; %)，并将其存储为名称。
   >* 您可以稍后更新 `Title` 字段，但 `Name` 字段是只读的。

## 将标记添加到标准标记 {#add-tags-to-standard-tags}

非结构化标记或没有任何层次结构的标记会存储在 `Standard Tags` 命名空间。此外，当您想要添加其他描述性术语而不影响受到管理的分类法时，您可以将该值存储在 `Standard Tags`。随着时间的推移，您可以将这些值移动到结构化命名空间下。此外，您还可以使用`Standard Tags`名称空间作为关键字的自由形式条目。

要创建标准标记，请单击根级别的 `Create Tag`。指定标题、名称和描述，然后单击 `Save`。

![将标记添加到标准标记](assets/adding-tags-to-standard-tags.png)

>[!NOTE]
>
>如果您使用 Assets as a Cloud Service 删除 `Standard Tags` 命名空间，则在可用标记的列表中不显示在根级别创建的标记。

## 移动标记 {#move-tags}

如果您将标记存储在错误的层次结构下或者分类法随着时间的推移而发生变化，您可以移动选定的标记以保持数据完整性。移动标记时必须考虑以下条件：

* 标记只能在现有命名空间下或现有标记层次结构内移动。
* 无法将标记移动到根目录以成为命名空间。
* 移动父标记也会移动存储在层次结构中的所有子标记。

执行以下步骤将标记从一个位置移动到另一位置：

1. 选择相应命名空间下的标记或整个标记层次结构，然后单击 `Move`。
1. 在“移动”对话框中，使用 `Select Tag` 部分选择新的目标标记或命名空间。
1. 单击 `Save`. 标记显示在新位置。

## 编辑标记 {#edit-tags}

要编辑标记的标题，请选择该标记并单击 `Edit`。指定新标题并单击 `Save`。

>[!NOTE]
>
>* 标记的 `Name` 无法更新。标记的根路径也基于标记的名称。即使更新了 `Title` 字段，路径也保持不变。
>* 在 Assets as a Cloud Service 中还有合并、本地化和发布等其他操作可用。

## 删除标记 {#delete-tags}

您可以同时删除多个命名空间或标记。删除操作无法撤消。

执行以下步骤可以删除标记：

1. 选择命名空间或标记，然后单击 `Delete`。
1. 单击 `Confirm`.

>[!NOTE]
>
>* 删除父标记或命名空间也会删除存储在层次结构中的子标记。如果需要删除或更新父命名空间，建议在删除父层次结构之前，先[将标记](#moving-tags)移动到新的目标。
>* 删除标记也会从资源中删除其所有引用。
>* 您无法删除根级别内的标准标记。

## 将标记组件添加到元数据表单 {#add-tags-to-metadata-form}

标记组件会自动添加到 `default` 元数据表单中。您可以使用模板或从头开始设计[元数据表单](https://experienceleague.adobe.com/docs/experience-manager-assets-essentials/help/metadata.html?lang=zh-Hans#metadata-forms)。如果您使用的不是现有的元数据表单模板，则可以修改您的元数据表单并添加标记组件。元数据属性映射是自动填充的，因此此时无法修改。[!DNL Assets as a Cloud Service] 用户可以更新映射以使用自定义命名空间存储标记值，并使用根路径仅公开层次结构的子集。

观看这段简短的视频以了解如何将标记组件添加到元数据表单：

>[!VIDEO](https://video.tv.adobe.com/v/3420452)


### 将标记添加到资源 {#add-tags-to-assets}

1. 转到资源详细信息页面，并导航到元数据表单的 `Tags` 部分。
1. 选择“标记”字段旁边的标记选择器图标，或开始输入标记名称以查看建议的结果。

   ![标记资源](assets/adding-tags-to-assets.png)

1. 选择一个或多个标记。 子标记将与父标记或名称空间一起自动选择。
在 Assets Essentials 中修改的标记还被应用于 Assets as a Cloud Service 中。

## 将标记添加到阻止列表 {#blocklist-essentials}

通过 [!DNL Assets view] 可配置一个阻止列表，其中包括在将资源上传到存储库时不应作为智能标记添加到资源的字词。此功能帮助您确保品牌合规，并减少审核智能标记的工作量。
<!--
### Block smart tags for single asset {#block-smart-tags-for-single-asset}
![block smart tags](assets/block-smart-tags.png)
-->

### 为所有资源阻止智能标记 {#block-smart-tags-for-all-assets}

通过 [!DNL Assets view]，管理员可为现有资源和新添加的资源阻止智能标记。要阻止标记，请执行以下步骤：

1. 导航到&#x200B;**[!UICONTROL 设置]**&#x200B;下的&#x200B;**[!UICONTROL 阻止的标记]**。
1. 单击&#x200B;**[!UICONTROL 添加阻止的标记]**。
1. 在文本框中键入要阻止的标记，然后单击&#x200B;**[!UICONTROL 输入]**。
1. 添加完标记后，单击&#x200B;**[!UICONTROL 添加]**。随后将在阻止的标记列表中列出所输入的标记。

   >[!NOTE]
   >
   >一次最多可将 25 个标记添加到列表。重复这些步骤以将更多标记添加到阻止列表。

还可为单个资源阻止智能标记。导航到资源的详细信息。在&#x200B;**[!UICONTROL 标记]**&#x200B;选项卡下，删除不需要的智能标记，然后单击&#x200B;**[!UICONTROL 保存]**。随后将在阻止列表中列出所选资源的标记。

### 对阻止列表执行的操作 {#blocklist-actions}

* **删除标记：**&#x200B;还可从阻止列表中删除标记。为此，请选择一个或多个要删除的标记。单击&#x200B;**[!UICONTROL 删除]**。一次最多可从列表中删除 25 个标记。
* **全选**：选中&#x200B;**标记名称**&#x200B;旁的复选框以选择阻止列表中的所有标记。
* **排序：**&#x200B;可按升序或降序将阻止列表排序。为此，请单击&#x200B;**标记名称**&#x200B;旁的箭头。

  ![阻止标记](assets/blocklist.gif)

  >[!NOTE]
  >
  >在阻止列表中添加标记时，请勿使用特殊字符。可使用 a-z、A-Z、0-9 和 - 等字符。

### 导出阻止列表{#export-blocklist}

Assets视图允许您将列出的阻止标记导出为CSV格式。 要导出阻止列表，请执行以下步骤：

1. 单击&#x200B;**[!UICONTROL 导出为 CSV]**。
1. 选择适当的位置以保存该 CSV 文件。还可根据要求重命名该文件。
1. 单击&#x200B;**[!UICONTROL 保存]**。随后将导出的 CSV 格式列表下载到所选位置。

### 导入阻止列表{#import-blocklist}

通过Assets视图，可以从数据源(CSV)导入阻止的标记。 要导入阻止列表，请执行以下步骤：

1. 单击&#x200B;**[!UICONTROL 导入为 CSV]**。
1. 从设备中选择该 CSV 文件。单击&#x200B;**[!UICONTROL 选择文件]**&#x200B;以从设备中导航到该文件。或者，还可从设备拖放该 CSV 文件。
1. 单击&#x200B;**[!UICONTROL 上传]**。随后将在阻止的标记列表中列出该 CSV 文件中的标记。

   ![导入阻止的标记列表](assets/import-blocked-tags.png)

如果要下载阻止的标记模板，请执行以下步骤：

1. 单击&#x200B;**[!UICONTROL 下载模板]**。
1. 选择适当的位置以保存该 CSV 文件。还可根据要求重命名该文件。
1. 单击&#x200B;**[!UICONTROL 保存]**。随后将 CSV 格式的阻止标记模板下载到所选位置。
