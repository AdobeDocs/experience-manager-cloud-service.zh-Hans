---
title: Assets as a [!DNL Cloud Service] 简介
description: 了解如何使用和管理 Experience Manager Assets as a Cloud Service。
contentOwner: AK
feature: Asset Management
role: User,Leader,Architect
exl-id: 4437f214-d058-4975-8b8f-869a12c8103b
source-git-commit: d91254b52c257a3758da200a2c74b736ca457884
workflow-type: tm+mt
source-wordcount: '892'
ht-degree: 94%

---


# Assets as a [!DNL Cloud Service] 简介 {#assets-cloud-service-introduction}

<!-- Need review information from gklebus -->

Adobe Experience Manager Assets as a [!DNL Cloud Service] 为企业提供了云原生的 PaaS 解决方案，不仅可用于快速执行其数字资源管理和动态媒体运营来实现影响力，而且还可在始终最新、始终可用和不断学习的系统中使用新一代智能功能，例如 AI/ML。

并行摄取多个资源或复杂资源是一项面向 Experience Manager Author 实例的资源密集型任务。在添加、处理甚至迁移资源时，主实例会占用大量 CPU、内存和 I/O 资源。此类性能问题会影响最终用户的创作和浏览体验。

企业需要为面向多设备、跨地域和多语言用例的一系列广泛的文件格式和内容解决方案提供支持。根据资源处理和存储要求，所需的资源和功能可能会导致传统解决方案的负担过重。有时，资源处理方面的技术限制会导致无法产生预期结果；在其他时候，存储成本会缩小利润空间。

首先，了解[云原生服务的好处](#solution-benefits)。查看[对 Experience Manager as a [!DNL Cloud Service]](/help/release-notes/aem-cloud-changes.md) 所做的显著更改，这些更改将在[对 Assets 进行显著更改](/help/assets/assets-cloud-changes.md)后影响 Experience Manager Assets。

继续阅读以了解[新 Assets 功能的详细信息](#whats-new-assets)和[已知问题](/help/release-notes/maintenance/latest.md)。查看[弃用或删除的功能](/help/release-notes/deprecated-removed-features.md)的列表以了解此版本中删除的功能。最后，通过此[词汇表](/help/overview/terminology.md)了解 Experience Manager 术语。

## 解决方案好处 {#solution-benefits}

以下是 Assets as a [!DNL Cloud Service] 的主要好处。要了解详细信息，请参阅 [Experience Manager as a [!DNL Cloud Service]](/help/overview/introduction.md) 概述。

* **用于资源处理的现代云服务**：新的资源微服务是一项基于云、可扩展、可靠、无忧的资源处理服务。
* **高度可扩展**：跨所有类型的部署的有弹性的可扩展性。在需要时按需提供的几乎无限的资源。与传统系统相比，节省了过度设计的成本。
* **最新软件**：始终最新且始终进行更新。所有用户都只能获得最新软件，其中包含他们可使用的所有补丁、功能、安全修复和错误修复。开发人员和集成商使用一组最新的 API，没有多版本支持问题。
* **始终在线**：零停机时间 (0dt)，这得益于部署在具有备份和冗余的群集中的实例。升级也可以实现 0dt。
* **持续监控**：系统监控是自动实施的，内置检查和触发器可帮助保持性能、可用性和整体可靠性。
* **无忧部署**：云中的 Experience Manager 操作是完全自动执行的，无需手动干预。对于自动化部署，Cloud Manager (CM) 组件将使构建包含自定义代码的可部署 Docker 图像的过程的自动化。

## 可用的基于角色的体验 {#persona-based-experiences}

Adobe 为您提供强大的数字资源管理（DAM）解决方案，让您能够充分利用数字资源。 Adobe Experience Manager Assets 具有两种使用相同 Cloud Service 存储库的独立体验：

* **管理视图**：现有资源作为 Cloud Service 用户界面。使用管理视图实现所有高级资源管理功能，包括集成、工作流程、内容自动化、发布等。

* **资源视图**：Adobe 的轻量级资源管理体验，用于存储、管理、发现和使用数字资源。简化的用户界面包含基本的资源管理功能。专为轻量级 DAM 用户设计，专注于上传、元数据管理、搜索、下载和共享。

有权访问管理视图的用户也可以访问资源视图。资源视图提供简化的用户界面，使您可以轻松管理、探索和分发数字资源。 来自不同职能部门（包括创意团队、营销团队和业务线团队）的广泛用户可以就资源进行协作，并在需要时随时随地访问正确的、经批准的资源。许多临时 DAM 用户更喜欢资源视图，因为它只包含一部分功能。该体验面向创意人员、只读资源消费者和轻量级 DAM 用户。

DAM 库管理员、开发人员和超级用户可以继续使用管理视图，或根据需要在这些用户界面之间切换。您可以选择最适合您角色的体验。

![添加标记](assets/newui-overview.svg)

有关如何访问资源视图及其通过“管理”视图提供的一些简化功能的信息，请参阅[资源视图简介。](/help/assets/assets-view-introduction.md)

## 与Edge Delivery Services的基于文档的创作集成 {#integrate-doc-authoring-edge-and-assets}

Edge Delivery 使您可快速创建吸引人的网站，作者从中可快速地更新和发布内容，并可快速地推出新网站。

将AEM Assets与基于文档的创作集成，以便Edge Delivery Services在Microsoft Word或Google文档中创作文档时，能够使用在AEM Assets存储库中可用的图像。 有关更多信息，请参阅 [将AEM Assets与基于文档的创作集成](/help/edge/using.md#integrate-assets-edge).

## 与 Adobe Journey Optimizer 集成 {#integration-with-ajo}

[Adobe Journey Optimizer](https://business.adobe.com/products/journey-optimizer/adobe-journey-optimizer.html) 简化了客户的历程管理，利用智能决策和见解为客户提供全渠道营销活动。在使用 Journey Optimizer 设计消息时，您可以直接从 Journey Optimizer 界面中访问 Assets as a Cloud Service 存储库。用户可以使用 Experience Manager Assets 的嵌入式用户界面访问资源。有关更多信息，请参阅[使用 Experience Manager Assets 创建和管理资源](https://experienceleague.adobe.com/docs/journey-optimizer/using/content-management/assets-images/assets.html)。

## 新 Assets 功能 {#whats-new-assets}

重要的新功能包括：

* [资源微服务](/help/assets/asset-microservices-overview.md)
* [资源上传方式](/help/assets/add-assets.md)

**另请参阅**

* [翻译资源](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [资源支持的文件格式](file-format-support.md)
* [搜索资源](search-assets.md)
* [连接的资源](use-assets-across-connected-assets-instances.md)
* [资源报告](asset-reports.md)
* [元数据架构](metadata-schemas.md)
* [下载资源](download-assets-from-aem.md)
* [管理元数据](manage-metadata.md)
* [搜索 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [批量元数据导入](metadata-import-export.md)
