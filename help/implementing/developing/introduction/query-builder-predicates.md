---
title: 查询生成器谓词参考
description: 查询生成器API的谓词引用。
exl-id: 77118ef7-4d29-470d-9c4b-20537a408940
source-git-commit: c08e442e58a4ff36e89a213aa7b297b538ae3bab
workflow-type: tm+mt
source-wordcount: '2218'
ht-degree: 2%

---

# 查询生成器谓词参考 {#query-builder-predicate-reference}

## 常规 {#general}

### 根 {#root}

这是根谓词组。 它支持组的所有功能，并允许设置全局查询参数。

查询中从未使用名称“root”，它是隐式的。

#### 属性 {#properties-18}

* **`p.offset`**  — 表示结果页面开始的数字，即要跳过的项目数
* **`p.limit`**  — 表示页面大小的数字
* **`p.guessTotal`**  — 建议：避免计算可能代价高昂的全部结果总数；表示最多总计的数字（例如1000，该数字可为用户提供对粗细大小和精确数字的足够反馈，以获得较小的结果）或 `true` 只计算最少所需的 `p.offset` + `p.limit`
* **`p.excerpt`**  — 如果设置为 `true`，在结果中包含全文摘录
* **`p.hits`**  — （仅适用于JSON Servlet）选择点击以JSON形式写入的方式，并使用这些标准点击（可通过ResultHitWriter服务扩展）：
   * **`simple`**  — 最小项目，例如 `path`, `title`, `lastmodified`, `excerpt` （如果已设置）
   * **`full`**  — 节点的sling JSON渲染，以及 `jcr:path` 指示点击的路径：默认情况下，仅列出节点的直接属性，包括包含更深层的树，其中包含 `p.nodedepth=N`，其中0表示整个无限子树；添加 `p.acls=true` 在给定结果项上包含当前会话的JCR权限(映射： `create` = `add_node`, `modify` = `set_property`, `delete` = `remove`)
   * **`selective`**  — 仅在 `p.properties`，表示分隔(使用 `+` （在URL中）相对路径列表；如果相对路径具有深度 `>1` 这些对象将表示为子对象；特殊 `jcr:path` 属性包含点击的路径

### 组 {#group}

此谓词允许生成嵌套条件。 组可以包含嵌套组。 查询生成器查询中的所有内容都隐式位于根组中，根组可以具有 `p.or` 和 `p.not` 参数。

以下示例用于将两个属性中的任一属性与值进行匹配：

```text
group.p.or=true
group.1_property=jcr:title
group.1_property.value=My Page
group.2_property=navTitle
group.2_property.value=My Page
```

从概念上讲 `(1_property` 或 `2_property)`.

以下是嵌套群组的示例：

```text
fulltext=Management
group.p.or=true
group.1_group.path=/content/wknd/ch/de
group.1_group.type=cq:Page
group.2_group.path=/content/dam/wknd
group.2_group.type=dam:Asset
```

这会搜索术语 **管理** 在页面内 `/content/wknd/ch/de` 或 `/content/dam/wknd`.

从概念上讲 `fulltext AND ( (path AND type) OR (path AND type) )`. 请注意，出于性能原因，此类OR连接需要良好的索引。

#### 属性 {#properties-6}

* **`p.or`**  — 如果设置为 `true`，组中只能有一个谓词匹配。 默认为 `false`表示必须匹配
* **`p.not`**  — 如果设置为 `true`，则会否定群组(默认为 `false`)
* **`<predicate>`**  — 添加嵌套谓词
* **`N_<predicate>`**  — 添加多个同时的嵌套谓词，如 `1_property, 2_property, ...`

### orderby {#orderby}

此谓词允许对结果进行排序。 如果需要按多个属性进行排序，则需要使用数字前缀多次添加此谓词，例如 `1_orderby=first`, `2_oderby=second`.

#### 属性 {#properties-13}

* **`orderby`**  — 例如，由前导@指示的JCR属性名称 `@jcr:lastModified` 或 `@jcr:content/jcr:title`，或查询中的其他谓词，例如 `2_property`，排序对象
* **`sort`**  — 排序方向 `desc` 为降序或 `asc` 升序（默认）
* **`case`**  — 如果设置为 `ignore` 将不区分大小写，这表示 `a` 先于 `B`;如果为空或遗漏，则排序区分大小写，这表示 `B` 先于 `a`

## 谓语 {#predicates}

### 布尔属性 {#boolproperty}

此谓词与JCR布尔属性匹配。 仅接受值 `true` 和 `false`. 如果 `false`，则当属性具有值时，该参数将匹配 `false` 或者，如果它根本不存在。 这可用于检查仅在启用时设置的布尔标记。

继承 `operation` 参数没有意义。

此谓词支持Facet提取，并为每个Facet提供存储段 `true` 或 `false` 值，但仅适用于现有属性。

#### 属性 {#properties}

* **`boolproperty`**  — 属性的相对路径，例如 `myFeatureEnabled` 或 `jcr:content/myFeatureEnabled`
* **`value`**  — 值检查属性， `true` 或 `false`

### contentfragment {#contentfragment}

此谓词将结果限制为内容片段。

* 它不支持过滤。
* 它不支持面提取。

#### 属性 {#properties-1}

* **`contentfragment`**  — 可将其与任何值一起使用，以检查内容片段。

### `dateComparison` {#datecomparison}

此谓词将比较两个JCR日期属性。 可以测试它们是否相等、不等、是否大于或等于。

这是仅限过滤的谓词，无法利用搜索索引。

#### 属性 {#properties-2}

* **`property1`**  — 首次日期属性的路径
* **`property2`**  — 第二个日期属性的路径
* **`operation`**
   * `=` （默认）
   * `!=` 不等式比较
   * `>` 表示 `property1` 大于 `property2`
   * `>=` 表示 `property1` 大于或等于 `property2`

### 达特朗日 {#daterange}

此谓词将JCR日期属性与日期/时间间隔相匹配。 日期和时间采用ISO8601格式(`YYYY-MM-DDTHH:mm:ss.SSSZ`)，并允许部分表示，例如 `YYYY-MM-DD`. 或者，可以将时间戳作为POSIX时间提供。

您可以查找两个时间戳之间的任何内容，即比给定日期晚或早的任何内容，也可以在包含时间戳和打开时间戳之间进行选择。

它支持Facet提取并提供存储段 `today`, `this week`, `this month`, `last 3 months`, `this year`, `last year`和 `earlier than last year`.

它不支持过滤。

#### 属性 {#properties-3}

* **`property`**  — 相对路径 `DATE` 属性，例如 `jcr:lastModified`
* **`lowerBound`**  — 例如，下限日期将检查属性 `2014-10-01`
* **`lowerOperation`** - `>` （较新）或 `>=` （at或更高版本）适用于 `lowerBound`. 默认为 `>`
* **`upperBound`**  — 例如，检查属性的上限 `2014-10-01T12:15:00`
* **`upperOperation`** - `<` （旧）或 `<=` （在或更早版本） `upperBound`. 默认为 `<`
* **`timeZone`**  — 未作为ISO-8601日期字符串指定时使用的时区ID。 默认时区是系统的默认时区。

### 排除路径 {#excludepaths}

此谓词从结果中排除节点的路径与正则表达式匹配的节点。

这是仅限过滤的谓词，无法利用搜索索引。

它不支持面提取。

#### 属性 {#properties-4}

* **`excludepaths`**  — 与结果路径匹配的正则表达式，从结果中排除匹配的路径。

### 全文 {#fulltext}

此谓词在全文索引中搜索术语。

它不支持过滤。

它不支持面提取。

#### 属性 {#properties-5}

* **`fulltext`**  — 全文搜索词
* **`relPath`**  — 属性或子节点中要搜索的相对路径。 此属性是可选的。

### hasPermission {#haspermission}

此谓词将结果限制为当前会话具有指定的项目 [JCR权限。](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)

这是仅限过滤的谓词，无法利用搜索索引。 它不支持面提取。

#### 属性 {#properties-7}

* **`hasPermission`**  — 以逗号分隔的JCR权限，当前用户会话必须对相关节点具有ALL权限；例如 `jcr:write`, `jcr:modifyAccessControl`

### 语言 {#language}

此谓词以特定语言查找AEM页面。 这会同时查看页面语言属性和页面路径，页面路径通常包括顶级站点结构中的语言或区域设置。

这是仅限过滤的谓词，无法利用搜索索引。

它支持Facet提取，并为每个唯一语言代码提供存储段。

#### 属性 {#properties-8}

* **`language`**  — 例如ISO语言代码 `de`

### 主资产 {#mainasset}

此谓词检查节点是否是DAM主资产而不是子资产。 这基本上是子资产节点内部的每个节点。 请注意，这不会检查 `dam:Asset` 节点类型。 要使用此谓词，只需设置 `mainasset=true` 或 `mainasset=false`. 没有其他属性。

这是仅限过滤的谓词，无法利用搜索索引。

它支持Facet提取，并为主资产和子资产提供两个存储段。

#### 属性 {#properties-9}

* **`mainasset`**  — 布尔值， `true` 对于主资产， `false` 对于子资产

### memberOf {#memberof}

此谓词会查找属于特定 [sling资源收集](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/resource/collection/ResourceCollection.html).

这是仅限过滤的谓词，无法利用搜索索引。

它不支持面提取。

#### 属性 {#properties-10}

* **`memberOf`** - Sling资源收集的路径

### nodename {#nodename}

此谓词与JCR节点名称匹配。

它支持Facet提取，并为每个唯一节点名称（文件名）提供存储段。

#### 属性 {#properties-11}

* **`nodename`**  — 允许使用通配符的节点名称模式： `*` =任何字符或无字符， `?` =任意字符， `[abc]` =仅在括号中显示字符

### notexpired {#notexpired}

此谓词通过检查JCR日期属性是否大于或等于当前服务器时间来匹配项。 这可用于检查 `expiresAt` 值并将结果限制为仅限那些尚未过期(`notexpired=true`)或已过期(`notexpired=false`)。

它不支持过滤。

它支持与 [`daterange`](#daterange) 谓词。

#### 属性 {#properties-12}

* **`notexpired`**  — 布尔值， `true` （日期为未来或等于）， `false` （过去的日期）（必需）
* **`property`**  — 相对路径 `DATE` 要检查的属性（必需）

### 路径 {#path}

此谓词将搜索给定路径中的。

它不支持面提取。

#### 属性 {#properties-14}

* **`path`**  — 这定义路径模式。
   * 根据 `exact` 属性，则整个子树都将匹配(例如，附加 `//*` 在xpath中，但请注意，这不包括基本路径)，或者只有精确的路径匹配项，该匹配项可以包含通配符(`*`)。
      * 默认为 `true`
   * 如果 `self`属性设置后，将搜索包含基础节点的整个子树。
* **`exact`**  — 如果 `exact` is `true`，则路径必须完全匹配，但可以包含简单的通配符(`*`)，匹配名称，但不匹配 `/`;如果为 `false` （默认）包含所有子体（可选）
* **`flat`**  — 仅搜索直接子项(例如附加 `/*` (仅在 `exact` 不为true，可选)
* **`self`**  — 搜索子树，但包含作为路径给定的基节点（无通配符）

### 属性 {#property}

此谓词与JCR属性及其值匹配。

它支持Facet提取，并为结果中的每个唯一属性值提供存储段。

#### 属性 {#properties-15}

* **`property`**  — 属性的相对路径，例如 `jcr:title`
* **`value`**  — 值，用于检查属性；将JCR属性类型跟踪到字符串转化
* **`N_value`**  — 使用 `1_value`, `2_value`,...检查多个值(与 `OR` 默认情况下，使用 `AND` if `and=true`)
* **`and`**  — 设置为 `true` 用于组合多个值(`N_value`)与 `AND`
* **`operation`**
   * `equals` （默认）
   * `unequals` 不等式比较
   * `like` 用于 `jcr:like` xpath函数（可选）
   * `not` (例如， `not(@prop)` 在xpath中，值参数将被忽略)
   * `exists` 是否存在检查
      * `true` 属性必须存在
      * `false` 与相同 `not` 和为默认值
* **`depth`**  — 属性/相对路径可存在的通配符级别数(例如， `property=size depth=2` 将检查 `node/size`, `node/*/size` 和 `node/*/*/size`)

### rangproperty {#rangeproperty}

此谓词将JCR属性与间隔匹配。 这适用于具有线性类型(如 `LONG`, `DOUBLE` 和 `DECIMAL`. 对于 `DATE` 请参见 [`daterange`](#daterange) 谓词，已优化日期格式输入。

您可以定义下限、上限或两者。 也可以单独为下界和上界指定操作（例如小于或等于）。

它不支持面提取。

#### 属性 {#properties-16}

* **`property`**  — 属性的相对路径
* **`lowerBound`**  — 下限检查属性
* **`lowerOperation`** - `>` （默认）或 `>=`，适用于 `lowerValue`
* **`upperBound`**  — 上界检查属性
* **`upperOperation`** - `<` （默认）或 `<=`，适用于 `lowerValue`
* **`decimal`** - `true` 如果选中的属性类型为“小数”

### 相对变量 {#relativedaterange}

此谓词匹配 `JCR DATE` 使用相对于当前服务器时间的时间偏移对日期/时间间隔进行属性。 您可以指定 `lowerBound` 和 `upperBound` 使用毫秒值或Bugzilla语法 `1s 2m 3h 4d 5w 6M 7y` （一秒、二分钟、三小时、四天、五个星期、六个月、七年）。 前缀为 `-` 表示当前时间之前的负偏移。 如果仅指定 `lowerBound` 或 `upperBound`，另一个默认设置为 `0`，表示当前时间。

例如：

* `upperBound=1h` （否） `lowerBound`)会在下一小时内选择任何内容
* `lowerBound=-1d` （否） `upperBound`)会选择过去24小时内的任何内容
* `lowerBound=-6M` 和 `upperBound=-3M` 在过去3到6个月里选择了任何东西
* `lowerBound=-1500` 和 `upperBound=5500` 选择1500毫秒到5500毫秒之间的任何内容
* `lowerBound=1d` 和 `upperBound=2d` 选择后天的任何内容

请注意，考虑时间不需要多年，所有月份都为30天。

它不支持过滤。

它支持与 [`daterange`](#daterange) 谓词。

#### 属性 {#properties-17}

* **`upperBound`**  — 以毫秒或以毫秒为单位的上限日期 `1s 2m 3h 4d 5w 6M 7y` （一秒、二分钟、三小时、四天、五周、六个月、七年） `-` 为负偏移
* **`lowerBound`**  — 以毫秒或以毫秒为单位的下限日期 `1s 2m 3h 4d 5w 6M 7y` （一秒、二分钟、三小时、四天、五周、六个月、七年） `-` 为负偏移

### savedquery {#savedquery}

此谓词将持久查询生成器查询的所有谓词作为子组谓词包含在当前查询中。

请注意，这不会执行额外的查询，而是扩展当前查询。

查询可以使用以编程方式持久保留 `QueryBuilder#storeQuery()`. 格式可以是多行 `String` 属性或 `nt:file` 节点，该节点将查询作为Java属性格式的文本文件。

它不支持对保存查询的谓词进行分面提取。

#### 属性 {#properties-19}

* **`savedquery`**  — 保存查询的路径(`String` 属性或 `nt:file` node)

### 相似 {#similar}

此谓词是使用JCR XPath的 `rep:similar()`.

它不支持过滤，也不支持分面提取。

#### 属性 {#properties-20}

* **`similar`**  — 要查找相似节点的节点的绝对路径
* **`local`**  — 子节点或子节点的相对路径 `.` 对于当前节点(可选，默认值为 `.`)

### 标记 {#tag}

此谓词通过指定标记标题路径来搜索带有一个或多个标记的内容。

它支持Facet提取，并使用每个唯一标记的当前标记标题路径为每个唯一标记提供存储段。

#### 属性 {#properties-21}

* **`tag`**  — 例如，要查找的标记标题路径 `properties:orientation/landscape`
* **`N_value`**  — 使用 `1_value`, `2_value`,...检查多个标记(与 `OR` 默认情况下，使用 `AND` if `and=true`)
* **`property`**  — 要查看的属性（或属性的相对路径）（默认） `cq:tags`)

### tagid {#tagid}

此谓词通过指定标记ID来搜索带有一个或多个标记的内容。

它支持Facet提取，并使用每个唯一标记的当前标记ID为其提供存储段。

#### 属性 {#properties-22}

* **`tagid`**  — 例如要查找的标记ID `properties:orientation/landscape`
* **`N_value`**  — 使用 `1_value`, `2_value`, ...检查多个标记ID(与 `OR` 默认情况下，使用 `AND` if `and=true`)
* **`property`**  — 要查看的属性（或属性的相对路径）（默认） `cq:tags`)

### tagsearch {#tagsearch}

此谓词通过指定关键字，搜索带有一个或多个标记的内容。 这将首先在其标题中搜索包含这些关键词的标记，然后将结果限制为仅使用这些关键词标记的项目。

它不支持面提取。

#### 属性 {#Properties-1}

* **`tagsearch`**  — 在标记标题中搜索的关键字
* **`property`**  — 要考虑的属性（或属性的相对路径）（默认） `cq:tags`)
* **`lang`**  — 仅在特定本地化的标记标题中搜索(例如， `de`)
* **`all`**  — 用于搜索整个标记全文（即所有标题、描述等）的布尔值。 (优先于 `lang`)

### 类型 {#type}

此谓词将结果限制为特定的JCR节点类型（主节点类型或混合类型）。 此外，还会查找该节点类型的子类型。 请注意，为了高效执行，存储库搜索索引需要涵盖节点类型。

它支持Facet提取，并为结果中的每种唯一类型提供存储段。

#### 属性 {#Properties-2}

* **`type`**  — 要搜索的节点类型或混合名称，例如 `cq:Page`
