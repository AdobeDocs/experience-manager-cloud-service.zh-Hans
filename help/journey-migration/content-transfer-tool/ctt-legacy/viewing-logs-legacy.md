---
title: 在内容传输工具中查看迁移集的日志（旧版）
description: 在内容传输工具中查看迁移集的日志
hide: true
hidefromtoc: true
source-git-commit: 1fb4d0f2a3b3f9a27f5ab1228ec2d419149e0764
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 64%

---

# 查看迁移集的日志（旧版） {#view-logs-content-transfer-tool}

完成每个步骤（提取和摄取）后，检查日志并查找错误。  任何错误都应立即通过处理报告的问题或联系Adobe支持部门来解决。

## 查看日志的步骤 {#viewing-logs}

您可以从&#x200B;*概述*&#x200B;页面查看现有迁移集的日志。应遵循以下步骤：

1. 导航到&#x200B;*概述*&#x200B;页面并选择您要删除的迁移集，然后单击操作栏中的&#x200B;**查看日志**。

   ![图像](/help/journey-migration/content-transfer-tool/assets/view-log1.png)

1. 此时将显示&#x200B;**日志**&#x200B;对话框。单击&#x200B;**提取日志**，以在新选项卡中查看日志。

   ![图像](/help/journey-migration/content-transfer-tool/assets/view-log2.png)
或者，

   您还可以从&#x200B;*概述*&#x200B;屏幕上查看迁移集的日志。选择迁移集，然后单击&#x200B;**提取**&#x200B;字段下的状态。在此例中，单击&#x200B;**已完成**&#x200B;以在新选项卡中查看日志。

   ![图像](/help/journey-migration/content-transfer-tool/assets/view-log3.png)

1. 要在不使用用户界面的情况下跟踪日志，您可以通过 SSH 连接到源 AEM 环境并跟踪 `crx-quickstart/cloud-migration/extraction-XXXXX/output.log file`。
