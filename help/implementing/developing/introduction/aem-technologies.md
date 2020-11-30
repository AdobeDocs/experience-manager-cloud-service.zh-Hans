---
title: AEM技术基础
description: 概述AEM的技术基础，包括AEM的结构和基本技术（如JCR、Sling和OSGi）。
translation-type: tm+mt
source-git-commit: 750fded1564de2b11f6c104cc70befc4453405b4
workflow-type: tm+mt
source-wordcount: '2187'
ht-degree: 0%

---


# AEM技术基础 {#aem-technical-foundations}

AEM是一个构建在久经考验、可扩展和灵活技术之上的强大平台。 本文档详细概述了组成AEM的各个部件，旨在作为完整堆栈AEM开发人员的技术附录。 它不是作为入门指南。 如果您是AEM开发的新手，请首先参 [阅开发AEM Sites- WKND教程](develop-wknd-tutorial.md) 。

>[!TIP]
>
>在深入探讨AEM的核心技术之前，Adobe建议完成《开 [发AEM Sites- WKND入门教程》。](develop-wknd-tutorial.md)

## 基本面 {#fundamentals}

作为一个现代内容管理系统，AEM依赖标准Web技术：

* 请求——响应(XMLHttpRequest / XMLHttpResponse)循环
* HTML
* CSS
* JavaScript

基础内容存储库和业务逻辑层围绕Java技术构建：

* JCR
* Sling
* OSGi

## Java内容存储库 {#java-content-repository}

Java内容存储库(JCR)标准 [JSR 283](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/index.html)，指定一种独立于供应商和独立于实施的方式，用于在内容存储库的粒度级别上双向访问内容。 Adobe研究公司（瑞士）AG持有规格线索。

JCR [API 2.0](https://docs.adobe.com/docs/en/spec/javax.jcr/javadocs/jcr-2.0/index.html) 包 `javax.jcr.*` ，用于直接访问和处理存储库内容。

AEM建立在JCR之上。

## 阿帕奇·杰克拉布特·奥克 {#jackrabbit-oak}

[Apache Jackrabbit](https://jackrabbit.apache.org/oak/) Oak是可伸缩的、高性能的分层内容存储库的实施，它作为现代世界级网站和其他要求苛刻的内容应用程序的基础，符合JCR标准。

Jackrabbit Oak（也称为Oak）是JCR标准的实施，AEM是基于该标准构建的。

## Sling请求处理 {#sling-request-processing}

AEM是使用Sling [构建的](https://sling.apache.org/site/index.html),Sling是一个基于REST原则的Web 应用程序框架，可轻松开发面向内容的应用程序。 Sling使用JCR存储库（如Apache Jackrabbit Oak）作为其数据存储。 Sling已经为Apache Software Foundation贡献了力量——有关更多信息，请访问Apache。

### Sling简介 {#introduction-to-sling}

使用Sling，要呈现的内容类型不是第一个处理考虑事项。 而主要考虑的是URL是否解析为内容对象，然后可以找到脚本来执行渲染。 这为Web内容作者提供了极好的支持，使他们能够轻松地根据自己的要求定制页面。

这种灵活性的优势在具有各种不同内容元素的应用程序中显而易见，或者在您需要可轻松自定义的页面时也显而易见。 特别是，在实施Web内容管理系统(如AEM)时。

参 [阅15分钟后发现Sling](https://sling.apache.org/documentation/getting-started/discover-sling-in-15-minutes.html) ，了解使用Sling进行开发的最初步骤。

下图说明了Sling脚本分辨率：它说明了如何从HTTP请求到内容节点、从内容节点到资源类型、从资源类型到脚本以及可以使用哪些脚本变量。

![了解Apache Sling脚本分辨率](assets/sling-cheatsheet-01.png)

下图说明了处理所有POST请求的默认处理函数时可以使用的所有隐藏但功能强大的请求参数，该处理函数为您提供了在存储库中创建、修改、删除、复制和移动节点的无穷选项。 `SlingPostServlet`

![使用SlingPostServlet](assets/sling-cheatsheet-02.png)

### Sling以内容为中心 {#sling-is-content-centric}

Sling以内 *容为中心*。 这意味着，当每个(HTTP)请求以JCR资源（存储库节点）的形式映射到内容时，处理将集中在内容上：

* 第一个目标是保存内容的资源（JCR节点）
* 其次，表示或脚本与请求的某些部分（例如选择器和／或扩展）一起从资源属性中定位

### REST风格的Sling {#restful-sling}

由于其以内容为中心的理念，Sling实现了面向REST的服务器，因此在Web应用程序框架中具有新的概念。 优点是：

* 非常REST风格，而不仅仅是表面；资源和表示形式在服务器内部正确建模
* 删除一个或多个数据模型
   * 其他内容管理框架可能需要URL结构、业务对象、数据库模式才能访问资源。
   * 使用Sling，可以简化为：URL =资源= JCR结构

### URL分解 {#url-decomposition}

在Sling中，处理由用户请求的URL驱动。 这定义了要由相应脚本显示的内容。 为此，会从URL中提取信息。

如果我们分析以下URL:

```text
https://myhost/tools/spy.printable.a4.html/a/b?x=12
```

我们可以把它分解成复合部分：

| 协议 | 主机 |  | 内容路径 | 选择器 | 扩展 |  | 后缀 |  | 参数 |
|---|---|---|---|---|---|---|---|---|---|
| `https://` | `myhost` | `/` | `tools/spy` | `.printable.a4.` | `html` | `/` | `a/b` | `?` | `x=12` |

* **协议** - HTTPS
* **主机** -站点的域
* **内容路径** -指定要呈现的内容并与扩展结合使用的路径；在本例中，它们转换为 `tools/spy.html`
* **选择器** -用于呈现内容的替代方法；在本示例中，打印机友好版本采用A4格式
* **扩展** -内容格式；还指定要用于渲染的脚本
* **后缀** -可用于指定其他信息
* **参数** -动态内容所需的任何参数

#### 从URL到内容和脚本 {#from-url-to-content-and-scripts}

使用URL分解的原则：

* 映射使用从请求中提取的内容路径来定位资源。
* 找到相应的资源后，将提取sling资源类型，并用于查找要用于渲染内容的脚本。

下图说明了所使用的机制，将在下几节中更详细地讨论该机制。

![URL映射机制](assets/url-mapping.png)

使用Sling，您可以指定哪个脚本渲染特定实体(通过在JCR `sling:resourceType` 节点中设置属性)。 此机制比脚本访问数据实体（PHP脚本中的SQL语句可以）的优惠更自由，因为资源可以具有多个再现。

#### 将请求映射到资源 {#mapping-requests-to-resources}

请求被分解并提取必要的信息。 系统会搜索存储库以查找所请求的资源（内容节点）:

* First Sling检查节点是否存在于请求中指定的位置；例如， `../content/corporate/jobs/developer.html`
* 如果找不到节点，则扩展被丢弃，搜索会重复；例如， `../content/corporate/jobs/developer`
* 如果找不到节点，则Sling将返回http代码404（找不到）。

Sling还允许JCR节点以外的其他资源，但这是一个高级功能。

### 查找脚本 {#locating-the-script}

找到相应的资源（内容节点）后，将提 **取sling资源类** 型。 这是一个路径，用于定位要用于呈现内容的脚本。

由指定的路 `sling:resourceType` 径可以是：

* 绝对
* 相对于配置参数

>[!TIP]
>
>相对路径是Adobe推荐的，因为它们提高了可移植性。

所有Sling脚本都存储在(可变、用户 `/apps` 脚本)或(不可变、系 `/libs` 统脚本)的子文件夹中，按此顺序进行搜索。

需要注意的其他几点是：

* 当需要该方法(GET、POST)时，将按照HTTP规范(如 `jobs.POST.esp`
* 支持各种脚本引擎，但常见的推荐脚本是HTL和JavaScript。

AEM的给定实例支持的脚本引擎列表列在Felix管理控制台() `http://<host>:<port>/system/console/slingscripting`上。

使用上一个示例，如果 `sling:resourceType` 是 `hr/jobs` 以下示例：

* GET/HEAD请求和以(默 `.html` 认请求类型，默认格式)结尾的URL
   * 剧本是 `/apps/hr/jobs/jobs.esp`;最后一部分 `sling:resourceType` 构成文件名。
* POST请求(除GET/HEAD外的所有请求类型，方法名称必须为大写)
   * POST将用在脚本名称中。
   * 脚本是 `/apps/hr/jobs/jobs.POST.esp`。
* 其他格式的URL，不以 `.html`
   * For example `../content/corporate/jobs/developer.pdf`
   * 剧本是 `/apps/hr/jobs/jobs.pdf.esp`;后缀将添加到脚本名称。
* 包含选择器的URL
   * 选择器可用于以替代格式显示相同的内容。 例如打印机友好版本、rss源或摘要。
   * 如果我们查看打印机友好版本，选择器可能位于该版本 `print`;as in `../content/corporate/jobs/developer.print.html`
   * 剧本是 `/apps/hr/jobs/jobs.print.esp`;选择器将添加到脚本名称。
* 如果尚 `sling:resourceType` 未定义，则：
   * 内容路径将用于搜索相应的脚本(如果基于路径 `ResourceTypeProvider` 的活动)。
   * 例如，脚本将 `../content/corporate/jobs/developer.html` 在中生成搜索 `/apps/content/corporate/jobs/`。
   * 将使用主节点类型。
* 如果根本找不到脚本，则将使用默认脚本。
   * 默认再现当前支持为纯文`.txt`本()、HTML`.html`()和JSON(`.json`)，所有这些都将列表节点的属性（格式适当）。 扩展的默认再现( `.res`或没有请求扩展的请求)是假设资源（如果可能）。
* 对于http错误处理（代码403或404）,Sling将在以下位置中查找脚本：
   * 自定义脚 `/apps/sling/servlet/errorhandler` 本的位置
   * 或标准脚本的位置 `/libs/sling/servlet/errorhandler/404.jsp`

如果多个脚本应用于给定请求，则选择具有最佳匹配项的脚本。 比赛越具体，越好；换言之，无论请求扩展名或方法名称是否匹配，选择器越多匹配越好。

例如，考虑访问资源的请求

* `/content/corporate/jobs/developer.print.a4.html`

类型

* `sling:resourceType="hr/jobs"`

假设我们在正确的位置具有以下脚本列表:

1. `GET.esp`
1. `jobs.esp`
1. `html.esp`
1. `print.esp`
1. `print.html.esp`
1. `print/a4.esp`
1. `print/a4/html.esp`
1. `print/a4.html.esp`

优先顺序为(8)-(7)-(6)-(5)-(4)-(3)-(2)-(1)。

除了资源类型（主要由属性定义） `sling:resourceType` 之外，还有资源超类型。 这通常由属性指 `sling:resourceSuperType` 示。 在尝试查找脚本时，也会考虑这些超类型。 资源超级类型的优势在于，它们可以构成资源的层次结构，其中默认资源类型(由默 `sling/servlet/default` 认Servlet使用)实际上是根。

资源的资源超类型可以通过两种方式进行定义：

* 按资 `sling:resourceSuperType` 源的属性。
* 按 `sling:resourceSuperType` 点所在的节点的属 `sling:resourceType` 性。

例如：

* `/`
   * `a`
   * `b`
      * `sling:resourceSuperType = a`
   * `c`
      * `sling:resourceSuperType = b`
   * `x`
      * `sling:resourceType = c`
   * `y`
      * `sling:resourceType = c`
      * `sling:resourceSuperType = a`

类型层次结构：

* `/x`
   * Is `[ c, b, a, <default>]`
* 为 `/y`
   * 层次结构为 `[ c, a, <default>]`

这是因为 `/y` 有属性， `sling:resourceSuperType` 而没有， `/x` 因此它的超类型是从其资源类型中获取的。

#### 无法直接调用Sling脚本 {#sling-scripts-cannot-be-called-directly}

在Sling中，无法直接调用脚本，因为这会破坏REST服务器的严格概念；您可以混合资源和演示。

如果您直接调用表示法（脚本），则将资源隐藏在脚本中，因此框架(Sling)不再了解它。 因此，您会丢失某些功能：

* 自动处理GET以外的http方法，包括：
   * POST、PUT、DELETE，使用sling默认实现处理
   * 您的 `POST.jsp` 位置中的脚 `sling:resourceType` 本
* 您的代码体系结构不再像原来那样清晰、结构清晰；对于大规模开发至关重要

### Sling API {#sling-api}

它使用Sling API包 `org.apache.sling.*`和标签库。

### 使用sling:include引用现有元素 {#referencing-existing-elements-using-sling-include}

最后需要参考脚本中的现有元素。

更复杂的脚本（聚合脚本）可能需要访问多个资源(例如导航、提要栏、页脚、列表元素)，并通过包括该资源来 *访问*。

要执行此操作，可使用命 `sling:include("/<path>/<resource>")` 令。 这将有效地包括引用资源的定义。

## OSGi {#osgi}

OSGi(Open Services Gateway Initiative)定义了用于开发和部署模块化应用程序和库的架构（也称为Dynamic Module System for Java）。 OSGi容器允许您将应用程序分为多个单个模块（它们是带有附加元信息的jar文件，在OSGi术语中称为绑定），并通过以下方式管理它们之间的交叉依赖关系：

* 在该容器内实施的服务
* 容器与应用程序之间的合同

这些服务和合同提供了一种使单个元素能够动态发现彼此以进行协作的架构。

然后，OSGi框架将您动态加载／卸载、配置和控制这些包，无需重新启动。

>[!NOTE]
>
>有关OSGi技术的完整信息可在OSGi网 [站上找到](https://www.osgi.org)。
>
>特别是，他们的“基础教育”页面包含一系列演示和教程。

此体系结构允许您使用特定于应用程序的模块扩展Sling。 Sling，因此AEM使用 [Apache Felix](https://felix.apache.org/) 实现OSGi。 它们都是在OSGi框架中运行的OSGi捆绑包的集合。

这样，您就可以对安装中的任何包执行以下操作：

* 安装
* 开始
* 停止
* 更新
* 卸载
* 查看当前状态
* 访问有关特定捆绑包的更多详细信息（例如符号名称、版本、位置等）

有关 [详细信息，请参阅将AEM的OSGi配置](/help/implementing/deploying/configuring-osgi.md) 为Cloud Service。

## 存储库中的结构 {#structure-within-the-repository}

以下列表概述了在存储库中将看到的结构。

* `/apps` -与应用相关；包括特定于您的网站的组件定义。 您开发的组件可以基于上提供的现成组件 `/libs/core/wcm/components`。
* `/content` -为网站创建的内容。
* `/etc`
* `/home` -用户和组信息。
* `/libs` -属于AEM核心的库和定义。 中的子文 `/libs` 件夹代表现成的AEM功能。 中的内 `/libs` 容不能修改。 网站的特定功能应在下制作 `/apps`。
* `/tmp` -临时工作区。
* `/var` -系统更改和更新的文件；如审计日志、统计、事件处理。

>[!CAUTION]
>
>应谨慎更改此结构或其中的文件。 确保您完全了解所做的任何更改的含义。
>
>您不得更改路径中的任 `/libs` 何内容。 对于配置和其他更改，将项目从复 `/libs` 制到 `/apps` 并在中进行任何更改 `/apps`。
