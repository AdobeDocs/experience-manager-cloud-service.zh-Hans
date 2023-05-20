---
title: AEMas a Cloud Service2021.10.0版中移轉工具的發行說明
description: AEMas a Cloud Service2021.11.0版中移轉工具的發行說明
feature: Release Information
exl-id: 6b1caa63-dcb0-4c48-ab2c-fd72617abf13
source-git-commit: 3c8035e4db5729f58bae29136a32a0b9944d6a2f
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 14%

---

# AEMas a Cloud Service2021.10.0版中移轉工具的發行說明 {#release-notes}

本頁面總覽AEMas a Cloud Service2021.10.0中移轉工具發行說明。

>[!NOTE]
>要查看 Adobe Experience Manager as a Cloud Service 的当前发行说明，请单击[此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/release-notes/release-notes-current.html)。

## Cloud Acceleration Manager {#cam-release}

### 发布日期 {#release-date-cam}

Cloud Acceleration Manager的發行日期為2021年10月25日。

### 新增功能 {#what-is-new-cam}

Cloud Acceleration Manager現在可讓使用者在趨勢線報告中檢視歷史BPA報告。 透過此報告，使用者能夠以易於使用的圖形表示來檢視他們正在取得的進度。 請參閱 [使用檢視趨勢線](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=en#trendline-view-cam) 以取得更多詳細資料。

### 发布日期 {#release-date-october-cam}

Cloud Acceleration Manager的發行日期為2021年10月4日。

### 新增功能 {#what-is-new-cam-oct}

Cloud Acceleration Manager現在可讓使用者在可列印的預覽中檢視BPA報告，以便進行簡單的列印或列印，以PDF輕鬆共用。 請參閱中的步驟6和7 [使用最佳做法分析卡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=en#best-practices-analysis).


## 内容转移工具 {#ctt-release}

### 发布日期 {#release-date-ctt-latest}

內容轉移工具v1.6.0的發行日期為2021年10月4日。

### 新增功能 {#what-is-new-ctt-oct}

* 透過簡化的使用者體驗改進使用者對應工具，包括以下列出的功能。 如需詳細資訊，請參閱 [使用使用者對應工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/legacy-user-mapping-tool/using-user-mapping-tool-legacy.html?lang=en).
   * 在執行使用者對應之前測試與使用者管理API的連線
   * 正常略過錯誤，並繼續使用者對應活動
   * 在下列情況下，使用者對應不再失敗： **存取Token** 24小時後過期。 可以從上次停止的位置重新執行使用者對應。

* 為了提高內容轉移工具的穩健性，內容可以一次擷取到作者執行個體或發佈執行個體。 另請參閱 [內容轉移工具快速入門](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=zh-Hans) 以取得更多詳細資料。

* 包含版本時，路徑 `/var/audit` 自動包含以移轉稽核事件。

## Best Practices Analyzer {#best-practices-analyzer}

### 发布日期 {#release-date-bpa-latest}

Best Practices Analyzer v2.1.20的發行日期為2021年10月5日。

### 新增功能 {#what-is-new-bpa-oct}

* 能夠偵測並報告節點名稱長度。

* 能夠偵測及報告索引總大小。

* 能夠偵測並報告缺少原始轉譯的資產。
