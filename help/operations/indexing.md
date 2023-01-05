---
title: 内容搜索与索引
description: 内容搜索与索引
exl-id: 4fe5375c-1c84-44e7-9f78-1ac18fc6ea6b
source-git-commit: 6fd5f8e7a9699f60457e232bb3cfa011f34880e9
workflow-type: tm+mt
source-wordcount: '2498'
ht-degree: 88%

---

# 内容搜索与索引 {#indexing}

## AEM as a Cloud Service 更改 {#changes-in-aem-as-a-cloud-service}

随着 AEM as a Cloud Service 的推出，Adobe 正在从以 AEM 实例为中心的模型转向基于服务的视图，该视图包含 n-x AEM 容器，由 Cloud Manager 中的 CI/CD 管道驱动。必须在部署之前指定索引配置，而不得在单个 AEM 实例上配置和维护索引。在生产过程中更改配置显然违反 CI/CD 策略。同样的情况也适用于更改索引，因为如果未规定在将索引投入生产之前测试和重新编制索引，则更改索引可能会影响系统稳定性和性能。

以下列出与 AEM 6.5 和更低版本相比的主要变化：

1. 用户将无法再访问单个 AEM 实例的索引管理器以调试、配置或维护索引编制。它仅用于本地开发和内部部署。
1. 用户将不会在单个 AEM 实例上更改索引，也不必再担心一致性检查或重新编制索引。
1. 一般在投入生产之前开始更改索引，以免回避 Cloud Manager CI/CD 管道中的质量关卡以及影响生产过程中的业务 KPI。
1. 客户可在运行时获得所有相关指标（包括生产过程中的搜索性能），以全面了解关于搜索和索引编制的话题。
1. 客户将能够根据自己的需要设置警报。
1. SRE 全天候监控系统运行状况，并将根据需要尽早采取措施。
1. 通过部署更改索引配置。像其他内容更改一样配置索引定义更改。
1. 在 AEM as a Cloud Service 的高层，随着引入[蓝绿部署模型](#index-management-using-blue-green-deployments)，将存在两组索引：一组用于旧版本（蓝色），另一组用于新版本（绿色）。
1. 客户可以在 Cloud Manager 生成页面上查看索引工作是否完成，并将在新版本准备好接收流量时收到通知。

限制：

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
1. 完全自定义的索引。示例为：`/oak:index/acme.product-1-custom-2`。为避免命名冲突，我们要求完全自定义索引具有前缀，例如， `acme.`

请注意，经过自定义的开箱即用索引和完全自定义的索引都需要包含 `-custom-`。只有完全自定义的索引必须以前缀开头。

## 准备新索引定义 {#preparing-the-new-index-definition}

>[!NOTE]
>
>如果自定义开箱即用索引，例如 `damAssetLucene-6`，请使用 CRX DE 包管理器 (`/crx/packmgr/`) 从 *Cloud Service 环境*&#x200B;复制最新的开箱即用索引定义。 然后将配置重命名为例如 `damAssetLucene-6-custom-1`，并将您的自定义添加到顶部。这样确保不会无意中删除所需的配置。例如，`/oak:index/damAssetLucene-6/tika` 下的 `tika` 节点需要在 Cloud Service 的自定义索引中。Cloud SDK 上不存在它。

您需要按照以下命名模式准备一个包含实际索引定义的新索引定义包：

`<indexName>[-<productVersion>]-custom-<customVersion>`

然后需要将它放在 `ui.apps/src/main/content/jcr_root` 下。所有自定义和自定义索引定义都需要存储在 `/oak:index` 中。

需要设置包的过滤器，以便保留现有的（开箱即用索引）。在文件 `ui.apps/src/main/content/META-INF/vault/filter.xml` 中，则需要列出每个自定义（或自定义）索引，例如 `<filter root="/oak:index/damAssetLucene-6-custom-1"/>`。 如果稍后更改了索引版本，则需要调整过滤器。

<!-- Alexandru: temporarily drafting this statement due to CQDOC-17701

The package from the above sample is built as `com.adobe.granite:new-index-content:zip:1.0.0-SNAPSHOT`. -->

>[!NOTE]
>
>任何包含索引定义的内容包都应该在位于 `/META-INF/vault/properties.xml` 的内容包属性文件中设置以下属性：
>
>`noIntermediateSaves=true`

## 部署索引定义 {#deploying-index-definitions}

索引定义被标为自定义并进行版本控制：

* 索引定义本身（例如 `/oak:index/ntBaseLucene-custom-1`）

要部署自定义或自定义索引，索引定义 (`/oak:index/definitionname`) 需要在 Git 和 Cloud Manager 部署过程中通过 `ui.apps` 投放。 例如，在FileVault筛选器中， `ui.apps/src/main/content/META-INF/vault/filter.xml`，分别列出每个自定义索引和自定义索引，例如 `<filter root="/oak:index/damAssetLucene-7-custom-1"/>`. 自定义/自定义索引定义本身随后将存储在文件中 `ui.apps/src/main/content/jcr_root/_oak_index/damAssetLucene-7-custom-1/.content.xml`，如下所示：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:oak="https://jackrabbit.apache.org/oak/ns/1.0" xmlns:dam="http://www.day.com/dam/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0" xmlns:nt="http://www.jcp.org/jcr/nt/1.0" xmlns:rep="internal"
        jcr:primaryType="oak:QueryIndexDefinition"
        async="[async,nrt]"
        compatVersion="{Long}2"
        ...
        </indexRules>
        <tika jcr:primaryType="nt:unstructured">
            <config.xml jcr:primaryType="nt:file"/>
        </tika>
</jcr:root>
```

上例包含 Apache Tika 的配置。 Tika 配置文件将存储在 `ui.apps/src/main/content/jcr_root/_oak_index/damAssetLucene-7-custom-1/tika/config.xml`。

### 项目配置

根据使用的 Jackrabbit Filevault Maven 包插件版本，需要在项目中进行其他配置。 当使用 Jackrabbit Filevault Maven Package Plugin 版本 **1.1.6** 或更新版本时，文件 `pom.xml` 需要在 `configuration/validatorsSettings` 中的 `filevault-package-maven-plugin` 的插件配置中包含以下部分（就在 `jackrabbit-nodetypes` 之前）：

```xml
<jackrabbit-packagetype>
    <options>
        <immutableRootNodeNames>apps,libs,oak:index</immutableRootNodeNames>
    </options>
</jackrabbit-packagetype>
```

此外，在本例中，`vault-validation` 版本需要升级到较新版本：

```xml
<dependency>
    <groupId>org.apache.jackrabbit.vault</groupId>
    <artifactId>vault-validation</artifactId>
    <version>3.5.6</version>
</dependency>
```

然后，在 `ui.apps.structure/pom.xml` 和 `ui.apps/pom.xml` 中，`filevault-package-maven-plugin` 的配置需要启用 `allowIndexDefinitions` 以及 `noIntermediateSaves`。 选项 `noIntermediateSaves` 确保自动添加索引配置。

```xml
<groupId>org.apache.jackrabbit</groupId>
    <artifactId>filevault-package-maven-plugin</artifactId>
    <configuration>
        <allowIndexDefinitions>true</allowIndexDefinitions>
        <properties>
            <cloudManagerTarget>none</cloudManagerTarget>
            <noIntermediateSaves>true</noIntermediateSaves>
        </properties>
    ...
```

在 `ui.apps.structure/pom.xml` 中，此插件的 `filters` 部分需要包含一个过滤器根，如下所示：

```xml
<filter><root>/oak:index</root></filter>
```

添加新的索引定义后，需要通过 Cloud Manager 部署新的应用程序。部署完毕后将开始执行两个作业，负责将索引定义分别添加到 MongoDB 和 Azure 段存储（如果需要，还可合并索引定义）以供编写和发布。在切换蓝绿之前，将用新的索引定义为底层存储库重新编制索引。

### 注意

如果在filevault验证中发现以下错误 <br>
`[ERROR] ValidationViolation: "jackrabbit-nodetypes: Mandatory child node missing: jcr:content [nt:base] inside node with types [nt:file]"` <br>
然后，可以执行以下任一步骤来修复该问题 —  <br>
1. 将文件降级到版本1.0.4，并将以下内容添加到顶级pom中：

```xml
<allowIndexDefinitions>true</allowIndexDefinitions>
```

以下示例说明了将上述配置放在pom中的位置。

```xml
<plugin>
    <groupId>org.apache.jackrabbit</groupId>
    <artifactId>filevault-package-maven-plugin</artifactId>
    <configuration>
        <properties>
        ...
        </properties>
        ...
        <allowIndexDefinitions>true</allowIndexDefinitions>
        <repositoryStructurePackages>
        ...
        </repositoryStructurePackages>
        <dependencies>
        ...
        </dependencies>
    </configuration>
</plugin>
```

1. 禁用nodetype验证。 在filevault插件配置的jackrabbit-nodetypes部分中设置以下属性：

```xml
<isDisabled>true</isDisabled>
```

以下示例说明了将上述配置放在pom中的位置。

```xml
<plugin>
    <groupId>org.apache.jackrabbit</groupId>
    <artifactId>filevault-package-maven-plugin</artifactId>
    ...
    <configuration>
    ...
        <validatorsSettings>
        ...
            <jackrabbit-nodetypes>
                <isDisabled>true</isDisabled>
            </jackrabbit-nodetypes>
        </validatorsSettings>
    </configuration>
</plugin>
```

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

在开发期间或在使用内部部署时，可在运行时添加、删除或更改索引。一旦有索引可用，即使用这些索引。如果还不需要在应用程序的旧版本中使用某个索引，则一般在计划停机期间编制该索引。删除索引或更改现有索引时也会发生同样的情况。在删除索引时，一旦删除，该索引即不可用。

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

目前，仅支持类型索引的索引管理 `lucene`，使用 `compatVersion` 设置为 `2`. 在内部，可以配置其他索引并用于查询，例如Elasticsearch索引。 针对 `damAssetLucene` 实际上，在AEMas a Cloud Service上，可能会针对此索引的Elasticsearch版本执行索引。 此差异对应用程序最终用户而言是不可见的，但某些工具(如 `explain` 功能将报告其他索引。 有关Lucene和Elasticsearch索引之间的差异，请参阅 [Apache Jackrabbit Oak中的Elasticsearch文档](https://jackrabbit.apache.org/oak/docs/query/elastic.html). 客户不能也不需要直接配置Elasticsearch索引。

仅支持内置分析程序（即随产品一起提供的分析程序）。 不支持自定义分析器。

为获得最佳运行性能，索引不应过大。 所有索引的总大小都可用作指南：如果在添加自定义索引并在开发环境中调整标准索引后，此值增加了100%以上，则应调整自定义索引定义。 AEMas a Cloud Service可以阻止部署会对系统稳定性和性能产生负面影响的索引。

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

### 还原更改 {#undoing-a-change}

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

## 索引和查询优化 {#index-query-optimizations}

通过 Apache Jackrabbit Oak，可灵活地配置索引以高效地处理搜索查询。索引对于大型存储库尤其重要。请确保所有查询都有合适的索引作为支持。没有合适索引的查询可能会读取成千上万个节点，然后将其记录为警告。

有关如何优化查询和索引的信息，请参见[本文档](query-and-indexing-best-practices.md)。
