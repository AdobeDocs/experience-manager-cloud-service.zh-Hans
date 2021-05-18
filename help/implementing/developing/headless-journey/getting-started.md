---
title: AEM Headless入门Cloud Service
description: 在此部分的AEM无头开发人员历程中，了解AEM无头的先决条件。
hide: true
hidefromtoc: true
index: false
exl-id: a39877d9-f5a1-48f0-a021-cc9849bd8ecb
source-git-commit: 83ed6295d2b29581025f5410236f2618ceb59012
workflow-type: tm+mt
source-wordcount: '3087'
ht-degree: 0%

---

# 将AEM Headless作为Cloud Service{#getting-started}入门

>[!CAUTION]
>
>正在进行中的工作 — 此文档的创建正在进行中，不应理解为完整或明确，也不应将其用于生产目的。

在[AEM无头开发者历程的这一部分中，](overview.md)了解开始使用AEM无头项目所需的操作。

## 迄今为止的故事{#story-so-far}

在AEM无外设旅程的上一个文档中，[了解CMS无外设开发](learn-about.md)您学习了无外设CMS的基本理论，现在您应：

* 了解无外设内容投放的基本概念和术语
* 了解为何和何时需要无头
* 深入了解无外设概念的使用方式及其相互关系

本文以这些基础为基础，因此您了解如何使用AEM实施无外设解决方案。

## 目标 {#objective}

此文档可帮助您在自己项目的上下文中了解AEM无头。 阅读后，您应：

* 了解AEM无外设功能的基础知识。
* 了解使用AEM无外设功能的先决条件。
* 了解AEM无外设集成级别。
* 能够根据范围定义您的项目。

## AEM基础知识{#aem-basics}

在AEM中定义无外设项目之前，了解一些基本的AEM概念非常重要。

### 作者实例 {#author}

最简单的方法是， AEM包含一个作者实例和一个[发布实例](#publish)，这两个实例可共同创建、管理和发布您的内容。

内容从创作实例开始。 内容作者可在此处创建其内容。 作者环境为作者优惠了各种工具，以创建、组织和重复使用其内容。

### 发布实例 {#publish}

在创作实例中创建内容后，必须发布内容，以便其他服务可以使用。 发布实例包含所有已发布的内容。

### 复制 {#replication}

复制是将内容从创作实例传输到发布实例的操作。 当作者或其他具有适当权限的用户发布内容时，AEM会自动执行此操作。

### AEM基础知识摘要{#aem-basics-summary}

在最简单的级别上，在AEM中创建数字体验需要以下步骤：

1. 您的内容作者将在创作实例中创建您的无外设内容。
1. 当此内容准备就绪时，它将复制到发布实例。
1. 然后，可以调用API来检索此内容。

AEM Headless通过提供强大的工具来管理下一节中描述的[无头内容，以此技术基础为基础。](#aem-headless-basics)

## AEM无头基础{#aem-headless-basics}

AEM的无外设功能基于几个关键功能。 这些内容将在旅程的后半部分详细说明。 现在，只有了解他们所做工作的基础知识和所谓的知识才很重要。

### 内容片段模型 {#content-fragment-models}

内容片段模型定义您将在AEM中创建和管理的数据和内容的结构。 它们用作内容的基架。 选择创建内容时，作者将从您定义的内容片段模型中进行选择，这些模型将引导他们创建内容。

### 内容片段 {#content-fragments}

内容片段允许您设计、创建、管理和发布独立于页面的内容。 它们允许您准备内容，准备好在多个位置和多个渠道中使用。

内容片段包含结构化内容，可以以JSON格式提供。

### GraphQL和REST API {#apis}

要无头地修改您的内容，AEM优惠了两个强大的API。

* GraphQL API允许您创建访问和传送内容片段的请求。
* 资产REST API允许您创建和修改内容片段（和其他资产）。

您将了解这些API以及如何在AEM无外设旅程的稍后部分使用它们。 或参阅下面的[其他资源](#additional-resources)部分以获取更多文档。

## 无外设集成级别{#integration-levels}

AEM支持CMS的全无外设和传统的完整堆栈或外设模型。 但AEM不仅优惠了这两种独有的选择，还能够支持混合模型，这两种模型结合了两者的优势，为您的无外设项目提供了独特的灵活性。

为了确保您对无头概念的理解，此AEM无头开发人员历程侧重于纯无头模型，使您能够尽快上手并运行，而无需在AEM中进行编码。

但是，理解AEM无头功能后，您应该会注意到您面临的其他混合可能性。 我们将这些案件列在下面，以便您了解。 在旅程结束时，您将更详细地介绍这些概念，以备您的项目需要此类灵活性。

### 您已经有了对无标题内容的外部消费，如单页应用程序(SPA)。{#already-have-a-spa}

假设您的基本要求至少是将内容从AEM交付到现有的外部服务。

#### 第1级：内容片段集成 — 传统无头模型{#level-1}

此集成级别是传统的无外设模型，它允许内容作者在AEM中创建内容，然后使用GraphQL将内容无缝地交付到任意数量的外部服务，或使用资产API从外部服务编辑内容。 AEM中无需编码。

在此模型中，AEM仅用于通过使用AEM内容片段创建和提供内容。 渲染以及与内容的交互被委托给消费性的外部应用程序，通常是单页应用程序(SPA)。

#### 级别2:将SPA嵌入AEM - Hybrid Model {#level-2}

此级集成构建于第一级，但也允许将外部应用程序(SPA)嵌入到AEM中，以便内容作者可以在AEM内外部应用程序的上下文中视图内容。 该应用程序还支持在AEM内对外部应用程序进行有限编辑。

此级别的优势在于，允许内容作者以强大的方式在AEM中灵活创作内容，其内容与嵌入的外部SPA进行上下文相关展示，同时仍无头地交付内容。

#### 第3级：在AEM中嵌入并完全启用SPA — 混合型号{#level-3}

此级别的集成在第二级的基础上构建，它允许外部SPA中的大多数内容在AEM中进行编辑。

### 您还没有无头内容的外部用户，如单页应用程序(SPA)。{#do-not-have-a-spa}

如果您的目标是创建一个无头地使用AEM内容的新SPA，则可以使用内容片段等功能管理无头内容，还可以使用AEM SPA Editor框架构建SPA。

使用SPA编辑器，SPA不仅会读取AEM中的内容，而且内容作者还可以在AEM中完全编辑，从而使您能够灵活地进行无头投放和AEM中的上下文编辑。

## 要求和先决条件{#requirements-prerequisites}

在开始无头AEM项目之前，有许多要求。

### 知识 {#knowledge}

* GraphQL
* 使用React或Angular框架创建SPA的开发经验
* AEM创建内容片段和使用编辑器的基本技能

### 工具 {#tools}

* 用于测试部署项目的沙箱访问
* 用于数据建模和测试的本地开发实例
* 现有外部SPA或您的无头AEM内容的其他消费者

## 定义项目{#defining-your-project}

对于任何成功的项目，不仅要明确项目的要求，还要明确其角色和责任。

### 范围 {#scope}

明确项目范围非常重要。 范围会通知接受标准并允许您确定完成的定义。

您需要扪心自问的第一个问题是“我如何使用AEM Headless？” 一般来说，答案应该是您已拥有或将来拥有一个使用您自己的开发工具而不是与AEM结合构建的体验应用程序。 此体验应用程序可以是移动应用程序、网站或任何其他面向最终用户的体验应用程序。 使用AEM Headless的目标是在AEM中创建、存储和管理的内容，并借助最新API为您的体验应用程序提供内容，这些API将调用AEM Headless直接从体验应用程序获取内容或甚至完整的CRUD内容。 如果您不希望这样做，您可能希望[返回AEM文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html)并找到最适合您想要完成的部分。

### 角色和责任{#roles-responsibilities}

任何单个项目的角色都会有所不同，但在AEM无外设开发内容中需要考虑的重要角色是：

* [管理员](#administrator)
* [内容作者](#content-author)
* [内容建模器](#content-modeler)
* [开发人员](#developer)

#### 管理员 {#administrator}

管理员负责系统的基本设置和配置。 例如，管理员将在Adobe用户管理系统中设置您的组织，即Identity Management系统(IMS)。 在IMS中的Adobe创建组织后，管理员将是组织中第一个从Adobe接收电子邮件邀请的用户。 管理员将能够登录IMS并添加其他角色的用户。

管理员配置用户后，将授予他们访问所有AEM资源的权限，以完成其使用AEM无头交付体验应用程序的贡献者的工作。

管理员应是设置AEM并准备运行时环境的用户，以使[内容作者](#content-author)能够创建和更新内容，并使[开发人员](#developer)能够使用API获取或修改其体验应用程序的内容。

#### 内容作者{#content-author}

内容作者创建和管理AEM无谓提供的内容。 内容作者使用AEM功能（如内容片段和资产控制台）管理其内容。

内容作者应牢记以下最佳实践。

#### 计划本地化 {#localization}

在项目开始时计划翻译和本地化。 将“国际化项目经理”视为一个单独的角色，其职责是定义哪些内容应进行翻译，哪些内容不进行翻译，哪些翻译的内容可能由区域或本地内容制作者修改。

根据您需要的内容本地化创建计划。

* 您只是需要不同的语言或语言才能采用区域特定语言吗？
* 您是否需要富媒体内容（如图像或视频）在不同区域设置中有所不同？

清楚您的内容更新工作流程。 系统需要支持哪些批准过程？ 是否可能利用AEM工作流来自动化此过程？

请注意，您的[内容层次结构](#content-hierarchy)可以利用它简化本地化。

有关AEM工作流和本地化工具的其他文档，请参阅[其他资源](#additional-resources)部分。

##### 利用内容层次结构{#content-hierarchy}

文件夹层次结构可以解决与内容管理相关的两个主要问题：

* [本地化](#localization) - AEM通过在特定于区域设置的文件夹中维护内容副本来管理内容本地化。
* 组织 — 文件夹用于定义支持本地化需求以及逻辑管理内容片段所需的内容层次结构。

AEM允许非常灵活的内容结构，并且层次结构可以任意大。 但是，必须认识到，对文件夹结构所做的任何更改都可能会对[依赖内容路径的现有查询产生意外的后果。](#developer) 因此，预先明确定义的层次结构对内容作者非常有用。

也可以限制文件夹仅允许某些类型的内容（基于内容片段模型）。 通常建议始终显式指定允许对层次结构中的所有文件夹使用的模型。 指定给定文件夹允许的内容：

* 阻止内容作者创作不属于该文件夹的内容。
* 通过筛选在创建过程中允许在文件夹中显示的内容类型来优化内容创建过程，从而仅显示有效类型的内容。

通过创建适当的内容结构，跨渠道协调无头内容创作变得更加轻松，以便最大化内容重用。 跨多个渠道利用内容将大大提高内容生产效率和更改管理。

##### 建立良好的命名约定{#naming-conventions}

内容片段名称必须为内容作者的描述性。 AEM透明地处理转义和/或截断存储库级别上使用的ID的名称。 因此，内容作者提供的逻辑名称应始终可读并表示内容。

* 错误名称：`cta_btn_1`
* 好名：`Call To Action Button`

有关AEM页面命名约定的其他文档，请参阅[其他资源](#additional-resources)部分。

##### 不要过度扩展内容嵌套{#content-nesting}

[内容](#content-fragments) 片段用在AEM中创建无头内容。AEM支持内容片段多达十级的内容嵌套。 但是，务必记住，AEM需要反复解析父内容片段中定义的每个引用，然后检查所有同级中是否存在任何子引用。 这些操作可以快速累加并成为性能问题。

作为一般经验法则，内容片段引用不应嵌套在五个级别以上。

#### 内容建模器{#content-modeler}

内容建模器可分析需要无头传送的数据需求，并定义此数据的结构。 这些结构在AEM中称为[内容片段模型](#content-fragment-models)。 内容片段模型用作内容作者创建的内容片段的基础。

定义内容片段模型时的一个有用方法是创建映射到将使用内容的应用程序的UX组件的模型。

由于内容作者在创建新内容时不断与模型交互，将模型与UX对齐有助于他们直观地呈现最终的数字体验。 更进一步，您可以将图标指定到表示UX元素的内容片段模型，以便作者能够根据视觉提示直观地选择正确的模型。

#### 开发人员 {#developer}

开发人员负责将在AEM中创建的内容无头地与该内容的消费者结合在一起，该内容通常可以是单页应用程序(SPA)、渐进式Web应用程序(PWA)、Web商店或AEM外部的其他服务。

GraphQL是AEM与无外设内容消费者之间的“纽带”。 GraphQL是查询AEM所需内容的语言。

开发人员在规划查询时应牢记一些基本建议：

* 查询不应依赖固定路径(`ByPath`)来检索内容片段。
   * [内容作者对内容片段层次结构具有](#content-hierarchy) 完全的控制权，并可以进行会破坏此类查询的更改。
   * 查询应选择使用动态查询参数引用内容片段模型，以过滤结果以生成所需的有效负荷。
* 为获得最佳查询性能，请始终在AEM中使用持久查询。 在旅程的稍后部分将讨论这些问题。
* GraphQL设计为遵循格言“请求您确切需要的内容，并准确获得所需内容”的声明性。 这意味着在创建GraphQL查询时，应始终避免在关系查询库中创建`select *`-type。

对于使用AEM的[典型的无头实施，](#level-1)开发人员不需要AEM的编码知识。

### 性能要求{#performance-requirements}

要使任何项目成功，必须在创建任何内容之前考虑性能。

您必须了解您的用户/访客期望，并为此进行设计。 设置服务级别目标(SLO)并衡量它们，了解您是否达到用户的期望。

#### 流量模式{#traffic-patterns}

了解流量和交通模式开始，收集过去所掌握的信息，然后预测未来几年的预期增长。 需要考虑的一些最重要变量：

* 您预计每小时/天/月有多少个API调用，是否存在高峰和季节性？
* 有多少个不同的内容作者？
* 您预计并发工作的内容作者有多少？
* 内容更新的频率是多少？
* 需要多少种内容模型？
* 需要多少个模型实例？

#### 更新频率{#update-frequency}

很多情况下，不同体验部分的内容更新频率不同。 了解这一点对于能够优化CDN和缓存配置非常重要。 这也是[内容建模器](#content-modeler)的重要输入，因为它们设计用于表示您的内容的模型。 请考虑：

* 某些类型的内容必须在特定时间段后过期？
* 是否存在特定于用户的元素，因此无法缓存？

## 下一步是什么{#what-is-next}

现在您已完成了AEM Headless Developer历程的这一部分，您应：

* 了解AEM无外设功能的基础知识。
* 了解使用AEM无外设功能的先决条件。
* 了解AEM无外设集成级别。
* 能够根据范围定义您的项目。

您应继续您的AEM无头旅程，接下来查看文档[使用AEM无头体验的第一条路径](path-to-first-experience.md)，了解如何设置必要的工具以及如何开始考虑在AEM中建模您的数据。

## 其他资源 {#additional-resources}

尽管建议您通过查看文档[使用AEM无头体验的第一条路径，进入无头开发旅程的下一部分，](path-to-first-experience.md)以下是一些附加的可选资源，可以更深入地了解本文档中提到的某些概念，但无需继续无头开发旅程。

* [Adobe Experience ManagerCloud Service体系结构简介](/help/core-concepts/architecture.md)  — 将AEM理解为Cloud Service
* [AEM无头Tutorials](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html)  — 使用这些实践教程探索如何使用AEM将内容交付到无头端点的各种选项并选择适合您的选项。
* [无外设内容管理使用](https://experienceleague.adobe.com/?Solution=Experience+Manager&amp;Solution=Experience+Manager+Sites&amp;Solution=Experience+Manager+Forms&amp;Solution=Experience+Manager+Screens&amp;launch=ExperienceManager-D-1-2020.1.headless#courses) GraphQL API — 请通过本课程概述在AEM中实现的GraphQL API。需要通过AdobeID进行身份验证。
* [AEM指南WKND - GraphQL](https://github.com/adobe/aem-guides-wknd-graphql)  — 此GitHub项目包括高亮显示AEM GraphQL API的示例应用程序。
* [创作概念](/help/sites-cloud/authoring/getting-started/concepts.md) - AEM创作环境的技术文档，包括有关创作发布设置的详细信息
* [发布页面](/help/sites-cloud/authoring/fundamentals/publishing-pages.md)  — 在AEM上发布内容的技术文档
* [命名约定](/help/implementing/developing/introduction/naming-conventions.md) - AEM中页面命名限制的技术文档
* [多站点管理器和翻译](/help/sites-cloud/administering/msm-and-translation.md)  — 关于AEM强大翻译功能的技术文档
* [AEM工作流](/help/sites-cloud/authoring/workflows/overview.md)  — 关于如何在AEM中自动工作流的技术文档
* [内容片段](/help/assets/content-fragments/content-fragments.md)  — 内容片段的技术文档。
* [内容片段模型](/help/assets/content-fragments/content-fragments-models.md)  — 内容片段模型的技术文档。
* [GraphQL技术文档](https://graphql.org) - GraphQL定义（外部链接）
* [GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md)  — 介绍如何创建访问和交付内容片段请求的技术文档
* [Assets REST API](/help/assets/content-fragments/assets-api-content-fragments.md)  — 介绍如何创建和修改内容片段（和其他资产）的技术文档
* [持久查询](/help/assets/content-fragments/graphql-api-content-fragments.md#persisted-queries-caching) - AEM中持久查询的技术文档
* [AEM中的无头和无头](/help/implementing/developing/headful-headless.md)  — 完整讨论AEM中可用的无头集成级别
