---
title: AEMas a Cloud Service版本2021.12.0中迁移工具的发行说明
description: AEMas a Cloud Service版本2021.12.0中迁移工具的发行说明
feature: Release Information
source-git-commit: 58dcf083ebf4cd2546213ba574f0f9c547aef008
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 7%

---


# AEMas a Cloud Service版本2021.12.0中迁移工具的发行说明 {#release-notes}

本页概述了AEM 2021.12.0中迁移工具的发行说明。

>[!NOTE]
>要查看最新的Adobe Experience Manager as a Cloud Service发行说明，请单击 [此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=zh-Hans).

## Best Practices Analyzer {#bpa-release}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer v2.1.22的发布日期是2021年12月1日。

### 新增功能 {#what-is-new-bpa}

* 能够检测并报告所使用的ACS Commons版本。
* 能够检测并报告群组中的用户和子群组的数量。
* 能够检测并报告MongoDB中超过16MB的节点属性值。

### 错误修复 {#bug-fixes-bpa}

* 对基础组件的检测进行了细化，以减少漏报。
* 对于AEM Forms客户，与 `EMAIL_PDF_SUBMIT_ACTION` 已修复在AEMas a Cloud Service上不可用的问题。


## 内容传输工具 {#ctt-release}

### 发布日期 {#release-date-ctt}

内容传输工具v1.7.10的发布日期是2021年12月8日。

### 新增功能 {#what-is-new-ctt}

* 在内容传输工具的摄取阶段添加切换以允许用户禁用 [预拷贝](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) 在摄取期间。 为了获得最佳摄取速度，对于较小的迁移集，或者自上次摄取后仅添加了几个Blob，应禁用摄取期间的预复制。
* 更新了用户映射，以使用经过改进的用户管理API，该API可以同时吸引2000个用户，从而显着提升性能。
