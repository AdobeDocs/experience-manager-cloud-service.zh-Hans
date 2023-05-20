---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2020.9.0 版的发行说明。'
description: '"[!DNL Adobe Experience Manager] 2020.9.0版as a Cloud Service發行說明」。'
exl-id: 2332512f-8c52-4569-a006-faa36a7670a1
source-git-commit: bc4da79735ffa99f8c66240bfbfd7fcd69d8bc13
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 20%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2020.9.0 版的发行说明  {#release-notes}

以下區段會概述以下專案的一般發行說明： [!DNL Experience Manager] as a Cloud Service2020.9.0。

## 发布日期 {#release-date}

的發行日期 [!DNL Adobe Experience Manager] as a Cloud Service2020.9.0為2020年9月24日。

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### [!DNL Sites] 的新增功能 {#what-is-new-sites}

* 单页面应用程序 (SPA) 编辑器 JavaScript SDK [现已开源](/help/implementing/developing/hybrid/reference-materials.md)。

## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

### [!DNL Assets] 的新增功能 {#what-is-new-assets}

* 透過資產微服務產生的轉譯支援浮水印影像檔案。 它可以設定為處理設定檔，並使用PNG檔案作為浮水印。 另請參閱 [為您的資產加上浮水印](/help/assets/watermark-assets.md).

* 中的增強功能 [!DNL Dynamic Media]

   * 選擇性發佈 — 行銷團隊現在可以存取 [!DNL Dynamic Media] 同步至的智慧型裁切影像和動態轉譯 [!DNL Dynamic Media] 因此他們可以建立促銷材料，而完全無須將這些資產發佈至 [!DNL Dynamic Media] 用於全域傳送。 [!DNL Experience Manager] 和 [!DNL Dynamic Media] 發佈是分離的，可個別執行以達成此目的。 另請參閱 [選擇性發佈](/help/assets/dynamic-media/selective-publishing.md).
   * 管理員現在可以重設 [!DNL Dynamic Media] 布建時收到的Cloud Service密碼。 重設可在中完成 [!DNL Experience Manager] 使用者介面，而不需使用 [!DNL Dynamic Media Classic] 案頭應用程式。

* 若要瞭解下列增強功能，請參閱 [Brand Portal的新功能](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html).

   * 透過Adobe Document Cloud View SDK整合強化PDF預覽。
   * 按一下即可下載功能。
   * 下載體驗的新管理設定。

<!--
### Bugs Fixed {#bugs-fixed-assets}

TBD: list of Assets aaCS bugs that are fixed.
-->

## Adobe Experience Manager Commerceas a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 已發行CIF Core Components v1.3.0。請參閱 [CIF Core Components](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.3.0) 以取得更多詳細資料。

* 產品和類別範本的產品/類別預覽功能現已可用。 這可讓AEM的業務使用者/行銷人員檢視具有真實資料的產品/類別範本。

* 產品和類別新增了屬性頁面，可讓業務使用者檢視與產品SKU/類別ID相關聯的詳細資料。

* 「產品控制檯」新增了排序功能，可依名稱或價格屬性排序產品/類別。

* 產品控制檯新增了產品搜尋功能。

### 错误修复 {#bug-fixes-commerce}

* Commerce Cloud設定未遵循繼承。 此問題已修正，以確保設定會繼承值。

## Cloud Manager {#cloud-manager}

### 发布日期 {#release-date-cm}

的發行日期 [!UICONTROL Cloud Manager] 2020.9.0版為2020年9月3日。

### 新增功能 {#what-is-new-cloud-manager}

* 内容审核已重新标记为体验审核。
* 构建过程分为三个单独的 Maven 命令。
* 如果 Git 存储库无法克隆，则最多允许重复尝试三次。

### 错误修复 {#bug-fixes-cm}

* “内容审核”选项卡使用作者域而非发布域错误地显示了基本 URL。

## Cloud Readiness Analyzer {#cloud-readiness-analyzer}

请阅读本章内容，了解 Cloud Readiness Analyzer v1.1.0 版的新增功能和更新。

### 新增功能 {#what-is-new-cra}

* Cloud Readiness Analyzer (CRA)有一個顯示明確的 **產生報表** 按鈕讓使用者按一下以執行CRA。

* CRA UI在執行時會顯示進度。 它會顯示正在分析的專案，以及在執行期間找到的結果。

* CRA報告會以表格格式顯示結果的摘要和數目，並依結果型別和重要性層級加以整理。 按一下該結果的數目將自動捲動到該結果在報告中的位置。

### 错误修复 {#cra-bug-fixes}

* 在某些情況下，在強制重新整理後，CRA報表沒有更新。 此版本已修正此問題。

## 内容传输工具 {#content-transfer-tool}

請詳閱本節，瞭解「內容轉移工具」版本1.1.10的新增功能和更新。

### 新增功能 {#what-is-new-ctt}

* 內容轉移工具(CTT)支援Azure Blob存放區資料存放區。

* CTT使用者介面具有自動重新載入功能，每30秒重新載入一次概觀頁面。

* 新增至CTT使用者介面的按鈕以擷取 *存取Token* 輕鬆進行。

* 已新增描述性驗證訊息 *URL* 和 *移轉集名稱*.

## 代码重构工具 {#code-refactoring}

請詳閱本節，瞭解程式碼重構工具的新增功能和更新。

### 新增功能 {#what-is-new-refactoring}

* AIO-CLI外掛程式支援Repository Modernizer，可讓使用者使用外掛程式執行工具。

   請參閱 [Git資源： aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) 以取得更多詳細資料。

* Repository Modernizer公用程式可用來將現有的專案套件重新建構為與針對AEMas a Cloud Service定義的專案結構相容的套件。

   請參閱 [Git資源： Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) 以取得更多詳細資料。
