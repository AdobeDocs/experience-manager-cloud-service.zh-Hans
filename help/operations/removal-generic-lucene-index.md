---
title: 删除通用Lucene索引
description: 了解计划删除通用Lucene索引以及您可能受到的影响。
exl-id: fe0e00ac-f9c8-43cf-83c2-5a353f5eaeab
source-git-commit: 7a3c8b59a5a642ffc335fc80898fb956221cfcc2
workflow-type: tm+mt
source-wordcount: '1349'
ht-degree: 0%

---


# 删除通用Lucene索引 {#generic-lucene-index-removal}

Adobe打算删除“通用Lucene”索引(`/oak:index/lucene-*`)来自Adobe Experience Manager as a Cloud Service。 此索引自AEM 6.5起便已被弃用。在本文档中，介绍了此决策的影响，以及如何检查AEM实例是否受到影响的详细说明。 它还包含更改查询的方法，以便它们在没有通用Lucene索引的情况下继续运行。

## 背景 {#background}

在AEM中，全文查询是使用以下函数的查询：

* `jcr:contains()` 在JCR XPATH中
* `CONTAINS` 在JCR-SQL2中

如果不使用索引，此类查询将无法返回结果。 与仅包含路径或属性限制的查询不同，包含全文限制且找不到索引（因此执行遍历）的查询将始终返回零结果。

通用Lucene索引(`/oak:index/lucene-*`)自AEM 6.0 / Oak 1.0起便已存在，以便在存储库的大多数层级中提供全文搜索，但有些路径(例如 `/jcr:system` 和 `/var` 一直被排除在此之外。 但是，此索引在很大程度上已被更具体节点类型上的索引(例如， `damAssetLucene-*` 对于 `dam:Asset` 节点类型)，该类型支持全文和属性搜索。

在AEM 6.5中，通用Lucene索引被标记为已弃用，这表示将在未来版本中删除该索引。 此后，当使用索引时，即会记录“警告”，如以下日志代码片段所示：

```text
org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'search term') and isdescendantnode(a, '/content/mysite') /* xpath: /jcr:root/content/mysite//*[jcr:contains(.,"search term")] */ fullText="search" "term", path=/content/mysite//*). Please change the query or the index definitions.
```

In recent AEM versions, the generic Lucene index has been used to support a very small number of features. 这些索引正在重新工作以使用其他索引，或者正在修改以删除对此索引的依赖关系。

例如，引用查找查询（如以下示例中的）现在应使用 `/oak:index/pathreference`，仅对其进行索引 `String` 与查找JCR路径的正则表达式匹配的属性值。

```text
//*[jcr:contains(., '"/content/dam/mysite"')]
```

为了支持较大的客户数据卷，Adobe将不再在新的AEMas a Cloud Service环境中创建通用Lucene索引。 此外，Adobe将开始从现有存储库中删除索引。 [查看时间轴](#timeline) 的详细信息。

Adobe已通过 `costPerEntry` 和 `costPerExecution` 属性，以确保其他索引，例如 `/oak:index/pathreference` 会尽可能优先使用。

Customer applications which use queries which still depend on this index should be updated immediately to leverage other existing indexes, which can be customized if required. 或者，也可以将新的自定义索引添加到客户应用程序。 有关AEMas a Cloud Service中索引管理的完整说明，请参阅 [索引文档。](/help/operations/indexing.md)

## 你受影响了吗？ {#are-you-affected}

如果没有其他全文索引可以为查询提供服务，则当前使用通用Lucene索引作为回退。 使用此已弃用索引时，将在“警告”级别记录如下消息：

```text
org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') /* xpath: //*[jcr:contains(.,"test")] */ fullText="test", path=*). Please change the query or the index definitions.
```

在某些情况下，Oak可能会尝试使用其他全文索引(例如 `/oak:index/pathreference`)以支持全文查询，但如果查询字符串与索引定义中的正则表达式不匹配，则将在WARN级别记录一条消息，并且查询可能不会返回结果。

```text
org.apache.jackrabbit.oak.query.QueryImpl Potentially improper use of index /oak:index/pathReference with queryFilterRegex (["']|^)/ to search for value "test"
```

删除通用Lucene索引后，如果全文查询无法找到任何合适的索引定义，则将在“警告”级别记录如下所示的消息：

```text
org.apache.jackrabbit.oak.query.QueryImpl Fulltext query without index for filter Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') /* xpath: //*[jcr:contains(.,"test")] */ fullText="test", path=*); no results will be returned
```

>[!IMPORTANT]
>
>**需要客户操作**
>
> 如果记录了上述任何警告消息，您可能需要重新编写查询以使用不同的全文索引，或提供新索引以支持查询。
>
>以下部分提供了您可能看到的依赖关系类型以及如何解决这些依赖关系的详细信息。

## 对通用Lucene索引的潜在依赖关系 {#potential-dependencies}

在许多方面，您的应用程序和AEM安装可能都依赖于创作实例和发布实例上的通用Lucene索引。

### 发布实例 {#publish-instance}

#### 自定义应用程序查询 {#custom-application-queries}

在发布实例中使用通用Lucene索引的查询最常见的来源是自定义应用程序查询。

在最简单的情况下，这些查询可能是未指定节点类型的查询，这表示 `nt:base` 或 `nt:base` 明确指定，例如：

```text
/jcr:root/content/mysite//*[jcr:contains(., 'search term')]
/jcr:root/content/mysite//element(*, nt:base)[jcr:contains(., 'search term')]
```

>[!IMPORTANT]
>
>**需要客户操作**
>
>上述查询应修改为使用相应的节点类型，如以下章节所述。

For example, the queries can be modified to return results matching pages or any of the aggregates beneath the `cq:Page node`. 因此，查询可能变为：

```text
/jcr:root/content/mysite//element(*, cq:Page)[jcr:contains(., 'search term')]
```

在其他情况下，查询可能会指定节点类型，但包含无法由其他全文索引处理的全文限制，例如：

```text
/jcr:root/content/dam//element(*, dam:Asset)[jcr:contains(jcr:content/metadata/@cq:tags, 'NewsTopics:cateogries/domestic'))]
```

在这种情况下，查询具有 `dam:Asset` 节点类型，但包含对 `jcr:content/metadata/@cq:tags` 属性。

此属性未在 `damAssetLucene` index，全文索引，最常用于针对 `dam:Asset` 节点类型。 因此，此索引不能用于此查询。

因此，查询会返回到通用全文索引中，其中所有包含的属性都将标记为由通配符匹配(在 `/oak:index/lucene-2/indexRules/nt:base/properties/prop`.

>[!IMPORTANT]
>
>**需要客户操作**
>
>标记 `jcr:content/metadata/@cq:tags` 在的自定义版本中分析的属性 `damAssetLucene` 索引将导致此查询由此索引处理，并且不记录任何警告。

### 创作实例 {#author-instance}

除了客户应用程序Servlet、OSGi组件和渲染脚本中的查询之外，通用Lucene索引还有许多特定于作者的用法。

#### 引用搜索 {#reference-search}

以前，通用的Lucene索引用于支持引用搜索或搜索包含对其他内容路径的引用的内容。 此类查询应已更新，以使用新 `/oak:index/pathreference` 索引。

#### 路径字段选取器搜索 {#picker-search}

AEM includes a custom dialog component with the Sling resource type `granite/ui/components/coral/foundation/form/pathfield`, which provides a browser/picker for selecting another AEM path. 默认路径字段选取器，在无自定义时使用 `pickerSrc` 属性在内容结构中定义，在弹出式对话框中呈现搜索栏。

可使用指定要搜索的节点类型 `nodeTypes` 属性。

目前，如果没有 `nodeTypes` 属性存在，则基础搜索查询将使用 `nt:base` 节点类型，因此可能使用通用Lucene索引，通常记录类似于以下内容的WARN消息。

```text
20.01.2022 18:56:06.412 *WARN* [127.0.0.1 [1642704966377] POST /mnt/overlay/granite/ui/content/coral/foundation/form/pathfield/picker.result.single.html HTTP/1.1] org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') and isdescendantnode(a, '/content') /* xpath: /jcr:root/content//element(*, nt:base)[(jcr:contains(., 'test'))] order by @jcr:score descending */ fullText="test", path=/content//*). Please change the query or the index definitions.
```

Prior to removal of the generic Lucene index, the `pathfield` component will be updated so that the search box is hidden for components using the default picker, which do not provide a `nodeTypes` property.

| 搜索路径字段选取器 | 不搜索的路径字段选取器 |
|---|---|
| ![搜索路径字段选取器](assets/index-pathfield-picker-with-search.png) | ![不搜索的路径字段选取器](assets/index-pathfield-picker-without-search.png) |

>[!IMPORTANT]
>
>**需要客户操作**
>
>如果客户希望保留路径字段选取器中的搜索功能，则 `nodeTypes` 应提供属性，其中列出了要查询的节点类型。 这些节点类型可以指定为 `String` 属性。 如果不需要搜索，则客户无需执行任何操作。

>[!NOTE]
>
>内容片段模型编辑器使用具有Sling资源类型的专用路径字段 `dam/cfm/models/editor/components/contentreference`.
> * 目前，这些查询在未指定节点类型的情况下执行查询，由于使用通用Lucene索引，导致记录WARN。
> * 这些组件的实例很快会自动默认使用 `cq:Page` 和 `dam:Asset` 节点类型，而无需进一步执行客户操作。
> * 的 `nodeTypes` 可以添加属性以覆盖这些默认节点类型。


## 删除通用Lucene的时间轴 {#timeline}

Adobe将采取两阶段方法来删除通用Lucene索引。

* **阶段1** （计划于2022年1月31日开始）：不再创建 `/oak:index/lucene-*` 在新的AEMas a Cloud Service环境中。
* **阶段2** （计划于2022年3月31日开始）：删除 `/oak:index/lucene-*` 从现有AEMas a Cloud Service环境中编入索引。

Adobe将监控上述日志消息，并尝试联系仍依赖通用Lucene索引的客户。

As a short term mitigation, Adobe will add custom index definitions directly to customer systems to prevent functional or performance issues as a result of the removal of the generic Lucene index as necessary.

在这种情况下，客户将获得更新的索引定义，并建议通过Cloud Manager将其包含在其应用程序的未来版本中。
