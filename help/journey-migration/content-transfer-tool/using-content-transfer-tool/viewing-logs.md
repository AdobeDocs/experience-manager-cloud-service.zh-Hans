---
title: 在内容传输工具中查看迁移集的日志
description: 在内容传输工具中查看迁移集的日志
exl-id: aed1ac83-a2fb-425e-aca4-39cd0bb42fd3
feature: Migration
role: Admin
source-git-commit: e1089810b3bf3db0cc440bb397e5549ade6eac37
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 36%

---

# 查看迁移集的日志 {#view-logs-content-transfer-tool}


>[!CONTEXTUALHELP]
>id="aemcloud_ctt_logs"
>title="查看日志"
>abstract="提取或引入完毕后，检查日志中是否有任何错误/警告。应立即通过处理所报告的问题或联系 Adobe 支持部门而纠正任何错误。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html#troubleshooting" text="疑难解答"
>additional-url="https://helpx.adobe.com/cn/enterprise/using/support-for-experience-cloud.html" text="联系 Adobe 支持"

完成每个步骤（提取和摄取）后，检查日志并查找错误。  应立即通过处理所报告的问题或联系 Adobe 支持部门而纠正任何错误。

## 查看日志的步骤 {#viewing-logs}

### 提取日志

要查看提取日志，请转到源Adobe Experience Manager实例，然后选择所需的迁移集。

然后，执行以下步骤：

1. 选择一个迁移集，然后单击操作栏中的&#x200B;**查看日志**。 这将显示日志对话框。 单击&#x200B;**提取日志**&#x200B;以在新选项卡中查看日志。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/logs.png) \
   或者，单击&#x200B;**已完成**&#x200B;状态以在新选项卡中查看日志。

1. 要在不使用用户界面的情况下跟踪日志，您可以通过 SSH 连接到源 AEM 环境并跟踪 `crx-quickstart/cloud-migration/extraction-XXXXX/output.log file`。

### 摄取日志

要查看引入日志，请转到Cloud Acceleration Manager中的引入作业列表，然后找到所需的迁移作业并单击该作业的三个圆点(**...**)。 然后，您可以单击&#x200B;**下载日志**&#x200B;来下载日志。

![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam28.png)
