---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2020.8.0 版的发行说明。'
description: '"[!DNL Adobe Experience Manager] 2020.8.0版as a Cloud Service發行說明」。'
exl-id: 83413130-ae90-4419-bcf7-42fdc740452b
source-git-commit: bc4da79735ffa99f8c66240bfbfd7fcd69d8bc13
workflow-type: tm+mt
source-wordcount: '1046'
ht-degree: 39%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2020.8.0 版的发行说明  {#release-notes}

以下部分概述了 Experience Manager as a Cloud Service 2020.8.0 的常规发行说明。


## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### [!DNL Sites] 的新增功能 {#what-is-new-sites}

* 能夠 [將頁面和子頁面（頁面樹狀結構）還原為舊版](/help/sites-cloud/authoring/features/page-versions.md#reinstating-versions).

* 能夠 [建立啟動](/help/sites-cloud/authoring/launches/overview.md) 在AEM中 [SPA編輯器。](/help/implementing/developing/hybrid/introduction.md)


## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

### [!DNL Assets] 的新增功能 {#what-is-new-assets}

* 資產微服務現在支援視訊轉碼。 中的新區段 [!UICONTROL 處理設定檔] 設定可讓您設定視訊位元速率和維度。 輸出格式為使用H.264轉碼器的MP4。 如需詳細資訊，請參閱 [管理視訊資產](/help/assets/manage-video-assets.md#transcode-video). 如需更多轉碼選項及視訊傳送，請使用 [!DNL Dynamic Media] 附加元件。

* 新增 [!DNL Experience Manager Assets] 部署，現在預設會設定智慧標籤功能。 無需手動整合 [!DNL Adobe Developer Console]. 在現有部署中，管理員會像之前一樣設定智慧標籤整合。

* 新 [資產下載體驗](/help/assets/download-assets-from-aem.md) 允許，

   * 非同步下載大量內容，讓使用者不需等待。
   * 適用於開發人員擴充性的新模組化API。

* 資產微服務的中繼資料擷取已改善效能。 這可增加整體資產擷取輸送量。

* 使用處理設定檔，以使用計算服務產生自訂中繼資料。 另請參閱 [使用處理設定檔的自訂中繼資料](/help/assets/manage-metadata.md#metadata-compute-service).

* 管理員可設定的Brand Portal使用者更簡單的下載體驗。 另請參閱 [下載體驗概述](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html#download-configurations).

* Brand Portal現在提供原始和高保真PDF檔案預覽。 另請參閱 [檔案檢視器概觀](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html#doc-viewer).

* 您現在可以直接從「 」使CDN （內容傳遞網路）快取失效 [!DNL Dynamic Media] 在AEMas a Cloud Service中(與使用 [!DNL Dynamic Media Classic])。 這可確保在幾分鐘內提供最新資產，而非數小時。 另請參閱 [透過Dynamic Media使CDN快取失效](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md).

* 使用者介面控制項、導覽、瀏覽和搜尋體驗新增了增強的協助工具支援 [!DNL Assets].

   * 如果您在選取後按Escape鍵 [!UICONTROL 新增轉譯] 選項時，焦點會回到工具列。 <!-- via CQ-4293594-->
   * 使用「電子郵件」下拉式方塊時，鍵盤焦點可如預期運作。 <!-- via CQ-4286215 -->
   * 搜尋篩選區段中的摺疊式功能表元素會解譯為標準可展開的摺疊式功能表。 <!-- via CQ-4273103 -->
   * 將標籤套用至資產時，對話方塊會將標籤顯示為樹狀元素。 ARIA屬性已適當套用至樹狀元素，現在即可供存取。 <!-- via CQ-4272964 -->

* [!DNL AEM Desktop app] 2.0.3版現已推出。 它改善了與的相容性 [!DNL Experience Manager] 6.5.5 service pack和更新的使用者端作業系統相容性清單。 [!DNL Windows] 7和 [!DNL macOS] 不支援10.14之前的版本。

### [!DNL Assets] 中修复的错误 {#bugs-fixed}

* 「關聯和取消關聯」選項在第一次點按時未回應。 (CQ-4299022)
* 下載資產時，如果您選取透過電子郵件接收資產的選項，則不會傳送電子郵件。 (CQ-4299146)

## Adobe Experience Manager Commerceas a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 產品主控台功能現已推出。 這可讓AEM中的行銷人員/作者檢視和導覽儲存於商務後端的類別和產品。 此外，產品主控台也支援類別和產品屬性。

* 產品和類別選擇器經過改良，行銷人員可透過SKU選取產品，或透過類別ID選取類別。

## Cloud Manager {#cloud-manager}

### 发布日期 {#release-date-cm}

的發行日期 [!UICONTROL Cloud Manager] 2020.8.0版為2020年8月6日。

### 新增功能 {#what-is-new-cloud-manager}

* 内容审核是 Cloud Manager Sites 生产管道上启用的一项功能。 带有 Sites 的程序的生产管道配置现在包括名为&#x200B;**内容审核**&#x200B;的第三个选项卡。 无论何时运行生产管道，都会在自定义功能测试后在管道中包含一个新的“内容审核”步骤，该步骤将根据多个维度评估网站，包括性能、SEO（搜索引擎优化）、可访问性、最佳实践和 PWA (Progressive Web App)。


   >[!NOTE]
   >内容审核已重命名为体验审核。

   有关详细信息，请参阅[体验审核测试](/help/implementing/cloud-manager/experience-audit-testing.md)。

* Assets 程序中新建环境现在将自动配置为智能内容服务。

* 休眠环境可以从 Cloud Manager 的&#x200B;**概述**&#x200B;页面中解除休眠。

* 能够在页面上执行体验检查，由 Google Lighthouse 提供支持。 作为 Cloud Manager 管道的一部分，最多可以根据体验 KPI 检查和验证 25 个页面，分数显示在 Cloud Manager UI 中。

### 错误修复 {#bug-fixes-cm}

* 作为代码质量扫描的一部分，正在执行一些不必要且不受欢迎的 SonarQube 插件。

* 在管道执行页面上，分支名称的格式不正确。

* 在某些情况下，已完成的管道执行未成功记录为已完成，从而阻止了新的管道执行。

* 由于内部通信问题，管道执行偶尔会&#x200B;*卡住*。

* 在配置新组织时，一些具有系统管理员以外管理角色的用户被错误地授予访问 Cloud Manager 的权限。

* 在某些情况下，更新索引作业同时多次启动，导致部署失败。

* 程序卡上的工具提示不一致。

* 删除用户界面时，错误地允许在环境上尝试操作。

* Cloud Manager 的&#x200B;**概述**&#x200B;页面上颜色不匹配。

### 已知问题 {#known-issues-cm}

* 包含无效页面，使内容审核平均分数低于应有值。

* “内容审核”选项卡使用作者域而非发布域错误地显示了基本 URL。

* 为了激活“内容审核”步骤，用户必须编辑管道，也可以选择添加页面。 如果没有添加页面，将审核主页。

## 内容传输工具 {#content-transfer-tool}

請詳閱本節，瞭解「內容轉移工具」版本1.0.4的新增功能和更新。

### 新增功能 {#what-is-new-ctt}

* 「內容轉移工具」現在支援共用的S3資料存放區。

### 错误修复 {#ctt-bug-fixes}

* 工具完成動作已新增其他逾時。

* 即使記錄顯示錯誤，舊版UI有時仍會顯示成功擷取。

## 代码重构工具 {#code-refactoring-tools}

請詳閱本節，瞭解程式碼重構工具的新增功能和更新。

### 新增功能 {#what-is-new-refactoring}

* 推出AIO-CLI增效模組，整合了程式碼重構工具，讓開發人員得以從單一位置叫用及執行程式碼重構工具。 請參閱 [Git資源： aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) 以取得更多詳細資料。

* 已擴充的AEM Dispatcher Converter可支援將內部部署和Adobe Managed Services Dispatcher設定轉換為與AEMas a Cloud Service相容的Dispatcher設定。 請參閱 [Git資源： AEM Cloud Service Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) 以取得更多詳細資料。

* AEM Dispatcher Converter重新寫入 ` node.js ` 並與AIO-CLI外掛程式整合。
