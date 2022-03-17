---
title: AEMas a Cloud Service版本2022.2.0中迁移工具的发行说明
description: AEMas a Cloud Service版本2022.2.0中迁移工具的发行说明
feature: Release Information
exl-id: b1cd871d-c71e-4902-a97e-2c859f6a4da4
source-git-commit: c497424271ea960d22a30b4a6c66432935ec820d
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 79%

---

# AEMas a Cloud Service版本2022.2.0中迁移工具的发行说明 {#release-notes}

本页概述了AEM 2022.2.0as a Cloud Service中迁移工具的发行说明。

## Best Practices Analyzer {#bpa-release}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer v2.1.24 的发布日期是 2022 年 2 月 1 日。

### 新增功能 {#what-is-new-bpa}

* 能够检测和报告带有和不带有智能标签的资源的数量。
* 能够检测和报告所使用的核心组件版本。
* 能够检测和报告执行 BPA 的源层的类型（创作或发布）。

### 错误修复 {#bug-fixes-bpa}

* BPA 大小调整逻辑变得更快、更高效。
* 在某些情况下，BPA 在运行时没有增加分析的计数。此问题已得到修复。

## 内容传输工具 {#ctt-release}

### 发布日期 {#release-date-ctt}

内容传输工具版本 1.8.6 的发布日期为 2022 年 2 月 3 日。

### 新增功能 {#what-is-new-ctt}

* 内容验证 - 用户能够可靠地确定内容传输工具提取的所有内容是否已成功引入到目标实例中。要使用此功能，您需要在源 AEM 环境的 `System Console` 中启用它。有关更多详细信息，请参阅[验证内容传输 - 快速入门](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/validating-content-transfers.html?lang=zh-Hans#getting-started)。

### 错误修复 {#bug-fixes-ctt}

* 某些用户未被映射，因为用户映射区分大小写。此问题已得到修复。用户映射不再区分大小写。
