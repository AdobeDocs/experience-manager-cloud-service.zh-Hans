---
title: AEM Sites作为Cloud Service的无外设开发
description: 了解AEM作为Cloud Service的强大无外设功能（如内容模型、内容片段和GraphQL API）如何相互配合，使您能集中管理您的体验并跨渠道提供这些体验。
translation-type: tm+mt
source-git-commit: e7ca6dc841ba777384be74021a27d523d530a956
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 2%

---


# 将AEM Sites作为Cloud Service{#headless-development}的无外设开发

了解AEM作为Cloud Service的强大无外设功能（如内容模型、内容片段和GraphQL API）如何相互配合，使您能集中管理您的体验并跨渠道提供这些体验。

## 概述 {#overview}

无外设实施对于向您的受众提供体验越来越重要，无论体验在何处，也不论渠道。

无外设实施可实现页面和组件管理，就像在完整堆栈和混合解决方案中一样，侧重于创建渠道中立、可重用的内容片段及其跨渠道投放。 它是用于实施Web体验的现代、动态的开发模式。

![AEM实施模型](assets/aem-implementation-models.png)

## 比较头部和无头{#headful-headless}

本文档重点介绍AEM的完全无头实施模型。 不过，在AEM中，“头脑”与“无头”未必是二进制选择。 无外设功能可用于管理内容并将内容交付到各种端点，同时使内容作者能够编辑单页应用程序。 全部在AEM中。

>[!TIP]
>
>有关详细信息，请参阅AEM](/help/implementing/developing/headful-headless.md)中的文档[Headful和Headless。

## AEM作为Cloud Service和Headless {#aem-headless}

AEM作为Cloud Service，通过提供三种强大的服务，为无外设实施模型提供了灵活的工具：

1. 内容模型
   * 内容模型是内容的结构化表示。
   * 这些定义由AEM内容片段模型编辑器中的信息架构师定义。
   * 内容模型用作内容片段的基础。
1. 内容片段
   * 内容片段是内容模型的实例化。
   * 这些内容由内容作者使用AEM内容片段编辑器创建。
   * 它们存储在AEM Assets中，并在资产管理UI中进行管理。
1. 内容API，用于投放
   * AEM GraphQL API支持内容片段投放。
   * AEM Assets REST API支持内容片段CRUD操作。
   * 通过[内容片段核心组件的JSON导出，还可以直接投放内容。](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/components/content-fragment-component.html)

## 无头入门指南{#getting-started}

无外设入门指南为使用AEM作为Cloud Service创建、管理和提供体验的简单路径进行了五步规划。 每本指南都以前面的指南为基础，因此建议按顺序彻底地探索它们。

1. [创建配置](getting-started/create-configuration.md)
1. [创建内容片段模型](getting-started/create-content-model.md)
1. [创建资产文件夹](getting-started/create-assets-folder.md)
1. [创建内容片段](getting-started/create-content-fragment.md)
1. [访问和传送内容片段](getting-started/create-api-request.md)

## 受众 {#audience}

对于AEM无头功能的基本端到端演示，[无头入门指南](#getting-started)中描述的任务是必需的。 任何具有管理员访问测试AEM实例权限的人都可以按照以下指南了解AEM中的无头投放，但具有开发人员经验的人是理想人选。

然而，在生产情况下，任务将由不同角色以不同次数执行。 例如：

* **管** 理员通常只需为内容设置初始配置和文件夹结构一次或偶尔。
* **信息** 架构通常会随着组织的发展需求而添加新模型。
* **内容** 作者将根据架构师定义的模型，持续创建新内容作为内容片段。

《无头入门指南》指出，一般由谁执行描述的任务以及执行频率。

## 下一步 {#next-step}

准备好了解更多信息？ 然后，阅读无头入门指南的第一部分开始：[创建配置。](getting-started/create-configuration.md)
