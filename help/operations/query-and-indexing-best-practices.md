---
title: 查询和索引最佳实践
description: 了解如何根据 Adobe 的最佳实践指南优化索引和查询。
topic-tags: best-practices
exl-id: 37eae99d-542d-4580-b93f-f454008880b1
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '3133'
ht-degree: 47%

---

# 查询和索引最佳实践 {#query-and-indexing-best-practices}

在 AEM as a Cloud Service 中，有关索引的所有操作方面都是自动化的。这使开发人员能够专注于创建高效的查询及其相应的索引定义。

## 何时使用查询 {#when-to-use-queries}

查询是访问内容的一种方式，但不是唯一可用的方法。在许多情况下，可以通过其他方式更有效地访问存储库中的内容。您应该考虑查询是否是访问用例内容的最佳和最有效的方式。

### 存储库和分类设计 {#repository-and-taxonomy-design}

在设计存储库的分类时，需要考虑几个因素。其中包括访问控制、本地化、组件和页面属性继承等。

在设计涵盖这些方面的分类法时，考虑索引设计的“可通行性”也很重要。在这种情况下，可通行性是分类法允许基于其路径以可预测地方式访问内容的能力。这样的系统比需要执行多个查询的系统更有效、容易维护。

此外，在设计分类法时，考虑排序是否重要也很关键。如果不需要显式排序，并且需要大量同级节点，则最好使用无序节点类型，如`sling:Folder`或`oak:Unstructured`。在需要排序的情况下，`nt:unstructured` 和 `sling:OrderedFolder` 更合适。

### 组件中的查询 {#queries-in-components}

由于查询可能是在 AEM 系统上执行的最繁重的操作之一，因此最好在组件中避免查询。每次呈现页面时执行多个查询通常会降低系统的性能。有两种策略可用于在呈现组件时避免执行查询：**[遍历节点](#traversing-nodes)**&#x200B;和&#x200B;**[预取结果。](#prefetching-results)**

### 遍历节点 {#traversing-nodes}

如果存储库的设计允许事先了解所需数据的位置，则可以部署从必要路径检索此数据的代码，而无需运行查询来查找它。

这方面的一个例子是呈现适合特定类别的内容。一种方法是使用类别属性组织内容，并且可以通过查询该属性来填充显示类别中项目的组件。

更好的方法是按类别通过分类法构造此内容，以便可以手动检索。

例如，如果内容存储在类似于以下的分类法中：

```xml
/content/myUnstructuredContent/parentCategory/childCategory/contentPiece
```

可以简单地检索 `/content/myUnstructuredContent/parentCategory/childCategory` 节点，解析其子节点并用于呈现组件。

此外，当您处理一个小的或同质的结果集时，遍历存储库并收集所需的节点可能比通过手工创建查询来返回相同的结果集更快。作为一般考虑，应尽可能避免查询。

### 预取结果 {#prefetching-results}

有时，组件周围的内容或需求不允许使用节点遍历作为检索所需数据的方法。在这种情况下，需要在呈现组件之前执行所需的查询，以确保最佳性能。

如果可以在编写组件时计算组件所需的结果，并且预期内容不会更改，则可以在完成更改后执行查询。

如果数据或内容会定期更改，则可以按计划或通过侦听器执行查询，以更新基础数据。然后，可以将结果写入存储库中的共享位置。任何需要此数据的组件都可以从该单个节点提取值，而无需在运行时执行查询。

类似的策略可用于将结果保存在内存缓存中，该缓存在启动时会被填充，并会在进行更改时更新（使用 JCR `ObservationListener` 或 Sling `ResourceChangeListener`）。

## 优化查询 {#optimizing-queries}

Oak 文档提供了如何执行查询的[高级概述。](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#query-processing)这是本文件所述所有优化活动的基础。

AEMas a Cloud Service提供 [查询性能工具](#query-performance-tool)，旨在支持实施高效查询。

* 它可显示已执行的查询及其相关性能特征和查询计划。
* 从仅显示查询计划到执行完整查询，它允许在不同级别执行特殊查询。

查询性能工具可通过云管理器中的[开发者控制台访问。](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html#queries)与 AEM 6.x 版本相比，AEM as a Cloud Service 的查询性能工具可提供更多有关查询执行细节的信息。

此图表说明了使用查询性能工具优化查询的一般流程。

![查询优化流程](assets/query-optimization-flow.png)

### 使用索引 {#use-an-index}

每个查询都应该使用索引来提供最佳性能。在大多数情况下，现有的开箱即用的索引应足以处理查询。

有时需要将自定义属性添加到现有索引中，以使用该索引查询其他约束。有关详细信息，请参阅文档[内容搜索和索引](/help/operations/indexing.md#changing-an-index)。此 [JCR查询备忘单](#jcr-query-cheatsheet) 本文档的部分描述了如何对索引进行属性定义，才能支持特定的查询类型。

### 使用正确的标准 {#use-the-right-criteria}

任何查询的主要约束都应该是一种属性匹配，因为这是最有效的类型。添加更多属性约束会进一步限制结果。

查询引擎只考虑单个索引。这意味着可以并且应该通过向现有索引添加更多自定义索引属性来对其进行自定义。

本文档的 [JCR 查询备忘表](#jcr-query-cheatsheet)部分列出了可用的约束条件，并概述了怎样对索引进行定义，以便于检索。使用[查询性能工具](#query-performance-tool)测试查询并确保使用了正确的索引，并且查询引擎不需要评估索引之外的约束。

### 排序 {#ordering}

如果请求的是结果的特定顺序，那么查询引擎可以通过两种方式实现这种排序：

1. 索引可以以正确的顺序完整地传递结果。
   * 如果用于排序的属性在索引定义中用`ordered=true`注释，则此操作有效。
1. 查询引擎执行排序过程。
   * 当查询引擎在索引之外执行过滤或排序属性未使用`ordered=true`属性进行注释时，可能会发生这种情况。
   * 这需要将完整的结果集读入内存进行排序，这比第一个选项慢得多。

### 限制结果大小 {#restrict-result-size}

查询结果的检索大小是查询性能的一个重要因素。由于结果是以延迟方式获取的，因此在运行时和内存使用方面，仅获取前 20 个结果与获取 10000 个结果是不同的。

这也意味着，只有在获取所有结果的情况下，才能正确确定结果集的大小。因此，请务必限制获取的结果集，要么通过增加查询（详见本文档的[ JCR 查询备忘表](#jcr-query-cheatsheet)部分），要么通过限制结果的读取来进行限制。

这样的限制还可以防止查询引擎达到 100000 个节点的&#x200B;**遍历限制**，这会导致强制停止查询。

请参阅部分 [具有大型结果集的查询](#queries-with-large-result-sets) 如果必须完全处理潜在的大型结果集，则显示此文档。

## 查询性能工具 {#query-performance-tool}

查询性能工具(位于 `/libs/granite/operations/content/diagnosistools/queryPerformance.html` 并可通过 [Cloud Manager中的开发人员控制台](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html#queries))提供 — 
* 任何“慢查询”的列表；当前定义为读取/扫描超过5000行的查询。
* “常见查询”列表
* “Explain Query”工具，用于了解Oak如何执行特定查询。

![查询性能工具](assets/query-performance-tool.png)

“慢查询”和“常用查询”表包括 — 
* 查询语句本身。
* 上一个执行查询的线程的详细信息，允许识别执行查询的页面或应用程序功能。
* 查询的“读取优化”分数。
   * 计算方法是扫描以运行查询的行数/节点数与读取的匹配结果数之间的比率。
   * 对于可以在索引处处理每个限制（以及任何排序）的查询，其分数通常为90%或更高。
* 最大行数的详细信息 — 
   * 读取 — 指示某行已作为结果集的一部分包括在内。
   * 已扫描 — 指示在基础索引查询（在索引查询的情况下）的结果中包含行，或从节点存储（在存储库遍历的情况下）读取行。

这些表有助于识别未完全编制索引的查询(请参阅 [使用索引](#use-an-index) 或读取的节点过多(另请参阅 [存储库遍历](#repository-traversal) 和 [索引遍历](#index-traversal))。 此类查询将突出显示，并将相应的关注领域标示为红色。

此 `Reset Statistics` 提供了用于删除表中收集的所有现有统计信息的选项。 这允许执行特定查询（通过应用程序本身或Explain查询工具）并分析执行统计信息。

### 说明查询

Explain查询工具允许开发人员了解查询执行计划(请参阅 [读取查询执行计划](#reading-query-execution-plan))，包括执行查询时使用的任何索引的详细信息。 这可用于了解为查询编制索引以预测或追溯分析其性能的效率。

#### 说明查询

要解释查询，请执行以下操作：

* 使用选择适当的查询语言 `Language` 下拉菜单。
* 将查询语句输入到 `Query` 字段。
* 如果需要，可使用提供的复选框选择查询的执行方式。
   * 默认情况下，无需运行JCR查询来标识查询执行计划（QueryBuilder查询并非如此）。
   * 提供了三个用于执行查询的选项 — 
      * `Include Execution Time`  — 执行查询，但不尝试读取任何结果。
      * `Read first page of results`  — 执行查询并读取20个结果的第一个“页面”（复制执行查询的最佳实践）。
      * `Include Node Count`  — 执行查询并读取整个结果集(通常不建议这样做 — 请参阅 [索引遍历](#index-traversal))。

#### 查询说明弹出窗口 {#query-explanation-popup}

![查询说明弹出窗口](./assets/query-explanation-popup.png)

选择后 `Explain`，用户会看到一个弹出窗口，描述查询说明的结果（和执行，如果选中）。
此弹出窗口包含的详细信息 — 
* 执行查询时使用的索引（或者如果使用执行查询，则无索引） [存储库遍历](#repository-traversal))。
* 执行时间(如果 `Include Execution Time` 复选框已选中)和读取的结果计数(如果 `Read first page of results` 或 `Include Node Count` 复选框)。
* 执行计划，允许对查询的执行方式进行详细分析 — 请参阅 [读取查询执行计划](#reading-query-execution-plan) 以了解如何解读此信息。
* 前20个查询结果的路径(如果 `Read first page of results` 复选框已选中)
* 查询计划的完整日志，显示为执行此查询而考虑的索引的相对成本（成本最低的索引将被选择）。

#### 读取查询执行计划 {#reading-query-execution-plan}

查询执行计划包含预测（或解释）特定查询的性能所需的一切。 通过比较原始JCR（或查询生成器）查询中的限制和排序与在基础索引（Lucene、Elastic或Property）中执行的查询，了解查询的执行效率。

请考虑以下查询 — 

```
/jcr:root/content/dam//element(*, dam:Asset) [jcr:content/metadata/dc:title = "My Title"] order by jcr:created
```

...其中包含 — 
* 3个限制
   * 节点类型 (`dam:Asset`)
   * 路径(子项 `/content/dam`)
   * 属性 (`jcr:content/metadata/dc:title = "My Title"`)
* 排序依据 `jcr:created` 属性

说明此查询会导致以下计划 — 

```
[dam:Asset] as [a] /* lucene:damAssetLucene-9(/oak:index/damAssetLucene-9) +:ancestors:/content/dam +jcr:content/metadata/dc:title:My Title ordering:[{ propertyName : jcr:created, propertyType : UNDEFINED, order : ASCENDING }] where ([a].[jcr:content/metadata/dc:title] = 'My Title') and (isdescendantnode([a], [/content/dam])) */
```

在此计划中，描述在基础索引中执行的查询的部分是 — 

```
lucene:damAssetLucene-9(/oak:index/damAssetLucene-9) +:ancestors:/content/dam +jcr:content/metadata/dc:title:My Title ordering:[{ propertyName : jcr:created, propertyType : UNDEFINED, order : ASCENDING }]
```

计划的这一部分指出：
* 索引用于执行此查询 — 
   * 在本例中，Lucene索引 `/oak:index/damAssetLucene-9` 由于将使用，因此剩余信息采用Lucene查询语法。
* 所有3个限制都由索引处理 — 
   * 节点类型限制
      * 隐含，因为 `damAssetLucene-9` 仅索引dam：Asset类型的节点。
   * 路径限制
      * 因为 `+:ancestors:/content/dam` 显示在Lucene查询中。
   * 属性限制
      * 因为 `+jcr:content/metadata/dc:title:My Title` 显示在Lucene查询中。
* 排序由索引处理
   * 因为 `ordering:[{ propertyName : jcr:created, propertyType : UNDEFINED, order : ASCENDING }]`  显示在Lucene查询中。

此类查询可能执行良好，因为从索引查询返回的结果不会在查询引擎中进一步过滤（除了访问控制过滤）。 但是，如果不遵循最佳实践，此类查询仍有可能执行缓慢 — 请参阅 [索引遍历](#index-traversal) 下。

考虑不同的查询 — 

```
/jcr:root/content/dam//element(*, dam:Asset) [jcr:content/metadata/myProperty = "My Property Value"] order by jcr:created
```

...其中包含 — 
* 3个限制
   * 节点类型 (`dam:Asset`)
   * 路径(子项 `/content/dam`)
   * 属性 (`jcr:content/metadata/myProperty = "My Property Value"`)
* 排序依据 `jcr:created` 属性**

说明此查询会导致以下计划 — 

```
[dam:Asset] as [a] /* lucene:damAssetLucene-9-custom-1(/oak:index/damAssetLucene-9-custom-1) :ancestors:/content/dam ordering:[{ propertyName : jcr:created, propertyType : UNDEFINED, order : ASCENDING }] where ([a].[jcr:content/metadata/myProperty] = 'My Property Value') and (isdescendantnode([a], [/content/dam])) */
```

在此计划中，描述在基础索引中执行的查询的部分是 — 

```
lucene:damAssetLucene-9(/oak:index/damAssetLucene-9) :ancestors:/content/dam ordering:[{ propertyName : jcr:created, propertyType : UNDEFINED, order : ASCENDING }]
```

计划的这一部分指出：
* 索引仅处理（3个）限制中的2个 — 
   * 节点类型限制
      * 隐含，因为 `damAssetLucene-9` 仅索引dam：Asset类型的节点。
   * 路径限制
      * 因为 `+:ancestors:/content/dam` 显示在Lucene查询中。
* 属性限制 `jcr:content/metadata/myProperty = "My Property Value"` 不是在索引处执行，而是将作为查询引擎筛选对基础Lucene查询的结果应用。
   * 这是因为 `+jcr:content/metadata/myProperty:My Property Value` 不会出现在Lucene查询中，因为此属性未在 `damAssetLucene-9` 用于此查询的索引。

此查询执行计划将生成以下每个资产 `/content/dam` 从索引中读取，然后由查询引擎进一步筛选（这将仅包括那些与结果集中的非索引属性限制匹配的属性）。

即使只有一小部分资源符合限制 `jcr:content/metadata/myProperty = "My Property Value"`，查询需要读取大量节点来（尝试）填充请求的结果“页面”。 这可能会导致查询性能不佳，表现为查询性能较低 `Read Optimization` 分数)，并且可能导致出现警告消息，指示大量节点正在被遍历(请参阅 [索引遍历](#index-traversal))。

要优化此第二个查询的性能，请创建 `damAssetLucene-9` 索引(`damAssetLucene-9-custom-1`)并添加以下属性定义 — 

```
"myProperty": {
  "jcr:primaryType": "nt:unstructured",
  "propertyIndex": true,
  "name": "jcr:content/metadata/myProperty"
}
```

## JCR查询备忘单 {#jcr-query-cheatsheet}

为了支持创建高效的 JCR 查询和索引定义，[JCR 查询备忘表](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/practices/best-practices-for-queries-and-indexing.html#jcrquerycheatsheet)可供下载，并可在开发过程中用作参考。

它包含 QueryBuilder、XPath 和 SQL-2 的示例查询，并涵盖了在查询性能方面表现不同的多个场景。它还提供了关于如何构建或定制 Oak 索引的建议。本备忘单的内容适用于AEMas a Cloud Service和AEM 6.5。

## 索引定义最佳实践 {#index-definition-best-practices}

以下是定义或扩展索引时要考虑的一些最佳实践。

* 对于具有现有索引的节点类型(例如 `dam:Asset` 或 `cq:Page`)除了添加新索引之外，还希望扩展OOTB索引。
   * 将新索引（特别是全文索引）添加到 `dam:Asset` 强烈建议不要使用节点类型(请参阅 [此注释](/help/operations/indexing.md##index-names-index-names))。
* 添加新索引时
   * 始终定义“lucene”类型的索引。
   * 在索引定义（和关联的查询）中使用索引标记，并且 `selectionPolicy = tag` 以确保该索引仅用于预期查询。
   * 确保 `queryPaths` 和 `includedPaths` 都会提供（通常使用相同的值）。
   * 使用 `excludedPaths` 以排除不包含有用结果的路径。
   * 使用 `analyzed` 属性仅在需要时，例如，当您需要仅对该属性使用全文查询限制时。
   * 始终指定 `async = [ async, nrt ] `， `compatVersion = 2` 和 `evaluatePathRestrictions = true`.
   * 仅指定 `nodeScopeIndex = true` 如果您需要节点范围全文索引。

>[!NOTE]
>
>有关更多信息，请参阅 [Oak Lucene索引文档](https://jackrabbit.apache.org/oak/docs/query/lucene.html).

Automated Cloud Manager管道检查将强制执行上述某些最佳实践。

## 具有大型结果集的查询 {#queries-with-large-result-sets}

虽然建议避免使用具有大型结果集的查询，但在某些情况下，必须处理大型结果集。通常情况下，结果的大小事先无法知道，因此应采取一些预防措施，以便可靠地进行处理。

* 不应在请求中执行查询。相反，查询应作为 Sling Job 或 AEM 工作流的一部分执行。它们的总运行时间没有任何限制，并且在处理查询及其结果期间实例发生故障时会重新启动。
* 要克服 100000 个节点的查询限制，应考虑使用[键集分页](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Keyset_Pagination)，并将查询拆分为多个子查询。

## 存储库遍历 {#repository-traversal}

遍历存储库的查询不使用索引，而是使用与以下类似的消息进行日志记录。

```text
28.06.2022 13:32:52.804 *WARN* [127.0.0.1 [1656415972414] POST /libs/settings/granite/operations/diagnosis/granite_queryperformance.explain.json HTTP/1.1] org.apache.jackrabbit.oak.plugins.index.Cursors$TraversingCursor Traversed 98000 nodes with filter Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a /* xpath: //* */, path=*) called by com.adobe.granite.queries.impl.explain.query.ExplainQueryServlet.getHeuristics; consider creating an index or changing the query
```

通过此日志片段，您可以确定：

* 查询本身：`//*`
* 执行此查询的 Java 代码：`com.adobe.granite.queries.impl.explain.query.ExplainQueryServlet::getHeuristics`，以帮助识别查询的创建者。

有了这些信息，可以使用本文件[优化查询](#optimizing-queries)部分中描述的方法优化该查询。

### 索引遍历 {#index-traversal}

使用索引但仍读取大量节点的查询将记录一条类似于以下内容的消息（请注意术语） `Index-Traversed` 而不是 `Traversed`)。

```text
05.10.2023 10:56:10.498 *WARN* [127.0.0.1 [1696502982443] POST /libs/settings/granite/operations/diagnosis/granite_queryperformance.explain.json HTTP/1.1] org.apache.jackrabbit.oak.plugins.index.search.spi.query.FulltextIndex$FulltextPathCursor Index-Traversed 60000 nodes with filter Filter(query=select [jcr:path], [jcr:score], * from [dam:Asset] as a where isdescendantnode(a, '/content/dam') order by [jcr:content/metadata/unindexedProperty] /* xpath: /jcr:root/content/dam//element(*, dam:Asset) order by jcr:content/metadata/unindexedProperty */, path=/content/dam//*)
```

出现这种情况的原因有很多 — 
1. 并非查询中的所有限制都可以在索引上处理。
   * 在这种情况下，正在从索引读取最终结果集的超集，并随后在查询引擎中过滤。
   * 这比在基础索引查询中应用限制慢许多倍。
1. 查询按属性排序，该属性在索引中未标记为“ordered”。
   * 在这种情况下，索引返回的所有结果必须由查询引擎读取并在内存中排序。
   * 这比在基础索引查询中应用排序慢许多倍。
1. 查询的执行器正在尝试迭代大型结果集。
   * 发生此情况的原因有很多，如下所列：

| 原因 | 缓解 |
|----------|--------------|
| 委员会的任务 `p.guessTotal` （或使用非常大的guessTotal）导致QueryBuilder迭代大量结果计数结果 | 提供 `p.guessTotal` 具有适当的值 |
| 在查询生成器中使用较大或无界限制(即 `p.limit=-1`) | 使用适当的值 `p.limit` （最好为1000或更低） |
| 在Query Builder中使用过滤谓词，从基础JCR查询中过滤大量结果 | 将筛选谓词替换为可在基础JCR查询中应用的限制 |
| 在QueryBuilder中使用基于比较器的排序 | 替换为基础JCR查询中基于属性的排序（使用按排序索引的属性） |
| 由于访问控制筛选了大量结果 | 将其他索引属性或路径限制应用于查询以镜像访问控制 |
| 使用具有大偏移量的“偏移分页” | 考虑使用 [键集分页](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Keyset_Pagination) |
| 大量或无界结果的迭代 | 考虑使用 [键集分页](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Keyset_Pagination) |
| 选择的索引不正确 | 在查询和索引定义中使用标记以确保使用预期的索引 |
