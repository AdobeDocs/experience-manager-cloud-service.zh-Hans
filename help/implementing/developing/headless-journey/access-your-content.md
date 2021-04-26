---
title: 如何通过AEM 投放 API访问您的内容
description: 在AEM无外设开发人员历程的这一部分中，了解如何使用GraphQL查询访问您的内容片段内容。
hide: true
hidefromtoc: true
index: false
translation-type: tm+mt
source-git-commit: 9fb18dbe60121f46dba1e11d4133e5264a6d538d
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 2%

---


# 如何通过AEM 投放 API {#access-your-content}访问您的内容

>[!CAUTION]
>
>正在进行中的工作 — 此文档的创建正在进行中，不应理解为完整或明确，也不应将其用于生产目的。

在[AEM无外设开发人员历程的这一部分中，](overview.md)了解如何使用GraphQL查询访问内容片段的内容。

## 迄今为止的故事{#story-so-far}

在AEM无头旅程的上一个文档中，[如何对您的内容建模](model-your-content.md)您学习了AEM中数据建模的基础知识，现在您应该：

* 了解设计内容时的重要规划注意事项。
* 了解根据您的集成级别要求实施无外设的步骤。
* 设置必要的工具和AEM配置。
* 了解最佳实践，让您的无头旅程变得顺畅、保持内容生成高效并确保内容快速交付。

本文以这些基础为基础，因此您了解如何通过API在AEM中访问现有无外设内容。

* **受众**:初学者
* **目标**:了解如何使用AEM GraphQL查询访问内容片段的内容：
   * 介绍GraphQL。
   * 介绍AEM GraphQL API。
   * 深入了解AEM GraphQL API的详细信息。
   * 查看一些示例查询，了解实际操作情况。

以Adobe Experience Manager(AEM)为Cloud Service，您可以将内容片段与AEM GraphQL API结合使用，无头地交付结构化内容以用于您的应用程序。 自定义单个API查询的功能允许您检索和提供您想要/需要渲染的特定内容(作为对单个API查询的响应)。

>[!NOTE]
>AEM GraphQL API是基于标准GraphQL的自定义实施。

## GraphQL — 简介{#graphql-introduction}

GraphQL是：

* &quot;*...用于API的查询语言和用于使用现有数据实现这些查询的运行时。*&quot;。

   请参阅&#x200B;*GraphQL*。

### GraphQL — 类型{#graphql-types}

### GraphQL -模式{#graphql-schemas}

### GraphQL -查询{#graphql-queries}

## AEM和GraphQL {#aem-graphql}

GraphQL用于AEM中的不同位置：

* 商务
   * 占位符
* 内容片段
   * 为此用例开发了自定义API。
   * 这是AEM GraphQL API。

## AEM GraphQL API {#aem-graphql-api}

对于Adobe Experience a Cloud Experience，已开发标准GraphQL API的自定义实施。

AEM GraphQL API允许您对内容片段执行（复杂）查询;每个查询都根据特定的模型类型。 返回的内容随后可供应用程序使用。

>[!NOTE]
>
>AEM GraphQL API实现基于GraphQL Java库。

### AEM GraphQL API和内容片段{#aem-graphql-content-fragments}

## 用于AEM GraphQL API {#content-fragments-use-with-aem-graphql-api}的内容片段

内容片段可用作AEM查询的GraphQL的基础，如下所示：

* 它们使您能够设计、创建、管理和发布独立于页面的内容。
* 内容片段模型通过定义的数据类型提供所需的结构。
* 定义模型时可用的片段引用可用于定义其他结构层。

### 内容片段 {#content-fragments}

内容片段:

* 包含结构化内容。

* 它们基于内容片段模型，该模型预定义生成片段的结构。

### 内容片段模型 {#content-fragments-models}

以下内容片段模型：

* 用于生成模式，只需&#x200B;**Enabled**&#x200B;一次。

* 提供GraphQL所需的数据类型和字段。 它们确保您的应用程序仅请求可能的内容，并接收预期内容。

* 数据类型&#x200B;**片段引用**&#x200B;可在模型中用于引用其他内容片段，因此引入其他结构级别。

### 片段引用{#fragment-references}

**片段引用**:

* 与GraphQL结合使用时特别感兴趣。

* 是在定义内容片段模型时可以使用的特定数据类型。

* 引用另一个片段，具体取决于特定的内容片段模型。

* 允许您检索结构化数据。

   * 当定义为&#x200B;**multifeed**&#x200B;时，主片段可以引用（检索）多个子片段。

### JSON预览{#json-preview}

要帮助设计和开发内容片段模型，您可以预览[JSON输出](/help/assets/content-fragments/content-fragments-json-preview.md)。

## 下一步是什么{#whats-next}

[了解如何使用REST API访问和更新内容片段的内容](/help/implementing/developing/headless-journey/update-your-content.md)。

## 其他资源 {#additional-resources}

* [AEM无头入门](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html)  — 一个简短的视频教程系列概述了如何使用AEM无头功能，包括数据建模和GraphQL
* [GraphQL.org](https://graphql.org)
   * [架构](https://graphql.org/learn/schema/)
   * [GraphQL Java库](https://graphql.org/code/#java)
* [AEM GraphQL API，与内容片段一起使用](/help/assets/content-fragments/graphql-api-content-fragments.md)
   * [了解如何将GraphQL与AEM结合使用 — 示例内容和查询](/help/assets/content-fragments/content-fragments-graphql-samples.md)
   * [内容片段上的远程AEM GraphQL查询身份验证](/help/assets/content-fragments/graphql-authentication-content-fragments.md)
* [使用内容片段](/help/assets/content-fragments/content-fragments.md)
   * [内容片段模型](/help/assets/content-fragments/content-fragments-models.md)
   * [JSON输出](/help/assets/content-fragments/content-fragments-json-preview.md)
