---
title: 使用内容片段
description: 了解Adobe Experience Manager(AEM)as a Cloud Service中的内容片段如何允许您设计、创建、策划和使用独立于页面的内容，非常适合无头交付。
feature: Content Fragments
role: User
exl-id: db17eff1-4252-48d5-bb67-5e476e93ef7e
source-git-commit: e592dd7a3a717259493f23943933fe3d0e71b7ab
workflow-type: tm+mt
source-wordcount: '2033'
ht-degree: 7%

---

# 使用内容片段 {#working-with-content-fragments}

利用Adobe Experience Manager(AEM)as a Cloud Service，内容片段允许您设计、创建、策划和 [发布独立于页面的内容](/help/sites-cloud/authoring/fundamentals/content-fragments.md) 利用这些功能，可准备内容以准备在多个位置/多个渠道上使用，非常适合无头投放。

内容片段包含结构化内容：

* 它们基于 [内容片段模型](/help/assets/content-fragments/content-fragments-models.md)，用于为生成片段预定义结构。
* 此结构可以介于以下两种之间：
   * 基本
      * 例如，单个多行文本字段。
      * 可用于准备直接内容以用于页面创作。
   * 复杂
      * 多种数据类型（包括文本、数字、布尔值、数据和时间等）的字段组合。
      * 可用于为页面创作准备更多结构化内容，或交付到应用程序。
   * 嵌套
      * 可用的引用数据类型允许您嵌套内容。
      * 通常用于将内容交付到应用程序。

使用AEM核心组件的Sling模型(JSON)导出功能，内容片段也可以以JSON格式交付。 此投放形式：

* 允许您使用组件管理要交付片段的哪些元素
* 允许批量交付，方法是在用于API交付的页面上添加多个内容片段核心组件

本页和以下页面介绍了创建、配置、维护和使用内容片段的任务：

* [为实例启用内容片段功能](/help/assets/content-fragments/content-fragments-configuration-browser.md)
* [内容片段模型](/help/assets/content-fragments/content-fragments-models.md)  — 启用、创建和定义模型
* [管理内容片段](/help/assets/content-fragments/content-fragments-managing.md)  — 创建内容片段；然后，编辑、发布和引用
* [变量 — 创作片段内容](/help/assets/content-fragments/content-fragments-variations.md)  — 创作片段内容并创建主控
* [Markdown](/help/assets/content-fragments/content-fragments-markdown.md)  — 使用片段的markdown语法
* [使用关联内容](/help/assets/content-fragments/content-fragments-assoc-content.md)  — 添加关联内容
* [元数据 — 片段属性](/help/assets/content-fragments/content-fragments-metadata.md)  — 查看和编辑片段属性
* 使用 [内容片段与GraphQL一起交付内容](/help/assets/content-fragments/content-fragments-graphql.md) ，以在您的应用程序中使用。 要帮助您完成此操作，您可以预览 [JSON输出](/help/assets/content-fragments/content-fragments-json-preview.md).

>[!NOTE]
>
>这些页面可以与以下内容一起阅读：
>
>* [通过内容片段进行页面创作](/help/sites-cloud/authoring/fundamentals/content-fragments.md).
>* [自定义和扩展内容片段](/help/implementing/developing/extending/content-fragments-customizing.md)
>* [内容片段配置用于渲染的组件](/help/implementing/developing/extending/content-fragments-configuring-components-rendering.md)
>* [AEM Assets HTTP API 中的内容片段支持](/help/assets/content-fragments/assets-api-content-fragments.md)
>* [用于内容片段的 AEM GraphQL API](/help/headless/graphql-api/content-fragments.md)


通信渠道的数量在逐年增加。 通常，渠道称为投放机制，如：

* 物理渠道；例如，台式机、移动设备。
* 实物渠道中的投放形式；例如，“产品详细信息页面”、“产品类别页面”（适用于桌面）或“移动设备Web”（适用于移动设备的移动设备应用程序）。

但是，您（可能）不希望在所有渠道中使用完全相同的内容 — 您需要根据特定渠道优化内容。

内容片段允许您：

* 考虑如何跨渠道高效地访问目标受众。
* 创建和管理渠道中性的编辑内容。
* 为一系列渠道构建内容池。
* 为特定渠道设计内容变体。
* 通过插入资产（混合媒体片段），向文本中添加图像。
* 创建嵌套内容以反映数据的复杂性。

然后，可以组合这些内容片段以通过各种渠道提供体验。

>[!NOTE]
>
>**内容片段**&#x200B;和&#x200B;**[体验片段](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)**&#x200B;是 AEM 中的两个不同功能：
>* **内容片段** 是编辑内容，可用于访问结构化数据，包括文本、数字和日期等。 它们是纯内容，具有定义和结构，但无需额外的可视设计和/或布局。
>* **体验片段**&#x200B;是经过充分布局的内容；例如，网页的一个片段。
>
>体验片段可以包含内容片段形式的内容，反之则不行。
>
>有关详细信息，另请参见 [了解AEM中的内容片段和体验片段](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html#content-fragments).

## 内容片段和内容服务 {#content-fragments-and-content-services}

AEM Content Services旨在对AEM中/从中提供的内容的描述和交付进行归纳，使其不仅仅限于网页。

它们使用可供任何客户使用的标准化方法，将内容交付到非传统AEM网页的渠道。 这些渠道可以包括：

* 单页应用程序
* 本机移动设备应用程序
* AEM外部的其他渠道和接触点

使用JSON导出程序以JSON格式进行交付。

AEM内容片段可用于描述和管理结构化内容。 结构化内容在可包含各种内容类型的模型中定义；包括文本、数值数据、布尔值、日期和时间等。

随后，此结构化内容与AEM核心组件的JSON导出功能一起，可用于将AEM内容交付到AEM页面以外的渠道。

>[!NOTE]
>
>请参阅 [无头和AEM](/help/headless/introduction.md) 介绍AEM Sitesas a Cloud Service的Headless开发。

>[!NOTE]
>
>AEM还支持片段内容的翻译。

>[!NOTE]
>
>AEM还支持片段内容的翻译。 请参阅 [翻译资产](/help/assets/translate-assets.md) 以了解更多信息。

## 内容类型 {#content-type}

内容片段包括：

* 存储为 **资产**:

   * 可以从 **资产** 控制台。
   * 在内容片段编辑器中创作和编辑。

* 在 [页面编辑器](/help/sites-cloud/authoring/fundamentals/content-fragments.md) （引用组件）：

   * 的 **内容片段** 组件适用于页面作者。 它允许他们以HTML或JSON格式引用和交付所需的内容片段。

* 可使用 [AEM GraphQL API](/help/headless/graphql-api/content-fragments.md).

内容片段是一种内容结构，其中：

* 没有布局或设计（在富文本模式下，可以使用一些文本格式）。
* 包含一个或多个， [组成部分](#constituent-parts-of-a-content-fragment).
* 可以 [包含或连接到图像](#fragments-with-visual-assets).
* 可以使用 [中间内容](#in-between-content-when-page-authoring-with-content-fragments) 在页面上引用时。

* 独立于投放机制（即页面、渠道）。

### 包含可视资产的片段 {#fragments-with-visual-assets}

为了让作者更好地控制其内容，可以将图像添加到内容片段和/或与其集成。

资产可以通过多种方式与内容片段一起使用；各具优势：

* **插入资产** 到片段（混合媒体片段）

   * 是片段的组成部分(请参阅 [内容片段的组成部分](#constituent-parts-of-a-content-fragment))。
   * 定义资产的位置。
   * 请参阅 [将资产插入片段](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment) （在片段编辑器中）以了解更多信息。

   >[!NOTE]
   >
   >插入到内容片段本身中的可视化资产会附加到前一段落。 将片段添加到页面后，在添加中间内容时，这些资产会相对于该段落进行移动。

* **关联的内容**

   * 连接到片段；但不是片段的固定部分(请参阅 [内容片段的组成部分](#constituent-parts-of-a-content-fragment))。
   * 具有一定的定位灵活性。
   * 在页面上使用片段时，可轻松使用（作为中间内容）。
   * 请参阅 [关联内容](/help/assets/content-fragments/content-fragments-assoc-content.md) 以了解更多信息。

* 页面编辑器的&#x200B;**资产浏览器**&#x200B;中的可用资产

   * 允许完全灵活地选择资产。
   * 具有一定的定位灵活性。
   * 不提供为特定片段批准的概念。
   * 请参阅 [资产浏览器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser) 以了解更多信息。

### 内容片段的组成部分 {#constituent-parts-of-a-content-fragment}

内容片段资产由以下部分（直接或间接）组成：

* **片段元素**

   * 元素与包含内容的数据字段关联。
   * 您可以使用内容模型创建内容片段。 模型中指定的元素（字段）定义片段的结构。 这些元素（字段）可以包含多种数据类型。

* **片段段落**

   * 以单个实体分隔的文本块，通常为多行。

   * 在富文 [本](/help/assets/content-fragments/content-fragments-variations.md#rich-text) 、标记 [下拉模式中](/help/assets/content-fragments/content-fragments-variations.md#markdown) ，段落可以格式化为标题，在这种情况下，它和以下段落同属一个单位。

   * 在页面创作期间启用内容控制。

* **插入到片段中的资产（混合媒体片段）**

   * 插入到实际片段中并用作片段内部内容的资产（图像）。
   * 嵌入在片段的段落系统中。
   * 可以在 [片段在页面上使用/引用](/help/sites-cloud/authoring/fundamentals/content-fragments.md).
   * 只能使用片段编辑器在片段中添加、删除或移动到片段中。 无法在页面编辑器中执行这些操作。
   * 只能使用 [片段编辑器中的富文本格式](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment).
   * 只能添加到多行文本元素（任何片段类型）。
   * 附于前文（段落）。

      >[!CAUTION]
      >
      >通过切换为纯文本格式，可以（意外）从片段中删除资产。

      >[!NOTE]
      >
      >资产也可以添加为 [其他（中间）内容](/help/sites-cloud/authoring/fundamentals/content-fragments.md#using-associated-content) 在页面上使用片段时；使用资产浏览器中的关联内容或资产。

* **关联的内容**

   * 这是片段外部的内容，但与编辑相关。 通常是图像、视频或其他片段。
   * 将收藏集中的单个资产添加到页面后，即可在页面编辑器中与片段一起使用。 这表示它们是可选的，具体取决于特定渠道的要求。
   * 资产包括 [通过收藏集关联到片段](/help/assets/content-fragments/content-fragments-assoc-content.md);关联的收藏集允许作者决定在创作页面时要使用的资产。

      * 收藏集可以作为默认内容与片段关联，也可以由作者在片段创作期间关联。
      * [资产(DAM)收藏集](/help/assets/manage-collections.md) 是片段关联内容的基础。
   * 或者，您也可以将片段本身添加到集合中以帮助跟踪。

* **片段元数据**

   * 使用 [资产元数据架构](/help/assets/metadata-schemas.md).
   * 标记可在以下情况下创建：

      * 创建和创作片段
      * 或更高版本：

         * 通过查看/编辑片段 **属性** 从控制台
         * 通过编辑 **元数据** 在片段编辑器中

   >[!CAUTION]
   >
   >元数据处理配置文件不适用于内容片段。

* **母版**

   * 片段的一个组成部分

      * 每个内容片段都有一个主控实例。
      * 无法删除主控。
   * 主控可在片段编辑器中的 **[变体](/help/assets/content-fragments/content-fragments-variations.md)**.
   * 主控不是此变体，而是所有变体的基础。


* **变体**

   * 特定于编辑目的的片段文本的呈现；可以与渠道相关，但不是强制性的，也可以用于临时本地修改。
   * 创建为的副本 **主控**，但随后可以根据需要进行编辑；变体本身之间通常存在内容重叠。
   * 可以在片段创作期间定义。
   * 存储在片段中，以帮助避免内容副本的散布。
   * 变量可以是 [已同步](/help/assets/content-fragments/content-fragments-variations.md#synchronizing-with-master) 如果主控内容已更新，则使用主控。
   * 可以 [概述](/help/assets/content-fragments/content-fragments-variations.md#summarizing-text) 以快速将文本截断为预定义的长度。
   * 可在 [变体](/help/assets/content-fragments/content-fragments-variations.md) 选项卡。

### 使用内容片段创作页面时的中间内容 {#in-between-content-when-page-authoring-with-content-fragments}

中间内容：

* 处理内容片段时，可在页面编辑器中使用。
* 是 [在片段流中添加的其他内容](/help/sites-cloud/authoring/fundamentals/content-fragments.md#adding-in-between-content) 在页面上使用/引用后，才会触发该事件。
* 可用于 [使用内容片段时的页面编辑器](/help/sites-cloud/authoring/fundamentals/content-fragments.md).
* 中间内容可以添加到任何片段中，其中只有一个元素可见。
* 关联内容的使用方式，以及相应浏览器中的资产和/或组件。

>[!CAUTION]
>
>中间内容是页面内容。它不会存储在内容片段中。

### 片段必需 {#required-by-fragments}

要创建内容片段，您需要：

* **内容模型**

   * 是 [使用配置浏览器启用](/help/assets/content-fragments/content-fragments-configuration-browser.md).
   * 是 [使用工具创建](/help/assets/content-fragments/content-fragments-models.md).
   * 需要 [创建片段](/help/assets/content-fragments/content-fragments-managing.md#creating-content-fragments).
   * 定义片段的结构（标题、内容元素、标记定义）。
   * 内容模型定义需要一个标题和一个数据元素；其他内容都是可选的。
   * 模型可定义默认内容（如果适用）。
   * 创作片段内容时，作者无法更改定义的结构。
   * 创建从属内容片段后对模型所做的更改可能会影响这些内容片段。

要将内容片段用于页面创作，您还需要：

* **内容片段组件**

   * 有助于以HTML和/或JSON格式传送片段。
   * 需要 [在页面上引用片段](/help/sites-cloud/authoring/fundamentals/content-fragments.md).
   * 负责片段的布局和交付；即渠道。
   * 片段需要一个或多个专用组件来定义布局并交付部分或全部元素/变体和关联内容。
   * 在创作中将片段拖动到页面上将自动关联所需的组件。

## 使用示例 {#example-usage}

片段及其元素和变量可用于为多个渠道创建一致的内容。 在设计片段时，您需要考虑将在何处使用的内容。

### WKND示例 {#wknd-sample}

的 [WKND站点](/help/implementing/developing/introduction/develop-wknd-tutorial.md) 提供了一些示例，帮助您了解AEMas a Cloud Service。

WKND项目包括：

* 在以下位置提供的内容片段模型：
   `http://<hostname>:<port>/libs/dam/cfm/models/console/content/models.html/conf/wknd`

* 在以下位置提供的内容片段（和其他内容）：
   `http://<hostname>:<port>/assets.html/content/dam/wknd/en`
