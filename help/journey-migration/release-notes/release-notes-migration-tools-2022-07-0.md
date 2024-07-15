---
title: AEM as a Cloud Service 2022.7.0版中的迁移工具发行说明
description: AEM as a Cloud Service 2022.7.0版中的迁移工具发行说明
feature: Release Information
exl-id: bc8f1a80-867e-423a-9c03-4a53b1ebc57c
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 9%

---

# AEM as a Cloud Service 2022.7.0版中的迁移工具发行说明 {#release-notes}

此页概述了AEM as a Cloud Service 2022.7.0中的迁移工具的发行说明。

## Best Practices Analyzer {#bpa-release}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer v2.1.30的发布日期是2022年7月27日。

### 新增功能 {#what-is-new-bpa}

* BPA现在可以检测和报告可迁移的Lucene索引总大小，即Lucene索引总数（不包括`/oak:index/lucene`和`/oak:index/damAssetLucene`）。
* 在BPA中添加了新模式，用于检测和报告自定义i18n词典的使用情况。 Translator.html在AEM as a Cloud Service中不可用，必须通过Cloud Manager CI/CD管道从Git部署自定义i18n词典。

### 错误修复 {#bug-fixes-bpa}

* BPA报告内容片段缺少原始演绎版。 由于内容片段没有演绎版，因此现在为内容片段跳过此检查。
* BPA UI中缺少筛选ACS Commons查找结果的选项。 此问题已得到修复。

## 内容转移工具 {#ctt-release}

### 发布日期 {#release-date-ctt}

内容传输工具版本2.0.12的发布日期为2022年7月19日。

### 新增功能 {#what-is-new-ctt}

* 通过LDAP登录的用户现在可以在CTT中运行检查大小和用户映射功能。
* 为帮助在提取期间调试SSL/TLS连接问题，用户现在可以启用SSL日志记录。
* 为帮助调试源连接问题，当与Azure的连接失败时，子域名现在会显示在日志中。
* 为帮助调试预复制期间出现的问题，现在，当预复制失败时，会将AzCopy日志附加到提取日志。
* 为了避免过时的“检查大小”结果，用户只能在上一次完成“检查大小”后重新运行“检查大小”。

### 错误修复 {#bug-fixes-ctt}

* 删除并重新创建迁移集后出现之前的提取日志。 此问题已得到修复。
* 查看进度操作按钮不可用于状态为“已停止”的迁移集。 此问题已得到修复。
* 删除操作按钮不可用于具有过期提取密钥的迁移集。 此问题已得到修复。
* 修复了多个UI错误。

## Cloud Acceleration Manager {#cam-release}

### 发布日期 {#release-date-cam}

Cloud Acceleration Manager的发布日期是2022年7月15日。

### 新增功能 {#what-is-new-cam}

* Cloud Acceleration Manager现在为用户提供了手动检索迁移令牌的功能，以便能够在自动检索失败时开始引入。 如果客户设置了阻止CAM的IP允许列表，或者非管理员用户尝试开始引入，则自动检索可能会失败。 有关详细信息，请参阅[疑难解答](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#troubleshooting)。
* 为了方便使用，“迁移复杂性”页面上的长表格现在可以折叠。
