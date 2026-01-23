---
title: 使用内容片段的概念和最佳实践概述
description: 了解Adobe Experience Manager (AEM) as a Cloud Service中的内容片段如何允许您创建和使用结构化内容；非常适用于Headless投放和页面创作。
feature: Content Fragments
role: User, Developer
exl-id: ce9cb811-57d2-4a57-a360-f56e07df1b1a
solution: Experience Manager Sites
source-git-commit: b3e1d3a3770531728d696be125f074881f179573
workflow-type: tm+mt
source-wordcount: '2401'
ht-degree: 71%

---

# 使用内容片段 — 概念和最佳实践 {#working-with-content-fragments-concepts-and-best-practices}

通过Adobe Experience Manager (AEM) as a Cloud Service，内容片段允许您设计、创建、管理和发布独立于页面的内容。 它们允许您准备内容以准备在多个位置和多个渠道上使用，非常适合[Headless投放](/help/headless/what-is-headless.md)和[页面创作](/help/sites-cloud/authoring/fragments/content-fragments.md)。

>[!TIP]
>
>内容片段可以[发布到Edge Delivery Services。](https://www.aem.live/developer/content-fragment-overlay)

>[!IMPORTANT]
>
>此部分中描述的许多功能仅&#x200B;*在* Unified Shell[中可用](/help/overview/aem-cloud-service-on-unified-shell.md)；因此&#x200B;*联机* Adobe Experience Manager (AEM) as a Cloud Service，而不是本地实例。

>[!IMPORTANT]
>
>可从&#x200B;**内容片段**&#x200B;和&#x200B;**资源**&#x200B;这两个控制台访问内容片段。
>
>还有两个编辑器用于创作内容片段；尽管基本功能相同，但存在一些差异。 两个编辑器都可从两个控制台中访问。
>
>此部分涉及&#x200B;**内容片段**&#x200B;控制台和&#x200B;*新*&#x200B;的内容片段编辑器。这些是专为 Headless 内容投放开发而成（虽然它们可用于所有场景）
>
>有关更多信息，请参阅：
>
>* 使用&#x200B;**资源**&#x200B;控制台[管理内容片段](/help/assets/content-fragments/content-fragments-managing.md)
>* 使用&#x200B;[*原始*&#x200B;内容片段编辑器](/help/assets/content-fragments/content-fragments-variations.md)
>* 使用[内容片段创作页面](/help/sites-cloud/authoring/fragments/content-fragments.md)。


内容片段包含结构化内容：

* 每个片段均基于一个[内容片段模型](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md)。
   * [内容片段模型定义了生成片段的结构](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)。
* 每个片段都由以下各项组成：
   * **[主控](#main-and-variations)** - 片段的组成部分，其中容纳核心内容；始终存在且无法删除
   * **[变体](#main-and-variations)** - 作者创建的内容的一个或多个排列组合
* 此结构可以介于以下两种之间：
   * 基本
      * 例如，单个多行文本字段。
      * 可用于准备简单明了的内容以供创作页面时使用。
      * 也可用于按 Headless 方式投放到您的应用程序。
   * 复杂
      * 多种数据类型（包括文本、数字、布尔值、日期和时间等）字段的组合。
      * 可用于准备更加结构化的内容以供创作页面或用于按 Headless 方式投放到您的应用程序。
   * 嵌套
      * 可用的引用数据类型允许您嵌套内容。
      * 往往用于按 Headless 方式投放到您的应用程序。

还可使用 AEM 核心组件的 Sling 模型 (JSON) 导出功能，以 JSON 格式投放内容片段。此投放形式：

* 允许您使用组件管理要投放片段的哪些元素
* 可批量投放；通过在用于 API 投放的页面上添加多个[内容片段核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=zh-Hans)

通信渠道的数量在逐年增加。通常，渠道称为投放机制，如：

* 物理渠道；例如，台式机、移动设备。
* 实物渠道中的投放形式；例如，“产品详细信息页面”、“产品类别页面”（适用于桌面）或“移动设备 Web”（适用于移动设备的移动设备应用程序）。

但是，您（可能）不想将&#x200B;*完全*&#x200B;相同的内容用于所有渠道 - 因此您需要根据特定渠道优化您的内容。

内容片段允许您：

* 考虑如何跨渠道高效地访问目标受众。
* 创建和管理渠道中性的可编辑内容。
* 为一系列渠道构建内容池。
* 为特定渠道设计内容变体。
* 通过插入资源，将图像添加到您的文本。
* 创建嵌套内容以反映数据的复杂性。

然后，可组装这些内容片段以通过多种渠道提供体验。

>[!NOTE]
>
>**内容片段**&#x200B;和&#x200B;**[体验片段](/help/sites-cloud/authoring/fragments/content-fragments.md)**&#x200B;是 AEM 中的两个不同功能：
>
>* **内容片段**&#x200B;是可编辑内容，具有定义和结构，但无需额外的可视设计和/或布局。它们可用于访问结构化数据，包括文本、数字和日期等。
>* **体验片段**&#x200B;是经过充分布局的内容；例如，网页的一个片段。
>
>体验片段可以包含内容片段形式的内容，反之则不行。
>
>有关详细信息，请参阅[了解 AEM 中的内容片段和体验片段](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html?lang=zh-Hans#content-fragments)。

本页和以下各页涉及创建、配置、维护和使用内容片段的任务：

* [为您的实例启用内容片段功能](/help/sites-cloud/administering/content-fragments/setup.md)
* [内容片段模型](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md) — 启用、创建和[定义您的模型](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)
* [创建内容片段](/help/sites-cloud/administering/content-fragments/managing.md#creating-a-content-fragment)（使用内容片段控制台）

创建片段后，您可以：

* [使用内容片段控制台](/help/sites-cloud/administering/content-fragments/managing.md) -：
   * 访问、发布（预览或生产）和引用您的片段
* [使用内容片段编辑器](/help/sites-cloud/administering/content-fragments/authoring.md) -：
   * 编辑、发布（用于预览或生产）和引用您的片段
   * 使用评论与其他作者协作
* 使用编辑器[分析](/help/sites-cloud/administering/content-fragments/analysis.md)您的内容片段的结构
* [用 GraphQL 访问您的片段，以供按 Headless 投放到您的应用程序](/help/sites-cloud/administering/content-fragments/content-delivery-with-graphql.md)。
* [在Adobe Journey Optimizer中集成和使用您的内容片段](/help/sites-cloud/administering/content-fragments/content-fragments-with-journey-optimizer.md)
* 创建并管理[内容片段的启动项](/help/sites-cloud/administering/content-fragments/launches-for-content-fragments.md)
* [或使用您的片段创作页面](/help/sites-cloud/authoring/fragments/content-fragments.md)

>[!NOTE]
>
>可与以下各项一起阅读这些页面：
>
>* [自定义和扩展内容片段](/help/implementing/developing/extending/content-fragments-customizing.md)
>* [内容片段配置用于呈现的组件](/help/implementing/developing/extending/content-fragments-configuring-components-rendering.md)
>* [AEM Assets HTTP API 中的内容片段支持](/help/assets/content-fragments/assets-api-content-fragments.md)
>* [用于内容片段的 AEM GraphQL API](/help/headless/graphql-api/content-fragments.md)
>* [用内容片段创作页面](/help/sites-cloud/authoring/fragments/content-fragments.md)。
>* [内容片段和内容片段模型 OpenAPI](/help/headless/content-fragment-openapis.md) 也可用。


## 主控和变体 {#main-and-variations}

变体是 AEM 的内容片段的一项重要功能。通过变体，可创建和编辑&#x200B;**主控**&#x200B;内容的副本以供在特定渠道和场景上使用，从而更加灵活地投放 Headless 内容和创作页面。

* **主控**

   * **主控**&#x200B;本身不是变体，而是所有变体的基础。
   * 片段的一个组成部分

      * 每个内容片段都有一个&#x200B;**主控**&#x200B;实例。
      * 无法删除&#x200B;**主控**。

   * 可在片段编辑器中的&#x200B;**[变体](/help/sites-cloud/administering/content-fragments/authoring.md#variations)**&#x200B;下访问&#x200B;**主控**。

  >[!NOTE]
  >
  >在可从&#x200B;**资源**&#x200B;控制台找到的编辑器中，**主控**&#x200B;称为&#x200B;**主要**。

* **变体**

   * 特定于编辑目的的片段文本的呈现；可以与渠道相关，但不是强制性的，也可以用于临时本地修改。
   * 创建为&#x200B;**主控**&#x200B;的副本，但随后可以根据需要进行编辑；在变体本身之间经常有内容相同的情况。
   * 可在创作片段期间从左侧面板定义变体。
   * 存储在片段中，以帮助避免内容副本分散在多处。
   * 变体可以与&#x200B;**主控**&#x200B;进行[比较和同步](/help/sites-cloud/administering/content-fragments/authoring.md#compare-and-synchronize-rich-text)。
  <!--
  * Can be [Summarized](/help/sites-cloud/administering/content-fragments/authoring.md#summarizing-text) to quickly truncate the text to a predefined length.
  -->

## 内容片段和内容服务 {#content-fragments-and-content-services}

AEM 内容服务旨在概括 AEM 中/来自 AEM 的内容的描述和投放，而不只是关注网页。

它们使用可供任何客户使用的标准化方法，将内容投放到非传统 AEM 网页的渠道。这些渠道可以包括：

* 单页面应用程序
* 本机移动设备应用程序
* AEM 外部的其他渠道和接触点

使用 JSON 导出程序以 JSON 格式进行投放。

AEM 内容片段可用于描述和管理结构化内容。结构化内容在可包含各种内容类型的模型中定义；包括文本、数值数据、布尔值、日期和时间等。

随后，此结构化内容与 AEM 核心组件的 JSON 导出功能一起，可用于将 AEM 内容投放到 AEM 页面以外的渠道。

>[!NOTE]
>
>有关 AEM Sites as a Cloud Service 的 Headless 开发的介绍，请参阅 [Headless 和 AEM](/help/headless/introduction.md)。

>[!NOTE]
>
>AEM 还支持片段内容的翻译。请参阅[翻译资产](/help/assets/translate-assets.md)以了解更多信息。

## 内容类型 {#content-type}

内容片段包括：

* **Sites**&#x200B;功能。

* 存储为&#x200B;**资源**：

   * 可以从[内容片段控制台](#content-fragments-console)创建和维护内容片段（及其变体）。
   * 在[内容片段编辑器](/help/sites-cloud/administering/content-fragments/authoring.md)中创作和编辑。

* 可使用 [AEM GraphQL API](/help/headless/graphql-api/content-fragments.md) 访问内容片段以供投放内容。

* 可通过使用（引用组件的）[内容片段组件](/help/sites-cloud/authoring/fragments/content-fragments.md)在页面编辑器中找到内容片段：

   * 页面作者有[内容片段核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=zh-Hans)可用。使其可按 HTML 或 JSON 格式引用和投放所需的内容片段。

内容片段是一个具有以下性质的内容结构：

* 没有布局或设计（对于文本字段可设置文本格式）。
* 独立于投放机制（例如，页面或渠道）。
* 包含一个或多个[组成部分](#constituent-parts-of-a-content-fragment)。
* 可以[包含或连接到图像](#fragments-with-visual-assets)。

### 带有视觉资源的片段 {#fragments-with-visual-assets}

为了让作者更好地控制其内容，可以将图像添加到内容片段和/或与其集成。

有多种方式可与内容片段一起使用资源；每种方式各具优势：

* 作为&#x200B;**内容引用**
* 用在&#x200B;**多行文本**&#x200B;字段中

### 内容片段的组成部分 {#constituent-parts-of-a-content-fragment}

内容片段资源由以下部分（直接或间接）组成：

* **片段元素**

   * 元素与包含内容的数据字段关联。
   * 您可以使用[内容片段模型](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md)创建内容片段。模型中指定的元素（字段）[定义片段](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)的结构。 这些元素（字段）可以包含多种数据类型。

* **片段段落**

   * 作为单独实体隔开的文本块，一般为多行。

   * 可在创作页面期间控制内容。

* **片段元数据**

   * 使用[资源元数据架构](/help/assets/metadata-schemas.md)。
   * 标记可在以下情况下创建：

      * 创建和创作片段
      * 或者，稍后在片段编辑器中[查看或编辑属性](/help/sites-cloud/administering/content-fragments/authoring.md#view-properties-tags)时

  >[!CAUTION]
  >
  >元数据处理配置文件不适用于内容片段。

  >[!CAUTION]
  >
  >内容片段模型通常可以定义名为&#x200B;**标题**&#x200B;和&#x200B;**描述**&#x200B;的数据字段。如果存在这两个字段，则它们是用户定义的字段，并可在编辑器的内容区域中更新这些字段。
  >
  >内容片段及其变体也具有名为&#x200B;**标题**&#x200B;和&#x200B;**描述**&#x200B;的元数据（属性）字段。这两个元数据字段是任何内容片段和变体的组成部分，并在创建该片段时初始定义这两个字段。可在编辑器的属性/元数据区域中更新它们。

* **[主控](#main-and-variations)**
* **[变体](#main-and-variations)**

### 片段必需 {#required-by-fragments}

要创建内容片段，您需要：

* **内容模型**

   * [使用配置浏览器启用](/help/sites-cloud/administering/content-fragments/setup.md)。
   * 是[使用内容片段控制台](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#creating-a-content-fragment-model)创建的。
   * 需要[创建片段](/help/sites-cloud/administering/content-fragments/managing.md#creating-content-fragments)。
   * 定义片段的结构（标题、内容元素、标记定义）。
   * 内容片段模型定义需要标题和数据元素；其他一切均为可选。
   * 模型可定义默认内容（如果适用）。
   * 作者在创作片段内容时无法更改已定义的结构；但是，他们可从片段编辑器中打开模型编辑器。
   * 已创建从属的内容片段后对模型作出的更改可能会影响这些内容片段。

要使用您的内容片段投放 Headless 内容，您还需要：

* [GraphQL 查询](/help/headless/graphql-api/content-fragments.md)以请求所需内容
* 然后可使用此内容开发您自己用于 AEM 的 SPA；有关详细信息，请查看以下文档：

   * [SPA WKND 教程](/help/implementing/developing/hybrid/wknd-tutorial.md)
   * [使用 React 快速入门](/help/implementing/developing/hybrid/getting-started-react.md)
   * [使用 Angular 快速入门](/help/implementing/developing/hybrid/getting-started-angular.md)

要使用您的内容片段创作页面，您还需要：

* **内容片段组件**

   * 有助于以 HTML 和/或 JSON 格式传送片段。
   * 需要[在页面上引用片段](/help/sites-cloud/authoring/fragments/content-fragments.md)。
   * 负责片段的布局和投放；例如，渠道。
   * 片段需要一个或多个专用组件以定义布局和投放部分或全部元素/变体和关联的内容。
   * 在创作中将片段拖动到页面上将自动关联所需的组件。
   * 请参阅[内容片段核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=zh-Hans)。

## 内容片段控制台 {#content-fragments-console}

内容片段控制台专门用于管理、搜索和创建[内容片段](/help/sites-cloud/administering/content-fragments/managing.md)、[内容片段模型](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md)和[Assets](/help/sites-cloud/administering/content-fragments/assets-content-fragments-console.md)。 它已针对在Headless上下文中使用进行了优化，但在创建用于页面创作的内容片段和内容片段模型时也会使用。

可以从全局导航的顶级直接访问该控制台。

![全局导航 – 内容片段控制台](assets/cf-managing-global-navigation.png)

您可以使用最左侧的面板选择要查看、浏览和管理的资源类型：

![内容片段控制台 — 导航](/help/sites-cloud/administering/content-fragments/assets/cf-console-assets-navigation.png)

有关详细信息，请参阅：

* [内容片段](/help/sites-cloud/administering/content-fragments/managing.md)
* [内容片段模型](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md)
* [Assets](/help/sites-cloud/administering/content-fragments/assets-content-fragments-console.md)

* 有一批[键盘快捷键](/help/sites-cloud/administering/content-fragments/keyboard-shortcuts.md)在此控制台中可用

>[!CAUTION]
>
>*只有*&#x200B;在线 Adobe Experience Manager (AEM) as a Cloud Service 中有此控制台可用。

>[!NOTE]
>
>如有必要，您的项目团队可以自定义控制台和编辑器。 有关进一步详细信息，请参阅[自定义内容片段控制台和编辑器](/help/implementing/developing/extending/content-fragments-console-and-editor.md)。

## 使用示例 {#example-usage}

片段及其元素和变体可用于为多个渠道创建一致的内容。在设计您的片段时，您需要考虑将使用什么和将在哪里使用。

### WKND 示例 {#wknd-sample}

提供 [WKND Sites 和 WKND Shared](/help/implementing/developing/introduction/develop-wknd-tutorial.md) 示例以帮助您了解 AEM as a Cloud Service。

<!-- CHECK: which links can/should be used these days? -->

WKND 项目包括：

* 在以下位置提供的内容片段模型：

   * `.../libs/dam/cfm/models/console/content/models.html/conf/wknd`

   * `.../ui#/aem/libs/dam/cfm/models/console/content/models.html/conf/wknd-shared`

* 在以下位置提供的内容片段（和其他内容）：

   * `.../assets.html/content/dam/wknd/en`

## 最佳做法 {#best-practices}

内容片段可用于形成复杂的结构。 Adobe提供了在定义和使用模型和片段时的最佳实践建议。

### 保持简单 {#keep-it-simple}

在AEM中为结构化内容建模时，应尽可能简化内容结构，以确保强大的系统性能和简化的管理。

### 模型数量 {#number-of-models}

根据需要创建尽可能多的内容模型，但不再创建。

模型过多，使治理复杂化，并且可能会减慢GraphQL查询速度。 一小部分模型（最多几十个）通常就足够了。 如果您接近数十或更高，请重新考虑建模策略。

### 嵌套模型和片段（非常重要） {#nesting-models-and-fragments}

使用内容片段引用避免对内容片段进行深嵌套或过度嵌套，这类引用允许片段引用其他片段，有时会跨多个级别。

大量使用内容片段引用可能会显着影响系统性能、UI响应性和GraphQL查询执行。 力求嵌套不超过10级。

### 每个模型的数据字段数和类型数 {#number-of-data-fields-and-types-per-model}

仅包括模型真正需要的数据字段和类型。

过于复杂的模型会导致片段过于复杂，这会增加创作难度并降低编辑器性能。

### 富文本字段 {#rich-text-fields}

请考虑使用富文本字段（**多行文本**&#x200B;数据类型）：

* 字段

  限制每个模型的富文本字段数。 出于性能原因，建议不要在一个模型中使用十个以上的富文本字段。 如果需要，建议您使用[嵌套内容片段](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#using-references-to-form-nested-content)。

* 内容

  您还应限制每个片段中存储的文本数量，以及HTML格式化的数量。 非常大的富文本内容可能会对系统性能产生负面影响。

### 变体数量 {#number-of-variations}

创建所需数量的片段变体，但不再创建。

变体在创作环境中和投放时都会向内容片段添加处理时间。 建议将变体的数量保持在可管理的最小值。

最佳实践为每个内容片段不超过10个变量。

### 生产前测试 {#test-before-production}

如有疑问，请在将预期内容结构推出到生产环境之前为其创建原型。 早期的概念验证以及充分的技术和用户验收测试，有助于避免以后在生产中遇到截止日期时发生问题。