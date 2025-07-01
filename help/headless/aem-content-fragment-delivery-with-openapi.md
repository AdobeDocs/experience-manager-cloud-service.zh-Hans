---
title: 通过 OpenAPI 进行 AEM 内容片段传递
description: 了解使用OpenAPI的tAEM内容片段交付
feature: Headless, Content Fragments, Edge Delivery Services
role: Admin, Developer
exl-id: b298db37-1033-4849-bc12-7db29fb77777
source-git-commit: 28d0d6bdfd9e6f1c1483bed7c5e65df340e8b559
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 2%

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

>[!IMPORTANT]
>
>要在AEM as a Cloud Service上使用OpenAPI启用内容片段投放，请确保尚未启用，然后提交标题为&#x200B;**使用OpenAPI启用内容片段投放**&#x200B;的Adobe支持票证，并指定：
>
>* Cloud Service项目和环境ID
>* 您希望通过内容片段投放OpenAPI解决的用例的详细信息
>* Adobe应响应并随时了解请求和项目（如果需要）的所有联系人的详细信息

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

使用OpenAPI的内容片段投放支持活动CDN缓存失效。 这意味着每当更新或发布内容时，相应的JSON OpenAPI响应都会通过向Fastly发出的软清除请求自动失效。 这样，您就可以在到达实际CDN缓存期限(`s-maxage`)之前，看到在JSON输出中反映的更改。

## 可用性 {#availability}

使用OpenAPI的内容片段投放在预览层和发布层上可用。 OpenAPI以JSON格式提供内容片段，用于预览和实时交付。

要预览使用OpenAPI的内容片段投放，可以：

* 发布到预览
* 启用访问以通过IP允许列表预览
* 获取预览URL

## CORS {#cors}

[CORS允许的源](/help/headless/deployment/cross-origin-resource-sharing.md)定义可以调用API的源。

此API不考虑在Dispatcher配置端定义、专门用于GraphQL的CORS允许的源。

## API速率限制 {#api-rate-limits}

API允许新请求的速率为每环境每秒最多200个请求。

一旦超过此限制，API就会开始发送429错误。 这些错误必须由任何客户端应用程序处理，并且失败的请求在指数回退重试后重试。

<!-- 
## Limitations {#limitations}
-->
