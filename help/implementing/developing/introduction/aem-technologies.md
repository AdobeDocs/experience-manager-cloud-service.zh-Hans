---
title: AEM技术基础
description: 概述AEM的技术基础，包括AEM的结构方式和基本技术（如JCR、Sling和OSGi）。
exl-id: ab6e7fe9-a25d-4351-a005-f4466cc0f40e
source-git-commit: 08559417c8047c592f2db54321afe68836b75bd1
workflow-type: tm+mt
source-wordcount: '2186'
ht-degree: 0%

---

# AEM技术基础 {#aem-technical-foundations}

AEM是一个基于经验证、可扩展和灵活的技术构建的强大平台。 本文档详细概述了构成AEM的各个部分，这些部分旨在作为全栈AEM开发人员的技术附录。 本指南不提供入门指南。 如果您是初次使用AEM开发，请参阅[AEM Sites开发入门 — WKND教程](develop-wknd-tutorial.md)作为第一步。

>[!TIP]
>
>在深入研究AEM的核心技术之前，Adobe建议先完成[AEM Sites开发入门 — WKND教程。](develop-wknd-tutorial.md)

## 基础 {#fundamentals}

作为现代内容管理系统，AEM依赖于标准的Web技术：

* 请求 — 响应(XMLHttpRequest / XMLHttpResponse)周期
* HTML
* CSS
* JavaScript

基础内容存储库和业务逻辑层是围绕Java技术构建的：

* JCR
* Sling
* OSGi

## Java内容存储库 {#java-content-repository}

Java内容存储库(JCR)标准[JSR 283](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/index.html)指定了一种独立于供应商和独立于实施的方式，用于在内容存储库的粒度级别上双向访问内容。 Adobe研究公司（瑞士）AG持有规格指标。

[JCR API 2.0](https://www.adobe.io/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/index.html)包`javax.jcr.*`用于直接访问和处理存储库内容。

AEM基于JCR构建。

## Apache Jackrabbit Oak {#jackrabbit-oak}

[Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/) 是一种可扩展且高性能的分层内容存储库的实施，用作现代世界级网站和其他要求苛刻的内容应用程序的基础，符合JCR标准。

Jackrabbit Oak（也简称Oak）是构建AEM的JCR标准的实施。

## Sling请求处理 {#sling-request-processing}

AEM是使用[Sling](https://sling.apache.org/site/index.html)构建的，Sling是一个基于REST原则的Web应用程序框架，可轻松开发面向内容的应用程序。 Sling使用JCR存储库（如Apache Jackrabbit Oak）作为其数据存储。 Sling已对Apache Software Foundation做出了贡献 — 有关更多信息，请参阅Apache 。

### Sling简介 {#introduction-to-sling}

使用Sling时，要呈现的内容类型不是首要处理考虑事项。 相反，主要考虑的是URL是否解析为内容对象，随后可以找到用于执行渲染的脚本。 这为Web内容作者构建可轻松根据其要求进行自定义的页面提供了极佳支持。

在具有多种不同内容元素的应用程序中，或者您需要能够轻松自定义的页面时，这种灵活性的优势显而易见。 特别是，在实施Web内容管理系统(如AEM)时。

请参阅[在15分钟内发现Sling](https://sling.apache.org/documentation/getting-started/discover-sling-in-15-minutes.html) ，了解使用Sling进行开发的首要步骤。

下图说明了Sling脚本解析：它显示了如何从HTTP请求到内容节点、从内容节点到资源类型、从资源类型到脚本，以及哪些脚本变量可用。

![了解Apache Sling脚本解析](assets/sling-cheatsheet-01.png)

下图说明了处理`SlingPostServlet`(所有POST请求的默认处理程序)时可以使用的所有隐藏但功能强大的请求参数，这些参数为您提供了无限的选项，用于在存储库中创建、修改、删除、复制和移动节点。

![使用SlingPostServlet](assets/sling-cheatsheet-02.png)

### Sling以内容为中心 {#sling-is-content-centric}

Sling以&#x200B;*以内容为中心*。 这意味着当每个(HTTP)请求以JCR资源（存储库节点）的形式映射到内容时，处理重点会放在内容上：

* 第一个目标是保存内容的资源（JCR节点）
* 其次，表示或脚本是与请求的某些部分（例如，选择器和/或扩展）组合在一起从资源属性中找到的

### RESTful Sling {#restful-sling}

Sling由于其以内容为中心的理念，实施了面向REST的服务器，因此在Web应用程序框架中具有新的概念。 优点是：

* 非常RESTful，不仅仅在表面；资源和表示在服务器内正确建模
* 删除一个或多个数据模型
   * 其他内容管理框架可能需要URL结构、业务对象、数据库模式才能访问资源。
   * 使用Sling，可简化为：URL = resource = JCR结构

### URL分解 {#url-decomposition}

在Sling中，处理由用户请求的URL驱动。 这定义了要由相应脚本显示的内容。 为此，将从URL中提取信息。

如果我们分析以下URL:

```text
https://myhost/tools/spy.printable.a4.html/a/b?x=12
```

我们可以把它分解成复合部分：

| 协议 | 主机 |  | 内容路径 | 选择器 | 扩展 |  | 后缀 |  | 参数 |
|---|---|---|---|---|---|---|---|---|---|
| `https://` | `myhost` | `/` | `tools/spy` | `.printable.a4.` | `html` | `/` | `a/b` | `?` | `x=12` |

* **协议**  - HTTPS
* **host**  — 网站的域
* **内容路径**  — 指定要呈现的内容并与扩展结合使用的路径；在本例中，它们转换为  `tools/spy.html`
* **选择器**  — 用于呈现内容的替代方法；在本例中，为A4格式的打印机友好版本
* **扩展**  — 内容格式；还指定用于渲染的脚本
* **后缀**  — 可用于指定其他信息
* **参数**  — 动态内容所需的任何参数

#### 从URL到内容和脚本 {#from-url-to-content-and-scripts}

使用URL分解的原则：

* 映射使用从请求提取的内容路径来查找资源。
* 找到相应的资源后，将提取Sling资源类型，并将其用于查找用于渲染内容的脚本。

下图说明了所使用的机制，将在以下各节中详细讨论该机制。

![URL映射机制](assets/url-mapping.png)

使用Sling，您可以指定哪个脚本渲染特定实体（通过在JCR节点中设置`sling:resourceType`属性）。 此机制比脚本在其中访问数据实体（如PHP脚本中的SQL语句那样）的自由度更高，因为资源可以具有多个演绎版。

#### 将请求映射到资源 {#mapping-requests-to-resources}

请求被划分，并提取必要的信息。 在存储库中搜索所请求的资源（内容节点）：

* 第一个Sling检查节点是否位于请求中指定的位置；例如`../content/corporate/jobs/developer.html`
* 如果未找到节点，则将删除扩展并重复搜索；例如`../content/corporate/jobs/developer`
* 如果未找到节点，则Sling将返回http代码404（未找到）。

Sling还允许JCR节点以外的其他内容作为资源，但这是一项高级功能。

### 查找脚本 {#locating-the-script}

在找到相应的资源（内容节点）后，将提取&#x200B;**sling资源类型**。 这是一个路径，用于查找用于呈现内容的脚本。

`sling:resourceType`指定的路径可以是：

* 绝对
* 相对于配置参数

>[!TIP]
>
>Adobe建议使用相对路径，因为它们可增加可移植性。

所有Sling脚本都存储在`/apps`（可变、用户脚本）或`/libs`（不可变、系统脚本）的子文件夹中，这些子文件夹将按此顺序进行搜索。

需要注意的其他几点是：

* 当需要方法(GET、POST)时，它将按照HTTP规范(例如，`jobs.POST.esp`
* 支持各种脚本引擎，但常见的推荐脚本是HTL和JavaScript。

给定AEM实例支持的脚本引擎列表列在Felix管理控制台(`http://<host>:<port>/system/console/slingscripting`)上。

在上一个示例中，如果`sling:resourceType`为`hr/jobs`，则表示：

* GET/HEAD请求和以`.html`结尾的URL（默认请求类型，默认格式）
   * 脚本将为`/apps/hr/jobs/jobs.esp`;`sling:resourceType`的最后一部分构成文件名。
* POST请求(除GET/HEAD以外的所有请求类型，方法名称必须大写)
   * POST将用在脚本名称中。
   * 脚本将为`/apps/hr/jobs/jobs.POST.esp`。
* 其他格式的URL，不以`.html`结尾
   * 例如 `../content/corporate/jobs/developer.pdf`
   * 脚本将为`/apps/hr/jobs/jobs.pdf.esp`;后缀会添加到脚本名称中。
* 包含选择器的URL
   * 选择器可用于以替代格式显示相同的内容。 例如，打印机友好版本、rss源或摘要。
   * 如果我们查看打印机友好版本，其中选择器可能为`print`;如`../content/corporate/jobs/developer.print.html`
   * 脚本将为`/apps/hr/jobs/jobs.print.esp`;选择器即会添加到脚本名称中。
* 如果尚未定义`sling:resourceType`，则：
   * 内容路径将用于搜索相应的脚本（如果基于`ResourceTypeProvider`的路径处于活动状态）。
   * 例如，`../content/corporate/jobs/developer.html`的脚本将在`/apps/content/corporate/jobs/`中生成搜索。
   * 将使用主节点类型。
* 如果根本找不到脚本，则将使用默认脚本。
   * 默认呈现版本当前支持纯文本(`.txt`)、HTML(`.html`)和JSON(`.json`)形式，所有这些格式都将列出节点的属性（格式合适）。 扩展`.res`或没有请求扩展的请求的默认呈现形式是将资源设置为假脱机（如果可能）。
* 对于http错误处理（代码403或404），Sling将在以下任一位置查找脚本：
   * 自定义脚本的`/apps/sling/servlet/errorhandler`位置
   * 或标准脚本`/libs/sling/servlet/errorhandler/404.jsp`的位置

如果给定请求应用多个脚本，则会选择具有最佳匹配项的脚本。 比赛越具体，越好；换言之，无论任何请求扩展名或方法名称是否匹配，选择器越匹配越好。

例如，考虑请求访问资源

* `/content/corporate/jobs/developer.print.a4.html`

类型

* `sling:resourceType="hr/jobs"`

假设我们在正确位置中有以下脚本列表：

1. `GET.esp`
1. `jobs.esp`
1. `html.esp`
1. `print.esp`
1. `print.html.esp`
1. `print/a4.esp`
1. `print/a4/html.esp`
1. `print/a4.html.esp`

然后，优先顺序为(8)-(7)-(6)-(5)-(4)-(3)-(2)-(1)。

除了资源类型（主要由`sling:resourceType`属性定义）之外，还有资源超类型。 这通常由`sling:resourceSuperType`属性指示。 在尝试查找脚本时，还会考虑这些超类型。 资源超级类型的优势在于，它们可以形成资源层次结构，其中默认资源类型`sling/servlet/default`（默认Servlet使用）实际上是根。

资源的资源超类型可以通过两种方式进行定义：

* 按资源的`sling:resourceSuperType`属性。
* `sling:resourceType`所指向节点的`sling:resourceSuperType`属性。

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

以下类型的层次结构类型：

* `/x`
   * 是`[ c, b, a, <default>]`
* 而对于`/y`
   * 层级为`[ c, a, <default>]`

这是因为`/y`具有`sling:resourceSuperType`属性，而`/x`没有，因此其超类型从其资源类型中获取。

#### 无法直接调用Sling脚本 {#sling-scripts-cannot-be-called-directly}

在Sling中，无法直接调用脚本，因为这会破坏REST服务器的严格概念；您将混合使用资源和表示法。

如果您直接调用表示法（脚本），则会将资源隐藏在脚本中，这样框架(Sling)就不再知道该资源了。 因此，您会丢失某些功能：

* 自动处理除GET以外的http方法，包括：
   * POST、PUT、DELETE，通过sling默认实施进行处理
   * `sling:resourceType`位置中的`POST.jsp`脚本
* 您的代码架构不再像应有的那样清晰、结构清晰；对大规模发展至关重要

### Sling API {#sling-api}

它使用Sling API包、 `org.apache.sling.*`和标记库。

### 使用sling:include引用现有元素 {#referencing-existing-elements-using-sling-include}

最后需要考虑的是需要引用脚本中的现有元素。

更复杂的脚本（聚合脚本）可能需要访问多个资源（例如，导航、侧栏、页脚、列表的元素），并通过包含&#x200B;*resource*&#x200B;来执行此操作。

为此，可使用`sling:include("/<path>/<resource>")`命令。 这将有效地包括引用资源的定义。

## OSGi {#osgi}

OSGi（开放服务网关计划）定义了用于开发和部署模块化应用程序和库的架构（又称为Dynamic Module System for Java）。 利用OSGi容器，可将应用程序划分为多个模块（是带有附加元信息的jar文件，在OSGi术语中称为包），并通过以下方式管理它们之间的交叉依赖关系：

* 在容器内实施的服务
* 容器与应用程序之间的合同

这些服务和合同提供了一个架构，使各个元素能够动态地发现彼此以进行协作。

然后，OSGi框架可为您提供这些包的动态加载/卸载、配置和控制 — 无需重新启动。

>[!NOTE]
>
>有关OSGi技术的完整信息，请访问[OSGi网站](https://www.osgi.org)。
>
>特别是，他们的“基础教育”页面包含一系列演示和教程。

此架构允许您使用应用程序特定模块扩展Sling。 Sling，因此也是AEM，使用OSGi的[Apache Felix](https://felix.apache.org/)实施。 它们都是在OSGi框架中运行的OSGi包集合。

这样，您就可以对安装中的任意包执行以下操作：

* 安装
* 开始
* 停止
* 更新
* 卸载
* 查看当前状态
* 访问有关特定包的更多详细信息（例如，符号名称、版本、位置等）

有关更多信息，请参阅[为AEMas a Cloud Service配置OSGi](/help/implementing/deploying/configuring-osgi.md) 。

## 存储库内的结构 {#structure-within-the-repository}

以下列表概述了您将在存储库中看到的结构。

* `/apps`  — 与申请相关；包括特定于您网站的组件定义。您开发的组件可以基于`/libs/core/wcm/components`上提供的现成组件。
* `/content`  — 为您的网站创建的内容。
* `/etc`
* `/home`  — 用户和组信息。
* `/libs`  — 属于AEM核心的库和定义。`/libs`中的子文件夹表示现成的AEM功能。 不能修改`/libs`中的内容。 您网站的特定功能应在`/apps`下进行。
* `/tmp`  — 临时工作区。
* `/var`  — 系统更改和更新的文件；例如审核日志、统计信息、事件处理。

>[!CAUTION]
>
>应谨慎更改此结构或其中的文件。 确保您完全了解所做任何更改的含义。
>
>不得更改`/libs`路径中的任何内容。 对于配置和其他更改，请将项目从`/libs`复制到`/apps`，并在`/apps`中进行任何更改。
