---
title: 创建 API 请求 – Headless 设置
description: 了解如何使用 GraphQL API 实现内容片段的 Headless 投放，以及如何使用 AEM 的 Assets REST API 管理内容片段。
exl-id: 2b72f222-2ba5-4a21-86e4-40c763679c32
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: 38a4bf89e099432163163e90e08aa0f47407724f
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 88%

---

# 创建 API 请求 – Headless 设置 {#accessing-delivering-content-fragments}

了解如何使用 GraphQL API 实现内容片段的 Headless 投放，以及如何使用 AEM 的 Assets REST API 管理内容片段。

## 什么是 GraphQL 和 Assets REST API？ {#what-are-the-apis}

[现在您已创建了一些内容片段](create-content-fragment.md)，可以使用AEM的API来无头交付它们。

* [GraphQL API](/help/headless/graphql-api/content-fragments.md) 允许您创建请求来访问和投放内容片段。此 API 提供了最可靠的一组功能用于查询和使用内容片段内容。
   * 若要使用该 API，[定义并启用 AEM](/help/headless/graphql-api/graphql-endpoint.md) 中的端点以及安装的 [GraphiQL 接口（如有必要）。](/help/headless/graphql-api/graphiql-ide.md)
* 用于结构化内容交付和管理的[AEM API](/help/headless/apis-headless-and-content-fragments.md)可供内容片段使用。

本指南的剩余部分侧重于 GraphQL 访问和内容片段投放。

## 启用 GraphQL 端点 {#enable-graphql-endpoint}

必须先创建 GraphQL 端点，然后才能使用 GraphQL API。

有关详细信息，请参阅[在AEM中管理GraphQL端点](/help/headless/graphql-api/graphql-endpoint.md)。

## 使用 GraphQL 及 GraphiQL 查询内容

信息架构师为其渠道端点设计查询来交付内容。每个端点、每个模型只考虑一次这些查询。对于本指南快速入门，您只需要创建一个。

GraphiQL 是一个 IDE，包含在您的 AEM 环境中； 在您[配置您的端点](#enable-graphql-endpoint)后，它是可访问/可见的。

有关详细信息，请参阅[使用GraphiQL IDE](/help/headless/graphql-api/graphiql-ide.md)。

GraphQL 启用结构化查询，不仅针对特定数据集或者单独的数据对象，而且还可以提供对象的特定元素，嵌套结果，提供查询变量支持，以及诸多功能。

GraphQL 可以避免迭代 API 以及过度投放，而是允许作为对单个 API 查询的响应，批量精确投放所需呈现的内容。生成的 JSON 可用于向其他站点或应用程序提供数据。

## 后续步骤 {#next-steps}

就是这样！现在，您已对 AEM 中的 Headless 内容管理有了基本了解。其中还有很多资源供您深入研究，以全面了解可用的功能。

* **[内容片段](/help/sites-cloud/administering/content-fragments/managing.md)** – 提供有关创建和管理内容片段的详细信息
* **[AEM Assets HTTP API 中的内容片段支持](/help/assets/content-fragments/assets-api-content-fragments.md)** – 提供直接通过 HTTP API 使用 CRUD 操作（创建、读取、更新、删除）访问 AEM 内容的详细信息
* **[GraphQL API](/help/headless/graphql-api/content-fragments.md)** – 提供有关如何以 Headless 方式投放内容片段的详细信息

>[!NOTE]
>
>[内容片段和内容片段模型 OpenAPI](/help/headless/content-fragment-openapis.md) 也可用。
