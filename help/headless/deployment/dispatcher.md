---
title: AEM Headless 的 Dispatcher 配置
description: Dispatcher 是位于 Adobe Experience Manager 发布环境前的缓存和安全层。使用多个配置将 GraphQL 端点打开到 Headless 应用程序。
feature: Dispatcher, GraphQL API
exl-id: 78a20021-910f-4cf0-87bf-6e2223994f76
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 93%

---

# AEM Headless 的 Dispatcher 配置

[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=zh-Hans) 是位于 Adobe Experience Manager 发布环境前的缓存和安全层。默认情况下包括多个配置用于将 GraphQL 端点打开到 Headless 应用程序。

>[!NOTE]
>
>有关 Dispatcher 的详细文档，请参阅 [Dispatcher 指南](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=zh-Hans)

AEM 项目中包括 Dispatcher 模块，其中包含用于 Dispatcher 的配置。从 [AEM 项目原型](https://github.com/adobe/aem-project-archetype)新生成的项目自动包括启用 GraphQL 端点的[筛选条件](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=zh-Hans?#defining-a-filter)。

## GraphQL 端点

作为默认筛选条件的一部分，[GraphQL 端点](/help/headless/graphql-api/graphql-endpoint.md)打开时遵循以下规则：

```
/0060 { /type "allow" /method '(POST|OPTIONS)' /url "/content/_cq_graphql/*/endpoint.json" }
```

`*` 通配符在 AEM 实例上打开多个端点。使用GraphQL端点进行查询时，使用 `POST` 而回应将会 **非** 已缓存。

## GraphQL 持久查询

对持久查询的请求对不同的端点发出。作为默认筛选配置的一部分，[持久查询](/help/headless/graphql-api/persisted-queries.md)的 URL 打开时遵循以下规则：

```
/0061 { /type "allow" /method '(GET|POST|OPTIONS)' /url "/graphql/execute.json*" }
```

可以使用 `GET` 请求持久查询，从而在 Dispatcher 和 CDN 级别缓存响应。有关缓存和缓存失效的更多详细信息见[此处](/help/implementing/dispatcher/caching.md)。
