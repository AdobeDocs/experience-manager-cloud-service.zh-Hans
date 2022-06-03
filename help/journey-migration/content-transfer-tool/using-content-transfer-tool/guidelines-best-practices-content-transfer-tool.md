---
title: 使用内容传输工具的准则和最佳实践
description: 使用内容传输工具的准则和最佳实践
exl-id: d1975c34-85d4-42e0-bb1a-968bdb3bf85d
source-git-commit: 98b81d918d60722ddb3f1c7736bc5b3506e05f6f
workflow-type: tm+mt
source-wordcount: '1654'
ht-degree: 21%

---

# 使用内容传输工具的准则和最佳实践 {#guidelines}

## 准则和最佳实践 {#best-practices}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_guidelines"
>title="准则和最佳实践"
>abstract="查看使用内容传输工具的准则和最佳实践，包括修订清理任务、磁盘空间注意事项等。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#pre-reqs" text="使用内容传输工具的重要注意事项"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#important-considerations" text="使用用户映射工具的重要注意事项"

提供了内容传输工具的新版本，该版本将内容传输流程与Cloud Acceleration Manager集成在一起。 强烈建议切换到此新版本，以利用它提供的所有优势：

* 一次提取迁移集并将其并行摄取到多个环境的自助方法
* 通过更好的加载状态、护栏和错误处理来改善用户体验
* 将保留摄取日志，并始终可用于疑难解答

要开始使用新版本(v2.0.10)，您需要卸载旧版内容传输工具。 这是必需的，因为新版本具有重大的体系结构变化。 在v2.0.10中，您将需要创建新的迁移集，并对新迁移集重新运行提取和摄取。 如果迁移已在进行中，您可以继续使用以前版本的CTT，直到迁移完成为止。

以下准则和最佳实践适用于新版本的内容传输工具：

* 建议对&#x200B;**源**&#x200B;存储库运行[修订清理](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html)和[数据存储一致性检查](https://helpx.adobe.com/cn/experience-manager/kb/How-to-run-a-datastore-consistency-check-via-oak-run-AEM.html)，以确定潜在问题，并减小存储库的大小。

* 如果将 AEM 云创作内容分发网络 (CDN) 配置为包含 IP 白名单，则应确保将源环境 IP 也添加到白名单中，以便源环境和 AEM 云环境可以相互通信。

* 在摄取阶段，建议在启用&#x200B;*划出*&#x200B;模式的情况下来运行摄取，在该模式下，目标 AEM 云服务环境中的现有存储库（创作或发布）将被完全删除，并且之后会使用迁移集数据对存储库进行更新。应用此模式的摄取速度比非划出模式快得多，在非划出模式下，迁移集将应用在当前内容至上。

* 内容传输活动完成后，需要在云服务环境中使用正确的项目结构，才能确保内容在云服务环境中成功呈现。

* 运行内容传输工具之前，必须确保源 AEM 实例的 `crx-quickstart` 子目录中有足够的磁盘空间。这是因为内容传输工具会创建存储库的本地副本，以便稍后将其上传到迁移集。计算所需可用磁盘空间的一般公式如下：
   `data store size + node store size * 1.5`

   * *数据存储大小*：内容传输工具使用 64 GB，即使实际数据存储更大也是如此。
   * *节点存储大小*：区段存储目录大小或 MongoDB 数据库大小。因此，对于 20 GB 的区段存储大小，所需的可用磁盘空间将为 94 GB。

* 需要在整个内容传输活动中维护迁移集，以支持内容增补。 在内容传输活动期间，Cloud Acceleration Manager中每个项目最多可以一次创建和维护5个迁移集。 如果需要五个以上的迁移集，则需要在Cloud Acceleration Manager中创建第二个项目。 但是，这将需要额外的项目管理和产品外管理，以避免多个用户覆盖目标上的内容。

## 使用内容传输工具之前的重要注意事项 {#important-considerations}

请阅读以下章节，以了解运行内容传输工具时的重要注意事项：

* 内容传输工具的最低系统要求为 AEM 6.3 + 和 JAVA 8。如果您使用的是较低版本的AEM，则需要将内容存储库升级到AEM 6.5，才能使用内容传输工具。

* 必须在AEM环境中配置Java，以便 `java` 命令可由启动AEM的用户执行。

* 内容传输工具可用于以下类型的数据存储：文件数据存储、S3数据存储、共享的S3数据存储和Azure Blob存储数据存储。

* 如果您使用 *沙盒环境*，请确保您的环境是最新的并已升级到最新版本。 如果您使用的是“生产环境”**，则会自动更新。

* 要使用内容传输工具，您需要成为源实例上的管理员用户，并且属于本地AEM **管理员** 组。 无特权的用户将无法开始摄取。

* 如果设置 **摄取前擦除云实例上的现有内容** 选项时，它会删除整个现有存储库并创建新存储库以将内容摄取到中。 这意味着它会重置所有设置，包括目标Cloud Service实例的权限。 对于添加到 **管理员** 群组。 必须将用户重新添加到 **管理员** 组，以检索内容传输工具的访问令牌。

* 如果将来自两个源的内容移动到目标上的相同路径，则内容传输工具不支持将来自多个源的内容合并到目标Cloud Service实例中。 要将多个源中的内容移动到单个目标Cloud Service实例，您需要确保源中的内容路径不重叠。

* 提取键值自创建/续订后14天内有效。 可以随时更新。 如果提取键值已过期，您将无法执行提取。

* 内容传输工具(CTT)在将内容从源实例传输到目标实例之前，不会执行任何类型的内容分析。 例如，CTT在将内容摄取到发布环境时，不会区分已发布和未发布的内容。 迁移集中指定的任何内容都将被摄取到所选目标实例中。 用户能够将迁移集摄取到创作实例或发布实例中，或同时摄取到两者中。 建议在将内容移动到生产实例时，在源创作实例上安装CTT以将内容移动到目标创作实例，同样，在源发布实例上安装CTT以将内容移动到目标发布实例。 请参阅 [在发布实例上运行内容传输工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#running-ctt-on-publish) 以了解更多详细信息。

* 内容传输工具传输的用户和组只是内容满足权限要求的用户和组。 的 *提取* 进程复制整个 `/home` 到迁移集和 *摄取* 进程会复制迁移内容ACL中引用的所有用户和组。 要自动将现有用户和组映射到其IMS ID，请参阅 [使用用户映射工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#cloud-migration).

* 在提取阶段，内容传输工具将在活动 AEM 源实例上执行。

* 完成 *提取* 内容传输过程的阶段和开始之前 *摄取阶段* 将内容摄取到AEMas a Cloud Service *阶段* 或 *生产* 实例时，您需要记录支持票证，以通知Adobe您打算运行 *摄取* 以便Adobe能够确保在 *摄取* 进程。 您需要在计划前1周记录支持票证 *摄取* 日期。 一旦您提交了支持票证，支持团队将就后续步骤提供指导。 您可以记录支持票证，其中包含以下详细信息：

   * 计划开始时的确切日期和预计时间（包括您所在的时区） *摄取* 阶段。
   * 您计划将数据摄取到的环境类型（暂存或生产）。
   * 程序ID。

* 的 *摄取阶段* 对于，作者会按比例缩小整个作者部署。 这意味着作者 AEM 在整个摄取过程中将不可用。另外，请确保在运行 *摄取* 阶段。

* 使用 `Amazon S3` 或 `Azure` 由于数据存储在源AEM系统上，因此应该配置数据存储，以便无法删除存储的Blob（垃圾收集）。 这确保了索引数据的完整性，并且未能配置这种方式，可能会由于此索引数据缺乏完整性而导致提取失败。

* 如果使用自定义索引，则必须确保使用 `tika` 节点。 请参阅 [准备新的索引定义](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#preparing-the-new-index-definition) 以了解更多详细信息。

* 如果您打算进行增补，则必须从采用初始提取到运行增补提取期间，不更改现有内容的内容结构。 无法对自初始提取以来结构已更改的内容运行增补。 请确保在迁移过程中限制此操作。

* 如果您打算将版本作为迁移集的一部分，并且要通过 `wipe=false`，则由于内容传输工具中的当前限制，您必须禁用版本清除。 如果您希望保持启用版本清除，并在迁移集中执行增补，则必须将摄取作为 `wipe=true`.

## 接下来呢？ {#whats-next}

了解了使用内容传输工具的准则、最佳实践和重要注意事项后，您现在可以从创建迁移集开始，安装和使用该工具。 请参阅 [内容传输工具快速入门](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en) 以了解更多。
