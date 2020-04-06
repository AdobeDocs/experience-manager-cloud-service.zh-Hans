---
title: 内容搜索与索引
description: '内容搜索与索引 '
translation-type: tm+mt
source-git-commit: 99dce041a6d7554785fd43eb82c671643e903f23

---


# 内容搜索与索引 {#indexing}

## AEM作为云服务的更改 {#changes-in-aem-as-a-cloud-service}

将AEM作为云服务，Adobe将从以AEM实例为中心的模型转变为基于服务的视图，该容器由Cloud Manager中的CI/CD管道驱动，具有n-x AEM。 必须在部署之前指定索引配置，而不是在单个AEM实例上配置和维护索引。 生产中的配置更改明显违反了CI/CD策略。 索引更改也是如此，因为如果未指定测试并重新编制索引，则可能会影响系统稳定性和性能，然后再将其投入生产。

以下是与AEM 6.5及更早版本相比的主要更改的列表:

1. 用户将无法再访问单个AEM实例的索引管理器来调试、配置或维护索引。 它仅用于本地开发和预先部署。

1. 用户不会更改单个AEM实例上的索引，也不必再担心一致性检查或重新构建索引。

1. 通常，在投入生产之前会启动索引更改，以避免绕过Cloud Manager CI/CD管道中的质量网关，并且不会影响生产中的业务KPI。

1. 包括生产中搜索性能在内的所有相关指标将在运行时提供给客户，以便提供有关搜索和索引主题的整体视图。

1. 客户将能够根据自己的需求设置警报。

1. SRE正在24/7全天候监测系统健康情况，并将根据需要及早采取行动。

1. 索引配置通过部署进行更改。 索引定义更改的配置方式与其他内容更改类似。

1. 在AEM作为云服务的高层，引入 [Blue-Green部署模型后](#index-management-using-blue-green-deployments) ，将存在两组索引：一组用于旧版本（蓝色），另一组用于新版本（绿色）。

使用的索引版本通过标志使用索引定义中的标志进行配 `useIfExist` 置。 索引只能用于应用程序的一个版本（例如，仅蓝色或绿色），或同时用于两个版本。 使用蓝绿部署的索 [引管理中提供了详细文档](#index-management-using-blue-green-deployments)。

1. 客户可以在Cloud Manager构建页面上查看索引构建作业是否完成，并在新版本可以接收流量时收到通知。

1. 限制：目前，AEM作为云服务的索引管理仅支持lucene类型的索引。

<!-- ## Sizing Considerations {#sizing-considerations}

AEM as a Cloud Service comes with a default capacity model to provide sufficient performance for average web applications. This "average" measure relates to the repository size and even more relevant to the indexing size. If we have reasons to believe that we need extended capacity for a specific customer project, an evaluation with SREs and Engineering will take place to determine the required capacity settings. 

AS NOTE: the above is internal for now.

-->

## 使用方法 {#how-to-use}

定义索引可包括以下3种用例：

1. 添加新的客户索引定义
1. 更新现有索引定义。 这实际上意味着添加现有索引定义的新版本
1. 删除冗余或过时的现有索引。

对于以上第1点和第2点，您需要在相应的Cloud Manager发布计划中创建新的索引定义作为自定义代码库的一部分。 有关详细信息，请参 [阅将Cloud Service部署到AEM文档](/help/implementing/deploying/overview.md)。

### 准备新的索引定义 {#preparing-the-new-index-definition}

您需要准备一个包含实际索引定义的新索引定义包，遵循以下命名模式：

`<indexName>[-<productVersion>]-custom-<customVersion>`

那就得下去 `ui.content/src/main/content/jcr_root`。 目前不支持子根文件夹。

<!-- need to review and link info on naming convention from https://wiki.corp.adobe.com/display/WEM/Merging+Customer+and+OOTB+Index+Changes?focusedCommentId=1784917629#comment-1784917629 -->

上述示例中的包构建为 `com.adobe.granite:new-index-content:zip:1.0.0-SNAPSHOT`。

### 部署索引定义 {#deploying-index-definitions}

索引定义现在标记为自定义和版本化：

* 索引定义本身(例如 `/oak:index/ntBaseLucene-custom-1`)是MUTABLE内容

因此，为了部署索引，索引定义(`/oak:index/definitionname`)应通过可变包提 **交**，通常通 `ui.content` 过Git和Cloud Manager部署过程。

添加新索引定义后，需要通过Cloud Manager部署新应用程序。 在部署时，将启动两个作业，负责将索引定义分别添加（并根据需要合并）到MongoDB和Azure区段存储，以供创作和发布。 在“蓝绿”切换开始之前，正在使用新索引定义重新索引基础存储库。

## 使用蓝绿色部署的索引管理 {#index-management-using-blue-green-deployments}

### 什么是索引管理 {#what-is-index-management}

索引管理是关于添加、删除和更改索引。 更改索 *引的定义很快* ，但应用更改（通常称为“构建索引”，或对于现有索引，“重新索引”）需要时间。 这不是瞬间的：必须扫描存储库才能索引数据。

### 什么是蓝绿色部署 {#what-is-blue-green-deployment}

蓝绿色部署可以减少停机时间。 它还允许零停机升级并提供快速回滚。 应用程序的旧版本（蓝色）与应用程序的新版本（绿色）同时运行。

### 只读和读写区域 {#read-only-and-read-write-areas}

存储库的某些区域（存储库的只读部分）在旧版（蓝色）和新版（绿色）应用程序中可能不同。 存储库的只读区域通常为“`/app`”和“`/libs`”。 在以下示例中，斜体用于标记只读区域，而粗体用于读写区域。

* **/**
* */apps（只读）*
* **/content**
* */libs（只读）*
* **/oak:index**
* **/oak:index/acme**
* **/jcr:system**
* **/系统**
* **/var**

存储库的读写区域在应用程序的所有版本之间共享，而应用程序的每个版本都有一组特定的和 `/apps` 组 `/libs`。

### 无需蓝绿色部署的索引管理 {#index-management-without-blue-green-deployment}

在开发过程中，或在使用内部部署安装时，可以在运行时添加、删除或更改索引。 索引一旦可用，即可使用。 如果应用程序的旧版本中尚未使用索引，则通常在计划停机期间构建索引。 删除索引或更改现有索引时也会出现同样的情况。 删除索引时，一旦删除索引，该索引就变得不可用。

### 蓝绿部署的索引管理 {#index-management-with-blue-green-deployment}

使用蓝绿色部署，不会停机。 但是，对于索引管理，这要求索引仅由某些版本的应用程序使用。 例如，在应用程序版本2中添加索引时，您还不希望应用程序版本1使用该索引。 相反，删除索引时的情况是：版本1中仍需要在版本2中删除的索引。 更改索引定义时，我们希望旧版本的索引仅用于版本1，新版本的索引仅用于版本2。

下表显示了5个索引定义：索引 `cqPageLucene` 在两个版本中都使用，而索引 `damAssetLucene-custom-1` 仅在版本2中使用。


> [!NOTE]
> `<indexName>-custom-<customerVersionNumber>` aem作为云服务需要将其标记为现有索引的替换项。

| 索引 | 现成的索引 | 在版本1中使用 | 在版本2中使用 |
|---|---|---|---|
| /oak:index/damAssetLucene | 是 | 是 | 否 |
| /oak:index/damAssetLucene-custom-1 | 是（自定义） | 否 | 是 |
| /oak:index/acmeProduct-custom-1 | 否 | 是 | 否 |
| /oak:index/acmeProduct-custom-2 | 否 | 否 | 是 |
| /oak:index/cqPageLucene | 是 | 是 | 是 |

每次更改索引时，版本号都会递增。 为避免自定义索引名称与产品本身的索引名称发生冲突，自定义索引以及对开箱即用索引的更改需要以结束 `-custom-<number>`。

### 对现成索引的更改 {#changes-to-out-of-the-box-indexes}

一旦Adobe更改了现成的索引（如“damAssetLucene”或“cqPageLucene”），即会创建名为或的新索引，或者，如果索引已经自定义，则自定义的索引定义将与现成的索引中的更改合并，如下所示。 `damAssetLucene-2``cqPageLucene-2` 合并更改会自动发生。 这意味着，如果现成的索引发生更改，您无需执行任何操作。 但是，以后可以再次自定义索引。

| 索引 | 现成的索引 | 在版本2中使用 | 在版本3中使用 |
|---|---|---|---|
| /oak:index/damAssetLucene-custom-1 | 是（自定义） | 是 | 否 |
| /oak:index/damAssetLucene-2-custom-1 | 是（自动从damAssetLucene-custom-1和damAssetLucene-2合并） | 否 | 是 |
| /oak:index/cqPageLucene | 是 | 是 | 否 |
| /oak:index/cqPageLucene-2 | 是 | 否 | 是 |

### 限制 {#limitations}

目前仅支持类型索引的索引管理 `lucene`。

### 删除索引 {#removing-an-index}

如果要在应用程序的更高版本中删除索引，您可以定义一个空索引（一个没有要索引的数据的索引），并带有一个新名称。 例如，您可以为其命名 `/oak:index/acmeProduct-custom-3`。 这将替换索引 `/oak:index/acmeProduct-custom-2`。 一旦 `/oak:index/acmeProduct-custom-2` 系统删除了空索引，也 `/oak:index/acmeProduct-custom-3` 可以删除空索引。

### 添加索引 {#adding-an-index}

要添加名为“/oak:index/acmeProduct-custom-1”的索引以用于应用程序的新版本和更高版本，需要按照如下方式配置该索引：

`/oak:index/acmeProduct-custom-1`

如上所述，这可确保索引仅由新版本的应用程序使用。

### 更改索引 {#changing-an-index}

当现有索引发生更改时，需要使用更改的索引定义添加新索引。 例如，考虑现有索引“/oak:index/acmeProduct-custom-1”已更改。 旧索引存储在下 `/oak:index/acmeProduct-custom-1`面，新索引存储在下面 `/oak:index/acmeProduct-custom-2`。

应用程序的旧版本使用以下配置：

`/oak:index/acmeProduct-custom-1`

应用程序的新版本使用以下（已更改）配置：

`/oak:index/acmeProduct-custom-2`