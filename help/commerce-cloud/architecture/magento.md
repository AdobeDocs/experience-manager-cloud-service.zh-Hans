---
title: AEM和Magento集成（使用Commerce Integration Framework）
description: AEM和Magento通过商务集成框架(CIF)无缝集成。 CIF使AEM能够访问Magento实例并通过GraphQL与Magento通信。 它还允许AEM作者使用产品和类别选择器以及产品控制台浏览从Magento按需获取的产品和类别数据。 此外，CIF还提供开箱即用的店面，可以加快商业项目。
thumbnail: aem-magento-architecture.jpg
translation-type: tm+mt
source-git-commit: 72d98c21a3c02b98bd2474843b36f499e8d75a03
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---


# AEM和Magento集成（使用Commerce Integration Framework {#aem-magento-framework}）

AEM和Magento通过商务集成框架(CIF)无缝集成。 CIF使AEM能够访问Magento实例并通过GraphQL与Magento通信。 它还允许AEM作者使用产品和类别选择器以及产品控制台浏览从Magento按需获取的产品和类别数据。 此外，CIF还提供开箱即用的店面，可以加快商业项目。

## 架构概述{#overview}

总体架构如下：

![CIF架构概述](../assets/AEM_Magento_Architecture.JPG)

CIF基于GraphQL支持。 AEM与Magento之间的主要通信渠道是Magento的[GraphQL API](https://devdocs.magento.com/guides/v2.4/graphql/) API。 有不同的方法将AEM配置为Cloud Service和Magento之间的通信，有关详细信息，请参阅[快速入门](../getting-started.md)页。

在CIF中，支持服务器端和客户端通信模式。
服务器端API调用是使用内置的通用[GraphQL客户端](https://github.com/adobe/commerce-cif-graphql-client)与用于MagentoGraphQL模式的[一组生成的数据模型](https://github.com/adobe/commerce-cif-magento-graphql)来实现的。 此外，还可以使用GQL格式的任何GraphQL查询或变异。

对于使用[React](https://reactjs.org/)构建的客户端组件，使用[Apollo客户端](https://www.apollographql.com/docs/react/)。

## AEM CIF核心组件架构{#cif-core-components}

![AEM CIF核心组件架构](../assets/cif-component-architecture.jpg)

[AEM CIF核心组](https://github.com/adobe/aem-core-cif-components) 件遵循与AEM WCM核心组件非常相似的设计 [模式和最佳实践](https://github.com/adobe/aem-core-wcm-components)。

AEM CIF核心组件的业务逻辑和与Magento的后端通信在Sling模型中实现。 如果需要自定义此逻辑以满足特定于项目的要求，则可以使用Sling模型的委托模式。

>[!TIP]
>
>[自定义AEM CIF核心组件](../customizing/customize-cif-components.md)页有一个详细的示例和关于如何自定义CIF核心组件的最佳实践。

在项目中，AEM CIF核心组件和自定义项目组件可以通过Sling上下文感知配置轻松检索与AEM页面关联的Magento存储的已配置客户端。
