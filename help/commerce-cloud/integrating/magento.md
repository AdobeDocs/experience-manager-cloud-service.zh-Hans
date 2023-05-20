---
title: 使用Commerce Integration Framework整合AEM和Adobe Commerce
description: 使用Commerce Integration Framework (CIF)將AEM和Adobe Commerce緊密整合。 CIF可讓AEM存取Adobe Commerce執行個體，並透過GraphQL與Adobe Commerce通訊。 它也可讓AEM作者使用產品和類別選擇器及產品主控台，瀏覽從Adobe Commerce隨選擷取的產品和類別資料。 此外，CIF提供立即可用的店面，可加速商業專案。
thumbnail: aem-magento-architecture.jpg
exl-id: 110ceef5-2c35-4b81-8e89-26929c0da91b,1cdfda88-a728-432f-b24a-f81347572bcf
source-git-commit: e304b49b44cf871f3c47120fad7899407c573234
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 12%

---

# 使用Commerce Integration Framework整合AEM和Adobe Commerce {#aem-framework}

使用Commerce Integration Framework (CIF)將Experience Manager和Adobe Commerce緊密整合。 CIF可讓AEM使用Adobe Commerce直接存取商業執行個體並與之通訊 [GRAPHQL API](https://devdocs.magento.com/guides/v2.4/graphql/).

>[!NOTE]
>
> 支援的最低GraphQL API版本為2.3.5。只有較新版本或Adobe Commerce版本才支援某些功能。

>[!NOTE]
>
>GraphQL 当前用于 Adobe Experience Manager (AEM) as a Cloud Service 中的两种（分隔的）场景：
>
>* 此情境中，CIF透過GraphQL與商務通訊。
>* [AEM 内容片段与 AEM GraphQL API（一种自定义实现，基于标准 GraphQL）配合使用，提供结构化内容用于您的应用程序](/help/headless/graphql-api/content-fragments.md)。


## 架构概述 {#overview}

整體架構如下：

![CIF架構概述](../assets/AEM_Magento_Architecture.png)

在CIF中，支援伺服器端和使用者端通訊模式。
伺服器端API呼叫是使用內建的一般來實作 [GraphQL使用者端](https://github.com/adobe/commerce-cif-graphql-client) 搭配 [一組產生的資料模型](https://github.com/adobe/commerce-cif-magento-graphql) 適用於商務GraphQL結構描述。 此外，您也可以使用GQL格式的任何GraphQL查詢或變異。

對於使用者端元件，使用建置 [React](https://reactjs.org/)，則 [Apollo使用者端](https://www.apollographql.com/docs/react/) 已使用。

## AEM CIF核心元件架構 {#cif-core-components}

![AEM CIF核心元件架構](../assets/cif-component-architecture.jpg)

[AEM CIF Core Components](https://github.com/adobe/aem-core-cif-components) 遵循非常類似的設計模式和最佳實務作為 [AEM WCM Core Components](https://github.com/adobe/aem-core-wcm-components).

在Sling模型中實作用於AEM CIF核心元件的商業邏輯和與Adobe Commerce的後端通訊。 如果需要自訂此邏輯以滿足專案特定的要求，可以使用Sling模型的委派模式。

>[!TIP]
>
>此 [自訂AEM CIF核心元件](../customizing/customize-cif-components.md) 頁面提供如何自訂CIF核心元件的詳細範例和最佳實務。

在專案中，AEM CIF核心元件和自訂專案元件可透過Sling內容感知設定，輕鬆擷取與AEM頁面相關聯之Adobe Commerce商店的已設定使用者端。
