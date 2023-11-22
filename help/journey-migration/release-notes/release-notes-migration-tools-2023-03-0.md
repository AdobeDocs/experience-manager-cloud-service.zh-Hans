---
title: AEMas a Cloud Service2023.03.0版中迁移工具的发行说明
description: AEMas a Cloud Service2023.03.0版中迁移工具的发行说明
feature: Release Information
exl-id: cdc57cca-e10a-4b0d-b803-910ccc9350a6
source-git-commit: d7e5a14c2dfee41b4ab5af733218fe58d17871fa
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 10%

---

# AEMas a Cloud Service2023.03.0版中迁移工具的发行说明 {#release-notes}

此页概述了AEMas a Cloud Service2023.03.0中迁移工具的发行说明。

## Best Practices Analyzer {#bpa-release}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer v2.1.40 的发布日期是 2023 年 3 月 03 日。

### 新增功能 {#what-is-new-bpa}

* BPA现在可以检测和报告冲突的节点 — 具有相同的节点的节点 `jcr:uuid`. 此类发现结果将标记为严重，因为在将内容移动到AEMas a Cloud Service时，它可能会导致内容摄取失败。
* BPA现在可以检测和报告事件侦听器的使用情况。 建议在迁移到AEMas a Cloud Service时，将此类型的事件处理机制重构为sling作业。

### 错误修复 {#bug-fixes-bpa}

* BPA报告了 `grouprendercondition`. 此问题已得到修复。

## 内容转移工具 {#ctt-release}

### 发布日期 {#release-date-ctt}

内容传输工具版本2.0.16的发布日期为2023年3月8日。

### 新增功能 {#what-is-new-ctt}

* 用户映射已得到简化并集成到内容提取步骤中。 无需进行设置，默认情况下，用户启动内容提取时会自动完成用户映射。 如果需要，用户可以选择禁用用户映射。 了解详情 [此处。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/user-mapping-and-migration.html?lang=en#user-mapping-detail)
* 预复制步骤，使用 [AzCopy](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) 已与内容传输工具集成，以显着加快内容提取。 安装此版本的CTT时，会自动配置和安装预复制。 默认情况下，在启动提取时，将对大于200 GB的迁移集自动运行预复制。 如果需要，用户可以选择禁用它。 了解详情 [此处。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en)
* CTT现在可以在Windows服务器上使用。

### 错误修复 {#bug-fixes-ctt}

* 修复了多个错误，以提高内容提取的可复原性。
