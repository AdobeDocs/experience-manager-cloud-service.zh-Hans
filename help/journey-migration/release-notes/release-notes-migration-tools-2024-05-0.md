---
title: AEM as a Cloud Service 2024.05.0版中的迁移工具发行说明
description: AEM as a Cloud Service 2024.05.0版中的迁移工具发行说明
feature: Release Information
role: Admin
exl-id: f50a74fa-ad7d-4837-b0a1-9945c32af02f
source-git-commit: 3b2ed44b438fe8587a9b9603ddfacc41111fb903
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 6%

---

# AEM as a Cloud Service 2024.05.0版中的迁移工具发行说明 {#release-notes}

此页概述了AEM as a Cloud Service 2024.05.0中迁移工具的发行说明。

## Best Practices Analyzer {#bpa-release}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer v2.1.50的发布日期是2024年5月。

### 新增功能 {#what-is-new-bpa}

* Best Practices Analyzer (BPA)现在支持将BPA生成的报告直接自动上传到Cloud Acceleration Manager (CAM)。 用户不再需要手动下载报告并将其上传到CAM。 有关更多详细信息，请参阅[使用最佳实践分析器](/help/journey-migration/best-practices-analyzer/using-best-practices-analyzer.md)

### 错误修复 {#bug-fixes-bpa}

* Best Practices Analyzer现在可检测大于16MB的所有节点
* 已修复导致偶尔发生NCC结果的竞争条件。

## Cloud Acceleration Manager {#cam-release}

### 新增功能 {#what-is-new-cam}

* Cloud Acceleration Manager (CAM)现在支持将BPA生成的报表自动直接上传到CAM。 要了解更多信息，请参阅Cloud Acceleration Manager中的[准备阶段 — 使用最佳实践Analysis卡](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#best-practices-analysis)

* Cloud Acceleration Manager现在提供了摄取可能需要多长时间的估计值，具体取决于节点数、数据存储大小等因素。 通过[将内容摄取到Cloud Service](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md)了解详情
