---
title: 内容传输工具概述
description: 内容传输工具概述
translation-type: tm+mt
source-git-commit: 23349f3350631f61f80b54b69104e5a19841272f
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 69%

---


# 概述 {#overview-content-transfer-tool}

内容传输工具是 Adobe 开发的一个工具，可用于将现有内容从源 AEM 实例（内部部署或 AMS）移动到目标 AEM 云服务实例。

此工具还会自动传输主体（用户或组）。

内容传输有两个相关阶段：

1. **提取**：提取是指将内容从源 AEM 实例提取到称为&#x200B;*迁移集*&#x200B;的临时区域。*迁移集*&#x200B;是 Adobe 提供的云存储区域，用于临时存储源 AEM 实例和云服务 AEM 实例之间的传输内容。

   有关更多详细信息，请参阅[内容传输中的提取流程](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#extraction-process)。

2. **摄取**：摄取是指将内容从&#x200B;*迁移集*&#x200B;摄取到目标云服务实例。

   有关更多详细信息，请参阅[内容传输中的摄取流程](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#ingestion-process)。

*迁移集*&#x200B;具有以下属性：

* 在内容传输活动期间，一次最多可以创建和维护 4 个迁移集。
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

请阅读以下章节，以了解有关使用内容传输工具的准则和最佳实践。

* 建议在源存储库 [上运行修订](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/deploying/revision-cleanup.html)[清理和数据存储一致性检](https://helpx.adobe.com/experience-manager/kb/How-to-run-a-datastore-consistency-check-via-oak-run-AEM.html) 查，以确 **定潜在问题** ，并减小存储库的大小。

* 如果将AEM Cloud作者内容投放网络(CDN)配置配置为包含IP的白名单，则应确保将源环境IP也添加到允许列表中，以便源环境和AEM Cloud环境可以相互通信。

* 在摄取阶段，建议在启用&#x200B;*划出*&#x200B;模式的情况下来运行摄取，在该模式下，目标 AEM 云服务环境中的现有存储库（创作或发布）将被完全删除，并且之后会使用迁移集数据对存储库进行更新。应用此模式的摄取速度比非划出模式快得多，在非划出模式下，迁移集将应用在当前内容至上。

* 内容传输活动完成后，需要在云服务环境中使用正确的项目结构，才能确保内容在云服务环境中成功呈现。

* 运行内容传输工具之前，必须确保源AEM实例的子目录中 `crx-quickstart` 有足够的磁盘空间。 这是因为内容传输工具创建了存储库的本地副本，稍后将其上传到迁移集。
计算所需可用磁盘空间的一般公式如下：
   `data store size + node store size * 1.5`

   * *数据存储大小*: 内容传输工具使用64 GB，即使实际数据存储空间更大。
   * *节点存储大小*: 区段存储目录大小或MongoDB数据库大小。
因此，对于20GB的区段存储大小，所需的可用磁盘空间将为94GB。