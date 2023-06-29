---
title: 缓存和性能
description: 了解各种配置，这些配置可用于启用GraphQL和内容缓存以优化Commerce实施的性能。
exl-id: 21ccdab8-4a2d-49ce-8700-2cbe129debc6
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 2%

---

# 缓存和性能 {#caching}

## 组件和GraphQL响应缓存 {#graphql}

AEM CIF核心组件已内置支持缓存各个组件的GraphQL响应。 可以使用此功能在很大程度上减少GraphQL后端调用的数量。 特别对于重复查询，如检索导航组件的类别树或获取在产品搜索和类别页面上显示的所有可用聚合/彩块化值，可以实现有效的缓存。

对于AEM CIF核心组件，缓存是基于组件配置的，因此可以控制是否对每个组件缓存GraphQL请求/响应（以及缓存时长）。 还可以使用GraphQL客户端定义OSGi服务的缓存行为。

### 配置 {#configuration}

为给定组件配置后，缓存将开始存储GraphQL查询和响应，如每个缓存配置条目所定义。 缓存的大小和每个条目的缓存持续时间是根据项目定义的，具体取决于以下因素：

* 目录数据可能更改的频率。
* 组件始终显示最新可能的数据是多么重要，等等。

没有任何缓存失效，因此设置缓存持续时间时要小心。

配置组件的缓存时，缓存名称必须是组件的名称， **代理** 您在项目中定义的组件。

在客户端发送GraphQL请求之前，会检查是否 **精确** 已缓存同一GraphQL请求，并且可能返回缓存的响应。 要匹配，请添加GraphQL请求 _必须_ 完全匹配。 即查询、操作名称（如果有）、变量（如果有） _必须_ 均等于缓存的请求。 所有可能设置的自定义HTTP标头 _必须_ 也是一样的。 例如，Adobe Commerce `Store` 标头 _必须_ 匹配。

### 示例 {#examples}

Adobe建议您为search服务配置一些缓存，以便获取“产品search”和“类别”页面上显示的所有可用聚合/彩块化值。 例如，只有在向产品添加新属性时，这些值才会发生更改。 因此，如果产品属性集不经常更改，则此缓存条目的持续时间可能很“长”。 虽然此条目特定于项目，但Adobe建议在项目开发阶段使用几分钟的值，在稳定生产系统上使用几小时的值。

此设置通常使用以下缓存条目进行配置：

```
com.adobe.cq.commerce.core.search.services.SearchFilterService:true:10:3600
```

建议使用GraphQl缓存功能的另一个示例方案是导航组件。 原因是它会在所有页面上发送相同的GraphQL查询。 在这种情况下，缓存条目通常设置为：

```
venia/components/structure/navigation:true:10:600
```

考虑到 [Venia引用存储](https://github.com/adobe/aem-cif-guides-venia) 已使用。 请注意组件代理名称的使用 `venia/components/structure/navigation`、和 **非** CIF导航组件的名称(`core/cif/components/structure/navigation/v1/navigation`)。

其他组件的缓存应基于项目定义，通常与在Dispatcher级别配置的缓存相协调。 请记住，这些缓存没有任何活动失效机制，因此应小心设置缓存持续时间。 没有任何“适合所有”的值能够匹配所有可能的项目和用例。 确保在项目级别定义最符合项目要求的缓存策略。

## Dispatcher缓存 {#dispatcher}

在中缓存AEM页面或片段 [AEM调度程序](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html) 是任何AEM项目的最佳实践。 通常，它依赖于失效技术，以确保在AEM中更改的任何内容在Dispatcher中正确更新。 此功能是AEM Dispatcher缓存策略的核心。

除了纯AEM管理的内容CIF之外，页面通常还可以显示通过GraphQL从Adobe Commerce动态获取的商务数据。 虽然页面结构本身可能永远不会更改，但商业内容可能会更改。 例如，如果产品数据（如名称和价格）在Adobe Commerce中发生更改。

为了确保CIF页面在AEM Dispatcher中的缓存时间有限，Adobe建议使用 [基于时间的缓存失效](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#configuring-time-based-cache-invalidation-enablettl) 在AEM Dispatcher中缓存CIF页面时（称为基于TTL的缓存）。 可在AEM中使用额外的 [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/) 包。

对于基于TTL的缓存，开发人员通常为选定的AEM页面定义一个或多个缓存持续时间。 此持续时间可确保仅在AEM Dispatcher中缓存CIF页面，最长可达配置的持续时间，并且内容会经常更新。

>[!NOTE]
>
>虽然AEM Dispatcher可能会缓存服务器端数据，但某些CIF组件(如 `product`， `productlist`、和 `searchresults` 组件通常在加载页面时始终在客户端浏览器请求中重新获取产品价格。 这样做可确保始终在页面加载时获取关键动态内容。

## 其他资源 {#additional}

* [Venia引用存储](https://github.com/adobe/aem-cif-guides-venia)
* [GraphQL缓存配置](https://github.com/adobe/commerce-cif-graphql-client#caching)
* [AEM调度程序](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html)
