---
title: 优化 GraphQL 查询
description: 了解如何在 Adobe Experience Manager as a Cloud Service 中对内容片段进行筛选、分页和排序时优化 GraphQL 查询，以实现 headless 内容交付。
source-git-commit: cda6d7e382b090fd726b27e565da08c8b1c80008
workflow-type: ht
source-wordcount: '1192'
ht-degree: 100%

---


# 优化 GraphQL 查询 {#optimizing-graphql-queries}

>[!NOTE]
>
>在应用这些优化建议之前，请考虑[更新内容片段以在 GraphQL 筛选中进行分页和排序](/help/headless/graphql-api/graphql-optimized-filtering-content-update.md)，从而获得最佳性能。

在具有大量共享同一模型的内容片段的 AEM 实例上，GraphQL 列表查询的成本可能会较高（就资源而言）。

这是因为&#x200B;*所有*&#x200B;共享将在 GraphQL 查询中使用的模型的片段都必须加载到内存中。这将消耗较多的时间和内存。只能在将整个结果集加载到内存中&#x200B;**后**，再应用筛选（它可能会减少最终结果集中的项目数）。

这可能会给人留下一种印象，那就是，即使较小的结果集也会导致性能不佳。然而，实际上这种缓慢是由初始结果集的大小引起的，因为必须先内部处理此情况，之后才能应用筛选。

要减少性能和内存问题，必须使该初始结果集尽可能的小。

AEM 提供了两种方法来优化 GraphQL 查询：

* [混合筛选](#hybrid-filtering)
* [分页](#paging)

   * [排序](#sorting)与优化没有直接关系，而与分页有关

每种方法都有自己的用例和限制。本文档提供了有关混合筛选和分页的信息，以及一些优化 GraphQL 查询的[最佳实践](#best-practices)。

## 混合筛选 {#hybrid-filtering}

混合筛选结合了 JCR 筛选和 AEM 筛选。

它在将结果集加载到内存中以进行 AEM 筛选之前应用 JCR 筛选（采用查询约束的形式）。这是为了减少加载到内存中的结果集，因为 JCR 筛选会在此之前删除多余的结果。

>[!NOTE]
>
>出于技术原因（例如灵活性、片段嵌套），AEM 无法将整个筛选工作委派给 JCR。

此技术保留了 GraphQL 筛选提供的灵活性，同时将尽可能多的筛选工作委派给 JCR。

## 分页 {#paging}

AEM 中的 GraphQL 支持两种类型的分页：

* [基于限制/偏移的分页](/help/headless/graphql-api/content-fragments.md#list-offset-limit)
此分页用于列表查询；它们以 
`List` 结尾；例如 `articleList`。
要使用它，您必须提供要返回的第一个项目的位置 (`offset`) 和要返回的项目数（`limit` 或页面大小）。

* [基于光标的分页](/help/headless/graphql-api/content-fragments.md#paginated-first-after)（由 `first` 和 `after` 表示）
这将为每个项目提供一个唯一 ID；也称为光标。
在查询中，您指定上一页的最后一项的光标，以及页面大小（要返回的项目的最大数量）。

   由于基于光标的分页不适合基于列表的查询的数据结构，因此，AEM 引入了 `Paginated` 查询类型；例如 `articlePaginated`。所使用的数据结构和参数遵循 [GraphQL 光标连接规范](https://relay.dev/graphql/connections.htm)。

   >[!NOTE]
   >
   >AEM 目前支持前向分页（使用 `after`/`first` 参数）。
   >
   >后向分页（使用 `before`/`last` 参数）不受支持。

## 排序 {#sorting}

仅在所有排序条件都与顶级片段相关时，排序才有效。

如果排序顺序包括某个嵌套片段上的一个或多个字段，则必须将所有共享顶级模型的片段加载到内存中。这会对性能产生负面影响。

>[!NOTE]
>
>对顶级字段进行排序也会对性能产生（虽然很小）影响。

## 最佳实践 {#best-practices}

所有优化的主要目标是减小初始结果集。此处列出的最佳实践提供了多种方法来实现此目的。可以（也应该）将它们结合使用。

### 仅筛选顶级属性 {#filter-top-level-properties-only}

目前，JCR 级别的筛选仅适用于顶级片段。

如果筛选处理嵌套片段的字段，则 AEM 必须回退以将所有共享基础模型的片段加载到内存中。

您仍可以使用 [AND 运算符](#logical-operations-in-filter-expressions)将顶级片段字段上的筛选表达式和嵌套片段字段上的筛选表达式组合起来，从而优化此类 GraphQL 查询。

### 使用内容结构 {#use-content-structure}

在 AEM 中，通常考虑的最佳实践是，使用存储库结构来缩小要处理的内容范围。

此方法也将应用于 GraphQL 查询。

这可以通过在顶级片段的 `_path` 字段上应用筛选来完成：

```graphql
{
  someList(filter: {
    _path: {
      _expressions: [ 
        {
          value: "/content/dam/some/sub/path/",
          _operator: STARTS_WITH
        }
      ]
    }
  }) {
    items {
      # ...
    }
  }
}
```

>[!NOTE]
>
>需要 `value` 上的尾随 `/` 来实现最佳性能。

### 使用分页 {#use-paging}

您还可以使用分页来减小初始结果集；特别是在您的请求不使用任何筛选和排序的情况下。

如果您对嵌套片段进行筛选或排序，分页查询可能仍然很慢，因为 AEM 可能仍需要将大量片段加载到内存中。因此，如果将筛选和分页结合使用，请考虑筛选规则（如上所述）。

对于分页，排序同样重要，因为分页的结果始终是已排序的 - 无论是通过显式还是隐式方式。

如果您主要只对检索前几页感兴趣，则使用 `...List` 或 `...Paginated` 查询之间没有显著区别。不过，如果您的应用程序不只是想阅读一两页，则应考虑 `...Paginated` 查询，因为此查询在阅读后续页面时的性能更佳。

### 筛选表达式中的逻辑运算 {#logical-operations-in-filter-expressions}

如果在嵌套片段上进行筛选，则仍可以通过提供使用 `AND` 运算符的顶级字段的附加筛选来利用 JCR 筛选。

一个典型用例是，对顶级片段的 `_path` 字段使用筛选器来限制查询的范围，然后筛选可能位于顶级或嵌套片段上的其他字段。

在此示例中，将使用 `AND` 组合不同的筛选表达式。因此，对 `_path` 进行筛选可以有效地限制初始结果集的大小。对顶级字段进行的所有其他筛选也可以帮助减小初始结果集 - 前提是使用 `AND` 将它们组合使用。

如果涉及嵌套的片段，则无法优化使用 `OR` 组合使用的筛选表达式。仅在&#x200B;*不*&#x200B;涉及嵌套片段的情况下，可以优化 `OR` 表达式。

### 避免筛选多行文本字段 {#avoid-filtering-multiline-textfields}

无法通过 JCR 查询筛选多行文本字段的字段（html、markdown、plaintext、json），因为必须即时计算这些字段的内容。

如果您仍需要筛选多行文本字段，请考虑通过添加额外的筛选表达式来限制初始结果集的大小，并使用 `AND` 将它们组合使用。通过筛选 `_path` 字段来限制范围也是一个好方法。

### 避免筛选虚拟字段 {#avoid-filtering-virtual-fields}

虚拟字段（大多数字段以 `_` 开始）是在执行 GraphQL 查询时计算的，因此不在基于 JCR 的筛选的范围内。

一个重要的例外是 `_path` 字段，可使用该字段有效地减小初始结果集 - 如果相应地构建了内容（请参阅[使用内容结构](#use-content-structure)）。

### 筛选：排除 {#filtering-exclusions}

还存在几种无法在 JCR 级别计算筛选表达式的情况（因此，应避免这些情况以实现最佳性能）：

* 使用 `_sensitiveness` 筛选选项的基于 `Float` 值的筛选表达式，其中 `_sensitiveness` 设置为 `0.0` 之外的任何值。

* 使用 `_ignoreCase` 筛选选项的基于 `String` 值的筛选表达式。

* 基于 `null` 值的筛选。

* 使用 `_apply: ALL_OR_EMPTY` 的基于数组的筛选。

* 使用 `_apply: INSTANCES` 和 `_instances: 0` 的基于数组的筛选。

* 使用 `CONTAINS_NOT` 运算符的筛选表达式。

* 使用 `NOT_AT` 运算符的基于 `Calendar`、`Date` 或 `Time` 值的筛选表达式。
