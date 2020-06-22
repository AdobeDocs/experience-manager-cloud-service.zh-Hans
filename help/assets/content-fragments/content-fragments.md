---
title: 使用内容片段
description: 了解Adobe Experience Manager(AEM)中的内容片段如何作为Cloud Service允许您设计、创建、策划和使用独立于页面的内容。
translation-type: tm+mt
source-git-commit: aefa7d6493ade255e06eaaa7676f8e018f311994
workflow-type: tm+mt
source-wordcount: '1804'
ht-degree: 7%

---


# 使用内容片段{#working-with-content-fragments}

With Adobe Experience Manager (AEM) as a Cloud Service, Content Fragments allow you to design, create, curate and [publish page-independent content](/help/sites-cloud/authoring/fundamentals/content-fragments.md). 它们允许您准备内容，准备好在多个位置／多个渠道使用。

内容片段包含结构化内容：

* 它们基于内容 [片段模型](/help/assets/content-fragments/content-fragments-models.md)，该模型为生成片段预定义结构。

使用AEM核心组件的Sling Model(JSON)导出功能，内容片段也可以以JSON格式交付。 这种投放:

* 使您能够使用组件管理片段中要传送的元素
* 允许批量投放，方法是在用于API投放的页面上添加多个内容片段核心组件

本页和以下各页涵盖创建、配置和维护内容片段的任务:

* [管理内容片段](/help/assets/content-fragments/content-fragments-managing.md) -创建您的内容片段； 然后，编辑、发布和引用
* [内容片段模型](/help/assets/content-fragments/content-fragments-models.md) -启用、创建和定义模型
* [变量——创作片段内容](/help/assets/content-fragments/content-fragments-variations.md) -创作片段内容并创建主片段的变量
* [Markdown](/help/assets/content-fragments/content-fragments-markdown.md) —— 为片段使用Markdown语法
* [使用关联内容](/help/assets/content-fragments/content-fragments-assoc-content.md) -添加关联内容
* [元数据——片段属性](/help/assets/content-fragments/content-fragments-metadata.md) -查看和编辑片段属性

>[!NOTE]
>
>这些页面应结合使用内容片 [段进行页面创作来阅读](/help/sites-cloud/authoring/fundamentals/content-fragments.md)。

通信渠道的数量每年都在增加。 通常，渠道指投放机制，如：

* 渠道; 例如，桌面、移动设备。
* 投放形式，以物理渠道; 例如，“产品详细信息页”、“产品类别页”（适用于桌面）或“移动网络”（适用于移动设备）、“移动应用程序”。

但是，您（可能）不希望对所有渠道使用完全相同的内容——您需要根据特定渠道优化您的内容。

内容片段允许您：

* 考虑如何跨目标有效地触及受众。
* 创建和管理渠道中性编辑内容。
* 为各种渠道构建内容池。
* 为特定渠道设计内容变体。
* 通过插入资产（混合媒体片段）将图像添加到文本。

然后，可以组合这些内容片段，以便在各种渠道上提供体验。

## 内容片段和内容服务 {#content-fragments-and-content-services}

AEM Content Services旨在将AEM中／来自内容的描述和投放概括到网页之外。

他们使用可供任何客户使用的标准化方法，向非传统AEM网页的渠道提供内容投放。 这些渠道可以包括：

* 单页应用程序
* 本机移动应用程序
* AEM外部的其他渠道和触点

投放是使用JSON导出器以JSON格式生成的。

AEM内容片段可用于描述和管理结构化内容。 结构化内容在可包含各种内容类型的模型中进行定义； 包括文本、数字数据、布尔值、日期和时间等。

此结构化内容与AEM核心组件的JSON导出功能一起，随后可用于将AEM内容交付给AEM页面以外的渠道。

>[!NOTE]
>
>**内容片段**&#x200B;和&#x200B;**[体验片段](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)**是 AEM 中的两个不同功能：
>* **内容片段**&#x200B;是可编辑的内容，主要为文本和相关图像。它们是纯内容，不带有任何设计和布局。
>* **体验片段**&#x200B;是经过充分布局的内容；例如，网页的一个片段。

>
>
体验片段可以包含内容片段形式的内容，反之则不行。
>
>有关更多信息，另请 [参阅了解AEM中的内容片段和体验片段](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/content-fragments-experience-fragments-article-understand.html)。

>[!NOTE]
>
>AEM还支持片段内容的转换。 有关更多信息，请参阅创建内容片段的翻译项目。

<!--
>[!NOTE]
>
>AEM also supports the translation of fragment content. See [Creating Translation Projects for Content Fragments](/help/assets/creating-translation-projects-for-content-fragments.md) for further information.
-->

## 内容类型 {#content-type}

内容片段包括：

* 存储为 **资产**:

   * 内容片段（及其变量）可以从“资产”控制台中创 **建和** 维护。
   * 在内容片段编辑器中创作和编辑。

* 通过内 [容片段组件(引用组件](/help/sites-cloud/authoring/fundamentals/content-fragments.md) )在页面编辑器中使用：

   * 内容 **片段组件** 可供页面作者使用。 它允许他们以HTML或JSON格式引用和提供所需的内容片段。

内容片段是一种内容结构，它：

* 没有布局或设计（在富文本模式下可以设置一些文本格式）。
* 包含一个或多个组成 [部分](#constituent-parts-of-a-content-fragment)。
* 可 [以包含或连接图像](#fragments-with-visual-assets)。
* 在页面 [上引用时](#in-between-content-when-page-authoring-with-content-fragments) ，可以使用中间内容。

* 独立于投放机制(即页面、渠道)。

### 具有可视资产的片段 {#fragments-with-visual-assets}

为了使作者能够更好地控制其内容，可以将图像添加到内容片段和／或与内容片段集成。

资产可以通过多种方式与内容片段一起使用； 各自有其优势：

* **将资产插入** 片段（混合媒体片段）

   * 是片段的一个完整部分(请参 [阅内容片段的组成部分](#constituent-parts-of-a-content-fragment))。
   * 定义资产的位置。
   * 有关 [详细信息，请参阅](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment) ：在片段编辑器中将资产插入片段。

   >[!NOTE]
   >
   >插入到内容片段本身中的可视资产会附加到前一段落。 将片段添加到页面时，在添加中间内容时，这些资产会与该段落相关移动。

* **关联的内容**

   * 连接到片段； 但不是片段的固定部分(请参 [阅内容片段的组成部分](#constituent-parts-of-a-content-fragment))。
   * 提供一定的定位灵活性。
   * 在页面上使用片段时，可轻松地使用（作为中间内容）。
   * 有关详 [细信息](/help/assets/content-fragments/content-fragments-assoc-content.md) ，请参阅关联内容。

* 页面编辑器的&#x200B;**资产浏览器**&#x200B;中的可用资产

   * 允许完全灵活地选择资产。
   * 提供一定的定位灵活性。
   * 不提供为特定片段批准的概念。
   * 有关更 [多信息](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser) ，请参阅资产浏览器。

### 内容片段的组成部分 {#constituent-parts-of-a-content-fragment}

内容片段资产由以下部分（直接或间接）组成：

* **片段元素**

   * 元素与包含内容的数据字段关联。
   * 您可以使用内容模型创建内容片段。 模型中指定的元素（字段）定义片段的结构。 这些元素（字段）可以是多种数据类型。

* **片段段落**

   * 文本块，即：

      * 由垂直空格分隔（回车）
      * 多行文本元素
   * 在富文 [本](/help/assets/content-fragments/content-fragments-variations.md#rich-text) 、标记 [下拉模式中](/help/assets/content-fragments/content-fragments-variations.md#markdown) ，段落可以格式化为标题，在这种情况下，它和以下段落同属一个单位。

   * 在页面创作过程中启用内容控制。


* **插入到片段（混合媒体片段）中的资产**

   * 插入到实际片段中并用作片段内部内容的资产（图像）。
   * 嵌入在片段的段落系统中。
   * 在页面上使用/ [引用片段时，可以设置格式](/help/sites-cloud/authoring/fundamentals/content-fragments.md)。
   * 只能使用片段编辑器添加到片段、从片段中删除片段或在片段中移动片段。 无法在页面编辑器中执行这些操作。
   * 只能在片段编辑器中使用富文本格式添加到片段、从片段 [中删除片段或在片段中移动](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment)。
   * 只能添加到多行文本元素（任何片段类型）。
   * 附加到前一文本（段落）。

   >[!CAUTION]
   >
   >可以切换为纯文本格式（无意中）从片段中删除。

   >[!NOTE]
   >
   >在页面上使用片 [段时，还可以将资产添加为](/help/sites-cloud/authoring/fundamentals/content-fragments.md#using-associated-content) 附加（中间）内容； 使用资产浏览器中的关联内容或资产。

* **关联的内容**

   * 这是片段外部的内容，但与片段的编辑相关。 通常是图像、视频或其他片段。
   * 将片段添加到页面时，集合中的单个资产可用于页面编辑器中的片段。 这意味着它们是可选的，具体取决于特定渠道的要求。
   * 资产通过集 [合与片段关联](/help/assets/content-fragments/content-fragments-assoc-content.md); 关联的集合允许作者决定在创作页面时要使用哪些资产。

      * 集合可以作为默认内容与片段关联，也可以由作者在片段创作过程中关联。
      * [资产(DAM)集合](/help/assets/manage-collections.md) 是片段关联内容的基础。
   * （可选）您也可以将片段本身添加到集合以帮助跟踪。

* **片段元数据**

   * 使用资产 [元数据模式](/help/assets/metadata-schemas.md)。
   * 在以下情况下可以创建标记：

      * 创建和创作片段
      * 或更高版本：

         * 通过从控制台查看／编 **辑片段** “属性”
         * 在片段编辑 **器中** ，通过编辑元数据

   >[!CAUTION]
   >
   >元数据处理用户档案不适用于内容片段。

* **母版**

   * 碎片的一个完整部分

      * 每个内容片段都有一个主实例。
      * 无法删除主视图。
   * 在片段编辑器中的变量下可访问 **[主节](/help/assets/content-fragments/content-fragments-variations.md)**。
   * “主”不是变体，而是所有变体的基础。


* **变量**

   * 特定于编辑目的的片段文本的呈现； 可以与渠道相关，但不是强制性的，也可以是临时本地修改。
   * 创建为主页的副 **本**，但之后可以根据需要进行编辑； 这些变体之间通常存在内容重叠。
   * 可以在片段创作过程中定义。
   * 存储在片段中，以帮助避免内容副本的散布。
   * 如果主内 [容已更新](/help/assets/content-fragments/content-fragments-variations.md#synchronizing-with-master) ，则可以与主内容同步变量。
   * 可以进行 [汇总](/help/assets/content-fragments/content-fragments-variations.md#summarizing-text) ，以将文本快速截断到预定义的长度。
   * 可在片段编 [辑器](/help/assets/content-fragments/content-fragments-variations.md) 的“变量”选项卡下找到。

### 使用内容片段进行页面创作时的中间内容 {#in-between-content-when-page-authoring-with-content-fragments}

中间内容：

* 可在处理内容片段时在页面编辑器中使用。
* 是 [否在片段流中使用](/help/sites-cloud/authoring/fundamentals/content-fragments.md#adding-in-between-content) /引用其后添加其他内容。
* 在处理内容片段时， [可在页面编辑器中使用](/help/sites-cloud/authoring/fundamentals/content-fragments.md)。
* 中间内容可以添加到任何片段，其中只有一个可见元素。
* 可以使用相关内容，也可以使用相应浏览器中的资产和／或组件。

>[!CAUTION]
>
>中间内容是页面内容。它不会存储在内容片段中。

### 片段要求 {#required-by-fragments}

要创建、编辑和使用内容片段，您还需要：

* **内容模型**

   * 启 [用，然后使用工具创建](/help/assets/content-fragments/content-fragments-models.md)。
   * 创建结 [构化片段时必需](/help/assets/content-fragments/content-fragments-managing.md#creating-content-fragments)。
   * 定义片段的结构（标题、内容元素、标记定义）。
   * 内容模型定义需要标题和一个数据元素； 其他一切都是可选的。 模型定义片段和默认内容的最小范围（如果适用）。 创作片段内容时，作者无法更改定义的结构。

* **内容片段组件**

   * 有助于以HTML和／或JSON格式传送片段。
   * 在页面 [上引用片段时必需](/help/sites-cloud/authoring/fundamentals/content-fragments.md)。
   * 负责片段的布局和投放; 即渠道。
   * 片段需要一个或多个专用组件来定义布局，并提供一些或所有元素／变量和相关内容。
   * 在创作过程中将片段拖到页面上将自动关联所需的组件。

## 示例使用 {#example-usage}

片段及其元素和变量可用于为多个渠道创建一致的内容。 在设计片段时，您需要考虑将在何处使用什么。

### WKND示例 {#wknd-sample}

WKND [站点示例](/help/implementing/developing/introduction/develop-wknd-tutorial.md) ，可帮助您了解AEM作为Cloud Service。 它包含示例片段，可在以下位置查看：

`hhttp://<host>:<port>/assets.html/content/dam/wknd/en/adventures`
