---
title: AEM GraphQL API，用于内容片段
description: 了解如何将Adobe Experience Manager(AEM)中的内容片段用作AEM GraphQL API的Cloud Service，用于无头内容投放。
translation-type: tm+mt
source-git-commit: 47ed0f516b724c4d9a966bd051a022f322acb08e
workflow-type: tm+mt
source-wordcount: '3192'
ht-degree: 1%

---


# AEM GraphQL API，用于内容片段{#graphql-api-for-use-with-content-fragments}

Adobe Experience Manager作为Cloud Service(AEM) GraphQL API与内容片段一起使用，它在很大程度上基于标准的开放源GraphQL API。

在AEM中使用GraphQL API，在无外设CMS实现中，可以将内容片段高效投放到JavaScript客户端：

* 避免像REST一样重复的API请求，
* 确保投放仅限于具体要求，
* 允许批量投放渲染所需的具体内容，作为对单个API查询的响应。

## GraphQL API {#graphql-api}

GraphQL是：

* &quot;*...用于API的查询语言和用于利用现有数据实现这些查询的运行时。 GraphQL提供了API中数据的完整且可理解的描述，使客户能够确切地询问他们需要什么，而无需更多，使API随着时间推移更易于开发，并支持功能强大的开发人员工具。*&quot;

   请参阅[GraphQL.org](https://graphql.org)

* &quot;*...灵活的API层的开放规范。 将GraphQL放在现有后端，以前所未有的速度构建产品…….*&quot;。

   请参阅[浏览GraphQL](https://www.graphql.com)。

* *“...数据查询语言和规范，由Facebook于2012年在内部开发，后于2015年公开开发。它为基于REST的体系结构提供了一种替代方法，目的是提高开发者的工作效率并最大限度地减少数据传输量。 GraphQL由数百个不同规模的组织在生产中使用……&quot;*

   请参阅[GraphQL Foundation](https://foundation.graphql.org/)。

<!--
"*Explore GraphQL is maintained by the Apollo team. Our goal is to give developers and technical leaders around the world all of the tools they need to understand and adopt GraphQL.*". 
-->

有关GraphQL API的详细信息，请参阅以下各节（以及其他许多资源）:

* 在[graphql.org](https://graphql.org):

   * [GraphQL简介](https://graphql.org/learn)

   * [GraphQL规范](http://spec.graphql.org/)

* 位于[graphql.com](https://graphql.com):

   * [参考线](https://www.graphql.com/guides/)

   * [教程](https://www.graphql.com/tutorials/)

   * [案例研究](https://www.graphql.com/case-studies/)

GraphQL for AEM实现基于标准GraphQL Java库。 请参阅：

* [graphQL.org - Java](https://graphql.org/code/#java)

* [GitHub上的GraphQL Java](https://github.com/graphql-java)

### GraphQL术语{#graphql-terminology}

GraphQL使用以下内容：

* **[查询](https://graphql.org/learn/queries/)**

* **[模式和类型](https://graphql.org/learn/schema/)**:

   * 模式由AEM根据内容片段模型生成。
   * GraphQL使用您的模式显示GraphQL for AEM实现允许的类型和操作。

* **[字段](https://graphql.org/learn/queries/#fields)**

* **[GraphQL端点](#graphql-aem-endpoint)**
   * AEM中响应GraphQL查询的路径，并提供对GraphQL模式的访问。

   * 有关更多详细信息，请参阅[启用GraphQL Endpoint](#enabling-graphql-endpoint)。

有关详细信息，请参阅[(GraphQL.org)GraphQL](https://graphql.org/learn/)简介，包括[最佳实践](https://graphql.org/learn/best-practices/)。

### GraphQL查询类型{#graphql-query-types}

通过GraphQL，您可以执行查询以返回：

* A **单个条目**

* **[条目列表](https://graphql.org/learn/schema/#lists-and-non-null)**

您还可以执行：

* [已缓存的保留查询](#persisted-queries-caching)

## AEM端点{#graphql-aem-endpoint}的GraphQL

端点是用于访问AEM的GraphQL的路径。 使用此路径，您（或您的应用程序）可以：

* 访问GraphQL模式,
* 发送您的GraphQL查询,
* 接收响应(对您的GraphQL查询)。

AEM端点的GraphQL的存储库路径为：

`/content/cq:graphql/global/endpoint`

您的应用程序可以在请求URL中使用以下路径：

`/content/_cq_graphql/global/endpoint.json`

要为AEM启用GraphQL的端点，您需要：

>[!CAUTION]
>
>这些步骤在不久的将来可能会发生变化。

* [启用GraphQL端点](#enabling-graphql-endpoint)
* [执行其他配置](#additional-configurations-graphql-endpoint)

### 启用GraphQL端点{#enabling-graphql-endpoint}

>[!NOTE]
>
>请参阅[支持包](#supporting-packages)，了解Adobe提供的包的详细信息，以帮助简化这些步骤。

要在AEM中启用GraphQL查询，请在`/content/cq:graphql/global/endpoint`处创建一个端点：

* 节点`cq:graphql`和`global`的类型必须为`sling:Folder`。
* 节点`endpoint`的类型必须为`nt:unstructured`，并且包含`graphql/sites/components/endpoint`的`sling:resourceType`。

>[!CAUTION]
>
>当前端点存在已知问题：
>
>* 条目`cq:graphql`显示在&#x200B;**站点**控制台中；在顶层。
   >  不得使用。


>[!CAUTION]
>
>每个人都可以访问该端点。 这可能会引起安全问题，因为GraphQL查询可能会给服务器带来沉重负载。
>
>您可以在端点上设置与用例相应的ACL。

>[!NOTE]
>
>您的终结点将无法开箱即用。 您必须单独提供GraphQL Endpoint](#additional-configurations-graphql-endpoint)的[其他配置。

>[!NOTE]
>此外，您还可以使用[GraphiQL IDE](#graphiql-interface)测试和调试GraphQL查询。

### GraphQL端点{#additional-configurations-graphql-endpoint}的其他配置

>[!NOTE]
>
>请参阅[支持包](#supporting-packages)，了解Adobe提供的包的详细信息，以帮助简化这些步骤。

需要其他配置：

* Dispatcher:
   * 允许所需的URL
   * 强制
* 虚 URL:
   * 为端点分配简化的URL
   * 可选
* OSGi配置：
   * GraphQL Servlet配置：
      * 处理对端点的请求
      * 配置名称为`org.apache.sling.graphql.core.GraphQLServlet`。 它需要作为OSGi工厂配置提供
      * `sling.servlet.extensions` 必须设置为  `[json]`
      * `sling.servlet.methods` 必须设置为  `[GET,POST]`
      * `sling.servlet.resourceTypes` 必须设置为  `[graphql/sites/components/endpoint]`
      * 强制
   * 模式Servlet配置：
      * 创建GraphQL模式
      * 配置名称为`com.adobe.aem.graphql.sites.adapters.SlingSchemaServlet`。 它需要作为OSGi工厂配置提供
      * `sling.servlet.extensions` 必须设置为  `[GQLschema]`
      * `sling.servlet.methods` 必须设置为  `[GET]`
      * `sling.servlet.resourceTypes` 必须设置为  `[graphql/sites/components/endpoint]`
      * 强制
   * CSRF配置：
      * 端点的安全保护
      * 配置名称为`com.adobe.granite.csrf.impl.CSRFFilter`
      * 将`/content/cq:graphql/global/endpoint`添加到已排除路径的现有列表(`filter.excluded.paths`)
      * 强制

### 支持包{#supporting-packages}

为简化GraphQL端点的设置，Adobe提供[GraphQL示例项目](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faemcloud%2Fpublic%2Faem-graphql%2Fgraphql-sample.zip)包。

此归档文件同时包含[所需的附加配置](#additional-configurations-graphql-endpoint)和[GraphQL端点](#enabling-graphql-endpoint)。 如果安装在普通AEM实例上，它将在`/content/cq:graphql/global/endpoint`处显示一个完全工作的GraphQL端点。

此包旨在成为您自己的GraphQL项目的蓝图。 有关如何使用软件包的详细信息，请参阅软件包&#x200B;**README**。

如果您希望手动创建所需的配置，Adobe还提供专用的[GraphQL Endpoint Content Package](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faemcloud%2Fpublic%2Faem-graphql%2Fgraphql-global-endpoint.zip)。 此内容包仅包含GraphQL端点，无任何配置。

## GraphiQL接口{#graphiql-interface}

<!--
AEM Graph API includes an implementation of the standard [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql) interface. This allows you to directly input, and test, queries.
-->

标准[GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql)接口的实现可与AEM GraphQL一起使用。 可以与AEM](#installing-graphiql-interface)一起安装[。

此界面允许您直接输入和测试查询。

例如：

* `http://localhost:4502/content/graphiql.html`

它提供语法高亮显示、自动完成、自动建议等功能以及历史记录和在线文档：

![GraphiQL接](assets/cfm-graphiql-interface.png "口GraphiQL接口")

### 安装AEM GraphiQL接口{#installing-graphiql-interface}

GraphiQL用户界面可以安装在AEM上并包含专用包：[GraphiQL内容包v0.0.4](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faemcloud%2Fpublic%2Faem-graphql%2Fgraphiql-0.0.4.zip)包。

有关完整的详细信息，请参见软件包&#x200B;**README**;包括在各种情况下如何在AEM实例上安装它的完整详细信息。

## 创作和发布环境的用例{#use-cases-author-publish-environments}

用例取决于AEM的类型，即Cloud Service环境:

* 发布环境;用于：
   * 查询JS应用程序数据（标准用例）

* 创作环境;用于：
   * 查询数据用于“内容管理目的”:
      * AEM中作为Cloud Service的GraphQL当前是只读API。
      * REST API可用于CR(u)D操作。

## 权限 {#permission}

这些权限是访问资产所需的权限。

## 模式生成{#schema-generation}

GraphQL是强类型API，这意味着数据必须按照类型清晰地进行结构化和组织。

GraphQL规范提供了有关如何创建健壮API以查询特定实例上的数据的一系列准则。 为此，客户端需要获取[模式](#schema-generation)，其中包含查询所需的所有类型。

对于内容片段，GraphQL模式（结构和类型）基于&#x200B;**Enabled** [内容片段模型](/help/assets/content-fragments/content-fragments-models.md)及其数据类型。

>[!CAUTION]
>
>所有GraphQL模式（从已启用&#x200B;****&#x200B;的内容片段模型派生）都可通过GraphQL端点进行读取。
>
>这意味着您需要确保没有敏感数据可用，因为这些数据可能会以这种方式泄露；例如，这包括在模型定义中可能作为字段名称显示的信息。

例如，如果用户创建了名为`Article`的内容片段模型，则AEM将生成类型为`ArticleModel`的对象`article`。 此类型中的字段与模型中定义的字段和数据类型相对应。

1. 内容片段模型：

   ![与GraphQLContent片段模型一起使](assets/cfm-graphqlapi-01.png "用的内容片段模型与GraphQL一起使用")

1. 相应的GraphQL模式（从GraphiQL自动文档输出i）:
   ![基于内容片段模型的](assets/cfm-graphqlapi-02.png "GraphQL模式基于内容片段模型的GraphQL模式")

   这表明生成的类型`ArticleModel`包含多个[字段](#fields)。

   * 其中三个由用户控制：`author`、`main`和`referencearticle`。

   * 其他字段由AEM自动添加，并代表提供特定内容片段相关信息的有用方法；在此示例中，`_path`、`_metadata`、`_variations`。 这些[帮助字段](#helper-fields)标有前面的`_`，以区分用户定义的内容和自动生成的内容。

1. 用户根据文章模型创建内容片段后，可以通过GraphQL进行询问。 例如，请参见[示例查询](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-sample-queries)（基于[示例内容片段结构，与GraphQL](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql)一起使用）。

在AEM的GraphQL中，模式是灵活的。 这意味着，每次创建、更新或删除内容片段模型时，都会自动生成该模型。 更新内容片段模型时，也会刷新模式缓存。

站点图形QL服务监听（在后台）对内容片段模型所做的任何修改。 检测到更新后，只会重新生成该模式部分。 这种优化节省了时间并提供了稳定性。

例如，如果：

1. 安装包，其中包含`Content-Fragment-Model-1`和`Content-Fragment-Model-2`:

   1. 将生成`Model-1`和`Model-2`的GraphQL类型。

1. 然后修改`Content-Fragment-Model-2`:

   1. 只有`Model-2` GraphQL类型将更新。

   1. 而`Model-1`将保持不变。

>[!NOTE]
>
>这一点很重要，以防您通过REST api或其他方式对内容片段模型进行批量更新。

模式通过与GraphQL查询相同的端点提供，客户端负责处理以扩展`GQLschema`调用模式的事实。 例如，对`/content/cq:graphql/global/endpoint.GQLschema`执行简单的`GET`请求将导致输出具有Content-type的模式:`text/x-graphql-schema;charset=iso-8859-1`。

## 字段 {#fields}

在模式中，有两个基本类别的单个字段：

* 生成的字段。

   选择[字段类型](#field-types)可根据您配置内容片段模型的方式创建字段。 字段名称取自&#x200B;**数据类型**&#x200B;的&#x200B;**属性名称**&#x200B;字段。

   * 还要考虑&#x200B;**Render As**&#x200B;属性，因为用户可以配置某些数据类型；例如，单行文本或多字段。

* AEM的GraphQL还生成许多[帮助字段](#helper-fields)。

   它们用于标识内容片段或获取有关内容片段的更多信息。

### 字段类型{#field-types}

GraphQL for AEM支持列表类型。 支持的所有内容片段模型数据类型和相应的GraphQL类型均表示：

| 内容片段模型——数据类型 | GraphQL类型 | 描述 |
|--- |--- |--- |
| 单行文本 | 字符串，[字符串] |  用于简单字符串，如作者姓名、位置名称等 |
| 多行文本 | 字符串 |  用于输出文本，如文章的正文 |
| 数字 |  浮点，[浮点] | 用于显示浮点数和正则数 |
| 布尔型 |  布尔型 |  用于显示复选框→简单的true/false语句 |
| 日期和时间 | 日历 |  用于以ISO 8086格式显示日期和时间 |
| 枚举 |  String |  用于显示在模型创建时定义的列表选项中的选项 |
|  标记 |  [String] |  用于显示表示AEM中使用的标记的字符串列表 |
| 内容引用 |  字符串 |  用于在AEM中显示指向另一个资产的路径 |
| 片段引用 |  *模型类型* |  用于引用特定模型类型的其他内容片段（在创建模型时定义） |

### 帮助字段{#helper-fields}

除了用户生成字段的数据类型外，AEM的GraphQL还生成许多&#x200B;*helper*&#x200B;字段，以帮助识别内容片段或提供有关内容片段的其他信息。

#### 路径 {#path}

路径字段用作GraphQL中的标识符。 它表示AEM存储库中内容片段资产的路径。 我们选择它作为内容片段的标识符，因为它：

* 在AEM中是独一无二的，
* 很容易被取走。

以下代码将显示根据内容片段模型`Person`创建的所有内容片段的路径。

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

请参阅[示例查询-单个特定城市片段](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-single-specific-city-fragment)。

#### 元数据 {#metadata}

通过GraphQL,AEM还公开内容片段的元数据。 元数据是描述内容片段的信息，如内容片段的标题、缩略图路径、内容片段的描述、创建日期等。

由于元数据是通过模式编辑器生成的，因此没有特定结构，因此实现了`TypedMetaData` GraphQL类型以公开内容片段的元数据。 `TypedMetaData` 显示按以下标量类型分组的信息：

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

每个标量类型表示单个名称——值对或名称——值对的数组，其中该对的值是其所分组的类型。

例如，如果要检索内容片段的标题，我们知道此属性是字符串属性，因此我们将查询所有字符串元数据：

查询元数据：

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

如果视图“生成的GraphQL”视图，则可以模式所有元数据GraphQL类型。 所有型号类型都具有相同的`TypedMetaData`。

>[!NOTE]
>
>**正常元数据与数组元数据的差异**
>请记住，`StringMetadata`和`StringArrayMetadata`都引用存储库中存储的内容，而不是如何检索它们。
>
>因此，例如，通过调用`stringMetadata`字段，您将收到存储库中存储的所有元数据的数组（作为`String`），如果调用`stringArrayMetadata`，您将收到存储在存储库中的所有元数据的数组（作为`String[]`）。

请参阅[元数据查询示例-列表标题为GB](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-metadata-awards-gb)的奖项的元数据。

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

请参阅[示例查询-所有具有命名变量的城市](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-cities-named-variation)。

<!--
## Security Considerations {#security-considerations}
-->

## GraphQL变量{#graphql-variables}

GraphQL允许将变量放置在查询中。 有关详细信息，请参阅GraphiQL](https://graphql.org/learn/queries/#variables)的[GraphQL文档。

例如，要获取具有特定变体的类型`Article`的所有内容片段，可在GraphiQL中指定变量`variation`。

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

例如，您可以在`AdventureModels`的查询中包含`adventurePrice`字段，该字段基于变量`includePrice`。

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

筛选使用基于逻辑运算符和表达式的语法。

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

* [用于AEM扩展的GraphQL的详细信息](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-extensions)

* [使用此示例内容和结构的示例查询](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-sample-queries-sample-content-fragment-structure)

   * 为样品查询准备的[样品内容和结构](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql)

* [基于WKND项目的示例查询](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-queries-using-wknd-project)

## 持久查询（缓存）{#persisted-queries-caching}

在准备具有查询请求的POST后，可以使用HTTP缓存或CDN缓存的GET请求执行该请求。

这是必需的，因为POST查询通常不进行缓存，如果将GET与查询一起使用作为参数，则参数对于HTTP服务和中间产品而言可能变得过大。

以下是保留给定查询所需的步骤：

>[!NOTE]
>在此之前，需要启用&#x200B;**GraphQL持久性查询**&#x200B;以获得相应的配置。 有关详细信息，请参阅[在配置浏览器中启用内容片段功能](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)。

1. 将查询输入到新的端点URL `/graphql/persist.json/<config>/<persisted-label>`，以准备该数据。

   例如，创建持久查询:

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

1. 此时，检查响应。

   例如，检查是否成功：

   ```xml
   {
     "action": "create",
     "configurationName": "wknd",
     "name": "plain-article-query",
     "shortPath": "/wknd/plain-article-query",
     "path": "/conf/wknd/settings/graphql/persistentQueries/plain-article-query"
   }
   ```

1. 然后，可以通过URL `/graphql/execute.json/<shortPath>`重播保留的查询。

   例如，使用保留的查询:

   ```xml
   $ curl -X GET \
       http://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. 通过将POST更新到现有的查询路径来更新保留的查询。

   例如，使用保留的查询:

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

1. 创建包装的纯查询。

   例如：

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-wrapped" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }"}'
   ```

1. 使用缓存控件创建包装的纯查询。

   例如：

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
   ```

1. 使用参数创建持久查询:

   例如：

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

1. 使用参数执行查询。

   例如：

   ```xml
   $ curl -X POST \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   
   $ curl -X GET \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   ```

1. 要在发布时执行查询，需要复制相关的持续树

   * 使用POST进行复制：

      ```xml
      $curl -X POST   http://localhost:4502/bin/replicate.json \
        -H 'authorization: Basic YWRtaW46YWRtaW4=' \
        -F path=/conf/wknd/settings/graphql/persistentQueries/plain-article-query \
        -F cmd=activate
      ```

   * 使用包：
      1. 创建新包定义。
      1. 包括配置（例如`/conf/wknd/settings/graphql/persistentQueries`）。
      1. 构建包。
      1. 复制包。
   * 使用复制／分发工具。
      1. 转到“分发”工具。
      1. 为配置选择树激活（例如`/conf/wknd/settings/graphql/persistentQueries`）。
   * 使用工作流（通过工作流启动器配置）:
      1. 定义一个工作流启动器规则，用于执行将在不同事件（例如，创建、修改等）上复制配置的工作流模型。



1. 在查询配置启用发布后，同样的原则也适用，只需使用发布端点。

   >[!NOTE]
   >
   >对于匿名访问，系统假定ACL允许“所有人”访问查询配置。
   >
   >如果情况不是这样，它将无法执行。

   >[!NOTE]
   >
   >需要对URL中的任何分号(“;”)进行编码。
   >
   >例如，在执行保留查询的请求中：
   >
   >
   ```xml
   >curl -X GET \ "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters%3bapath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   >```

## 从外部网站{#query-graphql-endpoint-from-external-website}查询GraphQL端点

>[!NOTE]
>
>有关AEM中CORS资源共享策略的详细概述，请参阅[了解跨来源资源共享(CORS)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=en#understand-cross-origin-resource-sharing-(cors))。

要允许第三方网站使用JSON输出，必须在客户Git存储库中配置CORS策略。 这是通过为所需端点添加适当的OSGi CORS配置文件来完成的。 此配置应指定应授予访问权限的受信任网站名称（或正则表达式）。

* 访问GraphQL端点：

   * alloworgin:[您的域]或alloworiginregexp:[域正则表达式]
   * 支持的方法：[POST]
   * allowedpaths:[&quot;/content/graphql/global/endpoint.json&quot;]

* 访问GraphQL持久查询端点：

   * alloworgin:[您的域]或alloworiginregexp:[域正则表达式]
   * 支持的方法：[GET]
   * allowedpaths:[&quot;/graphql/execute.json/.*&quot;]

>[!CAUTION]
>
>客户仍有责任：
>
>* 仅授予对受信任域的访问权限
>* 确保没有暴露任何敏感信息
>* 不使用通配符[*]语法；这既将禁用对GraphQL端点的已验证访问，也将向全世界展示它。


>[!CAUTION]
>
>所有GraphQL [模式](#schema-generation)（从已启用&#x200B;**的内容片段模型派生）都可通过GraphQL端点读取。**
>
>这意味着您需要确保没有敏感数据可用，因为这些数据可能会以这种方式泄露；例如，这包括在模型定义中可能作为字段名称显示的信息。

## 身份验证 {#authentication}

请参阅[内容片段上的远程AEM GraphQL查询的身份验证](/help/assets/content-fragments/graphql-authentication-content-fragments.md)。

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

1. **问**:“*AEM的GraphQL API与查询生成器API有何不同？*”

   * **答**:“*AEM GraphQL API优惠对JSON输出的完全控制，是查询内容的行业标准。今后，AEM计划投资于AEM GraphQL API。*&quot;

## 教程- AEM无头和GraphQL {#tutorial}入门

正在寻找实践教程？ 查看[AEM无外设和GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html)端到端教程入门，该教程说明了如何在无外设CMS场景中使用AEM的GraphQL API构建和公开内容并由外部应用程序使用。
