---
title: Cloud Acceleration Manager中的整備階段
description: 本頁提供Cloud Acceleration Manager整備階段的概觀。
exl-id: 2583985b-0358-433c-9d31-38e2c60dc3dc
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1057'
ht-degree: 5%

---

# Cloud Acceleration Manager中的整備階段 {#readiness-phase-cam}

在Cloud Acceleration Manager中建立專案後，您現在可以在「整備」階段開始評估目前的AEM實施。

整備階段包括：

* [最佳實務分析](#best-practices-analysis)
* [規劃與設定](#planning-setup)

請依照下列步驟導覽至「整備階段」：

1. 按一下您的專案卡片以開啟專案登入頁面。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/cam-landing1.png)

1. 導覽至 **整備** 區段，如下圖所示。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/readiness-1.png)

   >[!NOTE]
   >如需瞭解詳細資訊，請參閱在Cloud Acceleration Manager中建立和管理專案。

## 使用最佳做法分析卡 {#best-practices-analysis}

請依照下列步驟使用Best Practices Analysis卡：

1. 按一下 **檢閱** 按鈕來自 **最佳實務分析** 卡片。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/readiness-2.png)

1. 請依照下列步驟下載Best Practices Analyzer (BPA)。

   >[!NOTE]
   >為避免對業務關鍵例項造成影響，建議您在儘可能接近生產環境的製作環境中，對自訂、設定、內容和使用者應用程式等方面執行BPA。 或者，也可以在克隆的生产“创作”环境中运行。

   1. 導覽至 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) 入口網站，並以zip檔案格式下載Best Practices Analyzer。

      >[!NOTE]
      >檢閱 [使用Best Practices Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en#imp-considerations) 以瞭解如何執行BPA。

   1. 將報表匯出為CSV格式

1. 按一下 **上傳新報告** 以在CAM中上傳BPA報告。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/readiness-3.png)

   >[!IMPORTANT]
   >如果您處於瀏覽器的無痕模式，則無法上傳報告。

1. 上傳新報告後，您會看到「最佳實務分析」報告。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/cam-bpareport.png)

1. 檢閱並探索CAM中的「最佳實務分析」圖示板。 請參閱以下章節 [檢閱最佳實務分析報告](#analysis-report) 以取得更多詳細資料。

   >[!NOTE]
   >上傳新報告會重設所有評估。

### 使用列印預覽 {#print-preview-cam}

您可以在Cloud Acceleration Manager中選取列印預覽選項，以列印報表的預覽，或將報表列印成PDF格式，以方便共用。

应遵循以下步骤：

1. 按一下 **列印預覽** 圖示，如下所示。

   ![图像](/help/journey-migration/best-practices-analyzer/assets/bpa-printpreview1.png)

1. 按一下 **列印預覽** 開啟新標籤，報告顯示在可列印的預覽中。 按一下 **列印** 將報表列印成PDF格式。

   >[!IMPORTANT]
   >* 選項 **另存為PDF** 上述功能建議並支援。
   >* 如果使用瀏覽器的列印按鈕，它將只列印一頁。


   ![图像](/help/journey-migration/best-practices-analyzer/assets/bpa-printpreview2.png)

### 使用檢視趨勢線 {#trendline-view-cam}

當您在專案中上傳多個Best Practices Analyzer (BPA)報告時，可以選取 **檢視趨勢線** 檢視及比較歷史BPA報表結果的選項。

請依照下列步驟，從趨勢線選項檢視報表：

>[!NOTE]
>當您在專案中上傳多個BPA報告時，您會看到 **...** 圖示。

1. 導覽至您的專案，然後按一下 **檢閱** 從 **最佳實務分析** 中的卡片 **整備** 階段。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1a.png)

1. 按一下 **...** 圖示來顯示下拉式清單。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1.png)

   >[!IMPORTANT]
   >顯示的報表一律為具有最新報表日期的報告。

1. 按一下 **檢視趨勢線**，如下圖所示。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view2.png)

1. 按一下 **檢視趨勢線** 開啟報告的趨勢線檢視，如下圖所示。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view3a.png)


   >[!NOTE]
   >趨勢線報告會以圖形呈現方式顯示歷史BPA報告的結果。
   >
   >您會看到兩個顯示下列專案趨勢的圖表：
   >1. **報告發現趨勢**
   >1. **自訂元件和範本趨勢**

   >
   >您可以透過下拉式清單新增或變更圖形檢視，如下圖所示：
   >![图像](/help/journey-migration/cloud-acceleration-manager/assets/reports-bpa1.png)


### 审核最佳实践分析报告 {#analysis-report}

探索「最佳實務分析報告」頁面中可用的下列卡片：

![图像](/help/journey-migration/cloud-acceleration-manager/assets/cam-bpareport.png)

>[!NOTE]
> 每張卡都具備以下功能：
>* 按一下每個卡片以開啟其相關標籤
>* 將所有報表標籤（包括篩選）加入書籤，以便共用或日後擷取
>* 使用詳細資訊圖示可檢視每個報告發現的詳細資訊


#### 报表属性 {#report-properties}

此 **報表屬性** 卡片提供有關報告屬性的資訊，例如報告日期、持續時間、篩選器、上傳日期和Adobe Experience Manager (AEM)詳細資訊。

![图像](/help/journey-migration/cloud-acceleration-manager/assets/report-properties.png)

#### 報表概觀 {#report-overview}

此 **報表概觀** 卡片會提供報告發現專案和嚴重性層級，在評估移至AEMas a Cloud Service的整備程度時適用，如下圖所示。

![图像](/help/journey-migration/cloud-acceleration-manager/assets/report-overview.png)

按一下此報告會開啟 **報告** 標籤。

![图像](/help/journey-migration/cloud-acceleration-manager/assets/report-overview2.png)

您可以根據重要性、子型別或計數來篩選報表。

![图像](/help/journey-migration/cloud-acceleration-manager/assets/report-overview3.png)

>[!NOTE]
>請參閱 [解譯Best Practices Analyzer報表](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en) 瞭解結果類別和重要性層級。

#### 最佳實務評估 {#best-practices-assessment}

最佳實務評估選項會評估您目前的AEM執行個體，並提供採用AEM最佳實務後續步驟的指引。 您可以從此標籤檢閱下列資訊：

* AEM執行個體總覽
* 自訂元件和範本
* 其他發現
* 较慢查询
* 维护任务

#### 移轉複雜性評估 {#migration-complexity-assessment}

「移轉複雜性評估」選項可評估將現有AEM實作移轉到AEMas a Cloud Service的複雜性。

您可以從此標籤檢閱下列資訊：

* AEM執行個體總覽
* 評估
* 內容移轉考量事項

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/migration-complexity-1.png)

## 使用Planning and Setup卡 {#planning-setup}

請詳閱本節，以探索「規劃與設定」活動卡。

1. 按一下 **檢視** 按鈕來自 **規劃與設定** 卡片。 此卡片提供所有相關內容，可協助您規劃和設定AEM移轉。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/readiness-view.png)

1. 內容輪播會顯示移轉歷程這個階段的所有相關資訊。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/readiness-5-planning.png)

### 刪除最佳實務分析報告 {#delete-trendline}

請依照下列步驟，從趨勢線檢視中刪除報表：

>[!IMPORTANT]
>只有當一個專案中已上傳多個報告時，才能刪除報告。

1. 導覽至您的專案，然後按一下 **檢閱** 從 **最佳實務分析** 中的卡片 **整備** 階段。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1a.png)

1. 按一下 **...** 圖示來顯示下拉式清單。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1.png)

1. 按一下 **檢視趨勢線**，如下圖所示。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view2.png)

1. 按一下刪除圖示，從 **趨勢線報告** 畫面。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view5a.png)

1. 按一下 **刪除** 以確認刪除。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view6a.png)

## 后续内容 {#whats-next}

瞭解如何登入Cloud Acceleration Manager以及如何建立專案後，您就可以繼續檢閱中的下一個步驟了 [實作階段](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-implementation-phase.html?lang=en).
