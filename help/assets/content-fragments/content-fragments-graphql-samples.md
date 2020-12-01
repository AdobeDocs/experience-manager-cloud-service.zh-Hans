---
title: 学习将GraphQL与AEM结合使用——示例内容和查询
description: 学习将GraphQL与AEM结合使用——示例内容和查询。
translation-type: tm+mt
source-git-commit: 46e179faa7875c4b3e9da30356d2b82d4b25b130
workflow-type: tm+mt
source-wordcount: '1283'
ht-degree: 6%

---


# 学习将GraphQL与AEM结合使用——示例内容和查询{#learn-graphql-with-aem-sample-content-queries}

>[!CAUTION]
>
>针对内容片段投放的AEM GraphQL API将于2021年初发布。
>
>相关文档已经可供预览使用。

要开始使用GraphQL查询以及它们如何使用AEM内容片段，查看一些实际示例会有所帮助。

要获得此帮助，请参阅：

* A [示例内容片段结构](#content-fragment-structure-graphql)

* 以及某些[示例GraphQL查询](#graphql-sample-queries)，基于示例内容片段结构（内容片段模型和相关内容片段）。

## GraphQL for AEM —— 某些扩展{#graphql-some-extensions}

使用GraphQL for AEM的查询的基本操作符合标准的GraphQL规范。 对于具有AEM的GraphQL查询，有以下几个扩展：

* 如果您需要一个结果：
   * 使用模型名称；eg city

* 如果您希望获得一列表结果：
   * 在模型名称中添加“列表”;例如`cityList`

* 如果要使用逻辑OR:
   * 使用&quot; _logOp:或

* 逻辑AND也存在，但是是（通常）隐式

* 您可以查询与内容片段模型中的字段对应的字段名称

* 除了模型中的字段之外，还有一些系统生成的字段（以下划线为前面）:

   * 对于内容：

      * `_locale` :去揭示语言；基于语言管理器

      * `_metadata` :显示片段的元数据

      * `_path` :存储库中内容片段的路径

      * `_references` :显示引用；包括富文本编辑器中的内联引用

      * `_variations` :以显示内容片段中的特定变量
   * 运营：

      * `_operator` :应用特定运营商； `EQUALS`,  `EQUALS_NOT`,  `GREATER_EQUAL`,  `LOWER`,  `CONTAINS`

      * `_apply` :适用特定条件；例如，   `AT_LEAST_ONCE`

      * `_ignoreCase` :在查询时忽略大小写


* 支持GraphQL合并类型：

   * 使用`...on`


## 与GraphQL {#content-fragment-structure-graphql}一起使用的示例内容片段结构

对于简单的示例，我们需要：

* 一个或多个[示例内容片段模型](#sample-content-fragment-models-schemas) —— 构成GraphQL模式的基础

* [基于上](#sample-content-fragments) 述模型的示例内容片段

### 示例内容片段模型(模式){#sample-content-fragment-models-schemas}

对于示例查询，我们将使用以下内容模型及其相互关系（引用->）:

* [公司](#model-company)
-> [人物](#model-person)
    ->奖 [项](#model-award)

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
|  小马公司 | 亚当·斯密 | Lara Croft<br>Cutter Slade |
| NextStep Inc. | 史蒂夫·乔布斯 | 乔·史密斯<br>阿贝·林肯 |

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
| Basel | 瑞士 | 172258 | 城市： emea |
| 柏林 | 德国 | 3669491 | 城市：首都<br>城市：emea |
| 布加勒斯特 | 罗马尼亚 | 1821000 |  城市：首都<br>城市：emea |
| San Francisco |  美国 |  883306 |  城市：海滩<br>城市：na |
| 圣何塞 |  美国 |  102635 |  城市：纳 |
| 斯图加特 |  德国 |  634830 |  城市： emea |
|  苏黎世 |  瑞士 |  415367 |  城市：首都<br>城市：emea |

## GraphQL —— 使用示例内容片段结构{#graphql-sample-queries-sample-content-fragment-structure}的示例查询

有关创建查询的插图，请参阅示例查询以及示例结果。

>[!NOTE]
>
>根据您的实例，您可以直接访问AEM GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md#graphiql-interface)附带的[Graph *i* QL接口，以提交和测试查询。
>
>例如：`http://localhost:4502/content/graphiql.html`

### 示例查询-所有可用模式和数据类型{#sample-all-schemes-datatypes}

这将返回所有可用模式的所有类型。

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

### 示例查询-所有城市信息{#sample-all-information-all-cities}

要检索有关所有城市的所有信息，您可以使用非常基本的查询:
**示例查询**

```xml
{
  cityList {
    items
  }
}
```

执行时，系统将自动扩展查询以包含所有字段：

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

### 示例查询-所有城市名称{#sample-names-all-cities}

这是返回`city`查询中所有条目的`name`的直接模式。

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

### 示例查询-单个城市片段{#sample-single-city-fragment}

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

### 示例查询-具有命名变体{#sample-cities-named-variation}的所有城市

如果为`city`柏林新建一个名为“柏林中心”(`berlin_centre`)的变体，则可以使用查询返回变体的详细信息。

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

### 示例查询-名称为“Jobs”或“Smith” {#sample-all-persons-jobs-smith}的所有人员

这将过滤所有名为`Jobs`或`Smith`的`persons`。

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

### 示例查询-所有姓名不为“Jobs”{#sample-all-persons-not-jobs}的人员

这将过滤所有名为`Jobs`或`Smith`的`persons`。

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

### 查询示例——位于德国或瑞士人口在400000到99999之间的所有城市{#sample-all-cities-d-ch-population}

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

### 示例查询-名称中包含SAN的所有城市，无论大小写{#sample-all-cities-san-ignore-case}

此查询询问名称`SAN`的所有城市，无论如何。

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

### 示例查询-对具有项的数组进行筛选，该项必须至少发生一次{#sample-array-item-occur-at-least-once}

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

### 示例查询-对精确数组值{#sample-array-exact-value}进行筛选

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

### 嵌套内容片段的示例查询-至少有一个名为“Smith” {#sample-companies-employee-smith}的员工的所有公司

此查询说明了对`name` &quot;Smith&quot;的任何`person`的筛选，从两个嵌套片段返回信息- `company`和`employee`。

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

### 嵌套内容片段的示例查询-所有员工均获得“Gamestar”奖{#sample-all-companies-employee-gamestar-award}的所有公司

此查询说明了跨三个嵌套片段的筛选- `company`、`employee`和`award`。

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

### 元数据查询示例-列表标题为GB {#sample-metadata-awards-gb}的奖项的元数据

此查询说明了跨三个嵌套片段的筛选- `company`、`employee`和`award`。

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

这些示例查询基于WKND项目。

>[!NOTE]
>
>由于结果可以很广泛，因此在此处不再重复这些结果。

### 具有指定属性{#sample-wknd-all-model-properties}的特定模型的所有内容片段的示例查询

此示例查询询问：

* 对于类型`article`的所有内容片段
* 和`path`属性。`author`

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

* 对于类型`adventure`的所有内容片段
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

* 对于给定模型的单个内容片段
* 对于所有格式的内容：
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

### 嵌套内容片段的示例查询-单模型类型{#sample-wknd-nested-fragment-single-model}

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

### 嵌套内容片段的示例查询-多模型类型{#sample-wknd-nested-fragment-multiple-model}

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

### 具有内容引用的特定模型的内容片段的示例查询{#sample-wknd-fragment-specific-model-content-reference}

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

### 预取引用{#sample-wknd-multiple-fragments-prefetched-references}的多个内容片段的示例查询

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
  }
}
```

### 给定模型{#sample-wknd-single-fragment-given-model}的单个内容片段变体的示例查询

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

### 给定区域设置{#sample-wknd-multiple-fragments-given-locale}的多个内容片段的示例查询

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

### RTE内联引用{#sample-wknd-single-fragment-rte-inline-reference}的单个内容片段的示例查询

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

### 给定模型{#sample-wknd-variation-multiple-fragment-given-model}的多个内容片段的命名变体的示例查询

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
