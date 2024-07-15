---
title: AEM as a Cloud Service 2023.06.0版中的迁移工具发行说明
description: AEM as a Cloud Service 2023.06.0版中的迁移工具发行说明
feature: Release Information
exl-id: 021b7472-d1e4-4ef6-a040-c612fed8d3c3
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 3%

---

# AEM as a Cloud Service 2023.06.0版中的迁移工具发行说明 {#release-notes}

此页概述了AEM as a Cloud Service 2023.06.0中迁移工具的发行说明。

## 内容转移工具 {#ctt-release}

### 发布日期 {#release-date-ctt}

内容传输工具版本2.0.20的发布日期为2023年6月8日。

### 新增功能 {#what-is-new-ctt}

* 新的迁移工具 — 内容转换器(CT)已与此版本中的内容传输工具(CTT)集成。 在将内容从当前的AEM实施(内部部署或Managed Services)迁移到AEM as a Cloud Service之前，内容转换器可以自动检测和修复[最佳实践分析器(BPA)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=zh-Hans)报告的内容相关问题。
内容转换器提供的好处包括：
   * 故障保护：内容转换器每次对存储库进行修改以修复问题时，都会创建一个包。 如果需要，可以通过安装包恢复到以前的状态。
   * 易于使用： Content Transformer已与Content Transfer Tool集成，并附带简单直观的用户界面。
   * 节省时间：当大量内容问题属于一种模式类别时，您可以通过使用Content Transformer单击几次来解决所有问题，从而显着减少时间和迁移复杂性。
