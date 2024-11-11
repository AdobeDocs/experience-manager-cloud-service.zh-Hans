---
title: AEM as a Cloud Service 版本 2024.09 中的迁移工具发行说明
description: AEM as a Cloud Service 版本 2024.09.0 中的迁移工具发行说明
feature: Release Information
exl-id: 52709511-eab2-47a7-8bea-1b707cd568a1
role: Admin
source-git-commit: 0c16f264826a46907afc33c91a021e7696f5b7a8
workflow-type: ht
source-wordcount: '230'
ht-degree: 100%

---

# AEM as a Cloud Service 版本 2024.09.0 中的迁移工具发行说明 {#release-notes}

本页概述了 AEM as a Cloud Service 2024.09.0 中迁移工具的发行说明。

## 内容转移工具 {#ctt-release}

### 发布日期 {#release-date-ctt}

内容转移工具版本 v3.0.20 的发布日期为 2024 年 8 月 28 日。

### 新增功能 {#what-is-new-ctt}

* 此版本将不再收錄用户，因此用户映射可选功能已被删除。
* 添加了 OSGI 配置选项，以禁用或启用提取和提取期间的主体迁移（默认设置是启用它）

### 错误修复 {#bug-fixes-ctt}

* CTT 已得到改进，以防止在 azcopy 配置中取消保护密钥时出现错误
* CTT 现在可以在验证阶段复制 AzCopy 日志时妥善处理任何错误
* 更改提取过程中创建的 azcopy 日志目录

## Best Practices Analyzer {#bpa-release}

### 发布日期 {#release-date-bpa}

最佳做法分析器 v2.1.52 的发布日期是 2024 年 9 月 4 日。

### 新增功能 {#what-is-new-bpa}

* 引入了一种新图案来检测 AEM 中基于 JCR 的事件

### 错误修复 {#bug-fixes-bpa}

* 修复误报
* 提高了处理 Dispatcher 重定向响应的稳健性
* 修复了 /apps/wcm/core/resources/languages/下所有语言的 NCC 发现未报告的问题
* 添加了检查以检测节点的多个属性是否没有值

