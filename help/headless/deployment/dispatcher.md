---
title: 使用AEM Headless进行Dispatcher配置
description: Dispatcher是位于Adobe Experience Manager发布环境之前的缓存和安全层。 有些配置用于向无头应用程序打开GraphQL端点。
feature: Dispatcher, GraphQL API
source-git-commit: 0cc131209f497241949f8da6e8144dfcaffe7e6e
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 6%

---


# 使用AEM Headless进行Dispatcher配置

的 [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html) 是Adobe Experience Manager发布环境之前的缓存和安全层。 默认情况下，包含一些配置，用于将GraphQL端点打开到无头应用程序。

>[!NOTE]
>
>有关Dispatcher的详细文档，请参阅 [Dispatcher指南](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html)

作为AEM Project的一部分，包含一个包含调度程序配置的调度程序模块。 中新生成的项目 [AEM项目原型](https://github.com/adobe/aem-project-archetype) 自动包含 [过滤器](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?#defining-a-filter) 启用GraphQL端点。

## GraphQL端点

作为默认过滤器的一部分， [GraphQL端点](/help/headless/graphql-api/graphql-endpoint.md) 将使用以下规则打开：

```
/0060 { /type "allow" /method '(POST|OPTIONS)' /url "/content/_cq_graphql/*/endpoint.json" }
```

的 `*` 通配符会在AEM实例上打开多个端点。 将使用GraphQL端点进行查询 `POST` 然后回应 **not** 缓存。

## GraphQL持久查询

对持久化查询的请求针对其他端点发出。 作为默认过滤器配置的一部分， [持久化查询](/help/headless/graphql-api/persisted-queries.md) 将使用以下规则打开：

```
/0061 { /type "allow" /method '(GET|POST|OPTIONS)' /url "/graphql/execute.json*" }
```

可以使用 `GET`，从而在调度程序和CDN级别缓存响应。 有关缓存和缓存失效的更多详细信息，请参阅 [此处](/help/implementing/dispatcher/caching.md).
