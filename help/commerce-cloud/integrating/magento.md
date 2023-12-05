---
title: 使用Commerce integration framework集成AEM和Adobe Commerce
description: 使用Commerce integration framework(CIF)可无缝集成AEM和Adobe Commerce。 CIF使AEM能够访问Adobe Commerce实例，并通过GraphQL与Adobe Commerce通信。 它还允许AEM作者使用产品和类别选取器以及产品控制台来浏览从Adobe Commerce按需获取的产品和类别数据。 此外，CIF提供了一个开箱即用的店面，可以加快商业项目的执行。
thumbnail: aem-magento-architecture.jpg
exl-id: 110ceef5-2c35-4b81-8e89-26929c0da91b
source-git-commit: 6d63328ca17a00e0369c57714409f3f448cb311f
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 10%

---

# 使用Commerce integration framework集成AEM和Adobe Commerce {#aem-framework}

使用Commerce integration framework(CIF)可无缝集成Experience Manager和Adobe Commerce。 CIF使AEM能够使用Adobe Commerce直接访问商务实例并与之通信 [GRAPHQL API](https://devdocs.magento.com/guides/v2.4/graphql/).

>[!NOTE]
>
> 支持的最低GraphQL API版本为2.3.5。仅在较新版本或仅在Adobe Commerce版本中支持某些功能。

>[!NOTE]
>
>GraphQL 当前用于 Adobe Experience Manager (AEM) as a Cloud Service 中的两种（分隔的）场景：
>
>* 在此方案中，CIF通过GraphQL与commerce进行通信。
>* [AEM 内容片段与 AEM GraphQL API（一种自定义实现，基于标准 GraphQL）配合使用，提供结构化内容用于您的应用程序](/help/headless/graphql-api/content-fragments.md)。

## 架构概述 {#overview}

整体架构如下：

![CIF架构概述](../assets/AEM_Magento_Architecture.png)

在CIF中，支持服务器端和客户端通信模式。
服务器端API调用是使用内置的通用规则实现的 [GraphQL客户端](https://github.com/adobe/commerce-cif-graphql-client) 与 [生成的数据模型集](https://github.com/adobe/commerce-cif-magento-graphql) 商业的GraphQL架构。 此外，还可以使用GQL格式的任何GraphQL查询或突变。

对于客户端组件，使用构建 [React](https://reactjs.org/)， [Apollo客户端](https://www.apollographql.com/docs/react/) 已使用。

## AEM CIF核心组件架构 {#cif-core-components}

![AEM CIF核心组件架构](../assets/cif-component-architecture.jpg)

[AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components) 遵循与非常相似的设计模式和最佳实践 [AEM WCM核心组件](https://github.com/adobe/aem-core-wcm-components).

在Sling模型中实现与AEM CIF核心组件的Adobe Commerce的业务逻辑和后端通信。 如果必须自定义此逻辑以满足项目特定的要求，可以使用Sling模型的委托模式。

>[!TIP]
>
>此 [自定义AEM CIF核心组件](../customizing/customize-cif-components.md) 页面提供了有关如何自定义CIF核心组件的详细示例和最佳实践。

在项目中，AEM CIF核心组件和自定义项目组件可以通过Sling上下文感知配置，轻松检索与AEM页面关联的Adobe Commerce应用商店的配置客户端。

## 搜索 {#search}

CIF提供开箱即用的 [搜索核心组件](https://www.aemcomponents.dev/content/core-components-examples/library/commerce/search.html) 即服务器端渲染的搜索体验，基于 [Commerce GraphQL API](https://developer.adobe.com/commerce/webapi/graphql/). Commerce客户可以选择使用 [实时搜索](https://experienceleague.adobe.com/docs/commerce-merchant-services/live-search/guide-overview.html?lang=en) 而是。 关注此 [链接](/help/commerce-cloud/integrating/live-search-plp.md) 详细了解CIF - Live Search集成。

