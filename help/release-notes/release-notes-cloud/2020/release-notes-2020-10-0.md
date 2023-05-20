---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0 版的发行说明。'
description: '"[!DNL Adobe Experience Manager] 2020.10.0版as a Cloud Service發行說明」。'
exl-id: ac741744-5b47-47a4-b5af-e1089e92c3f0
source-git-commit: cc6565121a76f70b958aa9050485e0553371f3a3
workflow-type: tm+mt
source-wordcount: '1197'
ht-degree: 26%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0 版的发行说明  {#release-notes}

以下區段會概述以下專案的一般發行說明： [!DNL Experience Manager] as a Cloud Service2020.10.0。

## 发布日期 {#release-date}

的發行日期 [!DNL Adobe Experience Manager] as a Cloud Service2020.10.0為2020年10月28日。
下列版本(2020.11.0)將於2020年12月1日發行。

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### [!DNL Sites] 的新增功能 {#what-is-new-sites}

* **[核心元件2.12.0](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans)**：Adobe Experience Manager as a Cloud Service受益於最新版本核心元件的自動更新。 版本2.12.0包含社群貢獻的最新改善。 改善專案包括 [新的POST表單處理常式；](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/forms/form-container.html#post-data) 包含自訂CSS、JavaScript和中繼資料的功能 [透過內容感知設定的標籤；](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html#context-aware-loading) 和 [`DataLayerBuilder`](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/integrations.html#enabling-custom-components) 可簡化自訂元件中Adobe資料層整合的公用程式。 請參閱 [變更清單](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.12.0) 2.12.0版。

* **[專案原型24](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)**：建議的開始新Experience Manager專案基礎更臻完美。 現在包含新的 [Adobe使用者端資料層](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html)，的選項 [以AMP傳送網站，](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/amp.html) 和新 [擴充功能點以新增專案CSS/JS。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html#context-aware-loading)

* **[ContextHub資料夾](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md#organizing-segments)**：可建立受眾資料夾，以輕鬆組織、尋找和選取要用於ContextHub選件鎖定目標功能的受眾區段。

## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

* **[!DNL Adobe Sensei]支援的視訊智慧標籤**：透過套用AI模型來分析物件和動作特定標籤的視訊內容，DAM使用者可以花更少的時間新增標籤，而有更多時間使用公開的、豐富的資訊。 反過來，您也能為客戶提供合適的體驗。 另請參閱 [智慧標籤視訊資產](/help/assets/smart-tags-video-assets.md).

* **Brand Portal增強功能**：下列新功能和更多內容在以下網站中提供： [!DNL Brand Portal]. 如需詳細資訊，請參閱 [[!DNL Brand Portal] 發行說明](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal-release-notes.html).

   * [增強下載體驗](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html) 以簡化及加快下載速度。 管理员可以配置更多下载配置，以根据用户和企业的需求提供下载体验。
   * 按一下即可導覽至「檔案」， [集合](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/share/brand-portal-share-collection.html)，現在可以從任何頁面使用共用連結。
   * 使用者可以 [選取並下載特定轉譯](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html#download-assets-from-asset-details-page) 立即。 可在“资源详细信息”页面中的“演绎版”面板中找到下载演绎版的新选项。
   * 訪客使用者工作階段逾時15分鐘可確保所有並行使用者獲得更好的體驗。

* **[!DNL Adobe Asset Link]版本2.1**：新版本的 [Adobe資產連結](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) 擴充功能 [!DNL Adobe Photoshop]， [!DNL Adobe Illustrator]、和 [!DNL Adobe InDesign] 可用。 新增與最新版本的相容性 [!DNL Adobe Creative Cloud] 2020年10月發行的2021版應用程式。

* **[!DNL Assets]WebP檔案支援**： [!DNL Assets] as a Cloud Service現在支援WebP影像格式。 WebP是Google建立的新興影像格式。 WebP檔案格式的影像在視覺上與JPG或PNG檔案沒有區別，而且檔案更小。 降低資產的檔案大小可改善頁面載入時間，並幫助內容建立者提供更快速的網頁體驗。 瞭解如何在中使用WebP [建立處理設定檔](/help/assets/asset-microservices-configure-and-use.md#create-standard-profile).

## [!DNL Adobe Experience Manager Forms] as a Cloud Service {#forms-oct-2021}

### [!DNL Forms] 的新增功能 {#what-is-new-forms-oct-2021}

* **Analytics for Adaptive Forms**：您現在可以透過Adobe Analytics for Adaptive Forms擷取及追蹤已登入和未登入（匿名）的行為，以收集一般使用者的深入解析。 它可協助商務使用者根據收集的深入分析，針對最適化表單內容、版面配置和樣式做出明智的決策。

### [!DNL Forms]预发行渠道中提供的新功能 {#prerelease-features-forms-oct-2021}

* **外部化AEM Workflow資料以進行安全處理**：您可以將包含敏感個人資料(SPD)元素的程式內AEM Workflow變數資料儲存在客戶管理的存放庫中，以便安全處理。 處理工作流程時，儲存在工作流程變數中的資料不會儲存在AEM存放庫中。 系統會隨選從客戶管理的存放庫擷取。

### [!DNL Forms] 的 Beta 版功能 {#sep-what-is-new-forms-oct-prerelease}

* **[!DNL AEM Forms as a Cloud Service - Communications]**： [通訊API](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications.html) 協助您合併範本和XML資料，以產生多種格式的檔案。 此服務可讓您以同步和批次模式產生檔案。

您可以将电子邮件发送到 [!DNL formscsbeta@adobe.com] 以注册 Beta 项目。

## Adobe Experience Manager Commerceas a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 已發行CIF Venia Reference Site - 2020.10.2，其中包含最新CIF Core Components v1.4.0版。請參閱 [CIF Venia參考網站](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.2) 以取得更多詳細資料。

* 已發行CIF Core Components v1.4.0。請參閱 [CIF Core Components](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.4.0) 以取得更多詳細資料。

### 错误修复 {#bug-fixes-commerce}

* 產品控制檯和選取器中的GraphQL請求是透過HTTPPOST完成的。 此問題已修正，以確保Apollo GraphQL使用者端遵守GraphQL使用者端OSGi設定中的設定，以支援GET要求（若已設定）。

* CIF雲端設定UI針對/lib和/apps/中的設定顯示「儲存並關閉」按鈕。 但由於這些介面是唯讀的，因此UI已修復為僅顯示「關閉」按鈕。

## Cloud Manager {#cloud-manager}

### 发布日期 {#release-date-cm}

Experience Manageras a Cloud Service2020.10.0中的Cloud Manager發行日期是2020年10月2日。

### [!DNL Cloud Manager] 的新增功能 {#what-is-new-cm}

* “环境”页面已重新设计。

* 现在，进入休眠状态的环境在 Cloud Manager 中会显示离散状态。

* Cloud Manager「組建容器」現在支援使用Java™ 8或Java™ 11編譯專案。 Maven工具鏈系統支援Java™ 11。

* 每个环境的环境变量数量已增加至 200 个。

* 總覽頁面上的環境卡現在會列出最多三個環境。 用户可以选择&#x200B;**全部显示**&#x200B;按钮导航到“环境”摘要页面，查看包含完整环境列表的表。 有关更多信息，请参阅[查看环境](/help/implementing/cloud-manager/manage-environments.md#viewing-environment)。

### 错误修复 {#bug-fixes-cloud-manager}

* 在完全环境创建之前，从 Cloud Manager 到开发人员控制台的链接错误地处于活动状态。

* 直接从 Cloud Manager 链接到开发人员控制台不显示用于将沙盒程序的环境解除休眠/休眠的选项。

* 非生产管道编辑页面上的“取消”和“保存”选项并非一直可见。

* 代码质量控制过程中出现的某些问题可能会导致日志文件无法正确生成。

* 建立方案時，建議的名稱有時會傳回重複的現有方案名稱。

* 无法始终通过用户界面下载一些大型管道步骤日志文件。

* 验证环境名称时出现差一错误。

* 環境頁面有時會在未顯示任何內容時顯示發佈和Dispatcher區段。

## Adobe Experience Manager as a Cloud Service 基础 {#cloud-service-foundation}

### 工作流 {#workflows}

* 已新增根據工作流程標題、工作流程模型、狀態、發起人、裝載路徑和開始日期來搜尋工作流程例項的支援。 另請參閱 [搜尋工作流程例項](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/administering/workflows-administering.html).

## 内容传输工具 {#content-transfer-tool}

進一步瞭解的新增功能和更新 [內容轉移工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html) 發行版本1.1.12。

### 新增功能 {#what-is-new-ctt}

* 改善記錄的使用者體驗。 擷取和內嵌記錄檔中新增的時間戳記。 已新增訊息，以指出記錄檔是否為空白。

### 错误修复 {#ctt-bug-fixes}

* 如果移轉集包含的路徑具有部分相似的檔案名稱，則內容轉移工具會略過內容檔案。
