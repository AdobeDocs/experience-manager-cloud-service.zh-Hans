---
title: 使用内容传输工具的准则和最佳实践
description: 使用内容传输工具的准则和最佳实践
exl-id: d1975c34-85d4-42e0-bb1a-968bdb3bf85d
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '1547'
ht-degree: 19%

---

# 使用内容传输工具的准则和最佳实践 {#guidelines}

## 准则和最佳实践 {#best-practices}

<!-- Alexandru: hiding for now

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_guidelines"
>title="Guidelines and Best Practices"
>abstract="Review guidelines and best practices to use the Content Transfer tool including revision cleanup tasks, Disk space considerations and more."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html" text="Important Considerations for using Content Transfer Tool"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/user-mapping-and-migration.md#important-considerations" text="Important Considerations when Mapping and Migrating Users" 

-->

已提供新版本的内容传输工具，它将内容传输过程与 Cloud Acceleration Manager 集成。强烈建议切换到此新版本以使用它提供的所有好处：

* 一次性提取迁移集并将它并行摄取到多个环境中的自助方式
* 通过更好的加载状态、防护机制和错误处理改善用户体验
* 摄取日志将保留，并且始终可用于进行故障排除

要开始使用新版本，您需要卸载旧版本的内容传输工具。 之所以需要这样做，是因为新版本带来了重大的体系结构变化。 使用版本2.x时，您需要创建新迁移集，并对新迁移集重新运行提取和摄取。
不再支持2.0.0之前的版本，建议使用最新版本。

以下准则和最佳实践适用于新版本的内容传输工具：

* 建议对&#x200B;**源**&#x200B;存储库运行[修订清理](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html)和[数据存储一致性检查](https://helpx.adobe.com/cn/experience-manager/kb/How-to-run-a-datastore-consistency-check-via-oak-run-AEM.html)，以确定潜在问题，并减小存储库的大小。

* 在摄取阶段，建议使用运行摄取 *划出* 启用模式后，目标AEM Cloud Service环境中的现有存储库（创作或发布）将被完全删除，然后使用迁移集数据更新。 应用此模式的摄取速度比非划出模式快得多，在非划出模式下，迁移集将应用在当前内容至上。

* 内容传输活动完成后，需要在云服务环境中使用正确的项目结构，才能确保内容在云服务环境中成功呈现。

* 运行内容传输工具之前，必须确保源 AEM 实例的 `crx-quickstart` 子目录中有足够的磁盘空间。这是因为内容传输工具会创建存储库的本地副本，以便稍后将其上传到迁移集。计算所需可用磁盘空间的一般公式如下：
  `data store size + node store size * 1.5`

   * *数据存储大小*：内容传输工具使用 64 GB，即使实际数据存储更大也是如此。
   * *节点存储大小*：区段存储目录大小或 MongoDB 数据库大小。因此，对于 20 GB 的区段存储大小，所需的可用磁盘空间将为 94 GB。

* 在整个内容传输活动中，需要维护迁移集以支持内容增补。 在内容传输活动期间，Cloud Acceleration Manager中一次最多可以为每个项目创建和维护五个迁移集。 如果需要超过五个迁移集，则需要在Cloud Acceleration Manager中创建第二个项目。 但是，这需要额外的项目管理和产品外管理，以避免多个用户覆盖Target上的内容。

## 使用内容传输工具之前的重要注意事项 {#important-considerations}

请阅读以下章节，以了解运行内容传输工具时的重要注意事项：

* 内容传输工具的最低系统要求为 AEM 6.3 + 和 JAVA 8。如果您使用的是较低版本的AEM，则需要将内容存储库升级到AEM 6.5才能使用内容传输工具。

* 必须在AEM环境中配置Java，以便 `java` 命令可以由启动AEM的用户执行。

* 内容传输工具可与以下类型的数据存储一起使用：文件数据存储、S3数据存储、共享S3数据存储和Azure Blob存储数据存储。

* 如果您使用 *沙盒环境*，确保您的环境为最新版本并已升级到最新版本。 如果您使用的是“生产环境”**，则会自动更新。

* 要开始引入，您需要属于本地AEM **管理员** 组将内容传输到Cloud Service实例中。 没有权限的用户将无法在不手动提供迁移令牌的情况下开始引入。

* 如果设置 **在引入之前擦除云实例上的现有内容** 选项，它会删除整个现有存储库并创建一个新存储库以将内容摄取到。 这意味着它会重置所有设置，包括目标Cloud Service实例上的权限。 对于添加到的管理员用户也是如此 **管理员** 组。 必须将用户重新添加到 **管理员** 组以检索内容传输工具的访问令牌。

* 如果将来自两个源的内容移动到目标上的相同Cloud Service，则摄取不支持将来自多个源的内容合并到目标路径实例中。 要将多个源中的内容移动到单个目标Cloud Service实例中，您需要确保源中的内容路径不重叠。

* 提取密钥的有效期为从创建/续订之日起的14天。 可以随时续订。 如果提取密钥已过期，您将无法执行提取。

* 在将内容从源实例传输到目标实例之前，内容传输工具(CTT)不执行任何类型的内容分析。 例如，将内容摄取到发布环境时，CTT不区分已发布和未发布的内容。 迁移集中指定的任何内容都会被摄取到所选的目标实例中。 用户能够将迁移集摄取到创作实例和/或发布实例中。 建议在将内容移动到生产实例时，在源作者实例上安装CTT以将内容移动到目标作者实例，同样，在源发布实例上安装CTT以将内容移动到目标发布实例。 参见 [在发布实例上运行内容传输工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html#running-tool) 了解更多详细信息。

* 内容传输工具传输的用户和组只是内容满足权限要求的用户和组。 此 _提取_ 进程复制整个 `/home` 在迁移集中，它通过添加从每个用户的电子邮件地址生成的字段来进行用户映射。 有关更多信息，请参阅 [用户映射和主体迁移](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md). 此 _引入_ 进程会复制迁移的内容ACL中引用的所有用户和组。

* 在提取阶段，内容传输工具将在活动 AEM 源实例上执行。

* 完成 *提取* 内容传输过程的阶段以及开始 *摄取阶段* 将内容摄取到AEMas a Cloud Service *暂存* 或 *生产* 实例中，您需要记录支持工单以通知Adobe您打算运行 *引入* 以便Adobe能够确保在故障期间不发生中断， *引入* 进程。 您需要比计划提前1周记录支持工单 *引入* 日期。 提交支持工单后，支持团队将提供后续步骤的指导。 您可以记录支持工单，并提供以下详细信息：

   * 计划开始的确切日期和预计时间（以您的时区为准） *引入* 阶段。
   * 您计划将数据摄取到的环境类型（暂存或生产）。
   * 项目ID。

* 此 *摄取阶段* 对于作者，缩小了整个作者部署。 这意味着创作的AEM在整个摄取过程中不可用。 此外，请确保在运行时没有执行Cloud Manager管道 *引入* 阶段。

* 使用时 `Amazon S3` 或 `Azure` 作为源AEM系统上的数据存储，数据存储应进行配置，以便存储的blob无法删除（垃圾收集）。 这样可以确保索引数据的完整性，如果未能按此方式进行配置，则可能会导致因缺少此索引数据的完整性而导致提取失败。

* 如果使用自定义索引，则必须确保为自定义索引配置 `tika` 节点。 请参阅 [准备新索引定义](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html#preparing-the-new-index-definition) 了解更多详细信息。

* 如果您打算进行增补，则必须不要更改现有内容的内容结构，即从初次提取时更改到运行增补提取时。 无法对自初始提取以来结构已更改的内容运行增补。 请确保在迁移过程中对此进行限制。

* 如果您打算将版本包含在迁移集中，并使用执行增补 `wipe=false`，则由于内容传输工具中的当前限制，您必须禁用版本清除。 如果您希望启用版本清除，并且要对迁移集执行增补，则必须按以下方式执行引入 `wipe=true`.

* 迁移集将在长时间不活动后过期，之后其数据将不再可用。 请查阅 [迁移集到期](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html#migration-set-expiry) 了解更多详细信息。

## 后续内容 {#whats-next}

了解使用内容传输工具的准则、最佳实践和重要注意事项后，您现在就可以开始安装和使用工具了，从创建迁移集开始。 参见 [内容传输工具快速入门](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md) 了解更多信息。
