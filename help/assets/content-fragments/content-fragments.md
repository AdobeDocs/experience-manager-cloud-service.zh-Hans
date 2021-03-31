---
title: 使用内容片段
description: 了解Adobe Experience Manager(AEM)作为Cloud Service中的内容片段如何允许您设计、创建、策划和使用独立于页面的内容，这是无外设投放的理想选择。
feature: 内容片段
role: 商务从业人员
translation-type: tm+mt
source-git-commit: 6fa911f39d707687e453de270bc0f3ece208d380
workflow-type: tm+mt
source-wordcount: '2039'
ht-degree: 6%

---


# 使用内容片段 {#working-with-content-fragments}

以Adobe Experience Manager(AEM)为Cloud Service，内容片段允许您设计、创建、策划和[发布独立于页面的内容](/help/sites-cloud/authoring/fundamentals/content-fragments.md)。它们允许您准备内容，以便在多个位置/多个渠道中使用，非常适合无外设投放。

内容片段包含结构化内容：

* 它们基于[内容片段模型](/help/assets/content-fragments/content-fragments-models.md)，该模型预定义了生成片段的结构。
* 此结构可以介于以下之间：
   * 基本
      * 例如，单行多行文本字段。
      * 可用于准备直接的内容以用于页面创作。
   * 复杂
      * 多种数据类型不同的字段的组合，包括文本、数字、布尔值、数据和时间等。
      * 可用于准备更多结构化内容以用于页面创作，或用于投放应用程序。
   * 嵌套
      * 可用的引用数据类型允许您嵌套您的内容。
      * 通常用于投放应用程序。

使用AEM核心组件的Sling Model(JSON)导出功能，内容片段也可以以JSON格式提供。 这种投放:

* 使您能够使用组件来管理片段中要传送的元素
* 允许批量投放，方法是在用于API投放的页面上添加多个内容片段核心组件

本页和以下页介绍了创建、配置、维护和使用内容片段的任务:

* [为实例启用内容片段功能](/help/assets/content-fragments/content-fragments-configuration-browser.md)
* [内容片段模型](/help/assets/content-fragments/content-fragments-models.md)  — 启用、创建和定义模型
* [管理内容片段](/help/assets/content-fragments/content-fragments-managing.md)  — 创建您的内容片段；然后编辑、发布和引用
* [变量 — 创作片段内容](/help/assets/content-fragments/content-fragments-variations.md)  — 创作片段内容并创建主控的变量
* [标记](/help/assets/content-fragments/content-fragments-markdown.md)  — 对片段使用标记语法
* [使用关联内容](/help/assets/content-fragments/content-fragments-assoc-content.md)  — 添加关联内容
* [元数据 — 片段属性](/help/assets/content-fragments/content-fragments-metadata.md)  — 查看和编辑片段属性
* 使用[内容片段和GraphQL提供内容](/help/assets/content-fragments/content-fragments-graphql.md)以在您的应用程序中使用。 为此，您可以预览[JSON输出](/help/assets/content-fragments/content-fragments-json-preview.md)。

>[!NOTE]
>
>这些页面可结合以下内容进行阅读：
>
>* [通过内容片段进行页面创作](/help/sites-cloud/authoring/fundamentals/content-fragments.md).
>* [自定义和扩展内容片段](/help/implementing/developing/extending/content-fragments-customizing.md)
>* [内容片段配置用于渲染的组件](/help/implementing/developing/extending/content-fragments-configuring-components-rendering.md)
>* [AEM Assets HTTP API 中的内容片段支持](/help/assets/content-fragments/assets-api-content-fragments.md)
>* [AEM GraphQL API，与内容片段一起使用](/help/assets/content-fragments/graphql-api-content-fragments.md)


通信渠道的数量每年都在增加。 通常，渠道将投放机制称为：

* 物理渠道;例如，桌面、移动。
* 实体投放的渠道;例如，“产品详细信息页”、“产品类别页”（适用于桌面）或“移动Web”、“移动应用程序”（适用于移动设备）。

但是，您（可能）不想对所有渠道使用完全相同的内容 — 您需要根据特定渠道优化您的内容。

内容片段允许您：

* 考虑如何跨渠道高效接触目标受众。
* 创建和管理渠道中立的编辑内容。
* 为各种渠道构建内容池。
* 为特定渠道设计内容变体。
* 通过插入资产（混合媒体片段）将图像添加到文本。
* 创建嵌套内容，以反映数据的复杂性。

然后，可以组合这些内容片段，以提供跨各种渠道的体验。

>[!NOTE]
>
>**内容片段**&#x200B;和&#x200B;**[体验片段](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)**&#x200B;是 AEM 中的两个不同功能：
>* **内** 容片段是编辑内容，可用于访问结构化数据，包括文本、数字和日期等。它们是纯内容，具有定义和结构，但无需其他可视设计和/或布局。
>* **体验片段**&#x200B;是经过充分布局的内容；例如，网页的一个片段。

>
>
体验片段可以包含内容片段形式的内容，反之则不行。
>
>有关详细信息，另请参阅[了解AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html?lang=en#content-fragments)中的内容片段和体验片段。

## 内容片段和内容服务{#content-fragments-and-content-services}

AEM Content Services旨在将内容的描述和投放概括化到AEM中/从创建的内容，而不局限于网页。

它们使用任何客户都可使用的标准化方法，向非传统AEM网页的渠道提供内容投放。 这些渠道可以包括：

* 单页应用程序
* 本机移动应用程序
* AEM外部的其他渠道和触点

投放是使用JSON导出器以JSON格式创建的。

AEM内容片段可用于描述和管理结构化内容。 结构化内容在可包含各种内容类型的模型中进行定义；包括文本、数值数据、布尔值、日期和时间等。

此结构化内容与AEM核心组件的JSON导出功能一起，可用于向AEM页面以外的渠道提供AEM内容。

>[!NOTE]
>
>有关将AEM Sites作为Cloud Service的无头开发的简介，请参阅[无头和AEM](/help/implementing/developing/headless/introduction.md)。

>[!NOTE]
>
>AEM还支持片段内容的翻译。

>[!NOTE]
>
>AEM还支持片段内容的翻译。 有关详细信息，请参阅[翻译资产](/help/assets/translate-assets.md)。

## 内容类型 {#content-type}

内容片段包括：

* 存储为&#x200B;**资产**:

   * 可以从&#x200B;**资产**&#x200B;控制台创建和维护内容片段（及其变量）。
   * 在内容片段编辑器中创作和编辑。

* 在[页面编辑器中通过内容片段组件](/help/sites-cloud/authoring/fundamentals/content-fragments.md)（引用组件）使用：

   * **内容片段**&#x200B;组件可供页面作者使用。 它允许他们以HTML或JSON格式引用和提供所需的内容片段。

* 可使用[AEM GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md)访问。

内容片段是一种内容结构，可：

* 没有布局或设计（在富文本模式下可以设置一些文本格式）。
* 包含一个或多个[组成部分](#constituent-parts-of-a-content-fragment)。
* 可以[包含或连接图像](#fragments-with-visual-assets)。
* 在页面上引用时，可以使用[中间内容](#in-between-content-when-page-authoring-with-content-fragments)。

* 独立于投放机制(即页面、渠道)。

### 可视资产{#fragments-with-visual-assets}的片段

为了使作者能够更好地控制其内容，可以将图像添加到内容片段并/或与内容片段集成。

资产可以通过多种方式与内容片段一起使用；各自有其优势：

* **插入** 资产片段（混合媒体片段）

   * 是片段的一个完整部分（请参阅[内容片段的组成部分](#constituent-parts-of-a-content-fragment)）。
   * 定义资产的位置。
   * 有关详细信息，请参阅片段编辑器中的[将资产插入片段](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment)。

   >[!NOTE]
   >
   >插入到内容片段本身中的可视资产会附加到前一段落。 将片段添加到页面时，在添加中间内容时，这些资产会相对于该段落移动。

* **关联的内容**

   * 连接到片段；但不是片段的固定部分（请参阅[内容片段的组成部分](#constituent-parts-of-a-content-fragment)）。
   * 允许一些定位灵活性。
   * 在页面上使用片段时，可轻松地使用（作为中间内容）。
   * 有关详细信息，请参阅[关联内容](/help/assets/content-fragments/content-fragments-assoc-content.md)。

* 页面编辑器的&#x200B;**资产浏览器**&#x200B;中的可用资产

   * 允许完全灵活地选择资产。
   * 允许一些定位灵活性。
   * 不提供为特定片段批准的概念。
   * 有关详细信息，请参阅[资产浏览器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser)。

### 内容片段{#constituent-parts-of-a-content-fragment}的组成部分

内容片段资产由以下部分（直接或间接）组成：

* **片段元素**

   * 元素与包含内容的数据字段关联。
   * 您可以使用内容模型创建内容片段。 模型中指定的元素（字段）定义片段的结构。 这些元素（字段）可以是多种数据类型。

* **片段段落**

   * 文本块（通常是多行文本），以单个实体的形式分隔。

   * 在富文 [本](/help/assets/content-fragments/content-fragments-variations.md#rich-text) 、标记 [下拉模式中](/help/assets/content-fragments/content-fragments-variations.md#markdown) ，段落可以格式化为标题，在这种情况下，它和以下段落同属一个单位。

   * 在页面创作过程中启用内容控制。

* **插入到片段（混合媒体片段）中的资产**

   * 插入到实际片段中并用作片段内部内容的资产（图像）。
   * 嵌入到片段的段落系统中。
   * 在页面](/help/sites-cloud/authoring/fundamentals/content-fragments.md)上使用/引用[片段时，可以设置格式。
   * 只能使用片段编辑器添加到片段、从片段中删除片段或在片段中移动片段。 无法在页面编辑器中执行这些操作。
   * 只能使用片段编辑器](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment)中的[富文本格式添加到片段、从片段中删除片段或在片段中移动片段。
   * 只能添加到多行文本元素（任何片段类型）。
   * 附于前文（段落）。

      >[!CAUTION]
      >
      >通过切换到纯文本格式，可以（无意中）从片段中删除资产。

      >[!NOTE]
      >
      >在页面上使用片段时，资产也可以添加为[附加（中间）内容](/help/sites-cloud/authoring/fundamentals/content-fragments.md#using-associated-content);使用“资产”浏览器中的关联内容或资产。

* **关联的内容**

   * 这是片段外部的内容，但与片段的编辑相关。 通常是图像、视频或其他片段。
   * 将片段添加到页面时，集合中的各个资产便可以在页面编辑器中与片段一起使用。 这意味着它们是可选的，具体取决于特定渠道的要求。
   * 资产通过集合](/help/assets/content-fragments/content-fragments-assoc-content.md)与片段关联；关联的收藏集允许作者决定在创作页面时要使用的资产。[

      * 集合可以作为默认内容与片段关联，也可以由作者在片段创作过程中关联。
      * [资产(DAM)收](/help/assets/manage-collections.md) 集是片段关联内容的基础。
   * （可选）您还可以将片段本身添加到集合以帮助跟踪。

* **片段元数据**

   * 使用[资产元数据模式](/help/assets/metadata-schemas.md)。
   * 在以下情况下可以创建标记：

      * 创建和创作片段
      * 或更高版本：

         * 通过从控制台查看/编辑片段&#x200B;**属性**
         * 通过在片段编辑器中编辑&#x200B;**元数据**

   >[!CAUTION]
   >
   >元数据处理用户档案不适用于内容片段。

* **母版**

   * 碎片的一个完整部分

      * 每个内容片段都有一个主控实例。
      * 无法删除主控。
   * 主控可在&#x200B;**[变量](/help/assets/content-fragments/content-fragments-variations.md)**&#x200B;下的片段编辑器中访问。
   * 主控不是这样的变体，而是所有变体的基础。


* **变量**

   * 特定于编辑目的的片段文本的呈现；可以与渠道相关，但不是强制性的，也可以用于临时本地修改。
   * 创建为&#x200B;**主控**&#x200B;的副本，但随后可以根据需要进行编辑；这些变体之间通常存在内容重叠。
   * 可以在片段创作过程中定义。
   * 存储在片段中，以帮助避免内容副本的散布。
   * 如果主控内容已更新，则变量可以[synchronized](/help/assets/content-fragments/content-fragments-variations.md#synchronizing-with-master)为主控。
   * 可以是[Asmulated](/help/assets/content-fragments/content-fragments-variations.md#summarizing-text)以快速将文本截断到预定义的长度。
   * 可在片段编辑器的[变量](/help/assets/content-fragments/content-fragments-variations.md)选项卡下找到。

### 使用内容片段创作页面时的中间内容{#in-between-content-when-page-authoring-with-content-fragments}

中间内容：

* 在处理内容片段时，可在页面编辑器中使用。
* 在页面上使用/引用片段](/help/sites-cloud/authoring/fundamentals/content-fragments.md#adding-in-between-content)后，在片段流中添加的[附加内容。
* 在处理内容片段](/help/sites-cloud/authoring/fundamentals/content-fragments.md)时，可在[页面编辑器中使用。
* 中间内容可以添加到任何片段，其中只有一个元素可见。
* 与资产和/或组件相关的内容也可以使用。

>[!CAUTION]
>
>中间内容是页面内容。它不会存储在内容片段中。

### 片段{#required-by-fragments}所需

要创建内容片段，您需要：

* **内容模型**

   * 使用配置浏览器](/help/assets/content-fragments/content-fragments-configuration-browser.md)启用[。
   * 是使用工具](/help/assets/content-fragments/content-fragments-models.md)创建的[。
   * 创建片段](/help/assets/content-fragments/content-fragments-managing.md#creating-content-fragments)时需要。[
   * 定义片段的结构（标题、内容元素、标记定义）。
   * 内容模型定义需要一个标题和一个数据元素；其他一切都是可选的。
   * 模型可以定义默认内容（如果适用）。
   * 创作片段内容时，作者无法更改定义的结构。
   * 在创建从属内容片段后对模型所做的更改可能会影响这些内容片段。

要将内容片段用于页面创作，您还需要：

* **内容片段组件**

   * 有助于以HTML和/或JSON格式传送片段。
   * 在页面](/help/sites-cloud/authoring/fundamentals/content-fragments.md)上引用片段时需要。[
   * 负责片段的布局和投放;即渠道。
   * 片段需要一个或多个专用组件来定义布局并交付部分或全部元素/变量及关联内容。
   * 在创作过程中将片段拖动到页面上会自动关联所需的组件。

## 用法示例{#example-usage}

片段及其元素和变量可用于为多个渠道创建一致的内容。 在设计片段时，您需要考虑将在何处使用什么。

### WKND示例{#wknd-sample}

提供了[WKND Site](/help/implementing/developing/introduction/develop-wknd-tutorial.md)示例，以帮助您了解AEM作为Cloud Service。

WKND项目包括：

* 内容片段模型可在以下位置获取：
   `http://<hostname>:<port>/libs/dam/cfm/models/console/content/models.html/conf/wknd`

* 可从以下位置获得内容片段（和其他内容）：
   `http://<hostname>:<port>/assets.html/content/dam/wknd/en`
