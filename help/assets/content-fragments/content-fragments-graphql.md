---
title: 使用内容片段和GraphQL的无外设内容投放
description: 了解如何将AEM内容片段与GraphQL结合使用，实现无外设内容投放。
feature: 内容片段
role: 商务从业人员
translation-type: tm+mt
source-git-commit: 6fa911f39d707687e453de270bc0f3ece208d380
workflow-type: tm+mt
source-wordcount: '720'
ht-degree: 1%

---


# 使用内容片段和GraphQL {#headless-content-delivery-using-content-fragments-with-graphQL}的无标题内容投放

以Adobe Experience Manager(AEM)为Cloud Service，您可以将内容片段与AEM GraphQL API（一种基于标准GraphQL的自定义实现）结合使用，无拘无束地交付结构化内容以用于您的应用程序。 自定义单个API查询的功能允许您检索和提供您想要/需要渲染的特定内容(作为对单个API查询的响应)。

>[!NOTE]
>
>有关将AEM Sites作为Cloud Service的无头开发的简介，请参阅[无头和AEM](/help/implementing/developing/headless/introduction.md)。

>[!NOTE]
>
>GraphQL当前用于Adobe Experience Manager(AEM)中的两个（单独）方案作为Cloud Service:
>
>* [AEM Commerce通过GraphQL从商务平台中消耗数据](/help/commerce-cloud/architecture/magento.md)。
>* [AEM内容片段与AEM GraphQL API（一种基于标准GraphQL的自定义实施）一起提供结构化内容，以便在您的应用程序中使用](/help/assets/content-fragments/graphql-api-content-fragments.md)。


## 无外设CMS {#headless-cms}

无外设内容管理系统(CMS)是：

* &quot;*无外设内容管理系统或无外设CMS是从头开始构建的仅后端内容管理系统(CMS)，它是一个内容存储库，可通过API访问内容以在任何设备上显示。*

   请参阅[Wikipedia](https://en.wikipedia.org/wiki/Headless_content_management_system)。

就在AEM中创作内容片段而言，这意味着：

* 您可以使用内容片段创作并非主要用于在格式化页面上直接发布(1:1)的内容。

* 内容片段的内容将按照预先确定的方式 — 根据内容片段模型。 这简化了应用程序的访问，应用程序将进一步处理您的内容。

## GraphQL — 概述{#graphql-overview}

GraphQL是：

* &quot;*...用于API的查询语言和用于使用现有数据实现这些查询的运行时。*&quot;。

   请参阅[GraphQL.org](https://graphql.org)

[AEM GraphQL API](#aem-graphql-api)允许您对[内容片段](/help/assets/content-fragments/content-fragments.md)执行（复杂）查询;每个查询都根据特定的模型类型。 返回的内容随后可供应用程序使用。

## AEM GraphQL API {#aem-graphql-api}

对于Adobe Experience a Cloud Experience，已开发标准GraphQL API的自定义实施。 有关详细信息，请参阅[AEM GraphQL API以与内容片段](/help/assets/content-fragments/graphql-api-content-fragments.md)一起使用。

AEM GraphQL API实现基于[GraphQL Java库](https://graphql.org/code/#java)。

## 用于AEM GraphQL API {#content-fragments-use-with-aem-graphql-api}的内容片段

[内](#content-fragments) 容片段可用作AEM查询的GraphQL的基础：

* 它们使您能够设计、创建、管理和发布独立于页面的内容。
* [内容片段模型](#content-fragments-models)通过定义的数据类型提供所需的结构。
* 定义模型时可用的[片段引用](#fragment-references)可用于定义其他结构层。

![与GraphQLContent片段一起使](assets/cfm-nested-01.png "用的内容片段与GraphQL一起使用")

### 内容片段 {#content-fragments}

内容片段:

* 包含结构化内容。

* 它们基于[内容片段模型](#content-fragments-models)，该模型预定义生成片段的结构。

### 内容片段模型 {#content-fragments-models}

以下[内容片段模型](/help/assets/content-fragments/content-fragments-models.md):

* 用于生成[模式](https://graphql.org/learn/schema/)，一次&#x200B;**启用**。

* 提供GraphQL所需的数据类型和字段。 它们确保您的应用程序仅请求可能的内容，并接收预期内容。

* 数据类型&#x200B;**[片段引用](#fragment-references)**&#x200B;可在模型中用于引用其他内容片段，因此引入其他结构级别。

### 片段引用{#fragment-references}

**[片段引用](/help/assets/content-fragments/content-fragments-models.md#fragment-reference-nested-fragments)**:

* 与GraphQL结合使用时特别感兴趣。

* 是在定义内容片段模型时可以使用的特定数据类型。

* 引用另一个片段，具体取决于特定的内容片段模型。

* 允许您检索结构化数据。

   * 当定义为&#x200B;**multifeed**&#x200B;时，主片段可以引用（检索）多个子片段。

### JSON预览{#json-preview}

要帮助设计和开发内容片段模型，您可以预览[JSON输出](/help/assets/content-fragments/content-fragments-json-preview.md)。

## 了解如何将GraphQL与AEM一起使用 — 示例内容和查询{#learn-graphql-with-aem-sample-content-queries}

有关使用AEM GraphQL API的介绍，请参阅[学习将GraphQL与AEM一起使用 — 示例内容和查询](/help/assets/content-fragments/content-fragments-graphql-samples.md)。

## 教程 — AEM无外设和GraphQL入门

正在寻找实践教程？ 查看[无外设和GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html)入门教程，该教程说明了如何在无外设CMS场景中使用AEM GraphQL API构建和公开内容并由外部应用程序使用。