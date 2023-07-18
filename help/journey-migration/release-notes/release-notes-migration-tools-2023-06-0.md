---
title: AEMas a Cloud Service2023.06.0版中迁移工具的发行说明
description: AEMas a Cloud Service2022.06.0版中迁移工具的发行说明
feature: Release Information
source-git-commit: 88227693b7dfc3cbd30751718dc85e55ee67bb96
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 2%

---

# AEMas a Cloud Service2023.06.0版中迁移工具的发行说明 {#release-notes}

此页概述了AEMas a Cloud Service2022.06.0中迁移工具的发行说明。

## 内容转移工具 {#ctt-release}

### 发布日期 {#release-date-ctt}

内容传输工具版本2.0.20的发布日期是2023年6月8日。

### 新增功能 {#what-is-new-ctt}

* 新的迁移工具 — 内容转换器(CT)已与此版本中的内容传输工具(CTT)集成。 内容转换器可以自动检测并修复由报告的相关内容问题。 [Best Practices Analyzer (BPA)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en) 在将内容从当前AEM实施(内部部署或Managed Services)迁移到AEMas a Cloud Service之前。
内容转换器提供的好处包括：
   * 故障保护：内容转换器每次对存储库进行修改以修复问题时，都会创建一个包。 如果需要，可以通过安装包恢复为以前的状态。
   * 易于使用： Content Transformer已与Content Transfer Tool集成，并带有直观的简单用户界面。
   * 节省时间：当大量内容问题属于一种模式类别时，只需几次单击即可使用Content Transformer解决所有这些问题，从而显着减少时间和迁移复杂性。
