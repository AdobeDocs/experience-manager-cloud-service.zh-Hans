---
title: 实施阶段
description: 确保您的代码和内容已准备好迁移到云
exl-id: d124f9a5-a754-4ed0-a839-f2968c7c8faa
source-git-commit: 13cb8ae059f0a77e517d2e64eae96a08f88ac075
workflow-type: tm+mt
source-wordcount: '2416'
ht-degree: 9%

---

# 实施阶段 {#implementation-phase}

在历程的实施阶段，您将探索一些工具，通过这些工具，您可以准备将代码和内容移到AEM as a Cloud Service。

## 迄今为止的故事 {#story-so-far}

在历程的前几个阶段，你经历了 [熟悉AEMas a Cloud Service中的更改](/help/journey-migration/getting-started.md)，以及确定您的部署是否已准备就绪，可以通过 [就绪阶段](/help/journey-migration/readiness.md).

本文将继续提供有关如何使用Adobe提供的工具的建议，以确保您的代码和内容已准备好移至云。

## 目标 {#objective}

本文档旨在：

* 向您介绍用于将代码部署到AEMas a Cloud Service的Cloud Manager、AEM连续集成和交付框架
* 使用内容传输工具快速了解相关信息
* 介绍为使AEM as a Cloud Service的代码符合现代化要求而必须使用的代码重构工具

## 使用 Cloud Manager {#using-cloud-manager}

在开始之前，您必须熟悉Cloud Manager，因为它是将代码部署到AEMas a Cloud Service的唯一机制。

Cloud Manager 使组织能够在云中自行管理 AEM。它包含一个持续集成和持续交付 (CI/CD) 框架，使 IT 团队和实施合作伙伴能够在不影响性能或安全性的情况下快速交付自定义或更新。

您可以通过咨询以下资源来熟悉Cloud Manager的使用：

* [入门历程](/help/journey-onboarding/overview.md) 了解有关Experience Manageras a Cloud Service入门的自助资源。

* [将 Git 与 Adobe Cloud Manager 集成](/help/implementing/cloud-manager/managing-code/integrating-with-git.md)，了解使用 Single Git 存储库来部署代码的相关信息。

* [Adobe Experience as a Cloud Service 配置](/help/security/ims-support.md#aem-configuration)，了解有关在 Admin Console 中管理产品和用户访问权限的信息。

## 使用Adobe提供的工具使内容和代码云就绪 {#use-tools-to-make-code-and-content-cloud-ready}

您过渡到Cloud Service的确切步骤取决于您购买的系统以及您遵循的软件开发生命周期惯例。

下图显示了该阶段涉及转换代码和内容以与AEMas a Cloud Service一起使用的主要步骤：

![图像](/help/journey-migration/assets/exec-image1.png)

我们将在以下章节中开始详细介绍为实现此目标需要使用的工具。

## 内容迁移 {#content-migration}

要将内容从当前AEM实例迁移到Cloud Service实例，您可以使用Adobe的内容传输工具。

利用此工具，您可以指定要从源 AEM 实例传输到 AEM 云服务实例的所需内容子集。

内容迁移是一个多步流程，需要不同团队之间进行规划、跟踪和协作。

有关该工具的工作方式以及我们建议您如何使用该工具的完整详细信息，请参阅 [内容传输工具文档](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md).

## 代码重构 {#code-refactor}

### 设置以进行开发 {#set-up-for-development}

现在该开始重构现有功能以与Cloud Services兼容。

为此，您需要查看文档，其中详细介绍了开始重构代码所需的基本工具：


* 在规划期间，最好列出必须重构才能与AEMas a Cloud Service兼容的区域列表。 您可以查看 [开发准则](/help/implementing/developing/introduction/development-guidelines.md) 有关如何重构和优化代码以进行Cloud Service的更多详细信息。
* 了解如何 [管理配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/configurations.html?lang=en#what-is-a-configuration) 在AEMas a Cloud Service中。
* 了解如何通过下载 [AEMas a Cloud ServiceSDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en)
* 最后，请熟悉 [AEMas a Cloud ServiceJava API](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html).

此外，您还可以：

* 请观看此视频，了解如何在本地安装Dispatcher SDK:

   >[!VIDEO](https://video.tv.adobe.com/v/30601)

* 观看此视频，了解如何配置Dispatcher SDK:

   >[!VIDEO](https://video.tv.adobe.com/v/30602)

### 心态的改变 {#a-change-in-mindset}

在AEMas a Cloud Service中开发和运行代码需要改变思维方式。 需要注意的是，代码必须是可复原的，尤其是在实例可能随时停止时。在云服务中运行的代码必须意识到它始终在群集中运行这一事实。这意味着始终会有多个实例在运行。

AEM Maven项目需要进行某些更改才能与云兼容。 AEMas a Cloud Service要求将 *内容* 和 *代码* 到要部署到AEM的不同包中：

* `/apps` 和 `/libs` 被视为AEM的不可变区域，因为AEM启动后（即在运行时）无法对其进行更改。 这包括创建、更新或删除操作。 运行时对不可改变区域所做的任何更改尝试都将失败。

* 存储库中的所有其他内容(例如， `/content` , `/conf` , `/var` , `/home` , `/etc` , `/oak:index` , `/system` , `/tmp`)是所有可变区域，这意味着可在运行时更改它们。

您可以通过咨询 [推荐的包结构](/help/implementing/developing/introduction/aem-project-content-package-structure.md#recommended-package-structure) 文档。


### 云迁移工具 {#cloud-migration-tools}

Adobe提供了多个工具，可帮助加速某些代码重构任务。 了解这些工具以及它们所解决的问题将减少迁移的复杂性和时间。

* [资产工作流迁移](/help/journey-migration/moving-to-aem-assets/asset-workflow-migration-tool.md)，一种用于自动迁移资产处理工作流的工具
* [Dispatcher Converter](/help/journey-migration/refactoring-tools/dispatcher-transformation-utility-tools.md)，该工具可将您现有的Dispatcher配置转换为可准备用于AEMas a Cloud Service的格式。
* [Repository Modernizer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/moving/refactoring-tools/repo-modernizer.html?lang=en)，一种工具，可将AEM多模项目作为输入，并将其转换为AEMas a Cloud Service项目
* [索引转换器](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/moving/refactoring-tools/index-converter.html?lang=en)，可将索引转换为与AEM as a Cloud Service兼容的表单的工具
* [现代化工具](/help/journey-migration/refactoring-tools/aem-modernization-tools.md)，一套实用程序，可用于将旧版AEM功能转换为AEM as a Cloud Service的现代和支持功能。

设置本地开发环境后，请咨询 [文档](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md).

### 计划代码冻结 {#schedule-a-code-freeze}

要管理活动AEM上正在进行的代码开发以及过渡历程中的代码重构任务，我们建议您安排一个代码冻结期，直到您完成Maven项目重组以与AEMas a Cloud Service兼容为止。

项目重组完成后，您可以基于此新结构继续新的代码开发。 这可减少代码部署和测试期间Cloud Manager管道故障。

>[!NOTE]
>内容传输和代码重构任务不必按顺序完成。 这些任务可以相互独立地完成。但是，需要使用正确的项目结构来确保内容在云服务环境中成功呈现。

## 代码部署和测试的最佳实践 {#best-practices}

Cloud Manager管道支持执行针对暂存环境运行的测试。

请遵循以下文档中有关代码质量测试的最佳实践：

* [代码质量测试](/help/implementing/cloud-manager/code-quality-testing.md)，该文档描述编写测试脚本的过程并说明建议覆盖率至少为50%的概念。
* [了解自定义代码质量规则](/help/implementing/cloud-manager/custom-code-quality-rules.md) 它旨在描述由Cloud Manager根据AEM Engineering中的最佳实践创建的自定义代码质量规则。

## 为上线做准备 {#preparing-for-go-live}

准备源系统以进行迁移涉及系统和AEM管理员级别的任务。 您可以首先通过检查 [修订清理](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html) 和 [数据存储垃圾收集](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/data-store-garbage-collection.html) 任务状态。 如果您运行的是AEM 6.3版（因为内容传输工具从6.3版开始兼容），建议先执行离线压缩，然后再执行数据存储垃圾收集。

[数据一致性检查](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/consistency-check.html) 建议在所有AEM版本中使用，以确保内容存储库处于良好状态以启动迁移活动。

安装和配置需要系统管理员级别的访问权限 [AZCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md)

此外，还建议您查看任何未使用的资产、页面、AEM项目、用户和组，以节省迁移时间。 请参阅 [内容存储库运行状况](#repository-health) 中。

### 内容存储库运行状况 {#repository-health}

访问 [生产克隆](#proof-of-migration) 已建立，可继续检查存储库的运行状况。 如上节所述，目标是在开始迁移之前清理并压缩源上的存储库。 此步骤可能会节省大量时间，否则，在迁移开始后，将会花费大量时间对问题进行故障诊断。

| 操作项 | 主要优点 |
|---------|----------|
| 用户、组和权限 | 您需要了解用户数量、组以及成员资格的复杂性。 寻找在迁移前清理源中任何未使用的用户和组的机会。 |
| 资产处理未完成 | 在开始迁移之前，请尝试在源系统中完成资产处理，以避免在AEMas a Cloud Service迁移后出现潜在问题。 |
| 内容运行状况 | 建议在开始迁移之前查询错误内容并将其清除。 例如，查找没有原始演绎版或工作流处理中卡住的资产或页面。 另请参阅 [资产运行状况](#asset-health). |

## 收集数据 {#gathering-data}

>[!NOTE]
> 的 [内容迁移策略和时间表](#content-strategy-and-timeline) 部分进一步详细说明如何推断收集的数据并创建迁移计划。

收集数据可以帮助您规划迁移活动和相关任务。 提取和摄取时间特别有用，因为数据点可以与迁移集的特定大小相关联。 因此，可以推断这些数据点以制定计划：

* 所用总时间 [提取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md)
* 所用总时间 [摄取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md)
* 增补所花费的总时间 [提取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process)
* 增补所花费的总时间 [摄取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process)

一个更重要的数据点是完成 [用户映射](/help/journey-migration/content-transfer-tool/user-mapping-tool/overview-user-mapping-tool.md)，如果这与内容迁移相结合。 您可以考虑此数据点以进行更实际的估计，因为它将被添加到整体提取时间轴中，并且可能不需要在增补期间运行它。

这些数据点还可以帮助您 [建立KPI](/help/journey-migration/readiness.md#establish-kpis) 和其他与迁移相关的任务。

### 迁移计划 {#migration-plan}

根据您收集的数据点（请参阅上文），您可以创建可集成到宏项目计划中的迁移计划。 此步骤将允许所有关键利益相关方可视化并围绕迁移活动进行规划。

下表说明了典型的迁移计划：

| 迁移迭代 | 开始日期 | 预计结束日期 | 依赖项 | 预计持续时间（以天为单位） | 其他详细信息/操作项 |
|---|---|---|---|---|---|
| PRDCLONE-AUTHOR-INITIAL-USRMAP-CSSTAGE-AUTHOR |  |  |  |  |  |
| PRDCLONE-PUBLISH-TOPUP-CSSTAGE-AUTHOR |  |  |  |  |  |

如上表所示，遵循特定命名格式来标识迁移小版本非常有用，例如： **PRDCLONE** 对于源AEM环境， **创作/发布** 对于AEMas a Cloud Service环境， **CSSTAGE-AUTHOR** (例如AEMas a Cloud Service实例等)。

一些影响迁移计划的重要详细信息：

**所需提取的总数**

* 特定环境中的作者提取和发布提取被视为两个并行提取，因为它们彼此独立。
* 根据特定时间段内存储库增长情况提取的增补数量。

**所需的摄取总数**

* 务必将此项目捕获到计划中，因为提取的集可以摄取到多个Cloud Service环境中。
* 增补摄取的次数。
* 将内容从源作者迁移到云服务作者实例和从源发布迁移到Cloud Service发布是避免将所有创作内容摄取到Cloud Service发布的最佳实践。

### 迁移跟踪器 {#migration-tracker}

您可以使用迁移跟踪器记下初始运行和增补运行的时间。 这些数据点可帮助您在最终增补之前制定实际的内容冻结要求。

该跟踪器还将帮助您：

* 确定计划员中需要调整计划或上线时间表的任何偏差
* 提供可用于所有必要通信的实际状态
* 规划初始或将来的增补迁移

下表说明了一个功能迁移跟踪器：

| 源（环境/实例/ URL） | 目标（环境/实例/ URL） | 迁移集名称、类型（初始或增补） | 迁移集大小(MB) | 用户映射（是/否） | 提取持续时间（开始、结束、所用时间） | 摄取持续时间（开始、结束、所用时间） | 问题/解决方案/详细信息 |
|---|---|---|---|---|---|---|---|
|  |  |  |  |  |  |  |  |

## 内容迁移策略和时间表 {#content-strategyand-timeline}

以下部分显示了可用于制定内容迁移策略和时间轴的重要步骤和相关任务。

![图像](/help/journey-migration/assets/content-migration2.png)

### 装配 {#fitment}

* 执行修订清理、数据存储垃圾收集和数据一致性检查。 另请参阅 [为上线做准备](#preparing-for-go-live)
* [收集统计资料](#gathering-data) 关于AEM源存储库：
   * 区段存储大小
   * 索引存储大小
   * 页数
   * 资产数量
   * 用户和组数量
* 了解是否在AEM源上启用了以下功能(AEMas a Cloud Service中也需要此功能):
   * 智能标记
   * 相似性搜索
   * 搜索包含Word和PDF文档中的文本
* 收集最佳实践分析器 [报告](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md)
* 导入到 [Cloud Acceleration Manager](/help/journey-migration/cloud-acceleration-manager/introduction/overview-cam.md)
   * 查看自我分析建议，以确保AEMas a Cloud Service能够满足存储要求。
* 在继续执行迁移计划之前，请创建Adobe支持票证以获取任何说明。

### 迁移证明 {#proof-of-migration}

* 请求生产克隆：
   * 位于同一网络区域
   * 将提供生产内容，如用户和组
   * 克隆创作和发布 — 群集或发布场中每个节点一个
* 选择要迁移的内容的子集，以便：
   * 它包含所有可用内容类型
   * 包含所有用户和组（以防万一） [用户映射](/help/journey-migration/content-transfer-tool/user-mapping-tool/overview-user-mapping-tool.md) 必需
* 包括25%的内容或最多1 TB的内容（以较少者为准）。
* 至少执行一个完整和 [增补](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) 从生产克隆迁移到AEMas a Cloud Service非生产环境
* 解决任何潜在问题，例如：
   * AEM源上的磁盘空间
   * AEM源与AEMas a Cloud Service之间的连接
   * 任意 [摄取相关限制](go-live.md#known-limitations).
* 记录所用的时间 [提取和摄取](#gathering-data):
   * 了解每周添加的内容量
   * 根据迁移证明推断测量的时间，以创建 [迁移计划](#migration-plan).

## 下一步 {#what-is-next}

在您完全了解如何评估您的AEM安装是否已准备好移入云后（在我们了解如何使用所需工具做好准备时），您便可以转到 [上线阶段](/help/journey-migration/go-live.md).
