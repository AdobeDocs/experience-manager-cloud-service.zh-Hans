---
title: 用于结构化内容交付和内容片段管理的AEM API
description: 了解可用于结构化内容交付和内容片段管理的API
feature: Headless, Content Fragments, Edge Delivery Services
role: Admin, Developer
source-git-commit: 21599676916068f3529976410a93951b02f750b0
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 1%

---


# 用于结构化内容交付和管理的AEM API {#aem-apis-structured-content-delivery-and-management}

Adobe Experience Manager (AEM) as a Cloud Service为内容片段和内容片段管理的结构化内容投放提供了多个API。 有关特定API的更多详细信息，请参阅各个页面。

* 用于内容片段投放的[AEM REST OpenAPI](/help/headless/aem-rest-openapi-content-fragment-delivery.md)
   * 此API创建了JSON响应，用于从AEM中的内容片段提供结构化内容。
   * 它使用内容片段的路径作为端点。
   * 此API基于REST。
   * 它针对内容交付（包括CDN集成）进行了优化。
* [用于内容片段投放的AEM GraphQL API](/help/headless/graphql-api/content-fragments.md)
   * 此API基于架构。 API架构由内容片段模型表示，模型定义了内容结构。
   * 此API基于GraphQL。
* [Content Fragments 和 Content Fragment Models OpenAPIs](/help/headless/content-fragment-openapis.md)
   * 这些API用于结构化内容管理。
   * 各个GET运算符未针对内容交付进行优化。
   * 此API基于REST。
* [AEM Assets HTTP API中的内容片段支持](/help/assets/content-fragments/assets-api-content-fragments.md)
   * 用于AEM中结构化内容投放的JSON输出的原始API。
      * 虽然此API稳定可靠且经过验证，但它未提供&#x200B;*完全水合* JSON输出。 引用仅作为路径输出，需要辅助API请求以检索更多内容。
   * Assets HTTP API还可用于管理内容片段和内容片段模型(CRUD)。
   * 此API基于REST。
   * Assets HTTP API中的内容片段支持未来将被弃用，因为Edge Delivery ServicesJSON REST API将成功实现该支持。 时间刻度尚未确定。

<!--
## JSON vs HTML {#json-vs-HTML}

The content delivery format used is driven by frontend implementation. Unstructured content/HTML for full-stack implementations, structured content/JSON for headless implementations, or a combination of both in hybrid implementations. 

Key considerations include:

* Definition
  * JSON (JavaScript Object Notation) - used to represent, access and process structured data. 
  * HTML (HyperText Markup Language) - a markup language of tags and elements in a hierarchical structure.
* Primary Purpose
  * JSON is often used for transferring structure content between the server and client app.
  * HTML is the standard markup language for creating and rendering web pages in a browser.
-->

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
