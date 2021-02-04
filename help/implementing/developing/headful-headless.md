---
title: AEM中的头和头
description: AEM项目可以采用带有头和无头的模型，但选择不是二进制的。 AEM优惠在一个项目中灵活地利用两种模型的优点。
translation-type: tm+mt
source-git-commit: 772717b7ad3baa17a58e251c128663035eb89931
workflow-type: tm+mt
source-wordcount: '1009'
ht-degree: 0%

---


# AEM{#headful-headless}中的头和头

Adobe Experience Manager项目可以采用头戴式和无头戴式两种模式，但选择不是二元的。 AEM优惠在一个项目中灵活地利用两种模型的优点。 本文档提供并概述了不同的模型，并描述了SPA集成的各个级别。

## 概述 {#overview}

AEM优惠了强大的工具来管理内容的创建及其在一个平台中的投放。 这是一种传统的“强大”内容管理模型，内容作者和开发人员在同一平台上工作，为内容消费者提供体验。

AEM还可用于简单地管理内容，允许由其他平台管理内容的演示和投放。 这是“无头”内容管理模型，内容作者和开发人员在不同的平台上工作，为内容消费者提供体验。

但这不一定是二进制的选择。 AEM优惠具有前所未有的灵活性，让您能够充分利用两种模型在项目中的优势。

![AEM实施模型](headless/assets/aem-implementation-models.png)

在头型或全堆栈模型中，内容基于Java、HTL等在AEM存储库和AEM组件中进行管理。 用于为用户体验渲染内容。 在此模型中，创建内容、设置内容样式、展示内容并交付所有内容均在AEM中完成。

在无外设模型中，内容在AEM存储库中进行管理，但通过REST和GraphQL等API交付到另一个系统，以呈现用户体验的内容。 在此模型中，内容是在AEM中创建的，但样式设置、展示和交付都在其他平台上完成。

单页应用程序(SPA)通常是AEM直接交付内容的目标。 但是，这些SPA并不完全是AEM的外部。 AEM允许您决定SPA集成到AEM的程度。 让我们举个例子。

## Web Shop示例{#web-shop-example}

假设您现有作为SPA的公司的Web商店。 其中包含您的所有产品详细信息和图像。 然后引入AEM，以支持您的营销工作，如促销站点、博客和活动内容。 您如何将二者整合在一起？ AEM支持一系列选项：

* **允许系统独立运行。**
* **通过GraphQL从AEM提供内容有限的Web商店。** 内容可由作者在AEM中创建，但只能通过Web商店SPA查看。
* **将Web商店SPA嵌入AEM。** 内容可由作者在AEM中创建，并在AEM的Web商店环境中查看，但不能进行操作。
* **将Web商店SPA嵌入AEM，并启用可编辑点。** 内容可由作者在AEM中创建，并在AEM中在Web商店的上下文中查看，而作者在AEM中操作Web商店SPA的内容的能力有限。
* **在AEM中嵌入网页商店SPA，并启用整个区域进行编辑。** 内容可由作者在AEM中创建，并在AEM中在Web商店的上下文中查看，而作者在AEM中操作Web商店SPA的内容的能力有限。

下一节将更详细地研究这些集成级别。

>[!NOTE]
>
>当然，您也可以使用AEM SPA Editor框架将Web shop SPA重新实施为完全功能的SPA [。](/help/implementing/developing/hybrid/introduction.md) 如果您已经拥有AEM并希望创建新的Web商店或其他SPA，则建议使用这种方法，但它不在此文档的范围内。

## SPA集成级别{#integration-levels}

SPA的集成在AEM中属于四个级别。

* **0级：无集成**
   * SPA和AEM单独存在，不交换任何信息。
   * 内容是在两个独立的系统中独立创建、管理和交付的。
* **级别1:内容片段集成**
   * [内](/help/assets/content-fragments/content-fragments.md) 容片段用于AEM以创建和管理SPA的有限内容。
   * SPA通过AEM [GraphQL API检索此内容。](/help/assets/content-fragments/graphql-api-content-fragments.md)
   * 某些内容在AEM中管理，有些在外部系统中管理。
   * 内容只能在SPA中查看。
* **级别2:将SPA嵌入AEM**
   * [内](/help/assets/content-fragments/content-fragments.md) 容片段用于AEM创建和管理SPA的内容。
   * SPA通过AEM [GraphQL API检索此内容。](/help/assets/content-fragments/graphql-api-content-fragments.md)
   * 某些内容在AEM中管理，有些在外部系统中管理。
   * 内容可在AEM内的上下文中查看。
   * 有限内容可在AEM内进行编辑。
* **第3级：在AEM中嵌入并完全启用SPA**
   * [内](/help/assets/content-fragments/content-fragments.md) 容片段用于AEM创建和管理SPA的内容。
   * SPA通过AEM [GraphQL API检索此内容。](/help/assets/content-fragments/graphql-api-content-fragments.md)
   * 内容可在AEM内的上下文中查看。
   * 大多数内容都可在AEM内进行编辑。

1级是典型无头实施的示例。 但是，内容作者只能在SPA中视图其上下文内容。 AEM只是一个创作工具。

AEM的优势和灵活性在级别2和级别3中变得显而易见，同时仍保留SPA的优势。 内容作者可以在AEM中创建其内容，但也可以在AEM中在上下文中查看它。 SPA具有在AEM中创作的能力，但仍以SPA的身份提供。

## 实施集成级别{#implementing}

AEM中有不同的工具可用，具体取决于您选择的集成级别。 每个级别都构建于之前使用的工具之上。 以下列表链接到相关资源。

* **级别1：内** 容片段和AEM [无头](/help/implementing/developing/headless/introduction.md) 框架可用于将AEM内容交付到SPA。
* **第2级：** 除第1级之外：
   * [RemotePage组](/help/implementing/developing/hybrid/remote-page.md) 件可用于将外部SPA嵌入AEM中，以便在上下文中查看AEM内容。
   * SPA上的某些点也可以启用到[允许在AEM中进行有限的编辑。](/help/implementing/developing/hybrid/editing-external-spa.md)
* **第3级：** 除第2级之外：
   * 可以启用SPA的整个区域以在AEM中进行全面编辑。
