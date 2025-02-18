---
title: Universal Editor 简介
description: 通用编辑器是一款现代化的可视化创作工具，旨在使您的营销组织能够产生富有影响力的Web体验。
exl-id: d4fc2384-a0f5-4a6f-9572-62749786be4c
feature: Developing
role: Admin, Architect, Developer
source-git-commit: ae962d89b842b0708c1ac8633bb49c86cb2edfda
workflow-type: tm+mt
source-wordcount: '949'
ht-degree: 13%

---


# Universal Editor 简介 {#introduction}

通用编辑器是一款现代化的可视化创作工具，旨在使您的营销组织能够产生富有影响力的Web体验。

## 概述 {#overview}

通用编辑器是一个通用的可视化编辑器，它是Adobe Experience Manager Sites的一部分。 它允许创作者对任何Headless或Headful体验执行“所见即所得”(WYSIWYG)编辑。 它提供：

* **即时编辑**：作者可以直接在预览体验中编辑内容，而无需查找和导航到各个内容源。
* **可视化编辑**：进行更改时，作者会立即看到更改如何影响实际访客体验，从而最大限度地减少摩擦。
* **可发现选项**：标签明确的选项和直观的UI使作者能够轻松配置元数据和撰写布局。
* **非技术**：进行编辑不需要专业知识，而公司品牌指南会自动强制执行，从而便于在整个组织中扩展内容任务。
* **集成性和可扩展性**：与AEM完全集成，Universal Editor的灵活[扩展点](#extensibility)允许所有基本工具在单个有凝聚力的界面中统一。 从AI支持的功能到根据您独特的业务需求而定制的自定义扩展，它使团队能够轻松简化工作流并提高工作效率。

总而言之：

* **作者得益于通用编辑器的灵活性，因为它支持对所有形式的AEM内容进行相同一致的可视化编辑。**
* **开发人员从Universal Editor的多功能性中获益**，因为它支持实现真正的脱钩。

作为真正的editor-as-a-service并且总体更灵活，通用编辑器打算最终取代[页面编辑器。](/help/sites-cloud/authoring/page-editor/introduction.md)

## 支持的体系结构 {#supported-architectures}

通用编辑器支持以下两个主要的AEM设置：

1. **[Edge Delivery Services](/help/edge/overview.md)**：这是首选方法，因为它具有简单性、更快的价值实现和增强的性能。
1. **[Headless实施](/help/headless/introduction.md)**：如果您现有Headless项目或针对分离渲染的特定要求，则通用编辑器允许企业级可视化编辑，而无需重构整个项目。 它可与几乎任何架构(SSR、CSR)、Web框架（Next.js、React、Astro等）和托管模型（“自带应用程序”）兼容。

>[!TIP]
>
>有关支持的体系结构的更多详细信息，请参阅文档[通用编辑器用例和学习路径](/help/implementing/universal-editor/use-cases.md)。

## 支持的AEM版本 {#aem-versions}

以下内容支持通用编辑器：

* AEM as a Cloud Service（版本`2023.8.13099`或更高版本）
* AEM 6.5（Service Pack 21或22以及功能包）

本文档介绍如何将通用编辑器与AEM as a Cloud Service结合使用。 有关在AEM 6.5中使用通用编辑器的信息，[请参阅AEM 6.5文档。](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/implementing/developing/headless/universal-editor/introduction?lang=en)

## 功能 {#features}

通用编辑器提供了许多功能，可支持各种用例以实现高效的内容管理。

* **[WYSIWYG](/help/sites-cloud/authoring/universal-editor/authoring.md)**：对任何形式的Web内容（包括纯文本、富文本、媒体和元数据）执行“所见即所得”编辑。
* **[排版](/help/sites-cloud/authoring/universal-editor/authoring.md#editing-content)**：创建、编辑、重新排序、嵌套或删除各种类型（标题、按钮、Teaser、分区、嵌入等）的内容块。
* **[布局](/help/sites-cloud/authoring/universal-editor/templates.md)**：利用页面模板，应用可视化样式，并使用列、轮播和折叠等块撰写布局。
* **[设备模拟](/help/sites-cloud/authoring/universal-editor/navigation.md#emulator)**：编辑时预览和优化不同访客设备的内容。
* **全渠道**：跨多个渠道重用结构化和非结构化内容。
* **[本地化](/help/sites-cloud/authoring/universal-editor/inheritance.md)**：通过多站点管理器简化内容翻译工作流并高效处理本地化的内容继承。
* **一致性**：确保遵循品牌准则并保持所有内容的一致性。
* **安全性**： [强制访问控制](/help/implementing/universal-editor/authentication.md)，保护内容完整性，并使用[可靠的版本控制跟踪更改。](/help/sites-cloud/authoring/sites-console/page-versions.md)
* **[发布](/help/sites-cloud/authoring/universal-editor/publishing.md)**：直接在编辑器中集成审阅、审批和发布工作流。
* **统一**：与AEM工具（如[站点控制台、](/help/sites-cloud/authoring/sites-console/introduction.md) [内容片段编辑器、](/help/sites-cloud/administering/content-fragments/overview.md)等）完全集成，提供有凝聚力的创作体验。

## 可扩展性 {#extensibility}

通用编辑器不仅能够提供开箱即用的功能，而且还提供了多种扩展可能性。

* **扩展**&#x200B;数量众多且准备就绪，可满足支持工作流程、生成变体和启用试验等需求。
* **可扩展UI**&#x200B;允许您使用现成扩展所利用的基础框架创建自己的扩展，这些框架使您能够灵活地适应项目需求。
* **扩展点**，例如块、自定义数据类型和事件，允许无缝集成UI之外的自定义业务要求。

>[!TIP]
>
>有关通用编辑器可扩展性的更多信息，请参阅文档[扩展通用编辑器。](/help/implementing/universal-editor/extending.md)

## 内容片段编辑器中的 Universal Editor {#universal-editor-content-fragment-editor}

乍一看，Universal Editor 和内容片段编辑器似乎提供了类似的编辑功能。但这些编辑器却提供了完全不同的功能，并且它们为营销从业人员完成了不同的作业。

### 内容片段编辑器 {#content-fragment-editor}

营销从业人员希望创建内容而不必关注其布局，以便它能够在多种体验环境中重复使用。

* 要完成的基本作业是扩展内容策略。

### Universal Editor {#universal-editor}

营销从业人员想创建根据给定上下文的布局定制的内容，以提供卓越的体验。

* 要完成的基本作业是与读者建立令人信服的联系。

## 限制 {#limitations}

当您探索通用编辑器并在自己的项目中进一步实施时，请牢记以下限制。

* 在单个页面上，作为工具引用的AEM资源(内容片段、页面、体验片段、Assets等)不得超过25个。
* AEM as a Cloud Service和[AEM 6.5](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-65/content/implementing/developing/Headless/universal-editor/introduction)是唯一受支持的AEM后端。
* AEM as a Cloud Service需要版本`2023.8.13099`或更高版本。
* 内容作者必须具有自己的各个Experience Cloud帐户。
* 作为AEM的一部分，通用编辑器[支持与AEM相同的桌面浏览器。](/help/overview/supported-platforms.md)
   * 不支持这些浏览器的移动版本。

{{ue-ip-allow-lists}}

## 后续步骤 {#next-steps}

请参阅文档[通用编辑器用例和学习路径](/help/implementing/universal-editor/use-cases.md)，了解有关通用编辑器常见用例的更多信息，并发现可在项目中为您提供支持的正确文档资源。
