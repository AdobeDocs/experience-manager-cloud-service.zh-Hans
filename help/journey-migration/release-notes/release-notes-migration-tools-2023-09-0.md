---
title: AEMas a Cloud Service2023.09.0版中迁移工具的发行说明
description: AEMas a Cloud Service2022.09.0版中迁移工具的发行说明
feature: Release Information
exl-id: 52709511-eab2-47a7-8bea-1b707cd568a1
source-git-commit: c89ca7320d8f31d2545cadf98f39e577337b8918
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 4%

---

# AEMas a Cloud Service2023.09.0版中迁移工具的发行说明 {#release-notes}

此页概述了AEMas a Cloud Service2022.09.0中迁移工具的发行说明。

## 内容转移工具 {#ctt-release}

### 发布日期 {#release-date-ctt}

内容传输工具版本3.0.0的发布日期为2023年9月7日。

### 新增功能 {#what-is-new-ctt}

内容传输工具已得到显着改进，可提供以下优势：
* 利用AzCopy仅复制所需的blob id而不是复制所有blob id，在迁移内容存储库的子集时缩短了传输时间
* 使用Oak-upgrade更快地实现差异内容增补
* 通过将索引过程与内容摄取过程分离开来，提高了稳健性。 如果索引失败，则不必再次摄取内容。 只有索引会自动重新启动，从而节省大量时间和精力
