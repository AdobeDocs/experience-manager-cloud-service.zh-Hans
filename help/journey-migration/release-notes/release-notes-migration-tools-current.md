---
title: AEMas a Cloud Service版本2022.9.0中迁移工具的发行说明
description: AEMas a Cloud Service版本2022.9.0中迁移工具的发行说明
feature: Release Information
source-git-commit: 6b58b253c554fc2958fdff2b246f341f56b1639f
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 10%

---

# AEMas a Cloud Service版本2022.9.0中迁移工具的发行说明 {#release-notes}

本页概述了AEM 2022.9.0as a Cloud Service中迁移工具的发行说明。

## Best Practices Analyzer {#bpa-release}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer v2.1.34的发布日期是2022年9月12日。

### 新增功能 {#what-is-new-bpa}

* 现在，BPA可以检测并报告客户是否已添加自定义日志记录器配置。 AEMas a Cloud Service不支持自定义日志文件。 所有日志文件都需要通过管道传输到 `error.log`
* BPA现在可以报告客户存储库中存在的不同二进制MIME类型以及与这些类型关联的计数。

### 错误修复 {#bug-fixes-bpa}

* 在单一模式下显示大量发现结果时，BPA UI出现呈现问题。 此问题已得到修复。
* BPA错误地将某些发现报告为严重性为不兼容的更改。 此问题已得到修复。