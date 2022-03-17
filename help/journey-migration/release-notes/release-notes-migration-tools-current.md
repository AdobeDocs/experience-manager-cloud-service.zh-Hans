---
title: AEMas a Cloud Service版本2022.3.0中迁移工具的发行说明
description: AEMas a Cloud Service版本2022.3.0中迁移工具的发行说明
feature: Release Information
source-git-commit: c497424271ea960d22a30b4a6c66432935ec820d
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 7%

---


# AEMas a Cloud Service版本2022.3.0中迁移工具的发行说明 {#release-notes}

本页概述了AEM 2022.3.0as a Cloud Service中迁移工具的发行说明。

## Best Practices Analyzer {#bpa-release}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer v2.1.26的发布日期是2022年3月16日。

### 新增功能 {#what-is-new-bpa}

* 能够检测未处理的资产。 如果检测到未处理的资产，则需要将这些资产设置为已处理，或需要在内容传输期间从迁移集中删除，以避免在内容摄取期间遇到问题。
* 能够检测内容中是否有1000个以上的虚URL。 使用大量虚URL不是最佳做法，因为它会给调度程序和发布服务器带来负载。
* 能够识别与Oak索引定义相关的问题并检测与AEMas a Cloud Service的不兼容性。
* 能够检测并报告外部器配置的使用情况。 在AEMas a Cloud Service外部器配置由Cloud Manager设置，因此需要重构现有外部器配置以保持兼容性。

### 错误修复 {#bug-fixes-bpa}

* 在某些情况下，由于FormsSelectiveFeaturesAnalysis引发断言错误，BPA无法运行。 此问题已得到修复。
* BPA报告与MAJOR而不是CRITICAL的工作模式有关的调查结果。 此问题已得到修复。
* BPA错误地将与ui.apps中的OAK索引定义相关的发现结果报告为关键。 此问题已得到修复。

## 内容传输工具 {#ctt-release}

### 发布日期 {#release-date-ctt}

内容传输工具v1.9.0的发布日期是2022年2月28日。

### 新增功能 {#what-is-new-ctt}

* 检查大小护栏 — 内容传输工具检查大小功能有助于减少失败的内容传输。  使用“检查大小”功能，用户可以1)确定他们在 `crx-quickstart` 提取前的子目录，以及2)估计迁移集大小并验证它是否受支持。 如果违反了这两项检查之一或两项，用户将在CTT UI中看到警告。 利用此护栏，您可以避免内容传输失败，并主动与Adobe客户关怀团队讨论迁移选项。 请参阅 [确定迁移集大小和磁盘空间](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en#migration-set-size) 以了解更多详细信息。