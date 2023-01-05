---
title: 使用带有 GraphQL 的内容片段的 Headless 内容投放
description: 了解使用 GraphQL 中的内容片段实现 AEM Headless CMS 以进行 headless 内容投放的基本概念。
feature: Content Fragments, GraphQL API
role: User
exl-id: ef48f737-a5b3-4913-9f37-6b9f681bc048
source-git-commit: 6204830f30c28daba3ff87ba60acd0150847b523
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 100%

---

# 使用带有 GraphQL 的内容片段的 Headless 内容投放 {#headless-content-delivery-using-content-fragments-with-graphQL}

借助内容片段和 GraphQL API，您可以将 Adobe Experience Manager (AEM) as a Cloud Service 用作 Headless 内容管理系统(CMS)。

这是通过使用内容片段和 AEM GraphQL API（一种基于标准 GraphQL 的自定义实现）来实现的，以 headless 方式投放结构化内容以供您的应用程序使用。 通过自定义单个 API 查询的功能，您可以检索和投放您想要/需要呈现的特定内容（作为对单个 API 查询的响应）。

>[!NOTE]
>
>另请参阅：
>
>* [什么是 Headless？](/help/headless/what-is-headless.md) 有关 Headless 概念和术语的介绍。
>
>* [Headless 和 AEM](/help/headless/introduction.md) 介绍 AEM Sites as a Cloud Service 的 Headless 开发。


>[!NOTE]
>
>GraphQL 当前用于 Adobe Experience Manager (AEM) as a Cloud Service 中的两种（分隔的）场景：
>
>* [AEM Commerce 通过 GraphQL 使用来自 Commerce 平台的数据](/help/commerce-cloud/integrating/magento.md)。
>* [AEM 内容片段与 AEM GraphQL API（一种自定义实现，基于标准 GraphQL）配合使用，提供结构化内容用于您的应用程序](/help/headless/graphql-api/content-fragments.md)。


## Headless CMS {#headless-cms}

无头内容管理系统 (CMS) 是一种仅用于后端的内容管理系统，其明确作为内容存储库而设计和构建，使内容可通过 API 访问并在任何设备上显示。

在 AEM 中创作内容片段时，这意味着：

* 您可以使用内容片段来创作主要不打算在格式化页面上直接发布 (1:1) 的内容。

* 您的内容片段的内容将以预先确定的方式构建 – 根据内容片段模型。 这简化了对应用程序的访问，这将进一步处理您的内容。

## GraphQL — 概述 {#graphql-overview}

GraphQL 是：

* ”*...一种用于 API 和运行时的查询语言，使用您的现有数据满足这些查询。*“。

   请参阅 [GraphQL.org](https://graphql.org)

[AEM GraphQL API](#aem-graphql-api) 允许您对[内容片段](/help/sites-cloud/administering/content-fragments/content-fragments.md)执行（复杂）查询；每个查询都根据特定的模型类型。 然后，您的应用程序可以使用返回的内容。

## AEM GraphQL API {#aem-graphql-api}

对于作为云体验的 Adobe Experience，已经开发了标准 GraphQL API 的自定义实现。 请参阅[用于内容片段的 AEM GraphQL API](/help/headless/graphql-api/content-fragments.md) 以了解详细信息。

AEM GraphQL API 实施基于 [GraphQL Java 库](https://graphql.org/code/#java)。

## 用于 AEM GraphQL API 的内容片段 {#content-fragments-use-with-aem-graphql-api}

[内容片段](#content-fragments)可作为 AEM 查询的 GraphQL 的基础，如下所示：

* 它们允许您设计、创建、组织和发布独立于页面的内容。
* [内容片段模型](#content-fragments-models)通过定义的数据类型提供所需的结构。
* 定义模型时可用的[片段参考](#fragment-references)可用于定义额外的结构层。

![与 GraphQL 一起使用的内容片段](assets/cfm-nested-01.png "与 GraphQL 一起使用的内容片段")

### 内容片段 {#content-fragments}

内容片段：

* 包含结构化内容。

* 它们基于[内容片段模型](#content-fragments-models)，用于预定义生成片段的结构。

### 内容片段模型 {#content-fragments-models}

这些[内容片段模型](/help/sites-cloud/administering/content-fragments/content-fragments-models.md)：

* 一旦&#x200B;**启用**，用于生成[模式](https://graphql.org/learn/schema/)。

* 提供 GraphQL 所需的数据类型和字段。 它们确保您的应用程序仅请求可能的内容，并接收预期内容。

* 数据类型&#x200B;**[片段引用](#fragment-references)**&#x200B;可在模型中使用来引用其他内容片段，因此可引入其他级别的结构。

### 片段引用 {#fragment-references}

**[片段引用](/help/sites-cloud/administering/content-fragments/content-fragments-models.md#fragment-reference-nested-fragments)**：

* 与 GraphQL 结合使用时特别感兴趣。

* 是可在定义内容片段模型时使用的特定数据类型。

* 引用另一个片段，具体取决于特定的内容片段模型。

* 用于检索结构化数据。

   * 定义为&#x200B;**多源**，则主片段可以引用（检索）多个子片段。

### JSON 预览 {#json-preview}

要帮助设计和开发内容片段模型，您可以预览 [JSON 输出](/help/sites-cloud/administering/content-fragments/content-fragments-json-preview.md)。

## 了解如何将 GraphQL 与 AEM 结合使用 – 示例内容和查询 {#learn-graphql-with-aem-sample-content-queries}

有关使用 AEM GraphQL API 的介绍，请参阅[学习将 GraphQL 与 AEM 结合使用 – 示例内容和查询](/help/headless/graphql-api/sample-queries.md)。

## 教程 – AEM Headless 和 GraphQL 快速入门

正在寻找实践教程？请查看 [AEM Headless 和 GraphQL 快速入门](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html)端到端教程，其中说明了在 Headless CMS 场景中，如何使用 AEM GraphQL API 构建和公开内容并由外部应用程序使用。
