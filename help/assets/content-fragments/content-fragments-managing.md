---
title: 管理内容片段(Assets — 内容片段)
description: 了解如何使用Assets控制台管理您的AEM内容片段，作为您的Headless内容的基础或用于页面创作。
exl-id: 333ad877-db2f-454a-a3e5-59a936455932
feature: Content Fragments
role: User, Admin
solution: Experience Manager Sites
source-git-commit: 8a3ee333a0bd5904c43c424967a7b9c752fd38c2
workflow-type: tm+mt
source-wordcount: '1925'
ht-degree: 65%

---

# 管理内容片段 {#managing-content-fragments}

了解如何使用Assets控制台管理您的AEM内容片段，作为您的Headless内容的基础或用于页面创作。

定义完您的[内容片段模型](#creating-a-content-model)后，您可以使用这些模型[创建您的内容片段](#creating-a-content-fragment)。

[内容片段编辑器](#opening-the-fragment-editor)提供各种[模式](#modes-in-the-content-fragment-editor)，使您能够：

* [编辑内容](#editing-the-content-of-your-fragment)和[管理变体](#creating-and-managing-variations-within-your-fragment)
* [在片段中添加批注](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [将内容与片段关联](#associating-content-with-your-fragment)
* [配置元数据](#viewing-and-editing-the-metadata-properties-of-your-fragment)
* [查看结构树](/help/assets/content-fragments/content-fragments-structure-tree.md)
* [预览 JSON 表示形式](/help/assets/content-fragments/content-fragments-json-preview.md)


>[!NOTE]
>
>可以使用内容片段：
>
>* 创作页面时；请参阅[使用内容片段进行页面创作](/help/sites-cloud/authoring/fragments/content-fragments.md)。
>* 用于[使用带有 GraphQL 的内容片段](/help/assets/content-fragments/content-fragments-graphql.md)的 Headless 内容投放。

>[!NOTE]
>
>内容片段是一项&#x200B;**站点**&#x200B;功能，但存储为&#x200B;**资源**。
>
>它们主要通过&#x200B;**[内容片段](/help/sites-cloud/administering/content-fragments/overview.md#content-fragments-console)**&#x200B;控制台进行管理，但仍可以从&#x200B;**[Assets](/help/assets/content-fragments/content-fragments-managing.md)**&#x200B;控制台进行管理。
>
>创作内容片段有两个编辑器 — 新编辑器和原始编辑器。 默认使用新编辑器。 虽然基本功能相同，但存在一些差异。
>
>本节介绍原始编辑器。
>
>[内容片段 — 创作](/help/sites-cloud/administering/content-fragments/authoring.md)的默认编辑器是新编辑器，可从&#x200B;**内容片段**&#x200B;控制台和&#x200B;**Assets**&#x200B;控制台访问。 有关新编辑器的详细信息，请参阅站点文档[内容片段 — 创作](/help/sites-cloud/administering/content-fragments/authoring.md)。
>
>若要使用[原始编辑器](/help/assets/content-fragments/content-fragments-variations.md)，请先打开新编辑器，然后取消激活&#x200B;**新编辑器**&#x200B;开关。
>
>两个编辑器的顶部工具栏中都有一个切换开关，用于提供对另一个编辑器的快速访问。

## 创建内容片段 {#creating-content-fragments}

### 创建内容模型 {#creating-a-content-model}

[内容片段模型](/help/assets/content-fragments/content-fragments-models.md)可在使用结构化内容创建内容片段之前启用和创建。

### 创建内容片段 {#creating-a-content-fragment}

创建内容片段的方法是：

1. 导航到要 **创建片段** 的Assets文件夹。
1. 选择 **创建**，然后选择 **内容片段** ，以打开向导。
1. 向导的第一步要求您指定新片段的基础。

   * [模型](/help/assets/content-fragments/content-fragments-models.md) — 用于创建需要结构化内容的片段；例如，**冒险**&#x200B;模型

      * 将显示所有可用模型。

   选择后，使用&#x200B;**下一步**&#x200B;继续。

   ![选择内容片段模型](assets/cfm-managing-01.png)

1. 在属性 **步骤中** ，指定：

   * **基本**

      * **标题**

        片段标题。

        必填。

      * **描述**

      * **标记**

   * **高级**

      * **名称**

        名称；用于组成URL。

        必需；自动从标题派生，但可以更新。

1. 选 **择创建** ，以完成操作，然后打开片段 **进行编辑** ，或返回控制台并执行完 **成**。

   >[!NOTE]
   >在控制台的&#x200B;**列表**&#x200B;模式下，您可以更新&#x200B;**视图设置**&#x200B;以启用&#x200B;**内容片段模型**&#x200B;列。

## Assets控制台中的内容片段操作 {#actions-for-a-content-fragment-assets-console}

在&#x200B;**Assets**&#x200B;控制台中，您的内容片段可以执行一系列操作：

* 在工具栏中；选择片段后，所有适当的操作都可用。
* 作为[快速操作](/help/sites-cloud/authoring/basic-handling.md#quick-actions)；可用于各个片段信息卡的操作的子集。

工具栏中的![操作](assets/cfm-managing-02.png)

选择片段以显示包含适用操作的工具栏：

* **重新处理Assets**
* **创建**
* **下载**

   * 将片段另存为ZIP文件；您可以定义是否包含元素、变体、元数据。

* **签出**
* **属性**

   * 用于查看、编辑或同时查看或编辑片段的元数据。

* **编辑**

   * 允许您[打开片段以编辑内容](/help/assets/content-fragments/content-fragments-variations.md)及其元素、变体、关联的内容和元数据。

* **快速发布**
* **管理发布**
* **管理标记**
* **到收藏集**
* **复制**（和&#x200B;**粘贴**）
* **移动**
* **删除**

>[!NOTE]
>
>其中许多是Assets[和/或](/help/assets/manage-digital-assets.md)AEM桌面应用程序[的](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/get-started.html)标准操作。

## 打开片段编辑器 {#opening-the-fragment-editor}

要在原始编辑器中打开片段进行编辑，请执行以下操作：

>[!CAUTION]
>
>要编辑内容片段，您需要[相应的权限](/help/implementing/developing/extending/content-fragments-customizing.md#asset-permissions)。如果您遇到问题，请联系您的系统管理员。

1. 导航到内容片段的位置。

1. 打开片段进行编辑。

1. 片段在新编辑器中打开。 取消激活&#x200B;**新编辑器**&#x200B;开关（右上方）以打开原始编辑器：

   ![片段编辑器](assets/cfm-managing-03.png)

1. 根据需要进行更改。

1. 准备就绪后，根据需要使用&#x200B;**保存**、**保存并关闭**&#x200B;或&#x200B;**关闭**。

   >[!NOTE]
   >
   >**保存并关闭**&#x200B;可通过&#x200B;**保存**&#x200B;下拉列表使用。

   >[!NOTE]
   >
   >**保存并关闭**&#x200B;和&#x200B;**关闭**&#x200B;都将退出编辑器 – 请参阅[保存、关闭和版本](#save-close-and-versions)了解有关内容片段的各种选项如何操作的完整信息。

## 内容片段编辑器中的模式和操作 {#modes-actions-content-fragment-editor}

内容片段编辑器中提供了多种模式和操作。

### 内容片段编辑器中的模式 {#modes-in-the-content-fragment-editor}

使用侧面板中的图标在各种模式中导航：

* 变体：[编辑内容](#editing-the-content-of-your-fragment)和[管理变体](#creating-and-managing-variations-within-your-fragment)

* [注释](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [关联的内容](#associating-content-with-your-fragment)
* [元数据](#viewing-and-editing-the-metadata-properties-of-your-fragment)
* [结构树](/help/assets/content-fragments/content-fragments-structure-tree.md)
* [预览](/help/assets/content-fragments/content-fragments-json-preview.md)

内容片段编辑器中的![模式](assets/cfm-managing-04.png)

### 内容片段编辑器中的工具栏操作 {#toolbar-actions-in-the-content-fragment-editor}

顶部工具栏中的某些功能可以从多种模式使用：

![各种模式中可用的工具栏操作](assets/cfm-managing-top-toolbar.png)

* 当内容页面上已引用片段时，会显示一条消息。您可以&#x200B;**关闭**&#x200B;消息。

* 可以使用&#x200B;**切换侧面板**&#x200B;图标来隐藏/显示侧面板。

* 在片段名称下方，您可以看到用于创建当前片段的[内容片段模型](/help/assets/content-fragments/content-fragments-models.md)的名称：

   * 该名称还是一个打开模型编辑器的链接。

* 查看片段的状态；例如，有关创建、修改或发布时间的信息。状态也采用颜色编码：

   * **新建**：灰色
   * **草稿**：蓝色
   * **已发布**：绿色
   * **已修改**：橙色
   * **已停用**：红色

* 通过按钮可直接打开&#x200B;**新** *内容片段编辑器*（可通过[内容片段控制台](/help/sites-cloud/administering/content-fragments/authoring.md)访问），您可以[尝试新编辑器](/help/sites-cloud/administering/content-fragments/overview.md#content-fragments-console)。

  >[!WARNING]
  >
  >新编辑器将在同一选项卡中打开。 建议不要同时打开两个编辑器。

* **保存**&#x200B;提供对&#x200B;**保存并关闭**&#x200B;选项的访问。

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
>版本也可以从时间线[创建、比较和还原](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments)。

编辑器具有各种选项：

* **保存**&#x200B;和&#x200B;**保存并关闭**

   * **保存**&#x200B;将保存最新更改并保留在编辑器中。
   * **保存并关闭**&#x200B;将保存最新更改并退出编辑器。

  >[!CAUTION]
  >
  >要编辑内容片段，您需要[相应的权限](/help/implementing/developing/extending/content-fragments-customizing.md#asset-permissions)。如果您遇到问题，请联系您的系统管理员。

  >[!NOTE]
  >
  >在保存之前，可以保留在编辑器中并进行一系列更改。

  >[!CAUTION]
  >
  >除了仅保存您的更改外，这些操作还会更新任何引用，并确保 Dispatcher 按需要刷新。这些更改可能需要一些时间才能处理。因此，对于大型/复杂/重载系统，性能可能会受到影响。
  >
  >使用&#x200B;**保存并关闭**&#x200B;时请记住此过程，然后快速重新进入片段编辑器以进行并保存更多更改。

* **关闭**

  会退出编辑器，而不保存最新更改（即自上次&#x200B;**保存**&#x200B;后进行的更改）。

在编辑您的内容片段时，AEM 会自动创建版本，以确保在您取消更改时可以恢复先前的内容（使用&#x200B;**关闭**&#x200B;而不保存）：

1. 打开内容片段以编辑 AEM 时，会检查是否存在基于 Cookie 的令牌，以指示&#x200B;*编辑会话*&#x200B;存在：

   1. 如果找到令牌，则该片段将被视为现有编辑会话的一部分。
   2. 如果令牌为&#x200B;*不*&#x200B;可用，用户便开始编辑内容，并创建一个版本，并将此新编辑会话的令牌发送到客户端，客户端将保存在 Cookie 中。

2. 当有一个&#x200B;*活动*&#x200B;编辑会话时，正在编辑的内容每 600 秒自动保存一次（默认）。

   >[!NOTE]
   >
   >自动保存间隔可使用`/conf`机制进行配置。
   >
   >默认值，请参阅：
   >  `/libs/settings/dam/cfm/jcr:content/autoSaveInterval`

3. 如果用户取消编辑，则会恢复在编辑会话开始时创建的版本，并删除令牌以结束编辑会话。
4. 如果用户选择&#x200B;**保存**&#x200B;编辑，将保留更新的元素/变体，并删除令牌以结束编辑会话。

## 编辑片段的内容 {#editing-the-content-of-your-fragment}

打开片段后，您可以使用[变体](/help/assets/content-fragments/content-fragments-variations.md)选项卡来创作内容。

## 创建和管理片段中的变体 {#creating-and-managing-variations-within-your-fragment}

创建主控内容后，即可创建和管理[变体](/help/assets/content-fragments/content-fragments-variations.md)内容的一部分。

## 将内容与片段关联 {#associating-content-with-your-fragment}

您还可以[关联内容](/help/assets/content-fragments/content-fragments-assoc-content.md)与片段。这会提供一个连接，以便在将资源（即图像）添加到内容页面时，可以（可选）与片段一起使用资源（即图像）。

## 查看和编辑片段的元数据（属性） {#viewing-and-editing-the-metadata-properties-of-your-fragment}

您可以使用[元数据](/help/assets/content-fragments/content-fragments-metadata.md)选项卡查看和编辑片段的属性。

## 内容片段的时间线 {#timeline-for-content-fragments}

除了标准选项外，[时间线](/help/assets/manage-digital-assets.md#timeline)提供特定于内容片段的信息和操作：

* 查看有关版本、注释和批注的信息
* 版本操作

   * **[还原到此版本](#reverting-to-a-version)**（选择现有片段，然后选择特定版本）

   * **[与当前比较](#comparing-fragment-versions)**（选择现有片段，然后选择特定版本）

   * 添加&#x200B;**标签**&#x200B;和/或&#x200B;**注释**（选择现有片段，然后选择特定版本）

   * **保存为版本**（选择现有片段，然后选择时间线底部的向上箭头）

* 注释操作

   * **删除**

>[!NOTE]
>
>评论包括：
>
>* 所有资源的标准功能
>* 在时间线中制造
>* 与片段资源相关
>
>注释（适用于内容片段）包括：
>
>* 在片段编辑器中输入
>* 特定于片段中选定的文本区段
>
>两者都不显示新[内容片段编辑器](/help/sites-cloud/administering/content-fragments/authoring.md#commenting-on-your-fragment)中输入的注释。

例如：

![时间线](assets/cfm-managing-05.png)

## 比较片段版本 {#comparing-fragment-versions}

选择特定版本后，[时间线](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments)中的&#x200B;**与当前比较**&#x200B;操作可用。

这将打开：

* **当前**（最新）版本（左）

* 所选版本 **v&lt;*x.y*>**（右）

它们并排显示，其中：

* 任何差异都会突出显示

   * 已删除的文本 – 红色
   * 插入的文本 – 绿色
   * 替换文本 – 蓝色

* 全屏图标让您自行打开任一版本；然后切换回并行视图
* 您可以&#x200B;**还原**&#x200B;到特定版本
* **完成**&#x200B;将返回控制台

>[!NOTE]
>
>比较片段时无法编辑片段内容。

![比较变体](assets/cfm-managing-06.png)

## 恢复到某个版本  {#reverting-to-a-version}

您可以还原到片段的特定版本：

* 直接从[时间线](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments)。

  选择所需的版本，然后&#x200B;**还原到此版本**&#x200B;操作。

* [将版本与当前版本进行比较](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions)时，您可以&#x200B;**还原**&#x200B;到所选版本。

## 发布和引用片段 {#publishing-and-referencing-a-fragment}

>[!CAUTION]
>
>如果您的片段基于模型，则应确保[模型已发布](/help/assets/content-fragments/content-fragments-models.md#publishing-a-content-fragment-model)。
>
>如果发布的内容片段尚未发布模型，则会显示一个选择列表来指示该情况，并且模型将随该片段一起发布。

必须发布内容片段才能在发布环境中使用。 可使用标准Assets功能完成此操作：

* [快速发布](/help/assets/manage-publication.md#quick-publish)
* [管理发布](/help/assets/manage-publication.md#manage-publication)

此地址可以访问：

* 创建后；使用Assets控制台[中可用的](#actions-for-a-content-fragment-assets-console)操作。
* 从[内容片段编辑器](#toolbar-actions-in-the-content-fragment-editor)。

此外，当您[发布使用片段](/help/sites-cloud/authoring/fragments/content-fragments.md#publishing)的页面时；该片段在页面引用中列出。

>[!CAUTION]
>
>片段发布和/或引用后，当作者再次打开片段进行编辑时，AEM 将显示警告。 这是为了警告，对片段所做的更改也会影响引用的页面。

## 删除片段 {#deleting-a-fragment}

删除片段：

1. 在 **Assets** 控制台导航到内容片段的位置。
2. 选择片段。

   >[!NOTE]
   >
   >**删除**&#x200B;操作不能作为快速操作使用。

3. 从工具栏中选择&#x200B;**删除**。
4. 确认&#x200B;**删除**&#x200B;操作。

   >[!CAUTION]
   >
   >如果片段已在页面中被引用，您将看到一条警告消息，需要您确认是否继续执行&#x200B;**强制删除**。片段及其内容片段组件将从任何内容页面中删除。
