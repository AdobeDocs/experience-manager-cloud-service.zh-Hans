---
title: 如何通过AEM 投放 API访问您的内容
description: 在AEM无外设开发人员历程的这一部分中，了解如何使用GraphQL查询访问您的内容片段内容。
hide: true
hidefromtoc: true
index: false
exl-id: 5ef557ff-e299-4910-bf8c-81c5154ea03f
translation-type: tm+mt
source-git-commit: d21d5a496d4a82dd569e582b5b7d7425bd50077f
workflow-type: tm+mt
source-wordcount: '2155'
ht-degree: 1%

---

# 如何通过AEM 投放 API {#access-your-content}访问您的内容

>[!CAUTION]
>
>正在进行中的工作 — 此文档的创建正在进行中，不应理解为完整或明确，也不应将其用于生产目的。

在[AEM无头开发人员历程](overview.md)的这一部分中，您可以学习如何使用GraphQL查询访问内容片段的内容并将其提供给您的应用程序(无头投放)。

## 迄今为止的故事{#story-so-far}

在AEM无头旅程的上一个文档中，[如何为您的内容建模](model-your-content.md)您学习了AEM中内容建模的基础知识，因此您现在应该了解如何对您的内容结构建模，然后使用AEM内容片段模型和内容片段实现该结构：

* 识别与内容建模相关的概念和术语。
* 了解为何需要内容建模来实现无头内容投放。
* 了解如何使用AEM内容片段模型（以及使用内容片段创作内容）实现此结构。
* 了解如何对您的内容进行建模；基本样本的原则。

本文以这些基础知识为基础，因此您可以了解如何使用AEM GraphQL API在AEM中访问现有无外设内容。

* **受众**:初学者
* **目标**:了解如何使用AEM GraphQL查询访问内容片段的内容：
   * 介绍GraphQL和AEM GraphQL API。
   * 深入了解AEM GraphQL API的详细信息。
   * 查看一些示例查询，了解实际操作情况。

## 您想访问您的内容？{#so-youd-like-to-access-your-content}

所以……您已经拥有了所有这些内容，整洁地构建（在内容片段中），并且只是在等待您的新应用程序。 问题是，如何实现它？

您需要的是一种目标特定内容、选择所需内容并将其返回到应用程序以进一步处理的方法。

以Adobe Experience Manager(AEM)为Cloud Service，您可以使用AEM GraphQL API选择性地访问内容片段，以仅返回所需的内容。 这意味着您可以实现结构化内容的无外设投放，以便在应用程序中使用。

>[!NOTE]
>
>AEM GraphQL API是基于标准GraphQL API规范的自定义实施。

## GraphQL — 简介{#graphql-introduction}

GraphQL是一个开放源代码规范，它提供：

* 一种查询语言，允许您从结构化对象中选择特定内容。
* 一个运行时，用于使结构化内容实现这些查询。

GraphQL是&#x200B;*strongly*&#x200B;类型API。 这意味着&#x200B;*所有*&#x200B;内容必须按照类型清晰地结构化和组织，这样GraphQL *才能了解*&#x200B;要访问的内容和访问方式。 数据字段在GraphQL模式中定义，GraphQL定义内容对象的结构。

然后，GraphQL端点提供响应GraphQL查询的路径。

所有这些意味着您的应用程序能够准确、可靠、高效地选择所需内容 — 这正是您与AEM一起使用时需要的内容。

>[!NOTE]
>
>请参阅&#x200B;*GraphQL*.org和&#x200B;*GraphQL*.com。

## AEM和GraphQL {#aem-graphql}

GraphQL用于AEM中的不同位置；例如：

* 内容片段
   * 已为此用例开发自定义API(将无外设投放到您的应用程序)。
      * 这是AEM GraphQL API。
* 商务
   * AEM Commerce通过GraphQL从商务平台读取数据。
   * AEM与各种第三方商务解决方案之间都有GraphQL集成，这些解决方案与CIF核心组件提供的扩展挂钩一起使用。
      * 这不使用AEM GraphQL API。

>[!NOTE]
>
>此无头历程步骤仅涉及AEM GraphQL API和内容片段。

## AEM GraphQL API {#aem-graphql-api}

AEM GraphQL API是基于标准GraphQL API规范的自定义版本，专门配置为允许您对内容片段执行（复杂）查询。

使用内容片段，因为内容是根据内容片段模型构建的。 这满足了GraphQL的基本要求。

* 内容片段模型由一个或多个字段组成。
   * 每个字段都根据数据类型定义。
* 内容片段模型用于生成相应的AEM GraphQL模式。

要实际访问GraphQL for AEM（和内容），使用端点提供访问路径。

通过AEM GraphQL API返回的内容随后便可供应用程序使用。

>[!NOTE]
>
>AEM GraphQL API实现基于GraphQL Java库。

### 创作和发布环境的用例{#use-cases-author-publish-environments}

AEM GraphQL API的用例取决于AEM作为Cloud Service环境的类型：

* 发布环境;:
   * 查询JS应用程序内容（标准用例）

* 创作环境;:
   * 查询内容用于“内容管理目的”：
      * AEM中作为Cloud Service的GraphQL当前是只读API。
      * REST API可用于CR(u)D操作。

## 用于AEM GraphQL API {#content-fragments-use-with-aem-graphql-api}的内容片段

内容片段可用作AEM模式和查询的GraphQL的基础，如：

* 它们使您能够设计、创建、管理和发布独立于页面的内容。
* 它们基于内容片段模型，该模型通过定义的数据类型预定义生成片段的结构。
* 可使用“片段引用”数据类型实现其他结构层，在定义模型时可用。

### 内容片段模型 {#content-fragments-models}

以下内容片段模型：

* 用于生成模式，只需&#x200B;**Enabled**&#x200B;一次。

* 提供GraphQL所需的数据类型和字段。 它们确保您的应用程序仅请求可能的内容，并接收预期内容。

* 数据类型&#x200B;**片段引用**&#x200B;可在模型中用于引用其他内容片段，因此引入其他结构级别。

### 片段引用{#fragment-references}

**片段引用**:

* 是定义内容片段模型时可用的特定数据类型。

* 引用另一个片段，具体取决于特定的内容片段模型。

* 允许您创建结构化数据，然后进行检索。

   * 当定义为&#x200B;**multifeed**&#x200B;时，主片段可以引用（检索）多个子片段。

### JSON预览{#json-preview}

要帮助设计和开发内容片段模型，您可以在内容片段编辑器中预览JSON输出。

## 从内容片段{#graphql-schema-generation-content-fragments}生成GraphQL模式

GraphQL是强类型API，这意味着内容必须按照类型清晰地结构化和组织。 GraphQL规范提供了有关如何创建用于查询特定实例上的内容的强大API的一系列指南。 为此，客户端需要获取模式，其中包含查询所需的所有类型。

对于内容片段，GraphQL模式（结构和类型）基于&#x200B;**已启用**&#x200B;内容片段模型及其数据类型。

>[!CAUTION]
>
>所有GraphQL模式（从&#x200B;**已启用**&#x200B;的内容片段模型派生）均可通过GraphQL端点读取。
>
>这意味着您需要确保没有可用的敏感内容，以确保没有通过GraphQL端点公开敏感数据；例如，这包括在模型定义中可能作为字段名称显示的信息。

例如，如果用户创建了名为`Article`的内容片段模型，则AEM会生成类型为`ArticleModel`的对象`article`。 此类型中的字段与模型中定义的字段和数据类型相对应。

1. 内容片段模型：

   ![与GraphQLContent片段模型一起使](assets/graphqlapi-cfmodel.png "用的内容片段模型与GraphQL一起使用")

1. 相应的GraphQL模式（从GraphiQL自动文档输出）：
   ![基于内容片段模型的GraphQL模式基](assets/graphqlapi-cfm-schema.png "于内容片段模型的GraphQL模式")

   这表明生成的类型`ArticleModel`包含多个[字段](#fields)。

   * 其中三个由用户控制：`author`、`main`和`referencearticle`。

   * 其他字段由AEM自动添加，表示提供特定内容片段相关信息的有用方法；在此示例中，`_path`、`_metadata`、`_variations`。 这些[帮助字段](#helper-fields)标有前面的`_`，以区分用户定义的内容和自动生成的内容。

1. 在用户基于文章模型创建内容片段后，可以通过GraphQL进行询问。 有关示例，请参阅示例查询。md#graphql-sample-查询)(基于与GraphQL一起使用的示例内容片段结构。

在GraphQL for AEM中，模式是灵活的。 这意味着每次创建、更新或删除内容片段模型时，都会自动生成该片段。 在更新内容片段模型时，数据模式缓存也会刷新。

站点图形QL服务监听（在后台）对内容片段模型所做的任何修改。 检测到更新时，只会重新生成模式的该部分。 这种优化节省了时间并提供了稳定性。

例如，如果：

1. 安装包含`Content-Fragment-Model-1`和`Content-Fragment-Model-2`:

   1. 将生成`Model-1`和`Model-2`的GraphQL类型。

1. 然后修改`Content-Fragment-Model-2`:

   1. 只有`Model-2` GraphQL类型会更新。

   1. 而`Model-1`将保持不变。

>[!NOTE]
>
>当您希望通过REST api或以其他方式对内容片段模型进行批量更新时，请务必注意这一点。

模式通过与GraphQL查询相同的端点进行服务，客户端处理以扩展名`GQLschema`调用模式的事实。 例如，对`/content/cq:graphql/global/endpoint.GQLschema`执行简单的`GET`请求将导致输出具有Content-type的模式:`text/x-graphql-schema;charset=iso-8859-1`。

### 模式生成 — 未发布的模型{#schema-generation-unpublished-models}

嵌套内容片段时，父内容片段模型可能已发布，但引用的模型不会发布。

>[!NOTE]
>
>AEM UI可防止这种情况发生，但如果以编程方式或通过内容包进行发布，则可能会发生这种情况。

发生这种情况时，AEM会为父内容片段模型生成&#x200B;*不完整*&#x200B;模式。 这意味着从模式中删除依赖于未发布的模型的片段引用。

## AEM GraphQL端点{#aem-graphql-endpoints}

<!--
need details/examples
-->

端点是用于访问AEM的GraphQL的路径。 使用此路径，您（或您的应用程序）可以：

* 访问GraphQL模式,
* 发送您的GraphQL查询,
* 接收响应(对您的GraphQL查询)。

AEM允许：

* 全局端点 — 可供所有站点使用。
* 租户端点 — 您可以配置的，特定于指定的站点/项目。

## 权限 {#permissions}

这些权限是访问资产所需的权限。

## AEM GraphiQL接口{#aem-graphiql-interface}

为了帮助您直接输入和测试查询，可以与AEM GraphQL一起使用标准GraphiQL界面的实现。 这可以与AEM一起安装。

它提供语法高亮显示、自动完成、自动建议等功能，以及历史记录和在线文档。

![GraphiQL接](assets/graphiql-interface.png "口GraphiQL接口")

## 实际使用AEM GraphQL API {#actually-using-aem-graphiql}

在开始查询您的内容之前，您需要：

* 启用您的端点
   * 使用工具 — >站点 — > GraphQL

* 安装GraphiQL（如果需要）
   * 作为专用包安装

要在查询中实际使用AEM GraphQL API，我们可以使用两个非常基本的内容片段模型结构：

* 公司
   * 名称
   * 首席执行官（人）
   * 员工（人员）
* 人员
   * 名称
   * 名字

如您所见，CEO和Employees字段引用“人员”片段。

将使用片段模型：

* 在内容片段编辑器中创建内容时
* 生成要查询的GraphQL模式

这些查询可以在GraphiQL界面中输入，例如：

* `http://localhost:4502/content/graphiql.html `

直接的查询是返回公司模式中所有条目的名称。 在此处，您请求列表所有公司名：

```xml
query {
  companyList {
    items {
      name
    }
  }
}
```

一个稍微更复杂的查询是选择所有没有&quot;工作&quot;名称的人。 这将过滤所有未命名为Jobs的人员。 这是通过EQUALS_NOT运算符实现的（还有更多）：

```xml
query {
  personList(filter: {
    name: {
      _expressions: [
        {
          value: "Jobs"
          _operator: EQUALS_NOT
        }
      ]
    }
  }) {
    items {
      name
      firstName
    }
  }
}
```

您还可以构建更复杂的查询。 例如，查询至少有一个名为“Smith”的员工的所有公司。 此查询说明了对名为“Smith”的任何人的筛选，从嵌套片段返回信息：

```xml
query {
  companyList(filter: {
    employees: {
      _match: {
        name: {
          _expressions: [
            {
              value: "Smith"
            }
          ]
        }
      }
    }
  }) {
    items {
      name
      ceo {
        name
        firstName
      }
      employees {
        name
        firstName
      }
    }
  }
}
```

<!-- need code / curl / cli examples-->

有关使用AEM GraphQL API的完整详细信息，以及配置必需的元素，您可以参考：

* 了解如何将GraphQL与AEM结合使用
* 示例内容片段结构
* 了解如何将GraphQL与AEM结合使用 — 示例内容和查询

## 下一步是什么{#whats-next}

现在，您已经学习了如何使用AEM GraphQL API访问和查询您的无外设内容，现在您可以[了解如何使用REST API访问和更新您的内容片段](/help/implementing/developing/headless-journey/update-your-content.md)的内容。

## 其他资源 {#additional-resources}

* [GraphQL.org](https://graphql.org)
   * [架构](https://graphql.org/learn/schema/)
   * [变量](https://graphql.org/learn/queries/#variables)
   * [GraphQL Java库](https://graphql.org/code/#java)
* [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql)
* [了解如何将GraphQL与AEM结合使用](/help/assets/content-fragments/graphql-api-content-fragments.md)
   * [启用GraphQL端点](/help/assets/content-fragments/graphql-api-content-fragments.md#enabling-graphql-endpoint)
   * [安装AEM GraphQL界面](/help/assets/content-fragments/graphql-api-content-fragments.md#installing-graphiql-interface)
* [示例内容片段结构](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql)
* [了解如何将GraphQL与AEM结合使用 — 示例内容和查询](/help/assets/content-fragments/content-fragments-graphql-samples.md)
   * [示例查询 — 单个特定城市片段](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-single-specific-city-fragment)
   * [元数据查询示例 — 列表标题为GB的奖项的元数据](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-metadata-awards-gb)
   * [示例查询 — 所有具有已命名变量的城市](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-cities-named-variation)
* [在配置浏览器中启用内容片段功能](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)
* [使用内容片段](/help/assets/content-fragments/content-fragments.md)
   * [内容片段模型](/help/assets/content-fragments/content-fragments-models.md)
   * [JSON输出](/help/assets/content-fragments/content-fragments-json-preview.md)
* [了解跨来源资源共享(CORS)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=en#understand-cross-origin-resource-sharing-(cors))
* [为服务器端API生成访问令牌](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)
* [AEM无头入门](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html)  — 一个简短的视频教程系列概述了如何使用AEM无头功能，包括内容建模和GraphQL。
