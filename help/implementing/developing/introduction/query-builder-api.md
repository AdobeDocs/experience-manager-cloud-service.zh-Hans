---
title: 查询生成器 API
description: 资产共享查询生成器的功能通过Java&amp；trade； API和REST API公开。
exl-id: d5f22422-c9da-4c9d-b81c-ffa5ea7cdc87
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '1830'
ht-degree: 0%

---

# 查询生成器 API {#query-builder-api}

查询生成器提供了一种查询AEM内容存储库的简单方法。 该功能通过Java™ API和REST API公开。 本文档介绍了这些API。

服务器端查询生成器([`QueryBuilder`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/QueryBuilder.html))接受查询说明，创建并运行XPath查询，可以选择筛选结果集，并根据需要提取Facet。

查询描述只是一组谓词([`Predicate`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/Predicate.html))。 示例包括与XPath中的`jcr:contains()`函数对应的全文谓词。

对于每个谓词类型，都有一个计算器组件([`PredicateEvaluator`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/eval/PredicateEvaluator.html))，该组件知道如何处理XPath、筛选和Facet提取的特定谓词。 可以轻松创建自定义评估器，这些评估器通过OSGi组件运行时插入。

REST API通过HTTP提供对相同功能的访问，响应以JSON发送。

>[!NOTE]
>
>QueryBuilder API是使用JCR API构建的。 您还可以使用OSGi捆绑包中的JCR API查询AEM JCR。 有关信息，请参阅[使用JCR API查询Adobe Experience Manager数据](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/query-builder/querybuilder-api.html?lang=zh-Hans)。

## Gem会议 {#gem-session}

[AEM Gems](https://experienceleague.adobe.com/docs/events/experience-manager-gems-recordings/overview.html?lang=zh-Hans)是Adobe专家提供的一系列深入探讨Adobe Experience Manager的技术资料。

您可以[查看专门用于查询生成器的会话](https://experienceleague.adobe.com/docs/events/experience-manager-gems-recordings/gems2017/aem-search-forms-using-querybuilder.html?lang=zh-Hans)以了解该工具的概述和使用情况。

## 示例查询 {#sample-queries}

这些示例以Java™属性样式表示法提供。 要将其与Java™ API结合使用，请使用Java™ `HashMap`，如下面的API示例所示。

对于`QueryBuilder` JSON Servlet，每个示例都包含指向AEM安装的示例链接（默认位置`http://<host>:<port>`）。 在使用这些链接之前，请登录到您的AEM实例。

>[!CAUTION]
>
>默认情况下，查询生成器JSON Servlet最多显示10次点击。
>
>添加以下参数允许servlet显示所有查询结果：
>
>`p.limit=-1`

>[!NOTE]
>
>要在浏览器中查看返回的JSON数据，您可能要使用诸如JSONView for Firefox之类的插件。

### 返回所有结果 {#returning-all-results}

以下查询&#x200B;**返回十个结果**（或者确切地说，最多返回十个），但通知您可用的&#x200B;**点击数：**：

`http://<host>:<port>/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=wknd/components/structure/page&1_property.operation=like&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=wknd/components/structure/page
1_property.operation=like
orderby=path
```

相同的查询（带有参数`p.limit=-1`） **返回所有结果** （根据您的实例，它可能是一个很高的数字）：

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

`p.guessTotal`参数的目的是返回通过组合最小可行`p.offset`和`p.limit`值可以显示的适当数量的结果。 使用该参数的优点是改善了性能，且结果集大。 此参数还可避免计算完整总计（例如，调用`result.getSize()`）和读取整个结果集，这些结果集一直优化到Oak引擎和索引。 在执行时间和内存使用量方面，当结果达到数十万时，此过程可能会产生显着差异。

此参数的缺点是用户看不到确切的总数。 但您可以设置诸如`p.guessTotal=1000`之类的最小值，使其始终读取最多1000。 这样，您便可以获得较小结果集的准确总计，但如果更多结果集，则只能显示“和更多”。

将`p.guessTotal=true`添加到下面的查询中以查看其工作原理：

`http://<host>:<port>/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=wknd/components/structure/page&1_property.operation=like&p.guessTotal=true&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=wknd/components/structure/page
1_property.operation=like
p.guessTotal=true
orderby=path
```

该查询返回`p.limit`默认值，即`10`个包含`0`偏移量的结果：

```xml
"success": true,
"results": 10,
"total": 10,
"more": true,
"offset": 0,
```

您还可以使用数值来累加到自定义的最大结果数。 使用与上述相同的查询，但将`p.guessTotal`的值更改为`50`：

`http://<host>:<port>/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=wknd/components/structure/page&1_property.operation=like&p.guessTotal=50&orderby=path`

它会返回一个数字，该数字与带0偏移量、具有10个结果的默认限制相同，但只显示最多50个结果：

```xml
"success": true,
"results": 10,
"total": 50,
"more": true,
"offset": 0,
```

### 实施分页 {#implementing-pagination}

默认情况下，查询生成器还会提供点击数。 根据结果大小，此数字可能需要较长时间，因为确定准确计数涉及检查每个结果的访问控制。 总数主要用于为最终用户UI实现分页。 由于确定确切计数可能会较慢，建议您使用guessTotal功能实施分页。

例如，UI可以调整以下方法：

* 获取并显示总点击数的准确计数([SearchResult.getTotalMatches()](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/result/SearchResult.html#getTotalMatches)或`querybuilder.json`响应中的总计)小于或等于100；
* 将`guessTotal`设置为100以调用查询生成器。

* 响应可能会产生以下结果：

   * `total=43`， `more=false` — 表示点击总数为43。 UI可以在第一个页面中显示最多十个结果，并为后续三个页面提供分页。 您还可以使用此实现来显示描述性文本，如&#x200B;**&quot;43个找到的结果&quot;**。
   * `total=100`， `more=true` — 指示点击总数大于100，并且确切计数未知。 UI最多可以将10个作为第一页的一部分显示，并为接下来的10个页面提供分页。 您还可以使用此功能显示诸如&#x200B;**“找到100个以上的结果”**&#x200B;之类的文本。 当用户进入下一页时，调用查询生成器将增加`guessTotal`以及`offset`和`limit`参数的上限。

此外，在用户界面必须使用无限滚动以避免Query Builder确定确切点击计数的情况下，请使用`guessTotal`。

### 查找jar文件并对其进行排序，最新内容先于 {#find-jar-files-and-order-them-newest-first}

`http://<host>:<port>/bin/querybuilder.json?type=nt:file&nodename=*.jar&orderby=@jcr:content/jcr:lastModified&orderby.sort=desc`

```xml
type=nt:file
nodename=*.jar
orderby=@jcr:content/jcr:lastModified
orderby.sort=desc
```

### 查找所有页面并按上次修改时间对页面进行排序 {#find-all-pages-and-order-them-by-last-modified}

`http://<host>:<port>/bin/querybuilder.json?type=cq:Page&orderby=@jcr:content/cq:lastModified`

```xml
type=cq:Page
orderby=@jcr:content/cq:lastModified
```

### 查找所有页面，并按上次修改时间对页面进行排序（降序） {#find-all-pages-and-order-them-by-last-modified-but-descending}

`http://<host>:<port>/bin/querybuilder.json?type=cq:Page&orderby=@jcr:content/cq:lastModified&orderby.sort=desc`

```xml
type=cq:Page
orderby=@jcr:content/cq:lastModified
orderby.sort=desc
```

### 全文搜索，按得分排序 {#fulltext-search-ordered-by-score}

`http://<host>:<port>/bin/querybuilder.json?fulltext=Management&orderby=@jcr:score&orderby.sort=desc`

```xml
fulltext=Management
orderby=@jcr:score
orderby.sort=desc
```

### 搜索带有特定标记的页面 {#search-for-pages-tagged-with-a-certain-tag}

`http://<host>:<port>/bin/querybuilder.json?type=cq:Page&tagid=wknd:activity/cycling&tagid.property=jcr:content/cq:tags`

```xml
type=cq:Page
tagid=wknd:activity/cycling
tagid.property=jcr:content/cq:tags
```

如果您知道显式标记ID，请使用`tagid`谓词，如示例中所示。

为标记标题路径使用`tag`谓词（不含空格）。

在上一个示例中，由于您正在搜索页面（`cq:Page`节点），因此请使用该节点的`tagid.property`谓词的相对路径，即`jcr:content/cq:tags`。 默认情况下，`tagid.property`将为`cq:tags`。

### 搜索多个路径（使用组） {#search-under-multiple-paths-using-groups}

`http://<host>:<port>/bin/querybuilder.json?fulltext=Experience&group.1_path=/content/wknd/us/en/magazine&group.2_path=/content/wknd/us/en/adventures&group.p.or=true`

```xml
fulltext=Experience
group.p.or=true
group.1_path=/content/wknd/us/en/magazine
group.2_path=/content/wknd/us/en/adventures
```

此查询使用&#x200B;*组* （名为`group`），该组用于在查询中分隔子表达式，就像在更标准的符号中使用括号一样。 例如，上一个查询可能会以更熟悉的样式表示，如：

`"Experience" and ("/content/wknd/us/en/magazine" or "/content/wknd/us/en/adventures")`

在该示例中的组内，`path`谓词被多次使用。 要区分谓词的两个实例并对其进行排序（某些谓词需要排序），必须在谓词前面加上`N_`，其中`N`是排序索引。 在上一个示例中，生成的谓词是`1_path`和`2_path`。

`p.or`中的`p`是一个特殊分隔符，它指示后面的内容（在本例中为`or`）是组的&#x200B;*参数*，而不是组的子谓词，如`1_path`。

如果未给定`p.or`，则所有谓词都将进行AND运算，即，每个结果必须满足所有谓词。

>[!NOTE]
>
>不能在一个查询中使用相同的数字前缀，即使对于不同的谓词也是如此。

### 搜索属性 {#search-for-properties}

您在此处使用`cq:template`属性搜索给定模板的所有页面：

`http://<host>:<port>/bin/querybuilder.json?property=cq%3atemplate&property.value=%2fconf%2fwknd%2fsettings%2fwcm%2ftemplates%2fadventure-page-template&type=cq%3aPageContent`

```xml
type=cq:PageContent
property=cq:template
property.value=/conf/wknd/settings/wcm/templates/adventure-page-template
```

缺点是返回的是页面的`jcr:content`节点，而不是页面本身。 要解决此问题，您可以按相对路径搜索：

`http://<host>:<port>/bin/querybuilder.json?property=jcr%3acontent%2fcq%3atemplate&property.value=%2fconf%2fwknd%2fsettings%2fwcm%2ftemplates%2fadventure-page-template&type=cq%3aPage`

```xml
type=cq:Page
property=jcr:content/cq:template
property.value=/conf/wknd/settings/wcm/templates/adventure-page-template
```

### 搜索多个属性 {#search-for-multiple-properties}

多次使用属性谓词时，必须再次添加数字前缀：

`http://<host>:<port>/bin/querybuilder.json?1_property=jcr%3acontent%2fcq%3atemplate&1_property.value=%2fconf%2fwknd%2fsettings%2fwcm%2ftemplates%2fadventure-page-template&2_property=jcr%3acontent%2fjcr%3atitle&2_property.value=Cycling%20Tuscany&type=cq%3aPage`

```xml
type=cq:Page
1_property=jcr:content/cq:template
1_property.value=/conf/wknd/settings/wcm/templates/adventure-page-template
2_property=jcr:content/jcr:title
2_property.value=Cycling Tuscany
```

### 搜索多个属性值 {#search-for-multiple-property-values}

要搜索属性(`"A" or "B" or "C"`)的多个值时避免大型组，可以为`property`谓词提供多个值：

`http://<host>:<port>/bin/querybuilder.json?property=jcr%3atitle&property.1_value=Cycling%20Tuscany&property.2_value=Ski%20Touring&property.3_value=Whistler%20Mountain%20Biking`

```xml
property=jcr:title
property.1_value=Cycling Tuscany
property.2_value=Ski Touring
property.3_value=Whistler Mountain Biking
```

对于多值属性，您还可以要求多个值匹配(`"A" and "B" and "C"`)：

`http://<host>:<port>/bin/querybuilder.json?property=jcr%3atitle&property.and=true&property.1_value=Cycling%20Tuscany&property.2_value=Ski%20Touring&property.3_value=Whistler%20Mountain%20Biking`

```xml
property=jcr:title
property.and=true
property.1_value=Cycling Tuscany
property.2_value=Ski Touring
property.3_value=Whistler Mountain Biking
```

## 优化返回内容 {#refining-what-is-returned}

默认情况下，QueryBuilder JSON Servlet为搜索结果中的每个节点返回一组默认属性（例如，路径、名称和标题）。 要获得对返回哪些属性的控制权，您可以执行以下操作之一：

指定

```xml
p.hits=full
```

在这种情况下，每个节点包含所有属性：

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

并指定要访问的属性

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

您还可以在查询生成器响应中包含子节点。 指定

```xml
p.nodedepth=n
```

其中`n`是您希望查询返回的级别数。 对于要返回的子节点，必须由属性选择器指定

```xml
p.hits=full
```

示例：

`http://<host>:<port>/bin/querybuilder.json?p.hits=full&p.nodedepth=5&property=jcr%3atitle&property.value=Cycling%20Tuscany`

```xml
property=jcr:title
property.value=Cycling Tuscany
p.hits=full
p.nodedepth=5
```

## 更多谓词 {#morepredicates}

有关更多谓词，请参阅[查询生成器谓词引用页](query-builder-predicates.md)。

您还可以检查`PredicateEvaluator`类的[Javadoc](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/eval/PredicateEvaluator.html)。 这些类的Javadoc包含您可以使用的属性列表。

类名的前缀（例如，[`SimilarityPredicateEvaluator`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/eval/SimilarityPredicateEvaluator.html)中的`similar`）是该类的&#x200B;*主体属性*。 此属性也是要在查询中使用的谓词名称（小写）。

对于此类主体属性，您可以缩短查询并使用`similar=/content/en`而不是完全限定的变体`similar.similar=/content/en`。 全限定形式必须用于类的所有非主体属性。

## 示例查询生成器API用法 {#example-query-builder-api-usage}

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

使用查询生成器(JSON) Servlet通过HTTP执行的相同查询：

`http://<host>:<port>/bin/querybuilder.json?path=/content&type=cq:Page&group.p.or=true&group.1_fulltext=WKND&group.1_fulltext.relPath=jcr:content&group.2_fulltext=WKND&group.2_fulltext.relPath=jcr:content/@cq:tags&p.offset=0&p.limit=20`

## 存储和加载查询 {#storing-and-loading-queries}

查询可以存储在存储库中，以便您以后使用。 `QueryBuilder`为`storeQuery`方法提供了以下签名：

```java
void storeQuery(Query query, String path, boolean createFile, Session session) throws RepositoryException, IOException;
```

使用[`QueryBuilder#storeQuery`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/QueryBuilder.html#storeQuery-com.day.cq.search.Query-java.lang.String-boolean-javax.jcr.Session-)方法时，根据`createFile`参数值，给定的`Query`将作为文件或属性存储在存储库中。 以下示例显示如何将路径`/mypath/getfiles`的`Query`另存为文件：

```java
builder.storeQuery(query, "/mypath/getfiles", true, session);
```

可以使用[`QueryBuilder#loadQuery`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/QueryBuilder.html#loadQuery-java.lang.String-javax.jcr.Session-)方法从存储库加载任何以前存储的查询：

```java
Query loadQuery(String path, Session session) throws RepositoryException, IOException
```

例如，存储到路径`/mypath/getfiles`的`Query`可通过以下代码片段加载：

```java
Query loadedQuery = builder.loadQuery("/mypath/getfiles", session);
```

## 测试和调试 {#testing-and-debugging}

要绕过并调试Query Builder查询，您可以使用位于的Query Builder调试器控制台

`http://<host>:<port>/libs/cq/search/content/querydebug.html`

或者，也可以使用位于的查询生成器JSON Servlet

`http://<host>:<port>/bin/querybuilder.json?path=/tmp`

`path=/tmp`只是一个示例。

### 常规调试Recommendations {#general-debugging-recommendations}

### 通过日志记录获取可解释的XPath {#obtain-explain-able-xpath-via-logging}

说明在开发周期期间针对目标索引集进行的&#x200B;**所有**&#x200B;查询。

1. 启用QueryBuilder的DEBUG日志，以获取基础的可解释XPath查询
   * 导航到`https://<host>:<port>/system/console/slinglog`。 在&#x200B;**DEBUG**&#x200B;为`com.day.cq.search.impl.builder.QueryImpl`创建日志记录器。
1. 为上述类启用DEBUG后，日志会显示由Query Builder生成的XPath。
1. 从关联的Query Builder查询的日志条目中复制XPath查询，例如：
   * `com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "WKND") or jcr:contains(jcr:content/@cq:tags, "WKND"))]`
1. 将XPath查询作为XPath粘贴到Explain查询中，以便获取查询计划。

### 通过Query Builder Debugger获取可解释的XPath {#obtain-explain-able-xpath-via-the-query-builder-debugger}

使用AEM Query Builder调试器生成可解释的XPath查询。

![查询生成器调试器](assets/query-builder-debugger.png)

1. 在Query Builder调试器中提供Query Builder查询
1. 执行搜索
1. 获取生成的XPath
1. 将XPath查询作为XPath粘贴到Explain查询中，以便获取查询计划

>[!NOTE]
>
>可以直接提供非查询生成器查询(XPath、JCR-SQL2)来解释查询。

## 使用日志记录调试查询 {#debugging-queries-with-logging}

>[!NOTE]
>
>记录器的配置在文档[记录](/help/implementing/developing/introduction/logging.md)中描述。

执行上一节[测试和调试](#testing-and-debugging)中描述的查询时，查询生成器实现的日志输出（INFO级别）

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

如果您的查询使用谓词计算器，这些计算器过滤或使用按比较器排序的自定义规则，则查询中会记录该规则：

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
| [com.day.cq.search](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/package-summary.html) | 基本查询生成器和查询API |
| [com.day.cq.search.result](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/result/package-summary.html) | 结果API |
| [com.day.cq.search.facets](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/facets/package-summary.html) | Facet |
| [com.day.cq.search.facets.buckets](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/facets/buckets/package-summary.html) | 分段（包含在Facet中） |
| [com.day.cq.search.eval](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/eval/package-summary.html) | 谓词评估器 |
| [com.day.cq.search.facets.extractors](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/facets/extractors/package-summary.html) | Facet提取器（用于评估器） |
| [com.day.cq.search.writer](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/writer/package-summary.html) | 查询生成器servlet (`/bin/querybuilder.json`)的JSON结果点击编写器 |
