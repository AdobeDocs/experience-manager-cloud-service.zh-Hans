---
title: AEM as a Cloud Service 2023.07.0版中的迁移工具发行说明
description: AEM as a Cloud Service 2023.07.0版中的迁移工具发行说明
feature: Release Information
exl-id: 2f787321-f156-480d-bbe8-1a6d04f110c5
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 6%

---

# AEM as a Cloud Service 2023.07.0版中的迁移工具发行说明 {#release-notes}

此页概述了AEM as a Cloud Service 2023.07.0中迁移工具的发行说明。

## Best Practices Analyzer {#bpa-release}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer v2.1.42的发布日期是2023年7月6日。

### 新增功能 {#what-is-new-bpa}

* 多个最佳实践模式已添加到此最佳实践分析器的版本中。 其中包括：
   * 确定最低维护任务配置
   * 检测长时间运行的/大量查询
   * 检测大量处于运行或陈旧状态的创作工作流
   * 检测OSGI Apache sling作业配置
   * 检测自定义Guava缓存

### 错误修复 {#bug-fixes-bpa}

* 改进了BPA，以防止为发现大量结果的报告生成内存不足报告失败。
* 改进了BPA，可检测路径中的转义字符，以防止在将内容迁移到AEM as a Cloud Service时内容摄取失败。
