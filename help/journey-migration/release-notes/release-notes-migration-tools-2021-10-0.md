---
title: AEM as a Cloud Service 2021.10.0版中的迁移工具发行说明
description: AEM as a Cloud Service 2021.11.0版中的迁移工具发行说明
feature: Release Information
exl-id: 6b1caa63-dcb0-4c48-ab2c-fd72617abf13
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 11%

---

# AEM as a Cloud Service 2021.10.0版中的迁移工具发行说明 {#release-notes}

此页概述了AEM as a Cloud Service 2021.10.0中迁移工具的发行说明。

>[!NOTE]
>要查看 Adobe Experience Manager as a Cloud Service 的当前发行说明，请单击[此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/release-notes/release-notes-current.html)。

## Cloud Acceleration Manager {#cam-release}

### 发布日期 {#release-date-cam}

Cloud Acceleration Manager的发布日期为2021年10月25日。

### 新增功能 {#what-is-new-cam}

Cloud Acceleration Manager现在允许用户在趋势线报告中查看历史BPA报告。 通过此报表，用户能够以易于使用的图形表示形式查看他们所取得的进展。 有关更多详细信息，请参阅[使用查看趋势线](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-readiness-phase.html#trendline-view-cam)。

### 发布日期 {#release-date-october-cam}

Cloud Acceleration Manager的发布日期是2021年10月4日。

### 新增功能 {#what-is-new-cam-oct}

Cloud Acceleration Manager现在允许用户在可打印预览中查看BPA报告，并允许简单打印或打印以PDF以便于共享。 请参阅[使用最佳实践分析卡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-readiness-phase.html#best-practices-analysis)中的步骤6和步骤7。


## 内容转移工具 {#ctt-release}

### 发布日期 {#release-date-ctt-latest}

内容传输工具版本1.6.0的发布日期为2021年10月4日。

### 新增功能 {#what-is-new-ctt-oct}

* 改进了用户映射工具，简化了用户体验，包括以下列出的功能。 有关详细信息，请参阅[使用用户映射工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/legacy-user-mapping-tool/using-user-mapping-tool-legacy.html)。
   * 在运行用户映射之前测试与用户管理API的连接
   * 正常跳过错误并继续用户映射活动
   * 如果&#x200B;**访问令牌**&#x200B;在24小时后过期，则用户映射不再失败。 可以从上次停止的位置重新运行用户映射。

* 为了提高内容传输工具的稳健性，可以将内容一次摄取到创作实例或Publish实例。 有关更多详细信息，请参阅[内容传输工具快速入门](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=zh-Hans)。

* 当包含版本时，将自动包含路径`/var/audit`以迁移审核事件。

## Best Practices Analyzer {#best-practices-analyzer}

### 发布日期 {#release-date-bpa-latest}

Best Practices Analyzer v2.1.20的发布日期是2021年10月5日。

### 新增功能 {#what-is-new-bpa-oct}

* 能够检测和报告节点名称长度。

* 能够检测和报告索引总大小。

* 能够检测和报告缺少原始演绎版的资源。
