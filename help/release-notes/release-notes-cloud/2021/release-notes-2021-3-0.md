---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.3.0 版的发行说明。'
description: '"[!DNL Adobe Experience Manager] 2021.3.0版as a Cloud Service發行說明」。'
exl-id: 0c07364c-ba25-4081-8e35-3c1c84ed556f
source-git-commit: acd80887d71a528604d37fa2787bca3c3a48d7c4
workflow-type: tm+mt
source-wordcount: '1297'
ht-degree: 40%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明 {#release-notes}

以下部分概述了当前（最新）版本的 [!DNL Experience Manager] as a Cloud Service 的一般发行说明。

>[!NOTE]
>您可以在此處瀏覽至舊版的發行說明；例如，2020、2021等版本。

>[!NOTE]
>
>有关未与版本直接相关的文档更新的详细信息，请参阅[最新文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)。

## 发布日期 {#release-date}

的發行日期 [!DNL Adobe Experience Manager] as a Cloud Service2021.3.0是2021年3月25日。
下列版本(2021.4.0)將於2021年4月29日發行。

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

* [網站的漸進式網頁應用程式(PWA)版本](/help/sites-cloud/authoring/features/enable-pwa.md) 現在可透過簡易設定在專案層級啟用。
* 內容片段模式延伸模組 — 現在可以將多行文字資料型別定義為多欄位清單。
* 內容片段編輯器UX增強功能 — 巢狀子片段現在顯示在階層連結中，並改善發佈、儲存和儲存並結束動作的檢視

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 的新增功能 {#what-is-new-assets}

<!-- TBD: refine this list of features and enh. for Feb release.

Customers using the Connected Assets feature can now easily view and track assets used on remote Sites instances. This affords customers a complete view of being used across all Sites powered pages, allowing for better tracking, management, and brand consistency.  

Indicators for expired, approved, and rejected statuses now available for assets in Column view.

Ability to select a root path. select if a minimum number of tags is required. 

Add a Boolean or radio widget type to metadata schema setup. -->

* [!DNL Experience Manager] 擴充「連線資產」功能，支援使用 [!DNL Dynamic Media] 影像於支援的核心元件中。 另請參閱 [使用連線資產](/help/assets/use-assets-across-connected-assets-instances.md).
* Experience Manager管理員可以在特定日期或時間排程大量資產擷取。 此外，管理員可以根據日期和時間排程週期性內嵌。 另請參閱 [大量資產擷取](/help/assets/add-assets.md#asset-bulk-ingestor).

### [!DNL Assets] 中的错误修复 {#bug-fixes-assets}

* 嘗試下載多個許可權管理的資產時，未顯示版權頁面。 (CQ-4314403)
* 選擇編輯INDD檔案時，解析度會意外變更。 (CQ-4317376)
* PDF轉譯中只有InDesign範本的最後一頁。 (CQ-4317305)
* 當選取器是複雜中繼資料結構的一部分時，標籤選取器需要很長時間才能開啟。 (CQ-4316426)
* 上傳檔案名稱與現有資產相同的資產時，名稱衝突對話方塊不顯示以提示使用者建立版本。 (CQ-4315424)
* 您可以從資料夾的「屬性」頁面中的彈出式選單設定及儲存「資料夾中繼資料屬性」。 當選取專案儲存在存放庫時，再次開啟資料夾中繼資料屬性時不會顯示。 (CQ-4314429)
* 檔案名稱包含空格或特殊字元的資產會使用瀏覽器上傳。 (CQ-4318381)

## [!DNL Adobe Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

AEM Forms在多年來已幫助許多組織提供絕佳的上線和註冊體驗。 這些體驗已幫助組織將銷售線索轉換為銷售、處理擷取的客戶資料、根據對象設定檔提供回應式體驗等。 現在，AEM Forms以Cloud Service的形式提供。

您可以使用 [AEM Formsas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/home.html) 若要建立數位表格，請將表格連結至現有的資料來源、將表格與Adobe Sign整合以將電子簽章新增至表格、產生記錄檔案(DoR)以將提交的表格封存為PDF檔案。 此服務也可以將您現有的PDF forms轉換為數位表格。 除了標準AEM Forms功能外，此服務還提供數種雲端原生功能，例如自動縮放、升級時的零停機時間，以及雲端原生開發環境。

您可以聯絡您的Adobe代表來要求示範或註冊此服務。

## Adobe Experience Manager Commerceas a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 支援Adobe Commerce 2.4.2

* 現在可以在任何內容頁面上使用和設定產品詳細資料元件

* 已發行CIF Venia Reference Site - 2021.03.25，其中包含最新CIF Core Components v1.9.0版。請參閱 [CIF Venia參考網站](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.03.25) 以取得更多詳細資料。

* 已發行CIF Core Components v1.9.0。請參閱 [CIF Core Components](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.9.0) 以取得更多詳細資料。


## Cloud Manager {#cloud-manager}

此部分概述了 AEM as a Cloud Service 2021.3.0 中的 Cloud Manager 的发行说明。

## 发布日期 {#release-date-cm-march}

AEM as a Cloud Service 2021.3.0 中的 Cloud Manager 的发布日期是 2021 年 3 月 11 日。下一个版本计划于 2021 年 4 月 08 日发布。

### 新增功能 {#what-is-new-march}

* 其环境中具有预先存在的 [IP 允许列表](/help/implementing/cloud-manager/ip-allow-lists/managing-ip-allow-lists.md#pre-existing-cdn)、[SSL 证书](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md#pre-existing-cdn)和[自定义域名](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn)的自定义域名配置的客户现在可看到关于其以前存在的配置的消息，并能够通过 UI 进行自助服务。

* 具有所需权限的用户现在可编辑计划，于是这些用户可按自助方式执行以下操作：

   * 将 Sites 解决方案添加到具有 Assets 的现有程序，反之亦然。
   * 从具有 Sites 和 Assets 的现有计划中删除 Sites 或 Assets。
   * 将另一未使用的解决方案权利添加到现有计划或添加为新计划。

* **AEM推播更新** 標籤現在會同時顯示兩者 *管道執行* 和 *活動* 畫面。

* 如果环境已休眠，但还有 AEM 更新可用，则&#x200B;**已休眠**&#x200B;状态优先于&#x200B;**有可用更新**&#x200B;状态。

* 用户们现在通过在导航到 Unified Shell 的“用户个人资料”图标（右上角）之后选择“查看 Cloud Manager 角色”选项，即可查看其 Cloud Manager 角色。

* 为了更加清晰明了，**申请批准**&#x200B;标签已变为&#x200B;**批准生产**。

* “生产管道执行”屏幕中的&#x200B;**版本**&#x200B;标签已变为 **Git 标签**。

* 已改变定义在重要指标不符合所定义的阈值时发生的行为的若干标签以反映其真实行为：**立即取消**&#x200B;和&#x200B;**立即批准**。

* 已根据 AEM Cloud Service SDK 的 `2021.3.4997.20210303T022849Z-210225` 版本更新了类和方法的弃用列表。

* Cloud Manager Production 管道现在将包括[自定义 UI 测试](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing)功能。

### 错误修复 {#bug-fixes-cm-march}

* 在 AEM 推送升级过程中，某些情况下跳过了包版本控制。

* 当包嵌入到其他包中时，没有正确发现一些质量问题。

* 在不明显的情况下，打开“添加程序”对话框时生成的默认程序名可能与现有程序名重复。

* 有时，如果用户在启动管道后立即离开管道执行页面，则会显示一条错误消息，说明操作失败，尽管执行实际上已开始。

* 当客户生成导致无效包时，不必要地重新启动了生成步骤。

* 有时，即使未部署配置，用户也会在 IP 允许列表旁边看到绿色的“活动”状态。

* 所有现有生产管道都将通过体验审核步骤自动启用。

## 内容转移工具 {#content-transfer-tool}

### 发布日期 {#release-date-ctt}

內容轉移工具v1.3.4的發行日期為2021年3月19日。

### 错误修复 {#bug-fixes-ctt}

* CTT已略過名稱相同但名稱中有連字型大小的資料夾內容。 此问题已得到修复。

### 发布日期 {#release-date-ctt-march}

內容轉移工具v1.3.0的發行日期為2021年3月4日。

### 內容轉移工具的新增功能 {#what-is-new-ctt-march}

* CTT現在安裝至 `/apps` 而非 `/libs` 特定頁面的瀏覽器書籤可能不再有效。
* 安裝CTT時，使用者必須瀏覽其他層級，才能進入「內容轉移」頁面。 另請參閱 [使用內容轉移工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html) 以取得更多詳細資料。

### 错误修复 {#bug-fixes-ctt-march}

* 從特定路徑移轉內容時，CTT會提取不相關的資源。 此问题已得到修复

## Best Practices Analyzer {#best-practices-analyzer}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer v2.1.8 的发布日期是 2021 年 3 月 22 日。

### Best Practices Analyzer新增功能 {#what-is-new-bpa}

* 能夠從UI中的BPA報告以及匯出為CSV檔案的報告篩選掉ACS Commons發現。

## 代码重构工具 {#code-refactoring-tools}

### 程式碼重構工具的新增功能 {#what-is-new-crt}

* Repository Modernizer的新功能和增強功能。 請參閱 [GitHub資源： Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) 以取得最新版本。
   * 將OSGi設定（RepoInit設定除外）標準化為慣用的.cfg.json格式。
   * 將OSGi設定資料夾重新命名為指定的格式。
   * 產生ui.apps.structure專案。
   * 建立分析模組。

* Dispatcher轉換工具的新功能和增強功能。 請參閱 [GitHub資源： Dispatcher轉換工具](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)
   * 為不同的包含專案建立個別檔案，而非將內容排成一行。
   * 能夠處理vhosts的資料夾路徑和vhost檔案的路徑。
   * 產生具有範圍在600個或更多大型客戶設定的伺服器陣列檔案。
