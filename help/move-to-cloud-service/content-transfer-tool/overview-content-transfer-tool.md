---
title: 内容传输工具概述
description: 内容传输工具概述
translation-type: tm+mt
source-git-commit: 0ab2631dc5ae67a50522b3a6b29d1cb4c674d193
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 0%

---


# 概述 {#overview-content-transfer-tool}

内容传输工具是Adobe开发的工具，可用于将现有内容从源AEM实例（内部部署或AMS）移至目标AEM云服务实例。

此工具还自动传输承担者（用户或用户组）。

内容传输有两个相关阶段：

1. **提取**:  提取是指从源AEM实例将内容提取到称为迁移集的临 *时区域*。 迁 *移集* 是Adobe提供的一个云存储区，用于临时存储源AEM实例与云服务AEM实例之间传输的内容。

   有关更多 [详细信息，请参阅内容传输](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#extraction-process) 中的提取流程。

2. **摄取**: 摄取是指将迁移集中的内 *容引入* 目标云服务实例中。

   有关更多 [详细信息，请参阅内容传输](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#ingestion-process) 中的摄取过程。

迁移 *集具有* 以下属性：

* 在内容传输活动，最多一次可创建和维护四个迁移集。
* 每个迁移集都应有唯一的名称。
* 如果迁移集已停用超过30天，则将自动删除该迁移集。
* 每次创建迁移集时，它都与特定环境关联。 您只能将同一环境的作者或发布实例引入。

内容传输工具具有支持不同内容的上调功能，在该功能中，仅传输自上一内容传输活动以来所做的更改。

>[!NOTE]
> 初始内容传输后，建议在云服务上线之前，对不同内容进行频繁的补充，以缩短最终差异内容传输的内容冻结时间。

在提取阶段，要 ***补充现有*** 迁移集，必须 *禁用覆盖* 选项。 有关更多 [详细信息](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#top-up-extraction-process) ，请参阅“Top Up”提取。

在摄取阶段，要在当前内容上应用增量内容，必须禁 *用* “擦除”选项。 有关更多 [详细信息](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#top-up-ingestion-process) ，请参阅Top Up Ingestion。


## 准则和最佳实践 {#best-practices}

请按照以下部分了解使用内容传输工具的指南和最佳实践：

* 最好先在存储库上运行压缩、数据存储一致性检查，以发现潜在问题，并减少存储库中存在的垃圾。

* 如果将AEM Cloud作者内容投放网络(CDN)配置配置为包含IP的白名单，则应确保将源环境IP也添加到白名单中，以便源环境和AEM Cloud环境可以相互通信。

* 在摄取阶段，建议使用启用的擦除模式 *运行摄取* ，该模式将完全删除目标AEM云服务环境中的现有存储库（作者或发布），然后使用迁移集数据进行更新。 此模式比非划出模式快得多，在非划出模式下，迁移集将应用于当前内容的顶部。

* 内容传输活动完成后，云服务环境中需要正确的项目结构，以确保内容在云服务环境中成功呈现。

* 运行内容传输工具之前，必须确保源AEM实例的子目录中 `crx-quickstart` 有足够的磁盘空间。 这是因为内容传输工具创建了存储库的本地副本，稍后将其上传到迁移集。
计算所需可用磁盘空间的一般公式如下：
   *数据存储大小+节点存储大小* 1.5*

   * 对于数 *据存储大小*，内容传输工具使用64 GB，即使实际数据存储空间更大。
   * 节 *点存储大小* ，是段存储目录大小或MongoDB数据库大小。
因此，对于20GB的区段存储大小，所需的可用磁盘空间将为94GB。