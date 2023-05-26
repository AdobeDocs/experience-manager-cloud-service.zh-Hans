---
title: AEMas a Cloud Service2021.12.0版中迁移工具的发行说明
description: AEMas a Cloud Service2021.12.0版中迁移工具的发行说明
feature: Release Information
exl-id: 4155e1c0-cd40-4cbc-9d6c-b106d68a2db5
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 46%

---

# AEMas a Cloud Service2021.12.0版中迁移工具的发行说明 {#release-notes}

此页概述了AEMas a Cloud Service2021.12.0中迁移工具的发行说明。

>[!NOTE]
>要查看 Adobe Experience Manager as a Cloud Service 的当前发行说明，请单击[此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/aem-cloud-changes.html?lang=zh-Hans)。

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

* 已将切换添加到内容传输工具中的摄取阶段，以便允许用户禁用 [预复制](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) 摄取期间。 为获得最佳的摄取速度，对于小型迁移集或如果自上次摄取以来只添加了少量blob，应禁用摄取期间的预复制。
* 更新了用户映射以使用改进的用户管理API，从而一次可获得2000个用户，显着提高了性能。
