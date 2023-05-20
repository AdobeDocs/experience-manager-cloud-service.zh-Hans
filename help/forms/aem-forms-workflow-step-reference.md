---
title: 如何將工作流程指派給其他使用者、傳送電子郵件、在工作流程中使用Adobe Sign？
description: 以Forms為中心的工作流程可讓您快速建立最適化Forms工作流程。 您可以使用Adobe Sign以電子方式簽署檔案、建立表單式業務流程、擷取資料並傳送至多個資料來源，以及傳送電子郵件通知
exl-id: e1403ba6-8158-4961-98a4-2954b2e32e0d
google-site-verification: A1dSvxshSAiaZvk0yHu7-S3hJBb1THj0CZ2Uh8N_ck4
source-git-commit: 3c8035e4db5729f58bae29136a32a0b9944d6a2f
workflow-type: tm+mt
source-wordcount: '7190'
ht-degree: 1%

---

# 以Forms為中心的AEM工作流程 — 步驟參考 {#forms-centric-workflow-on-osgi-step-reference}

您可以使用工作流程模型將商業邏輯轉換為自動化重複式處理。 模型可協助您定義並執行一系列步驟。 您也可以定義模型屬性，例如工作流程是暫時的或使用多個資源。 您可以 [在模型中加入各種AEM Workflow步驟以實現商業邏輯](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=en#extending-aem).

## 以Forms為中心的步驟 {#forms-workflow-steps}

以Forms為中心的工作流程步驟會在AEM Workflow中執行AEM Forms特定的操作。 這些步驟可讓您在OSGi上快速建立以Adaptive Forms為基礎的Forms工作流程。 這些工作流程可用於開發基本的稽核和核准工作流程、內部和跨防火牆業務流程。 您也可以使用Forms Workflow步驟來：

* 建立業務流程、提交後工作流程和後端工作流程，以管理註冊流程。

* 建立任務並指派給使用者或群組。

* 使用 [!DNL Adobe Sign] 在AEM Workflow中傳送檔案以供簽署。

* 隨選或提交表單時產生記錄檔案。

* 將工作流程模型與各種資料來源連線，以輕鬆儲存和擷取資料。

* 使用電子郵件步驟，在動作完成和工作流程開始或完成時傳送通知電子郵件和其他附件。

>[!NOTE]
>
>如果將工作流程模型標示為外部儲存，則對於所有Forms工作流程步驟，您只能選取變數選項來儲存或擷取資料檔案和附件。


## 指派任務步驟 {#assign-task-step}

指派任務步驟會建立工作專案並將其指派給使用者或群組。 除了指派工作外，元件也會指定工作的最適化表單或非互動式PDF。 最適化表單必須接受使用者的輸入，且非互動式PDF或使用唯讀最適化表單進行僅稽核工作流程。

您也可以使用元件來控制工作的行為。 例如，建立自動記錄檔案、將任務指派給特定使用者或群組、指定提交資料的路徑、指定要預先填入的資料路徑，以及指定預設動作。 「指派工作」步驟具有以下屬性：

* **[!UICONTROL 標題]**：任務的標題。 標題會顯示在AEM收件匣中。
* **[!UICONTROL 說明]**：說明在任務中執行的操作。 當您在共用開發環境中工作時，此資訊對於其他程式開發人員很有用。

* **[!UICONTROL 縮圖路徑]**：任務縮圖的路徑。 若未指定路徑，則會針對最適化表單顯示預設縮圖，而針對記錄檔案，則會顯示預設圖示。
* **[!UICONTROL 工作流程階段]**：工作流程可以有多個階段。 這些階段會顯示在AEM收件匣中。 您可以在模型屬性中定義這些階段（Sidekick >頁面>頁面屬性>階段）。
* **[!UICONTROL 優先順序]**：選取的優先順序會顯示在AEM收件匣中。 可用的選項包括「高」、「中」和「低」。 預設值為Medium。
* **[!UICONTROL 到期日期]**：指定在幾天或幾小時後任務會標籤為過期。 如果您選取 **[!UICONTROL 關閉]**，則不會將任務標示為過期。 您也可以指定逾時處理常式，以便在任務逾期後執行特定任務。

* **[!UICONTROL 天]**：任務完成前的天數。 將任務指派給使用者後會計入天數。 如果任務未完成並超過「天數」欄位中指定的天數，則如果選取，逾時處理常式會在到期日後觸發。
* **[!UICONTROL 小時]**：完成任務之前的小時數。 將任務指派給使用者後會計入小時數。 如果任務未完成並超過「時數」欄位中指定的時數，則如果選取，逾時處理常式會在到期時數之後觸發。
* **[!UICONTROL 到期日後逾時]**：選取此選項以啟用「逾時處理常式」選取欄位。
* **[!UICONTROL 逾時處理常式]**：選取指派任務步驟超過到期日時要執行的指令碼。 放置在CRX存放庫中的指令碼： [應用程式]/fd/dashboard/scripts/timeoutHandler可供選取。 crx-repository中不存在指定的路徑。 管理員會在使用之前建立路徑。
* **[!UICONTROL 在任務詳細資訊中反白顯示上一個任務的動作和註解]**：選取此選項可顯示上次在任務的任務詳細資訊區段上採取的動作和收到的註解。
* **[!UICONTROL 型別]**：選擇工作流程啟動時要填寫的檔案型別。 您可以選擇最適化表單、唯讀最適化表單、非互動式PDF檔案。

<!-- , Interactive Communication Agent UI, or Interactive Communication Web Channel Document. -->


* **[!UICONTROL 使用最適化表單]**：指定尋找輸入的最適化表單的方法。 如果您從「型別」下拉式清單中選取「最適化表單」或「唯讀最適化表單」，即可使用此選項。 您可以使用提交至工作流程的最適化表單、在絕對路徑下提供的表單，或在變數中的路徑下提供的表單。 您可以使用字串型別的變數來指定路徑。\
   您可以將多個最適化Forms與工作流程建立關聯。 因此，您可以使用可用的輸入法，在執行階段指定最適化表單。

<!-- 

* **[!UICONTROL Use Interactive Communication]**: Specify the method to locate the input interactive communication. You can use the interactive communication submitted to the workflow, available at an absolute path, or available at a path in a variable. You can use a variable of type String to specify the path. This option is available if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list. 

> [!NOTE]
>
>You must have cm-agent-users and workflow-users group assignments to access Interactive Communications Agent UI in AEM inbox.  

-->

* **[!UICONTROL 最適化表單路徑]**：指定自適應表單的路徑。 您可以使用提交至工作流程的最適化表單（可在絕對路徑中使用），或從儲存在字串資料型別變數中的路徑擷取最適化表單。
* **[!UICONTROL 選擇輸入PDF，使用]**：指定非互動式PDF檔案的路徑。 當您在「型別」欄位中選擇非互動式PDF檔案時，該欄位可用。 您可以使用相對於承載的路徑、以絕對路徑儲存的路徑，或使用Document資料型別的變數來選取輸入PDF。 例如， [Payload_Directory]/Workflow/PDF/credit-card.pdf. crx-repository中不存在該路徑。 管理員會在使用之前建立路徑。 您需要啟用記錄檔案選項或基於表單範本的最適化Forms才能使用PDF路徑選項。
* **[!UICONTROL 對於已完成的工作，將最適化表單轉譯為]**：當任務標示為完成時，您可以將最適化表單轉譯為唯讀最適化表單或PDF檔案。 您需要啟用記錄檔案選項或表單範本式的最適化Forms，才能將最適化表單呈現為記錄檔案。
* **[!UICONTROL 預先填入]**：下列欄位會作為任務的輸入專案：

   * **[!UICONTROL 選擇輸入資料檔案，使用]**：輸入資料檔案的路徑（.json、.xml、.doc或表單資料模型）。 您可以使用相對於承載的路徑來擷取輸入資料檔案，或擷取儲存在Document、XML或JSON資料型別變數中的檔案。 例如，檔案包含透過AEM收件匣應用程式為表單提交的資料。 範例路徑為 [Payload_Directory]/workflow/data.
   * **[!UICONTROL 選擇輸入附件，使用]**：此位置可用的附件會附加至與任務相關聯的表單。 路徑可以是相對於承載或擷取儲存在檔案變數中的附件。 範例路徑為 [Payload_Directory]/attachments/. 您可以指定相對於承載放置的附件，或使用檔案型別（「陣列清單」>「檔案」）變數來指定最適化表單的輸入附件。

   <!-- 
    
    * **[!UICONTROL Choose input JSON]**: Select an input JSON file using a path that is relative to payload or stored in a variable of Document, JSON, or Form Data Model data type. This option is available if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list.

    * **[!UICONTROL Choose a custom prefill service]**: Select the prefill service to retrieve the data and prefill the Interactive Communication Web channel document or the Agent UI.  
    
    * **[!UICONTROL Use the prefill service of the interactive communication selected above]**: Use this option to use the prefill service of the Interactive Communication defined in the Use Interactive Communication drop-down list. 
    
    -->

   * **[!UICONTROL 請求屬性對應]**：使用請求屬性對應區段來定義 [要求屬性的名稱和值](work-with-form-data-model.md#bindargument). 根據請求中指定的屬性名稱和值，從資料來源擷取詳細資訊。 您可以使用常值或String資料型別的變數來定義請求屬性值。

   <!--  
     
     The prefill service and request attribute mapping options are available only if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list. 
     
     -->

* **[!UICONTROL 已提交的資訊]**：下列欄位會作為工作的輸出位置：

   * **[!UICONTROL 儲存輸出資料檔案，使用]**：儲存資料檔案（.json、.xml、.doc或表單資料模型）。 資料檔案包含透過相關表單提交的資訊。 您可以使用相對於承載的路徑來儲存輸出資料檔案，或將其儲存在Document、XML或JSON資料型別的變數中。 例如， [Payload_Directory]/Workflow/data，其中資料是檔案。
   * **[!UICONTROL 儲存附件，使用]**：儲存任務中提供的表單附件。 您可以使用相對於承載的路徑來儲存附件，或將其儲存在「檔案」資料型別的陣列清單中。
   * **[!UICONTROL 儲存記錄檔案，使用]**：儲存記錄檔案檔案的路徑。 例如， [Payload_Directory]/DocumentofRecord/credit-card.pdf. 您可以使用相對於承載的路徑來儲存記錄檔案，或將其儲存在Document資料型別的變數中。 如果您選取 **[!UICONTROL 相對於裝載]** 選項，如果路徑欄位留空，則不會產生記錄檔案。 只有當您從「型別」下拉式清單中選取「最適化表單」時，此選項才可用。

   <!-- 
    
    * **[!UICONTROL Save Web Channel data using]**: Save the Web Channel data file using a path that is relative to the payload or store it in a variable of Document, JSON, or Form Data Model data type. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list. c
    * **[!UICONTROL Save PDF document using]**: Save the PDF document using a path that is relative to the payload or store it in a variable of Document data type. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list.
    <!-- * **[!UICONTROL Save layout template using]**: Save the layout template using a path that is relative to the payload or store it in a variable of Document data type. The [layout template](layout-design-details.md) refers to an XDP file that you create using Forms Designer. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list. 
    
    -->

* **[!UICONTROL 被指定者]** > **[!UICONTROL 指派選項]**：指定將任務指派給使用者的方法。 您可以使用「參與者選擇器」指令碼動態地將任務指派給使用者或群組，或將任務指派給特定的AEM使用者或群組。
* **[!UICONTROL 參與者選擇器]**：此選項可在以下情況下使用： **[!UICONTROL 動態至使用者或群組]** 在「指派選項」欄位中選取選項。 您可以使用ECMAScript或服務來動態選取使用者或群組。 如需詳細資訊，請參閱 [動態指派工作流程給使用者](https://helpx.adobe.com/experience-manager/kb/HowToAssignAWorkflowDynamicallyToParticipants.html) 和 [建立自訂Adobe Experience Manager動態參與者步驟。](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en&amp;CID=RedirectAEMCommunityKautuk)

* **[!UICONTROL 參與者]**：此欄位適用於 **[!UICONTROL com.adobe.granite.workflow.core.process.RandomParticipantChooser]** 選項已選取 **[!UICONTROL 參與者選擇器]** 欄位。 欄位可讓您為RandomParticipantChooser選項選取使用者或群組。

* **[!UICONTROL 被指定者]**：此欄位適用於 **[!UICONTROL com.adobe.fd.workspace.step.service.VariableParticipantChooser]** 已選取以下專案中的 **[!UICONTROL 參與者選擇器]** 欄位。 欄位可讓您選取字串資料型別的變數，以定義受託人。

* **[!UICONTROL 引數]**：在「參與者選擇器」欄位中選取RandomParticipantChoose指令碼以外的指令碼時，該欄位可用。 欄位可讓您為「參與者選擇器」欄位中選取的指令碼提供逗號分隔引數清單。

* **[!UICONTROL 使用者或群組]**：任務已指派給所選的使用者或群組。 選項適用於 **[!UICONTROL 至特定使用者或群組選項]** 已選取以下專案中的 **[!UICONTROL 指派選項]** 欄位。 欄位會列出以下專案的所有使用者和群組： [!DNL workflow-users] 群組。\
   此 **[!UICONTROL 使用者或群組]** 下拉式功能表會列出登入使用者有權存取的使用者和群組。 使用者名稱的顯示取決於您是否擁有 **[!UICONTROL 使用者]** crx-repository中該特定使用者的節點。

* **[!UICONTROL 傳送通知電子郵件]**：選取此選項以傳送電子郵件通知給受指派人。 這些通知會在任務指派給使用者或群組時傳送。 您可以使用 **[!UICONTROL 收件者電子郵件地址]** 用於指定擷取電子郵件地址的機制的選項。

* **[!UICONTROL 收件者電子郵件地址]**：您可以將電子郵件地址儲存在變數中、使用常值來指定永久電子郵件地址，或使用受指派人設定檔中指定之受指派人的預設電子郵件地址。 您可以使用常值或變數來指定群組的電子郵件地址。 變數選項有助於動態擷取和使用電子郵件地址。 此 **[!UICONTROL 使用受指派人的預設電子郵件地址]** 選項僅適用於單一受指派人。 在此情況下，會使用儲存在受指派人使用者設定檔中的電子郵件地址。

* **[!UICONTROL HTML電子郵件範本]**：選取通知電子郵件的電子郵件範本。 若要編輯範本，請修改crx-repository中/libs/fd/dashboard/templates/email/htmlEmailTemplate.txt的檔案。
* **[!UICONTROL 允許委派至]**：AEM收件匣為登入使用者提供一個選項，將指派的工作流程委派給其他使用者。 您可以委派給相同群組內的工作流程使用者，或委派給其他群組的工作流程使用者。 如果任務指派給單一使用者並且 **[!UICONTROL 允許委派給受指派人群組的成員]** 選項，則無法將任務委派給其他使用者或群組。
* **[!UICONTROL 共用設定]**： AEM收件匣提供選項，讓您與其他使用者共用收件匣中的單一或所有任務：
   * 當 **[!UICONTROL 允許受分派者在收件匣中明確共用]** 選項，使用者可以在AEM收件匣中選取任務，並與其他AEM使用者共用。
   * 當 **[!UICONTROL 允許受分派者透過收件匣共用進行共用]** 選項已選取，且使用者共用其收件匣專案或允許其他使用者存取其收件匣專案，只有先前提及的選項已啟用的任務才會與其他使用者共用。
   * 當 **[!UICONTROL 允許受分派者使用「休假中」設定進行委派]** 「 」已選取。 受指派人可以啟用將任務委派給其他使用者的選項以及其他外出選項。 任何指派給休假使用者的新任務都會自動委派（指派）給休假設定中提到的使用者。

   它可讓其他使用者在休假時挑選受指派人任務，並且無法處理受指派任務。

* **[!UICONTROL 動作]** > **[!UICONTROL 預設動作]**：立即可用「提交」、「儲存」和「重設」動作。 預設會啟用所有預設動作。
* **[!UICONTROL 路由變數]**：路由變數的名稱。 路由變數會擷取使用者在AEM收件匣中選擇的自訂動作。
* **[!UICONTROL 路由]**：任務可以分支至不同的路由。 在AEM收件匣中選取時，路由會傳回值，而工作流程會根據選取的路由進行分支。 您可以將路由儲存在String資料型別陣列的變數中，或選取 **[!UICONTROL 常值]** 以手動新增路由。

* **[!UICONTROL 路由標題]**：指定路由的標題。 它會顯示在AEM收件匣中。
* **[!UICONTROL 珊瑚圖示]**：指定Coral圖示的HTML屬性。 AdobeCorelUI資料庫提供一組龐大的觸控優先圖示。 您可以選擇並使用路由圖示。 它會與標題一起顯示在AEM收件匣中。 如果您將路由儲存在變數中，路由會使用預設的「標籤」珊瑚圖示。
* **[!UICONTROL 允許受分派者新增註解]**：選取此選項可啟用任務的註解。 受分派者可在任務提交時從AEM收件匣新增註解。
* **[!UICONTROL 將註解儲存在變數中]**：將註解儲存在String資料型別的變數中。 只有在選取 **[!UICONTROL 允許受分派者新增註解]** 核取方塊。

* **[!UICONTROL 允許受分派者將附件新增至工作]**：選取此選項可啟用工作的附件。 受指派人可在任務提交時從AEM收件匣新增附件。 您也可以限制大小上限 **[!UICONTROL （檔案大小上限）]** 附件的URL。 預設大小為2 MB。

* **[!UICONTROL 儲存輸出工作附件，使用]**：指定附件資料夾的位置。 您可以使用相對於承載的路徑或在檔案資料型別陣列的變數中儲存輸出工作附件。 只有在選取 **[!UICONTROL 允許受分派者將附件新增至工作]** 核取方塊並選取 **[!UICONTROL 最適化表單]**， **[!UICONTROL 唯讀最適化表單]**，或 **[!UICONTROL 非互動式PDF檔案]** 從 **[!UICONTROL 型別]** 中的下拉式清單 **[!UICONTROL 表單/檔案]** 標籤。

* **[!UICONTROL 使用自訂中繼資料]**：選取此選項以啟用自訂中繼資料欄位。 自訂中繼資料用於電子郵件範本。
* **[!UICONTROL 自訂中繼資料]**：選取電子郵件範本的自訂中繼資料。 自訂中繼資料可在crx-repository的apps/fd/dashboard/scripts/metadataScripts取得。 crx-repository中不存在指定的路徑。 管理員會在使用之前建立路徑。 您也可以使用自訂中繼資料的服務。 您也可以擴充 `WorkitemUserMetadataService` 介面以提供自訂中繼資料。
* **[!UICONTROL 顯示先前步驟的資料]**：選取此選項可讓受指派人檢視先前的受指派人、已對任務採取的動作、新增至任務的註釋，以及已完成任務的記錄檔案（若有）。
* **[!UICONTROL 顯示後續步驟的資料]**：選取此選項可讓目前的受指派人檢視後續受指派人採取的動作及新增至任務的註解。 也可讓目前受指派人檢視已完成工作的記錄檔案（若有）。
* **[!UICONTROL 資料型別的可見度]**：依預設，受指派人可以檢視記錄檔案、受指派人、採取的動作，以及之前和後續受指派人新增的註解。 使用資料型別可見性選項來限制受託人可見的資料型別。

>[!NOTE]
>
>當您設定外部資料儲存的AEM工作流程模型時，將指派任務步驟儲存為草稿以及擷取指派任務步驟的歷史記錄的選項會停用。 此外，收件匣中已停用儲存的選項。

## 轉換為PDF/A步驟 {#convert-pdfa}

PDF/A是一種封存格式，用於透過嵌入字型和解壓縮檔案來長期儲存檔案內容。 因此，PDF/A 文档通常比标准 PDF 文档大。您可以使用 ***轉換為PDF/A*** 在AEM工作流程中步驟，將PDF檔案轉換為PDF/A格式。

轉換成PDF/A步驟具有以下屬性：

**[!UICONTROL 輸入檔案]**：輸入檔案可相對於裝載、具有絕對路徑、可作為裝載提供或儲存在Document資料型別的變數中。

**[!UICONTROL 轉換選項]**：使用此屬性可指定將PDF檔案轉換為PDF/A檔案的設定。 此標籤下可用的各種選項包括：
* **[!UICONTROL 合規性]**：指定輸出PDF/A檔案必須符合的標準。 它支援不同的PDF標準，例如PDF/A-1b、PDF/A-2b或PDF/A-3b。
* **[!UICONTROL 結果層級]**：將轉換輸出的結果層級指定為PassFail、Summary或Detailed。
* **[!UICONTROL 色域]**：將預先定義的色域指定為S_RGB、COATED_FOGRA27、JAPAN_COLOR_COATED或SWOP，可用於輸出PDF/A檔案。
* **[!UICONTROL 選擇性內容]**：只有在符合指定的標準集時，才允許在輸出PDF/A檔案中顯示特定圖形物件和/或註釋。

**[!UICONTROL 輸出檔案]**：指定儲存輸出檔案的位置。 輸出檔案可儲存在相對於承載的位置、覆寫承載（如果承載是檔案）或是Document資料型別的變數。


## 傳送電子郵件步驟 {#send-email-step}

使用電子郵件步驟來傳送電子郵件，例如包含記錄檔案、最適化表單連結的電子郵件 <!-- , link of an interactive communication-->，或是附加了PDF檔案。 傳送電子郵件步驟支援 [HTML電子郵件](https://en.wikipedia.org/wiki/HTML_email). HTML電子郵件會迅速回應，並因應收件者的電子郵件使用者端和熒幕大小。 您可以使用HTML電子郵件範本來定義電子郵件的外觀、色彩配置和行為。

電子郵件步驟使用Day CQ Mail Service來傳送電子郵件。 在使用電子郵件步驟之前，請確定已設定電子郵件服務。 預設情況下，電子郵件僅支援HTTP和HTTP通訊協定。 [聯絡支援團隊](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=en#sending-email) 啟用傳送電子郵件的連線埠，並為您的環境啟用SMTP通訊協定。 此限制有助於改善平台的安全性。

電子郵件步驟具有以下屬性：

**[!UICONTROL 標題]**：步驟的標題有助於識別工作流程編輯器中的步驟。

**[!UICONTROL 說明]**：當您在共用開發環境中工作時，此說明對於其他程式開發人員非常有用。

**[!UICONTROL 電子郵件主旨]**：您可以從工作流程中繼資料中擷取主旨、手動指定，或從變數中儲存的值中擷取。 從下列選項中選取：

* **[!UICONTROL 常值]** 手動指定主旨。
* **[!UICONTROL 從工作流程中繼資料擷取]**  — 從中繼資料屬性擷取主旨。
* **[!UICONTROL 變數]**  — 從字串資料型別變數中儲存的值擷取主旨。

**[!UICONTROL HTML電子郵件範本]**：電子郵件的HTML範本。 您可以在電子郵件範本中指定變數。 「電子郵件步驟」會擷取並顯示範本中包含的所有變數，以供您輸入。

**[!UICONTROL 電子郵件範本中繼資料]**：電子郵件範本變數的值可以是使用者指定的值、作者或發佈伺服器上的資產路徑、影像，或工作流程中繼資料屬性。

* **[!UICONTROL 常值]**：當您知道要指定的確切值時，請使用選項。 例如， [example@example.com](mailto:example@example.com).

* **[!UICONTROL 工作流程中繼資料]**：當要使用的值儲存至工作流程中繼資料屬性時，請使用選項。 選取選項後，在「工作流程中繼資料」選項下方的空白文字方塊中輸入中繼資料屬性名稱。 例如，emailAddress。

<!-- 

* **[!UICONTROL Asset URL]**: Use the option to embed a web link of an interactive communication to the email. After selecting the option, browse and choose the interactive communication to embed. The asset can reside on the author or the publish server. 

-->

* **[!UICONTROL 影像]**：使用選項將影像內嵌至電子郵件。 選取選項後，瀏覽並選擇影像。 影像選項僅適用於電子郵件範本中可用的影像標籤(&lt;img src=&quot;&lt;span id=&quot; translate=&quot;no&quot; />「/>」)。&#42;

**[!UICONTROL 寄件者/收件者的電子郵件地址]**：選取 **[!UICONTROL 常值]** 手動指定電子郵件地址或選取 **[!UICONTROL 從工作流程中繼資料擷取]** 從中繼資料屬性擷取電子郵件地址的選項。 您也可以為以下專案指定中繼資料屬性陣列清單： **[!UICONTROL 從工作流程中繼資料擷取]** 選項。 選取 **[!UICONTROL 變數]** 用於從儲存在字串資料型別變數中的值擷取電子郵件地址的選項。

* **[!UICONTROL 檔案附件]**：在指定位置可用的資產會附加至電子郵件。 資產的路徑可以是相對於承載或絕對路徑。 範例路徑為 [Payload_Directory]/attachments/.

選取 **[!UICONTROL 變數]** 用於擷取儲存在Document、XML或JSON資料型別變數中的檔案附件的選項。

**[!UICONTROL 檔案名稱]**：電子郵件附件檔案的名稱。 「電子郵件步驟」會將附件的原始檔案名稱變更為指定的檔案名稱。 可手動指定名稱，或從工作流程中繼資料屬性或變數中擷取名稱。 使用 **[!UICONTROL 常值]** 選項。 使用 **[!UICONTROL 變數]** 從儲存在字串資料型別變數中的值擷取檔案名稱的選項。 使用 **[!UICONTROL 從工作流程中繼資料擷取]** 選項（當要使用的值儲存在工作流程中繼資料屬性中時）。

## 產生記錄檔案步驟 {#generate-document-of-record-step}

填寫或提交表單時，您可以以列印或檔案格式保留表單記錄。 此記錄稱為記錄檔案(DoR)。 您可以使用「產生記錄檔案」步驟來建立最適化表單的唯讀或互動式PDF版本。 PDF版本包含填寫至表單的資訊以及最適化表單的版面。

「記錄檔案」步驟具有以下屬性：

**[!UICONTROL 使用最適化表單]**：指定尋找輸入的最適化表單的方法。 您可以使用提交至工作流程的最適化表單、在絕對路徑下提供的表單，或在變數中的路徑下提供的表單。 您可以使用String資料型別的變數，在 **[!UICONTROL 選取要解析的變數]** 欄位。\
您可以將多個最適化Forms與工作流程建立關聯。 因此，您可以使用可用的輸入法，在執行階段指定最適化表單。

**[!UICONTROL 最適化表單路徑]**：指定自適應表單的路徑。 當您選取 **[!UICONTROL 在絕對路徑上可用]** 選項來自 **[!UICONTROL 使用最適化表單]** 欄位。

**[!UICONTROL 選擇輸入資料，使用]**：最適化表單的輸入資料路徑。 您可以將資料保留在相對於承載的位置、指定資料的絕對路徑，或擷取儲存在Document、JSON或XML資料型別變數中的資料。 輸入資料會與最適化表單合併，以建立記錄檔案。

**[!UICONTROL 選擇輸入附件路徑，使用]**：附件的路徑。 這些附件包含在記錄檔案中。 您可以將附件保持在相對於承載的位置、指定附件的絕對路徑，或擷取儲存在「檔案」資料型別陣列中的附件。

如果您指定資料夾的路徑（例如附件），則資料夾中直接可用的所有檔案都會附加至記錄檔案。 如果在指定附件路徑中直接可用的資料夾中有任何檔案可用，則這些檔案會作為附件包含在記錄檔案中。 如果在直接可用的資料夾中有任何資料夾，則會略過這些資料夾。

**[!UICONTROL 使用以下選項儲存產生的記錄檔案]**：指定保留記錄檔案檔案的位置。 您可以選擇覆寫裝載資料夾、將記錄檔案放在裝載目錄內的某個位置，或將記錄檔案儲存在「檔案」資料型別的變數中。

**[!UICONTROL 地區設定]**：指定記錄檔案的語言。 選取 **[!UICONTROL 常值]** 從下拉式清單中選取地區設定或選取 **[!UICONTROL 變數]** 以從儲存在字串資料型別變數中的值擷取地區設定。 在變數中儲存地區設定的值時，定義地區設定代碼。 例如，指定 **en_US** 英文版和 **fr_FR** 法文版。

## 叫用DDX步驟 {#invokeddx}

檔案描述XML (DDX)是一種宣告式標籤語言，其元素代表檔案的建置組塊。 这些构建块包括 PDF 和 XDP 文档以及其他元素，例如注释、书签和样式文本。DDX定義了一組作業，可套用在一或多個輸入檔案上，以產生一或多個輸出檔案。 单个 DDX 可用于一系列源文档。您可以使用 ***叫用DDX步驟*** 在AEM工作流程中執行各種操作，例如組譯和解譯檔案、建立和修改Acrobat和XFA Forms，以及中描述的其他操作。 [DDX參考檔案](https://helpx.adobe.com/content/dam/help/en/experience-manager/forms-cloud-service/ddxRef.pdf).

叫用DDX步驟具有下列屬性：

**[!UICONTROL 輸入檔案]**：用於設定輸入檔案的屬性。 此標籤下可用的各種選項包括：
* **[!UICONTROL 指定DDX，使用]**：指定相對於承載的輸入檔案、具有絕對路徑、可作為承載提供，或儲存在Document資料型別的變數中。
* **[!UICONTROL 從承載建立地圖]**：將裝載資料夾下的所有檔案新增至輸入檔案的對應，以用於組合器中的invoke API。 每個檔案的節點名稱都會當做對應中的索引鍵。
* **[!UICONTROL 輸入檔案的地圖]**：選項是用來新增多個專案，使用 **[!UICONTROL 新增]** 按鈕。 每個專案代表檔案在地圖中的索引鍵和檔案的來源。

**[!UICONTROL 環境選項]**：此選項用於設定叫用API的處理設定。 此標籤下可用的各種選項包括：
* **[!UICONTROL 僅驗證]**：檢查輸入DDX檔案的有效性。
* **[!UICONTROL 因錯誤而失敗]**：表示叫用API服務是否失敗（如果發生錯誤）的布林值。 預設情況下，其值設定為False。
* **[!UICONTROL 第一個Bates數字]**：指定自動遞增的數字。 此自我遞增數字會自動顯示在每個連續頁面上。
* **[!UICONTROL 預設樣式]**：設定輸出檔案的預設樣式。

>[!NOTE]
>
>環境選項會與HTTP API保持同步。

**[!UICONTROL 輸出檔案]**：指定儲存輸出檔案的位置。 此標籤下可用的各種選項包括：
* **[!UICONTROL 將輸出儲存在承載中]**：將輸出檔案儲存在承載資料夾下，或覆寫承載，如果承載是檔案。
* **[!UICONTROL 輸出檔案的地圖]**：指定明確儲存每個檔案檔案的位置，方法是在每個檔案中新增一個專案。 每個專案代表檔案以及儲存檔案的位置。 如果有多個輸出檔案，則使用此選項。

## 啟動表單資料模型服務步驟 {#invoke-form-data-model-service-step}

您可以使用 [[!DNL AEM Forms] 資料整合](data-integration.md) 以設定並連線至不同的資料來源。 這些資料來源可以是Web服務、REST服務、OData服務和CRM解決方案。 [!DNL AEM Forms] 資料整合可讓您建立包含各種服務的表單資料模型，以執行資料擷取、新增、更新已設定之資料庫的作業。 您可以使用 **[!UICONTROL 啟動資料模型服務步驟]** 以選取表單資料模型(FDM)並使用FDM的服務來擷取、更新或新增資料至不同的資料來源。

為了說明步驟欄位的輸入，以下資料庫表格和JSON檔案為範例：

**[!UICONTROL 範例CustomerDetails表格]**

<table>
 <tbody> 
  <tr> 
   <td>属性</td> 
   <td>价值<br /> </td> 
  </tr> 
  <tr> 
   <td>名字<br /> </td> 
   <td>Sarah<br /> </td> 
  </tr> 
  <tr> 
   <td>姓氏</td> 
   <td>玫瑰</td> 
  </tr> 
  <tr> 
   <td>客戶ID</td> 
   <td>1</td> 
  </tr> 
  <tr> 
   <td>电子邮件地址<br /> </td> 
   <td>srose@we.info</td> 
  </tr> 
 </tbody> 
</table>

**[!UICONTROL 範例JSON檔案]**

```json
  { 
    customer: { 
     firstName: "Sarah", 
     lastName:"Rose", 
     customerId: "1", 
     emailAddress:"srose@we.info" 
   }, 
    insurance: {
     customerId: "1", 
    policyType: "Premium,
    policyNumber: "Premium-521499",
    customerDetails: { 
     firstName: "Sarah",
     lastName: "Rose",
     customerId: "1",
     emailAddress: "srose@we.info" 
    }
   }
  }
```

「叫用表單資料模型服務」步驟包含下列欄位，以利表單資料模型作業：

* **[!UICONTROL 標題]**：步驟的標題。 它有助於識別工作流程編輯器中的步驟。
* **[!UICONTROL 說明]**：說明適用於在共用開發環境中工作的其他程式開發人員。

* **[!UICONTROL 表單資料模型路徑]**：瀏覽並選取伺服器上顯示的表單資料模型。

* **[!UICONTROL 錯誤與驗證]**：選項可讓您擷取錯誤訊息，並為擷取及傳送至資料來源的資料指定驗證選項。 透過這些變更，您可以確保傳遞至叫用表單資料模型服務步驟的資料會遵守資料來源定義的資料限制。 如需詳細資訊，請參閱 [自動驗證輸入資料](work-with-form-data-model.md#automated-validation-of-input-data)

* **[!UICONTROL 驗證層級]**：驗證分為三類：基本、完整和關閉：

   * 完整：所有限制均已驗證。
   * 基本：僅限必要和空的限制
   * OFF：不會進行驗證。

* **[!UICONTROL 失敗時終止工作流程]**：當限制無法驗證時，工作流程會停止。

* **[!UICONTROL 將錯誤代碼儲存在變數中]**：您可以將錯誤碼儲存在 [字串型別變數](variable-in-aem-workflows.md).

* **[!UICONTROL 將錯誤訊息儲存在變數中]**：您可以將錯誤訊息儲存在 [字串型別變數](variable-in-aem-workflows.md).

* **[!UICONTROL 在變數中儲存錯誤詳細資料]**：您可以將錯誤詳細資料儲存在 [JSON型別變數](variable-in-aem-workflows.md).

* **[!UICONTROL 服務]**：所選表單資料模型提供的服務清單。
* **[!UICONTROL 服務輸入]** > **[!UICONTROL 提供使用常值、變數或工作流程中繼資料的輸入資料，以及JSON檔案]**：服務可以有多個引數。 選取選項，從工作流程中繼資料屬性、JSON物件、變數取得服務引數的值，或直接在提供的文字方塊中輸入值：

   * **[!UICONTROL 常值]**：當您知道要指定的確切值時，請使用選項。 例如，srose@we.info。
   * **[!UICONTROL 變數]**：使用選項來擷取儲存在變數中的值。
   * **[!UICONTROL 從工作流程中繼資料擷取]**：當要使用的值儲存至工作流程中繼資料屬性時，請使用選項。 例如，emailAddress。

   * **[!UICONTROL 相對於裝載]**：使用選項來擷取儲存在相對於承載路徑中的檔案附件。 選取選項並指定包含檔案附件的資料夾名稱，或在文字方塊中指定檔案附件名稱。

      例如，如果CRX存放庫中的「相對於裝載」資料夾在 `attachment\attachment-folder` 位置，指定 `attachment\attachment-folder` 在文字方塊中選取 **[!UICONTROL 相對於裝載]** 選項。

   * **[!UICONTROL JSON點標籤法]**：當要使用的值位於JSON檔案中時，請使用選項。 例如，insurance.customerDetails.emailAddress。 JSON點標籤法選項僅在選取了從輸入JSON對應輸入欄位選項時可用。
   * **[!UICONTROL 從輸入JSON對應輸入欄位]**：指定JSON檔案的路徑，以從JSON檔案取得某些服務引數的輸入值。 JSON檔案的路徑可以是相對於裝載、絕對路徑，或者您可以使用JSON或表單資料模型型別的變數來選取輸入JSON檔案。

* **[!UICONTROL 服務輸入]** > **[!UICONTROL 使用變數或JSON檔案提供輸入資料]**：選取選項，以從儲存在絕對路徑、相對於承載的路徑或變數中之JSON檔案取得所有引數的值。
* **[!UICONTROL 選擇輸入JSON檔案，使用]**：包含所有服務引數值的JSON檔案。 JSON檔案的路徑可以是 **[!UICONTROL 相對於裝載]** 或 **[!UICONTROL 絕對路徑]**. 您也可以使用JSON或表單資料模型資料型別的變數來擷取輸入JSON檔案。

* **[!UICONTROL JSON點標籤法]**：將欄位留空將使用指定JSON檔案的所有物件作為服務引數的輸入。 若要從指定的JSON檔案讀取特定JSON物件作為服務引數的輸入，請為JSON物件指定點標籤法。例如，如果您有和區段開頭所列出的JSON類似的JSON，請指定insurance.customerDetails以提供客戶的所有詳細資訊作為服務的輸入。
* **[!UICONTROL 服務輸出]** > **[!UICONTROL 將輸出值對應並寫入變數或中繼資料]**：選取選項以將輸出值儲存為crx-repository中工作流程執行個體中繼資料節點的屬性。 指定中繼資料屬性的名稱，並選取對應服務輸出屬性以對應中繼資料屬性，例如，將輸出服務傳回的phone_number對應至工作流程中繼資料的phone_number屬性。 同樣地，您可以將輸出儲存在Long資料型別的變數中。 當您為選取屬性時 **[!UICONTROL 要對應的服務輸出屬性]** 選項，只會填入能夠儲存所選屬性資料的變數 **[!UICONTROL 將輸出儲存至]** 選項。

* **[!UICONTROL 服務輸出]** > **[!UICONTROL 將輸出儲存至變數或JSON檔案]**：選取選項以將輸出值儲存在JSON檔案中的絕對路徑、相對於承載的路徑或變數中。
* **[!UICONTROL 使用以下選項儲存輸出JSON檔案]**：儲存輸出JSON檔案。 輸出JSON檔案的路徑可以是相對於承載或絕對路徑。 您也可以使用JSON或表單資料模型資料型別的變數儲存輸出JSON檔案。

## 簽署檔案步驟 {#sign-document-step}

「簽署檔案」步驟可讓您使用 [!DNL Adobe Sign] 以簽署檔案。 在使用 [!DNL Adobe Sign] Workflow 步骤对自适应表单进行签名时，可以将表单逐个传送给签名者，也可以将表单同时发送给所有签名者，具体取决于工作流步骤的配置。仅在所有签名者完成签名过程后，[!DNL Adobe Sign] 支持的自适应表单才提交到 Experience Manager Forms Server。

默认情况下，[!DNL Adobe Sign] 调度程序服务每 24 小时检查（轮询）一次签名者响应。您可以 [變更環境的預設間隔](adobe-sign-integration-adaptive-forms.md##configure-adobe-sign-scheduler-to-sync-the-signing-status).

「簽署檔案」步驟具有以下屬性：

* **[!UICONTROL 合約名稱]**：指定合約的標題。 合約名稱會成為傳送給簽署者之電子郵件的主旨與內文的一部分。 您可以將名稱儲存在String資料型別的變數中，或選取 **[!UICONTROL 常值]** 以手動新增名稱。

* **[!UICONTROL 地區設定]**：指定電子郵件和驗證選項的語言。 您可以將地區設定儲存在String資料型別的變數中，或選取 **[!UICONTROL 常值]** 從可用選項清單中選擇地區設定。 將地區設定的值儲存在變數中時，您必須定義地區設定代碼。 例如，指定 **[!UICONTROL en_US]** 英文版和 **[!UICONTROL fr_FR]** 法文版。

* **[!UICONTROL Adobe Sign雲端設定]**：選擇一個 [!DNL Adobe Sign] 雲端設定。 如果您尚未設定 [!DNL Adobe Sign] 的 [!DNL AEM Forms]，請參閱 [將Adobe Sign與整合 [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md).

* **[!UICONTROL 選擇檔案以簽署]**：您可以從相對於承載的位置選擇檔案、使用承載作為檔案、指定檔案的絕對路徑，或擷取儲存在「檔案」資料型別變數中的檔案。
* **[!UICONTROL 距離截止日期天數]**：當任務中沒有活動達到中指定的天數後，檔案會標籤為到期（超過期限）。 **[!UICONTROL 距離截止日期天數]** 欄位。 將檔案指派給使用者簽署後，會計入天數。
* **[!UICONTROL 提醒電子郵件頻率]**：您可以按每日或每週間隔傳送提醒電子郵件。 從將紀錄指派給使用者以供簽署的當天開始計算該周。
* **[!UICONTROL 簽章程式]**：您可以選擇以循序或並行順序簽署檔案。 依序由一位簽署者一次收到檔案以供簽署。 第一個簽署者完成檔案的簽署後，檔案會傳送給第二個簽署者，依此類推。 多個簽署者可同時以並行順序簽署一份檔案。
* **[!UICONTROL 重新導向URL]**：指定重新導向URL。 檔案簽署後，您可以將受指派人重新導向至URL。 此URL通常包含感謝訊息或進一步說明。
* **[!UICONTROL 工作流程階段]**：工作流程可以有多個階段。 這些階段會顯示在AEM收件匣中。 您可以在模型的屬性中定義這些階段( **[!UICONTROL Sidekick]** > **[!UICONTROL 頁面]** > **[!UICONTROL 頁面屬性]** > **[!UICONTROL 階段]**)。
* **[!UICONTROL 選取簽署者]**：指定選擇檔案簽署者的方法。 您可以動態地將工作流程指派給使用者或群組，或手動新增簽署者的詳細資訊。
* **[!UICONTROL 用於選取簽署者的指令碼或服務]**：只有在「選取簽署者」欄位中選取了「動態」選項時，才可使用選項。 您可以指定ECMAScript或服務，以選擇檔案的簽署者和驗證選項。
* **[!UICONTROL 簽署者詳細資訊]**：只有在「選取簽署者」欄位中選取了「手動」選項時，才能使用此選項。 指定電子郵件地址並選擇選用的驗證機制。 在選取兩步驟驗證機制之前，請確定已為設定的啟用對應的驗證選項 [!DNL Adobe Sign] 帳戶。 您可以使用字串資料型別的變數，來定義電子郵件、國家/地區代碼和電話號碼欄位的值。 只有當您從兩步驟驗證下拉式清單中選取「電話驗證」時，才會顯示「國家/地區代碼」和「電話號碼」欄位。

<!--
## Document Services steps {#document-services-steps}

AEM Document services are a set of services for creating, assembling, and securing PDF Documents. [!DNL AEM Forms] provides a separate AEM Workflow step for each document service.

Similar to other [!DNL AEM Forms] workflow steps, such as Assign Task, Send Email, and Sign Document, you can use variables in all AEM Document services steps. For more information on creating and managing variables, see [Variables in AEM workflows](variable-in-aem-workflows.md).
 
### Apply Document Time Stamp step {#apply-document-time-stamp-step}

Add time stamp to a document. You provide document details such as input document path, input document name, location to store exported data. You may choose to overwrite existing payload file, choose a different file name to store data in a different file under payload folder, provide an absolute path to the data, or store data in a variable of Document data type.

### Convert to image step {#convert-to-image-step}

Converts a PDF document to list of images. Supported image formats are JPEG, JPEG2000, PNG, and TIFF. The following information applies to conversions to TIFF images:

* A multi-page TIFF file is generated.
* Some annotations are not included in TIFF images. Annotations that require Acrobat to generate their appearance are not included.

### Convert to PDF/A step {#convert-to-pdf-a-step}

Converts a PDF document to PDF/A format using the options provided. The PDF/A version of Portable Document Format (PDF) is specialized for archiving and long-term preservation of documents.

### Convert to PS step {#convert-to-ps-step}

Convert PDF documents to PostScript. When converting to PostScript, you can use the conversion operation to specify the source document and whether to convert to PostScript level 2 or 3. The PDF document you convert to a PostScript file must be non-interactive.

### Create PDF from specified type step {#create-pdf-from-specified-type-step}

Generate a PDF document from an input file. The input document can be relative to the payload, have an absolute path, can be payload itself, or stored in a variable of Document data type.

### Create PDF from URL/HTML/ZIP step {#create-pdf-from-url-html-zip-step}

Generates a PDF document from supplied URL, HTML, and ZIP file.

### Export Data step {#export-data-step}

Exports data from a PDF forms or XDP file. It requires you to enter the file path of Input Document and the Export Data Format. The options for Export Data Format are Auto, XDP and XmlData.

### Export PDF to specified type step {#export-pdf-to-specified-type-step}

Converts a PDF document to a selected format.

### Generate Non-Interactive PDF step {#generatenoninteractive}

Generate a Non-Interactive PDF. It provides various customization options.

>[!NOTE]
>
>You can use variables to specify the template file for input documents. Store the path of the template file in a variable of String data type.

### Import Data step {#import-data-step}

Merges form data into a PDF form. You can import form data into a PDF form.

### Invoke DDX step {#invokeddx}

Executes the DDX file on the specified map of input documents and returns the manipulated PDF documents.

>[!NOTE]
>
>You can use variables to specify the DDX file for input documents. Store the DDX file in a variable of Document or XML data type.

### Optimize PDF step {#optimize-pdf-step}

Optimizes PDF files by reducing their size. The result of this conversion is PDF files that may be smaller than their original versions. This operation also converts PDF documents to the PDF version specified in the optimization parameters.

Optimization settings specify how files are optimized. Here are example settings:

* Target PDF version
* Discarding objects such as JavaScript actions and embedded page thumbnails
* Discarding user data such as comments and file attachments
* Discarding invalid or unused settings
* Compressing uncompressed data or using more efficient compression algorithms
* Removing embedded fonts
* Setting transparency values

### Render PDF Form step {#renderpdf}

Renders a form created in Form Designer (XDP) to a PDF form.

>[!NOTE]
>
>You can use variables to specify the template file for input documents. Store the path of the template file in a variable of String data type.

### Secure Document step {#secure-document-step}

Encrypt, Sign, and certify a document. [!DNL AEM Forms] supports both password based and certificate base encryption. You can also choose between various algorithms for signing documents. For example, SHA-256 and SH-512. You can also use the workflow step to reader extend PDF documents. The workflow step provides option to enable barcode decoding, digital signatures, import and export of PDF data, and other options.

### Send to Printer step {#send-to-printer-step}

Send a document directly to a printer. It supports the following printing access mechanisms:

* **[!UICONTROL Direct accessible printer]**: A printer that is installed on the same computer is called a direct accessible printer, and the computer is named printer host. This type of printer can be a local printer that is connected to the computer directly.
* **[!UICONTROL Indirect accessible printer]**: The printer that is installed on a print server is accessed from other computers. Technologies such as the common UNIX&reg; printing system (CUPS) and the Line Printer Daemon (LPD) protocol are available to connect to a network printer. To access an indirect accessible printer, specify the print server's IP or host name. Using this mechanism, you can send a document to an LPD URI when the network has an LPD running. The mechanism lets you route the document to any printer that is connected to the network that has an LPD running.
    -->

## 產生列印輸出步驟 {#generatePrintedOutput}

此步驟會產生PCL、PostScript、ZPL、IPL、TPCL或DPL輸出，並提供表單設計和資料檔案。 資料檔會與表單設計合併，並格式化以供列印。 此步驟產生的輸出可以直接傳送到印表機或另存為檔案。 當您想要使用表單設計或來自應用程式的資料時，建議您使用此步驟。 如果您的表單設計位於網路、本機檔案系統或HTTP位置，請使用generatePrintedOutput操作。

例如，您的應用程式要求您將表單設計與資料檔案合併。 資料包含數百筆記錄。 此外，還需要將輸出傳送至支援ZPL的印表機。 表單設計和您的輸入資料都在應用程式中。 使用generatePrintedOutput作業將每筆記錄與表單設計合併，並將輸出傳送至支援ZPL的印表機。

「產生列印輸出」步驟具有下列屬性：

**[!UICONTROL 輸入屬性]**

* **[!UICONTROL 選擇範本檔案，使用]**：指定範本檔案的路徑。 您可以使用相對於承載的路徑、以絕對路徑儲存的路徑，或使用Document資料型別的變數來選取範本檔案。 例如， [Payload_Directory]/Workflow/data.xml. 如果crx-repository中不存在該路徑，則管理員可以在使用該路徑之前建立該路徑。 此外，您也可以接受裝載作為輸入資料檔案。

* **[!UICONTROL 選擇資料檔案，使用]**：指定輸入資料檔案的路徑。 您可以使用相對於承載的路徑、以絕對路徑儲存的路徑，或使用Document資料型別的變數來選取輸入資料檔案。 例如， [Payload_Directory]/Workflow/data.xml. 如果crx-repository中不存在該路徑，則管理員可以在使用該路徑之前建立該路徑。

* **[!UICONTROL 印表機格式]**：指定未提供XDC檔案時用來產生輸出資料流的頁面描述語言的列印格式值。 如果您提供常值，請選取下列其中一個值：

   * **[!UICONTROL 色彩PCL]**：使用選項為PCL指定XDC檔案。
   * **[!UICONTROL 通用PostScript]**：使用選項為PostScript指定通用XDC檔案。
   * **[!UICONTROL ZPL 300 DPI]**：使用ZPL 300 DPI。 使用zpl300.xdc。
   * **[!UICONTROL ZPL 600 DPI]**：使用ZPL 600 DPI。 會使用zpl600.xdc檔案。
   * **[!UICONTROL IPL 300 DPI]**：使用IPL 300 DPI。 使用ipl300.xdc。
   * **[!UICONTROL IPL 400 DPI]**：使用IPL 400 DPI。 使用ipl400.xdc檔案。
   * **[!UICONTROL TPCL 600 DPI]**：使用TPCL 600 DPI。 使用tpcl600.xdc檔案。
   * **[!UICONTROL PostScript Plain]**：使用選項為PostScript指定純文字XDC檔案。
   * **[!UICONTROL DPL300DPI]**：使用DPL 300 DPI。 使用dpl300.xdc。
   * **[!UICONTROL DPL400DPI]**：使用DPL 400 DPI。 使用dpl400.xdc。
   * **[!UICONTROL DPL600DPI]**：使用DPL 600 DPI。 使用dpl600.xdc。
   * **[!UICONTROL HP_PCL_5e]**：使用選項支援多個Canon裝置。


**[!UICONTROL 输出属性]**

* **[!UICONTROL 儲存輸出檔案，使用]**：指定儲存輸出檔案的位置。 您可以將輸出檔案儲存在相對於承載的位置、變數中，或指定絕對位置來儲存輸出檔案。 如果crx-repository中不存在該路徑，則管理員可以在使用該路徑之前建立該路徑。

**[!UICONTROL 進階屬性]**

* **[!UICONTROL 選擇內容根目錄位置，使用]**：內容根是字串值，可指定存放庫中的URI、絕對參照或位置，以擷取表單設計使用的相對資產。 例如，如果表單設計相對參照影像，例如 `../myImage.gif`， `myImage.gif` 必須位於 `repository://`. 預設值為 `repository://`，指向存放庫的根層級。

   當您從應用程式中挑選資產時，內容根URI路徑必須具有正確的結構。 例如，如果從名為SampleApp的應用程式中挑選表單，並將表單放在 `SampleApp/1.0/forms/Test.xdp`，內容根URI必須指定為 `repository://administrator@password/Applications/SampleApp/1.0/forms/`，或 `repository:/Applications/SampleApp/1.0/forms/` （當授權為空）。 以這種方式指定內容根URI時，表單中所有參考資產的路徑都將針對此URI進行解析。

* **[!UICONTROL 選擇XCI檔案，使用]**：XCI檔案用於說明用於表單設計元素的字型和其他屬性。 您可以相對於承載將XCI檔案保留在絕對路徑上，或使用Document資料型別的變數。

* **[!UICONTROL 地區設定]**：指定用來產生PDF檔案的語言。 如果您提供常值，請從清單中選取語言或選取下列其中一個值：
   * **[!UICONTROL 使用伺服器預設值]**：（預設）使用設定的地區設定 [!DNL AEM Forms] 伺服器。 地區設定是使用Administration Console進行設定。 (請參閱 [Designer說明](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/using-designer.pdf).)

   * **[!UICONTROL 使用自訂值]**：在常值方塊中輸入地區設定代碼，或選取包含地區設定代碼的字串變數。 如需支援地區設定代碼的完整清單，請參閱https://docs.oracle.com/javase/1.5.0/docs/guide/intl/locale.doc.html。

* **[!UICONTROL 份數]**：整數值，指定要為輸出產生的副本數。 默认值为 1。

* **[!UICONTROL 雙面列印]**：指定使用雙面或單面列印的「分頁」值。 支援PostScript和PCL的印表機使用此值。 如果您提供常值，請選取下列其中一個值：
   * **[!UICONTROL 雙面長邊]**：使用雙面列印，並使用長邊分頁進行列印。
   * **[!UICONTROL 雙面短邊]**：使用雙面列印，並使用短邊分頁進行列印。
   * **[!UICONTROL 單面]**：使用單面列印。

## 產生非互動式PDF輸出步驟   {#generatePDFdocuments}

1. 將「產生非互動式PDF輸出」工作流程拖曳至Sidekick中「Forms Workflow」標籤下方。
1. 連按兩下新增的工作流程步驟以編輯元件。
1. 在「編輯元件」對話方塊中，設定輸入檔案、輸出檔案和其他引數，然後按一下 **[!UICONTROL 確定]**.

### 輸入檔案 {#input-documents-3}

* **範本檔案**：指定XDP範本的位置。 它是必填欄位。

* **資料檔案**：指定需要與範本合併的資料xml的位置。

### 輸出檔案 {#output-document}

**輸出檔案**：指定所產生PDF表單的名稱。

### 其他引數 {#additional-parameters-1}

* **內容根目錄**：指定存放庫中儲存輸入XDP範本中使用的片段或影像的資料夾路徑。
* **地區設定**：指定所產生PDF表單的預設地區設定。
* **Acrobat版本**：指定所產生PDF表單的目標Acrobat版本。
* **線性PDF**：指定是否將產生的PDF最佳化以供網頁檢視。
* **標籤PDF**：指定是否允許存取產生的PDF。
* **XCI檔案**：指定XCI檔案的路徑。
