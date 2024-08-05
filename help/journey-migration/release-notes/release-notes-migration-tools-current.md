---
title: AEM as a Cloud Service 2024.07版中的迁移工具发行说明
description: AEM as a Cloud Service 2024.07.0版中的迁移工具发行说明
feature: Release Information
exl-id: 52709511-eab2-47a7-8bea-1b707cd568a1
role: Admin
source-git-commit: 4f01ca0076248442fe93161bbc8b98bffb64551b
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 8%

---

# AEM as a Cloud Service 2024.07.0版中的迁移工具发行说明 {#release-notes}

此页概述了AEM as a Cloud Service 2024.07.0中迁移工具的发行说明。

## 内容转移工具 {#ctt-release}

### 发布日期 {#release-date-ctt}

内容传输工具版本3.0.16的发布日期为2024年7月。

### 新增功能 {#what-is-new-ctt}

* 发生故障时自动上传CTT提取日志。
* 现在，用户在续订提取密钥后可以成功执行摄取。
* 添加了对使用Azure访问密钥和密钥与AzureDataStore一起执行CTT提取的支持。
* 现在，当使用无效密钥创建迁移集时，用户将收到正确的错误消息。

## Best Practices Analyzer {#bpa-release}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer v2.1.50的发布日期是2024年5月。

### 错误修复 {#bug-fixes-bpa}

* Best Practices Analyzer现在可检测大于16MB的所有节点
* 已修复导致偶尔发生NCC结果的竞争条件。
