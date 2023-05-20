---
title: 關於Dynamic Media影像設定檔和視訊設定檔
description: 影像設定檔或視訊設定檔是套用至上傳至資料夾之資產的選項。 例如，您可以指定要套用至上傳之Dynamic Media視訊資產的視訊編碼。 或是套用至Dynamic Media影像資產的影像設定檔，以便正確加以裁切。
contentOwner: Rick Brough
feature: Asset Management,Image Profiles,Video Profiles
role: Admin,User
exl-id: 8c8f0a57-13f5-4903-8d76-bfb6ee83323c
source-git-commit: a641903bf47634cd969f23840c5e6e6fa5a3693b
workflow-type: tm+mt
source-wordcount: '1377'
ht-degree: 0%

---

# 關於Dynamic Media影像設定檔和視訊設定檔{#about-dm-image-video-profiles}

影像設定檔或視訊設定檔是套用至上傳至資料夾之資產的選項。 例如，您可以指定要套用至上傳之Dynamic Media視訊資產的視訊編碼。 或是套用至Dynamic Media影像資產的影像設定檔，以便正確加以裁切。

在Dynamic Media中，您可以建立兩種型別的設定檔，下列連結會詳細說明這些設定檔：

* [Dynamic Media影像設定檔](/help/assets/dynamic-media/image-profiles.md)
* [Dynamic Media視訊設定檔](/help/assets/dynamic-media/video-profiles.md)

另請參閱 [中繼資料設定檔](/help/assets/metadata-profiles.md).

您必須擁有管理員許可權，才能建立、編輯和刪除Dynamic Media影像設定檔或Dynamic Media視訊設定檔。

建立影像設定檔或視訊設定檔後，請將其指派至一或多個用於新上傳Dynamic Media資產的資料夾。

另請參閱 [組織數位資產以使用處理設定檔的最佳實務](/help/assets/organize-assets.md).


>[!NOTE]
>
>您從一個資料夾移至另一個資料夾的資產不會重新處理。 例如，假設您的資料夾1已指派設定檔A，而資料夾2已指派設定檔B。 如果您將資產從「資料夾1」移至「資料夾2」，則已移動的資產會保留「資料夾1」的原始處理作業。
>
>即使您在具有相同設定檔的兩個資料夾之間移動資產，情況也是如此。

## 重新處理資料夾中的Dynamic Media資產 {#reprocessing-assets}

若資料夾中已有您後來變更的現有Dynamic Media影像設定檔或Dynamic Media視訊設定檔，您可以重新處理該資料夾中的資產。

例如，假設您建立了一個Dynamic Media影像設定檔，並將其指派給一個資料夾。 您上傳至資料夾的任何影像資產都會自動將影像設定檔套用至資產。 不過，您稍後會決定在「影像描述檔」中新增智慧型裁切比例。 現在，您只需執行 *Scene7：重新處理資產* 工作流程。

您可以對首次處理失敗的資產執行重新處理工作流程。 即使您尚未編輯影像設定檔或視訊設定檔，或您已套用影像設定檔或視訊設定檔，您仍可隨時對資產的資料夾執行重新處理工作流程。

您可以選擇調整重新處理工作流程的批次大小，從預設的50個資產調整至1000個資產。 當您執行 _Scene7：重新處理資產_ 工作流程時，資產會依批次分組，然後傳送至Dynamic Media伺服器以供處理。 處理之後，整個批次集中每個資產的中繼資料會更新於 [!DNL Adobe Experience Manager]. 如果批次大小很大，您可能會遇到處理延遲。 或者，如果批次大小太小，可能會導致Dynamic Media伺服器的往返次數過多。

另請參閱 [調整重新處理工作流程的批次大小](#adjusting-load).

>[!NOTE]
>
>如果您要將資產從Dynamic Media Classic大量移轉至 [!DNL Experience Manager]，在Dynamic Media伺服器上啟用移轉復寫代理程式。 移轉完成後，請務必停用代理程式。
>
>必須在Dynamic Media伺服器上停用移轉發佈代理程式，才能讓重新處理工作流程按預期運作。

<!-- LEAVE IN PLACE, MAY BE USED IN THE FUTURE

Batch size is the number of assets that are amalgamated into a single IPS (Dynamic Media's Image Production System) job. When you run the Scene7: Reprocess Assets workflow, the job is triggered on IPS. The number of IPS jobs that are triggered is based on the total number of assets in the folder, divided by the batch size. For example, suppose you had a folder with 150 assets and a batch size of 50. In this case, three IPS jobs are triggered. The assets are updated when the entire batch size (50 in our example) is processed in IPS. The job then moves onto the next IPS job and so on until complete. If you increase the batch size, you may notice a longer delay with assets getting updated. 

-->

**若要重新處理資料夾中的Dynamic Media資產：**

1. 在 [!DNL Experience Manager]，從「資產」頁面，導覽至已指派影像設定檔或視訊設定檔且您想要套用其的資產資料夾。 **Scene7：重新處理資產** 工作流程。

   已指派影像設定檔或視訊設定檔的資料夾會以設定檔名稱直接顯示在「卡片檢視」的資料夾名稱下方。

1. 選取資料夾。

   * 工作流程會遞回考量所選資料夾中的所有檔案。
   * 如果主要選取資料夾中有一個或多個子資料夾包含資產，則工作流程會重新處理資料夾階層中的每個資產。
   * 最佳做法是避免在擁有超過1000個資產的資料夾階層執行此工作流程。

1. 在頁面的左上角附近，從下拉式清單中選取 **[!UICONTROL 時間表]**.
1. 在頁面的左下角附近， [!UICONTROL 註解] 欄位中，選取克拉圖示( **^** ) 。

   ![「Experience Manager中的資產」熒幕擷圖顯示選取的資產資料夾、「時間軸」下拉式清單熒游標示、「開始工作流程」按鈕熒游標示，以及「註解」欄位右側的克拉圖示熒游標示。](/help/assets/dynamic-media/assets/reprocess-assets1.png)

1. 選取 **[!UICONTROL 開始工作流程]**.
1. 從 **[!UICONTROL 開始工作流程]** 下拉式清單，選擇 **[!UICONTROL Scene7：重新處理資產]**.
1. （選用）在 **輸入工作流程的標題** 文字欄位，輸入工作流程的名稱。 如有必要，您可以使用名稱來參照工作流程例項。

   ![從「開始工作流程」下拉式清單中選取「Scene7：重新處理資產」且醒目提示「開始」按鈕的「時間軸」使用者介面熒幕擷圖。](/help/assets/dynamic-media/assets/reprocess-assets2.png)

1. 選取 **[!UICONTROL 開始]**，然後選取 **[!UICONTROL 確認]**.

   若要監視工作流程或檢查其進度，請從 [!DNL Experience Manager] 主控台首頁面，選取 **[!UICONTROL 工具>工作流程]**. 在「工作流程例項」頁面上，選取工作流程。 在功能表列上，選取 **[!UICONTROL 開啟歷史記錄]**. 您也可以從同一個「工作流程例項」頁面終止、暫停或重新命名選取的工作流程。

### 調整重新處理工作流程的批次大小（選擇性） {#adjusting-load}

（選用）重新處理工作流程中的預設批次大小是每個工作50個資產。 此最佳批次大小是由執行重新處理的平均資產大小和MIME資產型別所控制。 較高的值表示您在一個重新處理作業中有許多檔案。 因此，處理橫幅會保持開啟 [!DNL Experience Manager] 資產保留更長時間。 不過，如果平均檔案大小為1 MB以下或小於1 MB，建議您將值增加到數100，但絕不要超過1000Adobe。 如果平均檔案大小為數百MB，Adobe建議您減少批次大小，最多為10。

**若要選擇性地調整重新處理工作流程的批次大小，請執行下列步驟：**

1. 在 [!DNL Experience Manager]，選取 **[!UICONTROL Adobe Experience Manager]** 若要存取全域導覽主控台，請選取 **[!UICONTROL 工具]** （槌子）圖示> **[!UICONTROL 工作流程>模型]**.
1. 在「工作流程模型」頁面的「卡片檢視」或「清單檢視」中，選取 **[!UICONTROL Scene7：重新處理資產]**.

   ![在Experience Manager的卡片檢視中選取了「Scene7：重新處理資產」工作流程的「工作流程模型」頁面熒幕擷圖。](/help/assets/dynamic-media/assets/reprocess-assets7.png)

1. 在工具列中，選取 **[!UICONTROL 編輯]**. 新的瀏覽器標籤會開啟「Scene7：重新處理資產」工作流程模型頁面。
1. 在「Scene7：重新處理資產」工作流程頁面的右上角附近，選取「 」 **[!UICONTROL 編輯]** 以「解鎖」工作流程。
1. 在工作流程中，選取「Scene7批次上傳」元件以開啟工具列，然後選取「 」 **[!UICONTROL 設定]** （在工具列中）。

   ![「Scene7：重新處理資產」頁面上的「Scene7批次上傳」元件熒幕擷圖，將滑鼠指標暫留在「設定」圖示上。](/help/assets/dynamic-media/assets/reprocess-assets8.png)

1. 於 **[!UICONTROL 批次上傳至Scene7 — 步驟屬性]** 對話方塊中，設定下列專案：
   * 在 **[!UICONTROL 標題]** 和 **[!UICONTROL 說明]** 文字欄位，視需要輸入新的職稱和說明。
   * 選取 **[!UICONTROL 處理常式前進]** 如果您的處理常式將前進到下一個步驟。
   * 在 **[!UICONTROL 逾時]** 欄位，輸入外部程式逾時（秒）。
   * 在 **[!UICONTROL 期間]** 欄位，輸入輪詢間隔（秒）以測試外部程式的完成。
   * 在 **[!UICONTROL 批次欄位]**，輸入Dynamic Media伺服器批次處理上傳工作中要處理的資產數量上限(50-1000)。
   * 選取 **[!UICONTROL 逾時前進]** 如果您想要在達到逾時值時推進。 如果達到逾時時間時仍要進入收件匣，請取消選取。

   ![「批次上傳至Scene7 — 步驟屬性」頁面的熒幕擷圖。](/help/assets/dynamic-media/assets/reprocess-assets3.png)

1. 在的右上角 **[!UICONTROL 批次上傳至Scene7 — 步驟屬性]** 對話方塊，選取 **[!UICONTROL 完成]**.

1. 在「Scene7：重新處理資產」工作流程模型頁面的右上角，選取 **[!UICONTROL 同步]**. 當您看到 **[!UICONTROL 已同步]**，工作流程執行階段模型已成功同步化，並準備好重新處理資料夾中的資產。

   ![「Experience Manager中的資產」熒幕擷圖顯示選取的資產資料夾、「時間軸」下拉式清單熒游標示、「開始工作流程」按鈕熒游標示，以及「註解」欄位右側的克拉圖示熒游標示。](/help/assets/dynamic-media/assets/reprocess-assets1.png)

1. 關閉顯示「Scene7：重新處理資產」工作流程模型的瀏覽器標籤。

<!-- MAY BE NEEDED IN THE FUTURE

1. Return to the browser tab that has the open Workflow Models page, then press **Esc** to exit the selection.
1. In the upper-left corner of the page, select **[!UICONTROL Adobe Experience Manager]** to access the global navigation console, then select the **[!UICONTROL Tools]** (hammer) icon > **[!UICONTROL General > CRXDE Lite]**.
1. In the folder tree on the left side of the CRXDE Lite page, navigate to the following location:

   `/conf/global/settings/workflow/models/scene7_reprocess_assets/jcr:content/flow/reprocess/metaData`

   ![CRXDE Lite](/help/security/assets/workflow-models9.png)

1. On the right side of the CRXDE Lite page, in the lower portion, enter the following name, type, and value in its respective field:
    * **[!UICONTROL Name]**: `reprocess-batch-size`
    * **[!UICONTROL Type]**: `Long`
    * **[!UICONTROL Value]**: enter a default value (50-1000) for the batch size
1. In the lower-right corner, select **[!UICONTROL Add]**. The new property appears as the following:

    ![Saving the new property](/help/security/assets/workflow-models10.png)

1. On the menu bar of the CRXDE Lite page, select **[!UICONTROL Save All]**.
1. In the upper-left corner of the page, select **[!UICONTROL CRXDE Lite]** to return to the main Experience Manager console
1. Repeat steps 1-7 to re-synchronize the new batch size to the Scene7: Reprocess Assets workflow model.

-->
