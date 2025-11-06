---
title: 通用编辑器简介
description: 通用编辑器是一种现代可视化创作工具，旨在帮助您的营销组织创造具有影响力的网络体验。
exl-id: d4fc2384-a0f5-4a6f-9572-62749786be4c
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 100%

---


# 通用编辑器简介 {#introduction}

通用编辑器是一种现代可视化创作工具，旨在帮助您的营销组织创造具有影响力的网络体验。

## 概述 {#overview}

通用编辑器是一个多功能可视化编辑器，是 Adobe Experience Manager Sites 的一部分。它使作者能够以所见即所得 (WYSIWYG) 的方式对任何无头或有头体验进行编辑。它提供：

* **即时编辑**：作者可以在预览体验中直接编辑内容，无需定位和导航到各个内容源。
* **可视化编辑**：进行更改时，作者可以立即看到更改如何影响实际的访问者体验，从而最大限度地减少阻力。
* **可发现的选项**：清晰标记的选项和直观的用户界面使作者能够轻松配置元数据和编写布局。
* **非技术性**：无需专业知识即可进行编辑，而且自动强制执行企业品牌指南，促进整个组织的内容任务扩展。
* **集成和可扩展性**：与 AEM 完全集成，通用编辑器灵活的[扩展点](#extensibility)允许所有基本工具都集中在同一个统一的界面中。从 AI 驱动的功能到专为您的独特业务需求定制的自定义扩展，它使团队能够简化工作流，轻松提高生产力。

总结来说：

* **作者能够获益于**&#x200B;通用编辑器的灵活性，因为它支持为所有 AEM 内容的表单进行相同、一致的可视化编辑。
* **开发人员能够获益于**&#x200B;通用编辑器的多功能性，因为它支持对实施的真正解耦。

通用编辑器是一种真正的“编辑器即服务”，整体更加灵活，旨在最终取代[页面编辑器。](/help/sites-cloud/authoring/page-editor/introduction.md)

## 受支持的架构 {#supported-architectures}

通用编辑器支持以下两种主要 AEM 设置：

1. **[Edge Delivery Services](/help/edge/overview.md)**：这是首选方法，因为它简单、价值实现更快、性能更强。
1. **[无头实施](/help/headless/introduction.md)**：如果您已有一个无头项目或者有特定的解耦渲染要求，通用编辑器允许进行企业级可视化编辑，无需重构整个项目。它几乎与任何架构（SSR、CSR）、Web 框架（Next.js、React、Astro 等）和托管模型（“自带应用”）兼容。

>[!TIP]
>
>请参阅文档[通用编辑器用例和学习路径](/help/implementing/universal-editor/use-cases.md)，了解有关受支持架构的更多详细信息。

## 受支持的 AEM 版本 {#aem-versions}

通用编辑器受到以下支持：

* AEM as a Cloud Service（`2023.8.13099` 或更高版本）
* [AEM 6.5 LTS](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-65-lts/content/implementing/developing/headless/universal-editor/introduction)
   * 支持内部部署和 AMS 托管。
* [AEM 6.5](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-65/content/implementing/developing/headless/universal-editor/introduction)
   * 支持内部部署和 AMS 托管。

本文档介绍了通用编辑器与 AEM as a Cloud Service 的使用。

## 功能 {#features}

通用编辑器提供许多功能来支持广泛的用例，实现高效的内容管理。

* **[所见即所得](/help/sites-cloud/authoring/universal-editor/authoring.md)**：以所见即所得的方式编辑任何形式的 Web 内容，包括纯文本、富文本、媒体和元数据。
* **[构成](/help/sites-cloud/authoring/universal-editor/authoring.md#editing-content)**：创建、编辑、重新排序、嵌套或删除各种类型的内容块（标题、按钮、Teaser、分区、嵌入等）。
* **[布局](/help/sites-cloud/authoring/universal-editor/templates.md)**：使用页面模板，应用视觉样式，使用列、轮播和折叠项等区块编写布局。
* **[设备模拟](/help/sites-cloud/authoring/universal-editor/navigation.md#emulator)**：编辑时预览并优化针对不同访问者设备的内容。
* **全渠道**：为多个渠道重复使用结构化和非结构化内容。
* **[本地化](/help/sites-cloud/authoring/universal-editor/inheritance.md)**：使用多网站管理器简化内容翻译工作流，有效处理本地化内容的继承。
* **一致性**：确保遵守品牌指南，保持所有内容的统一性。
* **安全性**：[强制执行访问控制](/help/implementing/universal-editor/authentication.md)，保护内容完整性，通过[强大的版本控制](/help/sites-cloud/authoring/sites-console/page-versions.md)跟踪更改。
* **[发布](/help/sites-cloud/authoring/universal-editor/publishing.md)**：直接在编辑器中集成审阅、审批和发布工作流。
* **统一**：与 AEM 工具完全集成，例如 [Sites 控制台、](/help/sites-cloud/authoring/sites-console/introduction.md)[内容片段编辑器](/help/sites-cloud/administering/content-fragments/overview.md)等，提供一种综合性创作体验。

## 可扩展性 {#extensibility}

通用编辑器不仅开箱即用，而且提供了许多扩展可能性。

* 有大量的现成&#x200B;**扩展**，可以满足各种需求，例如支持工作流、生成变体以及支持试验等等。
* **可扩展的用户界面**&#x200B;允许您使用现成扩展所采用的相同底层框架创建您自己的扩展，从而实现最大的灵活性，以满足您的项目需求。
* 区块、自定义数据类型和事件等&#x200B;**扩展点**&#x200B;允许无缝集成 UI 之外的自定义业务要求。

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

当您探索通用编辑器，并在您自己的项目中实施时，请记住以下限制。

* 一个页面上作为适配引用的 AEM 资源（内容片段、页面、体验片段、资产等）不得超过 25 个。
* 只有 AEM as a Cloud Service、[AEM 6.5 LTS](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-65-lts/content/implementing/developing/headless/universal-editor/introduction) 和 [AEM 6.5](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-65/content/implementing/developing/headless/universal-editor/introduction) 是受支持的 AEM 后端。
* AEM as a Cloud Service 需要版本 `2023.8.13099` 或更高。
* 内容作者必须拥有自己的个人 Experience Cloud 帐户。
* 作为 AEM 的一部分，通用编辑器[支持与 AEM 相同的桌面浏览器。](/help/overview/supported-platforms.md)
   * 这些浏览器的移动版本不受支持。

{{ip-allow-lists-ue}}

## 后续步骤 {#next-steps}

请参阅文档[通用编辑器用例和学习路径](/help/implementing/universal-editor/use-cases.md)，了解有关通用编辑器常见用例的更多信息，并找到合适的文档资源来支持您的项目。
