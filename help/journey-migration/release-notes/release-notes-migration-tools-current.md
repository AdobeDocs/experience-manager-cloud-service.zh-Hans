---
title: AEM as a Cloud Service 2024.09版中的迁移工具发行说明
description: AEM as a Cloud Service 2024.09.0版中的迁移工具发行说明
feature: Release Information
exl-id: 52709511-eab2-47a7-8bea-1b707cd568a1
role: Admin
source-git-commit: 0c16f264826a46907afc33c91a021e7696f5b7a8
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 7%

---

# AEM as a Cloud Service 2024.09.0版中的迁移工具发行说明 {#release-notes}

此页概述了AEM as a Cloud Service 2024.09.0中迁移工具的发行说明。

## 内容转移工具 {#ctt-release}

### 发布日期 {#release-date-ctt}

内容传输工具版本3.0.20的发布日期为2024年8月28日。

### 新增功能 {#what-is-new-ctt}

* 此版本不再摄取用户，因此用户映射可选功能已被删除。
* 添加了OSGI配置选项，以在提取和引入期间禁用或启用主体迁移（默认设置是启用它）

### 错误修复 {#bug-fixes-ctt}

* 改进了CTT，以防止在azcopy配置中取消保护密钥时出错
* CTT现在可以正常处理在验证阶段复制AzCopy日志时产生的任何错误
* 更改在提取过程中创建的Azcopy日志目录

## Best Practices Analyzer {#bpa-release}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer v2.1.52的发布日期是2024年9月4日

### 新增功能 {#what-is-new-bpa}

* 针对AEM中基于JCR的事件检测提出了一种新的模式

### 错误修复 {#bug-fixes-bpa}

* 修复的误报
* 提高了处理来自Dispatcher的重定向响应的稳健性
* 修复了/apps/wcm/core/resources/languages/下所有语言的NCC调查结果未报告的问题
* 添加了检测节点的多属性是否没有值的检查

