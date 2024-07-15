---
title: AEM as a Cloud Service 2023.09.0版中的迁移工具发行说明
description: AEM as a Cloud Service 2023.09.0版中的迁移工具发行说明
feature: Release Information
exl-id: 484a60d4-a439-43d6-a23e-4a3b45ef4160
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 4%

---

# AEM as a Cloud Service 2023.09.0版中的迁移工具发行说明 {#release-notes}

此页概述了AEM as a Cloud Service 2023.09.0中迁移工具的发行说明。

## 内容转移工具 {#ctt-release}

### 发布日期 {#release-date-ctt}

内容传输工具版本3.0.0的发布日期为2023年9月7日。

### 新增功能 {#what-is-new-ctt}

内容传输工具已得到改进，可提供以下优势：

* 通过使用AzCopy仅复制所需的blob id而不是复制所有blob id来迁移内容存储库的子集时缩短了传输时间。
* 使用Oak升级更快地实现差异内容增补。
* 通过将索引过程与内容摄取过程分离开来，提高了稳健性。 如果索引失败，则不必再次摄取内容。 只有索引会自动重新启动，从而节省大量时间和精力。
