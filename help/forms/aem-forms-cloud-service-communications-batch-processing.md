---
title: Experience Manager [!DNL Forms] as a Cloud Service通訊批次處理
description: 如何建立品牌導向和個人化的通訊？
exl-id: 542c8480-c1a7-492e-9265-11cb0288ce98
source-git-commit: 6b546f551957212614e8b7a383c38797cc21fba1
workflow-type: tm+mt
source-wordcount: '1693'
ht-degree: 2%

---

# 使用批次處理

通訊可讓您建立、組合及傳遞品牌導向的個人化通訊，例如商務往來函、檔案、報表、索賠處理信函、福利通知、索賠處理信函、每月帳單和歡迎套件。 您可以使用Communications API將範本(XFA或PDF)與客戶資料結合，以產生PDF、PS、PCL、DPL、IPL和ZPL格式的檔案。

通訊提供API用於隨選和排程檔案產生。 您可以將同步API用於隨選和批次API （非同步API）用於排程檔案產生：

* 同步API適用於隨選、低延遲和單一記錄檔案產生使用案例。 这些 API 更适用于基于用户操作的用例。例如，在使用者填寫表單後產生檔案。

* 批次API （非同步API）適用於排程的高輸送量多檔案產生使用案例。 这些 API 会批量生成文档。例如，每月生成的电话帐单、信用卡对帐单和收益对帐单。

<!-- The following skills are required to create templates and use HTTP APIs: 

* Understanding of Adobe Forms Designer or Acrobat Forms to create templates

* Understanding of HTTP APIs and experience of using HTTP APIs

* Basic understanding of Adobe Experience Manager -->


## 批次作業 {#batch-operations}

批次作業是以排定的間隔為一組記錄產生多個類似型別的檔案的程式。 批次操作有兩個部分：設定（定義）和執行。

* **設定（定義）**：批次設定會儲存各種資產和屬性的相關資訊，以便為產生的檔案設定。 例如，它會提供有關XDP或PDF範本和要使用的客戶資料位置的詳細資訊，並為輸出檔案指定各種屬性。

* **執行**：若要開始批次作業，請將批次設定名稱傳遞至批次執行API。

### 批次作業的元件 {#components-of-a-batch-operations}

**雲端設定**：Experience Manger雲端設定可協助您將Experience Manager執行個體連線到客戶擁有的Microsoft Azure儲存體。 它可讓您指定客戶擁有的Microsoft Azure帳戶認證，以便連線至該帳戶。

**批次資料存放區設定(USC)**：批次資料設定可協助您為批次API設定Blob儲存體的特定執行個體。 它可讓您指定客戶擁有的Microsoft Azure Blob儲存體中的輸入和輸出位置。

**批次API**：可讓您建立批次設定並根據這些設定執行批次執行，以將PDF或XDP範本與資料合併，並產生PDF、PS、PCL、DPL、IPL和ZPL格式的輸出。 通訊提供批次API用於設定管理和批次執行。

![data-merge-table](assets/communications-batch-structure.png)

**儲存**：通訊API會使用客戶擁有的Microsoft Azure雲端儲存空間來擷取客戶記錄並儲存產生的檔案。 您可以在Experience Manager Cloud Service設定中設定Microsoft Azure儲存體。

**應用程式**：使用批次API產生和使用檔案的自訂應用程式。

## 使用批次作業產生多個檔案 {#generate-multiple-documents-using-batch-operations}

您可以使用批次作業，以排定的間隔產生多個檔案。

>[!VIDEO](https://video.tv.adobe.com/v/338349)

您可以觀看影片或執行以下指示，瞭解如何使用批次操作產生檔案。 影片中使用的API參考檔案以.yaml格式提供。 您可以下載 [批次API](assets/batch-api.yaml) 將其檔案並上傳至Postman以檢查API的功能並觀看影片。

### 先決條件 {#pre-requisites}

若要使用「批次API」，需具備下列條件：

* [Microsoft Azure儲存體帳戶](https://docs.microsoft.com/en-us/azure/storage/common/storage-account-create)
* PDF或XDP範本
* [要與範本合併的資料](#form-data)
* 具有Experience Manager管理員許可權的使用者

### 設定您的環境 {#setup-your-environment}

使用批次作業之前：

* 將客戶資料（XML檔案）上傳至Microsoft Azure Blob Storage
* 建立雲端設定
* 建立批次資料存放區設定
* 將範本和其他資產上傳至您的Experience Manager FormsCloud Service執行個體

### 將客戶資料（XML檔案）上傳至Azure儲存體 {#upload-customer-data-to-Azure-Storage}

在您的Microsoft Azure儲存體上，建立 [容器](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs) 和 [上傳客戶資料(XML)](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container) 至 [資料夾](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-quickstart-blobs-portal) 在容器內。
>[!NOTE]
>
>您可以設定Microsoft Azure儲存體以自動清除輸入資料夾，或依排程間隔將輸出資料夾的內容移至其他位置。 不過，請確保當參考資料夾的批次作業仍在執行時，不會清除資料夾。

### 建立雲端設定 {#create-a-cloud-configuration}

雲端設定會將您的Experience Manager執行個體連線至Microsoft Azure儲存體。 若要建立雲端設定：

1. 前往「工具>Cloud Services> Azure儲存體」
1. 開啟要裝載設定的資料夾，然後按一下「建立」。 您可以使用全域資料夾或建立資料夾。
1. 指定要連線至服務的組態名稱和認證。 您可以 [從您的Microsoft Azure儲存體入口網站擷取這些認證](https://docs.microsoft.com/en-us/azure/storage/common/storage-account-keys-manage?tabs=azure-portal#view-account-access-keys).
1. 单击创建。

您的Experience Manager執行個體現在已準備好連線至Microsoft Azure Storage，並視需要用它來儲存和讀取內容。

### 建立批次資料存放區設定 {#create-batch-data-store-configuration}

批次資料設定可幫助您設定用於輸入和輸出的容器和資料夾。 您會將客戶記錄儲存在來源資料夾中，而產生的檔案會放置在目的地資料夾中。

若要建立組態：

1. 前往「工具> Forms >統一儲存聯結器」。
1. 開啟要裝載設定的資料夾，然後按一下「建立」。 您可以使用全域資料夾或建立資料夾。
1. 指定設定的標題和名稱。 在儲存體中，選取Microsoft Azure儲存體。
1. 在儲存體設定路徑中，瀏覽並選取包含客戶擁有的Azure儲存體帳戶認證的雲端設定。
1. 在來源資料夾中，指定Azure儲存體容器的名稱和包含記錄的資料夾。
1. 在目標資料夾中，指定Azure儲存體容器的路徑，以及儲存產生檔案的資料夾。
1. 单击创建。

您的Experience Manager執行個體現在已連線至Microsoft Azure儲存體，並設定為擷取資料並傳送至Microsoft Azure儲存體上的特定位置。

### 將範本和其他資產上傳到您的Experience Manager執行個體 {#upload-templates-and-other-assets-to-your-AEM-instance}

組織通常有多個範本。 例如，信用卡對帳單、福利對帳單及索賠申請各一個範本。 將所有此類XDP和PDF範本上傳到您的Experience Manager執行個體。 若要上傳範本：

1. 開啟您的Experience Manager執行個體。
1. 前往「Forms > Forms和檔案」
1. 按一下「建立>資料夾」並建立資料夾。 開啟資料夾。
1. 按一下「建立>檔案上傳」並上傳範本。

## 使用批次API產生檔案 {#use-batch-API-to-generate-documents}

若要使用批次API，請建立批次設定，並根據該設定執行執行。 API檔案提供建立和執行批次的API、對應引數和可能錯誤的相關資訊。 您可以下載 [API定義檔案](assets/batch-api.yaml) 檔案並上傳至 [Postman](https://go.postman.co/home) 或類似的軟體來測試API，以建立和執行批次作業。

### 建立批次 {#create-a-batch}

若要建立批次，請使用 `POST /config` API。 在HTTP要求內文中加入下列必要屬性：

* **configname**：指定批次的唯一名稱。 例如，`wknd-job`
* **dataSourceConfigUri**：指定批次資料存放區設定的位置。 可以是設定的相對或絕對路徑。 例如：`/conf/global/settings/forms/usc/batch/wknd-batch`
* **outputType**：指定輸出格式：PDF和列印。 如果您使用PRINT輸出型別，在 `printedOutputOptionsList` 屬性，請至少指定一個列印選項。 列印選項由其轉譯器型別識別，因此目前不允許使用相同轉譯器型別的多個列印選項。 支援的格式為PS、PCL、DPL、IPL和ZPL。

* **範本**：指定範本的絕對或相對路徑。 例如，`crx:///content/dam/formsanddocuments/wknd/statements.xdp`

如果您指定相對路徑，請提供內容根。 如需內容根的詳細資訊，請參閱API檔案。

<!-- For example, you include the following JSON in the body of HTTP APIs to create a batch named wknd-job: -->

您可以使用 `GET /config /[configName]` 以檢視批次設定的詳細資訊。

### 執行批次 {#run-a-batch}

若要執行（執行）批次，請使用 `POST /config /[configName]/execution`. 例如，若要執行名為wknd-demo的批次，請使用/config/wknd-demo/execution。 伺服器接受請求時會傳回HTTP回應代碼202。 除了伺服器上執行的批次處理作業的HTTP回應標頭中的唯一代碼(execution-identifier)外，API不會傳回任何裝載。 您可以使用執行識別碼來擷取批次的狀態。

>[!NOTE]
>
>批次執行期間，請勿對對應的來源和目的地資料夾、資料來源設定和Microsoft Azure雲端設定進行任何變更。

### 檢查批次的狀態 {#status-of-a-batch}

若要擷取批次的狀態，請使用 `GET /config /[configName]/execution/[execution-identifier]`. 執行識別碼包含在批次執行請求的HTTP回應標頭中。

狀態請求的回應包含狀態區段。 它提供有關批次工作狀態、已在管道中的記錄數（已讀取和正在處理）以及每個outputType/renderType（進行中、成功和失敗專案的數目）的詳細資訊。 狀態也包含批次工作的開始和結束時間，以及有關錯誤的資訊（若有）。 結束時間是–1，直到批次執行實際完成。

>[!NOTE]
>
>* 當您請求多個PRINT格式時，狀態包含多個專案。 例如，PRINT/ZPL、PRINT/IPL。
>* 批次工作不會同時讀取所有記錄，而是會持續讀取和增加記錄數量。 因此，在讀取所有記錄之前，狀態會傳回–1。


### 檢視產生的檔案 {#view-generated-documents}

工作完成後，產生的檔案會儲存至 `success` 在批次資料存放區設定中指定的目的地位置資料夾。 如果有任何錯誤，服務會建立 `failure` 資料夾。 它提供有關錯誤型別和原因的資訊。

讓我們透過範例來瞭解：假設有一個輸入資料檔案 `record1.xml` 以及兩種輸出型別： `PDF` 和 `PCL`. 然後目的地位置包含兩個子資料夾 `pdf` 和 `pcl`，每種輸出型別各一個。 讓我們假設PDF產生成功，然後 `pdf` 子資料夾包含 `success` 包含實際產生PDF檔案的子資料夾 `record1.pdf`. 假設PCL產生失敗，則 `pcl` 子資料夾包含 `failure` 包含錯誤檔案的子資料夾 `record1.error.txt` 其中包含錯誤的詳細資料。 此外，目的地位置還包含名為的暫存資料夾 `__tmp__` 會保留批次執行期間所需的某些檔案。 當沒有參考目標資料夾的有效批次執行時，可以刪除此資料夾。

>[!NOTE]
>
>根據輸入記錄的數量和範本的複雜性，處理批次可能需要一些時間，請等候幾分鐘，然後再檢查輸出檔案的目標資料夾。

## API參考檔案

API參考檔案提供API所提供的所有引數、驗證方法和各種服務的詳細資訊。 API參考檔案提供.yaml格式。 您可以下載 [批次API](assets/batch-api.yaml) 檔案並將其上傳至Postman以檢查API的功能。
