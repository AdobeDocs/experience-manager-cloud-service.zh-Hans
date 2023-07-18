---
title: AEMas a Cloud Service2023.07.0版中迁移工具的发行说明
description: AEMas a Cloud Service2022.07.0版中迁移工具的发行说明
feature: Release Information
exl-id: 2f787321-f156-480d-bbe8-1a6d04f110c5
source-git-commit: 88227693b7dfc3cbd30751718dc85e55ee67bb96
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 7%

---

# AEMas a Cloud Service2023.07.0版中迁移工具的发行说明 {#release-notes}

此页概述了AEMas a Cloud Service2022.07.0中迁移工具的发行说明。

## Best Practices Analyzer {#bpa-release}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer v2.1.42的发布日期是2023年7月6日。

### 新增功能 {#what-is-new-bpa}

* 向此版本的Best Practices Analyzer添加了多个最佳实践模式。 其中包括：
   * 确定最低维护任务配置
   * 检测长时间运行的/大量查询
   * 检测大量处于运行或陈旧状态的创作工作流
   * 检测OSGI Apache sling作业配置
   * 检测自定义Guava缓存

### 错误修复 {#bug-fixes-bpa}

* 改进了BPA，以防止出现内存不足报告生成失败。
* 改进了BPA以检测路径中的转义字符，以防止在将内容迁移到AEMas a Cloud Service时内容摄取失败。


