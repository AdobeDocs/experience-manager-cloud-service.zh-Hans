---
title: AEM Headless简介
description: Adobe Experience Manager(AEM)无外设自助资源和文档链接。 了解如何使用内容模型、内容片段和GraphQL API等功能为AEM提供无头体验。
landing-page-description: 了解如何使用和管理Experience Manager无头as a Cloud Service。
exl-id: 24300499-ae9c-49d0-aa25-f51e14d9cf79
source-git-commit: c5d67e0ece40cdf7a9009436ec90305fe81425a2
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 2%

---


# Adobe Experience Manager Headless简介  {#introduction-aem-headless}

了解如何使用Adobe Experience Manager(AEM)的功能（如内容模型、内容片段和GraphQL API）来大规模提供无头体验。

## 概述 {#overview}

AEM Headless是一种来自Experience Manager的CMS解决方案，它允许AEM中的结构化内容（内容片段）由任何应用程序通过HTTP使用GraphQL来使用。 无外设实施可大规模跨平台和渠道交付体验。

与传统的全栈和混合解决方案一样，无头实施可用于页面和组件管理，并着重于创建渠道中性、可重复使用的内容片段及其跨渠道交付。 它是一种用于实施Web体验的现代化、动态开发模式。

![AEM实施模型](assets/aem-implementation-models.png)

## AEM Headless的功能 {#aem-headless-features}

AEM as a Cloud Service提供三项强大功能，是用于无头实施模型的灵活工具：

1. **内容模型**
   * 内容模型是内容的结构化表示形式。
   * 内容模型由AEM内容片段模型编辑器中的信息架构师定义。
   * 内容模型用作内容片段的基础。
1. **内容片段**
   * 内容片段是基于内容模型创建的。
   * 由内容作者使用AEM内容片段编辑器创建。
   * 内容片段存储在AEM Assets中，并在资产管理UI中进行管理。
1. **用于交付的内容API**
   * AEM GraphQL API支持内容片段交付。
   * AEM Assets REST API支持内容片段CRUD操作。
   * 此外，还可以通过 [内容片段核心组件的JSON导出](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html).

## 使用AEM Headless实现首要步骤 {#first-steps}

有多种资源可用于开始使用AEM无头功能。 每个指南都针对不同的用例和受众量身定制。

| 资源 | 描述 | 类型 | 受众 | 是。 时间 |
|---|---|---|---|---|
| [Headless 开发人员历程](/help/journey-headless/developer/overview.md) | **对于不熟悉AEM和Headless的开发人员** 技术，请从此处全面介绍AEM及其无头功能（从无头理论到使用您的第一个无头项目）。 | 指南 | 开发人员 **新增了AEM和headless** | 1小时 |
| [无头设置](/help/headless/setup/introduction.md) | **对于经验丰富的AEM用户** 需要简要概述AEM的主要无头功能的用户，请查看此快速入门概述。 | 引用设置 | 开发人员、管理员 **使用AEM体验** | 20分钟 |
| [无头动手教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html) | **如果您喜欢实际操作方法并熟悉AEM**，本教程将直接介绍如何实施一个简单的无头应用程序。 | 教程 | 开发人员 | 2小时 |
| [无外设架构师历程](/help/journey-headless/architect/overview.md) | **适用于刚接触AEM和无头的架构师** 技术，请单击此处开始介绍Adobe Experience Manager as a Cloud Service强大、灵活、无头的功能，以及如何为您的项目建立内容模型。 | 指南 | 架构师 | 1小时 |
| [无外设创作历程](/help/journey-headless/author/overview.md) | **对于初次使用AEM和Headless的企业用户** 技术，请单击此处开始介绍Adobe Experience Manager as a Cloud Service强大、灵活、无头的功能，以及如何为您的项目建立内容模型。 | 指南 | 内容创建者 | 1小时 |
| [Headless 翻译历程](/help/journey-headless/translation/overview.md) | 对于那些 **对使用AEM翻译方法到headless感兴趣**. 了解无头技术以及如何在AEM中创建和更新从A到Z的翻译项目。 | 指南 | 翻译专家 | 1小时 |

## 比较头部和无头部 {#headful-headless}

本指南重点介绍AEM的完全无头实施模型。 但是，在AEM中，“头部”与“无头”不必是二进制选择。 无标题功能可用于管理和将内容交付到多个接触点，同时使内容作者能够编辑单页应用程序。 全部在AEM中。

>[!TIP]
>
>查看文档 [AEM中的Headful和Headless](/help/implementing/developing/headful-headless.md) 以了解更多信息。