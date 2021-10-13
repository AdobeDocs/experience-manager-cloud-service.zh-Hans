---
title: 使用内容传输工具的准则和最佳实践
description: 使用内容传输工具的准则和最佳实践
source-git-commit: b421cc5e6078112adecb856d723a1bae628d8ec7
workflow-type: tm+mt
source-wordcount: '1503'
ht-degree: 25%

---


# 使用内容传输工具的准则和最佳实践 {#guidelines}

## 准则和最佳实践 {#best-practices}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_guidelines"
>title="准则和最佳实践"
>abstract="查看使用内容传输工具的准则和最佳实践，包括修订清理任务、磁盘空间注意事项等。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#pre-reqs" text="使用内容传输工具的重要注意事项"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#important-considerations" text="使用用户映射工具的重要注意事项"

请阅读以下章节，以了解有关使用内容传输工具的准则和最佳实践。

* 建议对&#x200B;**源**&#x200B;存储库运行[修订清理](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html)和[数据存储一致性检查](https://helpx.adobe.com/cn/experience-manager/kb/How-to-run-a-datastore-consistency-check-via-oak-run-AEM.html)，以确定潜在问题，并减小存储库的大小。

* 如果将 AEM 云创作内容分发网络 (CDN) 配置为包含 IP 白名单，则应确保将源环境 IP 也添加到白名单中，以便源环境和 AEM 云环境可以相互通信。

* 在摄取阶段，建议在启用&#x200B;*划出*&#x200B;模式的情况下来运行摄取，在该模式下，目标 AEM 云服务环境中的现有存储库（创作或发布）将被完全删除，并且之后会使用迁移集数据对存储库进行更新。应用此模式的摄取速度比非划出模式快得多，在非划出模式下，迁移集将应用在当前内容至上。

* 内容传输活动完成后，需要在云服务环境中使用正确的项目结构，才能确保内容在云服务环境中成功呈现。

* 运行内容传输工具之前，必须确保源 AEM 实例的 `crx-quickstart` 子目录中有足够的磁盘空间。这是因为内容传输工具会创建存储库的本地副本，以便稍后将其上传到迁移集。计算所需可用磁盘空间的一般公式如下：
   `data store size + node store size * 1.5`

   * *数据存储大小*：内容传输工具使用 64 GB，即使实际数据存储更大也是如此。
   * *节点存储大小*：区段存储目录大小或 MongoDB 数据库大小。因此，对于 20 GB 的区段存储大小，所需的可用磁盘空间将为 94 GB。

* 需要在整个内容传输活动中维护迁移集，以支持内容增补。 由于在内容传输活动期间一次最多可以创建和维护10个迁移集，因此建议相应地划分内容存储库，以确保不会耗尽迁移集。

## 使用内容传输工具之前的重要注意事项 {#important-considerations}

请阅读以下章节，以了解运行内容传输工具时的重要注意事项：

* 内容传输工具的最低系统要求为 AEM 6.3 + 和 JAVA 8。如果您使用的是较低版本的AEM，则需要将内容存储库升级到AEM 6.5，才能使用内容传输工具。

* 必须在AEM环境中配置Java，以便`java`命令可由启动AEM的用户执行。

* 在安装版本1.3.0时，建议卸载旧版内容传输工具，因为该工具在体系结构上发生了重大更改。 在1.3.0中，您还应该创建新迁移集，并对新迁移集重新运行提取和摄取。

* 内容传输工具可用于以下类型的数据存储：文件数据存储、S3数据存储、共享的S3数据存储和Azure Blob存储数据存储。

* 如果您使用的是&#x200B;*沙盒环境*，请确保您的环境是最新的，并将其升级到最新版本。 如果您使用的是“生产环境”**，则会自动更新。

* 要使用内容传输工具，您需要是源实例上的管理员用户，并且属于要将内容传输到的Cloud Service实例中的本地AEM **administrators**&#x200B;组。 无特权的用户将无法检索访问令牌，进而无法使用内容传输工具。

* 如果设置&#x200B;**在摄取**&#x200B;之前擦除云实例上的现有内容选项处于启用状态，则会删除整个现有存储库并创建新存储库以将内容摄取到中。 这意味着它会重置所有设置，包括目标Cloud Service实例的权限。 对于添加到&#x200B;**administrators**&#x200B;组的管理员用户，也是如此。 必须将用户重新添加到&#x200B;**administrators**&#x200B;组，以检索CTT的访问令牌。

* 访问令牌可在特定时间段后或Cloud Service环境升级后定期过期。 如果访问令牌已过期，您将无法连接到Cloud Service实例，因此您需要检索新的访问令牌。 与现有迁移集关联的状态图标将更改为红色云，并在您将鼠标悬停在该云上时显示一条消息。

* 内容传输工具(CTT)在将内容从源实例传输到目标实例之前，不会执行任何类型的内容分析。 例如，CTT在将内容摄取到发布环境时，不会区分已发布和未发布的内容。 迁移集中指定的任何内容都将被摄取到所选目标实例中。 用户能够将迁移集摄取到创作实例或发布实例中，或同时摄取到两者中。 建议在将内容移动到生产实例时，在源创作实例上安装CTT以将内容移动到目标创作实例，同样，在源发布实例上安装CTT以将内容移动到目标发布实例。 有关更多详细信息，请参阅[在发布实例上运行内容传输工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#running-ctt-on-publish) 。

* 内容传输工具传输的用户和组只是内容满足权限要求的用户和组。 *Extraction*&#x200B;进程将整个`/home`复制到迁移集中，而&#x200B;*Ingestion*&#x200B;进程复制迁移内容ACL中引用的所有用户和组。 要自动将现有用户和组映射到其IMS ID，请参阅[使用用户映射工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#cloud-migration)。

* 在提取阶段，内容传输工具将在活动 AEM 源实例上执行。

* 完成内容传输流程的&#x200B;*提取*&#x200B;阶段后，在开始&#x200B;*摄取阶段*&#x200B;以将内容摄取到AEMas a Cloud Service *暂存*&#x200B;或&#x200B;*生产*&#x200B;实例之前，您需要记录支持票证以通知Adobe您打算运行&#x200B;*摄取*，以便Adobe可以确保在&#x200B;*摄取A11/>流程期间不会发生中断。*&#x200B;您需要在计划的&#x200B;*摄取*&#x200B;日期之前1周记录支持票证。 一旦您提交了支持票证，支持团队将就后续步骤提供指导。 您可以记录支持票证，其中包含以下详细信息：

   * 计划启动&#x200B;*摄取*&#x200B;阶段时的确切日期和预计时间（包含您的时区）。
   * 您计划将数据摄取到的环境类型（暂存或生产）。
   * 程序ID。

* 作者的&#x200B;*摄取阶段*&#x200B;会按比例缩小整个作者部署。 这意味着作者 AEM 在整个摄取过程中将不可用。另外，请确保在运行&#x200B;*Ingestion*&#x200B;阶段时不执行Cloud Manager管道。

* 将`Amazon S3`或`Azure`用作源AEM系统上的数据存储时，应配置数据存储，以便无法删除存储的Blob（垃圾收集）。 这确保了索引数据的完整性，并且未能配置这种方式，可能会由于此索引数据缺乏完整性而导致提取失败。

* 如果使用自定义索引，则必须确保在运行内容传输工具之前使用`tika`节点配置自定义索引。 有关更多详细信息，请参阅[准备新索引定义](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#preparing-the-new-index-definition) 。

* 如果您打算进行增补，则必须从采用初始提取到运行增补提取期间，不更改现有内容的内容结构。 无法对自初始提取以来结构已更改的内容运行增补。 请确保在迁移过程中限制此操作。

* 如果您打算将版本作为迁移集的一部分包含在内，并且正在通过`wipe=false`执行增补，则由于内容传输工具中的当前限制，您必须禁用版本清除。 如果您希望启用版本清除，并在迁移集中执行增补，则必须将摄取作为`wipe=true`执行。

## 下一步 {#whats-next}

了解了使用内容传输工具的准则、最佳实践和重要注意事项后，您现在可以从创建迁移集开始，安装和使用该工具。 请参阅[内容传输入门](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en)以了解更多信息。
