---
title: 资产a [!DNL Cloud Service]简介
description: 资产中的新增功能： [!DNL Cloud Service]。
contentOwner: AG
feature: 资产管理
role: User,Leader,Architect
exl-id: 4437f214-d058-4975-8b8f-869a12c8103b
source-git-commit: 4be76f19c27aeab84de388106a440434a99a738c
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---

# [!DNL Cloud Service]资产简介 {#assets-cloud-service-introduction}

<!-- Need review information from gklebus -->

Adobe Experience Manager Assets as a [!DNL Cloud Service]为企业提供了云原生的PaaS解决方案，不仅可以快速高效地执行数字资产管理和Dynamic Media操作，还可以在始终保持最新、始终可用且始终学习的系统中使用下一代智能功能，如AI/ML。

对于Experience Manager创作实例，并发摄取多个资产或复杂资产是资源密集型任务。 在添加、处理或迁移资产时，主实例会消耗大量CPU、内存和I/O资源。 此类性能问题会影响最终用户的创作和浏览体验。

对于多设备、跨地理位置和多语言用例，企业需要支持多种文件格式以及内容分辨率。 资产处理和存储需求需要资源和功能，这些资源和功能可能会使传统解决方案负担过重。 有时，资产处理的技术限制不会产生期望的结果，有时存储成本会阻碍利润率。

首先，了解云原生产品](#solution-benefits)的优势。 [查看对Experience Managera [!DNL Cloud Service]](/help/release-notes/aem-cloud-changes.md)的显着[更改，这也会影响Experience Manager资产，接下来是对资产](/help/assets/assets-cloud-changes.md)的显着[更改。

请阅读并了解新Assets功能](#whats-new-assets)和[已知问题](/help/release-notes/known-issues.md)的详细信息。 [请参阅[已弃用或已移除的功能列表](/help/release-notes/deprecated-removed-features.md) ，了解此版本中将删除的内容，并查看此[即将推出的功能列表](/help/release-notes/known-issues.md#upcoming-assets-capabilities) ，了解即将推出的功能。 最后，借助此[术语表](/help/overview/terminology.md)，了解Experience Manager术语。

## 解决方案的优势 {#solution-benefits}

以下是[!DNL Cloud Service]资产的主要优势。 要了解更多信息，请参阅[Experience Manager概述a [!DNL Cloud Service]](/help/overview/introduction.md)。

* **用于资产处理的现代云服务**:新的资产微服务是一项基于云、可扩展、可靠且无忧无虑的资产处理服务。
* **高度可扩展**:跨所有类型部署的弹性可扩展性。按需提供的资源几乎是无限的。 与传统系统相比，节省了过度设计的成本。
* **最新软件**:始终为最新且始终更新。所有用户都只拥有最新的软件，且其中包含可供他们使用的所有修补程序、功能、安全性和错误修复。 开发人员和集成商可以使用最新的API集，而无需出现多版本支持问题。
* **始终在线**:零停机时间(0dt)，这要归功于在具有备份和冗余的群集中部署的实例。升级也为0dt。
* **持续监控**:系统的监控是自动的、内置的检查和触发器，有助于保持性能、可用性和总体稳健性。
* **轻松部署**:云操作中的Experience Manager是完全自动的，无需手动干预。对于自动部署，Cloud Manager(CM)组件会自动生成包含您的自定义代码的可部署Docker图像。

## 新资产功能 {#whats-new-assets}

重要的新功能包括：

* [资产微服务](/help/assets/asset-microservices-overview.md)
* [资产上传方法](/help/assets/add-assets.md)
