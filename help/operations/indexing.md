---
title: 内容搜索与索引
description: 了解AEM as a Cloud Service中的内容搜索和索引编制。
exl-id: 4fe5375c-1c84-44e7-9f78-1ac18fc6ea6b
feature: Operations
role: Admin
source-git-commit: 8d881caf5181e9c3cdc6dcb69f0deabc2d5eeed8
workflow-type: tm+mt
source-wordcount: '2918'
ht-degree: 17%

---

# 内容搜索与索引 {#indexing}

## AEM as a Cloud Service 更改 {#changes-in-aem-as-a-cloud-service}

随着 AEM as a Cloud Service 的推出，Adobe 正在从以 AEM 实例为中心的模型转向基于服务的视图，该视图包含 n-x AEM 容器，由 Cloud Manager 中的 CI/CD 管道驱动。必须在部署之前指定索引配置，而不是在单个AEM实例上配置和维护索引。 在生产过程中更改配置将违反CI/CD策略。 同样的情况也适用于更改索引，因为如果未指定、测试和重新编制索引，在将索引投入生产之前，更改索引可能会影响系统稳定性和性能。

以下列出与 AEM 6.5 和更低版本相比的主要变化：

1. 用户无法访问单个AEM实例的索引管理器，无法再调试、配置或维护索引。 它仅用于本地开发和内部部署。
1. 用户不会更改单个AEM实例上的索引，也不必再担心一致性检查或重新编制索引。
1. 一般在投入生产之前开始更改索引，以免回避Cloud Manager CI/CD管道中的质量关卡以及影响生产过程中的业务KPI。
1. 客户可在运行时获得所有相关指标（包括生产过程中的搜索性能），以提供关于搜索和索引编制主题的整体视图。
1. 客户能够根据自己的需求设置警报。
1. SRE全天候监控系统运行状况，并尽早采取行动。
1. 通过部署更改索引配置。像其他内容更改一样配置索引定义更改。
1. 在AEM as a Cloud Service的高层，随着[滚动部署模型](#index-management-using-rolling-deployments)的引入，存在两组索引：一组用于旧版本，另一组用于新版本。
1. 客户可以在Cloud Manager内部版本页面上查看索引作业是否完成，并在新版本准备好接收流量时收到通知。

限制：

* 目前，仅类型`lucene`的索引支持AEM as a Cloud Service上的索引管理。 这意味着所有索引自定义项都必须是`lucene`类型。 `async`属性只能是以下属性之一： `[async]`、`[async,nrt]`或`[fulltext-async]`。
* 可在内部配置其他索引并将其用于查询。例如，在AEM as a Cloud Service上，可能实际上针对`damAssetLucene`索引的Elasticsearch版本执行针对索引编写的查询。 此差异对用户不可见。 但是，某些工具（如`explain`功能）报告不同的索引。 有关 Lucene 索引与 Elastic 索引之间的区别，请参阅 [Apache Jackrabbit Oak 中的 Elastic 文档](https://jackrabbit.apache.org/oak/docs/query/elastic.html)。客户不需要直接配置Elasticsearch索引，也无法这样做。
* 仅支持标准分析器（即产品附带的分析器）。 不支持自定义分析器。
* 不支持按相似特征向量(`useInSimilarity = true`)搜索。

>[!TIP]
>
>有关Oak索引和查询的更多详细信息，包括高级搜索和索引功能的详细说明，请参阅[Apache Oak文档](https://jackrabbit.apache.org/oak/docs/query/query.html)。


## 使用方法 {#how-to-use}

索引定义可以分为三个主要用例，如下所示：

1. **添加**&#x200B;新的自定义索引定义。
2. **通过添加新版本来更新**&#x200B;现有的索引定义。
3. **删除**&#x200B;不再需要的索引定义。

对于上面的第1点和第2点，您需要在相应的Cloud Manager发布计划中创建一个索引定义，作为自定义代码库的一部分。 有关详细信息，请参阅[部署到AEM as a Cloud Service](/help/implementing/deploying/overview.md)文档。

## 索引名称 {#index-names}

索引定义可以分为以下类别之一：

1. 开箱即用(OOTB)索引。 这些是AEM提供的预定义索引。 对于实例： `/oak:index/cqPageLucene-2`或`/oak:index/damAssetLucene-8`。

2. 自定义OOTB索引。 要自定义OOTB索引，请附加`-custom-`后跟一个数字。 例如，`/oak:index/damAssetLucene-8-custom-1`是OOTB索引`/oak:index/damAssetLucene-8`的自定义。 自定义通常是OOTB索引的副本，外加需要编制索引的其他属性。

3. 完全自定义索引：您可以从头开始创建全新的索引。 这些索引还需要以`-custom-`和版本号结尾。 此外，为了避免命名冲突，请在索引名称中使用前缀。 例如： `/oak:index/acme.product-1-custom-2`，其中`acme.`是前缀。

>[!NOTE]
>
>强烈建议不要在`dam:Asset`节点类型中引入新索引（特别是全文索引），因为这些索引可能会与OOTB产品功能冲突，从而导致功能和性能问题。 相反，对`dam:Asset`节点类型上的查询进行索引的最合适方法是通过添加其他属性来自定义`damAssetLucene-*`索引。 在后续版本中，这些更改将自动合并到新产品版本中。 如有疑问，请联系Adobe支持人员以获取建议。

## 准备新索引定义 {#preparing-the-new-index-definition}

>[!NOTE]
>
>自定义开箱即用索引（例如`damAssetLucene-8`）时，使用CRX DE包管理器(`/crx/packmgr/`)从&#x200B;*Cloud Service环境*&#x200B;复制最新的开箱即用索引定义。 将其重命名为`damAssetLucene-8-custom-1`（或更高版本），并在XML文件中添加自定义项。 如果云环境中的索引是`elasticsearch`类型，则需要其他更改：将`type`属性更改为`lucene`，将`async`属性更改为`[async,nrt]`，并将属性`similarityTags`更改为`true`。 这样可确保不会无意中删除所需的配置。 例如，在部署到AEM Cloud Service环境的自定义索引中，`/oak:index/damAssetLucene-8/tika`下的`tika`节点是必需的，但在本地AEM SDK上不存在。

要自定义OOTB索引，请准备一个包含自定义或自定义索引定义的新包。 索引名称需要遵循命名模式：

`<indexName>-<productVersion>-custom-<customVersion>`

对于完全自定义的索引，请准备一个新的索引定义包，该包包含遵循此命名模式的索引定义：

`<prefix>.<indexName>-<productVersion>-custom-<customVersion>`

如限制部分中所述，自定义索引定义的`type`必须始终设置为`lucene`，即使使用包管理器提取的索引定义属于其他类型（例如`elasticsearch`）。
如果提取的索引定义设置为`elastic-async`，则还必须更改`async`属性。 对于自定义索引定义，`async`属性必须设置为以下之一： `[async]`、`[async,nrt]`或`[fulltext-async]`。

<!-- Alexandru: temporarily drafting this statement due to CQDOC-17701

The package from the above sample is built as `com.adobe.granite:new-index-content:zip:1.0.0-SNAPSHOT`. -->

>[!NOTE]
>
>任何包含索引定义的内容包都应在内容包的`properties.xml`文件中设置以下属性。 默认情况下，`properties.xml`是在新包中创建的，位于`<package_name>/META-INF/vault/properties.xml`：
>
> * `noIntermediateSaves=true`
>
> * `allowIndexDefinitions=true`

## 部署自定义索引定义 {#deploying-custom-index-definitions}

为了说明如何部署开箱即用索引`damAssetLucene-8`的自定义版本，我们将提供分步指南。 在此示例中，我们将它重命名为`damAssetLucene-8-custom-1`。 然后按照如下步骤进行操作：

1. 在`ui.apps`目录中创建一个具有更新索引名称的新文件夹：
   * 示例：`ui.apps/src/main/content/jcr_root/_oak_index/damAssetLucene-8-custom-1/`

2. 添加包含已创建文件夹中的自定义配置的配置文件`.content.xml`。 以下是自定义示例：
文件名： `ui.apps/src/main/content/jcr_root/_oak_index/damAssetLucene-8-custom-1/.content.xml`

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

3. 向`ui.apps/src/main/content/META-INF/vault/filter.xml`中的FileVault筛选器添加一个条目：

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <workspaceFilter version="1.0">
       ...
       <filter root="/oak:index/damAssetLucene-8-custom-1"/> 
   </workspaceFilter>
   ```

4. 在`ui.apps/src/main/content/jcr_root/_oak_index/damAssetLucene-8-custom-1/tika/config.xml`中添加Apache Tika的配置文件：

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

5. 确保您的配置符合[项目配置](#project-configuration)部分中提供的准则。 相应地进行任何必要的调整。

## 项目配置

我们强烈建议使用Jackrabbit `filevault-package-maven-plugin`的版本>= `1.3.2`。 将该集成到项目中的步骤如下所示：

1. 更新顶级`pom.xml`中的版本：

   ```xml
   <plugin>
       <groupId>org.apache.jackrabbit</groupId>
           <artifactId>filevault-package-maven-plugin</artifactId>
           ...
           <version>1.3.2</version>
       ...
   </plugin>
   ```

2. 将以下内容添加到顶级`pom.xml`：

   ```xml
   <jackrabbit-packagetype>
       <options>   
           <immutableRootNodeNames>apps,libs,oak:index</immutableRootNodeNames>
       </options>
   </jackrabbit-packagetype>
   ```

   以下是包含上述配置的项目顶级`pom.xml`文件的示例：

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

3. 在`ui.apps/pom.xml`和`ui.apps.structure/pom.xml`中，必须在`filevault-package-maven-plugin`中启用`allowIndexDefinitions`和`noIntermediateSaves`选项。 启用`allowIndexDefinitions`允许自定义索引定义，而`noIntermediateSaves`确保自动添加配置。

   文件名： `ui.apps/pom.xml`和`ui.apps.structure/pom.xml`

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

4. 在`ui.apps.structure/pom.xml`中添加`/oak:index`的筛选器：

   ```xml
   <filters>
       ...
       <filter><root>/oak:index</root></filter>
   </filters>
   ```

添加新的索引定义后，使用Cloud Manager部署新的应用程序。 此部署会启动两个作业，负责将索引定义分别添加到MongoDB和Azure区段存储以供创作和发布（如有必要，还会合并）。 在切换之前，基础存储库会使用更新的索引定义重新索引。

>[!TIP]
>
>有关AEM as a Cloud Service所需的包结构的更多详细信息，请参阅[AEM项目结构](/help/implementing/developing/introduction/aem-project-content-package-structure.md)。

## 使用滚动部署的索引管理 {#index-management-using-rolling-deployments}

### 索引管理是什么 {#what-is-index-management}

索引管理涉及添加、删除和更改索引。更改索引的&#x200B;*定义*&#x200B;很迅速，但应用更改（一般称为“编制索引”，对于现有索引称为“重新编制索引”）需要一段时间。此过程并非一蹴而就：必须扫描存储库才能为数据编制索引。

### 什么是滚动部署 {#what-are-rolling-deployments}

滚动部署允许零停机升级，并提供快速回滚。 应用程序的旧版本与应用程序的新版本同时运行。

### 只读和读写区域 {#read-only-and-read-write-areas}

存储库的某些区域（存储库的只读部分）在应用程序的旧版本和新版本中可能不同。 存储库的只读区域通常为`/app`和`/libs`。 在下面的示例中，斜体用于标记只读区域，而粗体用于标记读写区域。

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

升级到新版本后，系统可以对旧索引进行垃圾回收。旧索引通常保留一周，以加快回滚（如果需要回滚）。

下表显示五个索引定义：在两个版本中都使用索引 `cqPageLucene`，而仅在版本 2 中使用索引 `damAssetLucene-custom-1`。

>[!NOTE]
>
>AEM as a Cloud Service需要`<indexName>-custom-<customerVersionNumber>`才能将其标记为现有索引的替代。

| 索引 | 开箱即用索引 | 在版本 1 中使用 | 在版本 2 中使用 |
|---|---|---|---|
| /oak：index/damAssetLucene-8 | 是 | 是 | 否 |
| /oak：index/damAssetLucene-8-custom-1 | 是（自定义） | 否 | 是 |
| /oak：index/acme.product-1-custom-1 | 否 | 是 | 否 |
| /oak：index/acme.product-1-custom-2 | 否 | 否 | 是 |
| /oak:index/cqPageLucene-2 | 是 | 是 | 是 |

每次更改索引时，版本号都增大。为了避免自定义索引名与产品本身的索引名冲突，自定义索引以及对开箱即用索引的更改必须以`-custom-<number>`结尾。

### 对开箱即用索引的更改 {#changes-to-out-of-the-box-indexes}

Adobe更改开箱即用索引（如`damAssetLucene`或`cqPageLucene`）后，将创建名为`damAssetLucene-2`或`cqPageLucene-2`的新索引。 或者，如果已自定义索引，则自定义的索引定义将与现成索引中的更改合并，如下所示。 这些更改自动合并。这意味着，如果开箱即用索引发生更改，您无需执行任何操作。 但是，以后可以再次自定义索引。 在这种情况下，务必要使用最新（合并的）版本作为基准。

| 索引 | 开箱即用索引 | 在版本 2 中使用 | 在版本 3 中使用 |
|---|---|---|---|
| /oak：index/damAssetLucene-1-custom-1 | 是（自定义） | 是 | 否 |
| /oak:index/damAssetLucene-2-custom-1 | 是（自动从damAssetLucene-1-custom-1和damAssetLucene-2合并） | 否 | 是 |
| /oak:index/cqPageLucene-1 | 是 | 是 | 否 |
| /oak:index/cqPageLucene-2 | 是 | 否 | 是 |

请注意，环境可能使用不同的AEM版本，这一点很重要。 例如： `dev`环境在版本`X+1`上，而暂存和生产仍在版本`X`上，并且正在等待在`dev`上执行了所需的测试之后升级到版本`X+1`。 如果版本`X+1`附带已自定义的产品索引的较新版本，并且需要对该索引进行新的自定义，则下表将说明需要基于基于AEM版本的环境设置哪些版本：

| 环境(AEM发行版本) | 产品索引版本 | 现有自定义索引版本 | 新建自定义索引版本 |
|-----------------------------------|-----------------------|-------------------------------|----------------------------|
| 开发(X+1) | damAssetLucene-11 | damAssetLucene-11-custom-1 | damAssetLucene-11-custom-2 |
| 阶段(X) | damAssetLucene-10 | damAssetLucene-10-custom-1 | damAssetLucene-10-custom-2 |
| 生产(X) | damAssetLucene-10 | damAssetLucene-10-custom-1 | damAssetLucene-10-custom-2 |


### 当前限制 {#current-limitations}

仅类型`lucene`的索引（将`compatVersion`设置为`2`）支持索引管理。 在内部，可以配置其他索引并将其用于查询，例如Elasticsearch索引。 在AEM as a Cloud Service上，可能实际上针对此索引的Elasticsearch版本运行针对`damAssetLucene`索引编写的查询。 应用程序用户看不到此差异，但某些工具（如`explain`功能）报告不同的索引。 有关Lucene和Elasticsearch索引之间的差异，请参阅Apache Jackrabbit Oak中的[Elasticsearch文档](https://jackrabbit.apache.org/oak/docs/query/elastic.html)。 客户不能也不需要直接配置Elasticsearch索引。

仅支持内置分析器（即产品附带的分析器）。 不支持自定义分析器。

目前，不支持对`/oak:index`的内容编制索引。

为获得最佳运行性能，索引不应过大。 所有索引的总大小均可作为参考使用。 如果在添加了自定义索引并在开发环境中调整了标准索引后，此大小增加超过100%，则应调整自定义索引定义。 AEM as a Cloud Service可以阻止部署或删除可能会对系统稳定性和性能产生负面影响的索引。

### 添加索引 {#adding-an-index}

要添加一个要在应用程序的新版本和更高版本中使用的名为`/oak:index/acme.product-1-custom-1`的完全自定义索引，必须按如下方式配置该索引：

`acme.product-1-custom-1`

此配置的工作方式是在索引名称前加一个自定义标识符，后跟一个点(**`.`**)。 标识符应为2到5个字符长。

如上所述，此配置确保该索引仅供应用程序的新版本使用。

### 更改索引 {#changing-an-index}

更改现有索引时，必须添加更改了索引定义的新索引。 例如，设想更改了现有的索引 `/oak:index/acme.product-1-custom-1`。旧索引存储在 `/oak:index/acme.product-1-custom-1` 下，而新索引存储在 `/oak:index/acme.product-1-custom-2` 下。

应用程序的旧版本使用以下配置：

`/oak:index/acme.product-1-custom-1`

应用程序的新版本使用以下（经过更改的）配置：

`/oak:index/acme.product-1-custom-2`

>[!NOTE]
>
>AEM as a Cloud Service 上的索引定义可能与本地开发实例上的索引定义不完全相同。开发实例没有Tika配置，而AEM as a Cloud Service实例有。 如果使用Tika配置自定义索引，请保留Tika配置。

### 还原更改 {#undoing-a-change}

有时候，有必要撤消索引定义中的修改，例如由于错误或不再需要该修改。 例如，如果索引定义`damAssetLucene-8-custom-3`包含错误，您可能希望还原到以前的定义`damAssetLucene-8-custom-2`。 要完成此操作，请创建一个名为`damAssetLucene-8-custom-4`的新索引，它是上一个索引`damAssetLucene-8-custom-2.`的副本

### 删除索引 {#removing-an-index}

以下内容仅适用于现成(OOTB)索引的自定义以及完全自定义的索引。 请注意，无法删除原始OOTB索引，因为它们由AEM使用。

为确保系统完整性和稳定性，索引定义在部署后应被视为不可变。 如果需要删除自定义索引或自定义项，请使用该定义创建该索引的新版本，该定义可以有效地模拟删除
（请参阅下面的示例）。

一旦部署了索引的新版本，查询将不再使用同一索引的旧版本。
较旧的版本不会立即从环境中删除，
但将可以通过定期运行的清理机制进行垃圾收集。
经过宽限期后，在发生错误时可以进行恢复
（目前，索引从被删除起还有7天，但可能会发生更改），
这种清理机制将删除未使用的索引数据，
和将禁用或从环境中删除旧版本的索引。

下面我们描述了两种可能的情况：删除OOTB索引的自定义项和删除完全自定义索引。

#### 删除开箱即用索引的自定义项

按照[使用OOTB索引的定义作为新版本撤消更改](#undoing-a-change-undoing-a-change)中描述的步骤操作。 例如，如果已部署`damAssetLucene-8-custom-3`，但不再需要自定义，并且要切换回默认的`damAssetLucene-8`索引，则需要添加一个包含`damAssetLucene-8`的索引定义的索引`damAssetLucene-8-custom-4`。

#### 删除完全自定义索引

按照[使用虚拟索引作为新版本撤消更改](#undoing-a-change-undoing-a-change)中描述的步骤操作。 虚拟索引从未用于查询，并且不包含任何数据，因此其效果与不存在索引相同。 对于此示例，您可以将其命名为`/oak:index/acme.product-1-custom-3`。 此名称替换索引`/oak:index/acme.product-1-custom-2`。 这种虚拟索引的一个例子是：

```xml
<acme.product-1-custom-3
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
</acme.product-1-custom-3>
```

## 索引和查询优化 {#index-query-optimizations}

通过 Apache Jackrabbit Oak，可灵活地配置索引以高效地处理搜索查询。索引对于大型存储库尤其重要。确保所有查询都有适当的索引作为支持。 没有合适索引的查询可能会读取数千个节点，然后将其记录为警告。

有关如何优化查询和索引的信息，请参阅[本文档](query-and-indexing-best-practices.md)。
