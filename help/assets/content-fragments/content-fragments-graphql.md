---
title: 使用内容片段和GraphQL的无头内容投放
description: 了解如何将Adobe Experience Manager(AEM)中的内容片段用作GraphQL的Cloud Service，以实现无头内容投放。
translation-type: tm+mt
source-git-commit: da8fcf1288482d406657876b5d4c00b413461b21
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 0%

---


# 使用内容片段和GraphQL {#headless-content-delivery-using-content-fragments-with-graphQL}的无头内容投放

>[!CAUTION]
>
>AEM GraphQL API for Content Fragments投放可应请求提供。
>
>请联系[Adobe支持](https://experienceleague.adobe.com/?lang=en&amp;support-solution=General#support)，为AEM启用API作为Cloud Service项目。

以Adobe Experience Manager(AEM)为Cloud Service，您可以将内容片段与AEM GraphQL API（一种基于标准GraphQL的自定义实施）结合使用，以交付结构化内容以用于您的应用程序。

## 无外设CMS {#headless-cms}

无外设内容管理系统(CMS)是：

* &quot;*无外设内容管理系统或无外设CMS是从头开始构建的仅后端内容管理系统(CMS)，它是内容存储库，可通过API访问内容以在任何设备上显示。*

   *术语“无头”源于从“正文”（后端，即内容存储库）截断“头”（前端，即网站）的概念*。

   请参阅[Wikipedia](https://en.wikipedia.org/wiki/Headless_content_management_system)。

在AEM中创作内容片段时，这意味着：

* 您可以使用内容片段创作并非主要用于在格式化的页面上直接发布(1:1)的内容。

* 内容片段的内容将按照预定方式进行结构化——根据内容片段模型。 这简化了应用程序的访问，从而进一步处理您的内容。

>[!NOTE]
>
>有关AEM Sites作为Cloud Service的无头开发的简介，请参见[无头和AEM](/help/implementing/developing/headless/introduction.md)。

## GraphQL —— 概述{#graphql-overview}

GraphQL是：

* &quot;*...用于API的查询语言和用于利用现有数据实现这些查询的运行时。 GraphQL提供了API中数据的完整且可理解的描述，使客户能够确切地询问他们需要什么，而无需更多，使API随着时间推移更易于开发，并支持功能强大的开发人员工具。*&quot;

   请参阅[GraphQL.org](https://graphql.org)

* &quot;*...灵活的API层的开放规范。 将GraphQL放在现有后端，以前所未有的速度构建产品…….*&quot;。

   请参阅[浏览GraphQL](https://www.graphql.com)。 &quot;*Explore GraphQL由Apollo团队维护。 我们的目标是为全球的开发人员和技术领导者提供他们需要了解和采用GraphQL的所有工具。*”。

[AEM GraphQL API](#aem-graphql-api)允许您对[内容片段](/help/assets/content-fragments/content-fragments.md)执行（复杂）查询;每个查询都根据特定的模型类型。 返回的内容随后可供应用程序使用。

### GraphQL术语{#graphql-terminology}

GraphQL使用以下内容：

* **[查询](https://graphql.org/learn/queries/)**

* **[模式和类型](https://graphql.org/learn/schema/)** -使用这些，GraphQL显示GraphQL for AEM实现允许的类型和操作。

* **[字段](https://graphql.org/learn/queries/#fields)**

* **GraphQL端点** - AEM中响应GraphQL查询的路径，提供对GraphQL模式的访问。

有关详细信息，请参阅[(GraphQL.org)GraphQL](https://graphql.org/learn/)简介，包括[最佳实践](https://graphql.org/learn/best-practices/)。

### GraphQL查询类型{#graphql-query-types}

通过GraphQL，您可以执行以下任一查询:

* **单项**

* **[条目列表](https://graphql.org/learn/schema/#lists-and-non-null)**

## AEM GraphQL API {#aem-graphql-api}

对于[Adobe Experience作为云体验，已实施标准GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md)的自定义实施。

AEM GraphQL API实现基于[GraphQL Java库](https://graphql.org/code/#java)。

## 与AEM GraphQL API {#content-fragments-use-with-aem-graphql-api}一起使用的内容片段

[内](#content-fragments) 容片段可用作AEM查询的GraphQL的基础，如下：

* 它们使您能够设计、创建、策划和发布独立于页面的内容。
* [内容片段模型](#content-fragments-models)通过定义的数据类型提供所需的结构。
* 定义模型时可用的[片段引用](#fragment-references)可用于定义其他结构层。

![与GraphQLContent片段一](assets/cfm-nested-01.png "起使用的内容片段与GraphQL一起使用")

### 内容片段 {#content-fragments}

内容片段:

* 包含结构化内容。

* 它们基于[内容片段模型](#content-fragments-models)，该模型预定义生成片段的结构。

### 内容片段模型 {#content-fragments-models}

以下[内容片段模型](/help/assets/content-fragments/content-fragments-models.md):

* 提供GraphQL所需的数据类型和字段。 它们确保您的应用程序仅请求可能的内容并接收预期内容。

* 数据类型&#x200B;**[片段引用](#fragment-references)**&#x200B;可用于模型中引用其他内容片段，因此引入其他级别的结构。

### 片段引用{#fragment-references}

**[片段引用](/help/assets/content-fragments/content-fragments-models.md#fragment-reference-nested-fragments)**:

* 与GraphQL结合使用尤其受关注。

* 是一种特定数据类型，可在定义内容片段模型时使用。

* 引用另一个片段，具体取决于特定内容片段模型。

* 允许您检索结构化数据。

   * 当定义为&#x200B;**multifeed**&#x200B;时，多个子片段可由原始片段引用（检索）。

### JSON预览{#json-preview}

要帮助设计和开发内容片段模式，您可以预览[JSON输出](/help/assets/content-fragments/content-fragments-json-preview.md)。

## 学习将GraphQL与AEM结合使用——示例内容和查询{#learn-graphql-with-aem-sample-content-queries}

有关使用AEM GraphQL API的介绍，请参阅[学习将GraphQL与AEM一起使用——示例内容和查询](/help/assets/content-fragments/content-fragments-graphql-samples.md)。

## 教程- AEM无头和GraphQL入门

正在寻找实践教程？ 查看[AEM无外设和GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html)端到端教程入门，该教程说明了如何在无外设CMS场景中使用AEM的GraphQL API构建和公开内容并由外部应用程序使用。