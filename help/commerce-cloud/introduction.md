---
title: 简介和概述
description: 了解不同的店面选项
thumbnail: introducing-aem-commerce.jpg
exl-id: 29410f76-a63f-4b0a-b817-2ed724ad1a3c
feature: Commerce Integration Framework
role: Admin
source-git-commit: 80f1c9548b8b87dc6280e0e95988d84a8376f7ab
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 1%

---


# Content and Commerce {#content-commerce}

随着客户对基于意图的高性能商业体验的期望日益增长，品牌面临着更快交付更多内容的压力，同时不能牺牲质量。 借助Adobe Experience Manager，品牌可以更快地扩展和创新，打造沉浸式商务体验，并获取更多流量和不断增长的在线支出。

Adobe Experience Manager提供了强大的工具来创建和管理内容丰富、个性化的客户体验。 通过将AEM与商业解决方案(如Adobe Commerce、Salesforce Commerce、SAP Commerce Cloud或任何其他解决方案)集成，品牌商可以整合内容和商业，从而跨渠道提供无缝的购物历程。

## 概述店面方法 {#overview}

AEM可以根据您的情况和偏好为您提供支持。 请遵循以下指导选择适合您的方法：

* [使用Edge Delivery Services（推荐）](#edge)
* [使用您自己的店面(headless AEM集成)](#own-storefront)
* [使用AEM CIF店面](#cif)

### 使用Edge Delivery Services（推荐） {#edge}

如果您的企业希望在Web上拥有最快、最适合AI的店面，而您的开发人员希望获得一流的开发人员体验，请使用[Edge Delivery Services。](../edge/overview.md) Edge Delivery Services满足今天和明天的所有要求。 根据我们的后端和解决方案，您有不同的选择：

#### 1.与Adobe Commerce as a Cloud Service集成 {#acaacs}

Adobe建议使用Edge Delivery和[Adobe Commerce店面](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=zh-Hans)作为起点。 店面附带有与Adobe Commerce服务、API预集成的模板，并提供各种Commerce插入组件以快速构建店面。

适合：Adobe Commerce as a Cloud Service的典型店面体验

#### 2.与Adobe Commerce Optimizer集成（适用于任何第三方解决方案） {#aco}

如果要集成现有的商务解决方案并提高目录性能，Adobe建议使用[Adobe Commerce Optimizer](https://experienceleague.adobe.com/zh-hans/docs/commerce-learn/tutorials/adobe-commerce-optimizer/overview)作为现代集成层。 Commerce Optimizer通过用于目录和推销的高性能SaaS服务来增强您的商务解决方案。 与Adobe Commerce as a Cloud Service一样，[Adobe Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=zh-Hans)可与其一起开箱即用。

可与商业商业解决方案(如Salesforce Commerce)集成。 请联系您的Adobe代表。

契合度：现有商务解决方案的典型店面体验

#### 3.自定义集成 {#custom}

如果您要构建自定义集成，Adobe还建议使用Edge Delivery Services 。 您可以从头开始，也可以在Edge Delivery店面中重复使用现有JS-framework商业组件（例如，用于事务性部件）。 这样一来，您的客户将获得无与伦比的超快购物体验，同时您可以重复利用现有投资来增加TTV。 您的起始点是默认的[Edge Delivery样板](https://www.aem.live/developer/tutorial)。

适合：Edge Deliery店面的价值较低

### 使用您自己的店面(Headless AEM集成) {#own-storefront}

您有一个现有的店面（例如，使用React JS构建），并希望使用Adobe Experience Manager进行内容管理和交付（内容片段）、资源以及上下文编辑（通用编辑器）。 集成的起点是[Adobe Experience Manager as a Headless CMS简介](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/headless/introduction)和[CIF加载项](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/content-and-commerce/storefront/authoring/enrich-product-associated-content)。 CIF加载项允许将您的产品数据无缝集成到AEM(在AEM UI中搜索、浏览和查找产品)中，以便用于构建特定于商业的体验。

### AEM CIF店面 {#cif}

Adobe的推荐和参考架构是使用Edge Delivery Services。 CIF店面及其AEM CIF核心组件现在处于维护模式，不应在新项目中使用。 有关参考，请参阅[CIF文档。](/help/commerce-cloud/cif-storefront/introduction.md)

>[!NOTE]
>
>希望利用新AEM/Commerce功能的现有客户应将其网站移动到Edge Delivery。 一种常见模式是，首先仅将一部分页面移动到Edge Delivery并以并排方式运行Edge Deliery和CIF页面。 还可以使用新的[AEM CIF放置组件](https://experienceleague.adobe.com/developer/commerce/storefront/dropins/all/introduction/?lang=zh-Hans)替换Commerce组件，以利用新的Commerce功能。
