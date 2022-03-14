---
title: 上线
description: 了解在代码和内容云就绪后如何执行迁移
exl-id: 10ec0b04-6836-4e26-9d4c-306cf743224e
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1319'
ht-degree: 0%

---

# 上线 {#go-live}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_prep"
>title="上线准备"
>abstract="为确保在AEMas a Cloud Service上顺利、成功地上线，您应当规划代码和内容冻结期、测试迭代、内容增补、性能测试、安全测试等。"

在历程的这一部分中，您将了解在代码和内容准备好移至AEM as a Cloud Service后，如何规划和执行迁移。 此外，您还将了解执行迁移时的最佳实践和已知限制。

## 迄今为止的故事 {#story-so-far}

在历程的前几个阶段中：

* 您学习了如何开始在 [快速入门](/help/journey-migration/getting-started.md) 页面。
* 通过阅读 [准备阶段](/help/journey-migration/readiness.md)
* 熟悉可让代码和内容云随时使用的工具和流程 [实施阶段](/help/journey-migration/implementation.md).

## 目标 {#objective}

在您熟悉历程的前面步骤后，本文档将帮助您了解如何向AEMas a Cloud Service迁移。 您将了解如何执行初始生产迁移以及迁移到AEM as a Cloud Service时应遵循的最佳实践。

## 初始生产迁移 {#initial-migration}

在执行生产迁移之前，请按照 [内容迁移策略和时间表](/help/journey-migration/implementation.md##strategy-timeline) 部分 [实施阶段](/help/journey-migration/implementation.md).

* 根据您在克隆上执行AEMas a Cloud Service阶段迁移期间获得的经验，从生产中启动迁移：
   * 作者 — 作者
   * 发布 — 发布

* 验证已摄取到AEMas a Cloud Service创作层和发布层的内容。
* 指示内容创作团队在摄取完成之前，避免在源和目标上移动内容
* 可以添加、编辑或删除新内容，但避免移动新内容。 这同时适用于源和目标。
* 记录 [所用时间](/help/journey-migration/implementation.md#gathering-data) 以便对将来的增补迁移时间表进行估算，从而实现完整提取和摄取。
* 创建 [迁移计划员](/help/journey-migration/implementation.md#migration-plan) ，用于创作和发布。

## 增量增补 {#top-up}

从生产环境进行初始迁移后，您必须执行增量增补，以确保在云实例上使内容保持最新。 因此，建议您遵循以下最佳实践：

* 收集有关内容量的数据。 例如：每周、两周或一个月。
* 请确保规划增补，以避免超过48小时的内容提取和摄取。 建议进行此设置，以便内容增补将适合周末的时间范围。
* 规划所需的增补数量，并使用这些估计值在上线日期前后进行规划。

## 确定迁移的代码和内容冻结时间表 {#code-content-freeze}

如前所述，您必须计划代码和内容冻结期。 请使用以下问题来帮助您规划冻结期：

* 必须冻结内容创作活动多长时间？
* 我需要让投放团队停止添加新功能多长时间？

要回答第一个问题，您应该考虑在非生产环境中执行试用运行所花费的时间。 要回答第二个问题，您需要添加新功能的团队与重构代码的团队之间密切协作。 目标应该是确保同时向云服务分支添加、测试和部署添加到现有部署的所有代码。 一般而言，这意味着代码冻结量将会较低。

此外，您还需要在计划最终内容增补时计划内容冻结。

## 最佳实践 {#best-practices}

在规划或执行迁移时，您应考虑以下准则：

* 从创作迁移到创作并发布到发布
* 请求可用于以下目的的生产克隆：
   * 捕获存储库统计信息
   * 迁移活动的验证
   * 准备迁移计划
   * 确定内容冻结要求
   * 从生产环境进行迁移时，确定生产环境中的任何升级需求

**内容传输工具最佳实践**

确保上线时，在生产中运行内容迁移，而不是克隆。 一个好方法是 [AZCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) 对于初始迁移，然后频繁（甚至每天）运行增补提取，以提取较小的块，并避免源AEM上的任何长期负载。

执行生产迁移时，应避免从克隆中运行内容传输工具，因为：

* 如果客户要求在增补迁移期间迁移内容版本，则从克隆中执行内容传输工具不会迁移这些版本。 即使克隆经常从实时作者重新创建，每次创建克隆时，内容传输工具将用于计算增量的检查点都将重置。
* 由于克隆无法作为整体刷新，因此必须使用ACL查询包来打包和安装从生产中添加或编辑的内容以克隆。 此方法的问题在于，除非从源实例和克隆中手动删除，否则源实例上所有已删除的内容将永远无法访问克隆。 这会导致在克隆和AEMas a Cloud Service上删除生产上已删除的内容的可能性。

**执行内容迁移时优化AEM源上的负载**

请记住，在提取阶段，AEM源上的负载将会更大。 您应该注意：

* 内容传输工具是使用4 GB JVM堆的外部Java进程
* 非AzCopy版本下载二进制文件，将它们存储在源AEM作者上的临时空间上，使用磁盘I/O，然后上载到Azure容器，该容器占用网络带宽
* [AzCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) 将blob直接从blob存储传输到Azure容器，以节省磁盘I/O和网络带宽。 AzCopy版本仍使用磁盘和网络带宽提取区段存储中的数据并将其上传到Azure容器
* 在摄取阶段期间，内容传输工具流程在系统资源上更轻松，因为它只流式传输日志，而且源实例上的负载不大（就磁盘I/O或网络带宽而言）。

## 已知限制 {#known-limitations}

如果在提取的迁移集中发现以下任何限制，请考虑整个摄取失败：

* 名称长度超过150个字符的JCR节点
* 大于16 MB的JCR节点
* 具有的任何用户/组 `rep:AuthorizableID` 已摄取到AEM  as a Cloud Service
* 如果在迁移的下一次迭代之前，任何已提取和已摄取的资产都移至源或目标上的其他路径中。

## 资产运行状况 {#asset-health}

与摄取上面的部分相比 **不** 失败，原因如下： 但是，强烈建议您在以下情况下采取适当步骤：

* 缺少原始演绎版的任何资产
* 任何缺少的文件夹 `jcr:content` 节点

上述两个项目将在 [最佳实践分析器](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md) 报表。

## 上线核对清单 {#Go-Live-Checklist}

请查看下面介绍的活动列表，以确保您能够顺利、成功地执行迁移：

* 计划代码和内容冻结期。 另请参阅 [迁移的代码和内容冻结时间轴](#code-content-freeze).
* 执行最终内容增补
* 完成测试迭代
* 运行性能和安全测试
* 切换 和在生产实例上执行迁移

如果在执行迁移时需要重新校准任务，您始终可以引用该列表。

## 下一步 {#what-is-next}

了解如何迁移到AEM  as a Cloud Service后，您可以检查 [上线后](/help/journey-migration/post-go-live.md) 页面来确保实例顺利运行。
