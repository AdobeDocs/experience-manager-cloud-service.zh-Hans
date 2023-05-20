---
title: Cloud Acceleration Manager中的實作階段
description: 本頁提供Cloud Acceleration Manager中實作階段的概觀。
exl-id: e6ac88f0-4b3f-43a1-98bc-8c6608713784
source-git-commit: cba5dccd3b66220bbcd6d3b4dd5298702902b0e5
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 5%

---

# Cloud Acceleration Manager中的實作階段 {#implementation-phase-cam}

實作階段包括：

* [本地开发](#local-development)
* [代码重构](#code-refactoring)
* [AEMas a Cloud Service部署](#aem-as-a-cloud-service-deployment)
* [内容传输](#content-transfer)


按一下您的專案卡以開啟專案登入頁面，並導覽至 **實作** 區段，如下圖所示。

![图像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-1.png)

>[!NOTE]
>請參閱 [在Cloud Acceleration Manager中建立和管理專案](getting-started-cam.md#create-project) 以深入瞭解。


## 使用本機開發卡 {#local-development}

本機開發卡提供所有相關內容，可協助您在開始移轉歷程的實施階段時設定本機AEM開發環境。

請詳閱本節，以探索「本機開發」活動卡：

1. 按一下 **檢視** 按鈕來自 **本機開發** 卡片。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-2.png)

1. 內容輪播會顯示移轉歷程這個階段的相關資訊。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-3.png)


## 使用程式碼重構卡 {#code-refactoring}

「程式碼重構」活動卡片會提供所有相關資訊，並反白標示您在移至AEMas a Cloud Service時需要檢視和解決的程式碼重構區域。

請詳閱本節，以探索「程式碼重構」活動卡：

1. 按一下 **檢閱** 按鈕來自 **程式碼重構** 活動卡。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-4.png)

1. 頁面會顯示依嚴重性層級組織的程式碼重構活動清單。 您可以按一下兩個反白的圖示以瞭解更多資訊。

   此頁面會在三個不同的標籤中顯示程式碼重構的考量事項：

   * 概述
   * Dispatcher
   * 测试

>[!NOTE]
>請檢閱這些標籤中的內容，瞭解Best Practices Analyzer未涵蓋的其他領域。

此 **Dispatcher** 索引標籤提供有關如何架構AEMas a Cloud ServiceApache和Dispatcher設定，以及如何在部署到雲端環境之前在本機驗證和執行它的資訊。 此外也說明如何在雲端環境中進行除錯。

![图像](/help/journey-migration/cloud-acceleration-manager/assets/coderefactoring-2.png)

此 **測試** 索引標籤提供有關功能、體驗稽核和UI測試的資訊。

![图像](/help/journey-migration/cloud-acceleration-manager/assets/coderefactoring-3.png)


## 使用AEMas a Cloud Service部署卡 {#aem-as-a-cloud-service-deployment}

AEMas a Cloud Service部署卡提供所有相關內容，可幫助您將程式碼部署到AEMas a Cloud Service。

請依照本節內容，探索AEMas a Cloud Service部署卡活動卡：

1. 按一下 **檢視** 按鈕來自 **AEMas a Cloud Service部署** 活動卡。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-6.png)

1. 內容輪播會顯示移轉歷程這個階段的相關資訊。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/aem-deployment-card.png)


## 使用內容轉移卡 {#content-transfer}

「內容轉移」卡片可讓您開始並管理從目前AEM執行個體到AEMas a Cloud Service的內容轉移。

請詳閱本節，以探索「內容轉移」活動卡：

1. 按一下 **檢閱** 按鈕來自 **內容轉移** 活動卡。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-1.png)

1. 若要開始內容轉移，您必須建立移轉集。 按一下 **建立移轉集**. 移轉集允許將內容傳輸至AEMas a Cloud Service。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-2.png)

   >[!NOTE]
   >請注意，移轉集將在長時間不活動後過期。 請檢閱 [移轉集到期](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry) 以取得詳細資訊。

   >[!NOTE]
   >請檢閱 [必備條件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html) 和 [最佳實務和准則](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html) 使用「內容轉移工具」之前。

1. 您需要下載並安裝內容轉移工具以填入移轉集，並完成內容轉移的提取階段。 檢閱 [內容轉移工具快速入門](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html) 以瞭解如何使用內容轉移工具。

1. 若要將內容從移轉集內嵌至AEMas a Cloud Service的環境，您必須開始內嵌。 導覽至 **內嵌工作** 並按一下 **新內嵌**. 檢閱 [將內容擷取至Target](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/ingesting-content.html) 以瞭解如何完成內容轉移的擷取階段。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-3.png)

<!--### Estimating Content Transfer Time {#calculating}

A Content Transfer Tool calculator has been provided to estimate how long it could take to complete the content transfer activity. You can use the content repository size slider to select the size that applies to your project. The transfer times vary for the extraction and ingestion phases. 

   ![image](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-4.png)

   >[!NOTE]
   >These times are estimates only. Factor such as network speeds and time to scale up instances have not been accounted for in these estimates.

To estimate the size of the AEM Repository, you can run the Disk Usage report under `http://HOST:PORT/etc/reports/diskusage.html`. 

You can also estimate the size of specific repository paths by using the `path` parameter, for example, `http://HOST:PORT/etc/reports/diskusage.html?path=/content/dam`. -->

## 后续内容 {#whats-next}

在您瞭解如何登入Cloud Acceleration Manager以及如何利用實作階段後，您現在已準備好繼續檢閱中的下一個步驟 [上線階段](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-golive-phase.html).
