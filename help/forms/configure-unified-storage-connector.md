---
title: 如何設定AEM Forms的統一儲存聯結器？
description: 瞭解如何管理AEM Forms的統一儲存聯結器。 使用統一的儲存聯結器將AEM Forms連線到外部資料儲存體。
exl-id: c93d0242-0c15-4d69-82a1-d6fcc7da4bae
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 0%

---

# 管理AEM Forms的統一儲存聯結器 {#manage-unified-storage-connector}

您可以使用統一儲存聯結器將AEM Forms連線到外部資料儲存體。

例如，您可以在最適化表單中填寫欄位的值，並將其提交至AEM Workflow。 您可以進一步設定AEM Workflow將資料儲存在外部儲存空間，例如Microsoft Azure儲存伺服器。 使用統一的儲存聯結器在AEM Workflow和外部儲存裝置之間建立連線。

## 將AEM工作流程與Microsoft Azure儲存伺服器連線 {#connect-workflows-with-azure}

建立Azure儲存體設定，並使用統一儲存聯結器參照該設定。 然後，您可以設定AEM Workflow模型，將資料儲存區外部化，以將其連線至Azure儲存伺服器。

### 建立 [!DNL Azure] 儲存設定 {#create-azure-storage-configuration}

執行這些步驟之前，請確定您已 [!DNL Azure] 存放裝置帳戶與存取金鑰，用於授權存取 [!DNL Azure] 儲存體帳戶。

執行以下步驟來建立 [!DNL Azure] 儲存設定：

1. 導覽至 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Azure儲存體]**.
1. 選取資料夾以建立設定並點選 **[!UICONTROL 建立]**.
1. 在中指定設定的標題 **[!UICONTROL 標題]** 欄位。
1. 指定 [!DNL Azure] 中的儲存體帳戶 **[!UICONTROL Azure儲存體帳戶]** 欄位。
1. 指定用來存取Azure儲存體帳戶的金鑰 **[!UICONTROL Azure存取金鑰]** 欄位並點選 **[!UICONTROL 儲存]**.

### 設定AEM工作流程的統一儲存聯結器 {#configure-unified-storage-connector-workflows}

執行以下步驟，為AEM Workflow設定統一儲存聯結器：

1. 導覽至 **[!UICONTROL 工具]** > **[!UICONTROL Forms]** > **[!UICONTROL 統一的儲存聯結器]**.

1. 在 **[!UICONTROL 工作流程]** 區段，選取 **[!UICONTROL Azure]** 從「儲存」下拉式清單。
1. 指定 [Azure儲存體設定的設定路徑](#create-azure-storage-configuration) 在 **[!UICONTROL 儲存設定路徑]** 欄位。
1. 點選 **[!UICONTROL 發佈]** 然後點選 **[!UICONTROL 儲存]** 以儲存設定。

### 設定外部資料儲存的AEM Workflow模型 {#configure-workflow-external-data-storage}

執行以下步驟，為外部資料儲存設定AEM Workflow模型：

1. 導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]**.
1. 選取模型名稱並點選 **[!UICONTROL 編輯]**.
1. 點選「頁面資訊」圖示並點選 **[!UICONTROL 開啟屬性]**.
1. 選取 **[!UICONTROL 將工作流程資料儲存區外部化]**.
1. 點選 **[!UICONTROL 儲存並關閉]** 以儲存屬性。

>[!NOTE]
>
>當您設定外部資料儲存的AEM工作流程模型時，將指派任務步驟儲存為草稿以及擷取指派任務步驟的歷史記錄的選項會停用。

### 外部資料儲存的AEM工作流程准則 {#guidelines-workflows-external-data-storage}

以下是使用AEM Workflow並將資料儲存至外部資料儲存區(例如Microsoft Azure儲存伺服器)時的准則：

* 在工作流程模型步驟中定義輸入和輸出資料檔案及附件時，使用變數來儲存資料。 不要選取 **[!UICONTROL 相對於裝載]** 和 **[!UICONTROL 在絕對路徑上可用]** 選項。 此 **[!UICONTROL 相對於裝載]** 和 **[!UICONTROL 在絕對路徑上可用]** 選項不會在您之後自動顯示 [設定外部資料儲存的AEM Workflow模型](#configure-workflow-external-data-storage).

* 將最適化表單提交至AEM Workflow時，使用變數來儲存資料檔案和附件。 不要選取 **[!UICONTROL 相對於裝載]** 選項提交最適化表單至AEM Workflow。 此 **[!UICONTROL 相對於裝載]** 選項不會在您之後自動顯示 [設定外部資料儲存的AEM Workflow模型](#configure-workflow-external-data-storage).

* 請勿在工作流程模型中使用自訂AEM工作流程步驟來將資料儲存在CRX DE存放庫中。

* 當您 [設定外部資料儲存的AEM Workflow模型](#configure-workflow-external-data-storage)，請勿為AEM收件匣建立自訂欄，因為如果AEM收件匣中的工作專案屬於標籤為外部儲存的工作流程，則不會擷取自訂欄的值。
