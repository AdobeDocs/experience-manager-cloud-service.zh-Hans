---
title: AEM Headless 的 Dispatcher 端点配置
description: Dispatcher 是位于 Adobe Experience Manager 发布环境前的缓存和安全层。使用多个配置将 GraphQL 端点打开到 Headless 应用程序。
feature: Headless, Dispatcher, GraphQL API
exl-id: 78a20021-910f-4cf0-87bf-6e2223994f76
role: Admin, Developer
source-git-commit: 6719e0bcaa175081faa8ddf6803314bc478099d7
workflow-type: ht
source-wordcount: '222'
ht-degree: 100%

---


# AEM Headless 的 Dispatcher 端点配置

[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=zh-Hans) 是位于 Adobe Experience Manager 发布环境前的缓存和安全层。默认情况下包括多个配置用于将 GraphQL 端点打开到 Headless 应用程序。

>[!NOTE]
>
>有关 Dispatcher 的详细文档，请参阅 [Dispatcher 指南。](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=zh-Hans)

AEM 项目中包括 Dispatcher 模块，其中包含用于 Dispatcher 的配置。从 [AEM 项目原型](https://github.com/adobe/aem-project-archetype)新生成的项目自动包括启用 GraphQL 端点的[筛选条件](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=zh-Hans?#defining-a-filter)。

## GraphQL 端点

作为默认筛选条件的一部分，[GraphQL 端点](/help/headless/graphql-api/graphql-endpoint.md)打开时遵循以下规则：

```
/0060 { /type "allow" /method '(POST|OPTIONS)' /url "/content/_cq_graphql/*/endpoint.json" }
```

`*` 通配符在 AEM 实例上打开多个端点。通过 GraphQL 端点进行的查询会使用 `POST` 发出，并且&#x200B;**不**&#x200B;会缓存响应。

## GraphQL 持久查询

对持久查询的请求对不同的端点发出。作为默认筛选配置的一部分，[持久查询](/help/headless/graphql-api/persisted-queries.md)的 URL 打开时遵循以下规则：

```
/0061 { /type "allow" /method '(GET|POST|OPTIONS)' /url "/graphql/execute.json*" }
```

通过在 Dispatcher 和 CDN 级别缓存响应，可以使用 `GET` 请求持久查询。有关缓存和缓存失效的更多详细信息，请参阅 [AEM as a Cloud Service 的缓存介绍](/help/implementing/dispatcher/caching.md)。
