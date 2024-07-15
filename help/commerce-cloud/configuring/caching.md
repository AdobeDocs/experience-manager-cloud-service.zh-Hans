---
title: 缓存和性能
description: 了解可用于启用GraphQL和内容缓存以优化Commerce实施性能的各种配置。
exl-id: 21ccdab8-4a2d-49ce-8700-2cbe129debc6
feature: Commerce Integration Framework
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 0%

---

# 缓存和性能 {#caching}

## 组件和GraphQL响应缓存 {#graphql}

AEM CIF核心组件已内置支持缓存各个组件的GraphQL响应。 可以使用此功能在很大程度上减少GraphQL后端调用的数量。 特别对于重复查询，如检索导航组件的类别树或获取在产品搜索和类别页面上显示的所有可用聚合/彩块化值，可以实现有效的缓存。

对于AEM CIF核心组件，缓存是基于组件配置的，因此可以控制是否对每个组件缓存GraphQL请求/响应（以及缓存时长）。 也可以使用GraphQL客户端定义OSGi服务的缓存行为。

### 配置 {#configuration}

为给定组件配置后，缓存将开始存储由每个缓存配置条目定义的GraphQL查询和响应。 高速缓存的大小和每个条目的高速缓存持续时间是按项目定义的，具体取决于例如以下各项：

* 目录数据可能更改的频率。
* 组件始终显示最新可能的数据等重要信息。

没有任何缓存失效，因此设置缓存持续时间时要小心。

配置组件的缓存时，缓存名称必须是您在项目中定义的&#x200B;**代理**&#x200B;组件的名称。

在客户端发送GraphQL请求之前，它会检查是否已缓存&#x200B;**完全相同的**&#x200B;个GraphQL请求，并且可能会返回缓存的响应。 为了匹配，GraphQL请求&#x200B;_必须_&#x200B;完全匹配。 即，查询、操作名称（如果有）、变量（如果有） _必须_&#x200B;都等于缓存的请求。 而且，可能设置为&#x200B;_的所有自定义HTTP标头也必须_&#x200B;相同。 例如，Adobe Commerce `Store`标头&#x200B;_必须_&#x200B;匹配。

### 示例 {#examples}

Adobe建议您为search服务配置一些缓存，以便获取product search和category页上显示的所有可用聚合/彩块化值。 例如，只有在将新属性添加到产品时，这些值才会发生更改。 因此，如果产品属性集不经常更改，则此缓存条目的持续时间可能会“很大”。 虽然此条目特定于项目，但Adobe建议在项目开发阶段使用几分钟的值，在稳定生产系统中使用几小时的值。

此设置通常使用以下缓存条目进行配置：

```
com.adobe.cq.commerce.core.search.services.SearchFilterService:true:10:3600
```

推荐使用GraphQl缓存功能的另一个示例方案是导航组件。 原因是它会在所有页面上发送相同的GraphQL查询。 在这种情况下，缓存条目通常将设置为：

```
venia/components/structure/navigation:true:10:600
```

考虑到已使用[Venia引用存储](https://github.com/adobe/aem-cif-guides-venia)。 请注意，使用了组件代理名称`venia/components/structure/navigation`，而&#x200B;**不是** CIF导航组件的名称(`core/cif/components/structure/navigation/v1/navigation`)。

其他组件的缓存应基于项目定义，通常与在Dispatcher级别配置的缓存协调定义。 请记住，这些缓存没有任何活动失效机制，因此应小心设置缓存持续时间。 没有任何“适合所有”的值能够匹配所有可能的项目和用例。 确保在项目级别定义最符合项目要求的缓存策略。

## Dispatcher缓存 {#dispatcher}

在[AEM Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html)中缓存AEM页面或片段是任何AEM项目的最佳实践。 通常，它依赖于失效技术，以确保在AEM中更改的任何内容在Dispatcher中正确更新。 此功能是AEM Dispatcher缓存策略的核心。

除了纯AEM管理的内容CIF之外，页面通常还可以显示通过GraphQL从Adobe Commerce动态获取的商务数据。 虽然页面结构本身可能永远不会更改，但商业内容可能会更改。 例如，如果产品数据（如名称和价格）在Adobe Commerce中发生更改。

为了确保CIF页面在AEM Dispatcher中缓存的时间有限，Adobe建议在AEM Dispatcher中缓存CIF页面时使用[基于时间的缓存无效](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#configuring-time-based-cache-invalidation-enablettl)（也称为基于TTL的缓存）。 可以使用额外的[ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/)程序包在AEM中配置此功能。

对于基于TTL的缓存，开发人员通常会为选定的AEM页面定义一个或多个缓存持续时间。 此持续时间可确保CIF页面仅在AEM Dispatcher中缓存到配置的持续时间并且内容经常更新。

>[!NOTE]
>
>虽然AEM Dispatcher可能会缓存服务器端数据，但某些CIF组件（如`product`、`productlist`和`searchresults`组件）通常在加载页面时始终在客户端浏览器请求中重新获取产品价格。 这样做可确保始终在页面加载时获取关键的动态内容。

## 其他资源 {#additional}

* [Venia引用存储](https://github.com/adobe/aem-cif-guides-venia)
* [GraphQL缓存配置](https://github.com/adobe/commerce-cif-graphql-client#caching)
* [AEM Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html)
