---
title: 查询生成器 API
description: 资产共享查询生成器的功能通过Java API和REST API公开。
translation-type: tm+mt
source-git-commit: 6b754a866be7979984d613b95a6137104be05399
workflow-type: tm+mt
source-wordcount: '2039'
ht-degree: 0%

---


# 查询生成器 API {#query-builder-api}

查询 Builder优惠了一种查询AEM内容存储库的简单方式。 该功能通过Java API和REST API公开。 本文档介绍这些API。

服务器端查询生成器([`QueryBuilder`](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/QueryBuilder.html))将接受查询描述，创建并运行XPath查询，可选地过滤结果集，如果需要还提取彩块化。

查询描述只是一组谓词([`Predicate`](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/Predicate.html))。 示例包括一个全文谓词，它与XPath中的`jcr:contains()`函数相对应。

对于每个谓词类型，都有一个计算器组件([`PredicateEvaluator`](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/eval/PredicateEvaluator.html))，它了解如何处理XPath、筛选和facet提取的特定谓词。 创建自定义评估器非常容易，它们通过OSGi组件运行时插入。

REST API通过HTTP提供对完全相同功能的访问，响应以JSON格式发送。

>[!NOTE]
>
>QueryBuilder API是使用JCR API构建的。 您还可以从OSGi捆绑包中使用JCR API查询AEM JCR。 有关信息，请参阅[使用JCR API](https://helpx.adobe.com/experience-manager/using/querying-experience-manager-data-using1.html)查询Adobe Experience Manager数据。

## Gem会话{#gem-session}

[AEM ](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-index.html) Gemsis由Adobe专家提供一系列深入Adobe Experience Manager的技术。

您可以[查看专用于查询 builder](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-search-forms-using-querybuilder.html)的会话，以了解该工具的概述和使用。

## 示例查询{#sample-queries}

这些示例以Java属性样式表示法提供。 要将它们与Java API一起使用，请使用Java `HashMap`，如下面的API示例中所示。

对于`QueryBuilder` JSON Servlet，每个示例都包括指向AEM安装的示例链接（位于默认位置，`http://<host>:<port>`）。 请注意，在使用这些链接之前，您必须登录到AEM实例。

>[!CAUTION]
>
>默认情况下，查询 builder JSON servlet最多显示10次点击。
>
>添加以下参数后，servlet将显示所有查询结果：
>
>`p.limit=-1`

>[!NOTE]
>
>要在浏览器中视图返回的JSON数据，您可能希望使用JSONView for Firefox等插件。

### 返回所有结果{#returning-all-results}

以下查询将&#x200B;**返回十个结果**（或者确切地说，最多十个结果），但会通知您实际可用的&#x200B;**命中数：**:

`http://<host>:<port>/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=wknd/components/structure/page&1_property.operation=like&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=wknd/components/structure/page
1_property.operation=like
orderby=path
```

同一查询（参数为`p.limit=-1`）将&#x200B;**返回所有结果**（根据您的实例，这可能是一个高数字）：

`http://<host>:<port>/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=wknd/components/structure/page&1_property.operation=like&orderby=path&p.limit=-1`

```xml
path=/content
1_property=sling:resourceType
1_property.value=wknd/components/structure/page
1_property.operation=like
p.limit=-1
orderby=path
```

### 使用p.guessTotal返回结果{#using-p-guesstotal-to-return-the-results}

`p.guessTotal`参数的目的是返回通过组合最小可行`p.offset`和`p.limit`值可以显示的适当数目的结果。 使用此参数的优点是在大结果集下提高了性能。 这避免了计算全部总数（例如调用`result.getSize()`）和读取整个结果集，并一直优化到OAK引擎和索引。 当在执行时间和内存使用方面有数十万个结果时，这可能是一个显着的差异。

该参数的缺点是用户看不到确切的总数。 但是，您可以设置一个像`p.guessTotal=1000`这样的最小数字，这样它将始终读取1000，因此您可以获得较小结果集的确切总计，但是，如果它大于此值，则只能显示“和更多”。

将`p.guessTotal=true`添加到以下查询，了解其工作方式：

`http://<host>:<port>/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=wknd/components/structure/page&1_property.operation=like&p.guessTotal=true&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=wknd/components/structure/page
1_property.operation=like
p.guessTotal=true
orderby=path
```

查询将返回`10`的`p.limit`默认值，其结果具有`0`偏移：

```xml
"success": true,
"results": 10,
"total": 10,
"more": true,
"offset": 0,
```

您还可以使用数值计算最多自定义的最大结果数。 使用与上面相同的查询，但将`p.guessTotal`的值更改为`50`:

`http://<host>:<port>/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=wknd/components/structure/page&1_property.operation=like&p.guessTotal=50&orderby=path`

它将返回一个与默认限制相同的数字，该数字为10个结果，偏移为0，但最多只显示50个结果：

```xml
"success": true,
"results": 10,
"total": 50,
"more": true,
"offset": 0,
```

### 实施分页{#implementing-pagination}

默认情况下，查询 Builder还会提供点击数。 根据结果大小，这可能需要很长时间，因为确定准确计数涉及检查每个结果的访问控制。 大多数情况下，总计用于为最终用户UI实现分页。 由于确定准确计数可能会很慢，建议使用guessTotal功能来实现分页。

例如，UI可以采用以下方法：

* 获取并显示总点击数([SearchResult.getTotalMatches()](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/result/SearchResult.html#getTotalMatches)或`querybuilder.json`响应中的总点击数)小于或等于100的准确计数；
* 调用查询 Builder时，将`guessTotal`设置为100。

* 响应可能具有以下结果：

   * `total=43`,  `more=false`  — 指示点击总数为43。UI在第一页中最多可显示十个结果，并为后三页提供分页。 您还可以使用此实现来显示描述性文本，如&#x200B;**&quot;43 results found&quot;**。
   * `total=100`,  `more=true`  — 指示点击总数大于100且不知道确切计数。UI在第一页中最多可显示十页，并为后十页提供分页。 您还可以使用它显示类似&#x200B;**&quot;找到100个以上结果&quot;**&#x200B;的文本。 当用户转到下一页时，对查询 Builder进行的调用将增加`guessTotal`以及`offset`和`limit`参数的限制。

`guessTotal` 还应用于UI需要使用无限滚动的情况，以避免查询 Builder确定确切的点击计数。

### 查找jar文件并对它们排序，最新优先{#find-jar-files-and-order-them-newest-first}

`http://<host>:<port>/bin/querybuilder.json?type=nt:file&nodename=*.jar&orderby=@jcr:content/jcr:lastModified&orderby.sort=desc`

```xml
type=nt:file
nodename=*.jar
orderby=@jcr:content/jcr:lastModified
orderby.sort=desc
```

### 查找所有页面并按上次修改时间{#find-all-pages-and-order-them-by-last-modified}对它们排序

`http://<host>:<port>/bin/querybuilder.json?type=cq:Page&orderby=@jcr:content/cq:lastModified`

```xml
type=cq:Page
orderby=@jcr:content/cq:lastModified
```

### 查找所有页面并按上次修改时间、降序{#find-all-pages-and-order-them-by-last-modified-but-descending}排序

`http://<host>:<port>/bin/querybuilder.json?type=cq:Page&orderby=@jcr:content/cq:lastModified&orderby.sort=desc`

```xml
type=cq:Page
orderby=@jcr:content/cq:lastModified
orderby.sort=desc
```

### 全文搜索，按分数{#fulltext-search-ordered-by-score}排序

`http://<host>:<port>/bin/querybuilder.json?fulltext=Management&orderby=@jcr:score&orderby.sort=desc`

```xml
fulltext=Management
orderby=@jcr:score
orderby.sort=desc
```

### 搜索具有特定标记{#search-for-pages-tagged-with-a-certain-tag}的页面

`http://<host>:<port>/bin/querybuilder.json?type=cq:Page&tagid=wknd:activity/cycling&tagid.property=jcr:content/cq:tags`

```xml
type=cq:Page
tagid=wknd:activity/cycling
tagid.property=jcr:content/cq:tags
```

如果您知道显式标记ID，请使用示例中的`tagid`谓词。

使用`tag`谓词作为标记标题路径（不带空格）。

因为，在上例中，您正在搜索页面（`cq:Page`节点），您需要为`tagid.property`谓词使用该节点的相对路径，该谓词为`jcr:content/cq:tags`。 默认情况下，`tagid.property`只是`cq:tags`。

### 搜索多个路径（使用组）{#search-under-multiple-paths-using-groups}

`http://<host>:<port>/bin/querybuilder.json?fulltext=Experience&group.1_path=/content/wknd/us/en/magazine&group.2_path=/content/wknd/us/en/adventures&group.p.or=true`

```xml
fulltext=Experience
group.p.or=true
group.1_path=/content/wknd/us/en/magazine
group.2_path=/content/wknd/us/en/adventures
```

此查询使用&#x200B;*group*（名为`group`），它用于在查询中限定子表达式，就像括号在更标准的符号中所做的那样。 例如，上一个查询可能以更熟悉的样式表示为：

`"Experience" and ("/content/wknd/us/en/magazine" or "/content/wknd/us/en/adventures")`

在示例中的组中，将多次使用`path`谓词。 要区分并排序谓词的两个实例（某些谓词需要排序），您必须在谓词前面添加`N_` ，其中`N`是排序索引。 在上例中，生成的谓词为`1_path`和`2_path`。

`p.or`中的`p`是一个特殊分隔符，指示以下内容（本例中为`or`）是组的&#x200B;*参数*，而不是组的子谓词，如`1_path`。

如果未给出`p.or` ，则所有谓词都是ANDed的，即每个结果必须满足所有谓词。

>[!NOTE]
>
>不能在一个查询中使用相同的数字前缀，即使对于不同的谓词也是如此。

### 搜索属性{#search-for-properties}

在此，您将使用`cq:template`属性搜索给定模板的所有页面：

`http://<host>:<port>/bin/querybuilder.json?property=cq%3atemplate&property.value=%2fconf%2fwknd%2fsettings%2fwcm%2ftemplates%2fadventure-page-template&type=cq%3aPageContent`

```xml
type=cq:PageContent
property=cq:template
property.value=/conf/wknd/settings/wcm/templates/adventure-page-template
```

这样做的缺点是返回页面的`jcr:content`节点，而不是页面本身。 要解决此问题，您可以按相对路径搜索：

`http://<host>:<port>/bin/querybuilder.json?property=jcr%3acontent%2fcq%3atemplate&property.value=%2fconf%2fwknd%2fsettings%2fwcm%2ftemplates%2fadventure-page-template&type=cq%3aPage`

```xml
type=cq:Page
property=jcr:content/cq:template
property.value=/conf/wknd/settings/wcm/templates/adventure-page-template
```

### 搜索多个属性{#search-for-multiple-properties}

当多次使用属性谓词时，您必须再次添加数字前缀：

`http://<host>:<port>/bin/querybuilder.json?1_property=jcr%3acontent%2fcq%3atemplate&1_property.value=%2fconf%2fwknd%2fsettings%2fwcm%2ftemplates%2fadventure-page-template&2_property=jcr%3acontent%2fjcr%3atitle&2_property.value=Cycling%20Tuscany&type=cq%3aPage`

```xml
type=cq:Page
1_property=jcr:content/cq:template
1_property.value=/conf/wknd/settings/wcm/templates/adventure-page-template
2_property=jcr:content/jcr:title
2_property.value=Cycling Tuscany
```

### 搜索多个属性值{#search-for-multiple-property-values}

要避免在要搜索属性(`"A" or "B" or "C"`)的多个值时出现大组，可以向`property`谓词提供多个值：

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

## 优化返回的内容{#refining-what-is-returned}

默认情况下，QueryBuilder JSON Servlet将为搜索结果中的每个节点返回一组默认属性（例如路径、名称、标题等）。 要控制要返回的属性，您可以执行下列操作之一：

指定

```xml
p.hits=full
```

在这种情况下，将包括每个节点的所有属性：

`http://<host>:<port>/bin/querybuilder.json?p.hits=full&property=jcr%3atitle&property.value=Cycling%20Tuscany`

```xml
property=jcr:title
property.value=Cycling Tuscany
p.hits=full
```

用法

```xml
p.hits=selective
```

并指定要加入的属性

```xml
p.properties
```

用空格分隔：

`http://<host>:<port>/bin/querybuilder.json?p.hits=selective&p.properties=sling%3aresourceType%20jcr%3aprimaryType&property=jcr%3atitle&property.value=Cycling%20Tuscany`

```xml
property=jcr:title
property.value=Cycling Tuscany
p.hits=selective
p.properties=sling:resourceType jcr:primaryType
```

您还可以做的另一件事是在查询 Builder响应中包含子节点。 为此，您需要指定

```xml
p.nodedepth=n
```

其中`n`是您希望查询返回的级别数。 请注意，要返回子节点，必须由属性选择器指定

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

## 更多谓词{#morepredicates}

有关更多谓词，请参阅[“查询 Builder谓词引用”页](query-builder-predicates.md)。

您还可以检查`PredicateEvaluator`类](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/eval/PredicateEvaluator.html)的[Javadoc。 这些类的Javadoc包含可以使用的属性列表。

类名的前缀（例如，[`SimilarityPredicateEvaluator`](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/eval/SimilarityPredicateEvaluator.html)中的`similar`）是类的&#x200B;*principal属性*。 此属性也是要在查询中使用的谓词的名称（小写）。

对于此类主属性，您可以缩短查询并使用`similar=/content/en`，而不是完全限定的变体`similar.similar=/content/en`。 必须将完全限定的表单用于类的所有非主属性。

## 示例查询 Builder API使用{#example-query-builder-api-usage}

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

使用查询 Builder(JSON)Servlet通过HTTP执行的相同查询:

`http://<host>:<port>/bin/querybuilder.json?path=/content&type=cq:Page&group.p.or=true&group.1_fulltext=WKND&group.1_fulltext.relPath=jcr:content&group.2_fulltext=WKND&group.2_fulltext.relPath=jcr:content/@cq:tags&p.offset=0&p.limit=20`

## 存储和加载查询{#storing-and-loading-queries}

查询可以存储到存储库，以便您以后可以使用它们。 `QueryBuilder`为`storeQuery`方法提供以下签名：

```java
void storeQuery(Query query, String path, boolean createFile, Session session) throws RepositoryException, IOException;
```

使用[`QueryBuilder#storeQuery`](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/QueryBuilder.html#storeQuery-com.day.cq.search.Query-java.lang.String-boolean-javax.jcr.Session-)方法时，根据`createFile`参数值，给定的`Query`将作为文件或属性存储在存储库中。 下面的示例说明如何将`Query`保存到路径`/mypath/getfiles`中作为文件：

```java
builder.storeQuery(query, "/mypath/getfiles", true, session);
```

可以使用[`QueryBuilder#loadQuery`](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/QueryBuilder.html#loadQuery-java.lang.String-javax.jcr.Session-)方法从存储库加载任何以前存储的查询:

```java
Query loadQuery(String path, Session session) throws RepositoryException, IOException
```

例如，存储到路径`/mypath/getfiles`的`Query`可由以下代码片断加载：

```java
Query loadedQuery = builder.loadQuery("/mypath/getfiles", session);
```

## 测试和调试{#testing-and-debugging}

要播放和调试查询 Builder查询，可以使用查询 Builder调试器控制台

`http://<host>:<port>/libs/cq/search/content/querydebug.html`

或者，查询 Builder JSON servlet位于

`http://<host>:<port>/bin/querybuilder.json?path=/tmp`

`path=/tmp` 只是个例子。

### 常规调试Recommendations {#general-debugging-recommendations}

### 通过记录{#obtain-explain-able-xpath-via-logging}获取可解释的XPath

针对目标索引集说明开发周期中的&#x200B;**所有**&#x200B;查询。

1. 为QueryBuilder启用DEBUG日志以获得基础的、可解释的XPath查询
   * 导航至 `https://<host>:<port>/system/console/slinglog`. 在&#x200B;**DEBUG**&#x200B;为`com.day.cq.search.impl.builder.QueryImpl`创建新记录器。
1. 为上述类启用DEBUG后，日志将显示查询 Builder生成的XPath。
1. 从关联的查询 Builder查询的日志条目中复制XPath查询，例如：
   * `com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "WKND") or jcr:contains(jcr:content/@cq:tags, "WKND"))]`
1. 将XPath查询粘贴到Explain查询中作为XPath，以获取查询计划。

### 通过查询 Builder调试器{#obtain-explain-able-xpath-via-the-query-builder-debugger}获取可解释的XPath

使用AEM 查询 Builder调试器生成可解释的XPath查询。

![查询 Builder调试器](assets/query-builder-debugger.png)

1. 在查询 Builder调试器中提供查询 Builder查询
1. 执行搜索
1. 获取生成的XPath
1. 将XPath查询粘贴到Explain查询中作为XPath以获得查询计划

>[!NOTE]
>
>非查询 Builder查询(XPath、JCR-SQL2)可以直接提供给“解释查询”。

## 使用日志记录{#debugging-queries-with-logging}调试查询

>[!NOTE]
>
>记录器的配置在文档[Logging](/help/implementing/developing/introduction/logging.md)中有介绍。

执行上一节[测试和调试：](#testing-and-debugging)中所述的查询时，查询 builder实现的日志输出（INFO级别）

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

如果您有使用谓词计算器进行筛选的查询，或者使用按比较器进行的自定义顺序，则查询中也将注意到：

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

## Javadoc链接{#javadoc-links}

| **Javadoc** | **描述** |
|---|---|
| [com.day.cq.search](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/package-summary.html) | 基本查询 Builder和查询 API |
| [com.day.cq.search.result](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/result/package-summary.html) | 结果API |
| [com.day.cq.search.facets](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/facets/package-summary.html) | 彩块化 |
| [com.day.cq.search.facets.buckets](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/facets/buckets/package-summary.html) | 存储段（包含在facet中） |
| [com.day.cq.search.eval](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/eval/package-summary.html) | 谓词计算器 |
| [com.day.cq.search.facets.extractors](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/facets/extractors/package-summary.html) | Facet提取器（用于计算器） |
| [com.day.cq.search.writer](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/writer/package-summary.html) | 查询 Builder Servlet的JSON结果点击编写器(`/bin/querybuilder.json`) |
