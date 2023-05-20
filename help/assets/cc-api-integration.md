---
title: Creative Cloud整合的內容自動化
description: 使用Creative Cloud整合產生資產的變體
contentOwner: AG
feature: Upload,Asset Processing,Publishing,Asset Compute Microservices,Workflow
role: User,Admin
exl-id: 4cff355e-d12c-44c7-b519-4cc37f49e396
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 4%

---

# 使用以下專案產生資產的變體： [!DNL Adobe Creative Cloud] 整合 {#content-automation}

內容自動化附加元件整合 [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] 和 [!DNL Adobe Creative Cloud] API可大規模以創意方式處理您的資產。 [!DNL Experience Manager] 使用雲端型 [資產微服務](/help/assets/asset-microservices-overview.md) 以使用 [!DNL Adobe Creative Cloud] 並自動化資產的建立和媒體處理。

若要編輯中的資產 [!DNL Adobe Photoshop] 和 [!DNL Adobe Lightroom]，您不必從下載資產 [!DNL Experience Manager Assets]，再次編輯和上傳。 您可在以下位置建立和設定處理設定檔： [!DNL Experience Manager]，將設定檔套用至資料夾，然後上傳資產至資料夾。 系統會根據處理設定檔重新處理您上傳的資產，而您會得到這些資產的變數。 一致且輕鬆的大量處理可節省手動工作並提升內容速度，也無需卓越的創意技巧。 此外，開發人員和合作夥伴也可以透過直接存取這些API來擴充資產微服務，並包含自訂邏輯。

使用者可以建立處理設定檔，以對其資產自動執行下列創意操作：

* **自動色調**：使用人工智慧來分析影像內容，並根據影像的獨特屬性聰明地校正光源和色彩。

* **自動直立**：使用人工智慧來分析影像內容並修正影像中的傾斜透視。 例如，建立層級視野。

   ![自動色調](/help/assets/assets/content-automation-autotone.png)

   *圖：自動色調和自動拉直有助於改善傾斜影像。*

* **Lightroom預設集**：將使用者定義的外觀套用至影像，以使用自訂的預設集取得一致的外觀。

   ![Lightroom預設集](/help/assets/assets/content-automation-lrpresets.png)

   *圖：Adobe Lightroom預設集，可透過一致的方式改善許多影像的影像品質。*

* **影像挖剪圖案**：使用人工智慧在主要物件周圍建立選取範圍，並使用單一命令移除背景。

   ![移除背景並從像片中剪下影像](/help/assets/assets/content-automation-backgroundremove.png)

* **影像遮色片**：使用人工智慧透過單一命令在主要物件周圍建立遮色片。

   ![使用AI遮色影像](/help/assets/assets/content-automation-mask.png)

* **Photoshop動作**：套用一系列 [!DNL Adobe Photoshop] 將任務移至檔案或批次檔案。

   ![Photoshop動作](/help/assets/assets/content-automation-psactions.png)

* **智慧型物件取代**：可讓您交換影像，同時保留PSD檔案內套用的所有效果和調整，以大規模個人化。

   ![聰明地取代物件](/help/assets/assets/content-automation-objectreplace.png)

## 為AEMas a Cloud Service程式啟用內容自動化 {#enable-content-automation}

若要使用Cloud Manager為AEMas a Cloud Service程式啟用Content Automation附加元件：

1. 請聯絡您的客戶代表以授權Content Automation附加元件。
1. 存取Cloud Manager並使用組織選擇器切換到您的組織。
1. 按一下 **[!UICONTROL 新增計畫]** 並指定程式名稱。
1. 单击&#x200B;**[!UICONTROL “继续”]**。
1. 展開 **[!UICONTROL 資產]** 並選取 **[!UICONTROL 內容自動化]**.
1. 单击&#x200B;**[!UICONTROL 创建]**。
1. 執行管道至 [將變更部署到Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html).

如果您需要將Content Automation附加元件新增到Cloud Manager中的現有AEMas a Cloud Service計畫：

1. 按一下計畫卡片上的…… 。

1. 選取 **[!UICONTROL 編輯計畫]** 然後選取 **[!UICONTROL 解決方案和附加元件]** 標籤。

1. 展開 **[!UICONTROL 資產]** 並選取 **[!UICONTROL 內容自動化]**.
1. 单击&#x200B;**[!UICONTROL 更新]**。
1. 執行管道至 [將變更部署到Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html).

## 使用處理設定檔來大量編輯您的創意資產 {#process-assets}

若要使用處理設定檔來自動建立變化，請遵循下列步驟：

1. 導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 處理設定檔]**.

1. 選取 **[!UICONTROL 建立]**，並指定 **[!UICONTROL 名稱]**.

1. 選取 **[!UICONTROL Creative]** 索引標籤，指定輸出資料夾，選取 **[!UICONTROL 新增]** 以新增創意設定。

1. 提供 **[!UICONTROL 轉譯名稱]** （或輸出名稱）， **[!UICONTROL 副檔名]** （或檔案型別），選取 **[!UICONTROL 品質]** （或輸出引數），選取 **[!UICONTROL 包含]** 和 **[!UICONTROL 排除]** MIME型別清單（或輸入資產篩選器），並選取所需的創意操作。

   ![[!UICONTROL Creative] 定位於 [!UICONTROL 處理設定檔]](assets/creative-processing-profile.png)

1. 某些作業需要額外的引數（資產）。 視需要提供這些額外引數的值。

1. 將更多創意操作新增為相同處理設定檔的一部分，或儲存設定檔。

1. 將處理設定檔套用至資料夾。 在資料夾的 **[!UICONTROL 屬性]** 頁面，選取 **[!UICONTROL 資產處理]**，並選取要套用的處理設定檔。

將處理設定檔套用至DAM資料夾後，此資料夾中上傳或更新的所有資產除了執行標準處理外，還會執行定義的操作。 子資料夾會繼承與套用至父資料夾的相同設定檔。 使用者可以覆寫此繼承。

若要處理現有資產，請選取資產，然後選取 **[!UICONTROL 重新處理]** 選項，然後選取所需的處理設定檔。

## 提示和限制 {#limitations-best-practices}

* [!DNL Experience Manager] 將資產處理限製為每個環境每分鐘300個請求，每個組織每分鐘700個請求。
* 檔案大小限製為4 GB [!DNL Adobe Photoshop] API操作，以及1 GB [!DNL Adobe Lightroom] 作業。

**另请参阅**

* [翻译资源](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [资源支持的文件格式](file-format-support.md)
* [搜索资源](search-assets.md)
* [连接的资源](use-assets-across-connected-assets-instances.md)
* [资源报告](asset-reports.md)
* [元数据架构](metadata-schemas.md)
* [下载资源](download-assets-from-aem.md)
* [管理元数据](manage-metadata.md)
* [搜索 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [批量元数据导入](metadata-import-export.md)

>[!MORELIKETHIS]
>
>* [透過處理設定檔來設定和使用資產微服務](/help/assets/asset-microservices-configure-and-use.md).
>* [ [!DNL Experience Manager] 与 集成 [!DNL Creative Cloud]](/help/assets/aem-cc-integration-best-practices.md).
>* [使用資產微服務進行資產擷取和處理：概覽](/help/assets/asset-microservices-overview.md).

