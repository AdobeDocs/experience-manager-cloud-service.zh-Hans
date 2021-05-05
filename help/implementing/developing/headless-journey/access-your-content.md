---
title: 如何通过AEM 投放 API访问您的内容
description: 在AEM无外设开发人员历程的这一部分中，了解如何使用GraphQL查询访问您的内容片段内容。
hide: true
hidefromtoc: true
index: false
exl-id: 5ef557ff-e299-4910-bf8c-81c5154ea03f
translation-type: tm+mt
source-git-commit: 7b04ae2bfa75fe3d3af13271efe567a5fc401f49
workflow-type: tm+mt
source-wordcount: '4636'
ht-degree: 1%

---

# 如何通过AEM 投放 API {#access-your-content}访问您的内容

>[!CAUTION]
>
>正在进行中的工作 — 此文档的创建正在进行中，不应理解为完整或明确，也不应将其用于生产目的。

在[AEM无外设开发者历程](overview.md)的这一部分中，您可以学习如何使用GraphQL查询访问内容片段的内容。

## 迄今为止的故事{#story-so-far}

在AEM无头旅程的上一个文档中，[如何对您的内容建模](model-your-content.md)您学习了AEM中数据建模的基础知识，因此您现在应该了解如何对您的内容结构建模，然后使用AEM内容片段模型和内容片段实现该结构：

* 识别与[数据建模](#data-modeling)相关的概念和术语。
* 了解[为什么无头内容投放](#data-modeling-for-aem-headless)需要数据建模。
* 了解[如何使用AEM内容片段模型](#create-structure-content-fragment-models)（以及使用[内容片段](#use-content-to-author-content)创作内容）实现此结构。
* 了解[如何对内容进行建模](#getting-started-examples);基本样本的原则。

本文以这些基础知识为基础，因此您可以了解如何使用AEM GraphQL API在AEM中访问现有无外设内容。

* **受众**:初学者
* **目标**:了解如何使用AEM GraphQL查询访问内容片段的内容：
   * 介绍GraphQL和AEM GraphQL API。
   * 深入了解AEM GraphQL API的详细信息。
   * 查看一些示例查询，了解实际操作情况。

## 那么，您想访问您的数据吗？{#so-youd-like-to-access-your-data}

所以……您已经拥有了所有这些内容，整洁地构建（在内容片段中），并且只是在等待您的新应用程序。 问题是，如何实现它？

您需要的是一种目标特定内容、选择所需内容并将其返回到应用程序以进一步处理的方法。

以Adobe Experience Manager(AEM)为Cloud Service，您可以使用AEM GraphQL API选择性地访问内容片段，以仅返回所需的内容。 这意味着您可以实现结构化内容的无外设投放，以便在应用程序中使用。

>[!NOTE]
>
>AEM GraphQL API是基于标准GraphQL的自定义实施。

## GraphQL — 简介{#graphql-introduction}

GraphQL是一个开放源代码规范，它提供：

* 一种查询语言，允许您从结构化对象中选择特定内容。
* 一个运行时，用于使结构化内容实现这些查询。

GraphQL是&#x200B;*strongly*&#x200B;类型API。 这意味着&#x200B;*所有*&#x200B;内容必须按照类型清晰地结构化和组织，这样GraphQL *才能了解*&#x200B;要访问的内容和访问方式。 数据字段在GraphQL模式中定义，GraphQL定义内容对象的结构。

然后，GraphQL端点提供响应GraphQL查询的路径。

所有这些意味着您的应用程序能够准确、可靠、高效地选择所需数据 — 这正是您与AEM一起使用时需要的。

>[!NOTE]
>
>请参阅&#x200B;*GraphQL*.org和&#x200B;*GraphQL*.com。

## AEM和GraphQL {#aem-graphql}

GraphQL用于AEM中的不同位置；例如：

* 商务
   * AEM与各种第三方商务解决方案之间都有GraphQL集成，这些解决方案与CIF核心组件提供的扩展挂钩一起使用。
* 内容片段
   * 为此用例开发了自定义API。
   * 这是AEM GraphQL API。

>[!NOTE]
>
>此无头历程步骤仅涉及AEM GraphQL API和内容片段。

## AEM GraphQL API {#aem-graphql-api}

AEM GraphQL API是标准GraphQL API的自定义版本，专门配置为允许您对内容片段执行（复杂）查询。

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
   * 查询JS应用程序数据（标准用例）

* 创作环境;:
   * 查询数据用于“内容管理目的”：
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

* 与GraphQL结合使用时特别感兴趣。

* 是在定义内容片段模型时可以使用的特定数据类型。

* 引用另一个片段，具体取决于特定的内容片段模型。

* 允许您检索结构化数据。

   * 当定义为&#x200B;**multifeed**&#x200B;时，主片段可以引用（检索）多个子片段。

### JSON预览{#json-preview}

要帮助设计和开发内容片段模型，您可以在内容片段编辑器中预览JSON输出。

## 从内容片段{#graphql-schema-generation-content-fragments}生成GraphQL模式

GraphQL是强类型API，这意味着数据必须按照类型清晰地结构化和组织。 GraphQL规范提供了有关如何创建用于查询特定实例上的数据的强大API的一系列指南。 为此，客户端需要获取模式，其中包含查询所需的所有类型。

对于内容片段，GraphQL模式（结构和类型）基于&#x200B;**已启用**&#x200B;内容片段模型及其数据类型。

>[!CAUTION]
>
>所有GraphQL模式（从&#x200B;**已启用**&#x200B;的内容片段模型派生）均可通过GraphQL端点读取。
>
>这意味着您需要确保没有敏感数据可用，因为这些数据可能会以这种方式泄露；例如，这包括在模型定义中可能作为字段名称显示的信息。

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

<!--
new page?
-->

## 使用AEM GraphQL API {#using-aem-graphiql}

### 端点{#endpoints}

GraphQL for AEM全局端点的存储库路径为：

`/content/cq:graphql/global/endpoint`

您的应用程序可在请求URL中使用以下路径：

`/content/_cq_graphql/global/endpoint.json`

对于租户端点，路径是可比的：

`/content/cq:graphql/your-tenant/endpoint`
`/content/_cq_graphql/your-tenant/endpoint.json`

在使用之前，必须启用所有端点。 要为AEM的GraphQL启用端点（全局或租户），您需要：

* 启用GraphQL端点
* 发布您的端点

>[!CAUTION]
>
>内容片段编辑器允许一个租户的内容片段引用另一个租户的内容片段（通过策略）。
>
>在这种情况下，并非所有内容都可以使用租户特定的端点进行检索。
>
>内容作者应控制此方案；例如，考虑将共享内容片段模型放在全局租户下可能很有用。

### 启用GraphQL端点{#enabling-graphql-endpoint}

要启用GraphQL端点，您首先需要在配置浏览器中具有相应的配置。

>[!CAUTION]
>
>如果尚未启用对内容片段模型的使用，则&#x200B;**创建**&#x200B;选项将不可用。

要启用相应的端点，请执行以下操作：

1. 导航到&#x200B;**工具**、**站点**，然后选择&#x200B;**图形QL**。
1. 选择&#x200B;**创建**。
1. 将打开&#x200B;**新建GraphQL Endpoint**&#x200B;对话框。 您可以在此处指定：
   * **名称**:端点的名称；您可以输入任何文本。
   * **使用GraphQL模式**:使用下拉列表选择所需的站点/项目。

   >[!NOTE]
   >
   >对话框中显示以下警告：
   >
   >* *如果不对 GraphQL 端点仔细管理，则可能会带来数据安全和性能问题。请确保在创建端点后设置适当的权限。*


1. 使用&#x200B;**创建**&#x200B;进行确认。
1. **后续步骤**&#x200B;对话框将提供指向安全控制台的直接链接，以便您能够确保新创建的端点具有适当的权限。

   >[!CAUTION]
   >
   >每个人都可以访问该端点。 这可能会引起安全问题，因为GraphQL查询可能会对服务器施加大负载。
   >
   >您可以在端点上设置与用例相适应的ACL。

### 发布GraphQL端点{#publishing-graphql-endpoint}

选择新端点并选择&#x200B;**发布**，使其在所有环境中都完全可用。

>[!CAUTION]
>
>每个人都可以访问该端点。
>
>在发布实例中，这可能会引起安全问题，因为GraphQL查询可能会对服务器施加大负载。
>
>必须在端点上设置与用例相适应的ACL。

### 安装AEM GraphiQL接口{#installing-graphiql-interface}

GraphiQL用户界面可安装在AEM上并包含专用包：[GraphiQL内容包v0.0.6(2021.3)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-graphql/graphiql-0.0.6.zip)包。

### AEM GraphQL模式{#aem-graphql-schemas}

要访问您的数据，您首先需要选择所需的内容片段模型类型 — 由GraphQL模式表示。 AEM GraphQL模式是从您的内容片段模型派生的 — 用于您的GraphQL查询。

<!--
Confirm is the schema city or CityModel? -->

如果您有一个名为`City`的内容片段模型，则会有一个名为`city`的对应模式。 您可以使用以下查询来列表基于此模型的所有内容片段的`name`。

```xml
query {
  cityList {
    items {
      name
    }
  }
}
```

您可以使用以下查询列表所有`types`的`name`和`description`，以查看所有可用模式:

```xml
{
  __schema {
    types {
      name
      description
    }
  }
}
```

### AEM GraphQL字段{#aem-graphql-fields}

选择所需的模式后，您将需要访问特定数据 — 由模式中的字段表示。

在该模式中，有两个基本类别的单个字段：

* 生成的字段。

   选择[字段类型](#field-types)用于根据您配置内容片段模型的方式创建字段。 字段名称取自&#x200B;**数据类型**&#x200B;的&#x200B;**属性名称**&#x200B;字段。

   * 还有&#x200B;**Render As**&#x200B;属性要考虑，因为用户可以配置某些数据类型；例如，作为单行文本或多字段。

* GraphQL for AEM还生成许多帮助字段。

   它们用于标识内容片段或获取有关内容片段的更多信息。

### 字段类型{#field-types}

GraphQL for AEM支持列表类型。 所有支持的内容片段模型数据类型和相应的GraphQL类型均表示：

| 内容片段模型 — 数据类型 | 图形QL类型 | 描述 |
|--- |--- |--- |
| 单行文本 | 字符串，[字符串] | 用于简单字符串，如作者姓名、位置名称等。 |
| 多行文本 | 字符串 | 用于输出文本，如文章的正文 |
| 数字 | 浮点，[浮点] | 用于显示浮点数和正则数 |
| 布尔型 | 布尔型 | 用于显示复选→框的简单true/false语句 |
| 日期和时间 | 日历 | 用于以ISO 8086格式显示日期和时间。 根据所选的类型，AEM GraphQL中有三种可用方式：`onlyDate`、`onlyTime`、`dateTime` |
| 枚举 | 字符串 | 用于从创建模型时定义的列表选项中显示选项 |
| 标记 | [String] | 用于显示表示AEM中使用的标记的字符串列表 |
| 内容引用 | 字符串 | 用于在AEM中显示指向另一个资产的路径 |
| 片段引用 | *模型类型* | 用于引用某个“模型类型”的其他“内容片段”（在创建模型时定义） |

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

>[!NOTE]
>
>请参阅示例查询 — 单个特定城市片段。

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
| `booleanArrayMetadata:[booleanArrayMetadata]!` |
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

>[!NOTE]
>
>请参阅元数据的示例查询-列表标题为GB的奖项的元数据。

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

>[!NOTE]
>
>请参阅示例查询 — 所有具有指定变量的城市。

### AEM GraphQL变量{#aem-graphql-variables}

变量可用于任何形式的编程或查询，因为它们允许您在一个位置存储不同的值。 对于AEM GraphQL，这意味着您不必为每个值编写单独的查询，而是可以为一个变量编写查询，并且此变量的值会根据需要进行更改。

GraphQL允许将变量放置在查询中。

>[!NOTE]
>
>有关详细信息，请参阅变量的GraphQL文档。

例如，要获取具有特定变量的`Article`类型的所有内容片段，可以在GraphiQL中指定变量`variation`。 将在`GetArticlesByVariation`中检索所有实例，然后传递给`articleList`中使用。

![GraphQL变](assets/graphqlapi-variables.png "量GraphQL变量")

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

### AEM GraphQL指令{#aem-graphql-directives}

在GraphQL中，可以根据变量（称为GraphQL指令）更改查询。

例如，您可以根据变量`includePrice`将所有`AdventureModels`的查询包含`adventurePrice`字段。

!![GraphQL Directives]（assets/graphqlapi-directives .png &quot;GraphQL指令&quot;）

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

### AEM GraphQL过滤器{#aem-graphql-filters}

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

* GraphQL for AEM扩展的详细信息

* 使用此示例内容和结构的示例查询

### AEM GraphQL扩展{#aem-graphql-extensions}

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

### 持久查询（缓存）{#persisted-queries-caching}

在准备具有查询请求的GET后，可以使用HTTP缓存或CDN缓存的POST请求执行该请求。

这是必需的，因为POST查询通常不进行缓存，如果将查询作为参数使用，则参数对于HTTP服务和中间产品而言变得过大的风险很大。

持久查询必须始终使用与相应（租户）配置相关的端点；这样，他们就可以使用其中一种或两种方式：

* 全局配置和端点
查询可以访问所有内容片段模型。
* 特定租户配置和端点
为特定租户配置创建持久查询需要相应的租户特定端点（以提供对相关内容片段模型的访问）。
例如，要为WKND租户专门创建持久查询，必须提前创建相应的WKND特定租户配置和WKND特定终结点。

>[!NOTE]
>
>有关详细信息，请参阅在配置浏览器中启用内容片段功能。
>
>需要为相应的租户配置启用&#x200B;**GraphQL持久查询**。

例如，如果存在名为`my-query`的特定查询，它使用租户配置`my-conf`中的模型`my-model`:

* 您可以使用`my-conf`特定端点创建查询，然后查询将保存为：
   `/conf/my-conf/settings/graphql/persistentQueries/my-query`
* 您可以使用`global`端点创建相同的查询，但随后查询将保存为：
   `/conf/global/settings/graphql/persistentQueries/my-query`

>[!NOTE]
>
>这是两种不同的查询 — 保存在不同的路径下。
>
>他们恰巧使用了相同的模型 — 但是通过不同的端点。

以下是保持给定查询所需的步骤：

1. 将查询放置到新的端点URL `/graphql/persist.json/<config>/<persisted-label>`来准备。

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

1. 此时，请检查响应。

   例如，检查成功与否：

   ```xml
   {
     "action": "create",
     "configurationName": "wknd",
     "name": "plain-article-query",
     "shortPath": "/wknd/plain-article-query",
     "path": "/conf/wknd/settings/graphql/persistentQueries/plain-article-query"
   }
   ```

1. 然后，可以通过获取URL `/graphql/execute.json/<shortPath>`来重播保留的查询。

   例如，使用持久查询:

   ```xml
   $ curl -X GET \
       http://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. 通过将POST更新到现有查询路径来更新持续查询。

   例如，使用持久查询:

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

1. 使用缓存控件创建包装式纯查询。

   例如：

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
   ```

1. 使用参数创建持续查询:

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

1. 要在发布时执行查询，需要复制相关的持久树

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
   * 使用复制/分发工具。
      1. 转到“分发”工具。
      1. 为配置选择树激活（例如`/conf/wknd/settings/graphql/persistentQueries`）。
   * 使用工作流（通过工作流启动器配置）：
      1. 定义一个工作流启动器规则，用于执行将在不同事件（例如，创建、修改等）上复制配置的工作流模型。



1. 查询配置在发布后，同样的原则也适用，只需使用发布端点即可。

   >[!NOTE]
   >
   >对于匿名访问，系统假定ACL允许“所有人”访问查询配置。
   >
   >如果情况并非如此，它将无法执行。

   >[!NOTE]
   >
   >需要对URL中的任何分号(&quot;;&quot;)进行编码。
   >
   >例如，与执行持久查询的请求一样：
   >
   >
   ```xml
   >curl -X GET \ "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters%3bapath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   >```

### 从外部网站{#query-graphql-endpoint-from-external-website}查询GraphQL端点

要从外部网站访问GraphQL端点，您需要配置：

* CORS过滤器
* 推荐人过滤器

#### CORS过滤器{#cors-filter}

>[!NOTE]
>
>有关AEM中CORS资源共享策略的详细概述，请参阅了解跨来源资源共享(CORS)。

要访问GraphQL端点，必须在客户Git存储库中配置CORS策略。 为此，可为所需端点添加适当的OSGi CORS配置文件。

此配置必须指定必须授予访问权限的受信任的网站来源`alloworigin`或`alloworiginregexp`。

例如，要授予对`https://my.domain`的GraphQL端点和持久查询端点的访问权，可以使用：

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

如果已配置端点的虚路径，则还可在`allowedpaths`中使用它。

#### 推荐人过滤器{#referrer-filter}

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
>所有GraphQL模式（从&#x200B;**已启用**&#x200B;的内容片段模型派生）均可通过GraphQL端点读取。
>
>这意味着您需要确保没有敏感数据可用，因为这些数据可能会以这种方式泄露；例如，这包括在模型定义中可能作为字段名称显示的信息。

### AEM GraphQL身份验证{#aem-graphql-authentication}

将Adobe Experience Manager作为Cloud Service(AEM)GraphQL API用于内容片段投放的主要用例是接受来自第三方应用程序或服务的远程查询。 这些远程查询可能需要经过身份验证的API访问，以保护无外设内容投放。

>[!NOTE]
>
>对于测试和开发，您还可以使用GraphiQL界面直接访问AEM GraphQL API。

要进行身份验证，第三方服务需要使用访问令牌，然后可以在GraphQL请求中使用。

#### 检索访问令牌{#retrieving-access-token}

有关完整的详细信息，请参阅生成服务器端API的访问令牌。

#### 使用GraphQL请求{#use-access-token-in-graphql-request}中的访问令牌

要使第三方服务与AEM实例连接，它需要具有&#x200B;*访问令牌*。 然后，服务必须将此令牌添加到POST请求的`Authorization`标头中。

例如，GraphQL授权标头：

```xml
Authorization: Bearer <access_token>
```

#### 权限要求{#permission-requirements}

使用访问令牌发出的所有请求实际上将由生成令牌的用户帐户发出&#x200B;*。*

这意味着您需要检查帐户是否具有运行GraphQL查询所需的权限。

可以通过在本地实例上使用GraphiQL来检查此项。

## AEM GraphQL查询{#samples-aem-graphql-queries}示例

有关各种示例查询，请参阅学习将GraphQL与AEM一起使用 — 示例内容和查询。

<!--
## Code Samples for AEM GraphQL Queries {#code-samples-aem-graphql-queries}
-->

## 下一步是什么{#whats-next}

现在，您已经学习了如何使用AEM GraphQL API访问和查询您的无外设内容，现在您可以[了解如何使用REST API访问和更新您的内容片段](/help/implementing/developing/headless-journey/update-your-content.md)的内容。

## 其他资源 {#additional-resources}

* [GraphQL.org](https://graphql.org)
   * [架构](https://graphql.org/learn/schema/)
   * [变量](https://graphql.org/learn/queries/#variables)
   * [GraphQL Java库](https://graphql.org/code/#java)
* [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql)
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
* [AEM无头入门](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html)  — 一个简短的视频教程系列概述了如何使用AEM无头功能，包括数据建模和GraphQL。
