---
title: 管理内容片段
description: 了解如何使用AEM控制台来管理您的Assets内容片段（无头内容的基础）。
feature: 内容片段
role: User
exl-id: 333ad877-db2f-454a-a3e5-59a936455932
source-git-commit: 24a4a43cef9a579f9f2992a41c582f4a6c775bf3
workflow-type: tm+mt
source-wordcount: '1746'
ht-degree: 9%

---

# 管理内容片段 {#managing-content-fragments}

了解如何使用AEM控制台来管理您的Assets内容片段（无头内容的基础）。

定义[内容片段模型](#creating-a-content-model)后，可以使用这些模型来[创建内容片段](#creating-a-content-fragment)。

[内容片段编辑器](#opening-the-fragment-editor)提供了各种[模式](#modes-in-the-content-fragment-editor)，使您能够：

* [编辑内](#editing-the-content-of-your-fragment) 容并 [管理变体](#creating-and-managing-variations-within-your-fragment)
* [在片段中添加批注](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [将内容与片段关联](#associating-content-with-your-fragment)
* [配置元数据](#viewing-and-editing-the-metadata-properties-of-your-fragment)
* [查看结构树](/help/assets/content-fragments/content-fragments-structure-tree.md)
* [预览JSON表示形式](/help/assets/content-fragments/content-fragments-json-preview.md)


>[!NOTE]
>
>可以使用内容片段：
>
>* 创作页面时；请参阅[使用内容片段进行页面创作](/help/sites-cloud/authoring/fundamentals/content-fragments.md)。
>* 对于使用带有GraphQL](/help/assets/content-fragments/content-fragments-graphql.md)的内容片段的[无标题内容交付。


>[!NOTE]
>
>内容片段以&#x200B;**Assets**&#x200B;的形式存储，因此主要从&#x200B;**Assets**&#x200B;控制台中进行管理。

## 创建内容片段 {#creating-content-fragments}

### 创建内容模型 {#creating-a-content-model}

[在使用结](/help/assets/content-fragments/content-fragments-models.md) 构化内容创建内容片段之前，应启用并创建内容片段模型。

### 创建内容片段 {#creating-a-content-fragment}

创建内容片段的方法是：

1. 导航到要 **创建片段** 的Assets文件夹。
1. 选择 **创建**，然后选择 **内容片段** ，以打开向导。
1. 向导的第一步要求您指定新片段的基础。

   * [模型](/help/assets/content-fragments/content-fragments-models.md)  — 用于创建需要结构化内容的片段；例如，冒险 **** 模型

      * 将显示所有可用的模型。

   选择后，使用&#x200B;**Next**&#x200B;继续。

   ![片段基础](assets/cfm-managing-01.png)

1. 在属性 **步骤中** ，指定：

   * **基本**

      * **标题**

         片段标题。

         强制.

      * **描述**

      * **标记**
   * **高级**

      * **名称**

         名称；将用于形成URL。

         强制；将自动从标题派生，但可以更新。


1. 选 **择创建** ，以完成操作，然后打开片段 **进行编辑** ，或返回控制台并执行完 **成**。

   >[!NOTE]
   >在控制台的&#x200B;**列表**&#x200B;模式下，您可以更新&#x200B;**查看设置**&#x200B;以启用&#x200B;**内容片段模型**&#x200B;列。

## 资产控制台中内容片段的操作 {#actions-for-a-content-fragment-assets-console}

在&#x200B;**Assets**&#x200B;控制台中，可以对内容片段执行一系列操作：

* 工具栏中；选择片段后，所有适当的操作都可用。
* 作为[快速操作](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions);可用于单个片段卡的操作子集。

![操作](assets/cfm-managing-02.png)

选择片段以显示包含适用操作的工具栏：

* **重新处理资产**
* **创建**
* **下载**

   * 将片段另存为ZIP文件；您可以定义是否包含元素、变量、元数据。

* **签出**
* **属性**

   * 用于查看和/或编辑片段的元数据。

* **编辑**

   * 用于[打开片段以编辑内容](/help/assets/content-fragments/content-fragments-variations.md)及其元素、变体、关联内容和元数据。

* **快速发布**
* **管理发布**
* **管理标记**
* **目标收藏集**
* **复制** (并 **粘贴**)
* **移动**
* **删除**

>[!NOTE]
>
>其中许多操作是[资产](/help/assets/manage-digital-assets.md)和/或[AEM桌面应用程序](https://helpx.adobe.com/cn/experience-manager/desktop-app/aem-desktop-app.html)的标准操作。

## 打开片段编辑器 {#opening-the-fragment-editor}

要打开片段进行编辑，请执行以下操作：

>[!CAUTION]
>
>要编辑内容片段，您需要[相应的权限](/help/implementing/developing/extending/content-fragments-customizing.md#asset-permissions)。 如果您遇到问题，请联系您的系统管理员。

>[!CAUTION]
>
>要编辑内容片段，您需要相应的权限。 如果您遇到问题，请联系您的系统管理员。

1. 使用&#x200B;**Assets**&#x200B;控制台导航到内容片段的位置。
1. 通过以下任一方式打开片段进行编辑：

   * 单击/点按片段或片段链接（这取决于控制台视图）。
   * 选择片段，然后从工具栏中选择&#x200B;**编辑**。

1. 将打开片段编辑器。 根据需要进行更改：

   ![片段编辑器](assets/cfm-managing-03.png)

1. 进行更改后，根据需要使用&#x200B;**Save**、**Save &amp; close**&#x200B;或&#x200B;**Close**。

   >[!NOTE]
   >
   >**保存并关** 闭可通过保存下拉 **** 列表。

   >[!NOTE]
   >
   >**保存并关闭**&#x200B;和&#x200B;**关闭**&#x200B;将退出编辑器 — 有关各种选项如何对内容片段进行操作的完整信息，请参阅[保存、关闭和版本](#save-close-and-versions)。

## 内容片段编辑器中的模式和操作 {#modes-actions-content-fragment-editor}

内容片段编辑器中提供了多种模式和操作。

### 内容片段编辑器中的模式 {#modes-in-the-content-fragment-editor}

使用侧面板中的图标在各种模式中导航：

* 变体：[编辑内容](#editing-the-content-of-your-fragment)和[管理变量](#creating-and-managing-variations-within-your-fragment)

* [注释](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [关联的内容](#associating-content-with-your-fragment)
* [元数据](#viewing-and-editing-the-metadata-properties-of-your-fragment)
* [结构树](/help/assets/content-fragments/content-fragments-structure-tree.md)
* [预览](/help/assets/content-fragments/content-fragments-json-preview.md)

![模式](assets/cfm-managing-04.png)

### 内容片段编辑器中的工具栏操作 {#toolbar-actions-in-the-content-fragment-editor}

顶部工具栏中的某些功能可从多种模式中使用：

![模式](assets/cfm-managing-top-toolbar.png)

* 当内容页面上已引用片段时，将显示一条消息。 您可以&#x200B;**关闭**&#x200B;消息。

* 可使用&#x200B;**切换侧面板**&#x200B;图标隐藏/显示侧面板。

* 在片段名称下方，您可以看到用于创建当前片段的[内容片段模型](/help/assets/content-fragments/content-fragments-models.md)的名称：

   * 该名称还是一个将打开模型编辑器的链接。

* 查看片段的状态；例如，有关创建、修改或发布时间的信息。 状态也采用颜色编码：

   * **新增**:灰色
   * **草稿**:蓝色
   * **已发布**:绿色
   * **已修改**:橙色
   * **已停用**:红色

* **** 保存提供对保存并关 **闭选项** 的访问。

* 三个圆点(**...**)下拉列表提供对其他操作的访问：
   * **更新页面引用**
      * 这会更新任何页面引用。
   * **[快速发布](#publishing-and-referencing-a-fragment)**
   * **[管理发布](#publishing-and-referencing-a-fragment)**

<!--
This updates any page references and ensures that the Dispatcher is flushed as required. -->

## 保存、关闭和版本 {#save-close-and-versions}

>[!NOTE]
>
>也可以从时间轴](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments)中创建、比较和还原版本。[

编辑器具有各种选项：

* **** 保存并 **保存并关闭**

   * **** 保存将保存最新更改并保留在编辑器中。
   * **保存并关** 闭将保存最新更改并退出编辑器。

   >[!CAUTION]
   >
   >要编辑内容片段，您需要[相应的权限](/help/implementing/developing/extending/content-fragments-customizing.md#asset-permissions)。 如果您遇到问题，请联系您的系统管理员。

   >[!NOTE]
   >
   >在保存之前，可以保留在编辑器中并进行一系列更改。

   >[!CAUTION]
   >
   >除了仅保存您的更改外，这些操作还会更新任何引用，并确保Dispatcher按需要刷新。 这些更改可能需要一些时间才能处理。 因此，对于大型/复杂/重载系统，性能可能会受到影响。
   >
   >在使用&#x200B;**保存并关闭**&#x200B;后快速重新进入片段编辑器以进行和保存进一步更改时，请牢记这一点。

* **关闭**

   将退出编辑器，而不保存最新更改（即自上次&#x200B;**Save**&#x200B;以来所做的更改）。

在编辑内容片段时，AEM会自动创建版本，以确保在取消更改（使用&#x200B;**Close**&#x200B;而不保存）时可以恢复先前的内容：

1. 打开内容片段以编辑AEM时，会检查是否存在基于Cookie的令牌，该令牌指示是否存在编辑会话&#x200B;*:*

   1. 如果找到令牌，则该片段将被视为现有编辑会话的一部分。
   2. 如果令牌&#x200B;*不*&#x200B;可用，并且用户开始编辑内容，则会创建一个版本，并将此新编辑会话的令牌发送到客户端，并将其保存在Cookie中。

2. 当存在&#x200B;*活动*&#x200B;编辑会话时，每600秒会自动保存一次正在编辑的内容（默认）。

   >[!NOTE]
   >
   >可使用`/conf`机制配置自动保存间隔。
   >
   >默认值，请参阅：
   >  `/libs/settings/dam/cfm/jcr:content/autoSaveInterval`

3. 如果用户取消编辑，则会恢复在编辑会话开始时创建的版本，并删除令牌以结束编辑会话。
4. 如果用户选择&#x200B;**Save**&#x200B;编辑，则更新的元素/变量将被保留，并且令牌会被删除以结束编辑会话。

## 编辑片段的内容 {#editing-the-content-of-your-fragment}

打开片段后，可以使用[Variations](/help/assets/content-fragments/content-fragments-variations.md)选项卡创作内容。

## 创建和管理片段中的变量 {#creating-and-managing-variations-within-your-fragment}

创建主控内容后，即可创建和管理该内容的[变体](/help/assets/content-fragments/content-fragments-variations.md)。

## 将内容与片段关联 {#associating-content-with-your-fragment}

您还可以[将内容](/help/assets/content-fragments/content-fragments-assoc-content.md)与片段关联。 这提供了一个连接，以便在将资产（即图像）添加到内容页面时，可以（可选）与片段一起使用资产（即图像）。

## 查看和编辑片段的元数据（属性） {#viewing-and-editing-the-metadata-properties-of-your-fragment}

您可以使用[Metadata](/help/assets/content-fragments/content-fragments-metadata.md)选项卡查看和编辑片段的属性。

## 内容片段的时间轴 {#timeline-for-content-fragments}

除标准选项外， [时间轴](/help/assets/manage-digital-assets.md#timeline)还提供特定于内容片段的信息和操作：

* 查看有关版本、注释和批注的信息
* 版本操作

   * **[还原到此版本](#reverting-to-a-version)** （选择一个现有片段，然后选择特定版本）

   * **[与当前片段比较](#comparing-fragment-versions)** （选择一个现有片段，然后选择特定版本）

   * 添加&#x200B;**标签**&#x200B;和/或&#x200B;**注释**（选择现有片段，然后选择特定版本）

   * **另存为版本** （选择一个现有片段，然后向上箭头键在时间轴底部）

* 注释操作

   * **删除**

>[!NOTE]
评论包括：
* 所有资产的标准功能
* 在时间轴中制造
* 与片段资产相关

注释（适用于内容片段）包括：
* 在片段编辑器中输入
* 特定于片段中选定的文本区段



例如：

![时间线](assets/cfm-managing-05.png)

## 比较片段版本 {#comparing-fragment-versions}

选择特定版本后，**与当前比较**&#x200B;操作可从[时间轴](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments)中使用。

此时将打开：

* **当前**（最新）版本（左）

* 所选版本&#x200B;**v *x.y*>**（右）

它们将并排显示，其中：

* 任何差异都会突出显示

   * 已删除的文本 — 红色
   * 插入的文本 — 绿色
   * 替换文本 — 蓝色

* 全屏图标允许您自行打开任一版本；然后切换回并行视图
* 您可以&#x200B;**将**&#x200B;还原到特定版本
* **** Donewill会将您返回到控制台

>[!NOTE]
比较片段时无法编辑片段内容。

![比较](assets/cfm-managing-06.png)

## 还原到某个版本  {#reverting-to-a-version}

您可以还原到片段的特定版本：

* 直接从[时间轴](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments)访问。

   选择所需的版本，然后执行&#x200B;**还原到此版本**&#x200B;操作。

* 当[将某个版本与当前版本进行比较](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions)时，您可以&#x200B;**将**&#x200B;还原到选定的版本。

## 发布和引用片段 {#publishing-and-referencing-a-fragment}

>[!CAUTION]
如果您的片段基于模型，则应确保[模型已发布](/help/assets/content-fragments/content-fragments-models.md#publishing-a-content-fragment-model)。
如果发布的内容片段的模型尚未发布，则会显示一个选择列表来指示该情况，并且模型将随该片段一起发布。

必须发布内容片段才能在发布环境中使用。 它们可以发布：

* 创建后；使用资产控制台](#actions-for-a-content-fragment-assets-console)中可用的[操作。
* 从[内容片段编辑器](#toolbar-actions-in-the-content-fragment-editor)中。
* [发布使用片段](/help/sites-cloud/authoring/fundamentals/content-fragments.md#publishing)的页面时；片段将在页面引用中列出。

>[!CAUTION]
发布和/或引用片段后，当作者打开片段进行再次编辑时，AEM将显示警告。 这是为了警告，对片段所做的更改也会影响引用的页面。

## 删除片段 {#deleting-a-fragment}

要删除片段，请执行以下操作：

1. 在&#x200B;**资产**&#x200B;控制台中，导航到内容片段的位置。
2. 选择片段。

   >[!NOTE]
   **Delete**&#x200B;操作不可用作快速操作。

3. 从工具栏中选择&#x200B;**Delete**。
4. 确认&#x200B;**Delete**&#x200B;操作。

   >[!CAUTION]
   如果片段已在页面中被引用，您将看到一条警告消息，需要您确认是否继续执行&#x200B;**强制删除**。片段及其内容片段组件将从任何内容页面中删除。
