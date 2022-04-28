---
title: AEMas a Cloud Service版本2022.3.0中迁移工具的发行说明
description: AEMas a Cloud Service版本2022.3.0中迁移工具的发行说明
feature: Release Information
exl-id: ab43605d-d46e-43de-b71f-fab610609550
source-git-commit: 87e3291b4a72c24fc6cf8df488df305f1a078ea5
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 86%

---

# AEMas a Cloud Service版本2022.3.0中迁移工具的发行说明 {#release-notes}

本页概述了AEM 2022.3.0as a Cloud Service中迁移工具的发行说明。

## Best Practices Analyzer {#bpa-release}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer v2.1.26 的发布日期是 2022 年 3 月 16 日。

### 新增功能 {#what-is-new-bpa}

* 能够监测未处理资源。如果检测到未处理资源，则需要将这些资源设置为已处理，或者在内容转移期间从迁移设置中删除这些资源，以避免在内容摄取期间遇到问题。
* 能够监测内容是否超过 1000 个虚名 URL。使用大量虚名 URL 不是最佳做法，因为它会给 Dispatcher 和 Publish 服务器带来负载。
* 能够识别 Oak 索引定义相关问题并检测与 AEM as a Cloud Service 兼容性。
* 能够检测和报告所使用的外部化程序配置。在 AEM as a Cloud Service 中，外部化程序配置由 Cloud Manager 设置，因此，需要重构现有的外部化程序配置以保持兼容性。

### 错误修复 {#bug-fixes-bpa}

* 在某些情况下，BPA 无法运行，因为 FormsSelectiveFeaturesAnalysis 抛出断言错误。此问题已得到修复。
* BPA 将与 WRK 模式相关的发现报告为 MAJOR 而非 CRITICAL。此问题已得到修复。
* BPA 错误地将 ui.apps 中与 OAK 索引定义有关的发现报告为 CRITICAL。此问题已得到修复。

## 内容传输工具 {#ctt-release}

### 发布日期 {#release-date-ctt}

内容传输工具版本 1.9.0 的发布日期为 2022 年 2 月 28 日。

### 新增功能 {#what-is-new-ctt}

* 检查“大小护栏” - 内容传输工具检查大小功能有助于减少失败的内容传输。使用检查大小功能，用户可以 1）在提取之前确定`crx-quickstart`子目录中是否有足够的磁盘空间，以及 2）估计迁移集大小并验证其是否受支持。如果违反了其中一项或两项检查，用户将在 CTT UI 中看到警告。有了这道护栏，您可以避免内容传输失败，并主动与 Adobe 客户关怀讨论迁移选项。有关更多详细信息，请参阅[“确定迁移集大小和磁盘空间”](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=zh-Hans#migration-set-size)。
