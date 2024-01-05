---
title: AEMas a Cloud Service2022.1.0版中迁移工具的发行说明
description: AEMas a Cloud Service2022.1.0版中迁移工具的发行说明
feature: Release Information
exl-id: cbd0c316-bda3-48fb-89d6-a8f97bad1970
source-git-commit: a77e5dc4273736b969e9a4a62fcac75664495ee6
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 6%

---

# AEMas a Cloud Service2022.1.0版中迁移工具的发行说明 {#release-notes}

此页概述了AEMas a Cloud Service2022.1.0中迁移工具的发行说明。

## 内容转移工具 {#ctt-release}

### 发布日期 {#release-date-ctt}

内容传输工具版本1.7.18的发布日期为2022年1月18日。

### 新增功能 {#what-is-new-ctt}

* 已将切换添加到内容传输工具中的提取阶段，以允许用户禁用 [预复制](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html) 提取期间。 为获得最佳提取速度，对于小型迁移集或如果自上次提取以来只添加了少量Blob，则应禁用提取期间的预复制。

### 错误修复 {#bug-fixes-ctt}

* 更新了默认配置以减少提取期间的执行超时。
