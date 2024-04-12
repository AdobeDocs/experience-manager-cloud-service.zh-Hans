---
title: 使用内容片段（资产 — 内容片段）
description: 了解Adobe Experience Manager (AEM) as a Cloud Service中的内容片段如何允许您设计、创建、策划和使用独立于页面的内容，非常适用于页面创作和headless投放。 以及它们如何与MSM结合使用。
exl-id: db17eff1-4252-48d5-bb67-5e476e93ef7e
source-git-commit: 930eca968807eaa9b322010d582973d431b9fa01
workflow-type: tm+mt
source-wordcount: '2230'
ht-degree: 59%

---

# 使用内容片段 {#working-with-content-fragments}

通过Adobe Experience Manager (AEM)as a Cloud Service，您可以设计、创建、管理和使用内容片段 [发布独立于页面的内容](/help/sites-cloud/authoring/fragments/content-fragments.md). 利用这些功能，可准备内容以准备在多个位置/多个渠道上使用，非常适用于Headless投放。 它们也可以与一起使用 [多站点管理使您能够重复使用内容](#reusing-content-fragments-with-msm).

内容片段包含结构化内容：

* 它们基于[内容片段模型](/help/assets/content-fragments/content-fragments-models.md)，用于为生成片段预定义结构。
* 此结构可以介于以下两种之间：
   * 基本
      * 例如，单个多行文本字段。
      * 它可用于准备直接内容以用于页面创作。
   * 复杂
      * 多种数据类型（包括文本、数字、布尔值、数据和时间等）的字段组合。
      * 它可用于为页面创作准备更多结构化内容，或投放到应用程序。
   * 嵌套
      * 可用的引用数据类型允许您嵌套内容。
      * 通常用于将内容投放到应用程序。

使用 AEM 核心组件的 Sling 模型 (JSON) 导出功能，内容片段也可以以 JSON 格式投放。 此投放形式：

* 允许您使用组件管理要投放片段的哪些元素
* 允许批量投放，方法是在用于 API 投放的页面上添加多个内容片段核心组件

>[!NOTE]
>
>内容片段是一项站点功能，但存储为&#x200B;**资源**。
>
>现在，它们主要通过 **[内容片段](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console)** 控制台，但是仍然可以从以下位置管理它们 **资产** 控制台。 本节介绍以下管理方面的信息： **资产** 控制台。
>
>创作内容片段有两个编辑器。 本节介绍原始编辑器，可从以下位置访问该编辑器： **资产** 控制台。 请参阅Sites文档， [内容片段 — 创作](/help/sites-cloud/administering/content-fragments/authoring.md)，以了解新编辑器的详细信息(主要通过 **内容片段** 控制台)。 两个编辑器的顶部工具栏中都有一个切换开关，用于提供对另一个编辑器的快速访问。

本页和以下页面介绍了创建、配置、维护和使用内容片段的任务：

* [为您的实例启用内容片段功能](/help/assets/content-fragments/content-fragments-configuration-browser.md)
* [内容片段模型](/help/assets/content-fragments/content-fragments-models.md) – 启用、创建和定义您的模型
* [管理内容片段](/help/assets/content-fragments/content-fragments-managing.md)  — 创建内容片段；然后编辑、发布和引用
* [变体 – 创作片段内容](/help/assets/content-fragments/content-fragments-variations.md) – 创作片段内容并创建主控
* [Markdown](/help/assets/content-fragments/content-fragments-markdown.md) – 使用片段的 markdown 语法
* [使用关联内容](/help/assets/content-fragments/content-fragments-assoc-content.md) – 添加关联内容
* [元数据 – 片段属性](/help/assets/content-fragments/content-fragments-metadata.md) – 查看和编辑片段属性
* 使用 [内容片段，以及GraphQL，使您能够交付内容](/help/assets/content-fragments/content-fragments-graphql.md) 以便在您的应用程序中使用。 要帮助您完成此操作，您可以预览 [JSON输出](/help/assets/content-fragments/content-fragments-json-preview.md).
* [使用MSM重用内容片段](#reusing-content-fragments-with-msm)

>[!NOTE]
>
>可以通过以下方式读取这些页面：
>
>* [通过内容片段进行页面创作](/help/sites-cloud/authoring/fragments/content-fragments.md)。
>* [自定义和扩展内容片段](/help/implementing/developing/extending/content-fragments-customizing.md)
>* [内容片段配置用于呈现的组件](/help/implementing/developing/extending/content-fragments-configuring-components-rendering.md)
>* [AEM Assets HTTP API 中的内容片段支持](/help/assets/content-fragments/assets-api-content-fragments.md)
>* [用于内容片段的 AEM GraphQL API](/help/headless/graphql-api/content-fragments.md)
>* 此 [内容片段和内容片段模型OpenAPI](/help/headless/content-fragment-openapis.md)

通信渠道的数量在逐年增加。通常，渠道称为投放机制，如：

* 物理渠道；例如，台式机、移动设备。
* 实物渠道中的投放形式；例如，“产品详细信息页面”、“产品类别页面”（适用于桌面）或“移动设备 Web”（适用于移动设备的移动设备应用程序）。

但是，您（可能）不希望在所有渠道中使用相同的内容 — 您必须根据特定渠道优化内容。

内容片段允许您：

* 考虑如何跨渠道高效地访问目标受众。
* 创建和管理渠道中性的可编辑内容。
* 为一系列渠道构建内容池。
* 为特定渠道设计内容变体。
* 通过插入资源（混合媒体片段），向文本中添加图像。
* 创建嵌套内容，以便您反映数据的复杂性。

然后，可以组合这些内容片段以通过各种渠道提供体验。

>[!NOTE]
>
>**内容片段**&#x200B;和&#x200B;**[体验片段](/help/sites-cloud/authoring/fragments/content-fragments.md)**&#x200B;是 AEM 中的两个不同功能：
>* **内容片段**&#x200B;是可编辑内容，具有定义和结构，但无需额外的可视设计和/或布局。它们可用于访问结构化数据，包括文本、数字和日期等。
>* **体验片段**&#x200B;是经过充分布局的内容；例如，网页的一个片段。
>
>体验片段可以包含内容片段形式的内容，反之则不行。
>
>有关更多信息，另请参阅 [了解AEM中的内容片段和体验片段](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html#content-fragments).

## 内容片段和内容服务 {#content-fragments-and-content-services}

AEM 内容服务旨在概括 AEM 中/来自 AEM 的内容的描述和投放，而不只是关注网页。

它们使用可供任何客户使用的标准化方法，将内容投放到非传统 AEM 网页的渠道。这些渠道可以包括：

* 单页面应用程序
* 本机移动设备应用程序
* AEM 外部的其他渠道和接触点

使用 JSON 导出程序以 JSON 格式进行投放。

AEM 内容片段可用于描述和管理结构化内容。结构化内容在可包含各种内容类型（包括文本、数字数据、布尔值、日期和时间等）的模型中定义。

随后，此结构化内容与 AEM 核心组件的 JSON 导出功能一起，可用于将 AEM 内容投放到 AEM 页面以外的渠道。

>[!NOTE]
>
>有关 AEM Sites as a Cloud Service 的 Headless 开发的介绍，请参阅 [Headless 和 AEM](/help/headless/introduction.md)。

>[!NOTE]
>
>AEM 还支持片段内容的翻译。请参阅[翻译资产](/help/assets/translate-assets.md)以了解更多信息。

## 内容类型 {#content-type}

内容片段包括：

* 存储为&#x200B;**资源**：

   * 内容片段（及其变体）可以从以下内容创建和维护： **资产** 控制台。
   * 在内容片段编辑器中创作和编辑。

* 用于 [按内容片段组件显示的页面编辑器](/help/sites-cloud/authoring/fragments/content-fragments.md) （引用组件）：

   * **内容片段**&#x200B;组件可供页面作者使用。 它允许他们以 HTML 或 JSON 格式引用和投放所需的内容片段。

* 可使用 [AEM GraphQL API](/help/headless/graphql-api/content-fragments.md)。

内容片段是一种内容结构，其中：

* 没有布局或设计（在富文本模式下，可以使用某些文本格式）。
* 包含一个或多个 [组成部分](#constituent-parts-of-a-content-fragment).
* [包含或可以连接到图像](#fragments-with-visual-assets).
* 已使用 [中间内容](#in-between-content-when-page-authoring-with-content-fragments) 在页面上引用时。
* 它们独立于投放机制（即页面、渠道）。

### 包含可视资源的片段 {#fragments-with-visual-assets}

为了让作者更好地控制其内容，可以将图像添加到内容片段和/或与其集成。

资产可以通过多种方式与内容片段一起使用；各具优势：

* **插入资源**&#x200B;到片段（混合媒体片段）

   * 它们是片段的一部分(请参阅 [内容片段的组成部分](#constituent-parts-of-a-content-fragment))。
   * 定义资源的位置。
   * 请参阅[将资源插入片段](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment)（在片段编辑器中）以了解更多信息。

  >[!NOTE]
  >
  >插入到内容片段本身的视觉资源附在前面的段落中。 将片段添加到页面时，在添加中间内容时，这些资产会相对于该段落进行移动。

* **关联的内容**

   * 连接到片段；但不是片段的固定部分(请参阅 [内容片段的组成部分](#constituent-parts-of-a-content-fragment))。
   * 具有一定的定位灵活性。
   * 在页面上使用片段时，可以轻松使用（作为中间内容）。

  请参阅[关联内容](/help/assets/content-fragments/content-fragments-assoc-content.md)以了解更多信息。

* 页面编辑器的&#x200B;**资源浏览器**&#x200B;中的可用资源

   * 允许完全灵活地选择资源。
   * 具有一定的定位灵活性。
   * 不提供为特定片段批准的概念。

  请参阅[资源浏览器](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#assets-browser)以了解更多信息。

### 内容片段的组成部分 {#constituent-parts-of-a-content-fragment}

内容片段资源由以下部分（直接或间接）组成：

* **片段元素**

   * 元素与包含内容的数据字段关联。
   * 您可以使用内容模型创建内容片段。 模型中指定的元素（字段）定义片段的结构。 这些元素（字段）可以是各种数据类型。

* **片段段落**

   * 文本块，通常为以单个实体分隔的多行。

   * 在[富文本](/help/assets/content-fragments/content-fragments-variations.md#rich-text)和 [Markdown](/help/assets/content-fragments/content-fragments-variations.md#markdown) 模式中，一个段落可以被格式化为一个标题，在这种情况下它和后面的段落属于一个单元。

   * 在页面创作期间启用内容控制。

* **插入到片段中的资源（混合媒体片段）**

   * 插入到实际片段中并用作片段内部内容的资源（图像）。
   * 嵌入在片段的段落系统中。
   * 可以[在页面上使用/引用片段时](/help/sites-cloud/authoring/fragments/content-fragments.md)进行格式化。
   * 只能使用片段编辑器在片段中添加、删除或移动到片段中。 无法在页面编辑器中执行这些操作。
   * 只能使用在片段中添加、删除或移动片段 [片段编辑器中的富文本格式](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment).
   * 只能添加到多行文本元素（任何片段类型）。
   * 附于前文（段落）。

     >[!CAUTION]
     >
     >通过切换为纯文本格式，可以（意外）从片段中删除资源。

     >[!NOTE]
     >
     >在页面上使用片段时，资产也可以添加为其他（中间）内容；使用 [关联内容](/help/assets/content-fragments/content-fragments-assoc-content.md) 或资产。

* **关联的内容**

   * 这是片段外部的内容，但与编辑相关。 通常是图像、视频或其他片段。
   * 将收藏集中的单个资源添加到页面后，即可在页面编辑器中与片段一起使用。 这表示它们是可选的，具体取决于特定渠道的要求。
   * 这些资产包括 [通过收藏集关联到片段](/help/assets/content-fragments/content-fragments-assoc-content.md)；关联的收藏集允许作者决定在创作页面时要使用的资产。

      * 收藏集可以作为默认内容与片段关联，也可以由作者在片段创作期间关联。
      * [资源 (DAM) 收藏集](/help/assets/manage-collections.md)是片段关联内容的基础。
   * 或者，您也可以将片段本身添加到集合中以帮助跟踪。

* **片段元数据**

   * 使用[资源元数据架构](/help/assets/metadata-schemas.md)。
   * 标记可在以下情况下创建：

      * 创建和创作片段
      * 或更高版本：

         * 通过从控制台查看/编辑片段&#x200B;**属性**
         * 通过在片段编辑器中编辑&#x200B;**元数据**

  >[!CAUTION]
  >
  >元数据处理配置文件不适用于内容片段。

* **主控**

   * 片段的一部分

      * 每个内容片段都有一个主控实例。
      * 无法删除主控。

   * 主控可以在&#x200B;**[变体](/help/assets/content-fragments/content-fragments-variations.md)**&#x200B;下的片段编辑器中访问。
   * 主控不是此变体，而是所有变体的基础。

* **变体**

   * 特定于编辑目的的片段文本的演绎版；可以与渠道相关，但不是强制性的，也可以用于临时本地修改。
   * 创建为的副本 **母版**，但随后可以根据需要进行编辑。 变体本身之间存在内容重叠。
   * 可以在片段创作期间定义。
   * 存储在片段中，以帮助避免内容副本的散布。
   * 如果主控内容已更新，则变体可以与主控[同步](/help/assets/content-fragments/content-fragments-variations.md#synchronizing-with-master)。
   * 可以[概述](/help/assets/content-fragments/content-fragments-variations.md#summarizing-text)以快速将文本截断为预定义的长度。
   * 在片段编辑器的[变体](/help/assets/content-fragments/content-fragments-variations.md)选项卡下可用。

### 使用内容片段创作页面时的中间内容 {#in-between-content-when-page-authoring-with-content-fragments}

中间内容：

* 可用于处理内容片段时的页面编辑器。
* [在片段流中添加的其他内容](/help/sites-cloud/authoring/fragments/content-fragments.md#adding-in-between-content) 在页面上使用或引用之后。
* 可在以下位置使用： [使用内容片段时的页面编辑器](/help/sites-cloud/authoring/fragments/content-fragments.md).
* 中间内容可以添加到任何片段中，其中只有一个元素可见。
* 关联内容的使用方式，以及相应浏览器中的资源和/或组件。

>[!CAUTION]
>
>中间内容是页面内容。它不会存储在内容片段中。

### 片段必需 {#required-by-fragments}

要创建内容片段，您需要：

* **内容模型**

   * [使用配置浏览器启用](/help/assets/content-fragments/content-fragments-configuration-browser.md)。
   * [使用工具创建](/help/assets/content-fragments/content-fragments-models.md)。
   * 需要[创建片段](/help/assets/content-fragments/content-fragments-managing.md#creating-content-fragments)。
   * 定义片段的结构（标题、内容元素、标记定义）。
   * 内容模型定义需要一个标题和一个数据元素；其他内容都是可选的。
   * 模型可定义默认内容（如果适用）。
   * 创作片段内容时，作者无法更改定义的结构。
   * 创建从属内容片段后对模型所做的更改可能会影响这些内容片段。

要将内容片段用于页面创作，您还需要：

* **内容片段组件**

   * 有助于以HTML格式或JSON格式（或两者）传送片段。
   * 需要[在页面上引用片段](/help/sites-cloud/authoring/fragments/content-fragments.md)。
   * 负责片段的布局和投放；即渠道。
   * 片段需要一个或多个专用组件来定义布局并投放部分或全部元素/变体和关联内容。
   * 在创作中将片段拖动到页面上将自动关联所需的组件。

## 在MSM中重用内容片段 {#reusing-content-fragments-with-msm}

通过访问时 **资产** 控制台中，您可以使用MSM并为片段创建活动副本。

有关更多详细信息，请参阅：

* [使用MSM重用内容片段](/help/assets/content-fragments/content-fragments-msm.md)
* [使用MSM重新使用资产](/help/assets/reuse-assets-using-msm.md).

这些启用 [继承](/help/assets/content-fragments/content-fragments-variations.md#inheritance) 适用于变体和片段的单个字段。

>[!CAUTION]
>
>如果要使用MSM（这将创建内容片段的副本），则任意 **独特** 应从在各自中使用的所有数据类型中删除约束 [内容片段模型](/help/assets/content-fragments/content-fragments-models.md).

## 使用示例 {#example-usage}

片段及其元素和变体可用于为多个渠道创建一致的内容。在设计片段时，请考虑使用的内容及其使用位置。

### WKND 示例 {#wknd-sample}

[WKND Sites](/help/implementing/developing/introduction/develop-wknd-tutorial.md) 示例可帮助您了解 AEM as a Cloud Service。

WKND 项目包括：

* 在以下位置提供的内容片段模型：
  `http://<hostname>:<port>/libs/dam/cfm/models/console/content/models.html/conf/wknd`

* 在以下位置提供的内容片段（和其他内容）：
  `http://<hostname>:<port>/assets.html/content/dam/wknd/en`
