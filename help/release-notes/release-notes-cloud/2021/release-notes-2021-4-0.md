---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.4.0 版的发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.4.0 版的发行说明。'
exl-id: 775332b5-24ce-430e-97a2-6eeb80877c64
source-git-commit: a2c844d6f72c22ed085690ff98572a52e97de40d
workflow-type: tm+mt
source-wordcount: '1535'
ht-degree: 47%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明 {#release-notes}

以下部分概述了当前（最新）版本的 [!DNL Adobe Experience Manager] as a Cloud Service 的一般发行说明。

>[!NOTE]
>您可以在此處瀏覽至舊版的發行說明；例如，2020、2021等版本。

>[!NOTE]
>
>有关未与版本直接相关的文档更新的详细信息，请参阅[最新文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)。

## 发布日期 {#release-date}

的發行日期 [!DNL Adobe Experience Manager] as a Cloud Service2021.4.0是2021年5月6日。
下列版本(2021.5.0)將於2021年5月27日發行。

## AEMas a Cloud Service基礎{#aem-as-a-cloud-service-foundation}

### 新增功能 {#what-is-new-foundation}

* [發佈內容樹狀工作流程](/help/operations/replication.md#publish-content-tree-workflow)  — 新的工作流程模型和步驟可在發佈深層內容時提高效能。

## [!DNL Adobe Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites] 的新增功能 {#what-is-new-sites}

* GraphQL端點 — 現在可以為個別AEM Sites設定啟用AEM GraphQL API，並使用新的GraphQL Console UI為這些設定建立自訂GraphQL端點。 UI也可讓您管理GraphQL端點。

* 內容模型、增強型日期和時間資料型別 — 現在可以設定日期和時間資料型別，以允許撰寫僅限日期、僅限時間或是日期和時間的資訊。

* 內容模型、增強型標籤資料型別 — 現在可以設定標籤資料型別，以允許撰寫單一或多個標籤。

* 內容模型、新索引標籤預留位置資料型別 — 新索引標籤預留位置資料型別允許將資料型別分組到多個區段中，這些區段將會在內容片段編輯器中的索引標籤底下呈現。

### [!DNL Sites] 中的错误修复 {#bug-fixes-sites}

* 內容片段 — 移動內容片段或資料夾現在會更新片段內的巢狀參考(CQ-4320815)

* GraphQL — 持續查詢現在支援特定於AEM Sites設定的使用者定義端點(CQ-4315928)

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 的新增功能 {#what-is-new-assets}

* [!DNL Experience Manager] 不會封存下載原始檔案的單一資產下載。 此增強功能可加快下載速度。

* 透過linkshare選項下載資產時，您現在可以選擇下載或不下載轉譯。 之前則會下載所有資產轉譯。

* 管理員可以設定 [!DNL Experience Manager] 若要在執行大量資產擷取後刪除資產來源，請執行下列動作。 另請參閱 [大量資產擷取](/help/assets/add-assets.md#asset-bulk-ingestor).

* 在執行狀況檢查以大量匯入資產時，Experience Manager現在會提供失敗原因的更多資訊。 另請參閱 [大量資產擷取](/help/assets/add-assets.md#asset-bulk-ingestor).

* 使用大量匯入工具匯入資產時，管理員現在可以選擇在匯入成功後刪除來源檔案。 另請參閱 [大量資產擷取](/help/assets/add-assets.md#asset-bulk-ingestor).

* 編輯中繼資料結構描述時，新的根路徑選擇器欄位可讓管理員快速輕鬆地做出選擇，進而縮短設定時間。

* 編輯中繼資料結構描述時，會新增一個資料型別，在中繼資料編輯器中提供自由格式的文字區域。 使用者可以使用此文字區域輸入自由格式文字作為資產的中繼資料。 另請參閱 [中繼資料結構編輯器](/help/assets/metadata-schemas.md).

* 許多資產的中繼資料可以使用CSV檔案大量匯入，也可以匯出到CSV檔案。 預設日期格式現在為 `yyyy-MM-dd'T'HH:mm:ss.SSSXXX`. 使用者可以更新欄標題來運用不同的格式。 例如，新增 `Date: DateFormat: yyyy-MM-dd'T'HH:mm:ssXXX` 做為CSV檔案中的欄標題，而不是單字 `Date`.

* 在「欄」檢視中瀏覽資產時，視覺指示器會顯示每個資產的已核准或已拒絕狀態。

* 在「欄」檢視中瀏覽資產時，視覺指示器會顯示已到期的資產。

### [!DNL Assets] 中的错误修复 {#bug-fixes-assets}

* 嘗試移動多個資產或資料夾時，控制檯中會記錄錯誤，且移動作業未完成。 如果無法更新標題，移動作業會失敗。 (CQ-4322080)

* 中繼資料欄位可以根據規則隱藏，以便在滿足預先定義的條件時，中繼資料不是強制性的。 不過，此類隱藏的中繼資料欄位會顯示為必填欄位。 (CQ-4321285)

* 大量中繼資料匯入失敗，因為日期格式不正確。 (CQ-4319014)

* 在「屬性」頁面中選取要更新中繼資料時，如果結構描述提供了許多選項，介面的回應會很緩慢。 (CQ-4318538)

* 在單行文字欄位中更新和儲存中繼資料值時，即使下拉式選單上的編輯功能已停用，下拉式選單中的值也會被刪除。 (CQ-4317077)

* 您可以使用省略符號作為註解來檢閱資產。 使用小橢圓時，橢圓與列印版本中的註釋編號重疊。 (CQ-4316792)

* 在搜尋資產後，若從搜尋結果中選取資產，快速發佈選項不會顯示。 (CQ-4317748)

## [!DNL Adobe Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 的新增功能 {#what-is-new-forms}

* **在支持 Adobe Sign 的自适应表单中使用 Government ID 身份验证方法**

   通过先进的机器学习算法，Adobe Sign 的 Government ID 流程让世界各地的公司均可确保高质量地验证其收件人的身份。现在，您可以在支持 Adobe Sign 的自适应表单中使用 Government ID 身份验证方法。

   Government ID 是一种高级的身份验证方法，它指示收件人[上传政府颁发的身份证明文件（驾照、身份证、护照）的图像](https://helpx.adobe.com/in/sign/using/adobesign-authentication-government-id.html)，然后评估该证明文件以确保真实有效。

* **支持对异步提交自适应表单使用表单内签名体验**

   现在，您可以使用表单内签名体验来异步提交自适应表单。还可将自适应表单嵌入到 [!DNL Experience Manager Sites] 页面中，并使用表单内签名体验提交自适应表单。

* **支持在为“分配任务”步骤预先填充自适应表单时使用变量指定附件**

   在为“分配任务”步骤预先填充自适应表单时，现在可使用文档类型变量为该自适应表单选择输入附件。

* **支持使用字面选项设置 JSON 类型变量的值**

   可在 AEM Workflow 的“设置变量”步骤中使用字面选项设置 JSON 类型变量的值。通过字面选项，可按字符串的形式指定 JSON。

* **使用本地开发环境创建记录文档 (DoR)**

   可在 Cloud Service 实例和 AEM Forms as a Cloud Service SDK（本地开发环境）上使用 XDP 作为文档记录模板。以前仅限 Cloud Service 实例支持这样做。

### [!DNL Forms] 中的错误修复 {#bug-fixes-forms}

* 将配置为不生成记录文档的自适应表单提交到配置为生成记录文档的 AEM Workflow 时，不会显示任何错误消息，但任务无法提交。

### 其他更新 {#misc-2021-04-0-forms}

* 為了更方便識別內容，該服務現在會為XDP、動態PDF和結構描述檔案產生即時縮圖。
* 新增將PDF檔案移動到放置在AEM Forms UI上的資料夾的功能。

## Adobe Experience Manager Commerceas a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 類別UID的支援 — 針對使用字串作為類別ID的系統，這可解除鎖定第三方商業整合

* PWA Studio的AEM擴充功能，包括 整合範例

* 可擴充WCM導覽核心元件的新CIF導覽核心元件

* AEM店面中暫存目錄資料的視覺指示器

* 現在可透過Cloud Manager UI設定商務端點

### 错误修复 {#bug-fixes-commerce}

* 根類別欄位未顯示在類別頁面的頁面屬性中的商務索引標籤下

## Cloud Manager {#cloud-manager}

此部分概述了 AEM as a Cloud Service 2021.4.0 中的 Cloud Manager 的发行说明。

### 发布日期 {#release-date-cm-april}

AEM as a Cloud Service 2021.4.0 中的 Cloud Manager 的发布日期是 2021 年 4 月 8 日。
下一个版本计划于 2021 年 06 月 06 日发布。

### 新增功能 {#what-is-new-april}

* “添加和编辑程序”工作流的 UI 进行了更新，变得更加直观。

* 具有必需权限的用户现在可以通过 UI 提交商务端点。

* 现在可以将环境变量的作用域限定为特定服务（创作或发布）。要求 AEM 版本 `2021.03.5104.20210328T185548Z` 或更高版本。

* 即使未配置任何管道，“管道”卡上也会显示&#x200B;**“管理 Git”**&#x200B;按钮。

* Cloud Manager 使用的 AEM 项目原型的版本已更新到版本 27。

* Adobe I/O 开发人员控制台中由 Cloud Manager 创建的项目不会再被无意中编辑或删除。

* 当用户添加新环境时，将会通知他们，环境在创建后无法移动到其他区域。

* 现在可以将环境变量的作用域限定为特定服务（创作或发布）。 要求 AEM 版本 2021.03.5104.20210328T185548Z 或更高版本。

* 澄清了删除环境后启动管道时的错误消息。

* Eclipse 项目提供的 OSGi 捆绑包现已从规则 `CQBP-84--dependencies` 中排除。

### 错误修复 {#bug-fixes-cm-april}

* 编辑管道的体验审核页面时，以斜杠 `( / )` 开头的输入路径将不再会使步骤停留在挂起状态。

* 创建新的生产管道时，如果用户未添加内容审核覆盖，则默认主页未审核。

* `CloudServiceIncompatibleWorkflowProcess` 的问题在可下载的问题 CSV 文件中的严重性不正确。

* `Runmode` 检查在非文件夹节点上产生误报。

## Best Practices Analyzer {#best-practices-analyzer}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer v2.1.12的發行日期為2021年4月12日。

### 错误修复 {#bug-fixes-bpa-april}

* 在報告的BPA中看到重複列。 此问题已得到修复。
* AEM 6.4.2版上的BPA UI擲回停用產生報告按鈕的JS錯誤。 此问题已得到修复
