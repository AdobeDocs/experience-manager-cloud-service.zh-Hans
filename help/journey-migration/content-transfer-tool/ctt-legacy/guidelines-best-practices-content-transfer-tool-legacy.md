---
title: 使用内容传输工具的准则和最佳实践（旧版）
description: 使用内容传输工具的准则和最佳实践
hide: true
hidefromtoc: true
exl-id: 03449606-0fb4-4a9f-9abb-6b17c27a6046
source-git-commit: 3c8035e4db5729f58bae29136a32a0b9944d6a2f
workflow-type: tm+mt
source-wordcount: '1477'
ht-degree: 14%

---

# 使用内容传输工具的准则和最佳实践（旧版） {#guidelines}

## 准则和最佳实践 {#best-practices}

请阅读以下章节，以了解有关使用内容传输工具的准则和最佳实践。

* 运行 [修订版清理](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html) 和 [数据存储一致性检查](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-16550.html?lang=en) 在 **源** 存储库，以确定潜在问题并减小存储库的大小。

* 如果将AEM Cloud Author Content Delivery Network (CDN)配置配置为具有个IP，请确保将源环境IP也添加到允许列表 允许列表。 这样做可确保源环境和AEM Cloud环境可以相互通信。

* 使用运行引入 *划出* 启用模式，在这种模式下，将删除目标AEM Cloud Service环境中的现有存储库（创作或发布），然后使用迁移集数据进行更新。 应用此模式的摄取速度比非划出模式快得多，在非划出模式下，迁移集将应用在当前内容至上。

* 内容传输活动完成后，需要在云服务环境中使用正确的项目结构，才能确保内容在云服务环境中成功呈现。

* 运行内容传输工具之前，必须确保源 AEM 实例的 `crx-quickstart` 子目录中有足够的磁盘空间。这是因为内容传输工具会创建存储库的本地副本，以便稍后将其上传到迁移集。计算所需可用磁盘空间的一般公式如下：
   `data store size + node store size * 1.5`

   * *数据存储大小*：内容传输工具使用 64 GB，即使实际数据存储更大也是如此。
   * *节点存储大小*：区段存储目录大小或 MongoDB 数据库大小。因此，对于 20 GB 的区段存储大小，所需的可用磁盘空间将为 94 GB。

* 必须在整个内容传输活动中维护迁移集，以支持内容增补。 由于在内容传输活动期间，一次最多可以创建和维护10个迁移集，因此建议相应地拆分内容存储库。 这样做可确保迁移集不会用完。

## 使用内容传输工具之前的重要注意事项 {#important-considerations}

请阅读以下章节，以了解运行内容传输工具时的重要注意事项：

* 内容传输工具的最低系统要求为AEM 6.3 +和Java™ 8。 如果您使用的是较低版本的AEM，则需要将内容存储库升级到AEM 6.5才能使用内容传输工具。

* 必须在AEM环境中配置Java™，以便 `java` 命令可以由启动AEM的用户执行。

* 在安装版本1.3.0时卸载内容传输工具的旧版本，因为该工具中存在重大的体系结构更改。 对于1.3.0，您还应该创建迁移集，并对新的迁移集重新运行提取和摄取。

* 内容传输工具可与以下类型的数据存储一起使用：文件数据存储、S3数据存储、共享S3数据存储和Azure Blob存储数据存储。

* 如果您使用 *沙盒环境*，确保您的环境为最新版本并已升级到最新版本。 如果您使用的是“生产环境”**，则会自动更新。

* 要使用内容传输工具，您需要是源实例上的管理员用户，并且属于本地AEM **管理员** 组将内容传输到Cloud Service实例中。 无权限用户无法检索访问令牌以使用内容传输工具。

* 如果设置 **在引入之前擦除云实例上的现有内容** 选项时，会删除整个现有存储库并创建一个存储库以将内容摄取到。 此工作流表示它会重置所有设置，包括目标Cloud Service实例的权限。 即使管理员用户已添加到，也是如此 **管理员的** 组。 必须将用户重新编入 **管理员的** 组来检索内容传输工具的访问令牌。

* 如果将来自两个源的内容移动到目标上的相同Cloud Service，则内容传输工具不支持将来自多个源的内容合并到目标路径实例中。 要将多个源中的内容移动到单个目标Cloud Service实例中，您需要确保源中的内容路径不重叠。

* 访问令牌可在特定时间段后或在Cloud Service环境升级后定期过期。 如果访问令牌已过期，则您无法连接到Cloud Service实例。 在这种情况下，您需要检索新的访问令牌。 与现有迁移集关联的状态图标将更改为红色云，当您将鼠标悬停在该云上时，将显示一条消息。

* 在将内容从源实例传输到目标实例之前，内容传输工具(CTT)不执行任何类型的内容分析。 例如，将内容摄取到发布环境时，CTT不区分已发布和未发布的内容。 迁移集中指定的任何内容都会被摄取到所选的目标实例中。 用户可以将迁移集摄取到创作实例和/或发布实例。 将内容移动到生产实例时，请在源创作实例上安装CTT以将内容移动到目标创作实例。 同样，在源发布实例上安装CTT以将内容移动到目标发布实例。 请参阅 [在发布实例上运行内容传输工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en#running-tool) 了解更多详细信息。

* 内容传输工具传输的用户和组只是内容满足权限要求的用户和组。 此 *提取* 进程复制整个 `/home` 移入迁移集和 *引入* 进程会复制迁移的内容ACL中引用的所有用户和组。 要自动将现有用户和组映射到其IMS ID，请参阅 [使用用户映射工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/legacy-user-mapping-tool/using-user-mapping-tool-legacy.html?lang=en).

* 在提取阶段，内容传输工具将在活动 AEM 源实例上执行。

* 完成 *提取* 内容传输过程的阶段以及开始 *摄取阶段* 将内容摄取到AEMas a Cloud Service *暂存* 或 *生产* 实例中，记录支持服务单。 通知Adobe您打算运行 *引入* 以便Adobe能够确保在故障期间不发生中断， *引入* 进程。 在计划的前一周记录支持工单 *引入* 日期。 提交支持工单后，支持团队会提供后续步骤的指导。 记录支持票证，并提供以下详细信息：

   * 计划开始的确切日期和预计时间（以您的时区为准） *引入* 阶段。
   * 您计划将数据摄取到的环境类型（暂存或生产）。
   * 项目ID。

* 此 *摄取阶段* 对于作者，缩小了整个作者部署。 此过程意味着创作的AEM在整个摄取过程中不可用。 此外，请确保在运行时没有执行Cloud Manager管道 *引入* 阶段。

* 使用时 `Amazon S3` 或 `Azure` 作为源AEM系统上的数据存储，数据存储应进行配置，以便存储的blob无法删除（垃圾收集）。 这样可以确保索引数据的完整性，如果未能按此方式进行配置，则可能会导致因缺少此索引数据的完整性而导致提取失败。

* 如果使用自定义索引，则必须确保为自定义索引配置 `tika` 节点。 请参阅 [准备新索引定义](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html?lang=en#preparing-the-new-index-definition) 了解更多详细信息。

* 如果要执行增补，请确保现有内容的内容结构不会从初次提取时更改为运行增补提取时。 无法对自初始提取以来结构已更改的内容运行增补。 确保在迁移过程中对此进行限制。

* 如果您打算将版本包含在迁移集中，并使用执行增补 `wipe=false`，则由于内容传输工具中的当前限制，您必须禁用版本清除。 如果您希望启用版本清除，并且要对迁移集执行增补，则必须按以下方式执行引入 `wipe=true`.

## 后续内容 {#whats-next}

了解使用内容传输工具的准则、最佳实践和重要注意事项后，您现在就可以开始安装和使用工具了，从创建迁移集开始。 参见 [内容传输工具快速入门](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=zh-Hans) 了解更多信息。
