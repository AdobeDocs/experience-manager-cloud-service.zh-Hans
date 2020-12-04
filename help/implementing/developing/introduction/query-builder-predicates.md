---
title: 查询生成器谓词引用
description: 查询生成器API的谓词引用。
translation-type: tm+mt
source-git-commit: 90b635cb31af910e08bdee7925cec0c7beb05318
workflow-type: tm+mt
source-wordcount: '2221'
ht-degree: 1%

---


# 查询生成器谓词引用{#query-builder-predicate-reference}

## 常规 {#general}

### 根{#root}

这是根谓词组。 它支持组的所有功能并允许设置全局查询参数。

名称“root”在查询中从不使用，它是隐式的。

#### 属性 {#properties-18}

* **`p.offset`** -表示结果页面开始的数字，即要跳过的项目数
* **`p.limit`** -表示页面大小的数字
* **`p.guessTotal`** -推荐：避免计算全部结果总和，代价昂贵；一个数字，表示最大总数最多可计算(例如1000，该数字为用户提供了对粗细大小和精确数字的足够反馈，以获得较 `true` 小的结果)，或仅计算最多必要 `p.offset` +  `p.limit`
* **`p.excerpt`** -如果设置为， `true`则在结果中包含全文摘录
* **`p.hits`** -（仅用于JSON servlet）选择将点击写为JSON的方式，使用这些标准点击（可通过ResultHitWriter服务扩展）:
   * **`simple`** -最小项 `path`目， `title`如 `lastmodified`、、 `excerpt` （如果已设置）
   * **`full`** -节点的sling JSON渲染， `jcr:path` 指示点击路径：默认情况下，仅列表节点的直接属性，包含一个更深的树， `p.nodedepth=N`其中0表示整个无限子树；添 `p.acls=true` 加以包含当前会话对给定结果项的JCR权限(映射： `create` =  `add_node`, `modify`  =  `set_property`,  `delete` =  `remove`
   * **`selective`** -仅在中指定的属 `p.properties`性，即相对路径的空 `+` 格分隔列表（在URL中使用）;如果相对路径具有深度， `>1` 则这些路径将表示为子对象；特殊 `jcr:path` 属性包括点击路径

### 组 {#group}

此谓词允许构建嵌套条件。 组可以包含嵌套组。 查询生成器查询中的所有内容都隐式位于根组中，根组中也可以有`p.or`和`p.not`参数。

以下是将两个属性中的任何一个与值匹配的示例：

```text
group.p.or=true
group.1_property=jcr:title
group.1_property.value=My Page
group.2_property=navTitle
group.2_property.value=My Page
```

从概念上讲，这是`(1_property`或`2_property)`。

以下是嵌套组的示例：

```text
fulltext=Management
group.p.or=true
group.1_group.path=/content/wknd/ch/de
group.1_group.type=cq:Page
group.2_group.path=/content/dam/wknd
group.2_group.type=dam:Asset
```

这将搜索`/content/wknd/ch/de`中的页面或`/content/dam/wknd`中的资产中的术语&#x200B;**管理**。

从概念上讲，这是`fulltext AND ( (path AND type) OR (path AND type) )`。 请注意，出于性能原因，此类OR连接需要良好的索引。

#### 属性 {#properties-6}

* **`p.or`** -如果设置为 `true`，则组中只能有一个谓词匹配。此默认值为`false`，表示所有项必须匹配
* **`p.not`** -如果设置为 `true`，则会否定组(默认为 `false`)
* **`<predicate>`** -添加嵌套谓词
* **`N_<predicate>`** -添加多个同时嵌套的谓词，如  `1_property, 2_property, ...`

### orderby {#orderby}

此谓词允许对结果进行排序。 如果需要按多个属性排序，则需要使用数字前缀多次添加此谓词，如`1_orderby=first`、`2_oderby=second`。

#### 属性 {#properties-13}

* **`orderby`** - JCR属性名称由前导@(例如，或 `@jcr:lastModified` 查询 `@jcr:content/jcr:title`中的其他谓词表示，例如， `2_property`要对其排序
* **`sort`** -排序方向， `desc` 降序或 `asc` 升序（默认）
* **`case`** -如果设置为 `ignore` ，则排序不区分大小写， `a` 含义在前 `B`;如果为空或缺出，则排序区分大小写，即在排序 `B` 之前  `a`

## 谓词{#predicates}

### 布尔属性{#boolproperty}

此谓词与JCR布尔属性匹配。 仅接受值`true`和`false`。 对于`false`，如果属性的值为`false`，或者它根本不存在，则它将匹配。 这对于检查仅在启用时设置的布尔标志非常有用。

继承的`operation`参数没有含义。

此谓词支持facet提取，并为每个`true`或`false`值提供桶，但仅为现有属性提供桶。

#### 属性 {#properties}

* **`boolproperty`** -属性的相对路径，例 `myFeatureEnabled` 如  `jcr:content/myFeatureEnabled`
* **`value`** -值用于检查属性， `true` 或  `false`

### contentfragment {#contentfragment}

此谓词将结果限制为内容片段。

* 它不支持筛选。
* 它不支持facet提取。

#### 属性 {#properties-1}

* **`contentfragment`** -它可与任何值一起使用以检查内容片段。

### `dateComparison` {#datecomparison}

此谓词将两个JCR日期属性相互比较。 可以测试它们是否相等、不等、是否大于或大于等。

这是只筛选谓词，无法利用搜索索引。

#### 属性 {#properties-2}

* **`property1`** -第一个日期属性的路径
* **`property2`** -第二个日期属性的路径
* **`operation`**
   * `=` for exactmatch（默认）
   * `!=` 不等式比较
   * `>` 对于 `property1` 大于  `property2`
   * `>=` 大 `property1` 于或等于  `property2`

### daterange {#daterange}

此谓词将日期／时间间隔与JCR日期属性匹配。 它使用ISO8601
日期和时间的格式(`YYYY-MM-DDTHH:mm:ss.SSSZ`)，还允许部分表示，如`YYYY-MM-DD`。 或者，时间戳可以作为POSIX时间提供。

您可以查找两个时间戳之间的任何内容，即任何比给定日期更新或更旧的内容，也可以在包含时间间隔和打开时间间隔之间进行选择。

它支持facet提取，并提供桶`today`、`this week`、`this month`、`last 3 months`、`this year`、`last year`和`earlier than last year`。

它不支持筛选。

#### 属性 {#properties-3}

* **`property`** -属性的相 `DATE` 对路径，例如  `jcr:lastModified`
* **`lowerBound`** - lower date bound to check property for，例如  `2014-10-01`
* **`lowerOperation`** -( `>` 较新) `>=` 或（at或较新），适用于 `lowerBound`。默认为 `>`
* **`upperBound`** -检查属性的上限，例如  `2014-10-01T12:15:00`
* **`upperOperation`** - `<` （旧）或 `<=` （旧）适用于 `upperBound`。默认为 `<`
* **`timeZone`** -未作为ISO-8601日期字符串给定时区使用的ID。默认值是系统的默认时区。

### excludepaths {#excludepaths}

此谓词从其路径与常规表达式匹配的结果中排除节点。

这是只筛选谓词，无法利用搜索索引。

它不支持facet提取。

#### 属性 {#properties-4}

* **`excludepaths`** -与结果路径匹配的常规表达式，从结果中排除匹配的路径。

### 全文{#fulltext}

此谓词在全文索引中搜索词。

它不支持筛选。

它不支持facet提取。

#### 属性 {#properties-5}

* **`fulltext`** -全文搜索词
* **`relPath`** -要在属性或子节点中进行搜索的相对路径。此属性是可选的。

### hasPermission {#haspermission}

此谓词将结果限制为当前会话具有指定的[JCR权限的项目。](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)

这是只筛选谓词，无法利用搜索索引。 它不支持facet提取。

#### 属性 {#properties-7}

* **`hasPermission`** -以逗号分隔的JCR权限，当前用户会话必须全部拥有该节点；例如 `jcr:write`,  `jcr:modifyAccessControl`

### 语言 {#language}

此谓词查找特定语言的AEM页面。 这会查看页面语言属性和页面路径，它们通常包括顶级站点结构中的语言或区域设置。

这是只筛选谓词，无法利用搜索索引。

它支持facet提取并为每个唯一语言代码提供桶。

#### 属性 {#properties-8}

* **`language`** - ISO语言代码，例如  `de`

### mainasset {#mainasset}

此谓词检查节点是否是DAM主资产而非子资产。 这基本上是子资产节点内不存在的每个节点。 请注意，这不会检查`dam:Asset`节点类型。 要使用此谓词，只需设置`mainasset=true`或`mainasset=false`。 没有其他属性。

这是只筛选谓词，无法利用搜索索引。

它支持facet提取，并为主资产和子资产提供两个时段。

#### 属性 {#properties-9}

* **`mainasset`** -布尔值， `true` 对于主资产， `false` 对于子资产

### memberOf {#memberof}

此谓词查找特定[sling资源集合](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/resource/collection/ResourceCollection.html)的成员项。

这是只筛选谓词，无法利用搜索索引。

它不支持facet提取。

#### 属性 {#properties-10}

* **`memberOf`** - Sling资源收集路径

### nodename {#nodename}

此谓词与JCR节点名称匹配。

它支持facet提取，并为每个唯一节点名称（文件名）提供存储段。

#### 属性 {#properties-11}

* **`nodename`** -允许通配符的节点名称模式： `*` =任何或无字符， `?` =任何字符， `[abc]` =仅用括号表示字符

### notexpired {#notexpired}

此谓词通过检查JCR日期属性是否大于或等于当前服务器时间来匹配项。 这可用于检查`expiresAt`值，并将结果限制为仅限那些尚未过期(`notexpired=true`)或已过期(`notexpired=false`)的结果。

它不支持筛选。

它以与[`daterange`](#daterange)谓词相同的方式支持facet提取。

#### 属性 {#properties-12}

* **`notexpired`** -布尔值， `true` 对于尚未过期（将来日期或等于日期）, `false` 对于过期（过去日期）（必填）
* **`property`** -要检查的属 `DATE` 性的相对路径（必需）

### 路径 {#path}

此谓词在给定路径内搜索。

它不支持facet提取。

#### 属性 {#properties-14}

* **`path`** -这定义路径模式。
   * 根据`exact`属性，整个子树将匹配（如在xpath中附加`//*`，但请注意，这不包括基路径），或仅精确的路径匹配，其中可以包括通配符(`*`)。
      * 默认为 `true`
   * 如果设置了`self`属性，则将搜索包括基节点的整个子树。
* **`exact`** -如果 `exact` 是 `true`，则精确路径必须匹配，但它可以包含简单的通配符(`*`)，该通配符与名称匹配，但不匹配 `/`;如果它是( `false` 默认)，则包括所有后代（可选）
* **`flat`** -仅搜索直接子项(如附加 `/*` 在xpath中)(仅在不 `exact` 为true时使用，可选)
* **`self`** -搜索子树，但包括作为路径给定的基节点（无通配符）

### 属性 {#property}

此谓词与JCR属性及其值匹配。

它支持facet提取，并为结果中的每个唯一属性值提供桶。

#### 属性 {#properties-15}

* **`property`** -属性的相对路径，例如  `jcr:title`
* **`value`** -值检查属性；跟在JCR属性类型到字符串转换之后
* **`N_value`** -使 `1_value`用、 `2_value`、...检查多个值(默认 `OR` 与，如果 `AND` 结合 `and=true`)
* **`and`** -设置为 `true` 用于组合多个值(`N_value`)与  `AND`
* **`operation`**
   * `equals` for exactmatch（默认）
   * `unequals` 不等式比较
   * `like` 用于使 `jcr:like` 用xpath函数（可选）
   * `not` 对于无匹配项(例如， `not(@prop)` 在xpath中，值参数将被忽略)
   * `exists` 存在检查
      * `true` 属性必须存在
      * `false` 与相同， `not` 且是默认
* **`depth`** -属性／相对路径可存在的通配符级别数(例如， `property=size depth=2` 将检 `node/size`查 `node/*/size` 和 `node/*/*/size`)

### rangeproperty {#rangeproperty}

此谓词将JCR属性与间隔匹配。 这适用于线性类型（如`LONG`、`DOUBLE`和`DECIMAL`）的属性。 对于`DATE`，请参阅[`daterange`](#daterange)谓词，该谓词已优化了日期格式输入。

您可以定义下界、上界或两者。 也可以单独地为下界和上界指定操作（例如小于或等于）。

它不支持facet提取。

#### 属性 {#properties-16}

* **`property`** -属性的相对路径
* **`lowerBound`** -下界检查属性
* **`lowerOperation`** -  `>` （默认） `>=`或，应用至  `lowerValue`
* **`upperBound`** -检查属性的上限
* **`upperOperation`** -  `<` （默认） `<=`或，应用至  `lowerValue`
* **`decimal`** -如 `true` 果选中的属性类型为Decimal

### 相对变量{#relativedaterange}

此谓词使用相对于当前服务器时间的时间偏移，将`JCR DATE`属性与日期／时间间隔匹配。 您可以使用毫秒值或Bugzilla语法`1s 2m 3h 4d 5w 6M 7y`指定`lowerBound`和`upperBound`（1秒、2分钟、3小时、4天、5周、6个月、7年）。 前缀为`-`，表示当前时间之前的负偏移。 如果仅指定`lowerBound`或`upperBound`，则另一个将默认为`0`，表示当前时间。

例如：

* `upperBound=1h` （且无） `lowerBound`在下一小时内选择任何内容
* `lowerBound=-1d` (并且不 `upperBound`会)在过去24小时内选择任何内容
* `lowerBound=-6M` 在过 `upperBound=-3M` 去3到6个月里选择任何
* `lowerBound=-1500` 并选 `upperBound=5500` 择1500毫秒到5500毫秒之间的任何内容
* `lowerBound=1d` 后 `upperBound=2d` 天选择任何东西

请注意，它不需要花上几年时间考虑，所有月份都是30天。

它不支持筛选。

它以与[`daterange`](#daterange)谓词相同的方式支持facet提取。

#### 属性 {#properties-17}

* **`upperBound`** -相对于当前服务器时间的上限日期(以毫 `1s 2m 3h 4d 5w 6M 7y` 秒为单位，即1秒、2分钟、3小时、4天、5周、6个月、7年)，使用负偏 `-` 移值
* **`lowerBound`** -相对于当前服务器时 `1s 2m 3h 4d 5w 6M 7y` 间，日期下限（以毫秒为单位，一秒、二分钟、三小时、四天、五周、六个月、七年），使用负 `-` 偏移

### savedquery {#savedquery}

此谓词包括作为子组谓词存储到当前查询中的持久查询生成器查询的所有谓词。

请注意，这不会执行额外查询，而会扩展当前查询。

查询可以使用`QueryBuilder#storeQuery()`以编程方式持久化。 格式可以是多行`String`属性，也可以是`nt:file`节点，该节点将查询作为Java属性格式的文本文件。

它不支持已保存提取的谓词的facet查询。

#### 属性 {#properties-19}

* **`savedquery`** -保存查询的路径(`String` 属性或 `nt:file` 节点)

### 类似{#similar}

此谓词是使用JCR XPath的`rep:similar()`进行的相似性搜索。

它不支持筛选，也不支持facet提取。

#### 属性 {#properties-20}

* **`similar`** -要查找相似节点的节点的绝对路径
* **`local`** -子节点或当前节点的相 `.` 对路径(可选，默认为 `.`)

### 标签{#tag}

此谓词通过指定标记标题路径搜索用一个或多个标记标记的内容。

它支持facet提取，并使用每个唯一标签的当前标签标题路径为其提供桶。

#### 属性 {#properties-21}

* **`tag`** -要查找的标记标题路径，例如  `properties:orientation/landscape`
* **`N_value`** -使 `1_value`用、 `2_value`、...检查多个标记(默认 `OR` 与if组 `AND` 合 `and=true`)
* **`property`** -要查看的属性（或属性的相对路径）(默认 `cq:tags`)

### tagid {#tagid}

此谓词通过指定标记ID搜索用一个或多个标记标记的内容。

它支持facet提取，并使用每个唯一标记的当前标记ID为其提供桶。

#### 属性 {#properties-22}

* **`tagid`** -要查找的标记ID，例如  `properties:orientation/landscape`
* **`N_value`** -使 `1_value`用、 `2_value`、...检查多个标记ID(默认情况下， `OR` 与if结合使 `AND` 用 `and=true`)
* **`property`** -要查看的属性（或属性的相对路径）(默认 `cq:tags`)

### tagsearch {#tagsearch}

此谓词通过指定关键字搜索用一个或多个标记标记的内容。 这将首先搜索标题中包含这些关键字的标记，然后将结果限制为仅包含这些关键字的标记。

它不支持facet提取。

#### 属性 {#Properties-1}

* **`tagsearch`** -用于在标记标题中搜索的关键字
* **`property`** -要考虑的属性（或属性的相对路径）(默认 `cq:tags`)
* **`lang`** -仅搜索特定的本地化标记标题(例如， `de`)
* **`all`** -用于搜索整个标记全文的布尔值，即所有标题、说明等。（优先于`lang`）

### 类型 {#type}

此谓词将结果限制为特定的JCR节点类型，包括主节点类型或混合类型。 此外，还会查找该节点类型的子类型。 请注意，存储库搜索索引需要涵盖节点类型，以便有效执行。

它支持facet提取，并为结果中的每个唯一类型提供桶。

#### 属性 {#Properties-2}

* **`type`** -节点类型或混合名称，例如  `cq:Page`
