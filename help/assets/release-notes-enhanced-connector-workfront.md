---
title: 版发行说明 [!DNL Workfront for Experience Manager enhanced connector]
description: 版发行说明 [!DNL Workfront for Experience Manager enhanced connector]
exl-id: 12de589d-fe5d-4bd6-b96b-48ec8f1ebcb6
source-git-commit: 3a00faaf285be693243e3fb55159149520293610
workflow-type: tm+mt
source-wordcount: '1113'
ht-degree: 1%

---

#  版发行说明[!DNL Workfront for Experience Manager enhanced connector] {#release-notes-enhanced-connector-workfront}

以下區段會概述以下專案的一般發行說明： [!DNL Workfront for Experience Manager enhanced connector].

## 发布日期 {#release-date}

最新版本1.9.10的發行日期 [!DNL Workfront for Experience Manager enhanced connector] 是2023年5月18日。

## 發行重點說明 {#release-highlights}

最新版本的 [!DNL Workfront for Experience Manager enhanced connector] 包含下列更新：

* Workfront會根據從Experience Manager到Workfront的REST呼叫，針對重複事件訂閱傳回409 HTTP回應，這會導致Null指標例外狀況。


>[!IMPORTANT]
>
>Adobe建議您 [升級至最新的1.9.10版本](../assets/update-workfront-enhanced-connector.md) 的 [!DNL Workfront for Experience Manager enhanced connector].

## 已知问题 {#known-issues}

* 使用AEM 6.4設定專案連結資料夾時，Experience Manager不會儲存值 **[!UICONTROL 子資料夾]** 和 **[!UICONTROL 在具有投資組合的專案中建立連結資料夾]** 欄位。 的值 **[!UICONTROL 子資料夾]** 欄位更新至 **[!UICONTROL 未定義]** 和的值 **[!UICONTROL 在具有投資組合的專案中建立連結資料夾]** 欄位更新至 **[!UICONTROL 預設Portfolio]** 在儲存設定後自動執行。

* 當您使用傳統Workfront體驗時， **[!UICONTROL 傳送至]** 中可用的選項 **[!UICONTROL 更多]** 下拉式清單不允許您在Experience Manager中選取目標目的地。 此 **[!UICONTROL 傳送至]** 選項可透過以下方式正常運作： **[!UICONTROL 檔案動作]** 下拉式清單。 此 **[!UICONTROL 傳送至]** 選項正確運作於 **[!UICONTROL 更多]** 下拉式清單及 **[!UICONTROL 檔案動作]** 新Workfront Experience中可用的下拉式清單。

## 舊版 {#previous-releases}

### 2023年4月發行版本 {#april-2023-release}

[!DNL Workfront for Experience Manager enhanced connector] 1.9.9版（於2023年4月10日發行）包含下列更新：

* Experience Manager顯示 `DateTimeParseException` 連結資料夾建立期間從Workfront收到上次修改日期時發生例外狀況。

* 在短時間內建立多個連結的專案資料夾時出現問題。

* 無法設定一組新專案連結資料夾的臨界值限制。

### 2023年3月發行版本 {#march-2023-release}

[!DNL Workfront for Experience Manager enhanced connector] 1.9.8版（於2023年3月3日發行）包含下列更新：

* 改善在Workfront中建立專案連結資料夾時的Experience Manager效能。

* Workfront中的評論刪除現在會反映在Experience Manager中。

* 在as a Cloud Service於設定聯結器的Experience Manager上管理封鎖全新客戶的功能。


### 2023年1月發行版本 {#january-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 1.9.7版（於2023年2月2日發行）包含下列更新：

* 安裝1.9.6版後，中繼資料編輯器沒有列出Workfront自訂表單屬性。

* 開發主控台隨即顯示 `/content/dam/jcr:content/metadata/wfProjectURL not found` 安裝Workfront增強型聯結器並開啟Assets首頁後的錯誤訊息。

### 2022年12月發行版本 {#december-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 1.9.6版（於2009年12月發行）包含下列更新：

**增強功能**

<!--

* Workfront enhanced connector now allows you to use new search parameters to be more specific while defining folder names on large repositories.

-->

* Workfront增強型聯結器現在支援對資產和資料夾執行全文搜尋。

**错误修复**

* 檔案版本中繼資料未在Workfront和Experience Manager之間正確同步。
* 當資料夾使用的結構描述在全域設定中缺少定義時，建立連結到Workfront中Experience Manager的資料夾時出現問題。
* 由於載入時間比預期長，當您按一下任何欄位時，中繼資料結構描述編輯器表單會停止回應。 已新增自訂表單的特定OSGi設定以解決問題。 您新增至中繼資料結構描述編輯器的自訂表單名稱可在紀錄中取得。

### 2022年11月發行版本 {#november-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 1.9.5版（於11月11日發行）包含下列更新：

* 當您在Workfront中只為多值欄位定義一個值時，該欄位值未正確對應到Experience Manager。

* Experience Manager顯示 `SERVER_ERROR` 於 **[!UICONTROL 連結外部檔案和資料夾]** 存取資產資料夾時因為對的無效許可權而出現畫面 `/content/dam/collections`.

* 啟用 **[!UICONTROL 將資產發佈至Brand Portal]** Workfront增強型聯結器設定頁面上的選項會建立不正確的事件。 停用選項後，事件也不會被刪除。

   若要解決問題：

   1. 升級至增強型聯結器1.9.5版。

   1. 停用 **[!UICONTROL 將資產發佈至Brand Portal]** 選項（在進階設定下）。

   1. 啟用 **[!UICONTROL 將資產發佈至Brand Portal]** 選項。

   1. 刪除錯誤的事件訂閱。

      1. 執行GET呼叫至 `/attask/eventsubscription/api/v1/subscriptions?page=<page-number>`

         為每個頁碼執行一個API呼叫。

      1. 搜尋下列文字以尋找符合下列URL且沒有的事件訂閱 `objId`：

         ```
              "objId": "",
             "url": "<your-aem-domain>/bin/workfront-tools/events/linkedfolderprojectupdate<your-aem-domain>/
         ```

         確保內容介於 `"objId": "",` 和 `"url"` 符合JSON回應。 建議方法是從任何具有下列專案的「事件訂閱」複製： `objId` 然後刪除數字。

      1. 記下事件訂閱ID。

      1. 刪除錯誤的事件訂閱。 對進行Delete API呼叫 `<your-aem-domain>/attask/eventsubscription/api/v1/subscriptions/<event-subscription-ID-from-previous-step>`

         `200` 因為回應代碼表示成功刪除了錯誤的事件訂閱。
   >[!NOTE]
   >
   >如果您在執行此程式中所提及的步驟之前刪除了錯誤的事件訂閱，則可以跳過此程式的最後一個步驟。

### 2022年10月發行版本 {#october-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 1.9.4版（於2007年10月發行）包含下列更新：

* 由於大量事件，無法在增強型聯結器設定頁面上檢視「事件訂閱」索引標籤。

* Workfront無法擷取專案中現有資料夾的清單，因此會建立重複的資料夾。

### 2022年9月發行版本 {#september-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 版本1.9.3於9月16日發行，包含下列更新：

* 無法上傳大小超過8 GB的檔案。
* 自動發佈從Workfront傳送至AEM的資產時發生問題。
* 編輯預設中繼資料結構表單時，根路徑欄位不可用於標籤欄位。
* 使用AEM工作流程在Workfront中新增新版本時發生問題。
* 當您執行AEM搜尋Workfront中可用的資產時，AEM會顯示錯誤訊息。
* 當您從資產建立用於任務建立的AEM工作流程，但未定義父任務名稱時，任務不會在Workfront中建立。

### 2022年8月發行版本 {#august-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 1.9.2版（於2003年8月發行）包含下列更新：

* 此 **[!UICONTROL 上傳檔案]** 工作流程步驟無法將檔案附加至Workfront。

* 此 **[!UICONTROL 上傳檔案]** 工作流程步驟無法將檔案附加到Workfront中的任務和問題。 工作流程步驟已成功將檔案附加到專案。

### 2022年7月發行版本 {#july-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 1.9.1版包含下列更新：

* 針對移轉至Adobe IMS的執行個體，新增對Experience Manager與Workfront應用程式之間使用Workfront API金鑰進行驗證的支援。

* 當您連結外部檔案或資料夾時，Workfront應用程式會顯示 `SERVER_ERROR` 錯誤訊息。 錯誤訊息會因API金鑰不符而提及未經授權的例外狀況。

* 當您執行資產的「建立工作」工作流程時，「Null指標」例外會顯示在記錄訊息中。

* 當您啟用 `Replace Spaces with DASH` 「Experience Manager中的進階設定」底下的組態選項，會導致在Workfront中建立重複的資料夾。

### 2022年6月發行版本 {#june-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 現在包含下列更新：

* 當您透過連結的資料夾上傳或使用 `Send To` Workfront中可供上傳資產至Experience Manageras a Cloud Service的動作，資產會損毀，無法在Adobe Photoshop中開啟。

### 2022年3月發行版本 {#march-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 現在包含下列更新：

* 您現在可以在Adobe Workfront和AEM Assetsas a Cloud Service之間建立連結資料夾，即使有多個專案連結資料夾設定亦然。

* 新增對事件訂閱分頁的支援。

* 新增AEM 6.4.x支援。

* 新增對Proxy環境的支援。

* 根據合作夥伴和客戶的意見回應進行多項錯誤修正。

>[!MORELIKETHIS]
>
>* [整合 [!DNL Workfront for Experience Manager enhanced connector] 搭配Experience Manager6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-integrations.html?lang=en)

