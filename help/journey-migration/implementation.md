---
title: 实施阶段
description: 确保您的代码和内容已准备好迁移到云
exl-id: d124f9a5-a754-4ed0-a839-f2968c7c8faa
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '2339'
ht-degree: 10%

---

# 实施阶段 {#implementation-phase}

在此历程的实施阶段，您将探索用于使代码和内容准备好迁移至AEMas a Cloud Service的工具。

## 迄今为止的故事 {#story-so-far}

在历程的前面部分，您已完成 [熟悉AEMas a Cloud Service中的更改](/help/journey-migration/getting-started.md)，并确定您的部署是否准备好通过移动到云 [就绪阶段](/help/journey-migration/readiness.md).

本文接下来提供了有关如何使用Adobe提供的工具以确保您的代码和内容准备好移动到云的建议。

## 目标 {#objective}

本文档旨在：

* 向您介绍Cloud Manager、AEM持续集成和交付框架，该框架用于将代码部署到AEMas a Cloud Service
* 使用内容传输工具快速掌握
* 描述您必须使用的代码重构工具，以便您可以根据AEMas a Cloud Service对代码进行现代化改造

## 使用 Cloud Manager {#using-cloud-manager}

在开始之前，您必须熟悉Cloud Manager，因为它是将代码部署到AEMas a Cloud Service的唯一机制。

Cloud Manager 使组织能够在云中自行管理 AEM。它包含一个持续集成和持续交付 (CI/CD) 框架，使 IT 团队和实施合作伙伴能够在不影响性能或安全性的情况下快速交付自定义或更新。

您可以通过参阅以下资源来熟悉使用Cloud Manager：

* [入门历程](/help/journey-onboarding/overview.md) 了解有关Experience Manageras a Cloud Service入门的自助资源。

* [将 Git 与 Adobe Cloud Manager 集成](/help/implementing/cloud-manager/managing-code/integrating-with-git.md)，了解使用 Single Git 存储库来部署代码的相关信息。

* [Adobe Experience as a Cloud Service 配置](/help/security/ims-support.md#aem-configuration)，了解有关在 Admin Console 中管理产品和用户访问权限的信息。

## 使用Adobe提供的工具为您的内容和代码云做好准备 {#use-tools-to-make-code-and-content-cloud-ready}

向Cloud Service过渡的确切步骤取决于您所购买的系统以及所遵循的软件开发生命周期惯例。

下图显示了此阶段涉及的主要步骤，其中涉及转换代码和内容以用于AEMas a Cloud Service：

![图像](/help/journey-migration/assets/exec-image1.png)

我们将在以下章节中开始详细介绍您必须使用的工具，以便您能够实现这一点。

## 内容迁移 {#content-migration}

要将内容从当前AEM实例迁移到Cloud Service实例，您可以使用Adobe的内容传输工具。

利用此工具，您可以指定要从源 AEM 实例传输到 AEM 云服务实例的所需内容子集。

内容迁移是一个多步骤的过程，它需要在不同的团队之间进行规划、跟踪和协作。

有关该工具的工作方式以及Adobe建议您如何使用的完整详细信息，请参阅 [内容传输工具文档](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md).

## 代码重构 {#code-refactor}

### 为开发设置 {#set-up-for-development}

现在应该开始重构现有功能以与Cloud Service兼容。

首先，查看详细说明基本工具的文档，然后开始重构您的代码：


* 在规划期间，最好是列出必须重构才能与AEMas a Cloud Service兼容的区域。 您可以查看 [开发准则](/help/implementing/developing/introduction/development-guidelines.md) 有关如何重构和优化代码以进行Cloud Service的详细信息。
* 详细了解如何 [管理配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/configurations.html?lang=en#what-is-a-configuration) 在AEMas a Cloud Service中。
* 了解如何通过下载 [AEMAS A CLOUD SERVICESDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en)
* 最后，请熟悉 [AEMas a Cloud ServiceJava API](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html).

此外，您还可以：

* 观看此视频，了解如何本地安装Dispatcher SDK：

  >[!VIDEO](https://video.tv.adobe.com/v/30601)

* 观看此视频，了解如何配置Dispatcher SDK：

  >[!VIDEO](https://video.tv.adobe.com/v/30602)

### 思维方式的改变 {#a-change-in-mindset}

在AEMas a Cloud Service中开发和运行代码需要改变思维方式。 需要注意的是，代码必须是可复原的，尤其是在实例可能随时停止时。在云服务中运行的代码必须意识到它始终在群集中运行这一事实。这意味着始终会有多个实例在运行。

AEM Maven项目需要进行某些更改才能与云兼容。 AEMas a Cloud Service需要将 *内容* 和 *代码* 部署到不同的包中，以部署到AEM中：

* `/apps` 和 `/libs` 视为AEM的不可变区域，因为AEM启动后（即在运行时）无法对其进行更改。 这包括创建、更新或删除操作。 运行时对不可改变区域所做的任何更改尝试都将失败。

* 存储库中的其他所有内容(例如， `/content` ， `/conf` ， `/var` ， `/home` ， `/etc` ， `/oak:index` ， `/system` ， `/tmp`)都是可变区域，这意味着可在运行时更改这些区域。

欲了解更多信息，请参阅 [推荐的包结构](/help/implementing/developing/introduction/aem-project-content-package-structure.md#recommended-package-structure) 文档。


### 云迁移工具 {#cloud-migration-tools}

Adobe提供了多种工具来帮助加速某些代码重构任务。 了解这些工具及其解决的问题将降低迁移的复杂性和时间。

* [资产工作流迁移](/help/journey-migration/moving-to-aem-assets/asset-workflow-migration-tool.md)，用于自动迁移资产处理工作流的工具
* [Dispatcher转换器](/help/journey-migration/refactoring-tools/dispatcher-transformation-utility-tools.md)，该工具可将您现有的Dispatcher配置转换为可供AEMas a Cloud Service使用的格式。
* [存储库现代化器](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/moving/refactoring-tools/repo-modernizer.html?lang=en)，该工具将AEM多模式项目作为输入并将其转换为AEMas a Cloud Service项目
* [索引转换器](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/moving/refactoring-tools/index-converter.html?lang=en)，此工具可将索引转换为与AEMas a Cloud Service兼容的表单
* [现代化工具](/help/journey-migration/refactoring-tools/aem-modernization-tools.md)，这是一套实用程序，可用于将旧版AEM功能转换为AEMas a Cloud Service的现代化且受支持的功能。

AEM as a Cloud Service设置本地开发环境后，请查阅 [文档](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md).

### 计划代码冻结 {#schedule-a-code-freeze}

要管理活动AEM上正在进行的代码开发以及过渡历程中的代码重构任务，Adobe建议在完成Maven项目重组以与AEMas a Cloud Service兼容之前，设置一个代码冻结期。

项目重组完成后，您可以基于这个新结构继续新的代码开发。 这减少了在代码部署和测试期间出现的Cloud Manager管道故障。

>[!NOTE]
>内容传输和代码重构任务不必按顺序完成。 这些任务可以相互独立地完成。但是，需要使用正确的项目结构来确保内容在云服务环境中成功呈现。

## 代码部署和测试的最佳实践 {#best-practices}

Cloud Manager管道支持执行针对暂存环境运行的测试。

遵循以下文档中有关代码质量测试的最佳实践：

* [代码质量测试](/help/implementing/cloud-manager/code-quality-testing.md)，该文档描述了编写测试脚本的过程，并解释了建议覆盖率至少为50%的概念。
* [了解自定义代码质量规则](/help/implementing/cloud-manager/custom-code-quality-rules.md) 该文档旨在描述Cloud Manager根据AEM Engineering的最佳实践创建的自定义代码质量规则。

## 准备上线 {#preparing-for-go-live}

准备源系统以进行迁移涉及系统和AEM管理员级别任务。 首先，通过检查 [修订清理](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html) 和 [数据存储垃圾收集](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/data-store-garbage-collection.html) 任务状态。 如果您正在运行AEM版本6.3（因为内容传输工具与版本6.3及更高版本兼容），建议先执行离线压缩，然后再执行数据存储垃圾收集。

[数据一致性检查](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/consistency-check.html) 建议在所有AEM版本中使用，以确保内容存储库处于可启动迁移活动的良好状态。

需要系统管理员级别的访问权限才能安装和配置 [AZCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md)

此外，还建议您查看任何未使用的资产、页面、AEM项目、用户和组，以节省迁移时间。 请参阅 [内容存储库运行状况](#repository-health) 部分。

### 内容存储库运行状况 {#repository-health}

访问一次 [生产克隆](#proof-of-migration) 已建立，继续检查存储库的健康状况。 如上一节中所述，目标是在开始迁移之前清理并压缩源上的存储库。 此步骤可能会节省大量时间，否则，在迁移开始后，将花费大量时间对问题进行故障诊断。

| 操作项 | 主要要点 |
|---------|----------|
| 用户、组和权限 | 您需要了解成员资格相关的用户、组的数量和复杂性。 在迁移之前，寻找机会清理源中所有未使用的用户和组。 |
| 未完成资产处理 | 尝试在开始迁移之前完成源系统中的资源处理，以避免迁移后AEMas a Cloud Service中潜在的问题。 |
| 内容运行状况 | 建议在开始迁移之前查询并清除不良内容。 例如，查找没有原始演绎版或停滞在工作流处理中的资产或页面。 另请参阅 [资产运行状况](#asset-health). |

## 正在收集数据 {#gathering-data}

>[!NOTE]
> 此 [内容迁移策略和时间表](#content-strategy-and-timeline) 部分进一步详细说明了如何推断收集的数据和创建迁移计划。

收集数据可以帮助您规划迁移活动和相关任务。 提取和摄取时间特别有用，因为数据点可以与迁移集的特定大小相关联。 因此，可以推断这些数据点来制定计划：

* 花费的总时间 [提取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md)
* 花费的总时间 [摄取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md)
* 增补花费的总时间 [提取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process)
* 增补花费的总时间 [摄取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process)


<!-- Alexandru: hiding this for now

One more important datapoint is the amount of time it takes to complete the [user mapping](/help/journey-migration/content-transfer-tool/user-mapping-tool/overview-user-mapping-tool.md), if this is coupled with the content migration. You can take this data point into consideration for more realistic estimates, because it is added to the overall extraction timeline and it may not be required to run it during top-ups.

-->

这些数据点也可以帮助您 [建立KPI](/help/journey-migration/readiness.md#establish-kpis) 和其他迁移相关的任务。

### 迁移计划 {#migration-plan}

根据您收集的数据点（请参阅上文），您可以创建可集成到宏项目计划中的迁移计划。 此步骤将使所有关键利益相关者能够围绕迁移活动进行可视化和规划。

下表说明了典型的迁移计划：

| 迁移迭代 | 开始日期 | 估计结束日期 | 依赖项 | 估计持续时间（以天为单位） | 其他详细信息/措施项 |
|---|---|---|---|---|---|
| PRDCLONE-AUTHOR-INITIAL-USRMAP-CSSTAGE-AUTHOR |   |   |   |   |   |
| PRDCLONE-PUBLISH-TOP-UP-CSSTAGE-AUTHOR |   |   |   |   |   |

如上表所示，遵循特定命名格式标识迁移迭代很有帮助，例如： **PRDCLONE** 对于源AEM环境， **创作/发布** 对于AEMas a Cloud Service环境， **CSSTAGE-AUTHOR** (对于AEMas a Cloud Service实例，等等)。

一些影响您的迁移计划的重要详细信息：

**所需的提取总数**

* 特定环境中的创作提取和发布提取被视为两个并行提取，因为它们彼此独立。
* 基于特定时间段内存储库增长的增补提取次数。

**所需的引入总数**

* 将此项目捕获到计划中很重要，因为可以将提取的集摄取到多个Cloud Service环境中。
* 增补摄取的次数。
* 将内容从源作者迁移到Cloud Service Author实例，以及从源发布迁移到Cloud Service发布是避免将所有作者内容摄取到Cloud Service发布的最佳实践。

### 迁移跟踪器 {#migration-tracker}

您可以使用迁移跟踪器记下初始运行和增补运行的时间。 这些数据点将帮助您在最终充值之前制定现实的内容冻结要求。

该跟踪器还将帮助您：

* 确定需要调整计划或上线时间线的计划员的任何偏差
* 提供可用于所有必要通信的现实状态
* 规划初始或未来的增补迁移

下表说明了一个功能迁移跟踪器：

| 源（环境/实例/URL） | 目标（环境/实例/URL） | 迁移集名称、类型（初始或增补） | 迁移集大小(MB) | 用户映射（是/否） | 提取持续时间（开始、结束、所用时间） | 摄取持续时间（开始、结束、所用时间） | 问题/解决方案/详细信息 |
|---|---|---|---|---|---|---|---|
|   |   |   |   |   |   |   |   |

## 内容迁移策略和时间表 {#content-strategyand-timeline}

以下部分显示了可用于制定内容迁移策略和时间线的重要步骤和相关任务。

![图像](/help/journey-migration/assets/content-migration2.png)

### 设备 {#fitment}

* 执行修订清理、数据存储垃圾收集和数据一致性检查。 另请参阅 [准备上线](#preparing-for-go-live)
* [收集统计数据](#gathering-data) 关于AEM源资料库：
   * 区段存储大小
   * 索引存储大小
   * 页数
   * 资源数
   * 用户和组的数量
* 了解是否在AEM源上启用了以下功能(AEMas a Cloud Service中也要求这样做)：
   * 智能标记
   * 相似性搜索
   * 搜索包含Word和PDF文档中的文本
* 收集Best Practice Analyser [报告](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md)
* 将导入到 [Cloud Acceleration Manager](/help/journey-migration/cloud-acceleration-manager/introduction/overview-cam.md)
   * 查看自分析建议，以确保AEMas a Cloud Service可以处理存储需求。
* 在继续迁移计划之前，请为任何说明创建Adobe支持工单。

### 迁移证明 {#proof-of-migration}

* 请求满足以下条件的生产克隆：
   * 在同一网络区域中
   * 将提供用户和组等生产内容
   * 克隆创作和发布 — 群集或发布场中每个节点一个
* 选择已迁移内容的子集，以便：
   * 它是所有可用内容类型的组合
   * 包含所有用户和组
* 包括25%的内容或高达1 TB的内容（以较小者为准）。
* 至少执行一个完整的和 [增补](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) 从生产克隆迁移到AEMas a Cloud Service非生产环境
* 解决任何潜在问题，例如：
   * AEM源上的磁盘空间
   * AEM源和AEMas a Cloud Service之间的连接
   * 任何 [摄取相关限制](go-live.md#known-limitations).
* 记录所用时间 [提取和引入](#gathering-data)：
   * 了解每周添加的内容量
   * 根据迁移证明推断时间，以创建 [迁移计划](#migration-plan).

## 后续内容 {#what-is-next}

在您充分了解如何评估您的AEM安装是否已准备好迁移到云后，就像我们了解如何使用所需的工具使其做好准备一样，您是时候迁移到 [上线阶段](/help/journey-migration/go-live.md).
