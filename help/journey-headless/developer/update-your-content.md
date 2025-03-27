---
title: 如何通过AEM API更新您的内容
description: 在AEM Headless开发人员历程的这一可选部分中，了解如何使用可用的API访问和更新内容片段的内容。
exl-id: 84120856-fd1d-40f7-8df4-73d4cdfcc43b
solution: Experience Manager
feature: Headless, Content Fragments, GraphQL API
role: Admin, Architect, Developer
source-git-commit: d8e4fdc4f79e40a43a6845ab083dc231444b9c99
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 36%

---

# 如何通过AEM API更新您的内容 {#update-your-content}

在[AEM Headless开发人员历程](overview.md)的这一部分中，了解如何使用可用的API访问和更新内容片段的内容。

## 迄今为止的故事 {#story-so-far}

在 AEM Headless 历程的上一个文档[如何通过 AEM 交付 API 访问您的内容](access-your-content.md)中，您已了解如何通过 AEM GraphQL API 访问 AEM 中的 Headless 内容，现在应：

* 深入了解 GraphQL。
* 了解 AEM GraphQL API 的工作原理。
* 了解一些实际的示例查询。

本文基于这些基础之上，以便您了解如何通过可用的API在AEM中更新现有的Headless内容。

## 目标 {#objective}

* **受众**：高级
* **目标**：了解可用于访问和更新内容片段内容的API。

## 用于内容片段的AEM API {#aem-apis-for-use-with-content-fragments}

Adobe Experience Manager (AEM) as a Cloud Service为内容片段和内容片段管理的结构化内容投放提供了多个API。 有关特定API的更多详细信息，请参阅各个页面。

* 用于内容片段传递的 AEM REST OpenAPI
   * 此API用于创建从AEM中的内容片段提供结构化内容的JSON响应。
   * 它使用内容片段的路径作为端点。
   * 此API基于REST。
   * 它针对内容交付（包括CDN集成）进行了优化。
* 用于内容片段投放的AEM GraphQL API
   * 此API基于架构。 API架构由内容片段模型表示，模型定义了内容结构。
   * 此API基于GraphQL。
* Content Fragments 和 Content Fragment Models OpenAPIs
   * 这些API用于结构化内容管理。
   * 相应的GET运算符未针对内容交付进行优化。
   * 此API基于REST。
* AEM Assets HTTP API中的内容片段支持
   * 用于AEM中结构化内容投放的JSON输出的原始API。
      * 虽然此API稳定可靠且经过验证，但它未提供&#x200B;*完全水合* JSON输出。 引用仅作为路径输出，需要辅助API请求以检索更多内容。
   * Assets HTTP API还可用于管理内容片段和内容片段模型(CRUD)。
   * 此API基于REST。
   * Assets HTTP API中的内容片段支持未来将被弃用，因为Edge Delivery Services JSON REST API将接替此支持。 时间刻度尚未确定。

## 后续内容 {#whats-next}

现在您已完成 AEM Headless 开发人员历程的这一部分，您应：

* 了解可用的AEM API。
* 了解这些API如何支持内容片段。

您应继续您的 AEM Headless 历程，接下来查看文档[如何汇总您的应用程序和 AEM Headless 中的内容](put-it-all-together.md)，从而熟悉 AEM 架构基础知识以及用于将应用程序组合在一起的工具。

## 其他资源 {#additional-resources}

* [Adobe Experience Manager as a Cloud Service API](https://developer.adobe.com/experience-cloud/experience-manager-apis/)
* [用于结构化内容传递和管理的 AEM API](/help/headless/apis-headless-and-content-fragments.md)
* [用于内容片段传递的 AEM REST OpenAPI](/help/headless/aem-rest-openapi-content-fragment-delivery.md)
* [用于内容片段投放的AEM GraphQL API](/help/headless/graphql-api/content-fragments.md)
* [Content Fragments 和 Content Fragment Models OpenAPIs](/help/headless/content-fragment-openapis.md)
* [AEM Assets HTTP API中的内容片段支持](/help/assets/content-fragments/assets-api-content-fragments.md)
* [使用内容片段](/help/sites-cloud/administering/content-fragments/overview.md)
* [AEM 核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans)
* [已说明 CORS/AEM](https://helpx.adobe.com/cn/experience-manager/kt/platform-repository/using/cors-security-article-understand.html)
* [视频 – 使用 AEM 针对 CORS 进行开发](https://helpx.adobe.com/cn/experience-manager/kt/platform-repository/using/cors-security-technical-video-develop.html)
* [AEM as a Headless CMS 简介](/help/headless/introduction.md)
* [AEM 开发人员门户](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=zh-Hans)
* [AEM 中的 Headless 教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-Headless/overview.html?lang=zh-hans)
