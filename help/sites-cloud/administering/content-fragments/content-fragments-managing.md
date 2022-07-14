---
title: 管理内容片段
description: 了解如何使用“内容片段”控制台管理AEM内容片段；用于页面创作，或作为无头内容的基础。
source-git-commit: 9de8becfd69ea2a65a847cba88468c94e2fdf484
workflow-type: tm+mt
source-wordcount: '2047'
ht-degree: 2%

---

# 管理内容片段 {#managing-content-fragments}

了解如何使用 **内容片段** 用于管理AEM内容片段的控制台。 这些参数可用于页面创作，或用作无头内容的基础。

在定义 [内容片段模型](#creating-a-content-model) 您可以使用这些 [创建内容片段](#creating-a-content-fragment).

的 [内容片段编辑器](#opening-the-fragment-editor) 提供各种 [模式](#modes-in-the-content-fragment-editor) 要使您能够：

* [编辑内容](#editing-the-content-of-your-fragment) 和 [管理变量](#creating-and-managing-variations-within-your-fragment)
* [在片段中添加批注](/help/sites-cloud/administering/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [将内容与片段关联](#associating-content-with-your-fragment)
* [配置元数据](#viewing-and-editing-the-metadata-properties-of-your-fragment)
* [查看结构树](/help/sites-cloud/administering/content-fragments/content-fragments-structure-tree.md)
* [预览JSON表示形式](/help/sites-cloud/administering/content-fragments/content-fragments-json-preview.md)


>[!NOTE]
>
>可以使用内容片段：
>
>* 创作页面时；请参阅 [使用内容片段进行页面创作](/help/sites-cloud/authoring/fundamentals/content-fragments.md).
>* 表示 [通过GraphQL使用内容片段交付无头内容](/help/sites-cloud/administering/content-fragments/content-fragments-graphql.md).


>[!NOTE]
>
>内容片段存储为 **资产**. 它们主要通过 **内容片段** 控制台，但也可以从 **资产** 控制台。

## 创建内容片段 {#creating-content-fragments}

### 创建内容模型 {#creating-a-content-model}

[内容片段模型](/help/sites-cloud/administering/content-fragments/content-fragments-models.md) 可在使用结构化内容创建内容片段之前启用和创建。

### 创建内容片段 {#creating-a-content-fragment}

要创建内容片段，请执行以下操作：

1. 从 **内容片段** 控制台，选择 **创建** （右上方）。

   >[!NOTE]
   >
   >要预定义新片段的位置，您可以导航到要创建片段的文件夹，也可以在创建过程中指定该位置。

1. 的 **新内容片段** 对话框随即会打开，您可以从此处指定：

   * **位置**  — 这将使用当前位置自动完成，但您可以根据需要选择其他位置
   * **内容片段模型**  — 从下拉列表中选择要用作片段基础的模型
   * **标题**
   * **名称**  — 此操作将根据 **标题**，但您可以根据需要进行编辑
   * **描述**

   ![“新建内容片段”对话框](assets/cfm-managing-new-cf-01.png)

1. 选择 **创建**&#x200B;或 **创建并打开** 以保留您的定义。

## 内容片段的状态 {#statuses-content-fragments}

内容片段在存在期间可以具有多种状态，如 [内容片段控制台](/help/sites-cloud/administering/content-fragments/content-fragments-console.md):

* **新建**
已在内容片段编辑器中创建但从未编辑或打开新的内容片段。
* **草稿**
有人在内容片段编辑器中编辑或打开了（新）内容片段 — 但尚未发布。
* **已发布**
内容片段已发布。
* **已修改**
内容片段在发布后（但在发布修改之前）进行了编辑。
* **未发布**
内容片段已取消发布。

## 内容片段控制台中的内容片段的操作 {#actions-content-fragment-console}

在 **内容片段** 控制台工具栏中为您的内容片段提供了一系列操作：

![控制台操作](assets/cfm-managing-cf-console-01.png)

* **在资产中打开**
* **创建**
* 的 **引用者** 列还提供了显示该片段的所有父引用的直接链接；包括引用内容片段、体验片段和页面。
* 将鼠标悬停在文件夹名称上将显示JCR路径。

选择片段后，所有适当的操作均可用：

![控制台操作 — 已选择片段](assets/cfm-managing-cf-console-selected-01.png)

* **打开**
* **发布** (和 **取消发布**)
* **复制**
* **移动**
* **重命名**
* **删除**

>[!NOTE]
>
>“发布”、“取消发布”、“删除”、“移动”、“重命名”、“复制”等操作会触发异步作业。 可以通过AEM异步作业UI监控该作业的进度。

## 在内容片段控制台中自定义视图 {#viewing-content-fragment-console}

控制台在当前文件夹和所有子文件夹中显示有关内容片段的信息。

您可以使用 **自定义表** 图标：

![“自定义表”图标](assets/cfm-managing-cf-console-customize-table-icon.png)

这将打开 **自定义表** 对话框中，您可以选择/取消选择可用列：

![自定义表](assets/cfm-managing-cf-console-customize-table.png)

## 在内容片段控制台中搜索和过滤 {#search-filter-content-fragment-console}

您可以搜索和/或筛选要在控制台中显示的内容片段。

您可以：

* 选择所需的文件夹
* 选择过滤器，其中 **显示过滤器** 并行使用搜索框：

![“自定义表”图标](assets/cfm-managing-cf-console-filter-search-01.png)

提供了一系列过滤器：

![筛选和搜索](assets/cfm-managing-cf-console-filter-search-02.png)

还可以保存过滤器和搜索组合，供以后参考。

## 打开片段编辑器 {#opening-the-fragment-editor}

要打开片段进行编辑，请执行以下操作：

>[!CAUTION]
>
>要编辑内容片段，您需要 [相应的权限](/help/implementing/developing/extending/content-fragments-customizing.md#asset-permissions). 如果您遇到问题，请联系您的系统管理员。

1. 使用 **内容片段** 控制台以导航到内容片段的位置。
1. 通过选择片段，然后打开片段以进行编辑 **打开** 中。

1. 将打开片段编辑器。 根据需要进行更改：

   ![片段编辑器](assets/cfm-managing-03.png)

1. 进行更改后，请使用 **保存**, **保存并关闭** 或 **关闭** 。

   >[!NOTE]
   >
   >**保存并关闭** 可通过 **保存** 下拉列表。

   >[!NOTE]
   >
   >两者兼有 **保存并关闭** 和 **关闭** 将退出编辑器 — 请参阅 [保存、关闭和版本](#save-close-and-versions) 有关各种选项如何对内容片段进行操作的完整信息。

## 内容片段编辑器中的模式和操作 {#modes-actions-content-fragment-editor}

内容片段编辑器中提供了多种模式和操作。

### 内容片段编辑器中的模式 {#modes-in-the-content-fragment-editor}

使用侧面板中的图标在各种模式中导航：

* 变体： [编辑内容](#editing-the-content-of-your-fragment) 和 [管理变量](#creating-and-managing-variations-within-your-fragment)

* [注释](/help/sites-cloud/administering/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [关联的内容](#associating-content-with-your-fragment)
* [元数据](#viewing-and-editing-the-metadata-properties-of-your-fragment)
* [结构树](/help/sites-cloud/administering/content-fragments/content-fragments-structure-tree.md)
* [预览](/help/sites-cloud/administering/content-fragments/content-fragments-json-preview.md)

![模式](assets/cfm-managing-04.png)

### 内容片段编辑器中的工具栏操作 {#toolbar-actions-in-the-content-fragment-editor}

顶部工具栏中的某些功能可以从多种模式使用：

![模式](assets/cfm-managing-top-toolbar.png)

* 当内容页面上已引用片段时，将显示一条消息。 您可以 **关闭** 消息。

* 可以使用隐藏/显示侧面板 **切换侧面板** 图标。

* 在片段名称下，您可以看到 [内容片段模型](/help/sites-cloud/administering/content-fragments/content-fragments-models.md) 用于创建当前片段：

   * 该名称还是一个将打开模型编辑器的链接。

* 查看片段的状态；例如，有关创建、修改或发布时间的信息。 状态也采用颜色编码：

   * **新建**:灰色
   * **草稿**:蓝色
   * **已发布**:绿色
   * **已修改**:橙色
   * **已停用**:红色

* **保存** 提供对 **保存并关闭** 选项。

* 三个圆点(**...**)下拉列表提供了对其他操作的访问权限：
   * **更新页面引用**
      * 这会更新任何页面引用。
   * **[快速发布](#publishing-and-referencing-a-fragment)**
   * **[管理发布](#publishing-and-referencing-a-fragment)**

<!--
This updates any page references and ensures that the Dispatcher is flushed as required. -->

## 保存、关闭和版本 {#save-close-and-versions}

>[!NOTE]
>
>版本也可以 [从时间轴创建、比较和还原](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#timeline-for-content-fragments).

编辑器具有各种选项：

* **保存** 和 **保存并关闭**

   * **保存** 将保存最新更改并保留在编辑器中。
   * **保存并关闭** 将保存最新更改并退出编辑器。

   >[!CAUTION]
   >
   >要编辑内容片段，您需要 [相应的权限](/help/implementing/developing/extending/content-fragments-customizing.md#asset-permissions). 如果您遇到问题，请联系您的系统管理员。

   >[!NOTE]
   >
   >在保存之前，可以保留在编辑器中并进行一系列更改。

   >[!CAUTION]
   >
   >除了仅保存您的更改外，这些操作还会更新任何引用，并确保Dispatcher按需要刷新。 这些更改可能需要一些时间才能处理。 因此，对于大型/复杂/重载系统，性能可能会受到影响。
   >
   >在使用 **保存并关闭** 然后快速重新进入片段编辑器以进行并保存进一步的更改。

* **关闭**

   将退出编辑器，而不保存最新更改(即自上次 **保存**)。

在编辑内容片段时，AEM会自动创建版本，以确保在您取消更改(使用 **关闭** （不保存）：

1. 打开内容片段以编辑AEM时，会检查是否存在基于Cookie的令牌，以指示 *编辑会话* 存在：

   1. 如果找到令牌，则该片段将被视为现有编辑会话的一部分。
   2. 如果令牌为 *not* 可用，用户便开始编辑内容，并创建一个版本，并将此新编辑会话的令牌发送到客户端，客户端将保存在Cookie中。

2. 当 *活动* 编辑会话时，每600秒会自动保存一次所编辑的内容（默认）。

   >[!NOTE]
   >
   >可使用 `/conf` 机制。
   >
   >默认值，请参阅：
   >  `/libs/settings/dam/cfm/jcr:content/autoSaveInterval`

3. 如果用户取消编辑，则会恢复在编辑会话开始时创建的版本，并删除令牌以结束编辑会话。
4. 如果用户选择 **保存** 进行编辑后，将保留更新的元素/变体，并删除令牌以结束编辑会话。

## 编辑片段的内容 {#editing-the-content-of-your-fragment}

打开片段后，您可以使用 [变体](/help/sites-cloud/administering/content-fragments/content-fragments-variations.md) 选项卡来创作内容。

## 创建和管理片段中的变量 {#creating-and-managing-variations-within-your-fragment}

创建主控内容后，即可创建和管理 [变体](/help/sites-cloud/administering/content-fragments/content-fragments-variations.md) 内容的一部分。

## 将内容与片段关联 {#associating-content-with-your-fragment}

您还可以 [关联内容](/help/sites-cloud/administering/content-fragments/content-fragments-assoc-content.md) 片段。 这提供了一个连接，以便在将资产（即图像）添加到内容页面时，可以（可选）与片段一起使用资产（即图像）。

## 查看和编辑片段的元数据（属性） {#viewing-and-editing-the-metadata-properties-of-your-fragment}

您可以使用 [元数据](/help/sites-cloud/administering/content-fragments/content-fragments-metadata.md) 选项卡。

## 发布和引用片段 {#publishing-and-referencing-a-fragment}

>[!CAUTION]
如果您的片段基于模型，则应确保 [模型已发布](/help/sites-cloud/administering/content-fragments/content-fragments-models.md#publishing-a-content-fragment-model).
如果发布的内容片段的模型尚未发布，则会显示一个选择列表来指示该情况，并且模型将随该片段一起发布。

必须发布内容片段才能在发布环境中使用。 可使用标准资产功能完成此操作

* 从 **发布** 的 [内容片段控制台](#actions-content-fragment-console)
   * **现在**  — 确认后，片段将立即发布
   * **计划**  — 您可以选择片段的发布日期和时间

   必要时，您需要指定 **激活日期** 和引用发布的内容。 例如：
   ![“发布”对话框](assets/cfm-publish-01.png)

* 从 [内容片段编辑器](#toolbar-actions-in-the-content-fragment-editor)
   * [**快速发布**](/help/assets/manage-publication.md#quick-publish)
   * [**管理发布**](/help/assets/manage-publication.md#manage-publication)

此外，当您 [发布使用片段的页面](/help/sites-cloud/authoring/fundamentals/content-fragments.md#publishing);片段将在页面引用中列出。

>[!CAUTION]
发布和/或引用片段后，当作者打开片段进行再次编辑时，AEM将显示警告。 这是为了警告，对片段所做的更改也会影响引用的页面。

## 取消发布片段 {#unpublishing-a-fragment}

要取消发布内容片段，请选择一个或多个片段，然后 **取消发布**.

>[!NOTE]
的 **取消发布** 在可用已发布的片段时，操作将可见。

>[!CAUTION]
如果片段已从其他片段或页面引用，您将看到一条警告消息，需要您确认是否继续。

## 删除片段 {#deleting-a-fragment}

要删除片段，请执行以下操作：

1. 在 **内容片段** 控制台导航到内容片段的位置。
2. 选择片段。

   >[!NOTE]
   的 **删除** 操作不可用作快速操作。

3. 选择 **删除** 中。
4. 确认 **删除** 操作。

   >[!CAUTION]
   如果片段已从其他片段或页面引用，您将看到一条警告消息，需要您确认是否继续 **强制删除**. 片段及其内容片段组件将从任何内容页面中删除。

## 内容片段的时间轴 {#timeline-for-content-fragments}

>[!NOTE]
此功能仅在 **资产** 控制台

除了标准选项外， [时间轴](/help/assets/manage-digital-assets.md#timeline) 提供特定于内容片段的信息和操作：

* 查看有关版本、注释和批注的信息
* 版本操作

   * **[还原到此版本](#reverting-to-a-version)** （选择现有片段，然后选择特定版本）

   * **[与当前比较](#comparing-fragment-versions)** （选择现有片段，然后选择特定版本）

   * 添加 **标签** 和/或 **注释** （选择现有片段，然后选择特定版本）

   * **另存为版本** （选择现有片段，然后选择时间轴底部的向上箭头）

* 注释操作

   * **删除**

>[!NOTE]
评论包括：
* 所有资产的标准功能
* 在时间轴中制造
* 与片段资产相关
>
注释（适用于内容片段）包括：
* 在片段编辑器中输入
* 特定于片段中选定的文本区段
>


例如：

![时间线](assets/cfm-managing-05.png)

## 比较片段版本 {#comparing-fragment-versions}

>[!NOTE]
此功能仅在 **资产** 控制台

的 **与当前比较** 操作可从 [时间轴](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#timeline-for-content-fragments) 选择特定版本后，才会将其删除。

此时将打开：

* the **当前** （最新）版本（左）

* 所选版本 **v&lt;*x.y*>** （右）

它们将并排显示，其中：

* 任何差异都会突出显示

   * 已删除的文本 — 红色
   * 插入的文本 — 绿色
   * 替换文本 — 蓝色

* 全屏图标允许您自行打开任一版本；然后切换回并行视图
* 您可以 **还原** 到特定版本
* **完成** 将返回控制台

>[!NOTE]
比较片段时无法编辑片段内容。

![比较](assets/cfm-managing-06.png)

## 还原到某个版本  {#reverting-to-a-version}

>[!NOTE]
此功能仅在 **资产** 控制台

您可以还原到片段的特定版本：

* 直接从 [时间轴](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#timeline-for-content-fragments).

   选择所需的版本，然后 **还原到此版本** 操作。

* While [将版本与当前版本进行比较](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#comparing-fragment-versions) 您可以 **还原** 到所选版本。

