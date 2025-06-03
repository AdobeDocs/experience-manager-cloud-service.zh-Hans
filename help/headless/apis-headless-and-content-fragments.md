---
title: 用于结构化内容交付和内容片段管理的AEM API
description: 了解可用于结构化内容交付和内容片段管理的API
feature: Headless, Content Fragments, Edge Delivery Services
role: Admin, Developer
exl-id: 95aecd30-566a-42a9-b97a-7efe45fd389c
source-git-commit: 1995c84bb669fd52ecd53c7e695acc518a5226e8
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 28%

---


# 用于结构化内容传递和管理的 AEM API {#aem-apis-structured-content-delivery-and-management}

Adobe Experience Manager (AEM) as a Cloud Service 为内容片段的结构化内容传递和内容片段管理提供了多个 API。有关特定 API 的更多详细信息，请参阅各个页面。

* [通过 OpenAPI 进行 AEM 内容片段传递](/help/headless/aem-content-fragment-delivery-with-openapi.md)
   * 此 API 创建 JSON 响应，用于传递 AEM 中内容片段的结构化内容。
   * 它使用内容片段的路径作为端点。
   * 这个 API 基于 REST。
   * 它针对内容传递进行了优化，包括 CDN 集成。
* [用于内容片段传递的 AEM GraphQL API](/help/headless/graphql-api/content-fragments.md)
   * 这个 API 基于架构。API 构架由定义内容结构的内容片段模型表示。
   * 这个 API 基于 GraphQL。
* [Content Fragments 和 Content Fragment Models OpenAPIs](/help/headless/content-fragment-openapis.md)
   * 这些 API 旨在用于结构化内容管理。
   * 各个 GET 运算符并未针对内容传递进行优化。
   * 这个 API 基于 REST。

>[!NOTE]
>
>Assets HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md)中的[内容片段支持现在[已弃用](/help/release-notes/deprecated-removed-features.md)。 它已被替换为[OpenAPI的内容片段投放](/help/headless/aem-content-fragment-delivery-with-openapi.md)以及[内容片段和内容片段模型管理OpenAPI](/help/headless/content-fragment-openapis.md)。

## REST与GraphQL {#rest-vs-graphql}

使用的API是开发人员的决策 — AEM同时支持这两者。

可以在线进行许多比较，但REST的一些亮点和优点包括：

* 简单性

   * 开发人员（通常）熟悉HTTP和REST。 根据API报告](https://www.postman.com/state-of-api/)的[Postman状态，有高百分比的开发人员使用REST。

   * 简单又熟悉。 对于REST，不存在关于谁拥有查询以及谁拥有应用程序的组织问题，而GraphQL可能会出现这些问题。

   * 熟悉度（通常情况下）带来了广泛的社区和工具环境。 这不是GraphQL的固有劣势，但对REST而言，它可能会更广泛、更深入。

   * 更简单的方法还可以使安全实施更容易。 使用REST时，将在客户端应用程序中筛选以确定要呈现所有内容的内容。 使用GraphQL，这发生在客户端和服务器之间的基于架构的查询中。

* 灵活性

   * 使用REST，开发人员可以`GET`任何资源。 使用GraphQL时，限制使用架构中定义的资源。

* 缓存

   * 对REST `GET`请求的JSON响应本身可缓存。 无法缓存GraphQL `POST`请求，除非发出这些请求；例如，使用存储在服务器上并通过类似REST的`GET`请求请求请求的AEM持久查询。

GraphQL的好处包括：

* 内容交付效率

   * 焦点

      * 使用GraphQL客户端应用程序，可以请求渲染所需的确切内容，而不再请求。 此方法可防止内容过度交付、内容负载过多以及不必要的带宽消耗。

   * 单个端点

      * 在REST中，每个API请求都是一个端点，但在GraphQL中，只有一个公用端点，并且不同的内容请求都使用该公用端点表示为查询。

* 快速原型

   * 使用GraphQL，只需一步即可将查询功能整合在GraphQL中，从而更轻松地制作原型。 另一方面，REST分为两步：

      1. 使用API获取内容。
      2. 在JSON响应中，确定要在客户端应用程序中渲染的内容。
