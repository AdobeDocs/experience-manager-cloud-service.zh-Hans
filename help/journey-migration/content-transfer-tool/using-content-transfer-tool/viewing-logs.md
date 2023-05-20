---
title: 在內容轉移工具中檢視移轉集記錄
description: 在內容轉移工具中檢視移轉集記錄
exl-id: aed1ac83-a2fb-425e-aca4-39cd0bb42fd3
source-git-commit: 9d236e459f13fec6f0aaf80f588d20760636b9bb
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 39%

---

# 查看迁移集的日志 {#view-logs-content-transfer-tool}


>[!CONTEXTUALHELP]
>id="aemcloud_ctt_logs"
>title="查看日志"
>abstract="提取或引入完毕后，检查日志中是否有任何错误/警告。应立即通过处理所报告的问题或联系 Adobe 支持部门而纠正任何错误。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html#troubleshooting" text="疑难解答"
>additional-url="https://helpx.adobe.com/cn/enterprise/using/support-for-experience-cloud.html" text="联系 Adobe 支持"

完成每個步驟（擷取和擷取）後，請檢查記錄檔並尋找錯誤。  应立即通过处理所报告的问题或联系 Adobe 支持部门而纠正任何错误。

## 檢視記錄檔的步驟 {#viewing-logs}

### 擷取記錄

若要檢視擷取記錄，請前往來源Adobe Experience Manager執行個體，然後選取所需的移轉集。

然後，請遵循下列步驟：

1. 選取移轉集並按一下 **檢視記錄** 動作列中的。 此時會顯示「記錄」對話方塊。 按一下 **擷取記錄** 以在新索引標籤中檢視記錄。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam25.png) \
   或者，按一下 **已完成** 狀態：在新索引標籤中檢視記錄。

1. 要在不使用用户界面的情况下跟踪日志，您可以通过 SSH 连接到源 AEM 环境并跟踪 `crx-quickstart/cloud-migration/extraction-XXXXX/output.log file`。

### 擷取記錄

若要檢視內嵌記錄，請前往Cloud Acceleration Manager中的內嵌工作清單，然後找到所需的移轉工作，並按一下三個點(**...**)。 然後，您可以按一下 **下載記錄** 以下載記錄檔。

![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam28.png)
