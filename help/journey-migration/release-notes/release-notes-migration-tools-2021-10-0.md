---
title: AEMas a Cloud Service版本2021.10.0中迁移工具的发行说明
description: AEMas a Cloud Service版本2021.11.0中迁移工具的发行说明
feature: Release Information
exl-id: 6b1caa63-dcb0-4c48-ab2c-fd72617abf13
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 8%

---

# AEMas a Cloud Service版本2021.10.0中迁移工具的发行说明 {#release-notes}

本页概述了AEM 2021.10.0中迁移工具的发行说明。

>[!NOTE]
>要查看最新的Adobe Experience Manager as a Cloud Service发行说明，请单击 [此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html).

## Cloud Acceleration Manager {#cam-release}

### 发布日期 {#release-date-cam}

Cloud Acceleration Manager的发布日期是2021年10月25日。

### 新增功能 {#what-is-new-cam}

Cloud Acceleration Manager现在为用户提供了在趋势线报表中查看历史BPA报表的功能。 通过此报表，用户可以以易于使用的图形表示形式查看自己取得的进展。 请参阅 [使用查看趋势线](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=en#trendline-view-cam) 以了解更多详细信息。

### 发布日期 {#release-date-october-cam}

Cloud Acceleration Manager的发布日期是2021年10月4日。

### 新增功能 {#what-is-new-cam-oct}

Cloud Acceleration Manager现在为用户提供了以可打印预览方式查看BPA报表的功能，从而允许简单的打印或打印以PDF以方便共享。 请参阅 [使用最佳实践分析卡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=en#best-practices-analysis).


## 内容传输工具 {#ctt-release}

### 发布日期 {#release-date-ctt-latest}

内容传输工具v1.6.0的发布日期是2021年10月4日。

### 新增功能 {#what-is-new-ctt-oct}

* 通过简化的用户体验改进了用户映射工具，其中包括以下功能。 有关更多详细信息，请参阅 [使用用户映射工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/user-mapping-tool/using-user-mapping-tool.html).
   * 在运行用户映射之前，测试与用户管理API的连接
   * 优雅地跳过错误并继续“用户映射”活动
   * 如果 **访问令牌** 24小时后过期。 可以从上次停止的位置重新运行用户映射。

* 为了提高内容传输工具的稳健性，可以一次将内容摄取到创作实例或发布实例。 请参阅 [内容传输工具快速入门](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en) 以了解更多详细信息。

* 包含版本时，路径 `/var/audit` 会自动包含在内以迁移审核事件。

## Best Practices Analyzer {#best-practices-analyzer}

### 发布日期 {#release-date-bpa-latest}

Best Practices Analyzer v2.1.20的发布日期是2021年10月5日。

### 新增功能 {#what-is-new-bpa-oct}

* 能够检测并报告节点名称长度。

* 能够检测并报告总索引大小。

* 能够检测并报告缺少其原始演绎版的资产。
