---
title: 管理内容片段
description: 内容片段存储为资产，因此主要通过“资产”控制台进行管理。
translation-type: tm+mt
source-git-commit: f5dd39bd7379d56c4f7b5e180d35892ba1dd4da1

---


# 管理内容片段{#managing-content-fragments}

内容片段存储为资 **产**，因此主要通过“资产”控制台 **进行管理** 。

>[!NOTE]
>
>内容片段随后用于创作页面；请参 [阅使用内容片段进行页面创作](/help/sites-cloud/authoring/fundamentals/content-fragments.md)。

## 创建内容片段 {#creating-content-fragments}

### 创建内容模型 {#creating-a-content-model}


[在创建包含结构化内容的内容片段之前](/help/assets/content-fragments/content-fragments-models.md) ，可以启用和创建内容片段模型。

### 创建内容片段 {#creating-a-content-fragment}

创建内容片段的方法（基本上）对于简单片段和结构化片段都是相同的：

1. 导航到要 **创建片段** 的Assets文件夹。
2. 选择 **创建**，然后选择 **内容片段** ，以打开向导。
3. 向导的第一步要求您指定新片段的基础。

   * 这可以是：

      * 简单 **片段模板**

      * [模型](/help/assets/content-fragments/content-fragments-models.md) -用于创建需要结构化内容的片段；例如机 **场模型**

         * 将显示所有可用型号。
   选择后，使用“下 **一步** ”继续。

   ![片段基础](assets/cfm-managing-01.png)

4. 在属性 **步骤中** ，指定：

   * **基本**

      * **标题**

         片段标题。

         强制.

      * **描述**

      * **标记**
   * **高级**

      * **名称**

         姓名；将用于形成URL。

         强制；将自动从标题派生，但可以更新。


5. 选 **择创建** ，以完成操作，然后打开片段 **进行编辑** ，或返回控制台并执行完 **成**。

## 内容片段的操作 {#actions-for-a-content-fragment}

在“资 **产** ”控制台中，您的内容片段可以执行一系列操作：

* 工具栏中；选择片段后，所有相应的操作都可用。
* 作为 [快速行动](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions);可用于单个片段卡的操作子集。

![动作](assets/cfm-managing-02.png)

选择片段以显示包含适用操作的工具栏：

* **创建**
* **下载**

   * 将片段另存为ZIP文件；您可以定义是否包括元素、变量、元数据。

* **签出**
* **属性**

   * 允许您视图和／或编辑片段的元数据。

* **编辑**

   * 允许您打开片 [段以编辑内容](/help/assets/content-fragments/content-fragments-variations.md) ，以及其元素、变量、关联内容和元数据。

* **管理标记**
* **目标收藏集**

   * 将片段添加到集合。
   * 在将集合与片段关 [联时也可以执行此操作](/help/assets/content-fragments/content-fragments-assoc-content.md#adding-associated-content)。

* **复制**/粘&#x200B;**贴**

* **移动**
* **快速发布**
* **管理发布**
* **删除**

>[!NOTE]
>
>其中许多操作 [是Assets和](/help/assets/manage-digital-assets.md) /或 [AEM桌面应用程序的标准操作](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html)。

## 打开片段编辑器 {#opening-the-fragment-editor}

要打开片段进行编辑，请执行以下操作：

>[!CAUTION]
>
>要编辑内容片段，您需要 [相应的权限](/help/implementing/developing/extending/content-fragments-customizing.md#asset-permissions)。 如果您遇到问题，请联系您的系统管理员。

>[!CAUTION]
>
>要编辑内容片段，您需要相应的权限。 如果您遇到问题，请联系您的系统管理员。

1. 使用“ **资产** ”控制台导航到内容片段的位置。
2. 通过以下任一方式打开片段进行编辑：

   * 单击／点按片段或片段链接(这取决于控制台视图)。
   * 选择片段，然后从工 **具栏中** “编辑”。
   片段编辑器将打开：

   ![片段编辑器](assets/cfm-managing-03.png)

   >[!NOTE]
   >
   >1. 当内容页面上已引用片段时，将显示一条消息。
      >
      >
      >

   2. 可使用“切换侧面板”图标隐藏／显 **示侧面板** 。


3. 使用侧面板中的图标在三种模式之间导航：

   * 变量：编 [辑内容和](#editing-the-content-of-your-fragment) 管 [理变量](#creating-and-managing-variations-within-your-fragment)

   * [注释](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
   * [关联的内容](#associating-content-with-your-fragment)
   * [元数据](#viewing-and-editing-the-metadata-properties-of-your-fragment)
   ![模式](assets/cfm-managing-04.png)

4. 进行更改后，根据需要 **使用** “保 **存”或“取消** ”。

   >[!NOTE]
   >
   >“保 **存** ”和“取消 **”将退出编辑器——有关这两个选项如何对内容片段进行操作的完整信息，请参阅**[](#save-cancel-and-versions) “保存”、“取消”和“版本”。

## 保存、取消和版本 {#save-cancel-and-versions}

>[!NOTE]
>
>还可以从时间 [轴创建、比较和还原版本](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments)。

该编辑器有两个选项：

* **保存**

   将保存最新更改并退出编辑器。

   >[!CAUTION]
   >
   >要编辑内容片段，您需要 [相应的权限](/help/implementing/developing/extending/content-fragments-customizing.md#asset-permissions)。 如果您遇到问题，请联系您的系统管理员。

   >[!NOTE]
   >
   >在选择“保存”之前，可以保留在编辑器中并进行一系列 **更改**。

   >[!CAUTION]
   >
   >除了简单地保存更改外，“保 **存** ”还会更新任何引用，并确保调度程序根据需要被刷新。 这些更改可能需要时间进行处理。 因此，对于大型／复杂／重负载的系统，可能会产生性能影响。
   >
   >
   >使用“保存”时请牢记这 **一点** ，然后快速重新输入片段编辑器以进行和保存进一步的更改。

* **取消**

   将退出编辑器，而不保存最新更改。

在编辑内容片段时，AEM会自动创建版本，以确保在取消更改时可以恢复以 **前的** 内容：

1. 打开内容片段进行编辑时，AEM会检查是否存在基于cookie的令牌，该令牌指示编辑会 *话是否存在* :

   1. 如果找到令牌，则片段被视为现有编辑会话的一部分。
   2. 如果令牌不可用 ** ，且用户开始编辑内容，则会创建一个版本，并将此新编辑会话的令牌发送到客户端，在客户端中，该令牌保存在cookie中。

2. 当存在活动的编 *辑会话* ，所编辑的内容会每600秒（默认）自动保存一次。

   >[!NOTE]
   >
   >使用该机制可以配置自动保存 `/conf` 间隔。
   >
   >默认值，请参阅：
   >  `/libs/settings/dam/cfm/jcr:content/autoSaveInterval`

3. 如果用户选择取 **消编辑** ，则恢复在编辑会话的开始中创建的版本，并删除令牌以结束编辑会话。
4. 如果用户选择“保 **存** ”编辑，则更新的元素／变量将被保留，并删除令牌以结束编辑会话。

## 编辑片段内容 {#editing-the-content-of-your-fragment}

打开片段后，可以使用“变量” [选项卡](/help/assets/content-fragments/content-fragments-variations.md) ，创作内容。

## 在片段中创建和管理变量 {#creating-and-managing-variations-within-your-fragment}

创建主内容后，您便可以创建和管理该内容 [的变](/help/assets/content-fragments/content-fragments-variations.md) 体。

## 将内容与片段关联 {#associating-content-with-your-fragment}

您还可以将 [内容与片段](/help/assets/content-fragments/content-fragments-assoc-content.md) 关联。 这提供了一个连接，以便在将资产（即图像）添加到内容页面时，可以（可选）与片段一起使用。

## 查看和编辑片段的元数据（属性） {#viewing-and-editing-the-metadata-properties-of-your-fragment}

您可以使用“元数据”选项卡视图和编辑片段 [的属](/help/assets/content-fragments/content-fragments-metadata.md) 性。

## 内容片段的时间轴 {#timeline-for-content-fragments}

除了标准选项之外，时间轴还 [提供特定于内容片段的信息](/help/assets/manage-digital-assets.md#timeline) 和操作：

* 视图有关版本、注释和注释的信息
* 版本操作

   * **[还原到此版本](#reverting-to-a-version)**（选择现有片段，然后选择特定版本）

   * **[与当前版本比较](#comparing-fragment-versions)**（先选择一个现有片段，然后选择特定版本）

   * 添加标 **签和** /或 **评论** （选择现有片段，然后选择特定版本）

   * **另存为版本** （选择现有片段，然后选择时间轴底部的向上箭头）

* 注释操作

   * **删除**

>[!NOTE]
评论包括：
* 适用于所有资产的标准功能
* 在时间轴中制作
* 与片段资产相关

注释（针对内容片段）包括：
* 在片段编辑器中输入
* 特定于片段中的选定文本段



例如：

![时间轴](assets/cfm-managing-05.png)

## 比较片段版本 {#comparing-fragment-versions}

在 **选择特定版本后** ，时间轴中可 [以执行](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments) “与当前版本比较”操作。

此选项将打开：

* 当 **前** （最新）版本（左）

* 所选版 **本v&lt;*x.y*>** （右）

它们将并排显示，其中：

* 所有差异都会高亮显示

   * 删除的文本——红色
   * 插入的文本——绿色
   * 替换文本——蓝色

* 全屏图标允许您自行打开任一版本；然后切换回并行视图
* 您可以 **还原到** 特定版本
* **完成** ，将返回控制台

>[!NOTE]
在比较片段时，无法编辑片段内容。

![比较](assets/cfm-managing-06.png)

## Reverting to a Version  {#reverting-to-a-version}

您可以还原到片段的特定版本：

* 直接从时间 [轴](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments)。

   选择所需的版本，然后执 **行还原到此版本操作** 。

* 将某 [个版本与当前版本进行比较时](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions) ，您可 **以还原到选定版本** 。

## 发布和引用片段 {#publishing-and-referencing-a-fragment}

>[!CAUTION]
如果您的片段基于模型，则应确保该 [模型已发布](/help/assets/content-fragments/content-fragments-models.md#publishing-a-content-fragment-model)。
如果发布的内容片段尚未发布模型，则会显示一个选择列表，指示此情况，并且模型将随片段一起发布。

必须发布内容片段才能在发布环境中使用。 可以发布它们：

* 创建后；从“资 **产** ”控制台。
* 当您发 [布使用片段的页面时](/help/sites-cloud/authoring/fundamentals/content-fragments.md#publishing);片段将列在页面引用中。

>[!CAUTION]
在发布和／或引用片段后，当作者打开片段以再次进行编辑时，AEM将显示一条警告消息。 这将警告对片段所做的更改也会影响引用的页面。

## 删除片段 {#deleting-a-fragment}

要删除片段，请执行以下操作：

1. 在“资 **产** ”控制台中，导航到内容片段的位置。
2. 选择片段。

   >[!NOTE]
   The **Delete** action is not available as a quick action.

3. Select **Delete** from the toolbar.
4. 确认删 **除** 。

   >[!CAUTION]
   如果片段已在页面中被引用，您将看到一条警告消息，需要您确认是否继续执行&#x200B;**强制删除**。片段及其内容片段组件将从任何内容页面中删除。
