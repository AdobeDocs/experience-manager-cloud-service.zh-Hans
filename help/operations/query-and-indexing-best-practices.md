---
title: 查询和索引最佳实践
description: 了解如何根据 Adobe 的最佳实践指南优化索引和查询。
topic-tags: best-practices
exl-id: 37eae99d-542d-4580-b93f-f454008880b1
source-git-commit: afeff7cfb8606eb58126a4ca62ce9e6e58c44215
workflow-type: ht
source-wordcount: '1563'
ht-degree: 100%

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

AEM as a Cloud Service 提供查询性能工具，该工具旨在支持实现高效查询。

* 它可显示已执行的查询及其相关性能特征和查询计划。
* 从仅显示查询计划到执行完整查询，它允许在不同级别执行特殊查询。

查询性能工具可通过云管理器中的[开发者控制台访问。](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html#queries)与 AEM 6.x 版本相比，AEM as a Cloud Service 的查询性能工具可提供更多有关查询执行细节的信息。

此图表说明了使用查询性能工具优化查询的一般流程。

![查询优化流程](assets/query-optimization-flow.png)

### 使用索引 {#use-an-index}

每个查询都应该使用索引来提供最佳性能。在大多数情况下，现有的开箱即用的索引应足以处理查询。

有时需要将自定义属性添加到现有索引中，以使用该索引查询其他约束。有关详细信息，请参阅文档[内容搜索和索引](/help/operations/indexing.md#changing-an-index)。本文档的 [JCR 查询备忘表](#jcr-query-cheatsheet)部分描述了如何制定索引上的属性定义，才能支持特定的查询类型。

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

如果必须完全处理潜在的大型结果集，请参阅本文档的[对大型结果的查询](#queries-with-large-result-sets)部分。

## JCR 查询备忘单 {#jcr-query-cheatsheet}

为了支持创建高效的 JCR 查询和索引定义，[JCR 查询备忘表](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/practices/best-practices-for-queries-and-indexing.html#jcrquerycheatsheet)可供下载，并可在开发过程中用作参考。

它包含 QueryBuilder、XPath 和 SQL-2 的示例查询，并涵盖了在查询性能方面表现不同的多个场景。它还提供了关于如何构建或定制 Oak 索引的建议。本备忘单的内容适用于 AEM as a Cloud Service 以及 AEM 6.5。

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
