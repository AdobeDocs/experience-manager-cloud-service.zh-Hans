---
title: 查询生成器 API
description: 资产共享查询生成器的功能通过Java API和REST API公开。
exl-id: d5f22422-c9da-4c9d-b81c-ffa5ea7cdc87
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: tm+mt
source-wordcount: '2040'
ht-degree: 0%

---

# 查询生成器 API {#query-builder-api}

查询生成器提供了一种轻松的方法来查询AEM的内容存储库。 该功能通过Java API和REST API公开。 本文档介绍这些API。

服务器端查询生成器([`QueryBuilder`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/QueryBuilder.html))将接受查询描述、创建并运行XPath查询、（可选）筛选结果集，并根据需要提取facet。

查询描述只是一组谓词([`Predicate`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/Predicate.html))。 示例包括与 `jcr:contains()` 函数。

对于每个谓词类型，都有一个计算器组件([`PredicateEvaluator`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/eval/PredicateEvaluator.html))，它知道如何处理XPath、筛选和facet提取的特定谓词。 很容易创建自定义计算器，这些计算器通过OSGi组件运行时插入。

REST API通过HTTP提供对完全相同功能的访问，响应以JSON格式发送。

>[!NOTE]
>
>QueryBuilder API是使用JCR API构建的。 您还可以从OSGi包中使用JCR API来查询AEM JCR。 有关信息，请参阅 [使用JCR API查询Adobe Experience Manager数据](https://helpx.adobe.com/experience-manager/using/querying-experience-manager-data-using1.html).

## Gem会议 {#gem-session}

[AEM Gems](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-index.html) 是Adobe专家对Adobe Experience Manager进行的一系列深入技术探讨。

您可以 [查看专用于查询生成器的会话](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-search-forms-using-querybuilder.html) ，以了解该工具的概述和用法。

## 示例查询 {#sample-queries}

这些示例以Java属性样式表示法提供。 要将它们与Java API结合使用，请使用Java `HashMap` 与下面的API示例中的相同。

对于 `QueryBuilder` JSON Servlet的每个示例都包含一个指向AEM安装的示例链接(位于默认位置， `http://<host>:<port>`)。 请注意，您必须先登录AEM实例，然后才能使用这些链接。

>[!CAUTION]
>
>默认情况下，查询生成器JSON Servlet最多显示10次点击。
>
>添加以下参数后，Servlet可显示所有查询结果：
>
>`p.limit=-1`

>[!NOTE]
>
>要在浏览器中查看返回的JSON数据，您可能需要使用插件，如适用于Firefox的JSONView。

### 返回所有结果 {#returning-all-results}

以下查询将 **返回十个结果** （或者精确到最多十），但请通知您 **点击次数：** 实际可用：

`http://<host>:<port>/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=wknd/components/structure/page&1_property.operation=like&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=wknd/components/structure/page
1_property.operation=like
orderby=path
```

同一查询(使用参数 `p.limit=-1`)将 **返回所有结果** （根据您的实例，此数字可能很高）：

`http://<host>:<port>/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=wknd/components/structure/page&1_property.operation=like&orderby=path&p.limit=-1`

```xml
path=/content
1_property=sling:resourceType
1_property.value=wknd/components/structure/page
1_property.operation=like
p.limit=-1
orderby=path
```

### 使用p.guessTotal返回结果 {#using-p-guesstotal-to-return-the-results}

的目的 `p.guessTotal` 参数是返回通过组合最小可行值来显示的适当数目的结果 `p.offset` 和 `p.limit` 值。 使用此参数的优点是，在大结果集下提高了性能。 这可避免计算全部总计(例如，调用 `result.getSize()`)和读取整个结果集，一直优化到OAK引擎和索引。 当存在数十万个结果（执行时间和内存使用情况）时，这可能是一个显着差异。

参数的缺点是用户看不到确切的总计。 但是你可以设置一个 `p.guessTotal=1000` 因此，它将始终读取1000，因此您会获得较小结果集的确切总数，但如果超出此数量，则只能显示“更多”。

添加 `p.guessTotal=true` 查看以下查询以了解其工作方式：

`http://<host>:<port>/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=wknd/components/structure/page&1_property.operation=like&p.guessTotal=true&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=wknd/components/structure/page
1_property.operation=like
p.guessTotal=true
orderby=path
```

查询将返回 `p.limit` 默认 `10` 结果 `0` 偏移：

```xml
"success": true,
"results": 10,
"total": 10,
"more": true,
"offset": 0,
```

您还可以使用数值计算自定义的最大结果数。 使用与上面相同的查询，但更改 `p.guessTotal` to `50`:

`http://<host>:<port>/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=wknd/components/structure/page&1_property.operation=like&p.guessTotal=50&orderby=path`

它将返回一个与10个结果（默认限制为0个）相同的数字，但最多只显示50个结果：

```xml
"success": true,
"results": 10,
"total": 50,
"more": true,
"offset": 0,
```

### 实施分页 {#implementing-pagination}

默认情况下，查询生成器还会提供点击量。 根据结果大小，确定准确计数可能需要很长时间，因为需要检查访问控制的每个结果。 通常，总计用于为最终用户UI实施分页。 由于确定确切计数可能会比较慢，因此建议使用guessTotal功能来实施分页。

例如，UI可以调整以下方法：

* 获取并显示总点击量的准确计数([SearchResult.getTotalMatches()](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/result/SearchResult.html#getTotalMatches) 或 `querybuilder.json` 响应)小于或等于100;
* 已设置 `guessTotal` 调用查询生成器时设置为100。

* 响应可能会产生以下结果：

   * `total=43`, `more=false`  — 表示点击总数为43次。 UI在第一页中最多可显示10个结果，并为接下来的三个页面提供分页。 您还可以使用此实施来显示描述性文本，如 **&quot;发现43个结果&quot;**.
   * `total=100`, `more=true`  — 指示点击总数大于100，并且不知道确切计数。 UI在第一页中最多可显示10个页面，并为接下来的10个页面提供分页。 您还可以使用它显示类似 **“发现100个以上结果”**. 当用户转到下一页面时，对查询生成器发出的调用将提高 `guessTotal` 以及 `offset` 和 `limit` 参数。

`guessTotal` 当UI需要使用无限滚动时，还应使用，以避免查询生成器确定确切的点击计数。

### 查找Jar文件并排序，以最新为先 {#find-jar-files-and-order-them-newest-first}

`http://<host>:<port>/bin/querybuilder.json?type=nt:file&nodename=*.jar&orderby=@jcr:content/jcr:lastModified&orderby.sort=desc`

```xml
type=nt:file
nodename=*.jar
orderby=@jcr:content/jcr:lastModified
orderby.sort=desc
```

### 查找所有页面并按上次修改时间对它们进行排序 {#find-all-pages-and-order-them-by-last-modified}

`http://<host>:<port>/bin/querybuilder.json?type=cq:Page&orderby=@jcr:content/cq:lastModified`

```xml
type=cq:Page
orderby=@jcr:content/cq:lastModified
```

### 查找所有页面并按上次修改时间、降序进行排序 {#find-all-pages-and-order-them-by-last-modified-but-descending}

`http://<host>:<port>/bin/querybuilder.json?type=cq:Page&orderby=@jcr:content/cq:lastModified&orderby.sort=desc`

```xml
type=cq:Page
orderby=@jcr:content/cq:lastModified
orderby.sort=desc
```

### 全文搜索，按分数排序 {#fulltext-search-ordered-by-score}

`http://<host>:<port>/bin/querybuilder.json?fulltext=Management&orderby=@jcr:score&orderby.sort=desc`

```xml
fulltext=Management
orderby=@jcr:score
orderby.sort=desc
```

### 搜索具有特定标记的页面 {#search-for-pages-tagged-with-a-certain-tag}

`http://<host>:<port>/bin/querybuilder.json?type=cq:Page&tagid=wknd:activity/cycling&tagid.property=jcr:content/cq:tags`

```xml
type=cq:Page
tagid=wknd:activity/cycling
tagid.property=jcr:content/cq:tags
```

使用 `tagid` 谓词，如果您知道显式标记ID，则与示例中一样。

使用 `tag` 此谓词用于标记标题路径（不含空格）。

因为在上一个示例中，您正在搜索页面(`cq:Page` 节点)，则需要使用该节点的相对路径 `tagid.property` 谓词， `jcr:content/cq:tags`. 默认情况下， `tagid.property` 就是 `cq:tags`.

### 搜索多个路径（使用组） {#search-under-multiple-paths-using-groups}

`http://<host>:<port>/bin/querybuilder.json?fulltext=Experience&group.1_path=/content/wknd/us/en/magazine&group.2_path=/content/wknd/us/en/adventures&group.p.or=true`

```xml
fulltext=Experience
group.p.or=true
group.1_path=/content/wknd/us/en/magazine
group.2_path=/content/wknd/us/en/adventures
```

此查询使用 *群组* (已命名 `group`)，用于在查询中分隔子表达式，与括号在更多标准符号中的作用类似。 例如，上一个查询可以以更熟悉的样式表示：

`"Experience" and ("/content/wknd/us/en/magazine" or "/content/wknd/us/en/adventures")`

在示例的组内， `path` 谓词已被多次使用。 要区分并排序谓词的两个实例（某些谓词需要排序），您必须为谓词添加前缀 `N_` where `N` 是订购索引。 在上一个示例中，生成的谓词为 `1_path` 和 `2_path`.

的 `p` in `p.or` 是用于指示以下内容的特殊分隔符(在本例中为 `or`)是 *参数* 的子谓词，例如 `1_path`.

如果否 `p.or` 将所有谓词一起与之结合，即每个结果必须满足所有谓词。

>[!NOTE]
>
>不能在一个查询中使用相同的数字前缀，即使对于不同的谓词也是如此。

### 搜索属性 {#search-for-properties}

在此，您可以使用 `cq:template` 属性：

`http://<host>:<port>/bin/querybuilder.json?property=cq%3atemplate&property.value=%2fconf%2fwknd%2fsettings%2fwcm%2ftemplates%2fadventure-page-template&type=cq%3aPageContent`

```xml
type=cq:PageContent
property=cq:template
property.value=/conf/wknd/settings/wcm/templates/adventure-page-template
```

缺点是 `jcr:content` 将返回页面的节点，而不是页面本身。 要解决此问题，您可以按相对路径进行搜索：

`http://<host>:<port>/bin/querybuilder.json?property=jcr%3acontent%2fcq%3atemplate&property.value=%2fconf%2fwknd%2fsettings%2fwcm%2ftemplates%2fadventure-page-template&type=cq%3aPage`

```xml
type=cq:Page
property=jcr:content/cq:template
property.value=/conf/wknd/settings/wcm/templates/adventure-page-template
```

### 搜索多个属性 {#search-for-multiple-properties}

当多次使用属性谓词时，必须再次添加数字前缀：

`http://<host>:<port>/bin/querybuilder.json?1_property=jcr%3acontent%2fcq%3atemplate&1_property.value=%2fconf%2fwknd%2fsettings%2fwcm%2ftemplates%2fadventure-page-template&2_property=jcr%3acontent%2fjcr%3atitle&2_property.value=Cycling%20Tuscany&type=cq%3aPage`

```xml
type=cq:Page
1_property=jcr:content/cq:template
1_property.value=/conf/wknd/settings/wcm/templates/adventure-page-template
2_property=jcr:content/jcr:title
2_property.value=Cycling Tuscany
```

### 搜索多个属性值 {#search-for-multiple-property-values}

为避免在要搜索资产的多个值(`"A" or "B" or "C"`)时，您可以向 `property` 谓词：

`http://<host>:<port>/bin/querybuilder.json?property=jcr%3atitle&property.1_value=Cycling%20Tuscany&property.2_value=Ski%20Touring&property.3_value=Whistler%20Mountain%20Biking`

```xml
property=jcr:title
property.1_value=Cycling Tuscany
property.2_value=Ski Touring
property.3_value=Whistler Mountain Biking
```

对于多值属性，您还可以要求多个值匹配(`"A" and "B" and "C"`):

`http://<host>:<port>/bin/querybuilder.json?property=jcr%3atitle&property.and=true&property.1_value=Cycling%20Tuscany&property.2_value=Ski%20Touring&property.3_value=Whistler%20Mountain%20Biking`

```xml
property=jcr:title
property.and=true
property.1_value=Cycling Tuscany
property.2_value=Ski Touring
property.3_value=Whistler Mountain Biking
```

## 优化返回的内容 {#refining-what-is-returned}

默认情况下，QueryBuilder JSON Servlet将为搜索结果中的每个节点返回一组默认属性（例如，路径、名称、标题等）。 为了控制返回的属性，您可以执行以下操作之一：

指定

```xml
p.hits=full
```

在这种情况下，每个节点都将包含所有属性：

`http://<host>:<port>/bin/querybuilder.json?p.hits=full&property=jcr%3atitle&property.value=Cycling%20Tuscany`

```xml
property=jcr:title
property.value=Cycling Tuscany
p.hits=full
```

使用

```xml
p.hits=selective
```

并指定要加入的属性

```xml
p.properties
```

以空格分隔：

`http://<host>:<port>/bin/querybuilder.json?p.hits=selective&p.properties=sling%3aresourceType%20jcr%3aprimaryType&property=jcr%3atitle&property.value=Cycling%20Tuscany`

```xml
property=jcr:title
property.value=Cycling Tuscany
p.hits=selective
p.properties=sling:resourceType jcr:primaryType
```

另外，您还可以在查询生成器响应中包含子节点。 要执行此操作，您需要指定

```xml
p.nodedepth=n
```

where `n` 是您希望查询返回的级别数。 请注意，要返回子节点，必须由属性选择器指定该节点

```xml
p.hits=full
```

示例:

`http://<host>:<port>/bin/querybuilder.json?p.hits=full&p.nodedepth=5&property=jcr%3atitle&property.value=Cycling%20Tuscany`

```xml
property=jcr:title
property.value=Cycling Tuscany
p.hits=full
p.nodedepth=5
```

## 更多谓词 {#morepredicates}

有关更多谓词，请参阅 [“查询生成器谓词引用”页](query-builder-predicates.md).

您还可以检查 [的Javadoc `PredicateEvaluator` 类](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/eval/PredicateEvaluator.html). 这些类的Javadoc包含可使用的属性列表。

类名称的前缀(例如， `similar` in [`SimilarityPredicateEvaluator`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/eval/SimilarityPredicateEvaluator.html))表示 *主体属性* 全班同学。 此属性也是要在查询中使用的谓词的名称（小写）。

对于此类主体属性，您可以缩短查询并使用 `similar=/content/en` 而不是完全限定的变体 `similar.similar=/content/en`. 完全限定的表单必须用于类的所有非主属性。

## 查询生成器API使用示例 {#example-query-builder-api-usage}

```java
   String fulltextSearchTerm = "WKND";

    // create query description as hash map (simplest way, same as form post)
    Map<String, String> map = new HashMap<String, String>();

// create query description as hash map (simplest way, same as form post)
    map.put("path", "/content");
    map.put("type", "cq:Page");
    map.put("group.p.or", "true"); // combine this group with OR
    map.put("group.1_fulltext", fulltextSearchTerm);
    map.put("group.1_fulltext.relPath", "jcr:content");
    map.put("group.2_fulltext", fulltextSearchTerm);
    map.put("group.2_fulltext.relPath", "jcr:content/@cq:tags");

    // can be done in map or with Query methods
    map.put("p.offset", "0"); // same as query.setStart(0) below
    map.put("p.limit", "20"); // same as query.setHitsPerPage(20) below

    Query query = builder.createQuery(PredicateGroup.create(map), session);
    query.setStart(0);
    query.setHitsPerPage(20);

    SearchResult result = query.getResult();

    // paging metadata
    int hitsPerPage = result.getHits().size(); // 20 (set above) or lower
    long totalMatches = result.getTotalMatches();
    long offset = result.getStartIndex();
    long numberOfPages = totalMatches / 20;

    //Place the results in XML to return to client
    DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
    DocumentBuilder builder = factory.newDocumentBuilder();
    Document doc = builder.newDocument();

    //Start building the XML to pass back to the AEM client
    Element root = doc.createElement( "results" );
    doc.appendChild( root );

    // iterating over the results
    for (Hit hit : result.getHits()) {
       String path = hit.getPath();

      //Create a result element
      Element resultel = doc.createElement( "result" );
      root.appendChild( resultel );

      Element pathel = doc.createElement( "path" );
      pathel.appendChild( doc.createTextNode(path ) );
      resultel.appendChild( pathel );
    }
```

使用查询生成器(JSON)Servlet通过HTTP执行的同一查询：

`http://<host>:<port>/bin/querybuilder.json?path=/content&type=cq:Page&group.p.or=true&group.1_fulltext=WKND&group.1_fulltext.relPath=jcr:content&group.2_fulltext=WKND&group.2_fulltext.relPath=jcr:content/@cq:tags&p.offset=0&p.limit=20`

## 存储和加载查询 {#storing-and-loading-queries}

查询可以存储到存储库中，以便您稍后使用。 的 `QueryBuilder` 提供 `storeQuery` 方法（具有以下签名）：

```java
void storeQuery(Query query, String path, boolean createFile, Session session) throws RepositoryException, IOException;
```

使用 [`QueryBuilder#storeQuery`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/QueryBuilder.html#storeQuery-com.day.cq.search.Query-java.lang.String-boolean-javax.jcr.Session-) 方法，给定 `Query` 将作为文件或作为属性存储到存储库中， `createFile` 参数值。 以下示例显示如何保存 `Query` 路径 `/mypath/getfiles` 作为文件：

```java
builder.storeQuery(query, "/mypath/getfiles", true, session);
```

以前存储的任何查询都可以使用 [`QueryBuilder#loadQuery`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/QueryBuilder.html#loadQuery-java.lang.String-javax.jcr.Session-) 方法：

```java
Query loadQuery(String path, Session session) throws RepositoryException, IOException
```

例如， `Query` 存储到路径 `/mypath/getfiles` 代码片段可以加载：

```java
Query loadedQuery = builder.loadQuery("/mypath/getfiles", session);
```

## 测试和调试 {#testing-and-debugging}

要播放和调试查询生成器查询，您可以使用位于

`http://<host>:<port>/libs/cq/search/content/querydebug.html`

或在以下位置使用查询生成器JSON servlet

`http://<host>:<port>/bin/querybuilder.json?path=/tmp`

`path=/tmp` 只是一个示例。

### 常规调试Recommendations {#general-debugging-recommendations}

### 通过日志获取可解释的XPath {#obtain-explain-able-xpath-via-logging}

解释 **全部** 在开发周期中针对目标索引集进行查询。

1. 为QueryBuilder启用DEBUG日志以获取基础、可解释的XPath查询
   * 导航到 `https://<host>:<port>/system/console/slinglog`。为创建新的日志记录器 `com.day.cq.search.impl.builder.QueryImpl` at **调试**.
1. 为上述类启用DEBUG后，日志将显示查询生成器生成的XPath。
1. 从关联的查询生成器查询的日志条目中复制XPath查询，例如：
   * `com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "WKND") or jcr:contains(jcr:content/@cq:tags, "WKND"))]`
1. 将XPath查询粘贴到Explain Query as XPath中，以获取查询计划。

### 通过查询生成器调试器获取可解释的XPath {#obtain-explain-able-xpath-via-the-query-builder-debugger}

使用AEM查询生成器调试器生成可解释的XPath查询。

![查询生成器调试器](assets/query-builder-debugger.png)

1. 在查询生成器调试器中提供查询生成器查询
1. 执行搜索
1. 获取生成的XPath
1. 将XPath查询粘贴到Explain Query as XPath中，以获取查询计划

>[!NOTE]
>
>非查询生成器查询(XPath、JCR-SQL2)可直接提供给“解释查询”。

## 使用日志记录调试查询 {#debugging-queries-with-logging}

>[!NOTE]
>
>记录器的配置在文档中有介绍 [记录](/help/implementing/developing/introduction/logging.md).

执行上一节所述的查询时查询生成器实现的日志输出（信息级别） [测试和调试：](#testing-and-debugging)

```xml
com.day.cq.search.impl.builder.QueryImpl executing query (predicate tree):
null=group: limit=20, offset=0[
    {group=group: or=true[
        {1_fulltext=fulltext: fulltext=WKND, relPath=jcr:content}
        {2_fulltext=fulltext: fulltext=WKND, relPath=jcr:content/@cq:tags}
    ]}
    {path=path: path=/content}
    {type=type: type=cq:Page}
]
com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "WKND") or jcr:contains(jcr:content/@cq:tags, "WKND"))]
com.day.cq.search.impl.builder.QueryImpl no filtering predicates
com.day.cq.search.impl.builder.QueryImpl query execution took 69 ms
```

如果您的查询使用谓词计算器进行筛选，或者使用按比较器自定义顺序的查询，查询中也会注意到这一点：

```xml
com.day.cq.search.impl.builder.QueryImpl executing query (predicate tree):
null=group: [
    {nodename=nodename: nodename=*.jar}
    {orderby=orderby: orderby=@jcr:content/jcr:lastModified}
    {type=type: type=nt:file}
]
com.day.cq.search.impl.builder.QueryImpl custom order by comparator: jcr:content/jcr:lastModified
com.day.cq.search.impl.builder.QueryImpl XPath query: //element(*, nt:file)
com.day.cq.search.impl.builder.QueryImpl filtering predicates: {nodename=nodename: nodename=*.jar}
com.day.cq.search.impl.builder.QueryImpl query execution took 272 ms
```

## Javadoc链接 {#javadoc-links}

| **Javadoc** | **描述** |
|---|---|
| [com.day.cq.search](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/package-summary.html) | 基本查询生成器和查询API |
| [com.day.cq.search.result](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/result/package-summary.html) | 结果API |
| [com.day.cq.search.facets](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/facets/package-summary.html) | Facet |
| [com.day.cq.search.facets.buckets](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/facets/buckets/package-summary.html) | 存储段（包含在Facet中） |
| [com.day.cq.search.eval](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/eval/package-summary.html) | 谓词计算器 |
| [com.day.cq.search.facets.extractors](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/facets/extractors/package-summary.html) | 面提取器（用于评估器） |
| [com.day.cq.search.writer](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/writer/package-summary.html) | 查询生成器Servlet的JSON结果点击写入程序(`/bin/querybuilder.json`) |
