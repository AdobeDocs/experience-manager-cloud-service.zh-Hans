---
title: Assets as a [!DNL Cloud Service] 简介
description: Assets as a [!DNL Cloud Service] 中的新增功能。
contentOwner: AG
feature: Asset Management
role: User,Leader,Architect
exl-id: 4437f214-d058-4975-8b8f-869a12c8103b
source-git-commit: d0deca8acbf6049d5be6c27275eedf9b52b27658
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 68%

---

# Assets as a [!DNL Cloud Service] 简介 {#assets-cloud-service-introduction}

<!-- Need review information from gklebus -->

Adobe Experience Manager Assets as a [!DNL Cloud Service] 为企业提供了云原生的 PaaS 解决方案，不仅可用于快速执行其数字资源管理和动态媒体运营来实现影响力，而且还可在始终最新、始终可用和不断学习的系统中使用新一代智能功能，例如 AI/ML。

并行摄取多个资源或复杂资源是一项面向 Experience Manager Author 实例的资源密集型任务。在添加、处理甚至迁移资源时，主实例会占用大量 CPU、内存和 I/O 资源。此类性能问题会影响最终用户的创作和浏览体验。

企业需要为面向多设备、跨地域和多语言用例的一系列广泛的文件格式和内容解决方案提供支持。根据资源处理和存储要求，所需的资源和功能可能会导致传统解决方案的负担过重。有时，资源处理方面的技术限制会导致无法产生预期结果；在其他时候，存储成本会缩小利润空间。

首先，了解[云原生服务的好处](#solution-benefits)。查看[对 Experience Manager as a [!DNL Cloud Service]](/help/release-notes/aem-cloud-changes.md) 所做的显著更改，这些更改将在[对 Assets 进行显著更改](/help/assets/assets-cloud-changes.md)后影响 Experience Manager Assets。

继续阅读以了解[新 Assets 功能的详细信息](#whats-new-assets)和[已知问题](/help/release-notes/maintenance/latest.md)。查看[弃用或删除的功能](/help/release-notes/deprecated-removed-features.md)的列表以了解此版本中删除的功能。最后，通过此[词汇表](/help/overview/terminology.md)了解 Experience Manager 术语。

## 解决方案好处 {#solution-benefits}

以下是 Assets as a [!DNL Cloud Service] 的主要好处。要了解详情，请参阅 [Experience Manager as a [!DNL Cloud Service]](/help/overview/introduction.md) 概述。

* **用于资源处理的现代云服务**：新的资源微服务是一项基于云、可扩展、可靠、无忧的资源处理服务。
* **高度可扩展**：跨所有类型的部署的有弹性的可扩展性。在需要时按需提供的几乎无限的资源。与传统系统相比，节省了过度设计的成本。
* **最新软件**：始终最新且始终进行更新。所有用户都只能获得最新软件，其中包含他们可使用的所有补丁、功能、安全修复和错误修复。开发人员和集成商使用一组最新的 API，没有多版本支持问题。
* **始终在线**：零停机时间 (0dt)，这得益于部署在具有备份和冗余的群集中的实例。升级也可以实现 0dt。
* **持续监控**：系统监控是自动实施的，内置检查和触发器可帮助保持性能、可用性和整体可靠性。
* **无忧部署**：云中的 Experience Manager 操作是完全自动执行的，无需手动干预。对于自动化部署，Cloud Manager (CM) 组件将使构建包含自定义代码的可部署 Docker 图像的过程的自动化。

## 可用的基于角色的体验 {#persona-based-experiences}

Adobe 为您提供强大的数字资产管理（DAM）解决方案，让您能够充分利用数字资产。 Adobe Experience Manager Assets具有两个使用同一Cloud Services存储库的独立体验：

* **管理员视图**：现有的Assetsas a Cloud Service用户界面。 使用“管理员视图”可获得所有高级资产管理功能，包括集成、工作流、内容自动化、发布等。

* **资产视图**：Adobe的轻量级资源管理体验，可用于存储、管理、发现和使用数字资源。 简化的用户界面，包含基本资产管理功能。 专为轻量级DAM用户设计，重点关注上传、元数据管理、搜索、下载和共享。

有权访问“管理员”视图的用户还可以访问“资产”视图。 Assets视图提供了简化的用户界面，让您能够轻松管理、发现和分发数字资产。 来自不同职能部门（包括创意人员、营销和业务线团队）的广泛用户可就资产进行协作，并在需要时随时随地访问正确的、经过批准的资产。 许多临时DAM用户更喜欢资产视图，因为它只包含功能的子集。 该体验面向创意人员、只读资产使用者和较轻的DAM用户。

DAM库管理员、开发人员和超级用户可以根据需要继续使用管理员视图或在用户界面之间切换。 您可以选择最适合您的角色的体验。

![添加标记](assets/newui-overview.svg)

有关如何通过“管理员”视图访问“资产”视图及其提供的一些简化情况的信息，请参阅 [“资产”视图简介](/help/assets/assets-view-introduction.md).

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
