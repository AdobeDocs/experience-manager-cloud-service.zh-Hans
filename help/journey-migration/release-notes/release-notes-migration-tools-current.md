---
title: AEMas a Cloud Service版本2022.7.0中迁移工具的发行说明
description: AEMas a Cloud Service版本2022.7.0中迁移工具的发行说明
feature: Release Information
exl-id: 2f787321-f156-480d-bbe8-1a6d04f110c5
source-git-commit: ad9edf7bc164ea7e03496680dff8df6d1ebe266a
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 9%

---

# AEMas a Cloud Service版本2022.7.0中迁移工具的发行说明 {#release-notes}

本页概述了AEM 2022.7.0as a Cloud Service中迁移工具的发行说明。

## Best Practices Analyzer {#bpa-release}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer v2.1.30的发布日期是2022年7月27日。

### 新增功能 {#what-is-new-bpa}

* BPA现在可以检测并报告可迁移的Lucene索引总大小，即Total Lucene Index，不包括 `/oak:index/lucene` 和 `/oak:index/damAssetLucene`.
* 在BPA中添加了新模式，用于检测和报告自定义i18n词典的使用情况。 AEMas a Cloud Service中不提供Translator.html，自定义i18n词典需要通过Cloud Manager CI/CD管道从Git部署。

### 错误修复 {#bug-fixes-bpa}

* BPA报告内容片段缺少原始呈现版本。 由于内容片段没有呈现版本，因此现在已跳过此内容片段检查。
* BPA UI中缺少筛选ACS Commons发现结果的选项。 此问题已得到修复。

## 内容传输工具 {#ctt-release}

### 发布日期 {#release-date-ctt}

内容传输工具v2.0.12的发布日期是2022年7月19日。

### 新增功能 {#what-is-new-ctt}

* 现在，通过LDAP登录的用户能够在CTT中运行检查大小和用户映射功能。
* 为帮助调试提取期间的SSL/TLS连接问题，用户现在可以启用SSL日志记录。
* 为帮助调试源连接问题，现在，当与Azure的连接失败时，日志中会打印子域名。
* 为帮助调试预复制过程中出现的问题，在预复制失败时，AzCopy日志现在会附加到提取日志中。
* 为避免出现过时的“检查大小”结果，用户只有在完成之前的“检查大小”后才能重新运行“检查大小”。

### 错误修复 {#bug-fixes-ctt}

* 以前的提取日志在删除和重新创建迁移集后显示。 此问题已得到修复。
* “查看进度”操作按钮对于状态为“已停止”的迁移集不可用。 此问题已得到修复。
* 删除操作按钮对于提取键值已过期的迁移集不可用。 此问题已得到修复。
* 修复了多个UI错误。

## Cloud Acceleration Manager {#cam-release}

### 发布日期 {#release-date-cam}

Cloud Acceleration Manager的发布日期是2022年7月15日。

### 新增功能 {#what-is-new-cam}

* Cloud Acceleration Manager现在为用户提供了手动检索迁移令牌，以便在自动检索失败时能够启动摄取。 如果客户设置了阻止CAM的IP允许列表，或者非管理员用户尝试启动摄取，则自动检索可能会失败。 请参阅 [疑难解答](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#troubleshooting) 以了解更多信息。
* 现在，“迁移复杂性”页面上的长表可以折叠，以便于使用。
