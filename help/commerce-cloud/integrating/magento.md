---
title: AEM和Adobe Commerce(Magento)集成使用商务集成框架
description: AEM和Adobe Commerce(Magento)可使用商务集成框架(CIF)无缝集成。 CIF允许AEM访问Magento实例，并通过GraphQL与Magento通信。 它还允许AEM作者使用产品和类别选取器以及产品控制台来浏览从Magento中按需获取的产品和类别数据。 此外，CIF还提供开箱即用的店面，可加快商业项目的进度。
thumbnail: aem-magento-architecture.jpg
exl-id: 110ceef5-2c35-4b81-8e89-26929c0da91b,1cdfda88-a728-432f-b24a-f81347572bcf
source-git-commit: 96e7a7c38dd1275c9b0d291d12a0f768ab183c38
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 1%

---

# AEM和Adobe Commerce(Magento)集成使用商务集成框架 {#aem-magento-framework}

Experience Manager和Adobe Commerce(Magento)可使用商务集成框架(CIF)无缝集成。 CIF使AEM能够使用Adobe Commerce的 [GraphQL API](https://devdocs.magento.com/guides/v2.4/graphql/).

>[!NOTE]
>
> 支持的GraphQL API版本最低为2.3.5。某些功能仅在较新版本或仅在Adobe Commerce版本中受支持。

>[!NOTE]
>
>GraphQL当前用于Adobe Experience Manager(AEM)as a Cloud Service的两个（单独）方案：
>
>* 在这种情况下，CIF会通过GraphQL与商务通信。
>* [AEM内容片段可与AEM GraphQL API（一种基于标准GraphQL的自定义实施）一起使用，来提供结构化内容以供在应用程序中使用](/help/assets/content-fragments/graphql-api-content-fragments.md).


## 架构概述 {#overview}

总体架构如下：

![CIF架构概述](../assets/AEM_Magento_Architecture.png)

在CIF中，支持服务器端和客户端通信模式。
服务器端API调用是使用内置的通用API调用来实现的 [GraphQL客户端](https://github.com/adobe/commerce-cif-graphql-client) 与 [生成的数据模型集](https://github.com/adobe/commerce-cif-magento-graphql) （商务GraphQL架构）。 此外，还可以使用GQL格式的任何GraphQL查询或变异。

对于客户端组件，这些组件是使用 [React](https://reactjs.org/), [阿波罗客户](https://www.apollographql.com/docs/react/) 中，将使用。

## AEM CIF核心组件架构 {#cif-core-components}

![AEM CIF核心组件架构](../assets/cif-component-architecture.jpg)

[AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components) 遵循与 [AEM WCM核心组件](https://github.com/adobe/aem-core-wcm-components).

AEM CIF核心组件的业务逻辑和与Adobe Commerce的后端通信在Sling模型中实施。 如果需要自定义此逻辑以满足特定于项目的要求，则可以使用Sling模型的委派模式。

>[!TIP]
>
>的 [自定义AEM CIF核心组件](../customizing/customize-cif-components.md) 页面提供了有关如何自定义CIF核心组件的详细示例和最佳实践。

在项目中，AEM CIF核心组件和自定义项目组件可以通过Sling上下文感知配置，轻松检索与AEM页面关联的Adobe Commerce商店的配置客户端。
