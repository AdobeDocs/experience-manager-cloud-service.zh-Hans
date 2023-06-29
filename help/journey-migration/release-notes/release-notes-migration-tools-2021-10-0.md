---
title: AEMas a Cloud Service2021.10.0版中迁移工具的发行说明
description: AEMas a Cloud Service2021.11.0版中迁移工具的发行说明
feature: Release Information
exl-id: 6b1caa63-dcb0-4c48-ab2c-fd72617abf13
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 14%

---

# AEMas a Cloud Service2021.10.0版中迁移工具的发行说明 {#release-notes}

此页概述了AEMas a Cloud Service2021.10.0中迁移工具的发行说明。

>[!NOTE]
>要查看 Adobe Experience Manager as a Cloud Service 的当前发行说明，请单击[此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/release-notes/release-notes-current.html)。

## Cloud Acceleration Manager {#cam-release}

### 发布日期 {#release-date-cam}

Cloud Acceleration Manager的发布日期是2021年10月25日。

### 新增功能 {#what-is-new-cam}

Cloud Acceleration Manager现在允许用户在趋势线报告中查看历史BPA报告。 通过此报告，用户能够以易于使用的图形表示形式查看他们所取得的进展。 参见 [使用视图趋势线](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=en#trendline-view-cam) 了解更多详细信息。

### 发布日期 {#release-date-october-cam}

Cloud Acceleration Manager的发布日期是2021年10月4日。

### 新增功能 {#what-is-new-cam-oct}

Cloud Acceleration Manager现在使用户能够在可打印的预览中查看BPA报告，从而允许简单打印或打印以PDF以便于共享。 请参阅中的步骤6和7 [使用最佳实践分析卡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=en#best-practices-analysis).


## 内容转移工具 {#ctt-release}

### 发布日期 {#release-date-ctt-latest}

内容传输工具版本1.6.0的发布日期为2021年10月4日。

### 新增功能 {#what-is-new-ctt-oct}

* 改进了用户映射工具，简化了用户体验，包括以下列出的功能。 有关更多详细信息，请参阅 [使用用户映射工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/legacy-user-mapping-tool/using-user-mapping-tool-legacy.html?lang=en).
   * 在运行用户映射之前测试与用户管理API的连接
   * 正常跳过错误并继续用户映射活动
   * 在以下情况下，用户映射不再失败 **访问令牌** 将在24小时后过期。 可以从上次停止的位置重新运行用户映射。

* 为了提高内容传输工具的稳健性，可以将内容一次摄取到创作实例或发布实例。 参见 [内容传输工具快速入门](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=zh-Hans) 了解更多详细信息。

* 当包含版本时，路径 `/var/audit` 将自动包含以迁移审核事件。

## Best Practices Analyzer {#best-practices-analyzer}

### 发布日期 {#release-date-bpa-latest}

Best Practices Analyzer v2.1.20的发布日期是2021年10月5日。

### 新增功能 {#what-is-new-bpa-oct}

* 能够检测和报告节点名称长度。

* 能够检测和报告索引总大小。

* 能够检测和报告缺少原始演绎版的资源。
