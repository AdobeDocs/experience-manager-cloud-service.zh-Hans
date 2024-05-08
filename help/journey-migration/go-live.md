---
title: 上线
description: 了解在代码和内容准备就绪后，如何执行迁移
exl-id: 10ec0b04-6836-4e26-9d4c-306cf743224e
source-git-commit: 4a03e2fe3519fd9e0d8d646526ea6c9cc6637f52
workflow-type: tm+mt
source-wordcount: '1239'
ht-degree: 3%

---

# 上线 {#go-live}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_prep"
>title="上线准备"
>abstract="为确保 AEM as a Cloud Service 顺利上线，您应该规划代码和内容冻结期、测试迭代、内容增补、性能测试、安全测试等。"

在此历程的这一可选部分中，您将了解在代码和内容准备好移至AEMas a Cloud Service后，如何规划和执行迁移。 此外，您还可以了解执行迁移时的最佳实践和已知限制。

## 迄今为止的故事 {#story-so-far}

在历程的前几个阶段中：

* 您已在中了解如何开始迁移到AEMas a Cloud Service [快速入门](/help/journey-migration/getting-started.md) 页面。
* 通过阅读 [就绪阶段](/help/journey-migration/readiness.md)
* 熟悉各种工具和流程，通过这些工具和流程，您可以使代码和内容云可以使用 [实施阶段](/help/journey-migration/implementation.md).

## 目标 {#objective}

本文档可帮助您了解在熟悉历程的前几个步骤后，如何执行向AEMas a Cloud Service的迁移。 您将了解如何执行初始生产迁移，以及迁移到AEMas a Cloud Service时要遵循的最佳实践。

## 初始生产迁移 {#initial-migration}

在执行生产迁移之前，请遵循中概述的迁移步骤的装备和证明 [内容迁移策略和时间表](/help/journey-migration/implementation.md##strategy-timeline) 的部分 [实施阶段](/help/journey-migration/implementation.md).

* 根据您在克隆上执行AEMas a Cloud Service阶段迁移期间获得的经验，启动从生产环境的迁移：
   * Author-Author
   * Publish-Publish

* 验证摄取到AEMas a Cloud Service创作层和发布层的内容。
* 指示内容创作团队在摄取完成之前避免在源和目标上移动内容
* 可以添加、编辑或删除新内容，但应避免移动内容。 这同时适用于源和目标。
* 记录 [所用时间](/help/journey-migration/implementation.md#gathering-data) 对于完全提取和摄取，要估计未来的增补迁移时间线。
* 创建 [迁移规划者](/help/journey-migration/implementation.md#migration-plan) （创作和发布）。

## 增量增补 {#top-up}

从生产环境进行初始迁移后，您必须执行增量增补，以确保您在云实例上使内容保持最新。 因此，建议您遵循以下最佳实践：

* 收集有关内容量的数据。 例如：每一周、两周或一个月。
* 确保按照避免48小时以上的内容提取和引入的方式规划增补。 建议这样做，以便内容增补能够适应周末时间范围。
* 规划所需的增补数量，并使用这些估计在上线日期前后进行规划。

## 确定迁移的代码和内容冻结时间线 {#code-content-freeze}

如前所述，您必须计划代码和内容冻结期。 您可以使用以下问题来帮助计划冻结期：

* 必须冻结内容创作活动多长时间？
* 我应要求投放团队停止添加新功能多久？

要回答第一个问题，您应该考虑在非生产环境中执行试运行所用的时间。 要回答第二个问题，您需要在添加新功能的团队和重构代码的团队之间进行密切合作。 目标是确保添加到现有部署的所有代码均已添加、测试和部署到云服务分支。 通常，这意味着代码冻结的量较低。

此外，您还需要在计划最终内容增补时规划内容冻结。

## 最佳实践 {#best-practices}

在规划或执行迁移时，应考虑以下准则：

* 从作者迁移到作者，从发布迁移到发布
* 请求一个生产克隆，该克隆可用于：
   * 捕获资料档案库统计信息
   * 迁移活动证明
   * 准备迁移计划
   * 确定内容冻结要求
   * 从生产环境迁移时，确定生产环境上的任何规模调整需求

**内容传输工具最佳实践**

确保上线时，您在生产环境中运行内容迁移，而不是克隆。 一个好的方法是使用 [AZCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) 对于初始迁移，然后频繁运行增补提取（甚至每天）以提取较小的块，并避免源AEM上的任何长期负载。

在执行生产迁移时，您应该避免从克隆运行内容传输工具，因为：

* 如果客户要求在增补迁移期间迁移内容版本，则从克隆执行内容传输工具不会迁移这些版本。 即使经常从实时作者重新创建克隆，每次创建克隆时，内容传输工具用于计算增量值的检查点也会重置。
* 由于克隆无法作为一个整体进行刷新，因此必须使用ACL查询包来打包和安装从生产环境添加到克隆或从中进行编辑的内容。 此方法的问题在于，除非手动从源和克隆中删除源实例上任何已删除的内容，否则这些内容将永远不会到达克隆。 这会造成生产环境上已删除的内容在克隆和AEMas a Cloud Service上不被删除。

**在执行内容迁移的同时优化AEM源的负载**

请记住，在提取阶段，AEM源上的负载较大。 请注意以下事项：

* 内容传输工具是一个外部Java进程，它使用4 GB的JVM栈
* 非AzCopy版本下载二进制文件，将其存储在源AEM创作实例上的临时空间中，占用磁盘I/O，然后上载到占用网络带宽的Azure容器中
* [AzCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) 将blob直接从blob存储传输到Azure容器，从而节省磁盘I/O和网络带宽。 AzCopy版本仍使用磁盘和网络带宽来提取数据，并将数据从区段存储上传到Azure容器中
* 内容传输工具进程在摄取阶段对系统资源的影响较小，因为它只流式传输摄取日志，就磁盘I/O或网络带宽而言，源实例上的负载并不大。

## 已知限制 {#known-limitations}

请考虑，如果在提取的迁移集中发现以下任何限制，则整个摄取将失败：

* 名称长度超过150个字符的JCR节点
* 大于16 MB的JCR节点
* 任何用户/组具有 `rep:AuthorizableID` 被摄取，但在AEMas a Cloud Service上已存在
* 如果提取并引入的任何资源在迁移的下一次迭代之前移动到源或目标上的不同路径。

## 资产运行状况 {#asset-health}

与摄取上方部分相比 **不会** 失败，因为存在以下资产问题。 但是，强烈建议在这些情况下采取适当步骤：

* 缺少原始演绎版的任何资源
* 任何缺少的文件夹 `jcr:content` 节点。

上述两项均于 [Best Practice Analyzer](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md) 报告。

## 上线清单 {#Go-Live-Checklist}

欲知更多信息，请参见 [上线清单](/help/journey-onboarding/go-live-checklist.md) 文档。

## 后续内容 {#what-is-next}

了解如何迁移到AEMas a Cloud Service后，您可以检查 [上线后](/help/journey-migration/post-go-live.md) 页面来保持您的实例平稳运行。
