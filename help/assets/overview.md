---
title: Assets as a Cloud Service 简介
description: 资产作为Cloud Service的新增功能。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 26833f59f21efa4de33969b7ae2e782fe5db8a14
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 3%

---


# Assets as a Cloud Service 简介 {#assets-cloud-service-introduction}

<!-- Need review information from gklebus -->

Adobe Experience Manager资产作为Cloud Service优惠，为企业提供云本地的PaaS解决方案，不仅可以快速、有效地执行数字资产管理和动态媒体操作，还可以在始终处于最新状态、始终可用且始终处于学习状态的系统中使用下一代智能功能，如AI/ML。

对于AEM作者实例，并发获取许多资产或复杂资产是资源密集型任务。 在添加、处理甚至迁移资产时，主实例会消耗大量CPU、内存和I/O资源。 这类性能问题会影响最终用户的创作和浏览体验。

对于多设备、跨地理位置和多语言用例，企业需要支持各种文件格式和内容分辨率。 资产处理和存储要求需要资源和功能，这些资源和功能可能会使传统解决方案不堪重负。 有时，资产处理的技术限制无法产生期望的结果，有时存储成本会阻碍利润率。

首先，了解云本机产品](#solution-benefits)的[优势。 查看对AEM的显着[更改(作为Cloud Service](/help/release-notes/aem-cloud-changes.md))，这也会影响Experience Manager资产，随后对资产](/help/assets/assets-cloud-changes.md)的显着[更改。

阅读以了解新资产功能的[详细信息](#whats-new-assets)和[已知问题](/help/release-notes/known-issues.md)。 查看[已弃用或已删除功能](/help/release-notes/deprecated-removed-features.md)的列表，了解此版本中已删除的内容，并查看即将推出的功能[的列表，了解即将推出的功能。 ](/help/release-notes/known-issues.md#upcoming-assets-capabilities)最后，借助此[术语表](/help/overview/terminology.md)了解AEM术语。

## 解决方案优势{#solution-benefits}

以下是资产作为Cloud Service的主要优势。 要了解更多信息，请参阅[Experience ManagerCloud Service概述](/help/overview/introduction.md)。

* **用于资产处理的现代Cloud Service**:新的资产微服务是一种基于云、可扩展、可靠且无忧的资产处理服务。
* **高度可扩展**:跨所有类型的部署实现灵活的可扩展性。按需提供的几乎无限资源。 与传统系统相比，节省了过度设计的成本。
* **最新软件**:始终处于最新状态并始终更新。所有用户只有最新软件，并有所有修补程序、功能、安全性和错误修复可供他们使用。 开发人员和集成商可使用最新的API集，无多版本支持问题。
* **始终在线**:零停机时间(0dt)，这要归功于在具有备份和冗余的群集中部署的实例。升级也为0dt。
* **持续监视**:系统的监控是自动的和内置的检查和触发器，有助于保持性能、可用性和总体鲁棒性。
* **轻松部署**:云操作中的AEM完全自动化，无需手动干预。对于自动部署，云管理器(CM)组件可自动构建包含自定义代码的可部署Docker图像。

## 新资产功能{#whats-new-assets}

重要的新功能包括：

* [资产微服务](/help/assets/asset-microservices-overview.md)
* [资产上传方法](/help/assets/add-assets.md)
