---
title: Assets as a [!DNL Cloud Service] 简介
description: Assets as a [!DNL Cloud Service] 中的新增功能。
contentOwner: AG
feature: Asset Management
role: User,Leader,Architect
exl-id: 4437f214-d058-4975-8b8f-869a12c8103b
source-git-commit: efc0f317cf4540db49b6caf7bb9f6fd31b311583
workflow-type: ht
source-wordcount: '457'
ht-degree: 100%

---

# Assets as a [!DNL Cloud Service] 简介 {#assets-cloud-service-introduction}

<!-- Need review information from gklebus -->

Adobe Experience Manager Assets as a [!DNL Cloud Service] 为企业提供了云原生的 PaaS 解决方案，不仅可用于快速执行其数字资产管理和动态媒体运营来实现影响力，而且还可在始终最新、始终可用和不断学习的系统中使用新一代智能功能，例如 AI/ML。

并行摄取多个资产或复杂资产是一项面向 Experience Manager Author 实例的资源密集型任务。在添加、处理甚至迁移资产时，主实例会占用大量 CPU、内存和 I/O 资源。此类性能问题会影响最终用户的创作和浏览体验。

企业需要为面向多设备、跨地域和多语言用例的一系列广泛的文件格式和内容解决方案提供支持。根据资源处理和存储要求，所需的资源和功能可能会导致传统解决方案的负担过重。有时，资源处理方面的技术限制会导致无法产生预期结果；在其他时候，存储成本会缩小利润空间。

首先，了解[云原生服务的好处](#solution-benefits)。查看[对 Experience Manager as a [!DNL Cloud Service]](/help/release-notes/aem-cloud-changes.md) 所做的显著更改，这些更改将在[对 Assets 进行显著更改](/help/assets/assets-cloud-changes.md)后影响 Experience Manager Assets。

继续阅读以了解[新 Assets 功能的详细信息](#whats-new-assets)和[已知问题](/help/release-notes/maintenance/latest.md)。查看[弃用或删除的功能](/help/release-notes/deprecated-removed-features.md)的列表以了解此版本中删除的功能。最后，通过此[词汇表](/help/overview/terminology.md)了解 Experience Manager 术语。

## 解决方案好处 {#solution-benefits}

以下是 Assets as a [!DNL Cloud Service] 的主要好处。要了解详情，请参阅 [Experience Manager as a [!DNL Cloud Service]](/help/overview/introduction.md) 概述。

* **用于资产处理的现代云服务**：新的资产微服务是一项基于云、可扩展、可靠、无忧的资产处理服务。
* **高度可扩展**：跨所有类型的部署的有弹性的可扩展性。在需要时按需提供的几乎无限的资源。与传统系统相比，节省了过度设计的成本。
* **最新软件**：始终最新且始终进行更新。所有用户都只能获得最新软件，其中包含他们可使用的所有补丁、功能、安全修复和错误修复。开发人员和集成商使用一组最新的 API，没有多版本支持问题。
* **始终在线**：零停机时间 (0dt)，这得益于部署在具有备份和冗余的群集中的实例。升级也可以实现 0dt。
* **持续监控**：系统监控是自动实施的，内置检查和触发器可帮助保持性能、可用性和整体可靠性。
* **无忧部署**：云中的 Experience Manager 操作是完全自动执行的，无需手动干预。对于自动化部署，Cloud Manager (CM) 组件将使构建包含自定义代码的可部署 Docker 图像的过程的自动化。

## 新 Assets 功能 {#whats-new-assets}

重要的新功能包括：

* [资产微服务](/help/assets/asset-microservices-overview.md)
* [资产上传方式](/help/assets/add-assets.md)
