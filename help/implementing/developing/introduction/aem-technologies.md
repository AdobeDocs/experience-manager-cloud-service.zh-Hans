---
title: AEM 技术基础
description: AEM的技术基础概述，包括AEM的结构以及基础技术，如JCR、Sling和OSGi。
exl-id: ab6e7fe9-a25d-4351-a005-f4466cc0f40e
source-git-commit: a01583483fa89f89b60277c2ce4e1c440590e96c
workflow-type: tm+mt
source-wordcount: '2144'
ht-degree: 1%

---

# AEM 技术基础 {#aem-technical-foundations}

AEM是一个基于经验证、可扩展且灵活的技术构建的强大平台。 本文档详细概述了构成AEM的各个部分，旨在作为全栈AEM开发人员的技术附录。 本指南并非旨在作为入门指南。 如果您不熟悉AEM开发，请参阅 [AEM Sites开发入门 — WKND教程](develop-wknd-tutorial.md) 作为第一步。

>[!TIP]
>
>在深入了解AEM的核心技术之前，Adobe建议完成 [AEM Sites开发入门 — WKND教程。](develop-wknd-tutorial.md)

## 基础知识 {#fundamentals}

作为现代内容管理系统，AEM依赖于标准的Web技术：

* request-response (XMLHttpRequest / XMLHttpResponse)循环
* HTML
* CSS
* JavaScript

底层内容存储库和业务逻辑层是围绕Java™技术构建的：

* JCR
* Sling
* osgi

## Java™内容存储库 {#java-content-repository}

Java™内容存储库(JCR)标准、 [JSR 283](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/index.html)，指定了一种独立于供应商和实现的方法，用于在内容存储库中的粒度级别双向访问内容。 规范牵头方为Adobe研究（瑞士） AG。

此 [JCR API 2.0](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/index.html) 包， `javax.jcr.*` 用于直接访问和处理存储库内容。

AEM基于JCR构建。

## Apache Jackrabbit Oak {#jackrabbit-oak}

[Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/) 是一个可扩展的高性能分层内容存储库的实现，作为现代世界级网站和其他要求苛刻的内容应用程序的基础，符合JCR标准。

Jackrabbit Oak（也简称为Oak）是构建AEM所基于的JCR标准的实现。

## Sling请求处理 {#sling-request-processing}

AEM构建方式 [Sling](https://sling.apache.org/index.html)，这是一个基于REST原则的Web应用程序框架，它提供了易于开发的面向内容的应用程序。 Sling使用Apache Jackrabbit Oak等JCR存储库作为其数据存储。 Sling已对Apache Software Foundation做出了贡献 — 有关更多信息，请参阅Apache 。

### Sling简介 {#introduction-to-sling}

使用Sling时，要呈现的内容类型不是第一个处理注意事项。 相反，主要考虑的问题是URL是否解析为内容对象，然后可以找到脚本来执行渲染。 此过程为Web内容作者提供了绝佳的支持，让他们能够构建可轻松根据自己的需求进行自定义的页面。

在包含各种不同内容元素的应用中，或者在您需要易于自定义的页面时，此灵活性的优势显而易见。 特别是在实施Web内容管理系统(如AEM)时。

参见 [在15分钟内发现Sling](https://sling.apache.org/documentation/getting-started/discover-sling-in-15-minutes.html) 使用Sling进行开发的第一步。

下图说明了Sling脚本解析。 它显示了如何从HTTP请求获取到内容节点、从内容节点获取到资源类型、从资源类型获取到脚本，以及提供了哪些脚本变量。

![了解Apache Sling脚本解析](assets/sling-cheatsheet-01.png)

下图说明了您可以与一起使用的隐藏但功能强大的请求参数 `SlingPostServlet`，所有POST请求的默认处理程序。 该处理程序为您提供了在存储库中创建、修改、删除、复制和移动节点的无限选项。

![使用SlingPostServlet](assets/sling-cheatsheet-02.png)

### Sling以内容为中心 {#sling-is-content-centric}

Sling是 *以内容为中心*. 这意味着处理侧重于内容，因为每个(HTTP)请求都映射到JCR资源（存储库节点）形式的内容：

* 第一个目标是保存内容的资源（JCR节点）
* 其次，表示法或脚本通过请求的某些部分（例如，选择器和/或扩展）从资源属性中定位

### RESTful Sling {#restful-sling}

由于其以内容为中心的理念，Sling实现了一个面向REST的服务器，从而在Web应用程序框架中引入了新概念。 其优点是：

* RESTful，而不只是在曲面上；资源和表示在服务器内正确建模
* 删除一个或多个数据模型
   * 其他内容管理框架可能需要URL结构、业务对象、数据库架构才能访问资源。
   * 使用Sling可将其简化为：URL =资源= JCR结构

### URL分解 {#url-decomposition}

在Sling中，处理由用户请求的URL驱动。 它定义相应的脚本要显示的内容，并从URL中提取信息。

正在分析以下URL：

```text
https://myhost/tools/spy.printable.a4.html/a/b?x=12
```

可以将其划分为复合部分：

| 协议 | 主机 |  | 内容路径 | 选择器 | 扩展 |  | 后缀 |  | 参数 |
|---|---|---|---|---|---|---|---|---|---|
| `https://` | `myhost` | `/` | `tools/spy` | `.printable.a4.` | `html` | `/` | `a/b` | `?` | `x=12` |

* **协议** - HTTPS
* **主机**  — 站点的域
* **内容路径**  — 指定要渲染的内容并与扩展一起使用的路径。 在此示例中，它将转换为 `tools/spy.html`
* **选择器**  — 用于呈现内容的替代方法；在本例中为A4格式的打印机友好版本
* **扩展**  — 内容格式；还指定用于渲染的脚本
* **后缀**  — 可用于指定其他信息
* **参数**  — 动态内容所需的任何参数

#### 从URL到内容和脚本 {#from-url-to-content-and-scripts}

使用URL分解原理：

* 映射使用从请求中提取的内容路径来定位资源。
* 找到相应的资源后，将提取sling资源类型，并用于定位要用于呈现内容的脚本。

下图说明了所使用的机构，以下几节将对此进行更详细的讨论。

![URL映射机制](assets/url-mapping.png)

使用Sling，您可以指定哪个脚本渲染特定实体(通过设置 `sling:resourceType` 属性)。 此机制提供的自由度比脚本访问数据实体的自由度更大（正如PHP脚本中的SQL语句所做的那样），因为资源可以具有多个演绎版。

#### 将请求映射到资源 {#mapping-requests-to-resources}

将细分请求并提取必要信息。 在存储库中搜索请求的资源（内容节点）：

* 第一个Sling检查请求中指定的位置是否存在节点；例如， `../content/corporate/jobs/developer.html`
* 如果未找到节点，则将丢弃扩展并重复搜索；例如， `../content/corporate/jobs/developer`
* 如果未找到节点，则Sling返回http代码404（未找到）。

Sling还允许将JCR节点以外的内容作为资源，但此功能是一项高级功能。

### 定位脚本 {#locating-the-script}

找到相应的资源（内容节点）后， **sling资源类型** 被提取。 此路径定位用于呈现内容的脚本。

指定的路径 `sling:resourceType` 可以是：

* 绝对
* 相对于配置参数

>[!TIP]
>
>由于相对路径提高了可移植性，因此Adobe会推荐相对路径。

所有Sling脚本都存储在以下任一文件夹的子文件夹中： `/apps` （可变，用户脚本）或 `/libs` （不可变，系统脚本），将按此顺序搜索。

其他几点需要注意的是：

* 当需要方法(GET、POST)时，根据HTTP规范以大写形式指定，例如， `jobs.POST.esp`
* 虽然支持各种脚本引擎，但常见的推荐脚本是HTL和JavaScript。

Felix管理控制台上列出了给定的AEM实例支持的脚本引擎列表( `http://<host>:<port>/system/console/slingscripting`)。

使用上一个示例，如果 `sling:resourceType` 是 `hr/jobs` 然后用于：

* 以结尾的GET/HEAD请求和URL `.html` （默认请求类型，默认格式）
   * 脚本为 `/apps/hr/jobs/jobs.esp`；的最后一个部分 `sling:resourceType` 形成文件名。
* POST请求(除GET/HEAD之外的所有请求类型，方法名称必须大写)
   * POST在脚本名称中使用。
   * 脚本为 `/apps/hr/jobs/jobs.POST.esp`.
* 其他格式的URL，结尾不是 `.html`
   * 例如，`../content/corporate/jobs/developer.pdf`
   * 脚本为 `/apps/hr/jobs/jobs.pdf.esp`；后缀将添加到脚本名称中。
* 带有选择器的URL
   * 选择器可用于以替代格式显示相同的内容。 例如，打印机友好版本、rss馈送或摘要。
   * 如果您查看打印机友好版本，其中选择器可能是 `print`；如所示 `../content/corporate/jobs/developer.print.html`
   * 脚本为 `/apps/hr/jobs/jobs.print.esp`；选择器将添加到脚本名称中。
* 如果没有， `sling:resourceType` 定义之后：
   * 内容路径用于搜索适当的脚本(如果基于路径 `ResourceTypeProvider` 活动)。
   * 例如，的脚本 `../content/corporate/jobs/developer.html` 会在以下位置生成搜索： `/apps/content/corporate/jobs/`.
   * 使用主节点类型。
* 如果根本找不到脚本，则使用默认脚本。
   * 默认呈现版本支持为纯文本(`.txt`)，HTML(`.html`)和JSON (`.json`)，所有这些属性都列出了节点的属性（格式合适）。 扩展的默认演绎版 `.res`（或没有请求扩展名的请求）将假脱机资源（如果可能）。
* 对于http错误处理（代码403或404），Sling会在以下位置查找脚本：
   * 位置 `/apps/sling/servlet/errorhandler` 用于自定义脚本
   * 或标准脚本的位置 `/libs/sling/servlet/errorhandler/404.jsp`

如果给定请求应用了多个脚本，则会选择具有最佳匹配的脚本。 匹配项越具体，其效果就越好；换句话说，选择器越多，匹配效果就越好，无论请求扩展名或方法名是否匹配。

例如，考虑访问资源的请求

* `/content/corporate/jobs/developer.print.a4.html`

类型

* `sling:resourceType="hr/jobs"`

假设您在正确位置具有以下脚本列表：

1. `GET.esp`
1. `jobs.esp`
1. `html.esp`
1. `print.esp`
1. `print.html.esp`
1. `print/a4.esp`
1. `print/a4/html.esp`
1. `print/a4.html.esp`

那么优先顺序为(8)-(7)-(6)-(5)-(4)-(3)-(2)-(1)。

除了资源类型(主要由 `sling:resourceType` 属性)，还有资源超类型。 此类型由 `sling:resourceSuperType` 属性。 在尝试查找脚本时，也会考虑这些超类型。 资源超级类型的优点在于，它们可以形成资源的层次结构，其中默认资源类型 `sling/servlet/default` （由默认servlet使用）实际上是根。

可以通过两种方式定义资源的资源超级类型：

* 按 `sling:resourceSuperType` 资源的属性。
* 按 `sling:resourceSuperType` 节点属性，该节点的 `sling:resourceType` 点数。

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
   * 是 `[ c, b, a, <default>]`
* 而为 `/y`
   * 层次结构为 `[ c, a, <default>]`

原因在于 `/y` 具有 `sling:resourceSuperType` 属性，而 `/x` 不会，因此其超类型取自其资源类型。

#### 无法直接调用Sling脚本 {#sling-scripts-cannot-be-called-directly}

在Sling中，无法直接调用脚本，因为它将违反REST服务器的严格概念；您将混合使用资源和表示法。

如果直接调用表示形式（脚本），则会在脚本中隐藏资源，因此框架(Sling)不再知道该表示形式。 因此，您将丢失某些特征：

* 自动处理GET以外的http方法，包括：
   * 通过sling默认实现处理的POST、PUT、DELETE
   * 此 `POST.jsp` 中的脚本 `sling:resourceType` 位置
* 您的代码架构不再像以前那样干净和结构清晰；这对于大规模开发至关重要

### Sling API {#sling-api}

使用Sling API包， `org.apache.sling.*`和标记库之间的映射。

### 使用sling：include引用现有元素 {#referencing-existing-elements-using-sling-include}

最后需要考虑的是在脚本中引用现有元素的需要。

更复杂的脚本（聚合脚本）可访问多个资源（例如导航、侧栏、页脚、列表元素），具体操作是包括 *资源*.

在这种情况下，您可以使用 `sling:include("/<path>/<resource>")` 命令。 它有效地包含了引用资源的定义。

## osgi {#osgi}

OSGi(Open Services Gateway Initiative)定义了用于开发和部署模块化应用程序和库(也称为Dynamic Module System for Java™)的体系结构。 OSGi容器允许您将应用程序分成单独的模块（包含其他元信息的jar文件，在OSGi术语中称为捆绑包），并通过以下方式管理它们之间的交叉依赖关系：

* 在容器中实施的服务
* 容器与您的应用程序之间的合同

这些服务和合同提供了一个体系结构，使各个元素能够动态地发现彼此进行协作。

随后，OSGi框架将为您提供这些捆绑包的动态加载/卸载、配置和控制，而无需重新启动。

>[!NOTE]
>
>有关OSGi技术的完整信息，请访问 [OSGi网站](https://www.osgi.org).
>
>特别是，他们的“基础教育”页面包含一系列演示和教程。

利用此架构，可使用特定于应用程序的模块扩展Sling。 Sling以及AEM使用 [Apache Felix](https://felix.apache.org/documentation/index.html) OSGi的实现。 它们都是在OSGi框架内运行的OSGi捆绑包的集合。

此功能允许您对安装中的任何包执行以下操作：

* 安装
* 启动
* 停止
* 更新
* 卸载
* 查看最新状态
* 访问有关特定捆绑包的更多详细信息，例如符号名称、版本和位置

参见 [为AEMas a Cloud Service配置OSGi](/help/implementing/deploying/configuring-osgi.md) 了解更多信息。

## 存储库中的结构 {#structure-within-the-repository}

以下列表概述了您在存储库中看到的结构。

* `/apps`  — 与应用程序相关；包括特定于您网站的组件定义。 您开发的组件可以基于以下位置提供的现成组件 `/libs/core/wcm/components`.
* `/content`  — 为您的网站创建的内容。
* `/etc`
* `/home`  — 用户和组信息。
* `/libs`  — 属于AEM核心的库和定义。 中的子文件夹 `/libs` 表示现成的AEM功能。 中的内容 `/libs` 不能修改。 特定于您网站的功能应位于 `/apps`.
* `/tmp`  — 临时工作区。
* `/var`  — 系统更改和更新的文件；如审核日志、统计数据、事件处理。

>[!CAUTION]
>
>对此结构或其中的文件所做的更改应谨慎进行。 确保您充分了解所做任何更改的影响。
>
>请勿更改 `/libs` 路径。 对于配置和其他更改，从以下位置复制项目 `/libs` 到 `/apps` 并在中进行任何更改 `/apps`.
