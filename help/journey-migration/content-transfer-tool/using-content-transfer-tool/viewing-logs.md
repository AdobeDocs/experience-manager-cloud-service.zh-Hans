---
title: 在内容传输工具中查看迁移集的日志
description: 在内容传输工具中查看迁移集的日志
exl-id: aed1ac83-a2fb-425e-aca4-39cd0bb42fd3
source-git-commit: 9a098eefbb730ae2930169cf7402ab4799043291
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 12%

---

# 查看迁移集的日志 {#view-logs-content-transfer-tool}


>[!CONTEXTUALHELP]
>id="aemcloud_ctt_logs"
>title="查看日志"
>abstract="提取摄取完成后，检查日志中是否存在任何错误/警告。 任何错误都应立即通过处理报告的问题或联系Adobe支持部门来解决。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#troubleshooting" text="疑难解答"
>additional-url="https://helpx.adobe.com/ca/enterprise/admin-guide.html/ca/enterprise/using/support-for-experience-cloud.ug.html" text="联系Adobe支持"

完成每个步骤（提取和摄取）后，检查日志并查找错误。  任何错误都应立即通过处理报告的问题或联系Adobe支持部门来解决。

## 查看日志的步骤 {#viewing-logs}

要查看提取日志，请转到源Adobe Experience Manager实例，然后选择所需的迁移集。

然后，执行以下步骤：

1. 选择迁移集并单击 **查看日志** 中。 此时将显示日志对话框。 单击 **提取日志** 可在新选项卡中查看日志。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam25.png) \
   或者，单击 **已完成** 状态，以在新选项卡中查看日志。

1. 要在不使用用户界面的情况下跟踪日志，您可以通过 SSH 连接到源 AEM 环境并跟踪 `crx-quickstart/cloud-migration/extraction-XXXXX/output.log file`。

1. 要查看摄取日志，请转到Cloud Acceleration Manager中的摄取作业列表，然后单击三个圆点(**...**)。 然后，您可以单击 **下载日志** 下载日志。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam28.png)
