---
title: 查询生成器谓词参考
description: AEM as a Cloud Service中的查询生成器API的谓词引用。
exl-id: 77118ef7-4d29-470d-9c4b-20537a408940
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '2270'
ht-degree: 1%

---

# 查询生成器谓词参考 {#query-builder-predicate-reference}

## 常规 {#general}

### 根 {#root}

根谓词组。 它支持组的所有功能，并允许设置全局查询参数。

名称“root”从未在查询中使用；它是隐式的。

#### 属性 {#properties-18}

* **`p.offset`** — 指示结果页开始的数字，即要跳过多少项。
* **`p.limit`** — 表示页面大小的数字。
* **`p.guessTotal`** — 建议：避免计算完整结果总计，这可能代价高昂。 指示可计数的最大总数的数字（例如，1000，一个数字，该数字为用户提供对粗略大小的足够反馈以及用于较小结果的精确数字）。 或者，`true`仅计数到所需的最小值`p.offset` + `p.limit`。
* **`p.excerpt`** — 如果设置为`true`，则在结果中包含全文摘录。
* **`p.indexTag`** — 如果设置，将在查询中包含索引标记选项（请参阅[查询选项索引标记](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#query-option-index-tag)）。
* **`p.facetStrategy`** — 如果设置为`oak`，Query Builder将向Oak委派Facet提取（请参阅[Facet](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#facets)）。
* **`p.hits`** — （仅适用于JSON servlet）选择命中项作为JSON写入的方式，并使用这些标准命中项（可通过ResultHitWriter服务扩展）。
   * **`simple`** — 最小项目，如`path`、`title`、`lastmodified`、`excerpt`（如果已设置）。
   * **`full`** — 节点的sling JSON渲染，其中`jcr:path`指示点击的路径。 默认情况下，仅列出节点的直接属性，包括包含`p.nodedepth=N`的较深树，0表示整个无限子树。 添加`p.acls=true`以包含给定结果项上当前会话的JCR权限（映射： `create` = `add_node`，`modify` = `set_property`，`delete` = `remove`）。
   * **`selective`** — 仅在`p.properties`中指定的属性，该属性是以空格分隔的（在URL中使用`+`）相对路径列表。 如果相对路径的深度为`>1`，则这些属性表示为子对象。 特殊`jcr:path`属性包含点击的路径。

### 组 {#group}

此谓词允许构建嵌套条件。 组可以包含嵌套的组。 Query Builder查询中的所有内容都隐式位于根组中，该组也可以有`p.or`和`p.not`参数。

以下是将两个属性中的一个与值匹配的示例：

```text
group.p.or=true
group.1_property=jcr:title
group.1_property.value=My Page
group.2_property=navTitle
group.2_property.value=My Page
```

从概念上讲，它是`(1_property`或`2_property)`。

以下是嵌套组的示例：

```text
fulltext=Management
group.p.or=true
group.1_group.path=/content/wknd/ch/de
group.1_group.type=cq:Page
group.2_group.path=/content/dam/wknd
group.2_group.type=dam:Asset
```

在`/content/wknd/ch/de`中的页面或`/content/dam/wknd`中的资产中搜索术语&#x200B;**管理**。

从概念上讲，它是`fulltext AND ( (path AND type) OR (path AND type) )`。 出于性能原因，此类OR连接需要良好的索引。

#### 属性 {#properties-6}

* **`p.or`** — 如果设置为`true`，则组中只能有一个谓词匹配。 默认为`false`，表示所有规则必须匹配
* **`p.not`** — 如果设置为`true`，它将使组无效（默认为`false`）
* **`<predicate>`** — 添加嵌套谓词
* **`N_<predicate>`** — 同时添加多个嵌套谓词，如`1_property, 2_property, ...`

### orderby {#orderby}

此谓词允许对结果进行排序。 如果需要按多个属性排序，则必须使用数字前缀（如`1_orderby=first`、`2_oderby=second`）多次添加此谓词。

#### 属性 {#properties-13}

* **`orderby`** — 由前导@指示的JCR属性名称，例如`@jcr:lastModified`或`@jcr:content/jcr:title`，或者查询中的另一个谓词，例如`2_property`，要对其排序
* **`sort`** — 排序方向，`desc`表示降序，`asc`表示升序（默认）
* **`case`** — 如果设置为`ignore`，则排序不区分大小写，表示`a`在`B`之前；如果为空或缺席，则排序区分大小写，表示`B`在`a`之前

## 谓词 {#predicates}

### 布尔属性 {#boolproperty}

此谓词与JCR布尔属性匹配。 仅接受值`true`和`false`。 如果该值为`false`，则当该属性的值为`false`或根本不存在时，该值将匹配。 此谓词可用于检查仅在启用时设置的布尔标记。

继承的`operation`参数没有意义。

此谓词支持Facet提取并为每个`true`或`false`值提供存储段，但仅适用于现有属性。

#### 属性 {#properties}

* **`boolproperty`** — 属性的相对路径，例如`myFeatureEnabled`或`jcr:content/myFeatureEnabled`
* **`value`** — 要检查的属性，`true`或`false`的值

### contentfragment {#contentfragment}

此谓词将结果限制为内容片段。

* 它不支持筛选。
* 它不支持彩块化提取。

#### 属性 {#properties-1}

* **`contentfragment`** — 可与任何值一起使用来检查内容片段。

### `dateComparison` {#datecomparison}

此谓词将两个JCR日期属性相互进行比较。 可以测试它们是相等、不相等、大于还是大于或等于。

仅限过滤的谓词，不能使用搜索索引。

#### 属性 {#properties-2}

* **`property1`** — 指向第一个日期属性的路径
* **`property2`** — 指向第二个日期属性的路径
* **`operation`**
   * `=`表示完全匹配（默认）
   * 不相等比较的`!=`
   * `property1`的`>`大于`property2`
   * `property1`的`>=`大于或等于`property2`

### 日期范围 {#daterange}

此谓词根据日期/时间间隔匹配JCR日期属性。 使用ISO8601
日期和时间的格式(`YYYY-MM-DDTHH:mm:ss.SSSZ`)，并允许部分呈现，如`YYYY-MM-DD`。 或者，时间戳可以作为POSIX时间提供。

您可以查找介于两个时间戳之间的任何内容，比给定日期更新或更早的任何内容，也可以选择介于包含时间间隔和打开时间间隔之间的内容。

它支持Facet提取并提供存储段`today`、`this week`、`this month`、`last 3 months`、`this year`、`last year`和`earlier than last year`。

它不支持筛选。

#### 属性 {#properties-3}

* **`property`** - `DATE`属性的相对路径，例如`jcr:lastModified`
* **`lowerBound`** — 用于检查属性（例如，`2014-10-01`）的日期下限
* **`lowerOperation`** - `>` （较新）或`>=` （大于或等于），适用于`lowerBound`。 默认值为`>`
* **`upperBound`** — 检查属性的上限，例如`2014-10-01T12:15:00`
* **`upperOperation`** - `<` （较旧）或`<=` （等于或较旧）适用于`upperBound`。 默认值为`<`
* **`timeZone`** — 未作为ISO-8601日期字符串提供时要使用的时区ID。 默认值是系统的默认时区。

### 排除路径 {#excludepaths}

此谓词从路径与正则表达式匹配的结果中排除节点。

仅限过滤的谓词，不能使用搜索索引。

它不支持彩块化提取。

#### 属性 {#properties-4}

* **`excludepaths`** — 与结果路径匹配的正则表达式，从结果中排除匹配的路径。

### 全文 {#fulltext}

搜索全文索引中的术语。

它不支持筛选。

它不支持彩块化提取。

#### 属性 {#properties-5}

* **`fulltext`** — 全文搜索词
* **`relPath`** — 在属性或子节点中搜索的相对路径。 此属性是可选的。

### hasPermission {#haspermission}

此谓词将结果限制在当前会话具有指定[JCR权限的项目中。](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)

仅限过滤的谓词，不能使用搜索索引。 它不支持彩块化提取。

#### 属性 {#properties-7}

* **`hasPermission`** — 当前用户会话必须拥有的对相关节点的所有逗号分隔JCR权限。 例如，`jcr:write`，`jcr:modifyAccessControl`

### 语言 {#language}

此谓词查找特定语言的AEM页面。 它同时查看页面语言属性和页面路径，后者通常包括顶级网站结构中的语言或区域设置。

仅限过滤的谓词，不能使用搜索索引。

它支持Facet提取，并为每个唯一的语言代码提供存储桶。

#### 属性 {#properties-8}

* **`language`** - ISO语言代码，例如，`de`

### mainasset {#mainasset}

此谓词检查节点是否是DAM主资产而不是子资产。 它基本上是每个不在子资产节点内的节点。 它不检查`dam:Asset`节点类型。 若要使用此谓词，请设置`mainasset=true`或`mainasset=false`。 没有其他属性。

仅限过滤的谓词，不能使用搜索索引。

它支持彩块化提取，并为主资产和子资产提供两个存储桶。

#### 属性 {#properties-9}

* **`mainasset`** — 布尔值，`true`（主资产），`false`（子资产）

### memberOf {#memberof}

此谓词查找属于特定[sling资源集合](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/resource/collection/ResourceCollection.html)成员的项。

仅限过滤的谓词，不能使用搜索索引。

它不支持彩块化提取。

#### 属性 {#properties-10}

* **`memberOf`** - Sling资源集合的路径

### 节点名称 {#nodename}

此谓词与JCR节点名称匹配。

它支持Facet提取，并为每个唯一的节点名称（文件名）提供存储段。

#### 属性 {#properties-11}

* **`nodename`** — 允许使用通配符的节点名称模式： `*` =任何或不包含字符，`?` =任何字符，`[abc]` =仅包含括号中的字符

### notexpired {#notexpired}

此谓词通过检查JCR日期属性是否大于或等于当前服务器时间来匹配项。 它可用于检查`expiresAt`值，并将结果限制为仅包含尚未过期(`notexpired=true`)或已过期(`notexpired=false`)的值。

它不支持筛选。

它支持彩块化提取，其方式与[`daterange`](#daterange)谓词相同。

#### 属性 {#properties-12}

* **`notexpired`** — 布尔值，`true`表示尚未过期（日期在将来或等于），`false`表示过期（日期在过去）（必需）
* **`property`** — 要检查的`DATE`属性的相对路径（必需）

### 路径 {#path}

此谓词在给定路径内搜索。

它不支持彩块化提取。

#### 属性 {#properties-14}

* **`path`** — 定义路径模式。
   * 根据`exact`属性，整个子树匹配（如在xpath中附加`//*`，但请注意，它不包括基路径），或者只匹配精确路径，该路径可以包括通配符(`*`)。
      * 默认为`true`。
&lt;！—   *如果设置了`self`属性，则会搜索包含基节点的整个子树。—>
* **`exact`** — 如果`exact`是`true`，则确切的路径必须匹配，但它可以包含简单通配符(`*`)，这些通配符与名称匹配，但不匹配`/`；如果它是`false`（默认值），则包括所有后代（可选）。
* **`flat`** — 仅搜索直接子级（例如在xpath中附加`/*`）（仅在`exact`不是true或可选时使用）。
* **`self`** — 搜索子树，但包含作为路径指定的基节点（无通配符）。
   * *重要说明*：在查询生成器的当前实现中发现`self`属性存在问题，在查询中使用它可能无法生成正确的搜索结果。 更改`self`属性的当前实现也是不可行的，因为它可能会中断依赖它的现有应用程序。 由于此功能，`self`属性现已弃用；建议避免使用它。

### 属性 {#property}

此谓词与JCR属性及其值相匹配。

它支持方面提取，并为结果中的每个唯一属性值提供存储段。

#### 属性 {#properties-15}

* **`property`** — 属性的相对路径，例如`jcr:title`。
* **`value`** — 要检查属性的值；遵循JCR属性类型到字符串的转换。
* **`N_value`** — 使用`1_value`、`2_value`、...检查多个值（默认情况下与`OR`组合，如果`and=true`则为`AND`）。
* **`and`** — 设置为`true`以将多个值(`N_value`)与`AND`组合
* **`operation`**
   * `equals`表示完全匹配（默认）。
   * `unequals`进行不等式比较。
   * 使用`jcr:like` xpath函数的`like`（可选）。
   * 没有匹配项的`not`（例如，xpath中的`not(@prop)`，值参数将被忽略）。
   * `exists`是否存在检查。
      * `true`属性必须存在。
      * `false`与`not`相同，是默认值。
* **`depth`** — 属性/相对路径可以存在的通配符级别数（例如，`property=size depth=2`检查`node/size`、`node/*/size`和`node/*/*/size`）。

### rangeproperty {#rangeproperty}

此谓词根据间隔匹配JCR属性。 它适用于线性类型的属性，如`LONG`、`DOUBLE`和`DECIMAL`。 对于`DATE`，查看具有优化日期格式输入的[`daterange`](#daterange)谓词。

您可以定义下限、上限或同时定义两者。 也可以分别为下限和上限指定操作（例如，小于或小于或等于）。

它不支持彩块化提取。

#### 属性 {#properties-16}

* **`property`** — 属性的相对路径
* **`lowerBound`** — 检查属性的下限
* **`lowerOperation`** - `>` （默认）或`>=`适用于`lowerValue`
* **`upperBound`** — 检查属性的上限
* **`upperOperation`** - `<` （默认）或`<=`适用于`lowerValue`
* 如果检查的属性为Decimal类型，则为&#x200B;**`decimal`** - `true`

### 相对日期范围 {#relativedaterange}

此谓词使用相对于当前服务器时间的时间偏移，根据日期/时间间隔匹配`JCR DATE`属性。 您可以使用毫秒值或Bugzilla语法`1s 2m 3h 4d 5w 6M 7y`（一秒、两分钟、三小时、四天、五周、六个月、七年）指定`lowerBound`和`upperBound`。 前缀为`-`表示当前时间之前的负偏移。 如果仅指定`lowerBound`或`upperBound`，则另一个将默认为`0`，表示当前时间。

例如：

* `upperBound=1h` （没有任何`lowerBound`）在下一个小时选择任何内容
* `lowerBound=-1d` （无`upperBound`）选择过去24小时内的任何内容
* `lowerBound=-6M`和`upperBound=-3M`选择过去3到6个月的任何内容
* `lowerBound=-1500`和`upperBound=5500`选择在1500毫秒之前和将来5500毫秒之间的任何时间
* `lowerBound=1d`和`upperBound=2d`选择后天的任何内容

它不考虑闰年，所有月份都是30天。

它不支持筛选。

它支持彩块化提取，其方式与[`daterange`](#daterange)谓词相同。

#### 属性 {#properties-17}

* **`upperBound`** — 以毫秒为单位的上限日期或相对于当前服务器时间的`1s 2m 3h 4d 5w 6M 7y`（一秒、两分钟、三小时、四天、五周、六个月、七年），将`-`用于负偏移
* **`lowerBound`** — 以毫秒为单位的下限日期或相对于当前服务器时间的`1s 2m 3h 4d 5w 6M 7y`（一秒、两分钟、三小时、四天、五周、六个月、七年），将`-`用于负偏移

### savedquery {#savedquery}

此谓词包括作为子组谓词添加到当前查询中的持久查询生成器查询的所有谓词。

它不会运行额外的查询，但会扩展当前查询。

可以使用`QueryBuilder#storeQuery()`以编程方式保留查询。 格式可以是多行`String`属性，也可以是以Java™属性格式将查询作为文本文件包含的`nt:file`节点。

它不支持为已保存查询的谓词进行Facet提取。

#### 属性 {#properties-19}

* **`savedquery`** — 已保存查询的路径（`String`属性或`nt:file`节点）

### 相似 {#similar}

此谓词是使用JCR XPath的`rep:similar()`进行相似性搜索。

它不支持筛选，也不支持Facet提取。

#### 属性 {#properties-20}

* **`similar`** — 要查找相似节点的节点的绝对路径
* **`local`** — 下级节点的相对路径，或当前节点的`.`（可选，默认为`.`）

### 标记 {#tag}

此谓词通过指定标记标题路径来搜索使用一个或多个标记标记的内容。

它支持彩块化提取，并使用每个唯一标记的当前标记标题路径为其提供存储段。

#### 属性 {#properties-21}

* **`tag`** — 要查找的标记标题路径，例如`properties:orientation/landscape`
* **`N_value`** — 使用`1_value`、`2_value`、...检查多个标记（默认情况下与`OR`相结合，如果`and=true`则为`AND`）
* **`property`** — 要查看的属性（或属性的相对路径）（默认`cq:tags`）

### tagid {#tagid}

此谓词通过指定标记ID来搜索使用一个或多个标记标记标记的内容。

它支持彩块化提取，并使用每个唯一标记的当前标记ID为其提供存储桶。

#### 属性 {#properties-22}

* **`tagid`** — 要查找的标记ID，例如`properties:orientation/landscape`
* **`N_value`** — 使用`1_value`、`2_value`、...检查多个标记ID（默认情况下与`OR`组合，如果`and=true`则为`AND`）
* **`property`** — 要查看的属性（或属性的相对路径）（默认`cq:tags`）

### tagsearch {#tagsearch}

此谓词通过指定关键字来搜索使用一个或多个标记标记的内容。 首先在标题中搜索包含这些关键字的标记，然后将结果限制为仅包含这些关键字标记的项目。

它不支持彩块化提取。

#### 属性 {#Properties-1}

* **`tagsearch`** — 要在标记标题中搜索的关键字
* **`property`** — 要考虑的属性（或属性的相对路径）（默认`cq:tags`）
* **`lang`** — 仅搜索特定本地化的标记标题（例如，`de`）
* **`all`** — 用于搜索整个标记全文（即所有标题、描述等）的布尔值（优先于`lang`）

### 类型 {#type}

此谓词将结果限制为特定的JCR节点类型，包括主节点类型或`mixin`类型。 它还会查找该节点类型的子类型。 存储库搜索索引必须涵盖节点类型才能有效执行。

它支持方面提取，并为结果中的每种唯一类型提供存储段。

#### 属性 {#Properties-2}

* **`type`** — 要搜索的节点类型或`mixin`名称，例如`cq:Page`
