---
title: 内容投放，将内容片段与Adobe Experience Manager一起用作Cloud Service图QL API
description: 了解如何将Adobe Experience Manager(AEM)中的内容片段用作AEM GraphQL API的Cloud Service，用于无头内容投放。
translation-type: tm+mt
source-git-commit: 1e9596fb12a38f5c4c6e15d7c33af86e59e76083
workflow-type: tm+mt
source-wordcount: '2491'
ht-degree: 1%

---


# AEM GraphQL API，用于内容片段{#graphql-api-for-use-with-content-fragments}

>[!CAUTION]
>
>针对内容片段投放的AEM GraphQL API将于2021年初发布。
>
>相关文档已经可供预览使用。

Adobe Experience Manager作为Cloud Service(AEM) GraphQL API与内容片段一起使用，它在很大程度上基于标准的开放源GraphQL API。

在AEM中使用GraphQL API，在无外设CMS实现中，可以将内容片段高效投放到JavaScript客户端：

* 避免像REST一样重复的API请求，
* 确保投放仅限于具体要求，
* 允许批量投放呈现作为对单个API查询的响应所需的确切内容。

## GraphQL API {#graphql-api}

*“GraphQL是Facebook在2012年在内部开发的一种数据查询语言和规范，2015年公开开发。它为基于REST的体系结构提供了一种替代方法，目的是提高开发者的工作效率并最大限度地减少数据传输量。 GraphQL由数百个不同规模的组织在生产中使用……&quot;*&#x200B;请参阅[GraphQL Foundation](https://foundation.graphql.org/)。

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

## GraphiQL接口{#graphiql-interface}

AEM Graph API包括标准[GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql)接口的实现。 这允许您直接输入和测试查询。

例如：

* `http://localhost:4502/content/graphiql.html`

它提供语法高亮显示、自动完成、自动建议等功能以及历史记录和在线文档：

![GraphiQL接](assets/cfm-graphiql-interface.png "口GraphiQL接口")

## 创作和发布环境的用例{#use-cases-author-publish-environments}

用例取决于AEM的类型，即Cloud Service环境:

* 发布环境;用于：
   * 查询JS应用程序数据（标准用例）

* 创作环境;用于：
   * 查询数据用于“内容管理目的”:
      * AEM中作为Cloud Service的GraphQL当前是只读API。
      * REST API可用于CR(u)D操作。

## 模式生成{#schema-generation}

GraphQL是强类型API，这意味着数据必须按照类型清晰地进行结构化和组织。

GraphQL规范提供了有关如何创建健壮API以查询特定实例上的数据的一系列准则。 为此，客户端需要获取[模式](#schema-generation)，其中包含查询所需的所有类型。

对于内容片段，GraphQL模式（结构和类型）基于[内容片段模型](/help/assets/content-fragments/content-fragments-models.md)及其数据类型。

例如，如果用户创建了名为`Article`的内容片段模型，则AEM将生成类型为`ArticleModel`的对象`article`。 此类型中的字段与模型中定义的字段和数据类型相对应。

1. 内容片段模型：

   ![与GraphQLContent片段模型一起使](assets/cfm-graphqlapi-01.png "用的内容片段模型与GraphQL一起使用")

1. 相应的GraphQL模式（从GraphiQL自动文档输出i）:
   ![基于内容片段模型的](assets/cfm-graphqlapi-02.png "GraphQL模式基于内容片段模型的GraphQL模式")

   这表明生成的类型`ArticleModel`包含多个[字段](#fields)。

   * 其中三个由用户控制：`author`、`main`和`linked_article`。

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

模式通过与GraphQL查询相同的端点提供，客户端负责处理以扩展`GQLschema`调用模式的事实。 例如，对`/content/graphql/endpoint.GQLschema`执行简单的`GET`请求将导致输出具有Content-type的模式:`text/x-graphql-schema;charset=iso-8859-1`。

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
  persons {
    items {
      _path
    }
  }
}
```

要检索特定类型的单个内容片段，您还需要首先确定其路径。 例如：

```xml
{
    person(_path="/content/dam/path/to/fragment/john-doe") {
        _path
        name
        first-name
    }
}
```

请参阅[示例查询-单个城市片段](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-single-city-fragment)。

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
  person(_path: "/content/dam/path/to/fragment/john-doe") {
    _path
    _metadata {
      stringMetadata {
        name
        value
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
  person(_path: "/content/dam/path/to/fragment/john-doe") {
    _variations
  }
}
```

请参阅[示例查询-所有具有命名变量的城市](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-cities-named-variation)。

<!--
## Security Considerations {#security-considerations}
-->

## GraphQL变量{#graphql-variables}

GraphQL允许将变量放置在查询中。 有关详细信息，请参阅GraphiQL](https://graphql.org/learn/queries/#variables)的[GraphQL文档。

例如，要获取具有特定变体的类型`Article`的所有内容片段，可在GraphiQL中指定变量`variation`:

![GraphQL变](assets/cfm-graphqlapi-03.png "量GraphQL变量")

```xml
### query
query GetArticlesByVariation($variation: String!) {
    articles(variation: $variation) {
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
query getAdventureByType($includePrice: Boolean!) {
  adventures {
    items {
      adventureType
      adventurePrice @include(if: $includePrice)
    }
  }
}
 
### in query variables
{
    "includePrice": true
}
```

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
   * allowedpaths:[&quot;/apps/graphql-enablement/content/endpoint.gql(/persisted)?&quot;]

* 访问GraphQL持久查询端点：

   * alloworgin:[您的域]或alloworiginregexp:[域正则表达式]
   * 支持的方法：[GET]
   * allowedpaths:[&quot;/graphql/execute.json/.*&quot;]

>[!CAUTION]
>
>客户仍有责任：
>
>* 仅授予对受信任域的访问权限
>* 不使用通配符[*]语法；这将向全世界展示GraphQL端点。



## 筛选{#filtering}

您还可以在GraphQL查询中使用筛选来返回特定数据。

筛选使用基于逻辑运算符和表达式的语法。

有关示例，请参阅：

* [用于AEM扩展的GraphQL的详细信息](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-some-extensions)

* [为样本查询](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql) 准备的样本内容和结构

* [使用此示例内容和结构的示例查询](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-sample-queries-sample-content-fragment-structure)

* [基于WKND项目的示例查询](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-queries-using-wknd-project)

## 权限 {#permission}

这些权限是访问资产所需的权限。

<!-- to be addressed later -->

<!-- 
## Authentication {#authentication}
-->

<!-- to be addressed later -->

<!-- 
## Caching {#caching}
-->

<!-- to be addressed later -->

<!--
## Sorting {#sorting}
-->

<!-- to be addressed later -->

<!--
## Paging {#paging}
-->

## 结束点{#end-points}

端点是用于访问AEM的GraphQL的路径。 使用此路径，您（或您的应用程序）可以：

* 访问GraphQL模式,
* 发送您的GraphQL查询,
* 接收响应(对您的GraphQL查询)。

要访问AEM中的GraphQL Servlet，您需要配置端点。 这还包括两个OSGi配置。

1. 响应检索GraphQL模式请求的Sling模式servlet:

   ![AEM Sites图QL模式Servlet](assets/cfm-endpoint-01.png)

   * **选择器** (`sling.servlet.selectors`)必须留空。

   * **资源类型** (`sling.servlet.resourceTypes`)定义GraphQL servlet应侦听的资源类型。例如：
      `graphql-enablement/components/endpoint`。

   * **方法** (`sling.servlet.methods^)

      servlet应侦听的HTTP方法；通常`GET`。

   * **扩展** (`sling.servlet.extensions`)

      指定模式Servlet应响应的扩展。 在这种情况下，它是`GQLschema`，与GraphQL规范兼容。

2. 响应图形ql请求的Servlet:

   ![Apache Sling GraphQL Servlet](assets/cfm-endpoint-02.png)

   * **选择器** (`sling.servlet.selectors`)必须留空。

   * **资源类型** (`sling.servlet.resourceTypes`)GraphQL servlet应响应的资源类型。例如，`graphql-enablement/components/endpoint`。

   * **方法** (`sling.servlet.methods`)GraphQL servlet应响应的HTTP方法，通常 `GET` 和 `POST`。

   * **扩展** (`sling.servlet.extensions`)用于侦听GraphQL请求的扩展，通常 `gql`。

3. 您现在需要创建端点——这些配置中定义的sling:resourceType节点。
例如，要创建用于检索GraphQL模式的端点，请在`/apps/<my-site>/graphql`下创建一个新节点：

   * 名称: `endpoint`
   * 主类型：`nt:unstructured`
   * sling:resourceType: `graphql-enablement/components/endpoint`

## 常见问题解答{#faqs}

出现的问题：

1. **问**:“*AEM的GraphQL API与查询生成器API有何不同？*”

   * **答**:“*AEM GraphQL API优惠对JSON输出的完全控制，是查询内容的行业标准。今后，AEM计划投资于AEM GraphQL API。*&quot;

## 教程- AEM无头和GraphQL {#tutorial}入门

正在寻找实践教程？ 查看[AEM无外设和GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html)端到端教程入门，该教程说明了如何在无外设CMS场景中使用AEM的GraphQL API构建和公开内容并由外部应用程序使用。