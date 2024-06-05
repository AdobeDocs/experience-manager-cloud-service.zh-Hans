---
title: AEMas a Cloud Service2022.9.0版中迁移工具的发行说明
description: AEMas a Cloud Service2022.9.0版中迁移工具的发行说明
feature: Release Information
exl-id: 581370ba-e3e8-487e-af83-a1eacbda2763
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 10%

---

# AEMas a Cloud Service2022.9.0版中迁移工具的发行说明 {#release-notes}

此页概述了AEMas a Cloud Service2022.9.0中迁移工具的发行说明。

## Best Practices Analyzer {#bpa-release}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer v2.1.34的发布日期是2022年9月12日。

### 新增功能 {#what-is-new-bpa}

* BPA现在可以检测和报告客户是否已添加自定义记录器配置。 AEMas a Cloud Service不支持自定义日志文件。 所有日志文件都需要管道传输到 `error.log`
* BPA现在可以报告客户存储库中存在的不同二进制MIME类型以及与其关联的计数。

### 错误修复 {#bug-fixes-bpa}

* 在单个模式下显示大量发现时，BPA UI出现呈现问题。 此问题已得到修复。
* BPA错误地报告了一些发现为与严重性不兼容的更改。 此问题已得到修复。
