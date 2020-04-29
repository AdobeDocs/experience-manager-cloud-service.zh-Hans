---
title: 使用内容片段
description: 了解Adobe Experience Manager(AEM)中的内容片段如何作为云服务允许您设计、创建、管理和使用独立于页面的内容。
translation-type: tm+mt
source-git-commit: c93dfd1ca50933416de1eee7d6d4f820c30afa49

---


# 使用内容片段{#working-with-content-fragments}

With Adobe Experience Manager (AEM) as a Cloud Service, Content Fragments allow you to design, create, curate and [publish page-independent content](/help/sites-cloud/authoring/fundamentals/content-fragments.md). 它们允许您准备内容，准备好在多个位置／多个渠道中使用。

使用AEM核心组件的Sling Model(JSON)导出功能，内容片段也可以以JSON格式交付。 这种投放:

* 允许您使用组件管理片段中要传送的元素
* 允许批量投放，方法是在用于API投放的页面上添加多个内容片段核心组件

本页和以下各页涵盖创建、配置和维护内容片段的任务:

* [管理内容片段](/help/assets/content-fragments/content-fragments-managing.md) -创建您的内容片段；然后编辑、发布和引用
* [内容片段模型](/help/assets/content-fragments/content-fragments-models.md) -启用、创建和定义模型
* [变量——创作片段内容](/help/assets/content-fragments/content-fragments-variations.md) -创作片段内容并创建主节点的变量
* [Markdown](/help/assets/content-fragments/content-fragments-markdown.md) —— 对片段使用Markdown语法
* [使用关联内容](/help/assets/content-fragments/content-fragments-assoc-content.md) -添加关联内容
* [元数据——片段属性](/help/assets/content-fragments/content-fragments-metadata.md) -查看和编辑片段属性

>[!NOTE]
>
>这些页面应结合使用内容片段 [进行页面创作来读取](/help/sites-cloud/authoring/fundamentals/content-fragments.md)。

通信渠道的数量每年都在增加。 通常，渠道指投放机制，如下所示：

* 身体渠道;例如，桌面、移动设备。
* 投放形式；例如，“产品详细信息页”、“产品类别页”（适用于桌面）或“移动Web”（适用于移动设备的移动应用程序）。

但是，您（可能）不希望对所有渠道使用完全相同的内容——您需要根据特定渠道优化您的内容。

内容片段允许您：

* 考虑如何跨渠道有效地触及目标受众。
* 创建和管理不含渠道的编辑内容。
* 为各种渠道构建内容池。
* 为特定渠道设计内容变体。
* 通过插入资产（混合媒体片段）将图像添加到文本中。

然后，可以组合这些内容片段，以便在各种渠道上提供体验。

## 内容片段和内容服务 {#content-fragments-and-content-services}

AEM Content Services旨在将AEM中／来自AEM的内容的描述和投放概括为超出对网页的关注范围。

它们使用可供任何客户使用的标准化方法，向非传统AEM网页的渠道提供内容投放。 这些渠道包括：

* 单页应用程序
* 本机移动应用程序
* AEM外部的其他渠道和触点

投放采用JSON格式。

AEM内容片段可用于描述和管理结构化内容。 结构化内容在可包含各种内容类型的模型中进行定义；包括文本、数字数据、布尔值、日期和时间等。

此结构化内容与AEM核心组件的JSON导出功能一起可用于将AEM内容交付给AEM页面以外的渠道。

>[!NOTE]
>
>**内容片段**&#x200B;和&#x200B;**[体验片段](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)**是 AEM 中的两个不同功能：
>* **内容片段**&#x200B;是可编辑的内容，主要为文本和相关图像。它们是纯内容，不带有任何设计和布局。
>* **体验片段**&#x200B;是经过充分布局的内容；例如，网页的一个片段。
>
>
体验片段可以包含内容片段形式的内容，反之则不行。
>
>有关详细信息，另请参 [阅了解AEM中的内容片段和体验片段](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/content-fragments-experience-fragments-article-understand.html)。

>[!CAUTION]
>
>内容片段在经典UI中不可用。
>
>内容片段组件可在经典UI Sidekick中查看，但其他功能不可用。

>[!NOTE]
>
>AEM还支持片段内容的翻译。 有关更多信息，请参阅创建内容片段的翻译项目。

<!--
>[!NOTE]
>
>AEM also supports the translation of fragment content. See [Creating Translation Projects for Content Fragments](/help/assets/creating-translation-projects-for-content-fragments.md) for further information.
-->

## 内容片段的类型 {#types-of-content-fragment}

内容片段可以是：

* 简单片段

   * 它们没有预定义的结构。

   * 它们仅包含文本和图像。

   * 这些模板基于简 **单片段模板** 。

* 包含结构化内容的片段

   * 这些代码基于内容 [片段模型](/help/assets/content-fragments/content-fragments-models.md)，该模型为生成的片段预定义了结构。

   * 这些组件还可用于使用JSON导出器实现内容服务。

## 内容类型 {#content-type}

内容片段包括：

* 存储为 **资产**:

   * 内容片段（及其变体）可以从“资产”控制台中创建和 **维护** 。
   * 在内容片段编辑器中创作和编辑。

* 在页面编 [辑器中通过内容片段组件](/help/sites-cloud/authoring/fundamentals/content-fragments.md) （引用组件）使用：

   * 内容 **片段组件** 可供页面作者使用。 它允许他们以HTML或JSON格式引用和交付所需的内容片段。

内容片段是一种内容结构，它：

* 没有布局或设计（在富文本模式下可以设置一些文本格式）。
* 包含一个或多个组成 [部分](#constituent-parts-of-a-content-fragment)。
* 可 [以包含或连接到图像](#fragments-with-visual-assets)。
* 在页面 [上引用时](#in-between-content-when-page-authoring-with-content-fragments) ，可以使用中间内容。

* 独立于投放机制(即页面、渠道)。

### 带有可视资产的片段 {#fragments-with-visual-assets}

为了使作者能够更好地控制其内容，可以将图像添加到内容片段和／或与其集成。

资产可以通过多种方式与内容片段一起使用；每个都有自己的优势：

* **将资产插入** （混合媒体片段）

   * 是片段的一个组成部分(请参 [阅内容片段的组成部分](#constituent-parts-of-a-content-fragment))。
   * 定义资产的位置。
   * 有关 [详细信息，请参阅在片段编辑器中将资产插入片段](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment) 。
   >[!NOTE]
   >
   >插入到内容片段本身中的可视资产将附加到前一段落。 将片段添加到页面时，在添加中间内容时，这些资产会相对于该段落移动。

* **关联的内容**

   * 连接到片段；但不是片段的固定部分(请参 [阅内容片段的组成部分](#constituent-parts-of-a-content-fragment))。
   * 为定位提供了一定的灵活性。
   * 在页面上使用片段时，可轻松地使用（作为中间内容）。
   * 有关详 [细信息](/help/assets/content-fragments/content-fragments-assoc-content.md) ，请参阅关联内容。

* 页面编辑器的&#x200B;**资产浏览器**&#x200B;中的可用资产

   * 允许完全灵活地选择资产。
   * 为定位提供了一定的灵活性。
   * 不提供特定片段的批准概念。
   * 有关更 [多信息，请参阅](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser) “资产浏览器”。

### 内容片段的组成部分 {#constituent-parts-of-a-content-fragment}

内容片段资产由以下部分（直接或间接）组成：

* **片段元素**

   * 元素与包含内容的数据字段相关联。
   * 对于具有结构化内容的片段，可以使用内容模型创建内容片段。 在模型中指定的元素（字段）定义片段的结构。 这些元素（字段）可以是多种数据类型。
   * 对于简单的片段：

      * 内容保存在一个或多个多行文本字段或元素中。
      * 元素在简单片段模 **板中定义** 。

* **片段段落**

   * 文本块，即：

      * 由垂直空格（回车）分隔
      * 在多行文本元素中；在简单或结构化片段中
   * 在富文 [本](/help/assets/content-fragments/content-fragments-variations.md#rich-text) 、标记 [下拉模式中](/help/assets/content-fragments/content-fragments-variations.md#markdown) ，段落可以格式化为标题，在这种情况下，它和以下段落同属一个单位。

   * 在页面创作过程中启用内容控制。


* **插入到片段（混合媒体片段）中的资产**

   * 已插入到实际片段中并用作片段内部内容的资产（图像）。
   * 嵌入到片段的段落系统中。
   * 在页面上使用/ [引用片段时，可以设置格式](/help/sites-cloud/authoring/fundamentals/content-fragments.md)。
   * 只能使用片段编辑器添加到片段、从片段中删除片段或在片段中移动片段。 无法在页面编辑器中执行这些操作。
   * 只能使用片段编辑器中的富文本格式添加到片段、从片段中删除 [片段或在片段中移动](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment)。
   * 只能添加到多行文本元素（任何片段类型）。
   * 附加到前面的文本（段落）。
   >[!CAUTION]
   >
   >可以（无意中）通过切换为纯文本格式从片段中删除。

   >[!NOTE]
   >
   >在页面上使用片 [段时](/help/sites-cloud/authoring/fundamentals/content-fragments.md#using-associated-content) ，还可以将资产添加为附加（中间）内容；使用关联内容或资产浏览器中的资产。

* **关联的内容**

   * 这是片段外部的内容，但与片段的编辑相关。 通常是图像、视频或其他片段。
   * 将集合中的单个资产添加到页面时，这些资产可用于页面编辑器中的片段。 这意味着，根据特定渠道的要求，这些选项是可选的。
   * 资产通过集 [合与片段关联](/help/assets/content-fragments/content-fragments-assoc-content.md);关联的集合允许作者决定在创作页面时要使用哪些资产。

      * 集合可以作为默认内容与片段相关联，也可以由作者在片段创作过程中关联。
      * [资产(DAM)集合](/help/assets/manage-collections.md) 是片段关联内容的基础。
   * （可选）您还可以将片段本身添加到集合以帮助跟踪。

* **片段元数据**

   * 使用资产 [元数据模式](/help/assets/metadata-schemas.md)。
   * 在以下情况下可以创建标记：

      * 创建和创作片段
      * 或更高版本：

         * 通过从控制台查看／编辑片 **段** “属性”
         * 通过在片段编 **辑器中** ，编辑元数据
   >[!CAUTION]
   >
   >元数据处理用户档案不适用于内容片段。

* **母版**

   * 碎片的一个完整部分

      * 每个内容片段都有一个主实例。
      * 无法删除主视图。
   * 在片段编辑器中的“变量”下可访问主 **[页](/help/assets/content-fragments/content-fragments-variations.md)**。
   * “主”不是变体，而是所有变体的基础。


* **变量**

   * 特定于编辑目的的片段文本的再现；可以与渠道相关，但不是强制性的，也可以用于临时本地修改。
   * 创建为主页的副 **本**，但可以根据需要进行编辑；这些变体之间通常存在内容重叠。
   * 可以在片段创作过程中定义。
   * 存储在片段中，以帮助避免内容副本的散布。
   * 如果主内容 [已更新](/help/assets/content-fragments/content-fragments-variations.md#synchronizing-with-master) ，则可以与主内容同步变量。
   * 可以进行 [汇总](/help/assets/content-fragments/content-fragments-variations.md#summarizing-text) ，以将文本快速截断到预定义的长度。
   * 可在片段编辑 [器的](/help/assets/content-fragments/content-fragments-variations.md) “变量”选项卡下使用。

### 使用内容片段进行页面创作时的中间内容 {#in-between-content-when-page-authoring-with-content-fragments}

中间内容：

* 在处理内容片段时，可在页面编辑器中使用。
* 在 [页面上使用／引用片段后](/help/sites-cloud/authoring/fundamentals/content-fragments.md#adding-in-between-content) ，在片段流中添加的其他内容是否。
* 在处理内容片段时， [可在页面编辑器中使用](/help/sites-cloud/authoring/fundamentals/content-fragments.md)。
* 可以将中间内容添加到任何片段，其中只有一个元素可见。
* 可以使用关联的内容，也可以使用相应浏览器中的资产和／或组件。

>[!CAUTION]
>
>中间内容是页面内容。它不会存储在内容片段中。

### 片段要求 {#required-by-fragments}

要创建、编辑和使用内容片段，您还需要：

* **内容模型**

   * 启 [用，然后使用工具创建](/help/assets/content-fragments/content-fragments-models.md)。
   * 创建结 [构化片段必需](/help/assets/content-fragments/content-fragments-managing.md#creating-content-fragments)。
   * 定义片段的结构（标题、内容元素、标记定义）。
   * 内容模型定义需要一个标题和一个数据元素；其他一切都是可选的。 模型定义片段和默认内容的最小范围（如果适用）。 创作片段内容时，作者无法更改定义的结构。

* **片段模板**

   * 需 **要简单片段** 模板才能 [创建简单片段](/help/assets/content-fragments/content-fragments-managing.md#creating-content-fragments)。
   * 定义简单片段的基本属性（标题、文本元素数量、标记定义）。

* **内容片段组件**

   * 有助于以HTML和／或JSON格式传送片段。
   * 在页面 [上引用片段时必需](/help/sites-cloud/authoring/fundamentals/content-fragments.md)。
   * 负责片段的布局和投放;即渠道。
   * 片段需要一个或多个专用组件来定义布局并交付部分或全部元素／变量和相关内容。
   * 在创作过程中将片段拖动到页面上将自动关联所需的组件。

## 示例使用 {#example-usage}

片段及其元素和变量可用于为多个渠道创建一致的内容。 在设计片段时，您需要考虑将在何处使用什么。

### WKND示例 {#wknd-sample}

提 [供WKND Site](/help/implementing/developing/introduction/develop-wknd-tutorial.md) （WKND站点）示例，以帮助您了解AEM作为云服务。 它包括示例片段，这些片段可在以下位置查看：

`hhttp://<host>:<port>/assets.html/content/dam/wknd/en/adventures`
