---
title: AEM Sites作为Cloud Service的无头发展
description: 借助内容模型、内容片段和GraphQL API等强大功能，AEM作为Cloud Service，您可以集中管理体验并跨渠道提供这些体验。
translation-type: tm+mt
source-git-commit: e1db93e8f4cf8ef881b274879e800c9993753a66
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 2%

---


# AEM Sites作为Cloud Service的无头发展{#headless-development}

借助内容模型、内容片段和GraphQL API等强大功能，AEM作为Cloud Service，您可以集中管理体验并跨渠道提供这些体验。

## 概述 {#overview}

无头实施对于向受众提供体验越来越重要，无论体验在何处，也不管渠道。

无头实施与完全堆栈和混合解决方案中的传统方式一样，用于页面和组件管理，并侧重于创建渠道中性、可重用的内容片段及其跨渠道投放。 它是用于实现Web体验的现代、动态的开发模式。

![AEM实施模型](assets/aem-implementation-models.png)

## 比较头部和无头部{#headful-headless}

本文档重点介绍AEM的完全无头实施模型。 然而，在AEM中，头脑强大与头脑无需成为二元选择。 无头功能可用于管理内容并将内容交付到各种端点，同时使内容作者能够编辑单页应用程序。 都在AEM。

>[!TIP]
>
>有关详细信息，请参阅AEM](/help/implementing/developing/headful-headless.md)中的文档[头和头。

## AEM作为Cloud Service和无头{#aem-headless}

AEM作为Cloud Service提供三种强大的服务，是实现无头实施模型的灵活工具：

1. 内容模型
   * 内容模型是内容的结构化表示。
   * 这些信息由AEM内容片段模型编辑器中的信息架构师定义。
   * 内容模型用作内容片段的基础。
1. 内容片段
   * 内容片段是内容模型的实例化。
   * 这些内容作者使用AEM内容片段编辑器创建。
   * 它们存储在AEM Assets，并在资产管理员UI中进行管理。
1. 内容API用于投放
   * AEM GraphQL API支持内容片段投放。
   * AEM AssetsREST API支持内容片段CRUD操作。
   * 通过[内容片段核心组件的JSON导出，还可以直接投放内容。](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/components/content-fragment-component.html)

## 无头入门指南{#getting-started}

无头入门指南为使用AEM作为Cloud Service创建、管理和提供体验提供了简单的途径，只需五个步骤。 每本指南都以前的指南为基础，因此建议按顺序彻底地探索它们。

1. [创建配置](getting-started/create-configuration.md)
1. [创建内容片段模型](getting-started/create-content-model.md)
1. [创建资产文件夹](getting-started/create-assets-folder.md)
1. [创建内容片段](getting-started/create-content-fragment.md)
1. [访问和交付内容片段](getting-started/create-api-request.md)

## 受众 {#audience}

[无头入门指南](#getting-started)中描述的任务对于AEM无头功能的基本端到端演示是必需的。 对测试AEM实例具有管理员访问权限的任何人都可以按照这些指南来了解AEM中的无头投放，但具有开发人员经验的人是理想人选。

但是，在生产情况下，任务将由不同角色以不同次数进行。 例如：

* **管** 理员通常只需为内容设置初始配置和文件夹结构一次或偶尔。
* **信息** 架构通常会随着组织的发展而添加新模型。
* **内容** 作者将根据架构师定义的模型，持续创建新内容作为内容片段。

《无头入门指南》指出，一般由谁执行描述的任务以及执行频率。

## 下一步 {#next-step}

准备好了解更多信息？ 然后，阅读无头入门指南的第一部分，开始学习：[创建配置。](getting-started/create-configuration.md)
