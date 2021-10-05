---
title: 内容搜索与索引
description: 内容搜索与索引
exl-id: 4fe5375c-1c84-44e7-9f78-1ac18fc6ea6b
source-git-commit: dd62f1c0a5c679508c3cf8cc8a1460d86a777759
workflow-type: tm+mt
source-wordcount: '2157'
ht-degree: 1%

---

# 内容搜索与索引 {#indexing}

## AEM as a Cloud Service中的更改 {#changes-in-aem-as-a-cloud-service}

以AEM为Cloud Service,Adobe正在从以AEM实例为中心的模型转变为基于服务的视图，视图中带有n-x AEM容器，由Cloud Manager中的CI/CD管道驱动。 必须在部署之前指定索引配置，而不是在单个AEM实例上配置和维护索引。 生产中的配置更改显然会破坏CI/CD策略。 索引更改也是如此，因为如果未指定测试和重新编制索引，在将索引投入生产之前，它会影响系统稳定性和性能。

以下是与AEM 6.5及更早版本相比的主要更改列表：

1. 用户将无法再访问单个AEM实例的索引管理器来调试、配置或维护索引。 它仅用于本地开发和内部部署。

1. 用户不会更改单个AEM实例上的索引，他们也不必再担心一致性检查或重新编制索引。

1. 通常，在进入生产之前会先启动索引更改，以便不会绕过Cloud Manager CI/CD管道中的质量网关，而不会影响生产中的业务KPI。

1. 所有相关量度（包括生产中的搜索性能）将在运行时提供给客户，以便提供有关搜索和索引主题的整体视图。

1. 客户将能够根据自己的需求设置警报。

1. SRE正在监测系统健康24/7，将根据需要和尽早采取行动。

1. 索引配置通过部署进行更改。 索引定义更改的配置方式与其他内容更改类似。

1. 在AEM as aCloud Service的高级别，引入[Blue-Green部署模型](#index-management-using-blue-green-deployments)后，将存在两组索引：一个针对旧版本设置（蓝色），另一个针对新版本设置（绿色）。

1. 客户可以在Cloud Manager内部版本页面上查看索引作业是否已完成，并在新版本准备好接收流量时收到通知。

1. 限制:
* 目前，仅lucene类型的索引支持对AEM as aCloud Service的索引管理。
* 仅支持标准分析程序（即随产品一起提供的分析程序）。 不支持自定义分析程序。

## 使用方法 {#how-to-use}

定义索引可包括以下三个用例：

1. 添加新的客户索引定义
1. 更新现有索引定义。 这实际上意味着添加现有索引定义的新版本
1. 删除冗余或过时的现有索引。

对于以上第1点和第2点，您需要在相应的Cloud Manager发行计划中创建新的索引定义，以作为自定义代码库的一部分。 有关更多信息，请参阅[部署到AEM as a Cloud Service文档](/help/implementing/deploying/overview.md)。

### 准备新的索引定义 {#preparing-the-new-index-definition}

>[!NOTE]
>
>如果自定义现成索引（例如`damAssetLucene-6`），请从&#x200B;*Cloud Service环境*&#x200B;复制最新现成索引定义并在顶部添加自定义，这可确保不会无意中删除所需的配置。 例如，`/oak:index/damAssetLucene-6/tika`下的`tika`节点是必需的节点，也应是自定义索引的一部分，并且该节点不存在于Cloud SDK中。

您需要按照以下命名模式准备包含实际索引定义的新索引定义包：

`<indexName>[-<productVersion>]-custom-<customVersion>`

然后，该值需要在`ui.apps/src/main/content/jcr_root`下。 目前不支持子根文件夹。

上述示例中的包将作为`com.adobe.granite:new-index-content:zip:1.0.0-SNAPSHOT`构建。

>[!NOTE]
>
>包含索引定义的任何内容包都应在位于`/META-INF/vault/properties.xml`的内容包的属性文件中设置以下属性：
>
>`noIntermediateSaves=true`

### 部署索引定义 {#deploying-index-definitions}

>[!NOTE]
>
>Jackrabbit Filevault Maven包插件版本&#x200B;**1.1.0**&#x200B;存在已知问题，该版本不允许将`oak:index`添加到`<packageType>application</packageType>`的模块。 您应该更新到该插件的最新版本。

索引定义现在标记为自定义并已版本化：

* 索引定义本身（例如`/oak:index/ntBaseLucene-custom-1`）

因此，要部署索引，需要通过Git和Cloud Manager部署过程中的`ui.apps`传递索引定义(`/oak:index/definitionname`)。

添加新索引定义后，需要通过Cloud Manager部署新应用程序。 部署后，将启动两个作业，负责将索引定义分别添加（并在需要时合并）到MongoDB和Azure区段存储，以供创作和发布。 在蓝绿色切换开始之前，正在使用新索引定义重新索引基础存储库。

>[!TIP]
>
>有关AEM as a Cloud Service所需的包结构的更多详细信息，请参阅文档[AEM项目结构。](/help/implementing/developing/introduction/aem-project-content-package-structure.md)

## 使用蓝绿色部署的索引管理 {#index-management-using-blue-green-deployments}

### 什么是索引管理 {#what-is-index-management}

索引管理是关于添加、删除和更改索引。 更改索引的&#x200B;*定义*&#x200B;非常快，但应用更改（通常称为“构建索引”，或者对于现有索引，“重新索引”）需要时间。 它不是瞬间的：必须扫描存储库，才能将数据编入索引。

### 什么是蓝绿色部署 {#what-is-blue-green-deployment}

蓝绿色部署可减少停机时间。 它还允许零停机升级，并提供快速回滚。 应用程序的旧版本（蓝色）与应用程序的新版本（绿色）同时运行。

### 只读和读写区域 {#read-only-and-read-write-areas}

存储库的某些区域（存储库的只读部分）在应用程序的旧（蓝色）和新（绿色）版本中可能不同。 存储库的只读区域通常为“`/app`”和“`/libs`”。 在以下示例中，斜体用于标记只读区域，而粗体用于读写区域。

* **/**
* */apps（只读）*
* **/content**
* */libs（只读）*
* **/oak:index**
* **/oak:index/acme。**
* **/jcr:system**
* **/system**
* **/var**

存储库的读写区域在应用程序的所有版本之间共享，而对于应用程序的每个版本，都有一组特定的`/apps`和`/libs`。

### 无蓝绿色部署的索引管理 {#index-management-without-blue-green-deployment}

在开发期间或使用内部部署安装时，可以在运行时添加、删除或更改索引。 索引一经可用即可使用。 如果某个索引尚未在旧版本的应用程序中使用，则通常会在计划的停机时间内构建该索引。 删除索引或更改现有索引时也会发生同样的情况。 删除索引后，该索引一旦删除就变得不可用。

### 使用蓝绿色部署进行索引管理 {#index-management-with-blue-green-deployment}

使用蓝绿色部署时，不会出现停机。 但是，对于索引管理，这要求索引仅供某些版本的应用程序使用。 例如，在应用程序版本2中添加索引时，您不希望该索引被应用程序版本1使用。 而删除索引的情况则相反：在版本1中，仍需要在版本2中删除索引。 在更改索引定义时，我们希望旧版本的索引仅用于版本1，新版本的索引仅用于版本2。

下表显示了五个索引定义：索引`cqPageLucene`在两个版本中都使用，而索引`damAssetLucene-custom-1`仅在版本2中使用。

>[!NOTE]
>
>`<indexName>-custom-<customerVersionNumber>` 需要将AEM标记为现有索引的替换Cloud Service，才能将其标记为现有索引的替换。

| 索引 | 现成索引 | 在版本1中使用 | 在版本2中使用 |
|---|---|---|---|
| /oak:index/damAssetLucene | 是 | 是 | 否 |
| /oak:index/damAssetLucene-custom-1 | 是（自定义） | 否 | 是 |
| /oak:index/acme.product-custom-1 | 否 | 是 | 否 |
| /oak:index/acme.product-custom-2 | 否 | 否 | 是 |
| /oak:index/cqPageLucene | 是 | 是 | 是 |

每次更改索引时，版本号都会递增。 为避免自定义索引名称与产品本身的索引名称发生冲突，自定义索引以及对现成索引的更改必须以`-custom-<number>`结尾。

### 对现成索引的更改 {#changes-to-out-of-the-box-indexes}

一旦Adobe更改了现成索引（如“damAssetLucene”或“cqPageLucene”），将创建名为`damAssetLucene-2`或`cqPageLucene-2`的新索引，或者，如果已自定义该索引，则自定义索引定义将与现成索引中的更改合并，如下所示。 更改的合并会自动进行。 这意味着如果现成的索引发生更改，您无需执行任何操作。 但是，以后可以再次自定义索引。

| 索引 | 现成索引 | 在版本2中使用 | 在版本3中使用 |
|---|---|---|---|
| /oak:index/damAssetLucene-custom-1 | 是（自定义） | 是 | 否 |
| /oak:index/damAssetLucene-2-custom-1 | 是（自动从damAssetLucene-custom-1和damAssetLucene-2合并） | 否 | 是 |
| /oak:index/cqPageLucene | 是 | 是 | 否 |
| /oak:index/cqPageLucene-2 | 是 | 否 | 是 |

### 当前限制 {#current-limitations}

目前，仅`lucene`类型的索引支持索引管理。

### 添加索引 {#adding-an-index}

要添加名为`/oak:index/acme.product-custom-1`的索引以在新版应用程序及更高版本中使用，必须按如下方式配置该索引：

`acme.product-1-custom-1`

在索引名称前面加上一个自定义标识符，后跟一个圆点(**`.`**)，即可实现此目的。 标识符的长度应介于2到5个字符之间。

如上所述，这可确保索引仅供新版本的应用程序使用。

### 更改索引 {#changing-an-index}

更改现有索引时，需要使用更改的索引定义添加新索引。 例如，请考虑更改现有索引`/oak:index/acme.product-custom-1`。 旧索引存储在`/oak:index/acme.product-custom-1`下，新索引存储在`/oak:index/acme.product-custom-2`下。

应用程序的旧版本使用以下配置：

`/oak:index/acme.product-custom-1`

新版本的应用程序使用以下（已更改）配置：

`/oak:index/acme.product-custom-2`

>[!NOTE]
>
>作为Cloud Service的AEM上的索引定义可能与本地开发实例上的索引定义不完全匹配。 开发实例没有Tika配置，而AEM as a Cloud Service实例则有一个。 如果您使用Tika配置自定义索引，请保留Tika配置。

### 撤消更改 {#undoing-a-change}

有时，需要恢复索引定义中的更改。 原因可能是错误地做出了改变，或者不再需要改变。 例如，索引定义`damAssetLucene-8-custom-3`是错误创建的，并且已经部署。 因此，您可能希望还原到之前的索引定义`damAssetLucene-8-custom-2`。 为此，您需要添加一个名为`damAssetLucene-8-custom-4`的新索引，其中包含前一个索引`damAssetLucene-8-custom-2`的定义。

### 删除索引 {#removing-an-index}

以下内容仅适用于自定义索引。 不能删除产品索引，因为AEM使用了这些索引。

如果要在更高版本的应用程序中删除索引，您可以定义一个空索引（一个从未使用过且不包含任何数据的空索引），并使用新名称。 在本例中，您可以将其命名为`/oak:index/acme.product-custom-3`。 这将替换索引`/oak:index/acme.product-custom-2`。 系统删除`/oak:index/acme.product-custom-2`后，还可以删除空索引`/oak:index/acme.product-custom-3`。 此类空索引的示例有：

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

如果不再需要自定义现成索引，则必须复制现成索引定义。 例如，如果您已经部署了`damAssetLucene-8-custom-3`，但不再需要自定义，并且希望切换回默认的`damAssetLucene-8`索引，则必须添加一个包含`damAssetLucene-8`索引定义的索引`damAssetLucene-8-custom-4`。

## 索引优化

Apache Jackrabbit Oak支持灵活的索引配置，以高效处理搜索查询。 索引对于较大的存储库尤其重要。 请确保所有查询都有适当的索引作为备份。 没有合适索引的查询可能会读取数千个节点，这些节点随后将记录为警告。 此类查询应通过分析日志文件来识别，以便优化索引定义。 有关详细信息，请参阅[此页面](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/practices/best-practices-for-queries-and-indexing.html?lang=en#tips-for-creating-efficient-indexes)。

### AEM as aCloud Service上的Lucene全文索引

全文索引`/oak:index/lucene-2`可能会变得非常大，因为它默认为AEM存储库中的所有节点编制索引。  在Adobe计划停用此索引后，自2021年9月起，将不再部署在AEM作为Cloud Service。 因此，它不再用在AEM中的产品端作为Cloud Service，也不应该要求它运行客户代码。 对于AEM作为具有常用Lucene索引的Cloud Service环境，Adobe正在与客户单独合作，以采用协调的方法来弥补此索引的不足，并使用更好、优化的索引。 客户无需执行任何操作，而无需进一步通知Adobe。 AEM as a Cloud Service客户在需要针对此优化采取行动时，Adobe会通知客户。 如果自定义查询需要此索引，则作为临时解决方案，应使用其他名称（例如`/oak:index/acme.lucene-1-custom-1`）创建此索引的副本，如[此处](/help/operations/indexing.md)所述。
默认情况下，此优化不适用于其他AEM环境，这些环境是在内部部署托管的，或由Adobe Managed Services管理的。

## 查询优化

**查询性能**&#x200B;工具允许您同时查看常用和缓慢的JCR查询。 此外，它还能够分析查询并显示各种有关的信息，尤其是当某个索引正在用于此查询时。

与AEM on premise不同，AEM as aCloud Service不再在UI中显示&#x200B;**查询性能**&#x200B;工具。 现在，可通过开发人员控制台（在Cloud Manager中）在&#x200B;**查询**&#x200B;选项卡上使用此功能。
