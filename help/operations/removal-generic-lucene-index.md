---
title: 删除通用lucene索引
description: 删除通用lucene索引
exl-id: fe0e00ac-f9c8-43cf-83c2-5a353f5eaeab
source-git-commit: bc7ef6567ad5baa4becd28a7e7d96bd6b579e1ad
workflow-type: tm+mt
source-wordcount: '1305'
ht-degree: 0%

---

# 删除“通用lucene”索引

Adobe打算删除“通用lucene”索引(`/oak:index/lucene-*`)来自Adobe Experience Manager as a Cloud Service。 此索引自AEM 6.5起便已被弃用。在本文档中，介绍了此决策的影响，以及如何检查AEM实例是否受到影响的详细说明。 最后，它包含更改查询的方法，以便在不存在此索引的情况下使用查询。

## 背景

在AEM中，“fulltext”查询与使用以下函数的查询一样：

* `jcr:contains()` 在JCR XPATH中
* `CONTAINS` 在JCR-SQL2中

如果不使用索引，此类查询将无法返回结果。 与仅包含路径或属性限制的查询不同，包含全文限制的查询将始终返回0个结果，该限制找不到索引（因此执行遍历）。

“通用lucene”索引(`/oak:index/lucene-*`)自AEM 6.0 / Oak 1.0起便已存在，以便在大多数存储库层次结构(某些路径，例如 `/jcr:system` 和 `/var` 一直被排除在此之外)，但是，此索引在很大程度上被更具体节点类型(例如， `damAssetLucene-*` （适用于同时支持全文和属性搜索的“dam:Asset”节点类型）。

在AEM 6.5中，“generic lucene”索引被标记为已弃用（表示将在未来版本中删除该索引），自此，在使用该索引时便记录了警告：

```
org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'search term') and isdescendantnode(a, '/content/mysite') /* xpath: /jcr:root/content/mysite//*[jcr:contains(.,"search term")] */ fullText="search" "term", path=/content/mysite//*). Please change the query or the index definitions.
```

在最新的AEM版本中，“通用lucene”索引用于支持非常少的功能。 这些索引正在重新工作以使用其他索引，或者正在修改以删除对此索引的依赖关系。
例如，下面所示格式的“引用查找”查询现在应使用“/oak:index/pathreference”的索引（该索引仅对与查找JCR路径的正则表达式匹配的字符串属性值进行索引）。 

```
//*[jcr:contains(., '"/content/dam/mysite"')]
```

为了支持较大的客户数据卷，Adobe将不再在新的AEMas a Cloud Service环境中创建“通用lucene”索引，并且在此之后，将开始从现有存储库中删除该索引。 我们已经调整了索引成本计数（通过“costPerEntry”和“costPerExecution”属性），以确保其他索引(例如 `/oak:index/pathreference`)优先用于 `/oak:index/lucene-*` 尽可能。 

使用查询的客户应用程序仍然依赖于此索引，应立即更新以利用其他现有索引（如果需要，可以自定义），或者应将新的自定义索引添加到客户应用程序。 有关AEMas a Cloud Service中索引管理的完整说明，请访问 [索引文档](/help/operations/indexing.md).

## 如何判断您的应用程序是否依赖于“通用lucene”索引？

如果没有其他全文索引可以为查询服务，则“generic lucene”索引当前用作“回退”。 使用此已弃用索引时，将在“警告”级别记录如下消息：

```
org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') /* xpath: //*[jcr:contains(.,"test")] */ fullText="test", path=*). Please change the query or the index definitions.
```

在某些情况下，Oak可能会尝试使用其他全文索引(例如 `/oak:index/pathreference`)以支持全文查询，但如果查询字符串与索引定义中的正则表达式不匹配，则将在WARN级别记录一条消息，并且该查询可能不会返回结果。

```
org.apache.jackrabbit.oak.query.QueryImpl Potentially improper use of index /oak:index/pathReference with queryFilterRegex (["']|^)/ to search for value "test"
```

删除“通用lucene”索引后，如果全文查询无法找到任何合适的索引定义，则将在“警告”级别记录如下所示的消息：

```
org.apache.jackrabbit.oak.query.QueryImpl Fulltext query without index for filter Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') /* xpath: //*[jcr:contains(.,"test")] */ fullText="test", path=*); no results will be returned
```

如果其中任何一个已记录，您可能需要重新编写查询以使用不同的全文索引，或提供新索引以支持查询。 下面提供了您可能看到的依赖关系类型以及如何解决这些依赖关系的详细信息。

## 对“通用lucene”索引的潜在依赖

### 发布

#### 自定义应用程序查询

在“发布”中使用“通用lucene”索引的查询最常见的来源是自定义应用程序查询。

在最简单的情况下，这些查询可能是未指定nodetype（暗示“nt:base”）或明确指定nt:base的查询，例如：

```
/jcr:root/content/mysite//*[jcr:contains(., 'search term')]
/jcr:root/content/mysite//element(*, nt:base)[jcr:contains(., 'search term')]
```

所需操作：这些查询可以修改为使用适当的节点类型 — 例如，返回与页面匹配的结果（或cq:Page节点下的任何“聚合”），查询可能会变为：

```
/jcr:root/content/mysite//element(*, cq:Page)[jcr:contains(., 'search term')]
```

在其他情况下，查询可能会指定节点类型，但包含无法由其他全文索引处理的全文限制，例如：

```
/jcr:root/content/dam//element(*, dam:Asset)[jcr:contains(jcr:content/metadata/@cq:tags, 'NewsTopics:cateogries/domestic'))]
```

在这种情况下，查询具有“dam:Asset”节点类型，但包含对相对 `jcr:content/metadata/@cq:tags` 属性。

此属性在damAssetLucene索引（最常用于针对“dam:Asset”节点类型进行查询的全文索引）中未标记为“analysed”，因此此索引不能用于此查询。

因此，查询会返回到“通用全文”索引中，该索引中的所有包含属性都将标记为由通配符匹配(在 `/oak:index/lucene-2/indexRules/nt:base/properties/prop`.

所需的客户操作：标记 `jcr:content/metadata/@cq:tags` damAssetLucene索引的自定义版本中属性为“analysed”时，此索引将处理此查询，且不会记录任何警告。

### 创作 

除了客户应用程序Servlet中的查询、OSGi组件和渲染脚本之外，“generic lucene”索引还有许多特定于作者的用法。 

#### 引用搜索

以前，“通用lucene”索引用于支持“引用搜索”（搜索包含对其他内容路径的引用的内容）。 此类查询应已移至使用新的“/oak:index/pathreference”索引。
所需的客户操作：无需客户操作。


#### 路径字段选取器搜索

AEM包含一个自定义对话框组件（Sling资源类型“granite/ui/components/coral/foundation/form/pathfield”），该组件提供了一个用于选择其他AEM路径的浏览器（选取器）。  默认路径字段选取器（在内容结构中未定义自定义“pickerSrc”属性时使用）在弹出对话框中呈现搜索栏。
可使用“nodeTypes”属性指定要搜索的节点类型。

目前，如果不存在“nodeTypes”属性，则基础搜索查询将使用“nt:base”nodetype，因此可能使用“generic lucene”索引（通常记录下面显示的WARN消息）。

```
20.01.2022 18:56:06.412 *WARN* [127.0.0.1 [1642704966377] POST /mnt/overlay/granite/ui/content/coral/foundation/form/pathfield/picker.result.single.html HTTP/1.1] org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') and isdescendantnode(a, '/content') /* xpath: /jcr:root/content//element(*, nt:base)[(jcr:contains(., 'test'))] order by @jcr:score descending */ fullText="test", path=/content//*). Please change the query or the index definitions.
```

在删除“generic lucene”之前，将更新路径字段组件，以便使用默认选取器（不提供“nodeTypes”属性）为组件隐藏搜索框。

| 搜索路径字段选取器 | 不带搜索的Pathfield选取器 |
|---|---|
| ![搜索路径字段选取器](assets/index-pathfield-picker-with-search.png) | ![不带搜索的Pathfield选取器](assets/index-pathfield-picker-without-search.png) |


所需的客户操作：如果不需要搜索，则客户无需执行任何操作。

如果客户希望保留路径字段选取器中的搜索功能，则应提供属性“nodeTypes”，其中列出了他们要查询的节点类型。 可以在字符串属性中指定为以逗号分隔的节点类型列表。


>[!NOTE]
>内容片段模型编辑器使用具有Sling资源类型“dam/cfm/models/editor/components/contentreference”的专用路径字段。
> * 目前，这些查询在未指定节点类型的情况下执行查询，因为使用了“generic lucene”索引，导致记录“警告”。
> * 这些组件的实例很快会自动默认使用“cq:Page”和“dam:Asset”节点类型，无需客户进一步操作。
> * 可以添加“nodeTypes”属性以覆盖这些默认的节点类型。 





## 删除“通用lucene”的时间轴

Adobe将采取两阶段方法来删除“通用lucene”索引。

**阶段1** （计划于2022年1月31日开始）：不再在新的AEMas a Cloud Service环境中创建“/oak:index/lucene-*”。

**阶段2** （计划于2022年3月31日开始）：从新的AEMas a Cloud Service环境中删除“/oak:index/lucene-*”索引。

Adobe将监控上述日志消息，并尝试联系仍依赖“通用lucene”索引的客户。

作为短期缓解措施，如有必要，Adobe将直接将自定义索引定义添加到客户系统，以防止因删除“通用lucene”索引而出现功能或性能问题。

在这种情况下，客户将获得更新的索引定义，并建议通过Cloud Manager将其包含在其应用程序的未来版本中。
