---
title: 有关使用内容传输工具的准则和最佳实践
description: 了解使用内容传输工具的准则和最佳实践。
exl-id: d1975c34-85d4-42e0-bb1a-968bdb3bf85d
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1401'
ht-degree: 15%

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
* 通过更好的加载状态、护栏和错误处理来改善用户体验
* 摄取日志将保留，并且始终可用于进行故障排除

要开始使用新版本，请卸载旧版本的内容传输工具。 之所以需要，是因为新版本带来了重大的架构变化。 使用版本2.x，您可以创建迁移集，并对迁移集重新运行提取和摄取。
不支持低于2.0.0的版本，建议您使用最新版本。

以下准则和最佳实践适用于内容传输工具的新版本：

* 对&#x200B;**源**&#x200B;存储库运行[修订清理](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html)和[数据存储一致性检查](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-16550.html)，以便识别潜在问题并降低存储库的大小。

* 在摄取阶段，Adobe建议您在删除目标Adobe Experience Manager (AEM)Cloud Service环境中的现有存储库（创作或发布）的情况下使用启用的&#x200B;*划出*&#x200B;模式来运行摄取。 然后，使用迁移集数据更新。 此模式比非划出模式更快，在非划出模式下，迁移集将应用于当前内容的顶部。

* 内容传输活动完成后，需要在云服务环境中使用正确的项目结构，才能确保内容在云服务环境中成功呈现。

* 运行内容传输工具之前，必须确保源 AEM 实例的 `crx-quickstart` 子目录中有足够的磁盘空间。这是因为内容传输工具会创建存储库的本地副本，以便稍后将其上传到迁移集。计算所需可用磁盘空间的一般公式如下：
  `data store size + node store size * 1.5`

   * *数据存储大小*：内容传输工具使用 64 GB，即使实际数据存储更大也是如此。
   * *节点存储大小*：区段存储目录大小或 MongoDB 数据库大小。因此，对于 20 GB 的区段存储大小，所需的可用磁盘空间将为 94 GB。

* 必须在整个内容传输活动中维护迁移集，以支持内容增补。 在内容传输活动期间，Cloud Acceleration Manager中一次最多可以为每个项目创建和维护20个迁移集。 如果需要超过20个迁移集，请在Cloud Acceleration Manager中创建第二个项目。 但是，这需要额外的项目管理和产品外管理，以避免多个用户覆盖Target上的内容。

* 避免更改CTT工具的安装目录。 默认情况下，安装在crx-quickstart/cloud-migration路径中进行。 此特定位置由其他库在内部使用。 修改此路径可能会导致提取问题。

## 使用内容传输工具之前的重要注意事项 {#important-considerations}

请阅读以下章节，以了解运行内容传输工具时的重要注意事项：

* 内容传输工具的最低系统要求为AEM 6.3 +和Java™ 8。 如果您使用的是较低版本的AEM，请将内容存储库升级到AEM 6.5以使用内容传输工具。

* 必须在AEM环境中配置Java™，以便启动AEM的用户能够执行`java`命令。

* 内容传输工具可用于以下类型的数据存储：文件数据存储、S3数据存储、共享S3数据存储和Azure Blob存储数据存储。

* 如果您使用的是&#x200B;*沙盒环境*，请确保您的环境为最新版本并已升级到最新版本。 如果您使用的是“生产环境”**，则会自动更新。

* 要开始引入，您必须属于要向其传输内容的Cloud Service实例中的本地AEM **管理员**&#x200B;组。 如果未手动提供迁移令牌，则无权限用户无法开始引入。

* 如果启用了设置&#x200B;**在摄取之前擦除云实例上的现有内容**&#x200B;选项，它将删除整个现有存储库并创建一个新存储库以将内容摄取到。 这意味着它会重置所有设置，包括目标Cloud Service实例上的权限。 对于添加到&#x200B;**管理员**&#x200B;组的管理员用户也是如此。 必须将该用户读入&#x200B;**管理员**&#x200B;组，才能检索内容传输工具的访问令牌。

* 如果将来自两个源的内容移动到目标上的相同路径，则摄取不支持将来自多个源的内容合并到目标Cloud Service实例中。 要将内容从多个源移动到单个目标Cloud Service实例，请确保源中的内容路径不重叠。

* 提取密钥的有效期为自创建或续订密钥后的14天。 可以随时续订。 如果提取密钥已过期，则无法执行提取。

* 在将内容从源实例传输到目标实例之前，内容传输工具(CTT)不执行任何类型的内容分析。 例如，将内容摄取到Publish环境中时，CTT不区分已发布和未发布的内容。 迁移集中指定的任何内容都将摄取到所选的目标实例中。 用户可以将迁移集摄取到创作实例或Publish实例，或同时摄取两者。 Adobe建议在将内容移动到生产实例时，在源创作实例上安装CTT以将内容移动到目标创作实例。 同样，在源Publish实例上安装CTT以将内容移动到目标Publish实例。 有关更多详细信息，请参阅[在Publish实例上运行内容传输工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html#running-tool)。

* 内容传输工具传输的用户和组只是内容满足权限要求的用户和组。 _提取_&#x200B;进程将整个`/home`复制到迁移集中，并通过添加从每个用户的电子邮件地址创建的字段来进行用户映射。 有关详细信息，请参阅[用户映射和主体迁移](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md)。 _摄取_&#x200B;进程将复制迁移的内容ACL中引用的所有用户和组。 有关在封闭用户组(CUG)策略中使用的组的额外注意事项，请参阅[迁移封闭用户组](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/closed-user-groups-migration.md)。

* 在提取阶段，内容传输工具将在活动 AEM 源实例上执行。

* 作者的&#x200B;*摄取阶段*&#x200B;缩小了整个作者部署。 这意味着创作的AEM在整个摄取过程中不可用。 同时确保在运行&#x200B;*摄取*&#x200B;阶段时没有执行Cloud Manager管道。

* 使用`Amazon S3`或`Azure`作为源AEM系统上的数据存储时，应配置数据存储以便不能删除存储的Blob（垃圾收集）。 这将确保索引数据的完整性，如果未能按此方式进行配置，则可能会导致因此索引数据缺乏完整性而导致提取失败。

* 如果使用自定义索引，则必须确保在运行内容传输工具之前使用`tika`节点配置自定义索引。 有关详细信息，请参阅[准备新索引定义](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html#preparing-the-new-index-definition)。

* 如果要执行增补，则现有内容的内容结构不得从进行初始提取时更改为运行增补提取时。 无法对自初始提取以来结构已更改的内容运行增补。 确保在迁移过程中对此进行限制。

* 如果您打算将版本包含在迁移集中，并使用`wipe=false`执行增补，则由于“内容传输工具”中的当前限制，必须禁用版本清除。 如果您希望启用版本清除，并且正在对迁移集执行增补，则必须作为`wipe=true`执行引入。

* 迁移集在长时间不活动后过期，此后其数据将不再可用。 有关更多详细信息，请查看[迁移集到期](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html#migration-set-expiry)。

## 后续内容 {#whats-next}

了解使用内容传输工具的指南、最佳实践和重要注意事项后，您现在就可以开始安装和使用工具了，从创建迁移集开始。 请参阅[内容传输工具快速入门](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md)。
