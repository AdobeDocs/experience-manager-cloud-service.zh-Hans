---
title: AEM与Adobe商务(Magento)集成使用商务集成框架
description: AEM和Adobe商务(Magento)可使用商务集成框架(CIF)无缝集成。 CIF允许AEM访问Magento实例，并通过GraphQL与Magento通信。 它还允许AEM作者使用产品和类别选取器以及产品控制台来浏览从Magento中按需获取的产品和类别数据。 此外，CIF还提供开箱即用的店面，可加快商业项目的进度。
thumbnail: aem-magento-architecture.jpg
exl-id: 110ceef5-2c35-4b81-8e89-26929c0da91b,1cdfda88-a728-432f-b24a-f81347572bcf
source-git-commit: ef4abc74b90da80bfe556306f8ac93078b4958c7
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 1%

---

# AEM与Adobe商务(Magento)集成使用商务集成框架{#aem-magento-framework}

Experience Manager和Adobe商务(Magento)可使用商务集成框架(CIF)无缝集成。 CIF允许AEM使用Adobe商务的[GraphQL API](https://devdocs.magento.com/guides/v2.4/graphql/)直接访问通用实例并与之通信。

>[!NOTE]
>
>GraphQL当前用于Adobe Experience Manager(AEM)中的两个（单独）方案作为Cloud Service:
>
>* 在这种情况下，CIF会通过GraphQL与商务通信。
>* [AEM内容片段可与AEM GraphQL API（一种基于标准GraphQL的自定义实施）一起使用，来提供结构化内容以供在应用程序中使用](/help/assets/content-fragments/graphql-api-content-fragments.md)。


## 架构概述 {#overview}

总体架构如下：

![CIF架构概述](../assets/AEM_Magento_Architecture.png)

在CIF中，支持服务器端和客户端通信模式。
服务器端API调用使用内置的通用[GraphQL客户端](https://github.com/adobe/commerce-cif-graphql-client)与商务GraphQL模式的[一组生成的数据模型](https://github.com/adobe/commerce-cif-magento-graphql)组合来实现。此外，还可以使用GQL格式的任何GraphQL查询或变异。

对于使用[React](https://reactjs.org/)构建的客户端组件，使用[Apollo Client](https://www.apollographql.com/docs/react/)。

## AEM CIF核心组件架构{#cif-core-components}

![AEM CIF核心组件架构](../assets/cif-component-architecture.jpg)

[AEM CIF核心组](https://github.com/adobe/aem-core-cif-components) 件遵循与AEM WCM核心组件非常相似的设计模 [式和最佳实践](https://github.com/adobe/aem-core-wcm-components)。

AEM CIF核心组件的业务逻辑和与Adobe商务的后端通信在Sling模型中实施。 如果需要自定义此逻辑以满足特定于项目的要求，则可以使用Sling模型的委派模式。

>[!TIP]
>
>[自定义AEM CIF核心组件](../customizing/customize-cif-components.md)页面提供了有关如何自定义CIF核心组件的详细示例和最佳实践。

在项目中，AEM CIF核心组件和自定义项目组件可以通过Sling上下文感知配置，轻松检索与AEM页面关联的Adobe商务商店的配置客户端。
