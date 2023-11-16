---
title: 上线
description: 了解在代码和内容准备就绪后，如何执行迁移
exl-id: 10ec0b04-6836-4e26-9d4c-306cf743224e
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '1704'
ht-degree: 4%

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

此外，您需要计划在计划最终内容增补时冻结内容。

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

请记住，在提取阶段，AEM源上的负载较大。 您应了解：

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

请查看此活动列表，确保顺利成功地执行迁移。

* 运行具有功能和UI测试的端到端生产管道，以确保 **始终最新** AEM产品体验。 请参阅以下资源。
   * [AEM 版本更新](/help/implementing/deploying/aem-version-updates.md)
   * [自定义功能测试](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing)
   * [UI 测试](/help/implementing/cloud-manager/ui-testing.md)
* 将内容迁移到生产环境，并确保在暂存环境中有相关的子集可用于测试。
   * 适用于AEM的DevOps最佳实践意味着，当内容从生产环境向下移动时，代码会从开发环境向上移动到生产环境。
* 计划代码和内容冻结期。
   * 另请参阅部分 [用于迁移的代码和内容冻结时间线](#code-content-freeze)
* 执行最终内容增补。
* 验证Dispatcher配置。
   * 使用本地Dispatcher验证器，这有助于在本地配置、验证和模拟Dispatcher
      * [设置本地Dispatcher工具](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html?lang=en#prerequisites)
   * 仔细查看虚拟主机配置。
      * 最简单（默认）的解决方案是包括 `ServerAlias *` 在虚拟主机文件中 `/dispatcher/src/conf.d/available_vhostsfolder`.
         * 这将允许产品功能测试、Dispatcher缓存失效和克隆使用的主机别名正常运行。
      * 但是，如果 `ServerAlias *` 不可接受，至少如下所示 `ServerAlias` 除了自定义域外，还必须允许以下条目：
         * `localhost`
         * `*.local`
         * `publish*.adobeaemcloud.net`
         * `publish*.adobeaemcloud.com`
* 配置CDN、SSL和DNS。
   * 如果您使用自己的CDN，请输入支持票证以配置相应的路由。
      * 请参阅部分 [客户CDN指向AEM托管的CDN](/help/implementing/dispatcher/cdn.md#point-to-point-cdn) 详细信息，请参阅CDN文档。
      * 根据CDN供应商的文档配置SSL和DNS。
   * 如果您没有使用其他CDN，请按照以下文档管理SSL和DNS：
      * 管理 SSL 证书
         * [管理 SSL 证书简介](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
         * [管理SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)
      * 管理自定义域名(DNS)
         * 为了确保DNS直接转换不会引入意外问题，最好在正式启用并进行一轮UAT测试之前创建一个测试子域以将生产实例连接到该子域。 因此，如果您的域是example.com，则可以创建一个子域test.example.com并将其应用于生产环境。 在对域进行UAT测试期间，您需要查找适当的链接重定向、缓存和Dispatcher配置等。
         * [自定义域名简介](/help/implementing/cloud-manager/custom-domain-names/introduction.md)
         * [添加自定义域名](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)
         * [管理自定义域名](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)
   * 请记住验证DNS记录的TTL集。
      * TTL是在请求服务器更新之前DNS记录保留在缓存中的时间。
      * 如果您的TTL非常高，则传播对DNS记录的更新将需要较长时间。
* 运行符合您的业务要求和目标的性能和安全性测试。
* 切换并确保不进行任何新部署或内容更新而执行实际上线。
* 创建Admin Console用户通知配置文件。 请参阅 [通知配置文件](/help/journey-onboarding/notification-profiles.md)

在执行迁移时，如果您需要重新校准任务，您可以随时引用列表。

## 后续内容 {#what-is-next}

了解如何迁移到AEMas a Cloud Service后，您可以检查 [上线后](/help/journey-migration/post-go-live.md) 页面来保持您的实例平稳运行。
