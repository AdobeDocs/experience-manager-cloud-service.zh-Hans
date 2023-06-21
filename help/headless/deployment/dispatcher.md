---
title: AEM Headless 的 Dispatcher 配置
description: Dispatcher 是位于 Adobe Experience Manager 发布环境前的缓存和安全层。使用多个配置将 GraphQL 端点打开到 Headless 应用程序。
feature: Dispatcher, GraphQL API
exl-id: 78a20021-910f-4cf0-87bf-6e2223994f76
source-git-commit: f0edd0e3deeba89dcbd2dc1a07859138b24e2220
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 55%

---

# AEM Headless 的 Dispatcher 配置

[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=zh-Hans) 是位于 Adobe Experience Manager 发布环境前的缓存和安全层。默认情况下包括多个配置用于将 GraphQL 端点打开到 Headless 应用程序。

>[!NOTE]
>
>有关Dispatcher的详细信息，请参阅 [Dispatcher指南](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=zh-Hans).

作为AEM项目的一部分，包括一个Dispatcher模块，其中包含用于Dispatcher的配置。 新生成的项目 [AEM项目原型](https://github.com/adobe/aem-project-archetype) 自动包括 [过滤器](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=zh-Hans?#defining-a-filter) 启用GraphQL端点。

## GraphQL端点

作为默认筛选条件的一部分，[GraphQL 端点](/help/headless/graphql-api/graphql-endpoint.md)打开时遵循以下规则：

```
/0060 { /type "allow" /method '(POST|OPTIONS)' /url "/content/_cq_graphql/*/endpoint.json" }
```

`*` 通配符在 AEM 实例上打开多个端点。使用GraphQL端点进行查询时，使用 `POST` 回答是 **非** 已缓存。

## GraphQL 持久查询

对持久查询的请求是针对不同的端点发出的。 作为默认筛选配置的一部分，的URL [持久查询](/help/headless/graphql-api/persisted-queries.md) 打开时遵循以下规则：

```
/0061 { /type "allow" /method '(GET|POST|OPTIONS)' /url "/graphql/execute.json*" }
```

可以使用请求持久查询 `GET`，方法是：在Dispatcher和CDN级别缓存响应。 有关缓存和缓存失效的更多详细信息见[此处](/help/implementing/dispatcher/caching.md)。
