---
title: 通过 OpenAPI 进行 AEM 内容片段传递
description: 了解使用OpenAPI的tAEM内容片段交付
feature: Headless, Content Fragments, Edge Delivery Services
role: Admin, Developer
exl-id: b298db37-1033-4849-bc12-7db29fb77777
source-git-commit: 7f7ed3adcbd01f688f48f3ba4a0c25293b8b1551
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 4%

---

# 通过 OpenAPI 进行 AEM 内容片段传递 {#aem-content-fragment-delivery-with-openapi}

在Adobe Experience Manager (AEM) as a Cloud Service中，用于内容片段投放的AEM OpenAPI：

* 是一个OpenAPI，它针对JSON格式的AEM内容片段的实时投放进行了优化
* 提供允许活动内容失效的现代CDN集成
* 侧重于内容交付（性能、可扩展性、CDN集成、优化的JSON控制和输出）
* 包括为引用的片段和资产水合JSON的功能

此API：

* 是AEM Assets HTTP API中[内容片段支持的接替者](/help/assets/content-fragments/assets-api-content-fragments.md)

* 补充[内容片段和内容片段模型OpenAPI](/help/headless/content-fragment-openapis.md)，允许您管理内容片段和内容片段模型(CRUD)

* 是用于内容片段的[AEM GraphQL API的HTTP REST替代方法](/help/headless/graphql-api/content-fragments.md)

有关完整文档，请参阅[使用OpenAPI的AEM内容片段交付](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/contentfragments/delivery/)。

>[!NOTE]
>
>有关可用的各种API的概述以及所涉及概念的比较，请参阅结构化内容交付和管理的[AEM API](/help/headless/apis-headless-and-content-fragments.md)。

## 缓存 {#caching}

AEM与AEM CDN Fastly集成。 这意味着在发布层上提供的JSON响应将缓存在Fastly级别。

然后，根据预定义的缓存标头缓存响应（无法配置）：

* 响应在浏览器/客户端缓存中缓存5分钟
   * `max-age`=`300`
* 响应在CDN缓存中缓存1小时
   * `s-maxage`=`3600`
* 在重新验证新请求时，可为过时内容提供长达1小时的服务
   * `stale-while-revalidate`=`3600`
* 过时内容可错误提供长达1天
   * `stale-on-error`=`86400`

AEM还随附活动的CDN缓存失效功能。 这意味着每当更新或发布内容时，相应的JSON OpenAPI响应都会通过向Fastly发出的软清除请求自动失效。 这样，您就可以在到达实际CDN缓存期限(`s-maxage`)之前，看到在JSON输出中反映的更改。
