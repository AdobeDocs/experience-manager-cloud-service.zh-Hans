---
title: 使用Commerce Integration Framework集成AEM和Adobe Commerce
description: AEM和Adobe Commerce使用Commerce Integration Framework (CIF)无缝集成。 CIF允许AEM访问Adobe Commerce实例，并通过GraphQL与Adobe Commerce通信。 它还允许AEM作者使用产品和类别选取器以及产品控制台浏览从Adobe Commerce按需获取的产品和类别数据。 此外，CIF提供了一个现成的店面，可以加快商业项目的执行。
thumbnail: aem-magento-architecture.jpg
exl-id: 110ceef5-2c35-4b81-8e89-26929c0da91b,1cdfda88-a728-432f-b24a-f81347572bcf
source-git-commit: e304b49b44cf871f3c47120fad7899407c573234
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 12%

---

# 使用Commerce Integration Framework集成AEM和Adobe Commerce {#aem-framework}

使用Commerce Integration Framework (CIF)无缝集成Experience Manager和Adobe Commerce。 CIF使AEM能够使用Adobe Commerce直接访问商务实例并与之通信 [GRAPHQL API](https://devdocs.magento.com/guides/v2.4/graphql/).

>[!NOTE]
>
> 支持的最低GraphQL API版本为2.3.5。仅较新版本或仅在Adobe Commerce版本中支持某些功能。

>[!NOTE]
>
>GraphQL 当前用于 Adobe Experience Manager (AEM) as a Cloud Service 中的两种（分隔的）场景：
>
>* 在此方案中，CIF通过GraphQL与Commerce通信。
>* [AEM 内容片段与 AEM GraphQL API（一种自定义实现，基于标准 GraphQL）配合使用，提供结构化内容用于您的应用程序](/help/headless/graphql-api/content-fragments.md)。


## 架构概述 {#overview}

整体架构如下：

![CIF架构概述](../assets/AEM_Magento_Architecture.png)

在CIF中，支持服务器端和客户端通信模式。
服务器端API调用是使用内置的通用方法实现的 [GraphQL客户端](https://github.com/adobe/commerce-cif-graphql-client) 与 [生成的数据模型集](https://github.com/adobe/commerce-cif-magento-graphql) 用于商务GraphQL架构。 此外，还可以使用GQL格式的任何GraphQL查询或变异。

对于客户端组件，使用构建 [React](https://reactjs.org/)，则 [Apollo客户端](https://www.apollographql.com/docs/react/) 已使用。

## AEM CIF核心组件架构 {#cif-core-components}

![AEM CIF核心组件架构](../assets/cif-component-architecture.jpg)

[AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components) 遵循与非常相似的设计模式和最佳实践 [AEM WCM核心组件](https://github.com/adobe/aem-core-wcm-components).

在Sling模型中实现了用于AEM CIF核心组件的业务逻辑和与Adobe Commerce的后端通信。 如果需要自定义此逻辑以满足项目特定的要求，可以使用Sling模型的委托模式。

>[!TIP]
>
>此 [自定义AEM CIF核心组件](../customizing/customize-cif-components.md) 页面提供了有关如何自定义CIF核心组件的详细示例和最佳实践。

在项目中，AEM CIF核心组件和自定义项目组件可以通过Sling上下文感知配置，轻松检索与AEM页面关联的Adobe Commerce商店的配置客户端。
