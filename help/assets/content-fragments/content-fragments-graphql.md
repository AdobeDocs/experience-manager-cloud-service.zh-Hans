---
title: 通过GraphQL使用内容片段交付无头内容
description: 了解使用GraphQL中的内容片段实现AEM无头CMS以进行无头内容交付的基本概念。
feature: Content Fragments, GraphQL API
topic: Headless
role: User
exl-id: 4a3b030d-ed59-4920-bf94-e00a45f85b51
source-git-commit: 4e64683598ced4b9811e957082932971f0ec0bb1
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 13%

---

# 通过GraphQL使用内容片段交付无头内容 {#headless-content-delivery-using-content-fragments-with-graphQL}

借助内容片段和GraphQL API，您可以将Adobe Experience Manager(AEM)as a Cloud Service用作无头内容管理系统(CMS)。

这是通过使用内容片段和AEM GraphQL API（一种基于标准GraphQL的自定义实施）来无头地交付结构化内容以在应用程序中使用来实现的。 通过自定义单个API查询的功能，您可以检索和交付您想要/需要渲染的特定内容（作为对单个API查询的响应）。

>[!NOTE]
>
>另请参阅：
>
>* [什么是Headless?](/help/headless/what-is-headless.md) 有关Headless概念和术语的介绍。
>
>* [无头和AEM](/help/headless/introduction.md) 介绍AEM Sitesas a Cloud Service的Headless开发。


>[!NOTE]
>
>GraphQL 当前用于 Adobe Experience Manager (AEM) as a Cloud Service 中的两种（分隔的）场景：
>
>* [AEM Commerce通过GraphQL从商务平台使用数据](/help/commerce-cloud/integrating/magento.md).
>* [AEM内容片段可与AEM GraphQL API（一种基于标准GraphQL的自定义实施）一起使用，来提供结构化内容以供在应用程序中使用](/help/headless/graphql-api/content-fragments.md).


## 无头CMS {#headless-cms}

无头内容管理系统(CMS)包括：

* &quot;*无头内容管理系统（或无头CMS）是从头开始构建的仅后端内容管理系统(CMS)，它是一个内容存储库，通过API访问内容以在任何设备上显示。*

   请参阅 [维基百科](https://en.wikipedia.org/wiki/Headless_content_management_system).

在AEM中创作内容片段时，这意味着：

* 您可以使用内容片段创作主要不打算在带格式的页面上直(1:1)发布的内容。

* 内容片段的内容将按照预先确定的方式 — 根据内容片段模型进行构建。 这简化了对应用程序的访问，这将进一步处理您的内容。

## GraphQL — 概述 {#graphql-overview}

GraphQL 是：

* &quot;*...API的查询语言以及用于使用现有数据执行这些查询的运行时。*&quot;

   请参阅 [GraphQL.org](https://graphql.org)。

的 [AEM GraphQL API](#aem-graphql-api) 允许您对 [内容片段](/help/assets/content-fragments/content-fragments.md);每个查询都根据特定的模型类型。 然后，您的应用程序可以使用返回的内容。

## AEM GraphQL API {#aem-graphql-api}

对于Adobe Experience as a Cloud Experience，已开发标准GraphQL API的自定义实施。 请参阅 [AEM GraphQL API，用于内容片段](/help/headless/graphql-api/content-fragments.md) 以了解详细信息。

AEM GraphQL API实施基于 [GraphQL Java库](https://graphql.org/code/#java).

## 用于AEM GraphQL API的内容片段 {#content-fragments-use-with-aem-graphql-api}

[内容片段](#content-fragments) 可作为AEM查询的GraphQL的基础，如下所示：

* 它们允许您设计、创建、组织和发布独立于页面的内容。
* 的 [内容片段模型](#content-fragments-models) 通过定义的数据类型提供所需的结构。
* 的 [片段引用](#fragment-references)定义模型时可用，可用于定义其他结构层。

![与GraphQL一起使用的内容片段](assets/cfm-nested-01.png "与GraphQL一起使用的内容片段")

### 内容片段 {#content-fragments}

内容片段:

* 包含结构化内容。

* 它们基于 [内容片段模型](#content-fragments-models)，用于预定义生成片段的结构。

### 内容片段模型 {#content-fragments-models}

这些 [内容片段模型](/help/assets/content-fragments/content-fragments-models.md):

* 用于生成 [模式](https://graphql.org/learn/schema/)，一次 **已启用**.

* 提供GraphQL所需的数据类型和字段。 它们确保您的应用程序仅请求可能的内容，并接收预期内容。

* 数据类型 **[片段引用](#fragment-references)** 可在模型中使用来引用其他内容片段，因此可引入其他级别的结构。

### 片段引用 {#fragment-references}

的 **[片段引用](/help/assets/content-fragments/content-fragments-models.md#fragment-reference-nested-fragments)**:

* 与GraphQL结合使用时特别感兴趣。

* 是可在定义内容片段模型时使用的特定数据类型。

* 引用另一个片段，具体取决于特定的内容片段模型。

* 用于检索结构化数据。

   * 定义为 **多源**，则主片段可以引用（检索）多个子片段。

### JSON 预览 {#json-preview}

要帮助设计和开发内容片段模型，您可以预览 [JSON输出](/help/assets/content-fragments/content-fragments-json-preview.md).

## 了解如何将 GraphQL 与 AEM 结合使用 - 示例内容和查询 {#learn-graphql-with-aem-sample-content-queries}

请参阅 [了解如何将GraphQL与AEM结合使用 — 示例内容和查询](/help/headless/graphql-api/sample-queries.md) 有关使用AEM GraphQL API的简介。

## 教程 - AEM Headless 和 GraphQL 快速入门

正在寻找实践教程？请查看 [AEM Headless 和 GraphQL 快速入门](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html?lang=zh-Hans)端到端教程，其中说明了在 Headless CMS 场景中，如何使用 AEM GraphQL API 构建和公开内容并由外部应用程序使用。
