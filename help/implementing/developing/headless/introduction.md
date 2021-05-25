---
title: AEM Sites作为Cloud Service的无头开发
description: 了解AEM作为Cloud Service强大的无头功能（如内容模型、内容片段和GraphQL API）如何协同工作，从而让您能够集中管理您的体验并跨渠道提供它们。
exl-id: 24300499-ae9c-49d0-aa25-f51e14d9cf79
source-git-commit: 816c08b9351b3ce2fd4f31974d707e9d4a4eea27
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 4%

---


# AEM Sites as aCloud Service的无头开发{#headless-development}

了解AEM作为Cloud Service强大的无头功能（如内容模型、内容片段和GraphQL API）如何协同工作，从而让您能够集中管理您的体验并跨渠道提供它们。

## 概述 {#overview}

无头实施对于向受众提供体验越来越重要，无论这些体验位于何处，也不论渠道如何。

与传统的全栈和混合解决方案一样，无头实施可用于页面和组件管理，并着重于创建渠道中性、可重复使用的内容片段及其跨渠道交付。 它是一种用于实施Web体验的现代化、动态开发模式。

![AEM实施模型](assets/aem-implementation-models.png)

## 比较Headful和Headless {#headful-headless}

本文档重点介绍AEM的完整无头实施模型。 但是，在AEM中，“头部”与“无头”不必是二进制选择。 无标题功能可用于管理和将内容交付到各种端点，同时还允许内容作者编辑单页应用程序。 全部在AEM中。

>[!TIP]
>
>有关更多信息，请参阅AEM](/help/implementing/developing/headful-headless.md)中的文档[Headful和Headless。

## AEM as a Cloud Service和Headless {#aem-headless}

AEM as a Cloud Service通过提供三项功能强大的服务，为无头实施模型提供了灵活的工具：

1. 内容模型
   * 内容模型是内容的结构化表示形式。
   * 这些量度由AEM内容片段模型编辑器中的信息架构师定义。
   * 内容模型用作内容片段的基础。
1. 内容片段
   * 内容片段是内容模型的实例化。
   * 这些内容由内容作者使用AEM内容片段编辑器创建。
   * 它们存储在AEM Assets中，并在资产管理UI中进行管理。
1. 用于交付的内容API
   * AEM GraphQL API支持内容片段交付。
   * AEM Assets REST API支持内容片段CRUD操作。
   * 通过[内容片段核心组件的JSON导出，也可以直接交付内容。](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/components/content-fragment-component.html)

## 使用AEM Headless {#first-steps}的首要步骤

您可以使用许多资源来开始使用AEM无头功能。 这些功能适用于不同的用例，但都可以充分概述AEM的无头功能。

| 资源 | 描述 | 类型 | 受众 | 是。 时间 |
|---|---|---|---|---|
| [无头开发人员历程](/help/journey-headless/developer/overview.md) | 要全面了解从无头理论到使用您的第一个无头项目的AEM无头功能，请从此处开始。 | 指南 | 开发人员 | 1小时 |
| [Headless快速入门指南](/help/implementing/developing/headless/getting-started/introduction.md) | 有关AEM主要无头功能的简短摘要，请参阅此快速入门概述。 | 快速入门 | 开发人员、管理员 | 20分钟 |
| [AEM Headless动手操作入门教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html) | 如果您喜欢实用方法，本教程将直接深入探讨如何创建一个简单的无头项目。 | 教程 | 开发人员 | 2小时 |
