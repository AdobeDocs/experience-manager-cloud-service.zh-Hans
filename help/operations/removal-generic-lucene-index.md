---
title: 通用Lucene索引删除
description: 了解计划删除的通用Lucene索引以及可能受到的影响。
exl-id: 3b966d4f-6897-406d-ad6e-cd5cda020076
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '1345'
ht-degree: 0%

---

# 通用Lucene索引删除 {#generic-lucene-index-removal}

Adobe打算删除“通用Lucene”索引(`/oak:index/lucene-*`)从Adobe Experience Manager as a Cloud Service访问。 自AEM 6.5起，此索引已被弃用。本文档介绍了此决策的影响，并详细描述了如何检查AEM实例是否受到影响。 它还包含更改查询的方法，以便它们在没有通用Lucene索引的情况下继续运行。

## 背景 {#background}

在AEM中，全文查询是指使用以下函数的查询：

* `jcr:contains()` 在JCR XPATH中
* `CONTAINS` JCR-SQL2内容

如果不使用索引，此类查询无法返回结果。 与仅包含路径或属性限制的查询不同，包含全文限制的查询将始终返回零结果，因为其中找不到索引（因此执行遍历）。

通用Lucene索引(`/oak:index/lucene-*`)自AEM 6.0 / Oak 1.0之后已经存在，用于提供跨大多数存储库层次结构的全文搜索，不过也有一些路径，例如 `/jcr:system` 和 `/var` 一直被排除在外。 但是，此索引在很大程度上已被更具体节点类型的索引所取代(例如， `damAssetLucene-*` 对于 `dam:Asset` 节点类型)，支持全文和属性搜索。

在AEM 6.5中，通用Lucene索引被标记为已弃用，这表示它将在未来版本中删除。 从那时起，当使用索引时，会记录WARN，如以下日志片段所示：

```text
org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'search term') and isdescendantnode(a, '/content/mysite') /* xpath: /jcr:root/content/mysite//*[jcr:contains(.,"search term")] */ fullText="search" "term", path=/content/mysite//*). Change the query or the index definitions.
```

在近期AEM版本中，通用Lucene索引已用于支持极少数功能。 正在对这些索引进行重新处理以使用其他索引，或者进行其他修改以移除对此索引的依赖关系。

例如，引用查找查询（如以下示例中的）现在应使用位于的索引 `/oak:index/pathreference`，仅索引 `String` 与查找JCR路径的正则表达式匹配的属性值。

```text
//*[jcr:contains(., '"/content/dam/mysite"')]
```

为了支持更大的客户数据卷，Adobe不再在新的AEMas a Cloud Service环境中创建通用Lucene索引。 此外，Adobe会从现有存储库中删除索引。 [查看时间线](#timeline) ，以了解更多详细信息。

Adobe已透过以下方式调整指数成本： `costPerEntry` 和 `costPerExecution` 属性以确保其他索引 `/oak:index/pathreference` 会尽可能优先使用。

如果客户应用程序使用的查询仍依赖于此索引，则应立即更新以使用其他现有索引，如有必要，可以自定义这些索引。 或者，可以向客户应用程序添加新自定义索引。 有关AEMas a Cloud Service中索引管理的完整说明，请参阅 [索引文档](/help/operations/indexing.md).

## 您是否受影响？ {#are-you-affected}

如果没有其他全文索引可以为查询提供服务，则通用Lucene索引当前用作回退。 使用此已弃用的索引时，会在WARN级别记录一条类似于以下内容的消息：

```text
org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') /* xpath: //*[jcr:contains(.,"test")] */ fullText="test", path=*). Change the query or the index definitions.
```

在某些情况下，Oak可能会尝试使用其他全文索引(例如 `/oak:index/pathreference`)以支持全文查询，但如果查询字符串与索引定义上的正则表达式不匹配，则会在WARN级别记录消息，并且查询可能不会返回结果。

```text
org.apache.jackrabbit.oak.query.QueryImpl Potentially improper use of index /oak:index/pathReference with queryFilterRegex (["']|^)/ to search for value "test"
```

删除通用Lucene索引后，如果全文查询无法找到任何合适的索引定义，则会在WARN级别记录如下所示的消息：

```text
org.apache.jackrabbit.oak.query.QueryImpl Fulltext query without index for filter Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') /* xpath: //*[jcr:contains(.,"test")] */ fullText="test", path=*); no results are returned
```

>[!IMPORTANT]
>
>**需要客户操作**
>
> 如果上述任何警告消息被记录，您可能需要重新处理查询以使用不同的全文索引，或提供新索引来支持查询。
>
>以下部分提供了有关您可能会看到的依赖项类型以及如何解决这些类型的详细信息。

## 对通用Lucene索引的潜在依赖性 {#potential-dependencies}

在一些方面，您的应用程序和AEM安装可能依赖于创作实例和发布实例的通用Lucene索引。

### 发布实例 {#publish-instance}

#### 自定义应用程序查询 {#custom-application-queries}

在发布实例上使用通用Lucene索引的查询最常见的是自定义应用程序查询。

在最简单的情况下，这些查询可能未指定节点类型，这意味着 `nt:base` 或 `nt:base` 已显式指定，例如：

```text
/jcr:root/content/mysite//*[jcr:contains(., 'search term')]
/jcr:root/content/mysite//element(*, nt:base)[jcr:contains(., 'search term')]
```

>[!IMPORTANT]
>
>**需要客户操作**
>
>应修改上述查询以使用适当的节点类型，如下节所述。

例如，可以修改查询以返回与页面或下的任何聚合匹配的结果 `cq:Page node`. 因此，查询可以变为：

```text
/jcr:root/content/mysite//element(*, cq:Page)[jcr:contains(., 'search term')]
```

在其他情况下，查询可能会指定节点类型，但包含其他全文索引无法处理的全文限制，例如：

```text
/jcr:root/content/dam//element(*, dam:Asset)[jcr:contains(jcr:content/metadata/@cq:tags, 'NewsTopics:cateogries/domestic'))]
```

在这种情况下，查询具有 `dam:Asset` 节点类型，但包含对相对节点的全文限制 `jcr:content/metadata/@cq:tags` 属性。

此属性未标记为在中分析 `damAssetLucene` index，最常用于对 `dam:Asset` 节点类型。 因此，此索引不能用于此查询。

因此，查询回退到常规全文索引，其中所有包含的属性均标记为已由 `/oak:index/lucene-2/indexRules/nt:base/properties/prop`.

>[!IMPORTANT]
>
>**需要客户操作**
>
>标记 `jcr:content/metadata/@cq:tags` 在的自定义版本中分析的属性 `damAssetLucene` 索引导致此查询正由此索引处理，并且不记录WARN。

### 创作实例 {#author-instance}

除了在客户应用程序servlet、OSGi组件和渲染脚本中进行的查询之外，通用Lucene索引还可以有几个作者特定的用法。

#### 引用搜索 {#reference-search}

以前，通用Lucene索引用于支持引用搜索或搜索包含对另一内容路径的引用的内容。 此类查询应该已经更新为使用新的 `/oak:index/pathreference` 索引。

#### 路径字段选取器搜索 {#picker-search}

AEM包含一个具有Sling资源类型的自定义对话框组件 `granite/ui/components/coral/foundation/form/pathfield`，它提供了一个浏览器/选取器，用于选择其他AEM路径。 默认路径字段选取器，无自定义设置时使用 `pickerSrc` 属性在内容结构中定义，在弹出对话框中呈现搜索栏。

可以使用指定搜索的节点类型 `nodeTypes` 属性。

目前，如果没有 `nodeTypes` 属性存在，则基础搜索查询将使用 `nt:base` 节点类型，因此可能使用通用Lucene索引，通常记录类似于以下内容的WARN消息。

```text
20.01.2022 18:56:06.412 *WARN* [127.0.0.1 [1642704966377] POST /mnt/overlay/granite/ui/content/coral/foundation/form/pathfield/picker.result.single.html HTTP/1.1] org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') and isdescendantnode(a, '/content') /* xpath: /jcr:root/content//element(*, nt:base)[(jcr:contains(., 'test'))] order by @jcr:score descending */ fullText="test", path=/content//*). Change the query or the index definitions.
```

在删除通用Lucene索引之前， `pathfield` 将更新组件，以便使用默认选取器的组件隐藏搜索框，默认选取器不提供 `nodeTypes` 属性。

| 包含搜索的路径字段选取器 | 不搜索路径字段选取器 |
|---|---|
| ![包含搜索的路径字段选取器](assets/index-pathfield-picker-with-search.png) | ![不搜索路径字段选取器](assets/index-pathfield-picker-without-search.png) |

>[!IMPORTANT]
>
>**需要客户操作**
>
>如果客户希望在路径字段选取器中保留搜索功能， `nodeTypes` 应提供属性，其中列出要查询的节点类型。 这些节点类型可以指定为以逗号分隔的 `String` 属性。 如果不需要搜索，则无需客户执行任何操作。

>[!NOTE]
>
>内容片段模型编辑器使用具有Sling资源类型的专用路径字段 `dam/cfm/models/editor/components/contentreference`.
>
> * 目前，这些程序执行查询时未指定节点类型，导致由于使用通用Lucene索引而记录WARN。
> * 这些组件的实例将很快自动默认为使用 `cq:Page` 和 `dam:Asset` 节点类型，无需客户执行进一步的操作。
> * 此 `nodeTypes` 可以添加属性以覆盖这些默认节点类型。

## 通用Lucene删除时间线 {#timeline}

Adobe将采取两阶段方法移除通用Lucene索引。

* **阶段1** （计划于2022年1月31日开始）：不再创建 `/oak:index/lucene-*` 在新的AEMas a Cloud Service环境中。
* **阶段2** （计划于2022年3月31日开始）：删除 `/oak:index/lucene-*` 从现有AEMas a Cloud Service环境编制索引。

Adobe将监测上述日志消息，并尝试联系仍依赖于通用Lucene索引的客户。

作为短期的缓解措施，Adobe将自定义索引定义直接添加到客户系统，以防止在必要时删除通用Lucene索引导致的功能或性能问题。

在这种情况下，会向客户提供更新的索引定义，并建议他们将该定义包含在通过Cloud Manager发布的未来应用程序版本中。
