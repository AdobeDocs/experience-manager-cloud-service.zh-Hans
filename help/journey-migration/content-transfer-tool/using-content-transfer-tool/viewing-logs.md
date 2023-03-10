---
title: 在内容传输工具中查看迁移集的日志
description: 在内容传输工具中查看迁移集的日志
exl-id: aed1ac83-a2fb-425e-aca4-39cd0bb42fd3
source-git-commit: fac037b59753ba1de960df47311c1febc2059d27
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 12%

---

# 查看迁移集的日志 {#view-logs-content-transfer-tool}


>[!CONTEXTUALHELP]
>id="aemcloud_ctt_logs"
>title="查看日志"
>abstract="提取提取完成后，检查日志中是否有任何错误/警告。 应立即解决任何错误，方法是处理报告的问题或联系Adobe支持。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html#troubleshooting" text="疑难解答"
>additional-url="https://helpx.adobe.com/ca/enterprise/admin-guide.html/ca/enterprise/using/support-for-experience-cloud.ug.html" text="联系 Adobe 支持"

完成每个步骤（提取和摄取）后，检查日志并查找错误。  应立即解决任何错误，方法是处理报告的问题或联系Adobe支持。

## 查看日志的步骤 {#viewing-logs}

### 提取日志

要查看提取日志，请转到源Adobe Experience Manager实例，然后选择所需的迁移集。

然后，执行以下步骤：

1. 选择一个迁移集并单击 **查看日志** 操作栏中的。 这将显示“日志”对话框。 单击 **提取日志** 以在新选项卡中查看日志。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam25.png) \
   或者，单击 **已完成** 状态，以在新选项卡中查看日志。

1. 要在不使用用户界面的情况下跟踪日志，您可以通过 SSH 连接到源 AEM 环境并跟踪 `crx-quickstart/cloud-migration/extraction-XXXXX/output.log file`。

### 摄取日志

要查看摄取日志，请转到Cloud Acceleration Manager中的摄取作业列表，然后找到所需的迁移作业并单击三个圆点(**...**)。 然后，您可以单击 **下载日志** 以下载日志。

![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam28.png)
