---
title: AEMas a Cloud Service版本2022.2.0中迁移工具的发行说明
description: AEMas a Cloud Service版本2022.2.0中迁移工具的发行说明
feature: Release Information
source-git-commit: 8876702f1a172282fd1ff46387ade2a45e187fed
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 7%

---


# AEMas a Cloud Service版本2022.2.0中迁移工具的发行说明 {#release-notes}

本页概述了AEM 2022.2.0as a Cloud Service中迁移工具的发行说明。

## Best Practices Analyzer {#bpa-release}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer v2.1.24的发布日期是2022年2月1日。

### 新增功能 {#what-is-new-bpa}

* 能够检测和报告具有和不具有智能标记的资产数量。
* 能够检测并报告所使用的核心组件版本。
* 能够检测并报告执行BPA的源层（创作或发布）类型。

### 错误修复 {#bug-fixes-bpa}

* BPA大小调整逻辑的制作速度更快、效率更高。
* 在某些情况下，BPA在运行时不会递增分析计数。 此问题已修复。

## 内容传输工具 {#ctt-release}

### 发布日期 {#release-date-ctt}

内容传输工具v1.8.6的发布日期是2022年2月3日。

### 新增功能 {#what-is-new-ctt}

* 内容验证 — 用户能够可靠地确定是否已将内容传输工具提取的所有内容成功摄取到目标实例。 要使用此功能，您需要在 `System Console` 源AEM环境的。 请参阅 [验证内容传输 — 快速入门](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/validating-content-transfers.html?lang=en#getting-started) 以了解更多详细信息。

### 错误修复 {#bug-fixes-ctt}

* 由于用户映射区分大小写，因此未映射某些用户。 此问题已修复。 用户映射不再区分大小写。

