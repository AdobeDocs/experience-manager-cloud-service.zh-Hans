---
title: AEM as a Cloud Service 2021.12.0版中的迁移工具发行说明
description: AEM as a Cloud Service 2021.12.0版中的迁移工具发行说明
feature: Release Information
exl-id: 4155e1c0-cd40-4cbc-9d6c-b106d68a2db5
role: Admin
source-git-commit: 6719e0bcaa175081faa8ddf6803314bc478099d7
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 38%

---

# AEM as a Cloud Service 2021.12.0版中的迁移工具发行说明 {#release-notes}

此页概述了AEM as a Cloud Service 2021.12.0中迁移工具的发行说明。

>[!NOTE]
>
>请参阅[Adobe Experience Manager as a Cloud Service的最新发行说明](/help/release-notes/release-notes-cloud/release-notes-current.md)，了解最新的发行说明。

## Best Practices Analyzer {#bpa-release}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer v2.1.22 的发布日期是 2021 年 12 月 1 日。

### 新增功能 {#what-is-new-bpa}

* 能够检测和报告所使用的 ACS Commons 版本。
* 能够检测和报告一个组中用户和子组的数量。
* 能够检测和报告 MongoDB 中超过 16MB 的节点属性值。

### 错误修复 {#bug-fixes-bpa}

* 已改进对 Foundation 组件的检测来减少误报。
* 对于 AEM Forms 客户，已修复有关 `EMAIL_PDF_SUBMIT_ACTION` 在 AEM as a Cloud Service 中不可用的 BPA 消息。


## 内容转移工具 {#ctt-release}

### 发布日期 {#release-date-ctt}

内容传输工具版本1.7.10的发布日期为2021年12月8日。

### 新增功能 {#what-is-new-ctt}

* 已将切换添加到内容传输工具中的摄取阶段，以便允许用户在摄取期间禁用[预复制](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=zh-Hans)。 为获得最佳的摄取速度，对于小型迁移集或如果自上次摄取以来只添加了几个Blob，应禁用摄取期间的预复制。
* 用户映射已更新，以使用改进的用户管理API，允许一次获取2000个用户，显着提高了性能。
