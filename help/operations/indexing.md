---
title: 内容搜索与索引
description: 了解AEMas a Cloud Service中的“内容搜索”和“索引”。
exl-id: 4fe5375c-1c84-44e7-9f78-1ac18fc6ea6b
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '2442'
ht-degree: 29%

---

# 内容搜索与索引 {#indexing}

## AEM as a Cloud Service 更改 {#changes-in-aem-as-a-cloud-service}

随着 AEM as a Cloud Service 的推出，Adobe 正在从以 AEM 实例为中心的模型转向基于服务的视图，该视图包含 n-x AEM 容器，由 Cloud Manager 中的 CI/CD 管道驱动。必须在部署之前指定索引配置，而不得在单个 AEM 实例上配置和维护索引。在生产过程中更改配置显然违反 CI/CD 策略。同样的情况也适用于更改索引，因为如果未规定在将索引投入生产之前测试和重新编制索引，则更改索引可能会影响系统稳定性和性能。

以下列出与 AEM 6.5 和更低版本相比的主要变化：

1. 用户无法访问单个AEM实例的索引管理器，无法再调试、配置或维护索引。 它仅用于本地开发和内部部署。
1. 用户不会更改单个AEM实例上的索引，也不必再担心一致性检查或重新编制索引。
1. 一般在投入生产之前开始更改索引，以免回避Cloud Manager CI/CD管道中的质量关卡以及影响生产中的业务KPI。
1. 客户可在运行时获得所有相关量度（包括生产过程中的搜索性能），以提供关于搜索和索引编制主题的整体视图。
1. 客户能够根据自己的需求设置警报。
1. SRE全天候监控系统运行状况，并尽早采取行动。
1. 通过部署更改索引配置。像其他内容更改一样配置索引定义更改。
1. 在AEMas a Cloud Service的高层，随着 [滚动部署模型](#index-management-using-rolling-deployments)，则存在两组索引：一组用于旧版本，另一组用于新版本。
1. 客户可以在Cloud Manager构建页面上查看索引作业是否完成，并在新版本准备好接收流量时收到通知。

限制：

* 目前，仅限类型为 `lucene` 的索引支持 AEM as a Cloud Service 上的索引管理。
* 仅支持标准分析器（即产品附带的分析器）。 不支持自定义分析器。
* 可在内部配置其他索引并将其用于查询。例如，在 Skyline 上可能实际上针对 `damAssetLucene` 索引的 Elasticsearch 版本执行针对此索引编写的查询。应用程序和用户一般感受不到这一区别，但是，某些工具(例如 `explain` 功能报告不同的索引。 有关 Lucene 索引与 Elastic 索引之间的区别，请参阅 [Apache Jackrabbit Oak 中的 Elastic 文档](https://jackrabbit.apache.org/oak/docs/query/elastic.html)。客户不需要直接配置Elasticsearch索引，也无法这样做。
* 按相似特征向量搜索(`useInSimilarity = true`)不受支持。

>[!TIP]
>
>有关Oak索引和查询的更多详细信息，包括高级搜索和索引功能的详细说明，请参阅 [Apache Oak文档](https://jackrabbit.apache.org/oak/docs/query/query.html).


## 使用方法 {#how-to-use}

索引定义可以分为三个主要用例，如下所示：

1. **添加** 新的自定义索引定义。
2. **更新** 通过添加新版本而得到的现有索引定义。
3. **移除** 不再需要的索引定义。

对于上面的第1点和第2点，您需要在相应的Cloud Manager发布计划中创建一个索引定义，作为自定义代码库的一部分。 欲了解更多信息，请参见 [部署到AEMas a Cloud Service](/help/implementing/deploying/overview.md) 文档。

## 索引名称 {#index-names}

索引定义可以分为以下类别之一：

1. 开箱即用(OOTB)索引。 例如： `/oak:index/cqPageLucene-2` 或 `/oak:index/damAssetLucene-8`.

2. 自定义OOTB索引。 通过附加来指示这些变量 `-custom-` 后跟原始索引名的数字标识符。 例如：`/oak:index/damAssetLucene-8-custom-1`。

3. 完全自定义索引：可以从头开始创建全新的索引。 它们的名称必须具有前缀以避免命名冲突。 例如： `/oak:index/acme.product-1-custom-2`，其中前缀为 `acme.`

>[!NOTE]
>
>在上引入新索引 `dam:Asset` 强烈建议不要使用节点类型（特别是全文索引），因为这些类型可能与OOTB产品功能冲突，从而导致功能和性能问题。 通常，向当前添加其他属性 `damAssetLucene-*` 索引版本是对以下内容编制查询索引的最合适方式： `dam:Asset` nodetype (这些更改将自动合并到索引的新产品版本中（如果随后发布）。 如有疑问，请联系Adobe支持以获取建议。

## 准备新索引定义 {#preparing-the-new-index-definition}

>[!NOTE]
>
>例如，如果自定义开箱即用索引， `damAssetLucene-8`，从中复制最新的开箱即用索引定义 *Cloud Service环境* 使用CRX DE包管理器(`/crx/packmgr/`) 。 将其重命名为 `damAssetLucene-8-custom-1` （或更高版本），并将您的自定义项添加到XML文件中。 这样可确保不会无意中删除所需的配置。 例如， `tika` 节点在 `/oak:index/damAssetLucene-8/tika` 在部署到AEM Cloud Service环境的自定义索引中是必需的，但在本地AEM SDK上不存在。

对于OOTB索引的自定义，请准备一个新包，其中包含遵循此命名模式的实际索引定义：

`<indexName>-<productVersion>-custom-<customVersion>`

对于完全自定义的索引，请准备一个新的索引定义包，该包包含遵循此命名模式的索引定义：

`<prefix>.<indexName>-<productVersion>-custom-<customVersion>`

<!-- Alexandru: temporarily drafting this statement due to CQDOC-17701

The package from the above sample is built as `com.adobe.granite:new-index-content:zip:1.0.0-SNAPSHOT`. -->

>[!NOTE]
>
>任何包含索引定义的内容包都应该在位于的内容包属性文件中设置以下属性 `<package_name>/META-INF/vault/properties.xml`：
>
> * `noIntermediateSaves=true`
>
> * `allowIndexDefinitions=true`

## 部署自定义索引定义 {#deploying-custom-index-definitions}

说明如何部署开箱即用索引的自定义版本 `damAssetLucene-8`，我们将提供分步指南。 在本例中，我们将它重命名为 `damAssetLucene-8-custom-1`. 然后按照如下步骤进行操作：

1. 在中使用更新的索引名称创建新文件夹 `ui.apps` 目录：
   * 示例： `ui.apps/src/main/content/jcr_root/_oak_index/damAssetLucene-8-custom-1/`

2. 添加配置文件 `.content.xml` 将自定义配置放置在创建的文件夹中。 以下是自定义设置的示例：文件名： `ui.apps/src/main/content/jcr_root/_oak_index/damAssetLucene-8-custom-1/.content.xml`

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:jcr="http://www.jcp.org/jcr/1.0" xmlns:dam="http://www.day.com/dam/1.0" xmlns:nt="http://www.jcp.org/jcr/nt/1.0" xmlns:oak="http://jackrabbit.apache.org/oak/ns/1.0" xmlns:rep="internal"
       jcr:mixinTypes="[rep:AccessControllable]"
       jcr:primaryType="oak:QueryIndexDefinition"
       async="[async,nrt]"
       compatVersion="{Long}2"
       evaluatePathRestrictions="{Boolean}true"
       includedPaths="[/content/dam]"
       maxFieldLength="{Long}100000"
       type="lucene">
       <facets
           jcr:primaryType="nt:unstructured"
           secure="statistical"
           topChildren="100"/>
       <indexRules jcr:primaryType="nt:unstructured">
           <dam:Asset jcr:primaryType="nt:unstructured">
               <properties jcr:primaryType="nt:unstructured">
                   <cqTags
                       jcr:primaryType="nt:unstructured"
                       name="jcr:content/metadata/cq:tags"
                       nodeScopeIndex="{Boolean}true"
                       propertyIndex="{Boolean}true"
                       useInSpellcheck="{Boolean}true"
                       useInSuggest="{Boolean}true"/>
               </properties>
           </dam:Asset>
       </indexRules>
       <tika jcr:primaryType="nt:folder">
           <config.xml jcr:primaryType="nt:file"/>
       </tika>
   </jcr:root>
   ```

3. 向中的FileVault过滤器添加一个条目 `ui.apps/src/main/content/META-INF/vault/filter.xml`：

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <workspaceFilter version="1.0">
       ...
       <filter root="/oak:index/damAssetLucene-8-custom-1"/> 
   </workspaceFilter>
   ```

4. 在中添加Apache Tika的配置文件： `ui.apps/src/main/content/jcr_root/_oak_index/damAssetLucene-8-custom-1/tika/config.xml`：

   ```xml
   <properties>
       <detectors>
           <detector class="org.apache.tika.detect.TypeDetector"/>
       </detectors>
       <parsers>
           <parser class="org.apache.tika.parser.DefaultParser">
           <mime>text/plain</mime>
           </parser>
       </parsers>
       <service-loader initializableProblemHandler="ignore" dynamic="true"/>
   </properties>
   ```

5. 确保您的配置符合 [项目配置](#project-configuration) 部分。 相应地进行任何必要的调整。

## 项目配置

我们强烈建议使用版本>= `1.3.2` Jackrabbit的 `filevault-package-maven-plugin`. 将该集成到项目中的步骤如下所示：

1. 更新顶级中的版本 `pom.xml`：

   ```xml
   <plugin>
       <groupId>org.apache.jackrabbit</groupId>
           <artifactId>filevault-package-maven-plugin</artifactId>
           ...
           <version>1.3.2</version>
       ...
   </plugin>
   ```

2. 将以下内容添加到顶级 `pom.xml`：

   ```xml
   <jackrabbit-packagetype>
       <options>   
           <immutableRootNodeNames>apps,libs,oak:index</immutableRootNodeNames>
       </options>
   </jackrabbit-packagetype>
   ```

   以下是项目顶层的示例 `pom.xml` 文件包含上述配置：

   文件名： `pom.xml`

   ```xml
   <plugin>
       <groupId>org.apache.jackrabbit</groupId>
           <artifactId>filevault-package-maven-plugin</artifactId>
           ...
           <version>1.3.2</version>
           <configuration>
               ...
               <validatorsSettings>
                   <jackrabbit-packagetype>
                       <options>
                           <immutableRootNodeNames>apps,libs,oak:index</immutableRootNodeNames>
                       </options>
                   </jackrabbit-packagetype>
                   ...
               ...
   </plugin>
   ```

3. 在 `ui.apps/pom.xml` 和 `ui.apps.structure/pom.xml` 必须启用 `allowIndexDefinitions` 和 `noIntermediateSaves` 中的选项 `filevault-package-maven-plugin`. 正在启用 `allowIndexDefinitions` 允许自定义索引定义，而 `noIntermediateSaves` 确保自动添加配置。

   文件名： `ui.apps/pom.xml` 和 `ui.apps.structure/pom.xml`

   ```xml
   <plugin>
       <groupId>org.apache.jackrabbit</groupId>
           <artifactId>filevault-package-maven-plugin</artifactId>
           <configuration>
               <allowIndexDefinitions>true</allowIndexDefinitions>
               <properties>
                   <cloudManagerTarget>none</cloudManagerTarget>
                   <noIntermediateSaves>true</noIntermediateSaves>
               </properties>
       ...
   </plugin>
   ```

4. 添加筛选条件 `/oak:index` 在 `ui.apps.structure/pom.xml`：

   ```xml
   <filters>
       ...
       <filter><root>/oak:index</root></filter>
   </filters>
   ```

添加新的索引定义后，使用Cloud Manager部署新的应用程序。 此部署会启动两个作业，负责将索引定义分别添加到MongoDB和Azure区段存储以供创作和发布（如有必要，还会合并）。 在切换之前，基础存储库会使用更新的索引定义重新索引。

>[!TIP]
>
>有关AEMas a Cloud Service所需的包结构的更多详细信息，请参阅 [AEM项目结构](/help/implementing/developing/introduction/aem-project-content-package-structure.md).

## 使用滚动部署的索引管理 {#index-management-using-rolling-deployments}

### 索引管理是什么 {#what-is-index-management}

索引管理涉及添加、删除和更改索引。更改索引的&#x200B;*定义*&#x200B;很迅速，但应用更改（一般称为“编制索引”，对于现有索引称为“重新编制索引”）需要一段时间。此过程并非一蹴而就：必须扫描存储库才能为数据编制索引。

### 什么是滚动部署 {#what-are-rolling-deployments}

滚动部署可减少停机时间。 它还可实现零停机升级并提供快速回滚。应用程序的旧版本与应用程序的新版本同时运行。

### 只读和读写区域 {#read-only-and-read-write-areas}

存储库的某些区域（存储库的只读部分）在应用程序的旧版本和新版本中可能不同。 存储库的只读区域通常为 `/app` 和 `/libs`. 在下面的示例中，斜体用于标记只读区域，而粗体用于标记读写区域。

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

### 无需滚动部署的索引管理 {#index-management-without-rolling-deployments}

在开发期间或在使用内部部署时，可在运行时添加、删除或更改索引。 索引在可用时使用。 如果应用程序的旧版本中尚未使用索引，则通常在计划停机期间构建索引。 删除索引或更改现有索引时也会发生同样的情况。删除索引时，该索引在删除时不可用。

### 具有滚动部署的索引管理 {#index-management-with-rolling-deployments}

使用滚动部署，不会出现停机。 在更新过程中，应用程序的旧版本（例如，版本1）和新版本（版本2）会针对同一存储库同时运行。 如果版本1要求某个索引可用，则不得在版本2中删除此索引。 稍后应删除索引，例如在版本3中，此时应确保应用程序的版本1不再运行。 此外，应用程序应编写得即使版本 2 正在运行以及有版本 2 的索引可用，版本 1 也能正常运行。

升级到新版本后，系统可以对旧索引进行垃圾回收。旧索引可能仍会保留一段时间，以加快回滚（如果需要回滚）。

下表显示五个索引定义：在两个版本中都使用索引 `cqPageLucene`，而仅在版本 2 中使用索引 `damAssetLucene-custom-1`。

>[!NOTE]
>
>此 `<indexName>-custom-<customerVersionNumber>` 需要，以使AEMas a Cloud Service将其标记为现有索引的替代。

| 索引 | 开箱即用索引 | 在版本 1 中使用 | 在版本 2 中使用 |
|---|---|---|---|
| /oak:index/damAssetLucene | 是 | 是 | 否 |
| /oak:index/damAssetLucene-custom-1 | 是（自定义） | 否 | 是 |
| /oak:index/acme.product-custom-1 | 否 | 是 | 否 |
| /oak:index/acme.product-custom-2 | 否 | 否 | 是 |
| /oak:index/cqPageLucene | 是 | 是 | 是 |

每次更改索引时，版本号都增大。要避免自定义索引名与产品本身的索引名冲突，自定义索引以及对开箱即用索引的更改必须以结尾 `-custom-<number>`.

### 对开箱即用索引的更改 {#changes-to-out-of-the-box-indexes}

在Adobe更改开箱即用索引（如“damAssetLucene”或“cqPageLucene”）后，名为的新索引 `damAssetLucene-2` 或 `cqPageLucene-2` 创建。 或者，如果已自定义索引，则自定义的索引定义将与现成索引中的更改合并，如下所示。 这些更改自动合并。这意味着，如果开箱即用索引发生更改，您无需执行任何操作。 但是，之后可以再次自定义索引。

| 索引 | 开箱即用索引 | 在版本 2 中使用 | 在版本 3 中使用 |
|---|---|---|---|
| /oak:index/damAssetLucene-custom-1 | 是（自定义） | 是 | 否 |
| /oak:index/damAssetLucene-2-custom-1 | 是（自动从 damAssetLucene-custom-1 和 damAssetLucene-2 合并） | 否 | 是 |
| /oak:index/cqPageLucene | 是 | 是 | 否 |
| /oak:index/cqPageLucene-2 | 是 | 否 | 是 |

### 当前限制 {#current-limitations}

仅类型为的索引支持索引管理 `lucene`，替换为 `compatVersion` 设置为 `2`. 在内部，可以配置其他索引并将其用于查询，例如Elasticsearch索引。 针对编写的查询 `damAssetLucene` 在AEMas a Cloud Service上，索引实际上可能针对此索引的Elasticsearch版本运行。 应用程序用户不会察觉到这种差异，但是 `explain` 功能报告不同的索引。 有关Lucene和Elasticsearch索引之间的区别，请参阅 [Apache Jackrabbit Oak中的Elasticsearch文档](https://jackrabbit.apache.org/oak/docs/query/elastic.html). 客户不能也不需要直接配置Elasticsearch索引。

仅支持内置分析器（即产品附带的分析器）。 不支持自定义分析器。

为获得最佳运行性能，索引不应过大。 所有索引的总大小均可作为参考使用。 如果在添加了自定义索引并在开发环境中调整了标准索引后，此大小增加超过100%，则应调整自定义索引定义。 AEMas a Cloud Service可以阻止部署可能对系统稳定性和性能产生负面影响的索引。

### 添加索引 {#adding-an-index}

添加名为的完全自定义索引 `/oak:index/acme.product-custom-1`，以便在应用程序的新版本和更高版本中使用，必须按如下方式配置索引：

`acme.product-1-custom-1`

此配置的工作方式是在索引名称前加一个自定义标识符，后跟一个点(**`.`**)。 标识符应为2到5个字符长。

如上所述，此配置确保该索引仅供应用程序的新版本使用。

### 更改索引 {#changing-an-index}

更改现有索引时，必须添加更改了索引定义的新索引。 例如，设想更改了现有的索引 `/oak:index/acme.product-custom-1`。旧索引存储在 `/oak:index/acme.product-custom-1` 下，而新索引存储在 `/oak:index/acme.product-custom-2` 下。

应用程序的旧版本使用以下配置：

`/oak:index/acme.product-custom-1`

应用程序的新版本使用以下（经过更改的）配置：

`/oak:index/acme.product-custom-2`

>[!NOTE]
>
>AEM as a Cloud Service 上的索引定义可能与本地开发实例上的索引定义不完全相同。开发实例没有Tika配置，而AEMas a Cloud Service的实例有。 如果使用Tika配置自定义索引，请保留Tika配置。

### 还原更改 {#undoing-a-change}

有时，需要撤消索引定义中的修改。 这可能是由于意外错误或不再需要修改而导致的。 以索引定义为例 `damAssetLucene-8-custom-3,` 错误地创建并已部署。 因此，要恢复为以前的索引定义， `damAssetLucene-8-custom-2.` 要实现此目的，您需要引入名为的新索引 `damAssetLucene-8-custom-4` 包含了先前索引的定义， `damAssetLucene-8-custom-2.`

### 删除索引 {#removing-an-index}

以下内容仅适用于自定义索引。当 AEM 使用产品索引时，无法删除这些索引。

如果在应用程序的更高版本中删除了索引，则可以使用新名称定义空索引（从未使用且不包含任何数据的空索引）。 在本例中，您可以将其命名为 `/oak:index/acme.product-custom-3`. 此名称将替换索引 `/oak:index/acme.product-custom-2`. 之后 `/oak:index/acme.product-custom-2` 被系统删除，空索引 `/oak:index/acme.product-custom-3` 然后可以删除。 这种空索引的示例如下：

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

通过 Apache Jackrabbit Oak，可灵活地配置索引以高效地处理搜索查询。索引对于大型存储库尤其重要。确保所有查询都有适当的索引作为支持。 没有合适索引的查询可能会读取数千个节点，然后将其记录为警告。

请参阅 [本文档](query-and-indexing-best-practices.md) 有关如何优化查询和索引的信息。
