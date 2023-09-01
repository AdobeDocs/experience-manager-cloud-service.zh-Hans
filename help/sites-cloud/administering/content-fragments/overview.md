---
title: 使用内容片段的概述
description: 了解Adobe Experience Manager (AEM)as a Cloud Service中的内容片段如何允许您设计、创建、策划和使用独立于页面的内容，非常适用于Headless投放和页面创作。
feature: Content Fragments
role: User, Developer, Architect
source-git-commit: 3d20f4bca566edcdb5f13eab581c33b7f3cf286d
workflow-type: tm+mt
source-wordcount: '1823'
ht-degree: 40%

---


# 使用内容片段的概述 {#overview-working-with-content-fragments}

利用Adobe Experience Manager (AEM)as a Cloud Service，内容片段允许您设计、创建、策划和 [发布独立于页面的内容](/help/sites-cloud/authoring/fundamentals/content-fragments.md). 利用这些功能，可准备内容以准备在多个位置和多个渠道上使用，非常适用于Headless投放和页面创作。

>[!IMPORTANT]
>
>可以从两个控制台访问内容片段： **内容片段** 和 **资产**.
>
>还有两个编辑器可用于内容片段。 （两个编辑器都可从两个控制台中访问。）
>
>本节将介绍 **内容片段** 控制台和 *新建* 内容片段编辑器。 这些组件针对Headless内容投放而开发（尽管它们可用于所有场景）
>
>有关更多信息，请参阅：
>
>* 使用 **资产** 控制台 [管理内容片段](/help/assets/content-fragments/content-fragments-managing.md)
>* 使用 [*原有* 内容片段编辑器](/help/assets/content-fragments/content-fragments-variations.md)，
>* 使用 [用于页面创作的内容片段](/help/sites-cloud/authoring/fundamentals/content-fragments.md).


内容片段包含结构化内容：

* 每个片段都基于 [内容片段模型](/help/sites-cloud/administering/content-fragments/content-fragment-models.md).
   * 内容片段模型定义生成片段的结构。
* 每个片段都包含：
   * **[主要](#main-and-variations)**  — 包含核心内容的片段的组成部分；始终存在，无法删除
   * **[变体](#main-and-variations)**  — 作者创建的一个或多个内容排列
* 此结构可以介于以下两种之间：
   * 基本
      * 例如，单个多行文本字段。
      * 可用于准备直接内容以用于页面创作。
      * 还可用于向应用程序headless投放。
   * 复杂
      * 多种数据类型（包括文本、数字、布尔值、日期和时间等）的字段组合。
      * 可用于为页面创作准备更多结构化内容，或用于向应用程序headless投放。
   * 嵌套
      * 可用的引用数据类型允许您嵌套内容。
      * 通常用于向应用程序执行headless投放。

使用AEM核心组件的Sling模型(JSON)导出功能，内容片段也可以以JSON格式投放。 此投放形式：

* 允许您使用组件管理要投放片段的哪些元素
* 允许批量交付；通过添加多个 [内容片段核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html) 在用于API投放的页面上

通信渠道的数量在逐年增加。 通常，渠道称为投放机制，如：

* 物理渠道；例如，台式机、移动设备。
* 实物渠道中的投放形式；例如，“产品详细信息页面”、“产品类别页面”（适用于桌面）或“移动设备 Web”（适用于移动设备的移动设备应用程序）。

但是，您（可能）不希望使用 *精确* 所有渠道的内容都相同 — 您需要根据特定渠道优化内容。

内容片段允许您：

* 考虑如何跨渠道高效地访问目标受众。
* 创建和管理渠道中性的可编辑内容。
* 为一系列渠道构建内容池。
* 为特定渠道设计内容变体。
* 通过插入资产将图像添加到文本。
* 创建嵌套内容以反映数据的复杂性。

然后，可以组合这些内容片段以通过各种渠道提供体验。

>[!NOTE]
>
>**内容片段**&#x200B;和&#x200B;**[体验片段](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)**&#x200B;是 AEM 中的两个不同功能：
>* **内容片段**&#x200B;是可编辑内容，具有定义和结构，但无需额外的可视设计和/或布局。它们可用于访问结构化数据，包括文本、数字和日期等。
>* **体验片段**&#x200B;是经过充分布局的内容；例如，网页的一个片段。
>
>体验片段可以包含内容片段形式的内容，反之则不行。
>
>有关详细信息，请参阅 [了解AEM中的内容片段和体验片段](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html#content-fragments).

本页和以下页面介绍了创建、配置、维护和使用内容片段的任务：

* [为您的实例启用内容片段功能](/help/sites-cloud/administering/content-fragments/setup.md)
* [内容片段模型](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)  — 启用、创建和定义模型
* [创建您的内容片段](/help/sites-cloud/administering/content-fragments/managing.md#creating-a-content-fragment) （使用内容片段控制台）

创建片段后，您可以：

* [使用内容片段控制台](/help/sites-cloud/administering/content-fragments/managing.md)  — 访问、发布（预览或生产）和引用片段
* [使用内容片段编辑器](/help/sites-cloud/administering/content-fragments/authoring.md)  — 编辑、发布（预览或生产）和引用您的片段
* [分析](/help/sites-cloud/administering/content-fragments/analysis.md)  使用编辑器的内容片段的结构
* [使用GraphQL访问您的片段，以便向应用程序headless投放](/help/sites-cloud/administering/content-fragments/content-delivery-with-graphql.md).
* [或使用您的片段进行页面创作](/help/sites-cloud/authoring/fundamentals/content-fragments.md)

>[!NOTE]
>
>这些页面可以与以下内容一起阅读：
>
>* [自定义和扩展内容片段](/help/implementing/developing/extending/content-fragments-customizing.md)
>* [内容片段配置用于呈现的组件](/help/implementing/developing/extending/content-fragments-configuring-components-rendering.md)
>* [AEM Assets HTTP API 中的内容片段支持](/help/assets/content-fragments/assets-api-content-fragments.md)
>* [用于内容片段的 AEM GraphQL API](/help/headless/graphql-api/content-fragments.md)
>* [通过内容片段进行页面创作](/help/sites-cloud/authoring/fundamentals/content-fragments.md)。

## 主要和变量 {#main-and-variations}

变体是AEM内容片段的一项重要功能。 它们允许您创建和编辑 **主要** 内容用于特定渠道和场景，使headless内容投放和页面创作更加灵活。

* **主要**

   * **主要** 本身不是变量，而是所有变量的基础。
   * 片段的一个组成部分

      * 每个内容片段都有一个实例 **主要**.
      * **主要** 无法删除。

   * **主要** 可在片段编辑器中的以下位置访问 **[变体](/help/sites-cloud/administering/content-fragments/authoring.md#variations)**.

  >[!NOTE]
  >
  >在可从以下位置访问的编辑器中： **资产** 控制台， **主要** 标记为 **母版**.

* **变体**

   * 特定于编辑目的的片段文本的呈现；可以与渠道相关，但不是强制性的，也可以用于临时本地修改。
   * 创建为的副本 **主要**，但随后可以根据需要进行编辑；变体本身之间通常存在内容重叠。
   * 可以在片段创作期间定义；从左侧面板。
   * 存储在片段中，以帮助避免内容副本的散布。
   * 变体可以是 [已比较和同步](/help/sites-cloud/administering/content-fragments/authoring.md#compare-and-synchronize-rich-text) 替换为 **主要**.
  <!--
  * Can be [Summarized](/help/sites-cloud/administering/content-fragments/authoring.md#summarizing-text) to quickly truncate the text to a predefined length.
  -->

## 内容片段和内容服务 {#content-fragments-and-content-services}

AEM 内容服务旨在概括 AEM 中/来自 AEM 的内容的描述和投放，而不只是关注网页。

它们使用可供任何客户使用的标准化方法，将内容投放到非传统 AEM 网页的渠道。 这些渠道可以包括：

* 单页面应用程序
* 本机移动设备应用程序
* AEM 外部的其他渠道和接触点

使用 JSON 导出程序以 JSON 格式进行投放。

AEM 内容片段可用于描述和管理结构化内容。 结构化内容在可包含各种内容类型的模型中定义；包括文本、数值数据、布尔值、日期和时间等。

随后，此结构化内容与 AEM 核心组件的 JSON 导出功能一起，可用于将 AEM 内容投放到 AEM 页面以外的渠道。

>[!NOTE]
>
>有关 AEM Sites as a Cloud Service 的 Headless 开发的介绍，请参阅 [Headless 和 AEM](/help/headless/introduction.md)。

>[!NOTE]
>
>AEM 还支持片段内容的翻译。 请参阅[翻译资产](/help/assets/translate-assets.md)以了解更多信息。

## 内容类型 {#content-type}

内容片段包括：

* **Sites**&#x200B;功能。

* 存储为&#x200B;**资源**：

   * 内容片段（及其变体）可以从以下内容创建和维护： [内容片段控制台](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console).
   * 在中创作和编辑 [内容片段编辑器](/help/sites-cloud/administering/content-fragments/authoring.md).

* 可使用进行内容交付 [AEM GRAPHQL API](/help/headless/graphql-api/content-fragments.md).

* 中提供 [使用内容片段组件的页面编辑器](/help/sites-cloud/authoring/fundamentals/content-fragments.md) （引用组件）：

   * 此 [内容片段核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html) 可供页面作者使用。 它允许他们以HTML或JSON格式引用和投放所需的内容片段。

内容片段是一种内容结构，其中：

* 没有布局或设计（文本字段可以有文本格式）。
* 独立于投放机制（如页面或渠道）。
* 包含一个或多个[组成部分](#constituent-parts-of-a-content-fragment)。
* 可以[包含或连接到图像](#fragments-with-visual-assets)。

### 包含可视资源的片段 {#fragments-with-visual-assets}

为了让作者更好地控制其内容，可以将图像添加到内容片段和/或与其集成。

资产可以通过多种方式与内容片段一起使用；各具优势：

* as a **内容引用**
* 内部 **多行文本** 字段

### 内容片段的组成部分 {#constituent-parts-of-a-content-fragment}

内容片段资产由以下部分（直接或间接）组成：

* **片段元素**

   * 元素与包含内容的数据字段关联。
   * 您使用 [内容片段模型](/help/sites-cloud/administering/content-fragments/content-fragment-models.md) 创建内容片段。 模型中指定的元素（字段）定义片段的结构。 这些元素（字段）可以包含多种数据类型。

* **片段段落**

   * 以单个实体分隔的文本块，通常为多行。

   * 在页面创作期间启用内容控制。

* **片段元数据**

   * 使用[资源元数据架构](/help/assets/metadata-schemas.md)。
   * 标记可在以下情况下创建：

      * 创建和创作片段
      * 或以后，当你 [查看或编辑属性](/help/sites-cloud/administering/content-fragments/authoring.md#view-properties-tags) 在片段编辑器中时

  >[!CAUTION]
  >
  >元数据处理配置文件不适用于内容片段。

  >[!CAUTION]
  >
  >内容片段模型通常可以定义名为的数据字段 **标题** 和 **描述**. 如果存在这两个字段，则它们是用户定义的字段，可以在编辑器的内容区域中更新。
  >
  >内容片段及其变体还具有称为的元数据（属性）字段 **标题** 和 **描述**. 这两个元数据字段是任何内容片段和变体的组成部分，最初在创建片段时定义。 可以在编辑器的属性/元数据区域中更新它们。

* **[主要](#main-and-variations)**
* **[变体](#main-and-variations)**

### 片段必需 {#required-by-fragments}

要创建内容片段，您需要：

* **内容模型**

   * [使用配置浏览器启用](/help/sites-cloud/administering/content-fragments/setup.md)。
   * [使用工具创建](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)。
   * 需要[创建片段](/help/sites-cloud/administering/content-fragments/managing.md#creating-content-fragments)。
   * 定义片段的结构（标题、内容元素、标记定义）。
   * 内容片段模型定义需要一个标题和一个数据元素；其他内容都是可选的。
   * 模型可定义默认内容（如果适用）。
   * 作者在创作片段内容时无法更改定义的结构；但他们可以从片段编辑器中打开模型编辑器。
   * 创建从属内容片段后对模型所做的更改可能会影响这些内容片段。

要将内容片段用于Headless内容投放，您还需要：

* a [GraphQL查询](/help/headless/graphql-api/content-fragments.md) 以请求所需的内容
* 然后，可使用此内容来开发您自己的SPA for AEM；有关更多信息，请查看以下文档：

   * [SPA WKND 教程](/help/implementing/developing/hybrid/wknd-tutorial.md)
   * [使用 React 快速入门](/help/implementing/developing/hybrid/getting-started-react.md)
   * [使用 Angular 快速入门](/help/implementing/developing/hybrid/getting-started-angular.md)

要将内容片段用于页面创作，您还需要：

* A **内容片段组件**

   * 有助于以 HTML 和/或 JSON 格式传送片段。
   * 需要[在页面上引用片段](/help/sites-cloud/authoring/fundamentals/content-fragments.md)。
   * 负责片段的布局和投放；例如，渠道。
   * 片段需要一个或多个专用组件来定义布局并投放部分或全部元素/变体和关联内容。
   * 在创作中将片段拖动到页面上会自动关联所需的组件。
   * 请参阅 [内容片段核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html).

## 使用示例 {#example-usage}

片段及其元素和变体可用于为多个渠道创建一致的内容。 在设计片段时，您需要考虑将使用的内容以及在何处。

### WKND 示例 {#wknd-sample}

此 [WKND站点和WKND已共享](/help/implementing/developing/introduction/develop-wknd-tutorial.md) 提供的示例可帮助您了解AEMas a Cloud Service。

<!-- CHECK: which links can/should be used these days? -->

WKND 项目包括：

* 在以下位置提供的内容片段模型：

   * `.../libs/dam/cfm/models/console/content/models.html/conf/wknd`

   * `.../ui#/aem/libs/dam/cfm/models/console/content/models.html/conf/wknd-shared`

* 在以下位置提供的内容片段（和其他内容）：

   * `.../assets.html/content/dam/wknd/en`
