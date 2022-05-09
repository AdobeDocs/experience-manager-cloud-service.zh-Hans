---
title: 内容搜索与索引
description: 内容搜索与索引
exl-id: 4fe5375c-1c84-44e7-9f78-1ac18fc6ea6b
source-git-commit: 3682426cc333414a9fd20000e4d021fc622ff3b5
workflow-type: tm+mt
source-wordcount: '2420'
ht-degree: 98%

---

# 内容搜索与索引 {#indexing}

## AEM as a Cloud Service 更改 {#changes-in-aem-as-a-cloud-service}

随着 AEM as a Cloud Service 的推出，Adobe 正在从以 AEM 实例为中心的模型转向基于服务的视图，该视图包含 n-x AEM 容器，由 Cloud Manager 中的 CI/CD 管道驱动。必须在部署之前指定索引配置，而不得在单个 AEM 实例上配置和维护索引。在生产过程中更改配置显然违反 CI/CD 策略。同样的情况也适用于更改索引，因为如果未规定在将索引投入生产之前测试和重新编制索引，则更改索引可能会影响系统稳定性和性能。

以下列出与 AEM 6.5 和更低版本相比的主要变化：

1. 用户将无法再访问单个 AEM 实例的索引管理器以调试、配置或维护索引编制。它仅用于本地开发和现场部署。

1. 用户将不会在单个 AEM 实例上更改索引，也不必再担心一致性检查或重新编制索引。

1. 一般在投入生产之前开始更改索引，以免回避 Cloud Manager CI/CD 管道中的质量关卡以及影响生产过程中的业务 KPI。

1. 客户可在运行时获得所有相关指标（包括生产过程中的搜索性能），以全面了解关于搜索和索引编制的话题。

1. 客户将能够根据自己的需要设置警报。

1. SRE 全天候监控系统运行状况，并将根据需要尽早采取措施。

1. 通过部署更改索引配置。像其他内容更改一样配置索引定义更改。

1. 在 AEM as a Cloud Service 的高层，随着引入[蓝绿部署模型](#index-management-using-blue-green-deployments)，将存在两组索引：一组用于旧版本（蓝色），另一组用于新版本（绿色）。

1. 客户可以在 Cloud Manager 生成页面上查看索引工作是否完成，并将在新版本准备好接收流量时收到通知。

1. 限制：
* 目前，仅限类型为 `lucene` 的索引支持 AEM as a Cloud Service 上的索引管理。
* 仅支持标准分析器（即产品附带的分析器）。不支持自定义分析器。
* 可在内部配置其他索引并将其用于查询。例如，在 Skyline 上可能实际上针对 `damAssetLucene` 索引的 Elasticsearch 版本执行针对此索引编写的查询。应用程序和用户一般感受不到这一区别，但某些工具（如 `explain` 功能）将报告不同的索引。有关 Lucene 索引与 Elastic 索引之间的区别，请参阅 [Apache Jackrabbit Oak 中的 Elastic 文档](https://jackrabbit.apache.org/oak/docs/query/elastic.html)。客户不需要直接配置 Elasticsearch 索引，也无法这样做。

## 使用方法 {#how-to-use}

定义索引可以包括以下三个用例：

1. 添加新的客户索引定义。
1. 更新现有的索引定义。这实际上意味着添加现有索引定义的新版本。
1. 删除冗余或过时的现有索引。

对于上面的第 1 点和第 2 点，您需要在相应的 Cloud Manager 发布计划中创建一个新的索引定义，作为自定义代码库的一部分。有关更多信息，请参阅[部署到 AEM as a Cloud Service 的文档](/help/implementing/deploying/overview.md)。

## 索引名称 {#index-names}

索引定义可以是：

1. 开箱即用索引。示例为：`/oak:index/cqPageLucene-2`。
1. 经过自定义的开箱即用索引。由客户定义此类自定义。示例为：`/oak:index/cqPageLucene-2-custom-1`。
1. 完全自定义的索引。示例为：`/oak:index/acme.product-1-custom-2`。为了避免命名冲突，我们要求完全自定义的索引附有前缀，例如 `acme.`。

请注意，经过自定义的开箱即用索引和完全自定义的索引都需要包含 `-custom-`。只有完全自定义的索引必须以前缀开头。

## 准备新索引定义 {#preparing-the-new-index-definition}

>[!NOTE]
>
>如果自定义开箱即用索引，例如 `damAssetLucene-6`，请使用 CRX DE 包管理器 (`/crx/packmgr/`) 从&#x200B;*云服务环境*&#x200B;开发环境复制最新的开箱即用索引定义。然后将配置重命名为例如 `damAssetLucene-6-custom-1`，并将您的自定义添加到顶部。这样确保不会无意中删除所需的配置。例如，`/oak:index/damAssetLucene-6/tika` 下的 `tika` 节点需要在云服务的自定义索引中。Cloud SDK 上不存在它。

您需要按照以下命名模式准备一个包含实际索引定义的新索引定义包：

`<indexName>[-<productVersion>]-custom-<customVersion>`

然后需要将它放在 `ui.apps/src/main/content/jcr_root` 下。到目前为止不支持子根文件夹。

需要设置包的过滤器，以便保留现有的（开箱即用索引）。在文件中 `ui.apps/src/main/content/META-INF/vault/filter.xml`，则需要列出每个自定义（或自定义）索引，例如 `<filter root="/oak:index/damAssetLucene-6-custom-1"/>`. 如果稍后更改了索引版本，则需要调整过滤器。

上述示例中的包被构建为 `com.adobe.granite:new-index-content:zip:1.0.0-SNAPSHOT`。

>[!NOTE]
>
>任何包含索引定义的内容包都应该在位于 `/META-INF/vault/properties.xml` 的内容包属性文件中设置以下属性：
>
>`noIntermediateSaves=true`

## 部署索引定义 {#deploying-index-definitions}

>[!NOTE]
>
>Jackrabbit FileVault Maven Package 插件 **1.1.0** 版有一个已知的问题，使得您无法将 `oak:index` 添加到 `<packageType>application</packageType>` 的模块。应更新到该插件的更高版本。

索引定义现在被标为自定义并进行版本控制：

* 索引定义本身（例如 `/oak:index/ntBaseLucene-custom-1`）

因此，为了部署索引，需要通过 `ui.apps` 通过 Git 和 Cloud Manager 部署过程传递索引定义 (`/oak:index/definitionname`)。

添加新的索引定义后，需要通过 Cloud Manager 部署新的应用程序。部署完毕后将开始执行两个作业，负责将索引定义分别添加到 MongoDB 和 Azure 段存储（如果需要，还可合并索引定义）以供编写和发布。在切换蓝绿之前，将用新的索引定义为底层存储库重新编制索引。

>[!TIP]
>
>有关 AEM as a Cloud Service 所需的包结构的更多详细信息，请参阅文档 [AEM 项目结构](/help/implementing/developing/introduction/aem-project-content-package-structure.md)。

## 使用蓝绿部署的索引管理 {#index-management-using-blue-green-deployments}

### 索引管理是什么 {#what-is-index-management}

索引管理涉及添加、删除和更改索引。更改索引的&#x200B;*定义*&#x200B;很迅速，但应用更改（一般称为“编制索引”，对于现有索引称为“重新编制索引”）需要一段时间。此过程并非一蹴而就：必须扫描存储库才能为数据编制索引。

### 蓝绿部署是什么 {#what-is-blue-green-deployment}

蓝绿部署可减少停机时间。它还可实现零停机升级并提供快速回滚。应用程序的旧版本（蓝色）与应用程序的新版本（绿色）同时运行。

### 只读和读写区域 {#read-only-and-read-write-areas}

存储库的某些区域（存储库的只读部分）在应用程序的旧版本（蓝色）和新版本（绿色）中可能不同。存储库的只读区域一般为“`/app`”和“`/libs`”。在下面的示例中，斜体用于标记只读区域，而粗体用于标记读写区域。

* **/**
* */apps（只读）*
* **/content**
* */libs（只读）*
* **/oak:index**
* **/oak:index/acme.**
* **/jcr:system**
* **/system**
* **/var**

在应用程序的所有版本之间共用存储库的读写区域，而对于应用程序的每个版本，都有一组特定的 `/apps` 和 `/libs`。

### 没有蓝绿部署的索引管理 {#index-management-without-blue-green-deployment}

在开发期间或在使用内部安装时，可在运行时添加、删除或更改索引。一旦有索引可用，即使用这些索引。如果还不需要在应用程序的旧版本中使用某个索引，则一般在计划停机期间编制该索引。删除索引或更改现有索引时也会发生同样的情况。在删除索引时，一旦删除，该索引即不可用。

### 有蓝绿部署的索引管理 {#index-management-with-blue-green-deployment}

有蓝绿部署时不会产生停机时间。在升级过程中，有时同时针对同一存储库运行应用程序的旧版本（例如，版本 1）和新版本（版本 2）。如果版本 1 要求某个索引可用，则在版本 2 中不得删除此索引：应稍后在确保应用程序的版本 1 不再运行时删除此索引，例如在版本 3 中。此外，应用程序应编写得即使版本 2 正在运行以及有版本 2 的索引可用，版本 1 也能正常运行。

升级到新版本后，系统可以对旧索引进行垃圾回收。旧索引可能仍会保留一段时间，以加快回滚（如果需要回滚）。

下表显示五个索引定义：在两个版本中都使用索引 `cqPageLucene`，而仅在版本 2 中使用索引 `damAssetLucene-custom-1`。

>[!NOTE]
>
>需要使用 `<indexName>-custom-<customerVersionNumber>`，以使 AEM as a Cloud Service 将此项标为现有索引的替代。

| 索引 | 开箱即用索引 | 在版本 1 中使用 | 在版本 2 中使用 |
|---|---|---|---|
| /oak:index/damAssetLucene | 是 | 是 | 否 |
| /oak:index/damAssetLucene-custom-1 | 是（自定义） | 否 | 是 |
| /oak:index/acme.product-custom-1 | 否 | 是 | 否 |
| /oak:index/acme.product-custom-2 | 否 | 否 | 是 |
| /oak:index/cqPageLucene | 是 | 是 | 是 |

每次更改索引时，版本号都增大。为了避免自定义索引名与产品本身的索引名冲突，自定义索引以及对开箱即用索引的更改必须以 `-custom-<number>` 结尾。

### 对开箱即用索引的更改 {#changes-to-out-of-the-box-indexes}

一旦 Adobe 更改开箱即用索引（如“damAssetLucene”或“cqPageLucene”），即创建名为 `damAssetLucene-2` 或 `cqPageLucene-2` 的新索引，如果已自定义该索引，则自定义的索引定义与开箱即用索引中的更改合并，如下所示。这些更改自动合并。这意味着，如果开箱即用索引发生更改，您无需执行任何操作。但是，之后可以再次自定义索引。

| 索引 | 开箱即用索引 | 在版本 2 中使用 | 在版本 3 中使用 |
|---|---|---|---|
| /oak:index/damAssetLucene-custom-1 | 是（自定义） | 是 | 否 |
| /oak:index/damAssetLucene-2-custom-1 | 是（自动从 damAssetLucene-custom-1 和 damAssetLucene-2 合并） | 否 | 是 |
| /oak:index/cqPageLucene | 是 | 是 | 否 |
| /oak:index/cqPageLucene-2 | 是 | 否 | 是 |

### 当前限制 {#current-limitations}

当前，仅限类型为 `lucene` 的索引支持索引管理。在内部，可以配置其他索引并用于查询，例如弹性索引。

### 添加索引 {#adding-an-index}

要添加一个要在应用程序的新版本和更高版本中使用的名为 `/oak:index/acme.product-custom-1` 的完全自定义索引，必须按如下方式配置该索引：

`acme.product-1-custom-1`

其工作原理是在索引名前加一个自定义标识符，后跟一个点 (**`.`**)。该标识符应为 2 至 5 个字符长。

如上所述，这样确保只有应用程序的新版本使用该索引。

### 更改索引 {#changing-an-index}

当更改了现有的索引时，需要添加更改了索引定义的新索引。例如，设想更改了现有的索引 `/oak:index/acme.product-custom-1`。旧索引存储在 `/oak:index/acme.product-custom-1` 下，而新索引存储在 `/oak:index/acme.product-custom-2` 下。

应用程序的旧版本使用以下配置：

`/oak:index/acme.product-custom-1`

应用程序的新版本使用以下（经过更改的）配置：

`/oak:index/acme.product-custom-2`

>[!NOTE]
>
>AEM as a Cloud Service 上的索引定义可能与本地开发实例上的索引定义不完全相同。开发实例没有 Tika 配置，而 AEM as a Cloud Service 实例有。如果使用 Tika 配置自定义索引，请保留 Tika 配置。

### 撤消更改 {#undoing-a-change}

有时需要撤消索引定义中的更改。原因可能是错误地作出了更改，或者不再需要更改。例如，错误地创建并已部署了索引定义 `damAssetLucene-8-custom-3`。因此，您可能要恢复为以前的索引定义 `damAssetLucene-8-custom-2`。为此，需要添加一个名为 `damAssetLucene-8-custom-4` 的新索引，该索引包含上一个索引 `damAssetLucene-8-custom-2` 的定义。

### 删除索引 {#removing-an-index}

以下内容仅适用于自定义索引。当 AEM 使用产品索引时，无法删除这些索引。

如果要在应用程序的更高版本中删除索引，可用新名称定义一个空索引（从未使用且不含任何数据的空索引）。在本例中，您可以将其命名为 `/oak:index/acme.product-custom-3`。这将替换索引 `/oak:index/acme.product-custom-2`。一旦系统删除 `/oak:index/acme.product-custom-2`，随后即可删除空索引 `/oak:index/acme.product-custom-3`。这种空索引的示例如下：

```xml
<acme.product-custom-3
        jcr:primaryType="oak:QueryIndexDefinition"
        async="async"
        compatVersion="2"
        includedPaths="/dummy"
        queryPaths="/dummy"
        type="lucene">
        <indexRules jcr:primaryType="nt:unstructured">
            <rep:root jcr:primaryType="nt:unstructured">
                <properties jcr:primaryType="nt:unstructured">
                    <dummy
                        jcr:primaryType="nt:unstructured"
                        name="dummy"
                        propertyIndex="{Boolean}true"/>
                </properties>
            </rep:root>
        </indexRules>
    </acme.product-custom-3>
```

如果不再需要自定义开箱即用索引，则必须复制开箱即用索引定义。例如，如果已部署 `damAssetLucene-8-custom-3`，但不再需要自定义，并且要改回默认的 `damAssetLucene-8` 索引，则必须添加一个索引 `damAssetLucene-8-custom-4`，其中包含 `damAssetLucene-8` 的索引定义。

## 索引优化 {#index-optimizations}

通过 Apache Jackrabbit Oak，可灵活地配置索引以高效地处理搜索查询。索引对于大型存储库尤其重要。请确保所有查询都有合适的索引作为支持。没有合适索引的查询可能会读取成千上万个节点，然后将其记录为警告。应通过分析日志文件而找出此类查询，以便可优化索引定义。有关详细信息，请参阅[本页](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/practices/best-practices-for-queries-and-indexing.html?lang=zh-Hans#tips-for-creating-efficient-indexes)。

### AEM as a Cloud Service 上的 Lucene 全文索引 {#index-lucene}

全文索引 `/oak:index/lucene-2` 可能会变得非常大，因为它在默认情况下索引 AEM 存储库中的所有节点。根据 Adobe 停用此索引的计划，AEM as a Cloud Service 中的产品端将不再使用它，并且不需要它即可运行客户代码。对于具有常见 Lucene 索引的 AEM as a Cloud Service 环境，Adobe 正在与客户单独合作，以协调方式补偿该索引，并使用更好、优化的索引。未经 Adobe 进一步通知，客户无需采取任何行动。当关于此优化需要采取行动时，Adobe 将通知 AEM as a Cloud Service 客户。如果自定义查询需要此索引，则应使用不同的名称（例如 `/oak:index/acme.lucene-1-custom-1`）创建此索引的副本作为临时解决方案，如[此处](/help/operations/indexing.md)所述。此优化在默认情况下不适用于本地托管或受 Adobe Managed Services 管理的其他 AEM 环境。

## 查询优化 {#index-query}

通过&#x200B;**查询性能**&#x200B;工具，可观察常用和慢速的 JCR 查询。此外，它还能分析查询并显示尤其是关于是否正在将索引用于此查询的各种信息。

与 AEM 内部部署不同，AEM as a Cloud Service 在 UI 中不再显示&#x200B;**查询性能**&#x200B;工具。现在改为可通过[查询](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html#queries)选项卡上的开发者控制台（在 Cloud Manager 中）找到它。
