---
title: 了解如何将GraphQL与AEM结合使用 — 示例内容和查询
description: 了解如何通过探索示例内容和查询，将GraphQL与AEM结合使用来无头地提供内容。
translation-type: tm+mt
source-git-commit: e7ca6dc841ba777384be74021a27d523d530a956
workflow-type: tm+mt
source-wordcount: '1418'
ht-degree: 6%

---


# 了解如何将GraphQL与AEM一起使用 — 示例内容和查询{#learn-graphql-with-aem-sample-content-queries}

了解如何通过探索示例内容和查询，将GraphQL与AEM结合使用来无头地提供内容。

>[!NOTE]
>
>此页面应与以下内容一起阅读：
>
>* [内容片段](/help/assets/content-fragments/content-fragments.md)
>* [内容片段模型](/help/assets/content-fragments/content-fragments-models.md)
>* [AEM GraphQL API，与内容片段一起使用](/help/assets/content-fragments/graphql-api-content-fragments.md)


要开始使用GraphQL查询及其如何使用AEM内容片段，查看一些实际示例会有所帮助。

要帮助解决此问题，请参阅：

* [示例内容片段结构](#content-fragment-structure-graphql)

* 以及某些[示例GraphQL查询](#graphql-sample-queries)，基于示例内容片段结构（内容片段模型和相关内容片段）。


## GraphQL — 使用示例内容片段结构{#graphql-sample-queries-sample-content-fragment-structure}的示例查询

有关创建查询的插图，请参阅这些示例查询以及示例结果。

>[!NOTE]
>
>根据您的实例，您可以直接访问AEM GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md#graphiql-interface)附带的[Graph *i* QL接口，以提交和测试查询。
>
>例如：`http://localhost:4502/content/graphiql.html`

>[!NOTE]
>
>示例查询基于[示例内容片段结构，以与GraphQL](#content-fragment-structure-graphql)一起使用

### 示例查询 — 所有可用模式和数据类型{#sample-all-schemes-datatypes}

这将返回所有可用模式的所有`types`。

**示例查询**

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

**示例结果**

```xml
{
  "data": {
    "__schema": {
      "types": [
        {
          "name": "AdventureModel",
          "description": null
        },
        {
          "name": "AdventureModelArrayFilter",
          "description": null
        },
        {
          "name": "AdventureModelFilter",
          "description": null
        },
        {
          "name": "AdventureModelResult",
          "description": null
        },
        {
          "name": "AdventureModelResults",
          "description": null
        },
        {
          "name": "AllFragmentModels",
          "description": null
        },
        {
          "name": "ArchiveRef",
          "description": null
        },
        {
          "name": "ArrayMode",
          "description": null
        },
        {
          "name": "ArticleModel",
          "description": null
        },

...more results...

        {
          "name": "__EnumValue",
          "description": null
        },
        {
          "name": "__Field",
          "description": null
        },
        {
          "name": "__InputValue",
          "description": null
        },
        {
          "name": "__Schema",
          "description": "A GraphQL Introspection defines the capabilities of a GraphQL server. It exposes all available types and directives on the server, the entry points for query, mutation, and subscription operations."
        },
        {
          "name": "__Type",
          "description": null
        },
        {
          "name": "__TypeKind",
          "description": "An enum describing what kind of type a given __Type is"
        }
      ]
    }
  }
}
```

### 示例查询 — 有关所有城市的所有信息{#sample-all-information-all-cities}

要检索所有城市的所有信息，您可以使用非常基本的查询:
**示例查询**

```xml
{
  cityList {
    items
  }
}
```

执行时，系统将自动展开查询以包含所有字段：

```xml
{
  cityList {
    items {
      _path
      name
      country
      population
    }
  }
}
```

**示例结果**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "_path": "/content/dam/sample-content-fragments/cities/basel",
          "name": "Basel",
          "country": "Switzerland",
          "population": 172258
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/berlin",
          "name": "Berlin",
          "country": "Germany",
          "population": 3669491
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/bucharest",
          "name": "Bucharest",
          "country": "Romania",
          "population": 1821000
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/san-francisco",
          "name": "San Francisco",
          "country": "USA",
          "population": 883306
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/san-jose",
          "name": "San Jose",
          "country": "USA",
          "population": 1026350
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/stuttgart",
          "name": "Stuttgart",
          "country": "Germany",
          "population": 634830
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/zurich",
          "name": "Zurich",
          "country": "Switzerland",
          "population": 415367
        }
      ]
    }
  }
}
```

### 示例查询 — 所有城市名称{#sample-names-all-cities}

这是返回`city`模式中所有条目的`name`的直接查询。

**示例查询**

```xml
query {
  cityList {
    items {
      name
    }
  }
}
```

**示例结果**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "Basel"
        },
        {
          "name": "Berlin"
        },
        {
          "name": "Bucharest"
        },
        {
          "name": "San Francisco"
        },
        {
          "name": "San Jose"
        },
        {
          "name": "Stuttgart"
        },
        {
          "name": "Zurich"
        }
      ]
    }
  }
}
```

### 示例查询 — 单个特定城市片段{#sample-single-specific-city-fragment}

这是一个查询，用于返回存储库中特定位置的单个片段条目的详细信息。

**示例查询**

```xml
{
  cityByPath (_path: "/content/dam/sample-content-fragments/cities/berlin") {
    item {
      _path
      name
      country
      population
     categories
    }
  }
}
```

**示例结果**

```xml
{
  "data": {
    "cityByPath": {
      "item": {
        "_path": "/content/dam/sample-content-fragments/cities/berlin",
        "name": "Berlin",
        "country": "Germany",
        "population": 3669491,
        "categories": [
          "city:capital",
          "city:emea"
        ]
      }
    }
  }
}
```

### 示例查询 — 具有命名变量{#sample-cities-named-variation}的所有城市

如果您为`city`柏林新建了一个名为“柏林中心”(`berlin_centre`)的变体，则可以使用查询返回变体的详细信息。

**示例查询**

```xml
{
  cityList (variation: "berlin_center") {
    items {
      _path
      name
      country
      population
      categories
    }
  }
}
```

**示例结果**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "_path": "/content/dam/sample-content-fragments/cities/berlin",
          "name": "Berlin",
          "country": "Germany",
          "population": 3669491,
          "categories": [
            "city:capital",
            "city:emea"
          ]
        }
      ]
    }
  }
}
```

### 示例查询-公司CEO和员工的完整详细信息{#sample-full-details-company-ceos-employees}

使用嵌套片段的结构，此查询返回公司CEO及其所有员工的完整详细信息。

**示例查询**

```xml
query {
  companyList {
    items {
      name
      ceo {
        _path
        name
        firstName
        awards {
        id
          title
        }
      }
      employees {
       name
        firstName
       awards {
         id
          title
        }
      }
    }
  }
}
```

**示例结果**

```xml
{
  "data": {
    "companyList": {
      "items": [
        {
          "name": "Apple Inc.",
          "ceo": {
            "_path": "/content/dam/sample-content-fragments/persons/steve-jobs",
            "name": "Jobs",
            "firstName": "Steve",
            "awards": []
          },
          "employees": [
            {
              "name": "Marsh",
              "firstName": "Duke",
              "awards": []
            },
            {
              "name": "Caulfield",
              "firstName": "Max",
              "awards": [
                {
                  "id": "GB",
                  "title": "Gameblitz"
                }
              ]
            }
          ]
        },
        {
          "name": "Little Pony, Inc.",
          "ceo": {
            "_path": "/content/dam/sample-content-fragments/persons/adam-smith",
            "name": "Smith",
            "firstName": "Adam",
            "awards": []
          },
          "employees": [
            {
              "name": "Croft",
              "firstName": "Lara",
              "awards": [
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            },
            {
              "name": "Slade",
              "firstName": "Cutter",
              "awards": [
                {
                  "id": "GB",
                  "title": "Gameblitz"
                },
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            }
          ]
        },
        {
          "name": "NextStep Inc.",
          "ceo": {
            "_path": "/content/dam/sample-content-fragments/persons/steve-jobs",
            "name": "Jobs",
            "firstName": "Steve",
            "awards": []
          },
          "employees": [
            {
              "name": "Smith",
              "firstName": "Joe",
              "awards": []
            },
            {
              "name": "Lincoln",
              "firstName": "Abraham",
              "awards": []
            }
          ]
        }
      ]
    }
  }
}
```

### 示例查询 — 名称为“Jobs”或“Smith” {#sample-all-persons-jobs-smith}的所有人员

这将过滤所有`persons`，以查找名称为`Jobs`或`Smith`的任何文件。

**示例查询**

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

**示例结果**

```xml
{
  "data": {
    "personList": {
      "items": [
        {
          "name": "Smith",
          "firstName": "Adam"
        },
        {
          "name": "Smith",
          "firstName": "Joe"
        },
        {
          "name": "Jobs",
          "firstName": "Steve"
        }
      ]
    }
  }
}
```

### 示例查询 — 所有姓名不为“Jobs” {#sample-all-persons-not-jobs}的人员

这将过滤所有`persons`，以查找名称为`Jobs`或`Smith`的任何文件。

**示例查询**

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

**示例结果**

```xml
{
  "data": {
    "personList": {
      "items": [
        {
          "name": "Lincoln",
          "firstName": "Abraham"
        },
        {
          "name": "Smith",
          "firstName": "Adam"
        },
        {
          "name": "Slade",
          "firstName": "Cutter"
        },
        {
          "name": "Marsh",
          "firstName": "Duke"
        },
        {
          "name": "Smith",
          "firstName": "Joe"
        },
        {
          "name": "Croft",
          "firstName": "Lara"
        },
        {
          "name": "Caulfield",
          "firstName": "Max"
        }
      ]
    }
  }
}
```

### 示例查询 — 其`_path`以特定前缀{#sample-wknd-all-adventures-cycling-path-filter}开头的所有冒险

所有`adventures`，其中`_path`开始具有特定前缀(`/content/dam/wknd/en/adventures/cycling`)。

**示例查询**

```xml
query {
  adventureList(
    filter: {
      _path: {
        _expressions: [
        {
          value: "/content/dam/wknd/en/adventures/cycling"
         _operator: STARTS_WITH
        }]
       }
    })
    {
    items {
      _path
    }
  }
}
```

**示例结果**

```xml
{
  "data": {
    "adventureList": {
      "items": [
        {
          "_path": "/content/dam/wknd/en/adventures/cycling-southern-utah/cycling-southern-utah"
        },
        {
          "_path": "/content/dam/wknd/en/adventures/cycling-tuscany/cycling-tuscany"
        }
      ]
    }
  }
}
```

### 查询示例 — 位于德国或瑞士的所有城市，人口在400000到999999之间{#sample-all-cities-d-ch-population}

此处筛选字段组合。 `AND`（隐式）用于选择`population`范围，而`OR`（显式）用于选择所需的城市。

**示例查询**

```xml
query {
  cityList(filter: {
    population: {
      _expressions: [
        {
          value: 400000
          _operator: GREATER_EQUAL
        }, {
          value: 1000000
          _operator: LOWER
        }
      ]
    },
    country: {
      _logOp: OR
      _expressions: [
        {
          value: "Germany"
        }, {
          value: "Switzerland"
        }
      ]
    }
  }) {
    items {
      name
      population
      country
    }
  }
}
```

**示例结果**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "Stuttgart",
          "population": 634830,
          "country": "Germany"
        },
        {
          "name": "Zurich",
          "population": 415367,
          "country": "Switzerland"
        }
      ]
    }
  }
}
```

### 示例查询 — 名称中包含SAN的所有城市，而不考虑{#sample-all-cities-san-ignore-case}

此查询询问所有名称中`SAN`的城市，而不论如何。

**示例查询**

```xml
query {
  cityList(filter: {
    name: {
      _expressions: [
        {
          value: "SAN"
          _operator: CONTAINS
          _ignoreCase: true
        }
      ]
    }
  }) {
    items {
      name
      population
      country
    }
  }
}
```

**示例结果**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "San Francisco",
          "population": 883306,
          "country": "USA"
        },
        {
          "name": "San Jose",
          "population": 1026350,
          "country": "USA"
        }
      ]
    }
  }
}
```

### 示例查询 — 对包含项的数组进行筛选，该项必须至少发生一次{#sample-array-item-occur-at-least-once}

此查询过滤器在数组上，项(`city:na`)必须至少发生一次。

**示例查询**

```xml
query {
  cityList(filter: {
    categories: {
      _expressions: [
        {
          value: "city:na"
          _apply: AT_LEAST_ONCE
        }
      ]
    }
  }) {
    items {
      name
      population
      country
      categories
    }
  }
}
```

**示例结果**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "San Francisco",
          "population": 883306,
          "country": "USA",
          "categories": [
            "city:beach",
            "city:na"
          ]
        },
        {
          "name": "San Jose",
          "population": 1026350,
          "country": "USA",
          "categories": [
            "city:na"
          ]
        }
      ]
    }
  }
}
```

### 示例查询 — 对精确数组值{#sample-array-exact-value}进行筛选

此查询过滤器精确数组值。

**示例查询**

```xml
query {
  cityList(filter: {
    categories: {
      _expressions: [
        {
          values: [
            "city:beach",
            "city:na"
          ]
        }
      ]
    }
  }) {
    items {
      name
      population
      country
      categories
    }
  }
}
```

**示例结果**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "San Francisco",
          "population": 883306,
          "country": "USA",
          "categories": [
            "city:beach",
            "city:na"
          ]
        }
      ]
    }
  }
}
```

### 嵌套内容片段的示例查询 — 至少有一个员工且姓名为“Smith” {#sample-companies-employee-smith}的所有公司

此查询说明了对`name` &quot;Smith&quot;的任何`person`的筛选，返回信息来自两个嵌套片段 — `company`和`employee`。

**示例查询**

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

**示例结果**

```xml
{
  "data": {
    "companyList": {
      "items": [
        {
          "name": "NextStep Inc.",
          "ceo": {
            "name": "Jobs",
            "firstName": "Steve"
          },
          "employees": [
            {
              "name": "Smith",
              "firstName": "Joe"
            },
            {
              "name": "Lincoln",
              "firstName": "Abraham"
            }
          ]
        }
      ]
    }
  }
}
```

### 嵌套内容片段的示例查询 — 所有员工均获得“Gamestar”奖{#sample-all-companies-employee-gamestar-award}的所有公司

此查询说明了跨三个嵌套片段（`company`、`employee`和`award`）进行筛选。

**示例查询**

```xml
query {
  companyList(filter: {
    employees: {
      _apply: ALL
      _match: {
        awards: {
          _match: {
            id: {
              _expressions: [
                {
                  value: "GS"
                  _operator:EQUALS
                }
              ]
            }
          }
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
        awards {
          id
          title
        }
      }
    }
  }
}
```

**示例结果**

```xml
{
  "data": {
    "companyList": {
      "items": [
        {
          "name": "Little Pony, Inc.",
          "ceo": {
            "name": "Smith",
            "firstName": "Adam"
          },
          "employees": [
            {
              "name": "Croft",
              "firstName": "Lara",
              "awards": [
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            },
            {
              "name": "Slade",
              "firstName": "Cutter",
              "awards": [
                {
                  "id": "GB",
                  "title": "Gameblitz"
                },
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            }
          ]
        }
      ]
    }
  }
}
```

### 元数据查询示例 — 列表标题为GB {#sample-metadata-awards-gb}的奖项的元数据

此查询说明了跨三个嵌套片段（`company`、`employee`和`award`）进行筛选。

**示例查询**

```xml
query {
  awardList(filter: {
      id: {
        _expressions: [
          {
            value:"GB"
          }
        ]
    }
  }) {
    items {
      _metadata {
        stringMetadata {
          name,
          value
        }
      }
      id
      title
    }
  }
}
```

**示例结果**

```xml
{
  "data": {
    "awardList": {
      "items": [
        {
          "_metadata": {
            "stringMetadata": [
              {
                "name": "title",
                "value": "Gameblitz Award"
              },
              {
                "name": "description",
                "value": ""
              }
            ]
          },
          "id": "GB",
          "title": "Gameblitz"
        }
      ]
    }
  }
}
```

## 使用WKND项目{#sample-queries-using-wknd-project}的示例查询

这些示例查询基于WKND项目。 这包括：

* 内容片段模型可在以下位置获取：
   `http://<hostname>:<port>/libs/dam/cfm/models/console/content/models.html/conf/wknd`

* 可从以下位置获得内容片段（和其他内容）：
   `http://<hostname>:<port>/assets.html/content/dam/wknd/en`

>[!NOTE]
>
>由于结果可以很广泛，因此没有在此再现。

### 具有指定属性{#sample-wknd-all-model-properties}的特定模型的所有内容片段的示例查询

此示例查询询问：

* 对于`article`类型的所有内容片段
* 和`author`属性。`path`

**示例查询**

```xml
{
  articleList {
    items {
      _path
      author
    }
  }
}
```

### 元数据{#sample-wknd-metadata}的示例查询

这位查询质问：

* 对于`adventure`类型的所有内容片段
* 元数据

**示例查询**

```xml
{
  adventureList {
    items {
      _path,
      _metadata {
        stringMetadata {
          name,
          value
        }
        stringArrayMetadata {
          name,
          value
        }
        intMetadata {
          name,
          value
        }
        intArrayMetadata {
          name,
          value
        }
        floatMetadata {
          name,
          value
        }
        floatArrayMetadata {
          name,
          value
        }
        booleanMetadata {
          name,
          value
        }
        booleanArrayMetadata {
          name,
          value
        }
        calendarMetadata {
          name,
          value
        }
        calendarArrayMetadata {
          name,
          value
        }
      }
    }
  }
}
```

### 给定模型{#sample-wknd-single-content-fragment-of-given-model}的单个内容片段的示例查询

此示例查询询问：

* 用于特定路径上类型`article`的单个内容片段
   * 其中，所有格式的内容：
      * HTML
      * Markdown
      * 纯文本
      * JSON

**示例查询**

```xml
{
  articleByPath (_path: "/content/dam/wknd/en/magazine/alaska-adventure/alaskan-adventures") {
    item {
        _path
        author
        main {
          html
          markdown
          plaintext
          json
        }
    }
  }
}
```

### 模型{#sample-wknd-content-fragment-model-from-model}中内容片段模型的示例查询

此示例查询询问：

* 用于单个内容片段
   * 基础内容片段模型的详细信息

**示例查询**

```xml
{
  adventureByPath(_path: "/content/dam/wknd/en/adventures/riverside-camping-australia/riverside-camping-australia") {
    item {
      _path
      adventureTitle
      _model {
        _path
        title
      }
    }
  }
}
```

### 嵌套内容片段的示例查询 — 单模型类型{#sample-wknd-nested-fragment-single-model}

这位查询质问：

* 用于特定路径上类型`article`的单个内容片段
   * 其中，引用（嵌套）片段的路径和作者

>[!NOTE]
>
>字段`referencearticle`的数据类型为`fragment-reference`。

**示例查询**

```xml
{
  articleByPath (_path: "/content/dam/wknd/en/magazine/skitouring/skitouring") {
    item {
        _path
        author
        referencearticle {
          _path
          author
      }
    }
  }
}
```

### 嵌套内容片段的示例查询 — 多模型类型{#sample-wknd-nested-fragment-multiple-model}

这位查询质问：

* `bookmark`类型的多个内容片段
   * with Fragment对特定模型类型`article`和`adventure`的其他片段的引用

>[!NOTE]
>
>字段`fragments`具有数据类型`fragment-reference`，并选择了模型`Article`、`Adventure`。

```xml
{
  bookmarkList {
    items {
        fragments {
          ... on ArticleModel {
            _path
            author
          }
          ... on AdventureModel {
            _path
            adventureTitle
          }
        }
     }
  }
}
```

### 包含内容引用的特定模型的内容片段的示例查询{#sample-wknd-fragment-specific-model-content-reference}

这种查询有两种风格：

1. 返回所有内容引用。
1. 返回类型`attachments`的特定内容引用。

这些查询质问：

* `bookmark`类型的多个内容片段
   * 包含对其他片段的内容引用

#### 具有预取引用{#sample-wknd-multiple-fragments-prefetched-references}的多个内容片段的示例查询

以下查询使用`_references`返回所有内容引用：

```xml
{
  bookmarkList {
     _references {
         ... on ImageRef {
          _path
          type
          height
        }
        ... on MultimediaRef {
          _path
          type
          size
        }
        ... on DocumentRef {
          _path
          type
          author
        }
        ... on ArchiveRef {
          _path
          type
          format
        }
    }
    items {
        _path
    }
  }
}
```

#### 附件{#sample-wknd-multiple-fragments-attachments}的多个内容片段的示例查询

以下查询返回所有`attachments` — 类型为`content-reference`的特定字段（子组）：

>[!NOTE]
>
>字段`attachments`具有数据类型`content-reference`，并选择了各种形式。

```xml
{
  bookmarkList {
    items {
      attachments {
        ... on PageRef {
          _path
          type
        }
        ... on ImageRef {
          _path
          width
        }
        ... on MultimediaRef {
          _path
          size
        }
        ... on DocumentRef {
          _path
          author
        }
        ... on ArchiveRef {
          _path
          format
        }
      }
    }
  }
}
```

### RTE内联引用{#sample-wknd-single-fragment-rte-inline-reference}的单个内容片段的示例查询

这位查询质问：

* 用于特定路径上类型`bookmark`的单个内容片段
   * 其中，RTE内联引用

>[!NOTE]
>
>RTE内联引用在`_references`中水合。

**示例查询**

```xml
{
  bookmarkByPath(_path: "/content/dam/wknd/en/bookmarks/skitouring") {
    item {
      _path
      description {
        json
      }
    }
    _references {
      ... on ArticleModel {
        _path
      }
      ... on AdventureModel {
        _path
      }
      ... on ImageRef {
        _path
      }
      ... on MultimediaRef {
        _path
      }
      ... on DocumentRef {
        _path
      }
      ... on ArchiveRef {
        _path
      }
    }
  }
}
```

### 给定模型{#sample-wknd-single-fragment-given-model}的单个内容片段变体的示例查询

这位查询质问：

* 用于特定路径上类型`article`的单个内容片段
   * 其中，与变量相关的数据：`variation1`

**示例查询**

```xml
{
  articleByPath (_path: "/content/dam/wknd/en/magazine/alaska-adventure/alaskan-adventures", variation: "variation1") {
    item {
      _path
      author
      main {
        html
        markdown
        plaintext
        json
      }
    }
  }
}
```

### 给定模型{#sample-wknd-variation-multiple-fragment-given-model}的命名内容片段变体的示例查询

这位查询质问：

* 对于类型为`article`且具有特定变量的内容片段：`variation1`

**示例查询**

```xml
{
  articleList (variation: "variation1") {
    items {
      _path
      author
      main {
        html
        markdown
        plaintext
        json
      }
    }
  }
}
```

### 给定区域设置{#sample-wknd-multiple-fragments-given-locale}的多个内容片段的示例查询

这位查询质问：

* 对于`fr`区域设置中类型`article`的内容片段

**示例查询**

```xml
{ 
  articleList (_locale: "fr") {
    items {
      _path
      author
      main {
        html
        markdown
        plaintext
        json
      }
    }
  }
}
```

## 示例内容片段结构（与GraphQL一起使用）{#content-fragment-structure-graphql}

示例查询基于以下结构，其使用：

* 一个或多个[示例内容片段模型](#sample-content-fragment-models-schemas) — 构成GraphQL模式的基础

* [基于上](#sample-content-fragments) 述模型的示例内容片段

### 示例内容片段模型(模式){#sample-content-fragment-models-schemas}

对于示例查询，我们将使用以下内容模型及其相互关系（引用 — >）：

* [公司](#model-company)
-> [人](#model-person)
    -> [奖](#model-award)

* [城市](#model-city)

#### 公司 {#model-company}

定义公司的基本字段有：

| 字段名称 | 数据类型 | 针对开发人员的 Adobe AIR API 参考 |
|--- |--- |--- |
| 公司名称 | 单行文本 |  |
| 首席执行官 | 片段引用（单个） | [人员](#model-person) |
| 员工 | 片段引用（多字段） | [人员](#model-person) |

#### 人员 {#model-person}

定义人员（也可以是员工）的字段：

| 字段名称 | 数据类型 | 针对开发人员的 Adobe AIR API 参考 |
|--- |--- |--- |
| 名称 | 单行文本 |  |
| 名字 | 单行文本 |  |
| 奖项 | 片段引用（多字段） | [奖项](#model-award) |

#### 奖项{#model-award}

定义奖励的字段包括：

| 字段名称 | 数据类型 | 针对开发人员的 Adobe AIR API 参考 |
|--- |--- |--- |
| 快捷键/ID | 单行文本 |  |
| 标题 | 单行文本 |  |

#### 城市 {#model-city}

用于定义城市的字段有：

| 字段名称 | 数据类型 | 针对开发人员的 Adobe AIR API 参考 |
|--- |--- |--- |
| 名称 | 单行文本 |  |
| 国家/地区 | 单行文本 |  |
| 人口 | 数字 |  |
| 类别 | 标记 |  |

### 示例内容片段{#sample-content-fragments}

以下片段用于相应的模型。

#### 公司 {#fragment-company}

| 公司名称 | 首席执行官 | 员工 |
|--- |--- |--- |
| Apple | 史蒂夫·乔布斯 | 杜克·马什<br>马克斯·考尔菲尔德 |
|  小马 | 亚当·斯密 | Lara Croft<br>Cutter Slade |
| NextStep Inc. | 史蒂夫·乔布斯 | 乔·史密斯<br>亚伯·林肯 |

#### 人员 {#fragment-person}

| 名称 | 名字 | 奖项 |
|--- |--- |--- |
| 林肯 |  阿部 |  |
| 史密斯 | Adam |   |
| 斯莱德 |  刀具 |  Gameblitz<br>Gamestar |
| 马什 |  杜克 |   |   |
|  史密斯 |  乔 |   |
| 克罗夫特 |  拉拉 | Gamestar |
| Caulfield |  最大 |  加梅布利茨 |
|  作业 |  Steve |   |

#### 奖项{#fragment-award}

| 快捷键/ID | 标题 |
|--- |--- |
| GB | 加梅布利茨 |
|  GS | Gamestar |
|  OSC | 奥斯卡 |

#### 城市 {#fragment-city}

| 名称 | 国家/地区 | 人口 | 类别 |
|--- |--- |--- |--- |
| Basel | 瑞士 | 172258 | 城市：emea |
| 柏林 | 德国 | 3669491 | city:capital<br>city:emea |
| 布加勒斯特 | 罗马尼亚 | 1821000 |  city:capital<br>city:emea |
| San Francisco |  美国 |  883306 |  city:beach<br>city:na |
| 圣何塞 |  美国 |  102635 |  城市：纳 |
| 斯图加特 |  德国 |  634830 |  城市：emea |
|  苏黎世 |  瑞士 |  415367 |  city:capital<br>city:emea |
