---
title: AEMas a Cloud Service2023.03.0版中迁移工具的发行说明
description: AEMas a Cloud Service2022.03.0版中迁移工具的发行说明
feature: Release Information
exl-id: 2f787321-f156-480d-bbe8-1a6d04f110c5
source-git-commit: 5815dacd2806cc7886aa0c7c5c9fd329306b3e1b
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 15%

---

# AEMas a Cloud Service2023.03.0版中迁移工具的发行说明 {#release-notes}

此页概述了AEMas a Cloud Service2022.03.0中迁移工具的发行说明。

## Best Practices Analyzer {#bpa-release}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer v2.1.40 的发布日期是 2023 年 3 月 03 日。

### 新增功能 {#what-is-new-bpa}

* BPA现在可以检测和报告冲突的节点 — 具有相同的节点的节点 `jcr:uuid`. 此类发现结果会被标记为严重，因为在将内容移动到AEMas a Cloud Service时，它可能会导致内容摄取失败。
* BPA现在可以检测和报告事件侦听器的使用情况。 迁移到AEMas a Cloud Service时，建议将此类型的事件处理机制重构为Sling作业。

### 错误修复 {#bug-fixes-bpa}

* BPA报告 `grouprendercondition`. 此问题已得到修复。