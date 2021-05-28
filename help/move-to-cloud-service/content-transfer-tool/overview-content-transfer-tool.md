---
title: 内容传输工具概述
description: 内容传输工具概述
exl-id: 4715937e-4c4c-4680-af15-016db4fe7db9
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '858'
ht-degree: 72%

---

# 概述 {#overview-content-transfer-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_overview"
>title="概述"
>abstract="内容传输工具是由Adobe开发的工具，可用于将现有内容从源AEM实例（内部部署或AMS）移至目标AEMCloud Service实例。 此工具还会自动传输主体（用户或组）。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#extraction-process" text="提取流程"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#ingestion-process" text="摄取流程"

内容传输工具是 Adobe 开发的一个工具，可用于将现有内容从源 AEM 实例（内部部署或 AMS）移动到目标 AEM 云服务实例。

此工具还会自动传输主体（用户或组）。

内容传输有两个相关阶段：

1. **提取**：提取是指将内容从源 AEM 实例提取到称为&#x200B;*迁移集*&#x200B;的临时区域。*迁移集*&#x200B;是 Adobe 提供的云存储区域，用于临时存储源 AEM 实例和云服务 AEM 实例之间的传输内容。

   有关更多详细信息，请参阅[内容传输中的提取流程](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#extraction-process)。

>[!NOTE]
>
> 建议在提取阶段中运行用户映射工具。 有关更多详细信息，请参阅[使用用户映射工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#cloud-migration) 。

1. **摄取**：摄取是指将内容从&#x200B;*迁移集*&#x200B;摄取到目标云服务实例。

   有关更多详细信息，请参阅[内容传输中的摄取流程](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#ingestion-process)。

*迁移集*&#x200B;具有以下属性：

* 在内容传输活动期间，一次最多可以创建和维护10个迁移集。
* 每个迁移集应具有唯一的名称。
* 如果迁移集处于非活动状态的时间超过 30 天，则将会自动删除该迁移集。
* 每当您创建迁移集时，它都会与特定环境关联。您只能摄取到同一环境的创作或发布实例中。


内容传输工具具备支持差异内容增补的功能，借助该功能，您可以仅传输自上次内容传输活动以来所做的更改。

>[!NOTE]
>
>初始内容传输完成后，建议在云服务上线之前，经常对差异内容进行增补，以缩短最终差异内容传输的内容冻结期。

在提取阶段，要对现有迁移集进行&#x200B;***增补***，则必须禁用&#x200B;*覆盖*&#x200B;选项。有关更多详细信息，请参阅[增补提取](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#top-up-extraction-process)。

在摄取阶段，要在当前内容之上应用增量内容，则必须禁用&#x200B;*划出*&#x200B;选项。有关更多详细信息，请参阅[增补摄取](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#top-up-ingestion-process)。


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