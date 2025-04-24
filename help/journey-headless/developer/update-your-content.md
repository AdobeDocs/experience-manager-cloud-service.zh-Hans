---
title: 如何通过 AEM APIs 更新您的内容
description: 在 AEM Headless 开发人员历程的这一部分中，了解如何使用可用的 API 访问和更新内容片段的内容。
exl-id: 84120856-fd1d-40f7-8df4-73d4cdfcc43b
solution: Experience Manager
feature: Headless, Content Fragments, GraphQL API
role: Admin, Architect, Developer
source-git-commit: d9db32110e1e0aaa5bdc20bd6b4bff6da6a3a3a3
workflow-type: ht
source-wordcount: '578'
ht-degree: 100%

---

# 如何通过 AEM APIs 更新您的内容 {#update-your-content}

在 [AEM Headless 开发人员历程](overview.md)的这一部分中，了解如何使用可用的 API 访问和更新内容片段的内容。

## 迄今为止的故事 {#story-so-far}

在 AEM Headless 历程的上一个文档[如何通过 AEM 传递 API 访问您的内容](access-your-content.md)中，您已了解如何通过 AEM GraphQL API 访问 AEM 中的 Headless 内容，现在应：

* 深入了解 GraphQL。
* 了解 AEM GraphQL API 的工作原理。
* 了解一些实际的示例查询。

本文基于这些基础知识编写，以便您了解如何通过可用的 API 更新 AEM 中现有的 Headless 内容。

## 目标 {#objective}

* **受众**：高级
* **目标**：了解可用于访问和更新内容片段的内容的 API。

## 用于内容片段的 AEM API {#aem-apis-for-use-with-content-fragments}

Adobe Experience Manager (AEM) as a Cloud Service 为内容片段的结构化内容传递和内容片段管理提供了多个 API。有关特定 API 的更多详细信息，请参阅各个页面。

* 通过 OpenAPI 进行 AEM 内容片段传递
   * 此 API 创建 JSON 响应，用于传递 AEM 中内容片段的结构化内容。
   * 它使用内容片段的路径作为端点。
   * 这个 API 基于 REST。
   * 它针对内容传递进行了优化，包括 CDN 集成。
* 用于内容片段传递的 AEM GraphQL API
   * 这个 API 基于架构。API 构架由定义内容结构的内容片段模型表示。
   * 这个 API 基于 GraphQL。
* Content Fragments 和 Content Fragment Models OpenAPIs
   * 这些 API 旨在用于结构化内容管理。
   * 各个 GET 运算符并未针对内容传递进行优化。
   * 这个 API 基于 REST。
* AEM Assets HTTP API 中的内容片段支持
   * 用于 AEM 中结构化内容传递的 JSON 输出的原始 API。
      * 虽然该 API 功能强大且经过验证，但它不传递&#x200B;*完全水合的* JSON 输出。引用仅作为路径输出，需要辅助 API 请求来进一步检索内容。
   * Assets HTTP API 还可用于管理内容片段和内容片段模型（CRUD）。
   * 这个 API 基于 REST。
   * 未来，Assets HTTP API 中对内容片段的支持将被弃用，因为它将被 Edge Delivery Services JSON REST API 取代。具体时间尚未确定。

## 后续内容 {#whats-next}

现在您已完成 AEM Headless 开发人员历程的这一部分，您应：

* 了解可用的 AEM API。
* 了解这些 API 如何支持内容片段。

您应继续您的 AEM Headless 历程，接下来查看文档[如何汇总您的应用程序和 AEM Headless 中的内容](put-it-all-together.md)，从而熟悉 AEM 架构基础知识以及用于将应用程序组合在一起的工具。

## 其他资源 {#additional-resources}

* [Adobe Experience Manager as a Cloud Service API](https://developer.adobe.com/experience-cloud/experience-manager-apis/)
* [用于结构化内容传递和管理的 AEM API](/help/headless/apis-headless-and-content-fragments.md)
* [通过 OpenAPI 进行 AEM 内容片段传递](/help/headless/aem-content-fragment-delivery-with-openapi.md)
* [用于内容片段传递的 AEM GraphQL API](/help/headless/graphql-api/content-fragments.md)
* [Content Fragments 和 Content Fragment Models OpenAPIs](/help/headless/content-fragment-openapis.md)
* [AEM Assets HTTP API 中的内容片段支持](/help/assets/content-fragments/assets-api-content-fragments.md)
* [使用内容片段](/help/sites-cloud/administering/content-fragments/overview.md)
* [AEM 核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans)
* [已说明 CORS/AEM](https://helpx.adobe.com/cn/experience-manager/kt/platform-repository/using/cors-security-article-understand.html)
* [视频 – 使用 AEM 针对 CORS 进行开发](https://helpx.adobe.com/cn/experience-manager/kt/platform-repository/using/cors-security-technical-video-develop.html)
* [AEM as a Headless CMS 简介](/help/headless/introduction.md)
* [AEM 开发人员门户](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=zh-Hans)
* [AEM 中的 Headless 教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-Headless/overview.html?lang=zh-hans)
