---
title: 内容搜索与索引
description: 内容搜索与索引
translation-type: tm+mt
source-git-commit: 610615534cb5a798e37d34fadb9a3bf341565526
workflow-type: tm+mt
source-wordcount: '1521'
ht-degree: 2%

---


# 内容搜索与索引 {#indexing}

## AEM中Cloud Service{#changes-in-aem-as-a-cloud-service}的更改

以AEM为Cloud Service,Adobe正在从以AEM实例为中心的模型转变为基于服务的视图，其中n-x AEM容器由云管理器中的CI/CD管道驱动。 必须在部署之前指定索引配置，而不是在单个AEM实例上配置和维护索引。 生产中的配置更改明显违反了CI/CD策略。 索引更改也是如此，因为如果不指定测试并重新编制索引，则可能会影响系统稳定性和性能，然后再将其投入生产。

以下是与AEM 6.5及更早版本相比的主要更改列表:

1. 用户将无权访问单个AEM实例的索引管理器来调试、配置或维护索引。 它仅用于本地开发和预先部署。

1. 用户不会更改单个AEM实例上的索引，也不必再担心一致性检查或重新索引。

1. 通常，在投入生产前会启动索引更改，以避免绕过Cloud Manager CI/CD管道中的质量网关，并且不影响生产中的业务KPI。

1. 在运行时，客户可以使用包括生产中搜索性能在内的所有相关指标，以提供有关搜索和索引主题的整体视图。

1. 客户将能够根据自己的需要设置警报。

1. SRE正在24/7全天候监测系统健康状况，并将根据需要及早采取行动。

1. 索引配置通过部署进行更改。 索引定义更改的配置方式与其他内容更改类似。

1. 在AEM作为Cloud Service的高度上，引入[Blue-Green部署模型](#index-management-using-blue-green-deployments)后，将存在两组索引：一个用于旧版本（蓝色），另一个用于新版本（绿色）。

1. 客户可以在Cloud Manager构建页面上查看索引编制作业是否完成，并在新版本准备就绪后收到通知。

1. 限制：目前，AEM asCloud Service上的索引管理仅支持lucene类型的索引。

<!-- ## Sizing Considerations {#sizing-considerations}

AEM as a Cloud Service comes with a default capacity model to provide sufficient performance for average web applications. This "average" measure relates to the repository size and even more relevant to the indexing size. If we have reasons to believe that we need extended capacity for a specific customer project, an evaluation with SREs and Engineering will take place to determine the required capacity settings.

AS NOTE: the above is internal for now.

-->

## 使用方法 {#how-to-use}

定义索引可以包括以下3种用例：

1. 添加新的客户索引定义
1. 更新现有索引定义。 这实际上意味着添加现有索引定义的新版本
1. 删除冗余或过时的现有索引。

对于以上第1点和第2点，您需要在相应的Cloud Manager发布计划中创建新的索引定义，作为自定义代码库的一部分。 有关详细信息，请参阅[作为Cloud Service文档部署到AEM](/help/implementing/deploying/overview.md)。

### 准备新索引定义{#preparing-the-new-index-definition}

您需要准备一个包含实际索引定义的新索引定义包，遵循以下命名模式：

`<indexName>[-<productVersion>]-custom-<customVersion>`

然后，它需要位于`ui.apps/src/main/content/jcr_root`下。 目前不支持子根文件夹。

<!-- need to review and link info on naming convention from https://wiki.corp.adobe.com/display/WEM/Merging+Customer+and+OOTB+Index+Changes?focusedCommentId=1784917629#comment-1784917629 -->

上述示例中的包构建为`com.adobe.granite:new-index-content:zip:1.0.0-SNAPSHOT`。

### 部署索引定义{#deploying-index-definitions}

>[!NOTE]
>
>Jackrabbit Filevault Maven包插件版本&#x200B;**1.1.0**&#x200B;存在已知问题，它不允许您向`<packageType>application</packageType>`的模块添加`oak:index`。 要解决此问题，请使用版本&#x200B;**1.0.4**。

索引定义现在标记为自定义和版本化：

* 索引定义本身（例如`/oak:index/ntBaseLucene-custom-1`）

因此，要部署索引，需要通过`ui.apps`通过Git和Cloud Manager部署流程提供索引定义(`/oak:index/definitionname`)。

添加新索引定义后，需要通过云管理器部署新应用程序。 部署时，将启动两个作业，负责将索引定义分别添加（并根据需要合并）到MongoDB和Azure区段存储，以便进行创作和发布。 在“蓝绿”切换开始之前，正在使用新索引定义重新索引基础存储库。

>[!TIP]
>
>有关AEM作为Cloud Service所需的包结构的更多详细信息，请参阅文档[AEM项目结构。](/help/implementing/developing/introduction/aem-project-content-package-structure.md)

## 使用蓝绿部署{#index-management-using-blue-green-deployments}的索引管理

### 什么是索引管理{#what-is-index-management}

索引管理是关于添加、删除和更改索引。 更改索引的&#x200B;*定义*&#x200B;很快，但应用更改（通常称为“构建索引”，或对于现有索引，“重新索引”）需要时间。 它不是瞬间发生的：必须扫描存储库，才能索引数据。

### 什么是蓝绿部署{#what-is-blue-green-deployment}

蓝绿部署可减少停机时间。 它还允许零停机时间升级并提供快速回滚。 应用程序的旧版本（蓝色）与应用程序的新版本（绿色）同时运行。

### 只读和读写区域{#read-only-and-read-write-areas}

旧（蓝色）和新（绿色）版本的应用程序中，存储库的某些区域（存储库的只读部分）可以不同。 存储库的只读区域通常为“`/app`”和“`/libs`”。 在以下示例中，斜体用于标记只读区域，而粗体用于读写区域。

* **/**
* */apps（只读）*
* **/content**
* */libs（只读）*
* **/oak:index**
* **/oak:index/acme。**
* **/jcr:system**
* **/system**
* **/var**

存储库的读写区域在所有版本的应用程序之间共享，而对于每个版本的应用程序，都有一组特定的`/apps`和`/libs`。

### 无蓝绿部署的索引管理{#index-management-without-blue-green-deployment}

在开发过程中或在使用内部部署安装时，可以在运行时添加、删除或更改索引。 索引一旦可用，即可使用。 如果应用程序的旧版本中尚未使用索引，则通常在计划停机期间构建索引。 删除索引或更改现有索引时也会发生同样的情况。 删除索引时，一旦删除索引，该索引将变得不可用。

### 蓝绿部署{#index-management-with-blue-green-deployment}的索引管理

蓝绿部署不会停机。 但是，对于索引管理，这要求索引仅用于某些版本的应用程序。 例如，在应用程序版本2中添加索引时，您还不希望该索引被应用程序版本1使用。 相反，删除索引时的情况是：版本1中仍需要在版本2中删除的索引。 更改索引定义时，我们希望旧版本的索引仅用于版本1，新版本的索引仅用于版本2。

下表显示了5个索引定义：索引`cqPageLucene`在两个版本中都使用，而索引`damAssetLucene-custom-1`仅在版本2中使用。

>[!NOTE]
>
>`<indexName>-custom-<customerVersionNumber>` 需要AEM作为Cloud Service来将其标记为现有索引的替换。

| 索引 | 现成索引 | 在版本1中使用 | 在版本2中使用 |
|---|---|---|---|
| /oak:index/damAssetLucene | 是 | 是 | 否 |
| /oak:index/damAssetLucene-custom-1 | 是（自定义） | 否 | 是 |
| /oak:index/acme.product-custom-1 | 否 | 是 | 否 |
| /oak:index/acme.product-custom-2 | 否 | 否 | 是 |
| /oak:index/cqPageLucene | 是 | 是 | 是 |

每次更改索引时版本号都会递增。 为了避免自定义索引名称与产品本身的索引名称发生冲突，自定义索引以及对开箱即用索引的更改必须以`-custom-<number>`结束。

### 对现成索引{#changes-to-out-of-the-box-indexes}的更改

一旦Adobe更改现成索引（如“damAssetLucene”或“cqPageLucene”），将创建名为`damAssetLucene-2`或`cqPageLucene-2`的新索引，或者，如果索引已自定义，则自定义的索引定义将与现成索引中的更改合并，如下所示。 自动合并更改。 这意味着，如果现成的索引发生更改，您无需执行任何操作。 但是，以后可以再次自定义索引。

| 索引 | 现成索引 | 在版本2中使用 | 在版本3中使用 |
|---|---|---|---|
| /oak:index/damAssetLucene-custom-1 | 是（自定义） | 是 | 否 |
| /oak:index/damAssetLucene-2-custom-1 | 是（自动从damAssetLucene-custom-1和damAssetLucene-2合并） | 否 | 是 |
| /oak:index/cqPageLucene | 是 | 是 | 否 |
| /oak:index/cqPageLucene-2 | 是 | 否 | 是 |

### 限制 {#limitations}

目前仅支持类型`lucene`的索引管理。

### 删除索引{#removing-an-index}

如果要在应用程序的更高版本中删除索引，您可以定义一个空索引（一个没有要索引的数据的索引），并使用一个新名称。 例如，您可以将其命名为`/oak:index/acme.product-custom-3`。 这将替换索引`/oak:index/acme.product-custom-2`。 系统删除`/oak:index/acme.product-custom-2`后，还可以删除空索引`/oak:index/acme.product-custom-3`。

### 添加索引{#adding-an-index}

要添加名为“/oak:index/acme.product-custom-1”的索引以用于应用程序的新版本和更高版本，需要按照以下方式配置该索引：

`acme.product-1-custom-1`

这通过在索引名称前预定自定义标识符(后跟点(**`.`**))来实现。 标识符长度应介于2到5个字符之间。

如上所述，这确保索引只被新版本的应用程序使用。

### 更改索引{#changing-an-index}

更改现有索引时，需要使用更改的索引定义添加新索引。 例如，考虑现有索引“/oak:index/acme.product-custom-1”已更改。 旧索引存储在`/oak:index/acme.product-custom-1`下，新索引存储在`/oak:index/acme.product-custom-2`下。

应用程序的旧版本使用以下配置：

`/oak:index/acme.product-custom-1`

新版本的应用程序使用以下（已更改）配置：

`/oak:index/acme.product-custom-2`

### 索引可用性／容错{#index-availability}

建议为极其重要的功能创建重复索引（请注意上述索引的命名规范），因此，在索引损坏或任何此类无法预见的事件下，有一个回退索引可用于响应查询。
