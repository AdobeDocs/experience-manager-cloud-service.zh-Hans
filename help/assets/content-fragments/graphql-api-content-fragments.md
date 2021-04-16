---
title: AEM GraphQL API，与内容片段一起使用
description: 了解如何将Adobe Experience Manager(AEM)中的内容片段用作AEM GraphQL API的Cloud Service，实现无外设内容投放。
feature: 内容片段，GraphQL API
exl-id: bdd60e7b-4ab9-4aa5-add9-01c1847f37f6
translation-type: tm+mt
source-git-commit: 1e005f7eace2fa2c40acddc215833606342a9357
workflow-type: tm+mt
source-wordcount: '3257'
ht-degree: 1%

---

# AEM GraphQL API，用于内容片段{#graphql-api-for-use-with-content-fragments}

了解如何将Adobe Experience Manager(AEM)中的内容片段用作AEM GraphQL API的Cloud Service，实现无外设内容投放。

AEM作为Cloud ServiceGraphQL API与内容片段一起使用，这在很大程度上是基于标准的开放源GraphQL API。

使用AEM中的GraphQL API，可以在无外设CMS实施中将内容片段高效投放到JavaScript客户端：

* 避免像REST那样迭代API请求，
* 确保投放仅限于具体要求，
* 允许批量投放渲染所需的具体内容，作为对单个API查询的响应。

>[!NOTE]
>
>GraphQL当前用于Adobe Experience Manager(AEM)中的两个（单独）方案作为Cloud Service:
>
>* [AEM Commerce通过GraphQL从商务平台读取数据](/help/commerce-cloud/integrating/magento.md)。
>* AEM内容片段与AEM GraphQL API（一种基于标准GraphQL的自定义实施）一起提供结构化内容，以便在您的应用程序中使用。


## GraphQL API {#graphql-api}

GraphQL是：

* &quot;*...用于API的查询语言和用于使用现有数据实现这些查询的运行时。 GraphQL提供了对API中数据的完整而易于理解的描述，使客户能够确切地询问他们需要什么，而无需做更多工作，使API随着时间推移更加易于开发，并支持功能强大的开发人员工具。*&quot;。

   请参阅[GraphQL.org](https://graphql.org)

* &quot;*...灵活的API层的开放规范。 将GraphQL置于现有后端之上，以比以往更快的速度构建产品…….*&quot;。

   请参阅[浏览GraphQL](https://www.graphql.com)。

* *&quot;。..一种数据查询语言和规范，由Facebook于2012年在内部开发，后于2015年公开开放采购。它为基于REST的体系结构提供了一种替代方法，目的是提高开发者的工作效率并最大限度地减少数据传输量。 GraphQL由数百个不同规模的组织用于生产……&quot;*

   请参阅[GraphQL Foundation](https://foundation.graphql.org/)。

<!--
"*Explore GraphQL is maintained by the Apollo team. Our goal is to give developers and technical leaders around the world all of the tools they need to understand and adopt GraphQL.*". 
-->

有关GraphQL API的更多信息，请参阅以下部分（以及其他许多资源）：

* 在[graphql.org](https://graphql.org):

   * [GraphQL简介](https://graphql.org/learn)

   * [GraphQL规范](http://spec.graphql.org/)

* 位于[graphql.com](https://graphql.com):

   * [参考线](https://www.graphql.com/guides/)

   * [教程](https://www.graphql.com/tutorials/)

   * [案例研究](https://www.graphql.com/case-studies/)

用于AEM实施的GraphQL基于标准GraphQL Java库。 请参阅：

* [graphQL.org - Java](https://graphql.org/code/#java)

* [GitHub上的GraphQL Java](https://github.com/graphql-java)

### GraphQL术语{#graphql-terminology}

GraphQL使用以下功能：

* **[查询](https://graphql.org/learn/queries/)**

* **[模式和类型](https://graphql.org/learn/schema/)**:

   * 模式由AEM基于内容片段模型生成。
   * GraphQL使用您的模式显示GraphQL for AEM实施允许的类型和操作。

* **[字段](https://graphql.org/learn/queries/#fields)**

* **[GraphQL端点](#graphql-aem-endpoint)**
   * AEM中响应GraphQL查询的路径，提供对GraphQL模式的访问。

   * 有关更多详细信息，请参阅[启用GraphQL Endpoint](#enabling-graphql-endpoint)。

有关详细信息，请参阅[(GraphQL.org)GraphQL](https://graphql.org/learn/)简介，包括[最佳实践](https://graphql.org/learn/best-practices/)。

### GraphQL查询类型{#graphql-query-types}

通过GraphQL，您可以执行查询以返回以下任一项：

* **单个条目**

* **[条目列表](https://graphql.org/learn/schema/#lists-and-non-null)**

<!--
You can also perform:

* [Persisted Queries, that are cached](#persisted-queries-caching)
-->

## AEM Endpoint {#graphql-aem-endpoint}的GraphQL

endpoint是用于访问AEM的GraphQL的路径。 使用此路径，您（或您的应用程序）可以：

* 访问GraphQL模式,
* 发送您的GraphQL查询,
* 接收响应(对您的GraphQL查询)。

GraphQL for AEM端点的存储库路径为：

`/content/cq:graphql/global/endpoint`

您的应用程序可以在请求URL中使用以下路径：

`/content/_cq_graphql/global/endpoint.json`

要为AEM的GraphQL启用端点，您需要：

>[!CAUTION]
>
>这些步骤在不久的将来可能会发生变化。

* [启用GraphQL端点](#enabling-graphql-endpoint)
* [执行其他配置](#additional-configurations-graphql-endpoint)

### 启用GraphQL端点{#enabling-graphql-endpoint}

>[!NOTE]
>
>请参阅[支持包](#supporting-packages)，了解Adobe提供的包的详细信息以帮助简化这些步骤。

要在AEM中启用GraphQL查询，请在`/content/cq:graphql/global/endpoint`处创建一个端点：

* 节点`cq:graphql`和`global`的类型必须为`sling:Folder`。
* 节点`endpoint`必须为`nt:unstructured`类型，并包含`graphql/sites/components/endpoint`的`sling:resourceType`。

>[!CAUTION]
>
>每个人都可以访问该端点。 这可能会引起安全问题，因为GraphQL查询可能会对服务器施加大负载。
>
>您可以在端点上设置与用例相适应的ACL。

>[!NOTE]
>
>您的端点不会开箱即用。 您必须单独提供GraphQL Endpoint](#additional-configurations-graphql-endpoint)的[其他配置。

>[!NOTE]
>此外，您还可以使用[GraphiQL IDE](#graphiql-interface)测试和调试GraphQL查询。

### GraphQL端点{#additional-configurations-graphql-endpoint}的其他配置

>[!NOTE]
>
>请参阅[支持包](#supporting-packages)，了解Adobe提供的包的详细信息以帮助简化这些步骤。

需要其他配置：

* Dispatcher:
   * 允许所需的URL
   * 强制
* 虚 URL:
   * 为端点分配简化的URL
   * 可选

### 支持包{#supporting-packages}

为简化GraphQL端点的设置，Adobe提供[GraphQL示例项目(2021.3)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-graphql/graphql-sample1.zip)包。

此归档文件包含[所需的附加配置](#additional-configurations-graphql-endpoint)和[GraphQL终结点](#enabling-graphql-endpoint)。 如果安装在普通AEM实例上，它将在`/content/cq:graphql/global/endpoint`处公开一个完全工作的GraphQL端点。

此包旨在成为您自己的GraphQL项目的蓝图。 有关如何使用该包的详细信息，请参阅包&#x200B;**README**。

如果您希望手动创建所需的配置，Adobe还提供专用的[GraphQL Endpoint Content Package](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faemcloud%2Fpublic%2Faem-graphql%2Fgraphql-global-endpoint.zip)。 此内容包仅包含GraphQL端点，无任何配置。

## GraphiQL接口{#graphiql-interface}

<!--
AEM Graph API includes an implementation of the standard [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql) interface. This allows you to directly input, and test, queries.
-->

标准[GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql)接口的实现可与AEM GraphQL一起使用。 可以与AEM](#installing-graphiql-interface)一起安装[。

此界面允许您直接输入和测试查询。

例如：

* `http://localhost:4502/content/graphiql.html`

它提供语法高亮显示、自动完成、自动建议等功能，以及历史记录和在线文档：

![GraphiQL接](assets/cfm-graphiql-interface.png "口GraphiQL接口")

### 安装AEM GraphiQL接口{#installing-graphiql-interface}

GraphiQL用户界面可安装在AEM上并包含专用包：[GraphiQL内容包v0.0.6(2021.3)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-graphql/graphiql-0.0.6.zip)包。

<!--
See the package **README** for full details; including full details of how it can be installed on an AEM instance - in a variety of scenarios.
-->

## 创作和发布环境的用例{#use-cases-author-publish-environments}

用例取决于AEM作为Cloud Service环境的类型：

* 发布环境;:
   * 查询JS应用程序数据（标准用例）

* 创作环境;:
   * 查询数据用于“内容管理目的”：
      * AEM中作为Cloud Service的GraphQL当前是只读API。
      * REST API可用于CR(u)D操作。

## 权限 {#permission}

这些权限是访问资产所需的权限。

## 模式生成{#schema-generation}

GraphQL是强类型API，这意味着数据必须按照类型清晰地结构化和组织。

GraphQL规范提供了有关如何创建用于查询特定实例上的数据的强大API的一系列指南。 为此，客户端需要获取[模式](#schema-generation)，其中包含查询所需的所有类型。

对于“内容片段”，GraphQL模式（结构和类型）基于&#x200B;**Enabled** [内容片段模型](/help/assets/content-fragments/content-fragments-models.md)及其数据类型。

>[!CAUTION]
>
>所有GraphQL模式（从&#x200B;**已启用**&#x200B;的内容片段模型派生）均可通过GraphQL端点读取。
>
>这意味着您需要确保没有敏感数据可用，因为这些数据可能会以这种方式泄露；例如，这包括在模型定义中可能作为字段名称显示的信息。

例如，如果用户创建了名为`Article`的内容片段模型，则AEM会生成类型为`ArticleModel`的对象`article`。 此类型中的字段与模型中定义的字段和数据类型相对应。

1. 内容片段模型：

   ![与GraphQLContent片段模型一起使](assets/cfm-graphqlapi-01.png "用的内容片段模型与GraphQL一起使用")

1. 相应的GraphQL模式（从GraphiQL自动文档输出）：
   ![基于内容片段模型的GraphQL模式基](assets/cfm-graphqlapi-02.png "于内容片段模型的GraphQL模式")

   这表明生成的类型`ArticleModel`包含多个[字段](#fields)。

   * 其中三个由用户控制：`author`、`main`和`referencearticle`。

   * 其他字段由AEM自动添加，表示提供特定内容片段相关信息的有用方法；在此示例中，`_path`、`_metadata`、`_variations`。 这些[帮助字段](#helper-fields)标有前面的`_`，以区分用户定义的内容和自动生成的内容。

1. 在用户基于文章模型创建内容片段后，可以通过GraphQL进行询问。 有关示例，请参阅[示例查询](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-sample-queries)（基于[示例内容片段结构，以与GraphQL](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql)一起使用）。

在GraphQL for AEM中，模式是灵活的。 这意味着每次创建、更新或删除内容片段模型时，都会自动生成该片段。 在更新内容片段模型时，数据模式缓存也会刷新。

<!--
>[!NOTE]
>
>AEM does not use the concept of namespacing for Content Fragment Models. 
>
>If required, you can edit the **[GraphQL](/help/assets/content-fragments/content-fragments-models.md#content-fragment-model-properties)** properties of a Model to assign specific names.
-->

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

## 字段 {#fields}

在该模式中，有两个基本类别的单个字段：

* 生成的字段。

   选择[字段类型](#field-types)用于根据您配置内容片段模型的方式创建字段。 字段名称取自&#x200B;**数据类型**&#x200B;的&#x200B;**属性名称**&#x200B;字段。

   * 还有&#x200B;**Render As**&#x200B;属性要考虑，因为用户可以配置某些数据类型；例如，作为单行文本或多字段。

* AEM的GraphQL还生成许多[帮助字段](#helper-fields)。

   它们用于标识内容片段或获取有关内容片段的更多信息。

### 字段类型{#field-types}

GraphQL for AEM支持列表类型。 所有支持的内容片段模型数据类型和相应的GraphQL类型均表示：

| 内容片段模型 — 数据类型 | 图形QL类型 | 描述 |
|--- |--- |--- |
| 单行文本 | 字符串，[字符串] |  用于简单字符串，如作者姓名、位置名称等。 |
| 多行文本 | 字符串 |  用于输出文本，如文章的正文 |
| 数字 |  浮点，[浮点] | 用于显示浮点数和正则数 |
| 布尔型 |  布尔型 |  用于显示复选→框的简单true/false语句 |
| 日期和时间 | 日历 |  用于以ISO 8086格式显示日期和时间 |
| 枚举 |  String |  用于从创建模型时定义的列表选项中显示选项 |
|  标记 |  [String] |  用于显示表示AEM中使用的标记的字符串列表 |
| 内容引用 |  字符串 |  用于在AEM中显示指向另一个资产的路径 |
| 片段引用 |  *模型类型* |  用于引用某个“模型类型”的其他“内容片段”（在创建模型时定义） |

### 帮助字段{#helper-fields}

除了用户生成字段的数据类型外，GraphQL for AEM还生成许多&#x200B;*helper*&#x200B;字段，以帮助识别内容片段或提供有关内容片段的其他信息。

#### 路径 {#path}

路径字段用作GraphQL中的标识符。 它表示AEM存储库内的内容片段资产的路径。 我们选择它作为内容片段的标识符，因为它：

* 在AEM中是独一无二的，
* 很容易被取走。

以下代码将显示基于内容片段模型`Person`创建的所有内容片段的路径。

```xml
{
  personList {
    items {
      _path
    }
  }
}
```

要检索特定类型的单个内容片段，您还需要首先确定其路径。 例如：

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _path
      firstName
      name
    }
  }
}
```

请参阅[示例查询 — 单个特定城市片段](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-single-specific-city-fragment)。

#### 元数据 {#metadata}

通过GraphQL，AEM还公开内容片段的元数据。 元数据是描述内容片段的信息，例如内容片段的标题、缩略图路径、内容片段的描述、创建日期等。

由于元数据是通过模式编辑器生成的，因此没有特定的结构，因此实现了`TypedMetaData` GraphQL类型以公开内容片段的元数据。 `TypedMetaData` 显示按以下标量类型分组的信息：

| 字段 |
|--- |
| `stringMetadata:[StringMetadata]!` |
| `stringArrayMetadata:[StringArrayMetadata]!` |
| `intMetadata:[IntMetadata]!` |
| `intArrayMetadata:[IntArrayMetadata]!` |
| `floatMetadata:[FloatMetadata]!` |
| `floatArrayMetadata:[FloatArrayMetadata]!` |
| `booleanMetadata:[BooleanMetadata]!` |
| `booleanArrayMetadata:[booleanArrayMetadata]!`  |
| `calendarMetadata:[CalendarMetadata]!` |
| `calendarArrayMetadata:[CalendarArrayMetadata]!` |

每个标量类型表示单个名称 — 值对或名称 — 值对数组，其中该对的值是其分组的类型。

例如，如果您要检索内容片段的标题，我们知道此属性是String属性，因此我们将查询所有String Metadata:

要查询元数据：

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _path
      _metadata {
        stringMetadata {
          name
          value
        }
      }
    }
  }
}
```

如果您视图“生成的GraphQL”模式，则可以视图所有元数据GraphQL类型。 所有型号类型具有相同的`TypedMetaData`。

>[!NOTE]
>
>**普通元数据与数组元数据的区别**
>请记住，`StringMetadata`和`StringArrayMetadata`都引用存储库中存储的内容，而不是如何检索它们。
>
>因此，例如，通过调用`stringMetadata`字段，您将收到存储在存储库中的所有元数据的`String`数组，如果调用`stringArrayMetadata`，您将收到存储在存储库中的所有元数据的`String[]`数组。

请参阅[元数据示例查询-列表标题为GB](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-metadata-awards-gb)的奖项的元数据。

#### 变量 {#variations}

`_variations`字段已实现，以简化查询内容片段所具有的变量。 例如：

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _variations
    }
  }
}
```

请参阅[示例查询 — 所有具有命名变量的城市](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-cities-named-variation)。

<!--
## Security Considerations {#security-considerations}
-->

## GraphQL变量{#graphql-variables}

GraphQL允许将变量放置在查询中。 有关详细信息，请参阅GraphiQL](https://graphql.org/learn/queries/#variables)的[GraphQL文档。

例如，要获取具有特定变量的`Article`类型的所有内容片段，可以在GraphiQL中指定变量`variation`。

![GraphQL变](assets/cfm-graphqlapi-03.png "量GraphQL变量")

```xml
### query
query GetArticlesByVariation($variation: String!) {
    articleList(variation: $variation) {
        items {
            _path
            author
        }
    }
}
 
### in query variables
{
    "variation": "uk"
}
```

## GraphQL指令{#graphql-directives}

在GraphQL中，可以根据变量（称为GraphQL指令）更改查询。

例如，您可以根据变量`includePrice`将所有`AdventureModels`的查询包含`adventurePrice`字段。

![GraphQL指](assets/cfm-graphqlapi-04.png "令GraphQL指令")

```xml
### query
query GetAdventureByType($includePrice: Boolean!) {
  adventureList {
    items {
      adventureTitle
      adventurePrice @include(if: $includePrice)
    }
  }
}
 
### in query variables
{
    "includePrice": true
}
```

## 筛选{#filtering}

您还可以在GraphQL查询中使用筛选来返回特定数据。

过滤使用基于逻辑运算符和表达式的语法。

例如，以下（基本）查询过滤器名为`Jobs`或`Smith`的所有人员：

```xml
query {
  personList(filter: {
    name: {
      _logOp: OR
      _expressions: [
        {
          value: "Jobs"
        },
        {
          value: "Smith"
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

有关更多示例，请参阅：

* [用于AEM扩展](#graphql-extensions)的GraphQL的详细信息

* [使用此示例内容和结构的示例查询](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-sample-queries-sample-content-fragment-structure)

   * 和准备用于样本查询的[样本内容和结构](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql)

* [基于WKND项目的示例查询](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-queries-using-wknd-project)

## GraphQL for AEM — 扩展{#graphql-extensions}摘要

使用GraphQL for AEM的查询的基本操作符合标准的GraphQL规范。 对于具有AEM的GraphQL查询，有以下几个扩展：

* 如果您需要一个结果：
   * 使用模型名称；eg city

* 如果您希望获得一列表结果：
   * 将`List`添加到模型名称；例如，`cityList`
   * 请参阅[示例查询 — 所有城市相关信息](#sample-all-information-all-cities)

* 如果要使用逻辑OR:
   * 使用` _logOp: OR`
   * 请参阅[示例查询 — 名称为“Jobs”或“Smith”](#sample-all-persons-jobs-smith)的所有人员

* 逻辑AND也存在，但是是（通常）隐式的

* 您可以查询与内容片段模型中的字段相对应的字段名称
   * 请参阅[示例查询-公司CEO和员工的完整详细信息](#sample-full-details-company-ceos-employees)

* 除了模型中的字段之外，还有一些系统生成的字段（前面有下划线）：

   * 对于内容：

      * `_locale` :去揭示语言；基于语言管理器
         * 请参阅[给定区域设置的多个内容片段的示例查询](#sample-wknd-multiple-fragments-given-locale)
      * `_metadata` :显示片段的元数据
         * 请参阅[元数据示例查询-列表标题为GB](#sample-metadata-awards-gb)的奖项的元数据
      * `_model` :允许查询内容片段模型（路径和标题）
         * 请参阅[模型](#sample-wknd-content-fragment-model-from-model)中内容片段模型的示例查询
      * `_path` :存储库中内容片段的路径
         * 请参阅[示例查询 — 单个特定城市片段](#sample-single-specific-city-fragment)
      * `_reference` :显示引用；包括富文本编辑器中的内联引用
         * 请参阅[具有预取引用的多个内容片段的示例查询](#sample-wknd-multiple-fragments-prefetched-references)
      * `_variation` :以显示内容片段中的特定变量
         * 请参阅[示例查询 — 具有命名变量的所有城市](#sample-cities-named-variation)
   * 操作：

      * `_operator` :应用特定的经营者； `EQUALS`,  `EQUALS_NOT`,  `GREATER_EQUAL`,  `LOWER`,  `CONTAINS`,  `STARTS_WITH`
         * 请参阅[示例查询 — 所有姓名不为“Jobs”](#sample-all-persons-not-jobs)的人员
         * 请参阅[示例查询 — 所有Adventures，其中`_path`开始具有特定前缀](#sample-wknd-all-adventures-cycling-path-filter)
      * `_apply` :（二）适用特定条件；例如，   `AT_LEAST_ONCE`
         * 请参阅[示例查询 — 对包含项目的数组进行筛选，该项目必须至少发生一次](#sample-array-item-occur-at-least-once)
      * `_ignoreCase` :在查询时忽略大小写
         * 请参阅[示例查询 — 名称中包含SAN的所有城市，而不考虑大小写](#sample-all-cities-san-ignore-case)










* 支持GraphQL合并类型：

   * 使用`... on`
      * 请参阅[具有内容引用的特定模型的内容片段的示例查询](#sample-wknd-fragment-specific-model-content-reference)

<!--
## Persisted Queries (Caching) {#persisted-queries-caching}

After preparing a query with a POST request, it can be executed with a GET request that can be cached by HTTP caches or a CDN.

This is required as POST queries are usually not cached, and if using GET with the query as a parameter there is a significant risk of the parameter becoming too large for HTTP services and intermediates.

Here are the steps required to persist a given query:

>[!NOTE]
>Prior to this the **GraphQL Persistence Queries** need to be enabled, for the appropriate configuration. See [Enable Content Fragment Functionality in Configuration Browser](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser) for more details.

1. Prepare the query by PUTing it to the new endpoint URL `/graphql/persist.json/<config>/<persisted-label>`.

   For example, create a persisted query:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query" \
       -d \
   '{
     articleList {
       items{
           _path
           author
           main {
               json
           }
       }
     }
   }'
   ```

1. At this point, check the response.

   For example, check for success:

     ```xml
     {
       "action": "create",
       "configurationName": "wknd",
       "name": "plain-article-query",
       "shortPath": "/wknd/plain-article-query",
       "path": "/conf/wknd/settings/graphql/persistentQueries/plain-article-query"
     }
     ```

1. You can then replay the persisted query by GETing the URL `/graphql/execute.json/<shortPath>`.

   For example, use the persisted query:

   ```xml
   $ curl -X GET \
       http://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. Update a persisted query by POSTing to an already existing query path.

   For example, use the persisted query:

   ```xml
   $ curl -X POST \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query" \
       -d \
   '{
     articleList {
       items{
           _path
           author
           main {
               json
           }
         referencearticle {
           _path
         }
       }
     }
   }'
   ```

1. Create a wrapped plain query.

   For example:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-wrapped" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }"}'
   ```

1. Create a wrapped plain query with cache control.

   For example:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
   ```

1. Create a persisted query with parameters:

   For example:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-parameters" \
       -d \
   'query GetAsGraphqlModelTestByPath($apath: String!, $withReference: Boolean = true) {
     articleByPath(_path: $apath) {
       item {
         _path
           author
           main {
           plaintext
           }
           referencearticle @include(if: $withReference) {
           _path
           }
         }
       }
     }'
   ```

1. Executing a query with parameters.

   For example:

   ```xml
   $ curl -X POST \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"

   $ curl -X GET \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   ```

1. To execute the query on publish, the related persist tree need to replicated

   * Using a POST for replication:

     ```xml
     $curl -X POST   http://localhost:4502/bin/replicate.json \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -F path=/conf/wknd/settings/graphql/persistentQueries/plain-article-query \
       -F cmd=activate
     ```

   * Using a package:
     1. Create a new package definition.
     1. Include the configuration (for example, `/conf/wknd/settings/graphql/persistentQueries`).
     1. Build the package.
     1. Replicate the package.

   * Using replication/distribution tool.
     1. Go to the Distribution tool.
     1. Select tree activation for the configuration (for example, `/conf/wknd/settings/graphql/persistentQueries`).

   * Using a workflow (via workflow launcher configuration):
     1. Define a workflow launcher rule for executing a workflow model that would replicate the configuration on different events (for example, create, modify, amongst others).

1. Once the query configuration is on publish, the same principles apply, just using the publish endpoint.

   >[!NOTE]
   >
   >For anonymous access the system assumes that the ACL allows "everyone" to have access to the query configuration.
   >
   >If that is not the case it will not be able to execute.

   >[!NOTE]
   >
   >Any semicolons (";") in the URLs need to be encoded.
   >
   >For example, as in the request to Execute a persisted query:
   >
   >```xml
   >curl -X GET \ "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters%3bapath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   >```
-->

## 从外部网站{#query-graphql-endpoint-from-external-website}查询GraphQL端点

要从外部网站访问GraphQL端点，您需要配置：

* [CORS过滤器](#cors-filter)
* [推荐人过滤器](#referrer-filter)

### CORS过滤器{#cors-filter}

>[!NOTE]
>
>有关AEM中CORS资源共享策略的详细概述，请参阅[了解跨来源资源共享(CORS)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=en#understand-cross-origin-resource-sharing-(cors))。

要访问GraphQL端点，必须在客户Git存储库中配置CORS策略。 为此，可为所需端点添加适当的OSGi CORS配置文件。

此配置必须指定必须授予访问权限的受信任的网站来源`alloworigin`或`alloworiginregexp`。

<!--
For example, to grant access to the GraphQL endpoint and persisted queries endpoint for `https://my.domain` you can use:
-->

例如，要授予对`https://my.domain`的GraphQL端点的访问权限，可以使用：

<!--
```xml
{
  "supportscredentials":true,
  "supportedmethods":[
    "GET",
    "HEAD",
    "POST"
  ],
  "exposedheaders":[
    ""
  ],
  "alloworigin":[
    "https://my.domain"
  ],
  "maxage:Integer":1800,
  "alloworiginregexp":[
    ""
  ],
  "supportedheaders":[
    "Origin",
    "Accept",
    "X-Requested-With",
    "Content-Type",
    "Access-Control-Request-Method",
    "Access-Control-Request-Headers"
  ],
  "allowedpaths":[
    "/content/_cq_graphql/global/endpoint.json",
    "/graphql/execute.json/.*"
  ]
}
```
-->

```xml
{
  "supportscredentials":true,
  "supportedmethods":[
    "GET",
    "HEAD",
    "POST"
  ],
  "exposedheaders":[
    ""
  ],
  "alloworigin":[
    "https://my.domain"
  ],
  "maxage:Integer":1800,
  "alloworiginregexp":[
    ""
  ],
  "supportedheaders":[
    "Origin",
    "Accept",
    "X-Requested-With",
    "Content-Type",
    "Access-Control-Request-Method",
    "Access-Control-Request-Headers"
  ],
  "allowedpaths":[
    "/content/_cq_graphql/global/endpoint.json"
  ]
}
```

如果已配置端点的虚路径，则还可在`allowedpaths`中使用它。

### 推荐人过滤器{#referrer-filter}

除了CORS配置之外，还必须配置推荐人过滤器以允许从第三方主机访问。

通过添加相应的OSGi推荐人过滤器配置文件来完成此操作，该配置文件：

* 指定受信任的网站主机名；`allow.hosts`或`allow.hosts.regexp`,
* 授予对此主机名的访问权限。

例如，要授予推荐人`my.domain`的请求访问权限，您可以：

```xml
{
    "allow.empty":false,
    "allow.hosts":[
      "my.domain"
    ],
    "allow.hosts.regexp":[
      ""
    ],
    "filter.methods":[
      "POST",
      "PUT",
      "DELETE",
      "COPY",
      "MOVE"
    ],
    "exclude.agents.regexp":[
      ""
    ]
}
```

>[!CAUTION]
>
>客户仍有责任：
>
>* 仅授予对受信任域的访问权限
>* 确保没有暴露任何敏感信息
>* 不使用通配符[*]语法；这既将禁用对GraphQL端点的经过身份验证的访问，也会将其呈现给全世界。


>[!CAUTION]
>
>所有GraphQL [模式](#schema-generation)（派生自&#x200B;**已启用**&#x200B;的内容片段模型）均可通过GraphQL端点读取。
>
>这意味着您需要确保没有敏感数据可用，因为这些数据可能会以这种方式泄露；例如，这包括在模型定义中可能作为字段名称显示的信息。

## 身份验证 {#authentication}

请参阅[内容片段上的远程AEM GraphQL查询身份验证](/help/assets/content-fragments/graphql-authentication-content-fragments.md)。

<!-- to be addressed later -->

<!--
## Sorting {#sorting}
-->

<!-- to be addressed later -->

<!--
## Paging {#paging}
-->

## 常见问题解答{#faqs}

出现的问题：

1. **问**:“*AEM的GraphQL API与查询 Builder API有何不同？*”

   * **答**:“AEM *GraphQL API优惠对JSON输出的完全控制，是查询内容的行业标准。展望未来， AEM计划投资于AEM GraphQL API。*&quot;

## 教程 — AEM无外设和GraphQL {#tutorial}快速入门

正在寻找实践教程？ 查看[无外设和GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html)入门教程，该教程说明了如何在无外设CMS场景中使用AEM GraphQL API构建和公开内容并由外部应用程序使用。
