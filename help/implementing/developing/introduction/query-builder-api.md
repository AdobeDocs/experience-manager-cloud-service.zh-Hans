---
title: 查询生成器 API
description: Asset Share Query Builder的功能會透過Java API和REST API公開。
exl-id: d5f22422-c9da-4c9d-b81c-ffa5ea7cdc87
source-git-commit: 47910a27118a11a8add6cbcba6a614c6314ffe2a
workflow-type: tm+mt
source-wordcount: '2040'
ht-degree: 0%

---

# 查询生成器 API {#query-builder-api}

查詢產生器提供查詢AEM內容存放庫的簡單方式。 此功能會透過Java API和REST API公開。 本檔案說明這些API。

伺服器端查詢產生器([`QueryBuilder`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/QueryBuilder.html))將接受查詢說明、建立並執行XPath查詢、選擇性地篩選結果集，以及視需要擷取Facet。

查詢說明只是一組述詞([`Predicate`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/Predicate.html))。 範例包括全文檢索述詞，其對應至 `jcr:contains()` XPath中的函式。

對於每個述詞型別，都有一個求值器元件([`PredicateEvaluator`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/eval/PredicateEvaluator.html))，知道如何處理XPath、篩選和Facet擷取的特定述詞。 建立自訂評估器非常容易，可透過OSGi元件執行階段插入。

REST API可讓您透過HTTP存取完全相同的功能，且回應會以JSON傳送。

>[!NOTE]
>
>QueryBuilder API是使用JCR API建置。 您也可以使用OSGi套件中的JCR API來查詢AEM JCR。 如需詳細資訊，請參閱 [使用JCR API查詢Adobe Experience Manager資料](https://helpx.adobe.com/experience-manager/using/querying-experience-manager-data-using1.html).

## Gem講座 {#gem-session}

[AEM Gems](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-index.html) 是Adobe專家為Adobe Experience Manager提供的一系列深入技術探討。

您可以 [檢閱查詢產生器專屬的工作階段](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-search-forms-using-querybuilder.html) 以取得工具的概述和使用。

## 範例查詢 {#sample-queries}

這些範例以Java屬性樣式標籤法提供。 若要搭配Java API使用，請使用Java `HashMap` 與下列API範例相同。

對於 `QueryBuilder` JSON Servlet，每個範例都包含指向AEM安裝的範例連結(在預設位置， `http://<host>:<port>`)。 請注意，您必須先登入您的AEM執行個體，才能使用這些連結。

>[!CAUTION]
>
>依預設，查詢產生器JSON servlet最多可顯示10次點選。
>
>新增以下引數可讓servlet顯示所有查詢結果：
>
>`p.limit=-1`

>[!NOTE]
>
>若要在瀏覽器中檢視傳回的JSON資料，您可能會想要使用外掛程式，例如Firefox適用的JSONView。

### 傳回所有結果 {#returning-all-results}

下列查詢將 **傳回10個結果** （精確地說，最多為10個），但通知您 **點選次數：** 實際可用的：

`http://<host>:<port>/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=wknd/components/structure/page&1_property.operation=like&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=wknd/components/structure/page
1_property.operation=like
orderby=path
```

相同查詢（使用引數） `p.limit=-1`)會 **傳回所有結果** （根據您的執行個體，此數字可能會很高）：

`http://<host>:<port>/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=wknd/components/structure/page&1_property.operation=like&orderby=path&p.limit=-1`

```xml
path=/content
1_property=sling:resourceType
1_property.value=wknd/components/structure/page
1_property.operation=like
p.limit=-1
orderby=path
```

### 使用p.guessTotal傳回結果 {#using-p-guesstotal-to-return-the-results}

目的 `p.guessTotal` 引數為傳回適當數目的結果，可藉由結合最小可行值來顯示 `p.offset` 和 `p.limit` 值。 使用此引數的優點是在大型結果集中改善效能。 這樣可避免計算完整總計(例如呼叫 `result.getSize()`)並讀取整個結果集，一直最佳化至OAK引擎和索引。 在執行時間和記憶體使用量都有數十萬項結果時，這可能會導致重大差異。

此引數的缺點是使用者看不到確切的總數。 但您可以設定最小值，例如 `p.guessTotal=1000` 因此它一律會讀取高達1000，因此您可取得較小結果集的精確總計，但若超過此值，您只能顯示「及其他」。

新增 `p.guessTotal=true` 若要檢視其運作方式，請執行下列動作：

`http://<host>:<port>/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=wknd/components/structure/page&1_property.operation=like&p.guessTotal=true&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=wknd/components/structure/page
1_property.operation=like
p.guessTotal=true
orderby=path
```

查詢會傳回 `p.limit` 預設 `10` 結果包含 `0` offset：

```xml
"success": true,
"results": 10,
"total": 10,
"more": true,
"offset": 0,
```

您也可以使用數值來計數，最多可自訂結果數量上限。 使用與上述相同的查詢，但變更值 `p.guessTotal` 至 `50`：

`http://<host>:<port>/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=wknd/components/structure/page&1_property.operation=like&p.guessTotal=50&orderby=path`

它會傳回一個數字，預設限製為10個結果，位移為0，但最多只會顯示50個結果：

```xml
"success": true,
"results": 10,
"total": 50,
"more": true,
"offset": 0,
```

### 實作分頁 {#implementing-pagination}

依預設，查詢產生器也會提供點選次數。 根據結果大小，這可能需要很長的時間，因為要判斷準確的計數，需要檢查存取控制的每個結果。 總計主要用於為一般使用者UI實作分頁。 由於判斷確切計數可能會變慢，建議使用guessTotal功能來實作分頁。

例如，UI可以調整以下方法：

* 取得並顯示點選總數的精確計數([SearchResult.getTotalMatches()](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/result/SearchResult.html#getTotalMatches) 或中的總計 `querybuilder.json` response)小於或等於100；
* 設定 `guessTotal` 至100，同時呼叫查詢產生器。

* 回應可能會產生下列結果：

   * `total=43`， `more=false`  — 表示點選總數為43。 UI可以在第一個頁面中顯示最多十個結果，並為接下來的三個頁面提供分頁。 您也可以使用此實作來顯示描述性文字，例如 **「找到43個結果」**.
   * `total=100`， `more=true`  — 表示點選總數大於100，但不確定確切計數。 UI最多可顯示10個做為第一頁的一部分，並為接下來的10個頁面提供分頁。 您也可以使用此選項來顯示文字，例如 **「找到100個以上的結果」**. 當使用者前往下一頁時，對查詢產生器的呼叫將增加限制 `guessTotal` 以及 `offset` 和 `limit` 引數。

`guessTotal` 當UI需要使用無限捲動時，也應使用，以避免Query Builder判斷確切的點選計數。

### 尋找jar檔案並對其進行排序，最新的先排序 {#find-jar-files-and-order-them-newest-first}

`http://<host>:<port>/bin/querybuilder.json?type=nt:file&nodename=*.jar&orderby=@jcr:content/jcr:lastModified&orderby.sort=desc`

```xml
type=nt:file
nodename=*.jar
orderby=@jcr:content/jcr:lastModified
orderby.sort=desc
```

### 尋找所有頁面，並按上次修改時間排序 {#find-all-pages-and-order-them-by-last-modified}

`http://<host>:<port>/bin/querybuilder.json?type=cq:Page&orderby=@jcr:content/cq:lastModified`

```xml
type=cq:Page
orderby=@jcr:content/cq:lastModified
```

### 尋找所有頁面，並按上次修改時間（降序）排序 {#find-all-pages-and-order-them-by-last-modified-but-descending}

`http://<host>:<port>/bin/querybuilder.json?type=cq:Page&orderby=@jcr:content/cq:lastModified&orderby.sort=desc`

```xml
type=cq:Page
orderby=@jcr:content/cq:lastModified
orderby.sort=desc
```

### 全文檢索搜尋，依分數排序 {#fulltext-search-ordered-by-score}

`http://<host>:<port>/bin/querybuilder.json?fulltext=Management&orderby=@jcr:score&orderby.sort=desc`

```xml
fulltext=Management
orderby=@jcr:score
orderby.sort=desc
```

### 搜尋具有特定標籤的頁面 {#search-for-pages-tagged-with-a-certain-tag}

`http://<host>:<port>/bin/querybuilder.json?type=cq:Page&tagid=wknd:activity/cycling&tagid.property=jcr:content/cq:tags`

```xml
type=cq:Page
tagid=wknd:activity/cycling
tagid.property=jcr:content/cq:tags
```

使用 `tagid` 如果您知道明確的標籤ID，請依照此範例使用述詞。

使用 `tag` 標籤標題路徑的述詞（不含空格）。

因為在上一個範例中，您搜尋的頁面(`cq:Page` 節點)，則您需要使用該節點的相對路徑 `tagid.property` 述詞，即 `jcr:content/cq:tags`. 根據預設， `tagid.property` 將只是 `cq:tags`.

### 搜尋多個路徑（使用群組） {#search-under-multiple-paths-using-groups}

`http://<host>:<port>/bin/querybuilder.json?fulltext=Experience&group.1_path=/content/wknd/us/en/magazine&group.2_path=/content/wknd/us/en/adventures&group.p.or=true`

```xml
fulltext=Experience
group.p.or=true
group.1_path=/content/wknd/us/en/magazine
group.2_path=/content/wknd/us/en/adventures
```

此查詢使用 *群組* (已命名 `group`)，其作用是在查詢中分隔子運算式，就像括弧在較標準符號中所做的那樣。 例如，先前的查詢可能會以更熟悉的樣式表示，例如：

`"Experience" and ("/content/wknd/us/en/magazine" or "/content/wknd/us/en/adventures")`

在範例的群組內， `path` 述詞使用多次。 若要區分和排序述詞的兩個執行個體（某些述詞需要排序），您必須為述詞加上前置詞 `N_` 位置 `N` 是排序索引。 在上一個範例中，產生的述詞是 `1_path` 和 `2_path`.

此 `p` 在 `p.or` 是一個特殊分隔符號，指示接續的內容(在此例中為 `or`)是 *引數* 群組的，而不是群組的子述詞，例如 `1_path`.

若否 `p.or` 然後所有述詞一起進行AND運算，也就是說，每個結果都必須滿足所有述詞。

>[!NOTE]
>
>您無法在一個查詢中使用相同的數值首碼，即使對於不同的述詞亦然。

### 搜尋屬性 {#search-for-properties}

您在這裡使用 `cq:template` 屬性：

`http://<host>:<port>/bin/querybuilder.json?property=cq%3atemplate&property.value=%2fconf%2fwknd%2fsettings%2fwcm%2ftemplates%2fadventure-page-template&type=cq%3aPageContent`

```xml
type=cq:PageContent
property=cq:template
property.value=/conf/wknd/settings/wcm/templates/adventure-page-template
```

其缺點在於 `jcr:content` 會傳回頁面的節點，而非頁面本身。 若要解決此問題，您可以依相對路徑搜尋：

`http://<host>:<port>/bin/querybuilder.json?property=jcr%3acontent%2fcq%3atemplate&property.value=%2fconf%2fwknd%2fsettings%2fwcm%2ftemplates%2fadventure-page-template&type=cq%3aPage`

```xml
type=cq:Page
property=jcr:content/cq:template
property.value=/conf/wknd/settings/wcm/templates/adventure-page-template
```

### 搜尋多個屬性 {#search-for-multiple-properties}

多次使用屬性述詞時，您必須再次新增數字首碼：

`http://<host>:<port>/bin/querybuilder.json?1_property=jcr%3acontent%2fcq%3atemplate&1_property.value=%2fconf%2fwknd%2fsettings%2fwcm%2ftemplates%2fadventure-page-template&2_property=jcr%3acontent%2fjcr%3atitle&2_property.value=Cycling%20Tuscany&type=cq%3aPage`

```xml
type=cq:Page
1_property=jcr:content/cq:template
1_property.value=/conf/wknd/settings/wcm/templates/adventure-page-template
2_property=jcr:content/jcr:title
2_property.value=Cycling Tuscany
```

### 搜尋多個屬性值 {#search-for-multiple-property-values}

若要在搜尋屬性的多個值時避免大型群組(`"A" or "B" or "C"`)，則可以將多個值提供給 `property` 述詞：

`http://<host>:<port>/bin/querybuilder.json?property=jcr%3atitle&property.1_value=Cycling%20Tuscany&property.2_value=Ski%20Touring&property.3_value=Whistler%20Mountain%20Biking`

```xml
property=jcr:title
property.1_value=Cycling Tuscany
property.2_value=Ski Touring
property.3_value=Whistler Mountain Biking
```

針對多值屬性，您也可以要求多個值相符(`"A" and "B" and "C"`)：

`http://<host>:<port>/bin/querybuilder.json?property=jcr%3atitle&property.and=true&property.1_value=Cycling%20Tuscany&property.2_value=Ski%20Touring&property.3_value=Whistler%20Mountain%20Biking`

```xml
property=jcr:title
property.and=true
property.1_value=Cycling Tuscany
property.2_value=Ski Touring
property.3_value=Whistler Mountain Biking
```

## 精簡傳回的專案 {#refining-what-is-returned}

依預設，QueryBuilder JSON Servlet會傳回搜尋結果中每個節點的預設屬性集（例如路徑、名稱、標題等）。 若要取得傳回哪些屬性的控制權，您可以執行下列任一項作業：

指定

```xml
p.hits=full
```

在這種情況下，每個節點都將包含所有屬性：

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

並指定要加入的屬性

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

另一個您可以做的是在查詢產生器回應中包含子節點。 若要這麼做，您需要指定

```xml
p.nodedepth=n
```

位置 `n` 是您希望查詢傳回的層級數。 請注意，若要傳回子節點，它必須由屬性選取器指定

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

## 更多述詞 {#morepredicates}

如需更多述詞，請參閱 [查詢產生器述詞參考頁面](query-builder-predicates.md).

您也可以檢查 [的Javadoc `PredicateEvaluator` 類別](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/eval/PredicateEvaluator.html). 這些類別的Javadoc包含您可以使用的屬性清單。

類別名稱的前置詞(例如 `similar` 在 [`SimilarityPredicateEvaluator`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/eval/SimilarityPredicateEvaluator.html))是 *主體屬性* 類別的。 此屬性也是要在查詢中使用的述詞名稱（小寫）。

對於這類主體屬性，您可以縮短查詢並使用 `similar=/content/en` 而不是完整變體 `similar.similar=/content/en`. 類別的所有非主要屬性都必須使用完整表單。

## 查詢產生器API使用範例 {#example-query-builder-api-usage}

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

使用查詢產生器(JSON) Servlet透過HTTP執行的相同查詢：

`http://<host>:<port>/bin/querybuilder.json?path=/content&type=cq:Page&group.p.or=true&group.1_fulltext=WKND&group.1_fulltext.relPath=jcr:content&group.2_fulltext=WKND&group.2_fulltext.relPath=jcr:content/@cq:tags&p.offset=0&p.limit=20`

## 儲存和載入查詢 {#storing-and-loading-queries}

查詢可以儲存在存放庫中，以便您稍後使用。 此 `QueryBuilder` 提供 `storeQuery` 具有下列簽章的方法：

```java
void storeQuery(Query query, String path, boolean createFile, Session session) throws RepositoryException, IOException;
```

使用時 [`QueryBuilder#storeQuery`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/QueryBuilder.html#storeQuery-com.day.cq.search.Query-java.lang.String-boolean-javax.jcr.Session-) 方法，給定 `Query` 會根據「 」以檔案或屬性的形式儲存至存放庫 `createFile` 引數值。 以下範例說明如何儲存 `Query` 至路徑 `/mypath/getfiles` 以檔案形式：

```java
builder.storeQuery(query, "/mypath/getfiles", true, session);
```

任何先前儲存的查詢都可使用從存放庫載入 [`QueryBuilder#loadQuery`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/QueryBuilder.html#loadQuery-java.lang.String-javax.jcr.Session-) 方法：

```java
Query loadQuery(String path, Session session) throws RepositoryException, IOException
```

例如， `Query` 儲存至路徑 `/mypath/getfiles` 可透過下列程式碼片段載入：

```java
Query loadedQuery = builder.loadQuery("/mypath/getfiles", session);
```

## 測試和偵錯 {#testing-and-debugging}

若要解決和偵錯Query Builder查詢，您可以使用Query Builder Debugger主控台：

`http://<host>:<port>/libs/cq/search/content/querydebug.html`

或查詢產生器JSON servlet位於

`http://<host>:<port>/bin/querybuilder.json?path=/tmp`

`path=/tmp` 只是一個範例。

### Recommendations一般偵錯 {#general-debugging-recommendations}

### 透過記錄取得可解釋的XPath {#obtain-explain-able-xpath-via-logging}

說明 **全部** 在開發週期期間針對目標索引集進行查詢。

1. 啟用QueryBuilder的DEBUG記錄檔，以取得基礎、可解釋的XPath查詢
   * 导航到 `https://<host>:<port>/system/console/slinglog`。建立新的記錄器 `com.day.cq.search.impl.builder.QueryImpl` 於 **偵錯**.
1. 為上述類別啟用DEBUG後，記錄會顯示Query Builder產生的XPath。
1. 從相關Query Builder查詢的記錄專案複製XPath查詢，例如：
   * `com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "WKND") or jcr:contains(jcr:content/@cq:tags, "WKND"))]`
1. 將XPath查詢貼入Explain Query as XPath以取得查詢計畫。

### 透過Query Builder Debugger取得可解釋的XPath {#obtain-explain-able-xpath-via-the-query-builder-debugger}

使用AEM Query Builder Debugger產生可解釋的XPath查詢。

![Query Builder Debugger](assets/query-builder-debugger.png)

1. 在Query Builder Debugger中提供查詢產生器查詢
1. 執行搜尋
1. 取得產生的XPath
1. 將XPath查詢貼入Explain Query做為XPath以取得查詢計畫

>[!NOTE]
>
>非查詢產生器查詢(XPath、JCR-SQL2)可直接提供給Explain查詢。

## 使用記錄功能偵錯查詢 {#debugging-queries-with-logging}

>[!NOTE]
>
>檔案中會說明記錄器的設定 [記錄](/help/implementing/developing/introduction/logging.md).

執行上一節所述的查詢時，查詢產生器實作的記錄輸出（資訊層級） [測試和偵錯：](#testing-and-debugging)

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

如果您的查詢使用述詞評估器，這些評估器會篩選或使用自訂的比較順序，這也會在查詢中記錄：

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

## Javadoc連結 {#javadoc-links}

| **Javadoc** | **描述** |
|---|---|
| [com.day.cq.search](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/package-summary.html) | 基本查詢產生器和查詢API |
| [com.day.cq.search.result](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/result/package-summary.html) | 結果API |
| [com.day.cq.search.facets](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/facets/package-summary.html) | Facet |
| [com.day.cq.search.facets.buckets](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/facets/buckets/package-summary.html) | 值區（包含在Facet中） |
| [com.day.cq.search.eval](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/eval/package-summary.html) | 述詞評估器 |
| [com.day.cq.search.facets.extractors](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/facets/extractors/package-summary.html) | Facet擷取器（適用於評估器） |
| [com.day.cq.search.writer](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/writer/package-summary.html) | 查詢產生器servlet的JSON結果點選寫入器(`/bin/querybuilder.json`) |
