---
title: 验证内容转移
description: 使用內容轉移工具來驗證內容轉移
exl-id: a12059c3-c15a-4b6d-b2f4-df128ed0eea5
source-git-commit: c1f60a1ead466b47694b8918e5b39011041c5f25
workflow-type: tm+mt
source-wordcount: '1070'
ht-degree: 2%

---

# 验证内容转移 {#validating-content-transfers}

## 快速入门 {#getting-started}

使用者能夠可靠地判斷「內容轉移工具」擷取的所有內容是否已成功擷取到目標例項中。 此驗證功能的運作方式是，比較擷取期間涉及的所有節點的路徑摘要，以及擷取期間涉及的所有節點的路徑摘要。 如果擷取摘要中納入的任何節點路徑遺漏了擷取摘要，則驗證會被視為失敗，且可能需要額外的手動驗證。

>[!INFO]
>
>此功能將在內容轉移工具(CTT) 1.8.x版發行後提供。 AEM Cloud Service目標環境必須至少執行6158版或更高版本。 還需要設定來源環境才能執行 [預先複製](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#setting-up-pre-copy-step). 驗證功能會尋找來源上的azcopy.config檔案。 如果找不到此檔案，則不會執行驗證。 若要進一步瞭解如何設定azcopy.config檔案，請參閱 [此頁面](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#configure-azcopy-config-file).

驗證內容轉移是一項選擇性功能。 啟用此功能會增加執行擷取和擷取所需的時間。 若要使用此功能，請在來源AEM環境的「系統主控台」中啟用它，請執行以下步驟：

1. 導覽至來源執行個體上的Adobe Experience Manager Web Console，方法是前往 **工具 — 作業 — Web主控台** 或直接前往URL，網址為 *https://serveraddress:serverport/system/console/configMgr*
1. 搜尋 **內容轉移工具提取服務設定**
1. 使用鉛筆圖示按鈕來編輯其設定值
1. 啟用 **在擷取期間啟用移轉驗證** 設定，然後按 **儲存**：

   ![图像](/help/journey-migration/content-transfer-tool/assets/CTTvalidation1.png)

啟用此設定且目標AEM Cloud Service環境執行相容版本時，將會在後續的所有擷取和擷取期間進行移轉驗證。

如需如何安裝內容轉移工具的詳細資訊，請參閱 [內容轉移工具快速入門](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md).

## 如何驗證內容轉移 {#how-to-validate-a-content-transfer}

在來源AEM環境中啟用移轉驗證後，開始擷取。

若 **在擷取期間覆寫暫存容器** 已啟用，與擷取相關的所有節點將記錄到擷取路徑摘要。 使用此設定時，請務必啟用 **在內嵌之前擦除雲端例項上的現有內容** 在內嵌期間進行設定，否則在內嵌摘要中可能會遺漏節點。 這些是先前擷取中已經存在於目標上的節點。

如需圖解說明，請參考以下範例：

### 示例 1 {#example-1}

* **擷取（覆寫）**

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/validation-01.png)

* **內嵌（擦去）**

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/validation-02.png)

* **注释**

   此「覆寫」和「擦去」的組合會產生一致的驗證結果，即使是重複擷取亦然。

### 示例 2 {#example-2}

* **提取**

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/validation-03.png)

* **內嵌**

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/validation-04.png)

* **注释**

   此「覆寫」和「擦去」的組合將導致初始內嵌的一致驗證結果。

   如果重複內嵌，內嵌摘要將會是空的，而驗證將會顯示為失敗。 擷取摘要將為空白，因為此擷取的所有節點都將存在於目標上。

擷取完成後，即可開始內嵌。

內嵌記錄檔的頂端會包含一個專案，類似於 `aem-ethos/tools:1.2.438`. 確定此版本編號為 **1.2.438** 或更新的版本，否則您使用的AEMas a Cloud Service版本不支援驗證。

擷取完成並開始驗證後，將在擷取記錄中記錄以下記錄專案：

```
Gathering artifacts for migration validation...
```

驗證的詳細資訊會在此專案後面。 尋找以下大型移轉的範例：

```
Beginning publish migration validation. Migration job id=[3aba1f96-84b6-4bd0-8642-c61c0d528387]
Extraction path digest is being processed...
Extraction path digest processing took 982 seconds
Ingestion path digest is being processed...
Ingestion path digest processing took 999 seconds
Comparing the Extraction and Ingestion path digests...
----------------------------------------------------------
EXTRACTION: Number of nodes extracted: 51674784
INGESTION: Number of nodes ingested: 51674784
----------------------------------------------------------
Validation succeeded! No entries were detected to be missing from the ingestion digest.
----------------------------------------------------------
Comparing the path digests took 29 seconds
Migration validation took 33 minutes
```

這是成功驗證的範例，因為擷取摘要中不存在擷取摘要中遺漏的專案。

若要比較，以下說明驗證失敗時驗證報告的外觀：

```
Beginning publish migration validation. Migration job id=[ac217e5a-a08d-4e81-cbd6-f39f88b174ce]
Extraction path digest is being processed...
Extraction path digest processing took 0 seconds
Ingestion path digest is being processed...
Ingestion path digest processing took 0 seconds
Comparing the Extraction and Ingestion path digests...
----------------------------------------------------------
EXTRACTION: Number of nodes extracted: 4635
INGESTION: Number of nodes ingested: 0
----------------------------------------------------------
Validation failed. However, the following nodes may already be present in the target environment.
Please refer to our Migration Validation FAQ (https://www.adobe.com/go/aem_cloud_ctt_validation_en) or open a ticket with Customer Care.
There are 4635 entries present in the extraction digest that are missing from the ingestion digest.
/content/dam/bruce
/content/dam/bruce-assets
... more paths listed (up to 10k) ...
----------------------------------------------------------
Comparing the path digests took 0 seconds
Migration validation took 0 minutes
```

上述失敗範例是透過執行內嵌，然後在停用擦去的情況下再次執行相同的內嵌來達成，這樣在內嵌期間不會涉及任何節點 — 目標上已存在所有內容。

除了包含在擷取記錄中外，驗證報告也可以從以下網址存取： **內嵌工作** Cloud Acceleration Manager中的使用者介面。 若要這麼做，請按一下三個點(**...**)然後按一下 **驗證報告** 以檢視驗證報告。


![图像](/help/journey-migration/content-transfer-tool/assets-ctt/CTTvalidationreportnew.png)

## 如何驗證主體移轉 {#how-to-validate-principal-migration}

另請參閱 [使用者對應和主體移轉](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md) 以瞭解主要移轉的詳細資料以及為何需要。

成功完成擷取和內嵌後，即可使用主體移轉的摘要和報告。 此資訊可用於驗證哪些使用者和群組已成功移轉，或許也可用於判斷部分使用者及群組未成功移轉的原因。

若要檢視此資訊，請前往Cloud Acceleration Manager。 按一下您的專案卡，然後按一下「內容轉移」卡。 導覽至 **內嵌工作** 並找到您要驗證的內嵌。 按一下三個點(**...**)，然後按一下 **檢視主體摘要** （在下拉式清單中）。

![图像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-principal-action.png)

您會看到包含摘要資訊的對話方塊。 使用說明圖示來閱讀更完整的說明。 按一下 **下載報告** 按鈕以下載完整的逗號分隔(CSV)報表。

![图像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-principal-dialog.png)

>[!NOTE]
>
>如果停用使用者對應，則會顯示此對話方塊的另一個變體。 這會指出使用者對應已停用，且不會顯示提供使用者對應值的3個欄位。

## 疑难解答 {#troubleshooting}

### 验证失败. 现在该做什么？ {#validation-fail}

第一步是判斷內嵌是否真的失敗，或擷取的內容是否已存在於目標環境中。 如果內嵌重複出現 **在內嵌之前擦除雲端例項上的現有內容** 選項已停用。

若要驗證，請從驗證報表中選擇路徑，並檢查該路徑是否存在於目標環境中。 如果這是發佈環境，您可能會受限於直接檢查頁面和資產。 如果您需要此步驟的協助，請透過客戶服務開立票證。

### 節點計數低於我的預期。 為什麼？ {#node-count-lower-than-expected}

會刻意排除擷取和擷取摘要的部分路徑，以管理這些檔案的大小，目標是在擷取完成後的兩小時內計算移轉驗證結果。

我們目前從摘要中排除的路徑包括： `cqdam.text.txt` 轉譯，內的節點 `/home`，以及內的節點 `/jcr:system`.
