---
title: 内容片段
description: Adobe Experience Manager as a Cloud Service 内容片段允许您设计、创建、策划和使用独立于页面的内容
exl-id: 7a44fc4e-3793-4aa3-8c21-db0567c93244
source-git-commit: 3d20f4bca566edcdb5f13eab581c33b7f3cf286d
workflow-type: ht
source-wordcount: '1286'
ht-degree: 100%

---

# 内容片段 {#content-fragments}

Adobe Experience Manager (AEM) as a Cloud Service 中的内容片段是[作为独立于页面的资源创建和管理的](/help/sites-cloud/administering/content-fragments/overview.md)。

这允许您创建渠道中性内容，以及各种（特定于渠道的）变体。您随后可以在创作内容页面时使用这些片段及其变体。

结构化内容片段与更新的 JSON 导出程序结合使用时，还可用于通过 Content Services 将 AEM 内容传送到 AEM 页面以外的渠道。

>[!NOTE]
>
>内容片段是一项&#x200B;**站点**&#x200B;功能，但存储为&#x200B;**资源**。
>
>现在主要用&#x200B;**[内容片段](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console)**&#x200B;控制台管理它们，但仍可从&#x200B;**[资源](/help/assets/content-fragments/content-fragments-managing.md)**&#x200B;控制台管理它们。
>
>有两个编辑器用于创作内容片段：
>
>* 主要从&#x200B;**内容片段**&#x200B;控制台访问[内容片段 - 创作](/help/sites-cloud/administering/content-fragments/authoring.md)的新编辑器。
>* 主要从&#x200B;**资源**&#x200B;控制台访问[原始编辑器](/help/assets/content-fragments/content-fragments-variations.md)。

>[!NOTE]
>
>**内容片段**&#x200B;和&#x200B;**[体验片段](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)**&#x200B;是 AEM 中的两个不同功能：
>* **内容片段**&#x200B;是可编辑内容，具有定义和结构，但无需额外的可视设计和/或布局。它们可用于访问结构化数据，包括文本、数字和日期等。
>* **体验片段**&#x200B;是经过充分布局的内容；例如，网页的一个片段。
>
>体验片段可以包含内容片段形式的内容，反之则不行。
>
>有关更多信息，请参见[了解 AEM 中的内容片段和体验片段](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html#content-fragments)。

>[!CAUTION]
>
>本页必须结合[使用内容片段](/help/sites-cloud/administering/content-fragments/overview.md)（及相关页面）一起阅读，因为它不仅介绍了基本术语和概念，还介绍了如何创建和管理片段。

内容片段允许：

* **营销和营销活动策略**
   * 通过集中管理的内容片段审核内容。
* **Creative Pro**
   * 通过与内容片段关联的收藏集跟踪创意资源。
* **撰稿人**
   * 在 AEM 内容片段编辑器中编写。
   * 可以创建内容变体。
   * 可以将相关内容与内容片段关联。
   * 可以使用版本控制/工作流。
   * 可以共享内容片段。
   * 可以集中管理翻译。
* **生成器和旅行管理器**
   * 从 AEM 内的预定义片段和具有创作功能的变体中选择。
   * 可以依赖始终保持最新的片段和关联内容，因为撰稿人和创意人员会在集中管理的片段和资源中进行更新。
   * 可以依赖为了相关性而进行管理的关联媒体内容。
   * 可以快速创建随机内容变体，同时仍然确保这些变体在片段中受到集中管理。

## 将内容片段添加到您的页面 {#adding-a-content-fragment-to-your-page}

1. 打开您的页面进行编辑。
2. 添加&#x200B;**内容片段**&#x200B;组件；通过&#x200B;**组件**&#x200B;浏览器或&#x200B;**插入新组件**。
3. 您可以：
   * 打开&#x200B;**资源**&#x200B;浏览器并筛选&#x200B;**内容片段**（默认为图像）。然后，将所需的片段拖到组件实例上。
   * 选择内容片段组件，然后从工具栏中选择&#x200B;**配置**。在对话框中，您可以打开选择对话框以浏览并选择所需的&#x200B;**内容片段**。

   >[!NOTE]
   >
   >备选方法是将特定的内容片段直接拖到页面上。这将自动创建关联的组件（内容片段）。

4. 最初会显示&#x200B;**主**&#x200B;元素和&#x200B;**母版**（变体）中的内容。您可以根据需要[选择其他元素和/或变体](#selecting-the-element-or-variation)。

   ![资源浏览器中的内容片段](/help/sites-cloud/authoring/assets/content-fragments.png)

   >[!NOTE]
   >
   >有关其他编辑功能的更多信息，另请参阅：
   >
   >* [响应式布局](/help/sites-cloud/authoring/features/responsive-layout.md)
   >* [编辑页面内容](/help/sites-cloud/authoring/fundamentals/editing-content.md)

### 选择元素或变体 {#selecting-the-element-or-variation}

打开片段的&#x200B;**配置**&#x200B;对话框以配置片段在当前页面上使用。该对话框取决于所使用的组件。

>[!NOTE]
>
>另请参阅[核心组件和内容片段组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=zh-Hans)

在相应的配置对话框中，您可以选择可用的参数，包括：

* **内容片段**
   * 指定要使用的片段。
* **显示模式**：
   * **单个文本元素**
   * **多个元素**
* **元素**
   * 可用的选项取决于所使用的模型。

  >[!NOTE]
  >
  >可用的元素取决于所使用的模型。

* **变体**
   * 默认&#x200B;**主要视图**&#x200B;始终可用。
   * 如果变体是为片段而创建的，则有可选择的变体可用。

* **ID**

   * 应用于组件的 **HTML ID** 属性。

### 到片段编辑器的快速连接 {#quick-connection-to-fragment-editor}

您可以打开片段源，以使用组件工具栏中的&#x200B;**编辑**&#x200B;图标编辑（资源）。这将允许您[编辑和管理内容片段](/help/sites-cloud/administering/content-fragments/overview.md)。

>[!CAUTION]
>
>通常情况下，编辑片段源将会影响引用该内容片段的所有页面。

### 添加中间内容 {#adding-in-between-content}

当指定的内容片段被添加到页面时，在片段的每个 HTML 段落之间（和顶部/底部）会有一个&#x200B;**将组件拖动到此处**&#x200B;占位符。

这使您在片段内容[中间](/help/assets/content-fragments/content-fragments.md#in-between-content-when-page-authoring-with-content-fragments)的任何可用位置添加额外内容（即中间内容），而无需更改根片段。

对于中间内容，您可以：

* 从[组件浏览器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser)添加组件。
* 从[资源浏览器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser)添加资源。
* 使用[关联内容](#using-associated-content)作为中间内容的源。

>[!CAUTION]
>
>中间内容是页面内容。它不会存储在内容片段中。

![插入组件](/help/sites-cloud/authoring/assets/content-fragments-insert.png)

>[!NOTE]
>
>您还可以[在片段本身中插入可视资源（图像）](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment)。
>
>在片段本身中插入的可视资源会附加到片段中的前一段落后面。这意味着无法在可视资源与前一段落之间放置中间内容。如果需要达到此关联程度，可以将图像添加到片段（形成[混合媒体片段](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets)）。

>[!CAUTION]
>
>在将中间内容添加到页面上的内容片段之后，更改基础内容片段的结构（例如在内容片段编辑器中）可能会导致错误/意外的结果。
>
>在发生此问题时，中间内容会按原样保留：
>
>* 中间组件在片段流的组件序列中具有一个绝对位置。即使片段中段落的内容发生更改，此位置也不会变化。
>
>  这可能使其看起来像是相对位置发生了更改一样，因为中间段落与它们旁边的（片段）段落之间没有上下文关系。
>* 除非两个段落结构产生冲突；在这种情况下，将不会显示中间内容（尽管它在内部依然存在）。

### 使用关联内容 {#using-associated-content}

如果您有与[内容片段](/help/assets/content-fragments/content-fragments.md)[关联的内容](/help/sites-cloud/administering/content-fragments/content-fragments-assoc-content.md)，则这些资源在侧面板（在将片段放置到内容页面后）中可用。关联内容实际上是[中间内容](/help/assets/content-fragments/content-fragments.md#in-between-content-when-page-authoring-with-content-fragments)的特殊内容源。

>[!NOTE]
>
>可以通过多种方法向片段和/或页面中添加[可视资源（例如图像）](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets)。

>[!NOTE]
>
>如果您在一个页面中拥有多个内容片段，**关联内容**&#x200B;选项卡将显示适用于所有片段的资源。

在将具有关联内容的片段添加到页面之后，将会在侧面板中打开一个新的选项卡（**关联内容**）。

从此处，您可以将资源拖到所需的位置（可以是一个现有的组件，或是在其中创建合适组件的所需位置）：

![插入图像](/help/sites-cloud/authoring/assets/content-fragments-image.png)

### 插入到片段中的资源 {#assets-inserted-into-the-fragment}

如果已在片段本身中插入资源（例如，图像）形成[混合媒体片段](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets)，则页面编辑器中用于编辑这些资源的选项会受到限制。

例如，您可以对图像执行以下操作

* 裁切、旋转或翻转图像。
* 添加标题或替换文本。
* 指定大小。
* 您还可以配置版面。

移动、复制和删除等其他更改必须在片段编辑器中进行。

### 发布 {#publishing}

片段需要发布，才能在您已发布的网页中使用。

* [在内容片段控制台](/help/sites-cloud/administering/content-fragments/managing.md#publishing-and-previewing-a-fragment)中创建片段后，可以发布片段。
* 如果在当前发布的页面中使用了&#x200B;*未发布的片段*，那么也可以在这一时候发布该片段。

## 导出内容片段 {#exporting-content-fragments}

要导出到 Adobe Target，可使用 JSON 交付片段。请参阅：

* [与 Adobe Target 集成](/help/sites-cloud/integrating/integrating-adobe-target.md)
* [将内容片段导出到 Adobe Target](/help/sites-cloud/integrating/content-fragments-target.md)
