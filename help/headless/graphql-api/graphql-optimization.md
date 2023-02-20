---
title: 优化GraphQL查询
description: 了解在Adobe Experience Manager as a Cloud Service中过滤、分页和排序内容片段以进行无头内容交付时，如何优化GraphQL查询。
source-git-commit: e156ed7348815e02c942cb8feace70c675956752
workflow-type: tm+mt
source-wordcount: '1192'
ht-degree: 0%

---


# 优化GraphQL查询 {#optimizing-graphql-queries}

>[!NOTE]
>
>在应用这些优化推荐之前，请考虑 [在GraphQL筛选中更新内容片段以进行分页和排序](/help/headless/graphql-api/graphql-paging-sorting-content-update.md) 以获得最佳性能。

在具有大量共享同一模型的内容片段的AEM实例上，GraphQL列表查询可能会变得成本高昂（就资源而言）。

这是因为 *全部* 与GraphQL查询中使用的模型共享的片段必须加载到内存中。 这会消耗时间和内存。 筛选(可能会减少（最终）结果集中的项目数)只能应用 **after** 将整个结果集加载到内存中。

这可能会导致这样一种印象，即即使是较小的结果集（可能）也会导致性能不佳。 但是，实际上，速度慢是由初始结果集的大小造成的，因为必须在内部处理该结果后才能应用过滤。

为了降低性能和内存问题，必须尽可能小地保持初始结果集。

AEM提供了两种优化GraphQL查询的方法：

* [混合滤波](#hybrid-filtering)
* [分页](#paging) （或分页）

   * [排序](#sorting) 与优化无直接关系，但与分页相关

每种方法都有其自身的用例和限制。 本文档提供了有关混合过滤和分页的信息，其中包含 [最佳实践](#best-practices) 以优化GraphQL查询。

## 混合滤波 {#hybrid-filtering}

混合过滤将JCR过滤与AEM过滤相结合。

在将结果集加载到内存中以进行AEM筛选之前，它会应用JCR筛选器（以查询约束的形式）。 这是为了减少加载到内存中的结果集，因为JCR滤波器会在此之前删除多余的结果。

>[!NOTE]
>
>由于技术原因（例如灵活性、片段嵌套），AEM无法将整个过滤委派给JCR。

此技术可保持GraphQL过滤器提供的灵活性，同时将尽可能多的过滤权限委派给JCR。

## 分页 {#paging}

AEM中的GraphQL支持两种类型的分页：

* [限制/基于偏移的分页](/help/headless/graphql-api/content-fragments.md#list-offset-limit)
用于列表查询；以 
`List`;例如， `articleList`.
要使用它，您必须提供要返回的第一个项目的位置( `offset`)和要返回的项目数( `limit`，或页面大小)。

* [基于光标的分页](/help/headless/graphql-api/content-fragments.md#paginated-first-after) (代表 `first`和 `after`)这会为每个项目提供一个唯一的ID;也称为光标。
在查询中，指定上一页最后一项的光标，加上页面大小（要返回的最大项数）。

   由于基于游标的分页不适合基于列表的查询的数据结构，因此AEM已引入 `Paginated` 查询类型；例如， `articlePaginated`. 使用的数据结构和参数遵循 [GraphQL游标连接规范](https://relay.dev/graphql/connections.htm).

   >[!NOTE]
   >
   >AEM当前支持正向分页(使用 `after`/`first` 参数)。
   >
   >反向分页(使用 `before`/`last` 参数)。

## 排序 {#sorting}

仅当所有排序条件都与顶级片段相关时，排序才会有效。

如果排序顺序包括位于嵌套片段上的一个或多个字段，则共享顶级模型的所有片段都必须加载到内存中。 这会对性能产生负面影响。

>[!NOTE]
>
>对顶级字段进行排序还会对性能产生（尽管小）影响。

## 最佳实践 {#best-practices}

所有优化的主要目标是减少初始结果集。 此处列出的最佳实践提供了实现此目的的方法。 它们可以（而且应该）合并。

### 仅对顶级属性进行筛选 {#filter-top-level-properties-only}

目前，JCR级别的筛选仅适用于顶级片段。

如果过滤器处理嵌套片段的字段，则AEM必须回退到加载（到内存中）共享基础模型的所有片段。

您仍然可以通过将顶级片段字段和嵌套片段字段中的过滤器表达式与 [AND运算符](#logical-operations-in-filter-expressions).

### 使用内容结构 {#use-content-structure}

在AEM中，通常认为使用存储库结构缩小待处理内容的范围是最佳做法。

此方法还应用于GraphQL查询。

这可以通过在 `_path` 顶级片段的字段：

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
>尾随 `/` on `value` 才能获得最佳性能。

### 使用分页 {#use-paging}

您还可以使用分页来减少初始结果集；特别是当您的请求不使用任何过滤和排序时。

如果您对嵌套片段进行过滤或排序，则分页查询仍可能会变慢，因为AEM可能仍需要将大量片段加载到内存中。 因此，如果将过滤和分页结合使用，请考虑过滤规则（如上所述）。

对于分页，排序同样重要，因为分页结果始终按显式或隐式方式进行排序。

如果您主要希望仅检索前几个页面，则使用 `...List` 或 `...Paginated` 查询。 但是，如果您的应用程序希望仅阅读一两页以上的内容，则应考虑 `...Paginated` 查询，因为在后续的页面中，该功能的效果显着优于其他功能。

### 过滤器表达式中的逻辑运算 {#logical-operations-in-filter-expressions}

如果您对嵌套片段进行筛选，则仍可以通过在使用 `AND` 运算符。

典型的用例是：在 `_path` 字段，然后筛选可能位于顶级或嵌套片段上的其他字段。

在这种情况下，不同的过滤器表达式将与 `AND`. 因此， `_path` 可以有效地限制初始结果集。 顶级字段中的所有其他过滤器也有助于减少初始结果集，只要它们与 `AND`.

过滤器表达式与 `OR` 如果涉及嵌套片段，则无法进行优化。 `OR` 只有在 *否* 嵌套片段涉及。

### 避免对多行文本字段进行过滤 {#avoid-filtering-multiline-textfields}

无法通过JCR查询过滤多行文本字段（html、Markdown、纯文本、json）的字段，因为必须即时计算这些字段的内容。

如果仍需要对多行文本字段进行筛选，请考虑通过添加其他筛选表达式来限制初始结果集的大小，并将它们与 `AND`. 通过 `_path` 现场也是个好方法。

### 避免对虚拟字段进行过滤 {#avoid-filtering-virtual-fields}

虚拟字段(大多数字段以 `_`)会在执行GraphQL查询时计算，因此不在基于JCR的筛选范围内。

一个重要的例外是 `_path` 字段，可用于有效地减小初始结果集的大小 — 如果内容的结构相应(请参阅 [使用内容结构](#use-content-structure))。

### 过滤：排除项 {#filtering-exclusions}

在以下几种情况下，无法在JCR级别上评估过滤器表达式（因此，应避免使用以获得最佳性能）：

* 在 `Float` 值 `_sensitiveness` 筛选器选项，其中 `_sensitiveness` 设置为 `0.0` .

* 在 `String` 值 `_ignoreCase` 过滤器选项。

* 筛选条件 `null` 值。

* 对具有 `_apply: ALL_OR_EMPTY`.

* 对具有 `_apply: INSTANCES`, `_instances: 0`.

* 使用 `CONTAINS_NOT` 运算符。

* 在 `Calendar`, `Date` 或 `Time` 值 `NOT_AT` 运算符。
