---
title: AEMas a Cloud Service版本2022.1.0中迁移工具的发行说明
description: AEMas a Cloud Service版本2022.1.0中迁移工具的发行说明
feature: Release Information
source-git-commit: 45520a55958030fa053491b921e70da18b16377f
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 6%

---


# AEMas a Cloud Service版本2022.1.0中迁移工具的发行说明 {#release-notes}

本页概述了AEM 2022.1.0as a Cloud Service中迁移工具的发行说明。

## 内容传输工具 {#ctt-release}

### 发布日期 {#release-date-ctt}

内容传输工具v1.7.18的发布日期是2022年1月18日。

### 新增功能 {#what-is-new-ctt}

* 切换添加到内容传输工具中的提取阶段，以允许用户禁用 [预拷贝](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) 提取期间。 为了获得最佳提取速度，对于较小的迁移集，或者自上次提取后仅添加了几个Blob，应在提取期间禁用预复制。

### 错误修复 {#bug-fixes-ctt}

* 更新了默认配置，以减少提取期间的执行超时。

