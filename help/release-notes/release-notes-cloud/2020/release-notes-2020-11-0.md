---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2020.11.0 版的发行说明。'
description: '"[!DNL Adobe Experience Manager] 2020.11.0版as a Cloud Service發行說明」。'
exl-id: 8066c0fb-c2f5-4625-9448-b0c74ff4e192
source-git-commit: bc4da79735ffa99f8c66240bfbfd7fcd69d8bc13
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 18%

---

# [!DNL Adobe Experience Manager]as a Cloud Service 版的发行说明 {#release-notes}

以下區段會概述以下專案的一般發行說明： [!DNL Experience Manager] as a Cloud Service。

## 发布日期 {#release-date}

的發行日期 [!DNL Adobe Experience Manager] as a Cloud Service2020.11.0是2020年12月2日。
下列版本(2020.12.0)將於2020年12月17日發行

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### [!DNL Sites] 的新增功能 {#what-is-new-sites}

* **[啟動階層管理](/help/sites-cloud/authoring/launches/managing-pages.md) 和 [未來時間扭曲](/help/sites-cloud/authoring/launches/preview.md)**：新的UI可在啟動項內新增/移除頁面，且使用時間扭曲功能瀏覽網站會顯示啟動項的未來狀態。

* **[延伸內容片段模型與編輯器](/help/assets/content-fragments/content-fragments-models.md)**：適用於各種資料型別的輸入驗證新選項、透過新表單視覺效果改良的列舉資料型別，以及可在Assets UI中顯示和搜尋內容片段模式名稱。

* **排序可用於轉出的即時副本頁面**：新選項，可排序可用於轉出的即時副本頁面，使用 [!UICONTROL 名稱]， [!UICONTROL 上次修改日期]、和 [!UICONTROL 上次轉出日期] 屬性。 此 [!UICONTROL 上次轉出日期] 頁面適用的是推出的新屬性。

## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

### 的新增功能 [!DNL Assets] 和 [!DNL Dynamic Media] {#what-is-new-assets}

* **大量資產擷取**：為客戶提供可擴充的雲端原生擷取服務，並運用 [!DNL Experience Manager] as a Cloud Service架構，包括資產微服務。 主要使用案例包括大規模擷取及監控、報告和排程，同時允許使用通用雲端上傳工具將資產初步轉移至雲端資料存放區。 另請參閱 [資產大量擷取器工具](/help/assets/add-assets.md#asset-bulk-ingestor).

   此工具適用於系統管理員、顧問或實作合作夥伴角色。 此功能允許大規模擷取，最適合用於初始擷取或偶爾的大量擷取。 對於較小的內嵌工作，請使用 [[!DNL Experience Manager] 案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html?lang=en) 或 [使用Assets使用者介面上傳](/help/assets/add-assets.md#upload-assets).

   ![大量匯入工具的設定](/help/assets/assets/bulk-import-config-low-res.png)

* 使用者現在可以在卡片檢視和欄檢視中排序數位資產。

   ![排序資產](/help/assets/assets/asset-sort-options.png)

* 下列增強功能針對中的協助工具而完成 [!DNL Experience Manager Assets] 在這個版本中。 如需詳細資訊，請參閱 [中的協助工具功能 [!DNL Assets]](/help/assets/accessibility.md).

   * 使用鍵盤導覽時間軸時，Esc鍵可以摺疊「全部顯示」選項而不會失去焦點。
   * 使用鍵盤Tab鍵導覽時，從新增的標籤中移除最後一個標籤後，標籤欄位會保持焦點。
   * [!DNL Experience Manager] 元件現在包含熒幕朗讀程式使用的名稱、角色和值的適當資訊。
   * 刪除「型別/大小」下拉式方塊、「連結」下拉式方塊、「語言」下拉式方塊或「文字」編輯方塊後，鍵盤焦點會回到下一個或上一個使用者介面元素，或是更相關的使用者介面元素。
   * 將指標暫留在選項上時，會出現「選取」和「下載」等提示。 由於這些秘訣，使用熒幕放大鏡的使用者可能無法看到檔案縮圖。 現在，在使用移除選項後，可以保留焦點 `Escape` 金鑰。
   * 從頁面中顯示的格線選取格線儲存格時，焦點會移至熒幕上顯示的動作列。
   * 視覺化使用者可以區分一般文字和連結，因為視覺化線索（底線和V形圖示）會顯示中所有解決方案的連結 [!DNL Experience Manager] 首頁。

* **Dynamic Media中的批次集預設集**：現在您可以單獨或使用大量擷取將資產檔案上傳至資料夾時，自動建立及組織影像集或迴轉集中的多個資產。

   另請參閱 [關於批次集預設集](/help/assets/dynamic-media/batch-set-presets-dm.md).

* 下列協助工具增強功能現已開放使用 [!DNL Dynamic Media]：

   * 熒幕助讀程式（JAWS、朗讀程式）會在「內嵌大小」選單選項中講述選單專案的名稱、角色和狀態。
   * 使用者可以使用以下工具瀏覽電子郵件連結對話方塊： `Tab` 金鑰。
   * 有了熒幕助讀程式的增強功能，建立視訊編碼設定檔的工作流程會更方便使用。
   * 使用導覽時 `Tab` 鍵，焦點會移至工作流程中的適當使用者介面元素，以建立互動式視訊。
   * 改善「發佈」頁面、「編輯資產」頁面、「編輯智慧型裁切」頁面和「影像集編輯器」頁面，以符合Web標準。 輔助技術(AT)使用者現在可以輕鬆導覽這些頁面，並執行下列動作，例如裁切影像。
   * 檢視器經過改良，可讓使用者使用鍵盤導覽。
   * 鍵盤和熒幕助讀程式的使用者可以使用裁切功能。
   * 鍵盤使用者可以更好地管理熱點。

   另請參閱 [中的協助工具 [!DNL Dynamic Media]](/help/assets/dynamic-media/accessibility-dm.md).

## Adobe Experience Manager Commerceas a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 已發行CIF Venia Reference Site - 2020.11.05，其中包含最新CIF Core Components v1.5.0版。請參閱 [CIF Venia參考網站](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.27) 以取得更多詳細資料。

* 已發行CIF Core Components v1.5.0。請參閱 [CIF Core Components](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.5.0) 以取得更多詳細資料。

### 错误修复 {#bug-fixes-commerce}

* 未直接在Sling CA設定（但其中一個父設定）中指定設定時，GraphQL使用者端設定無法正確讀取。 此问题已得到修复。

## Cloud Manager {#cloud-manager}

### 发布日期 {#release-date-cm}

AEM as a Cloud Service 2020.11.0 中的 Cloud Manager 的发布日期是 2020 年 11 月 12 日。

### [!DNL Cloud Manager] 的新增功能 {#what-is-new-cm}

* 新功能表選項 **本機登入** 現在可供使用者從 **環境** 卡片和 **環境** 摘要頁面。
有关更多详细信息，请参阅[管理环境](/help/implementing/cloud-manager/manage-environments.md#login-locally)。

* Cloud Manager 中的&#x200B;**学习**&#x200B;选项卡已在 UI 中用新图像刷新。

### 错误修复 {#bug-fixes-cloud-manager}

* 在构建执行之前完成的依赖项加载需要下载 Maven 插件。
* Cloud Manager 页脚中用于选择语言的链接现在将导航到正确的位置。
* 有时在代码扫描期间，SonarQube 进程不会启动。 现在将自动检测并尝试重新启动。
* 所有现有生产管道都将通过体验审核步骤自动启用。

## Adobe Experience Manager as a Cloud Service 基础 {#cloud-service-foundation}

### 工作流 {#workflows}

* 已新增根據工作流程標題、工作流程模型、狀態、發起人、裝載路徑和開始日期來搜尋工作流程例項的支援。 另請參閱 [搜尋工作流程例項](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/administering/workflows-administering.html).

### 發佈層使用者資料同步 {#user-sync}

* 使用者資料（包括設定檔屬性和群組成員）可儲存於發佈層級。 若要深入瞭解此功能，請參閱 [註冊、登入和使用者個人資料檔案](/help/sites-cloud/authoring/personalization/user-and-group-sync-for-publish-tier.md).

### SDK 内部版本分析程序 {#analyzers}

AEM as a Cloud Service SDK 生成分析器 Maven 插件可检测 Maven 项目中的问题，包括缺少依赖项的问题。 它使开发人员有机会在使用 Cloud Manager 部署到云环境之前，在本地开发期间发现问题。如需詳細資訊，請參閱檔案 [此處](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=zh-Hans#developing) 和 [此處](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#building-for-the-sdk).

### 其他 {#others-foundation}

新增 [&quot;httpd -t&quot;語法](/help/implementing/dispatcher/disp-overview.md#local-validation) 檢查在Cloud Manager建置期間執行的Apache和Dispatcher設定，這些設定也可以使用AEMas a Cloud ServiceSDK的Dispatcher工具執行。

## 内容传输工具 {#content-transfer-tool}

請詳閱本節，瞭解的新增功能和更新 [內容轉移工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html) 發行版本1.1.12。

### 新增功能 {#what-is-new-ctt}

* 改善記錄的使用者體驗。 擷取和內嵌記錄檔中新增的時間戳記。 已新增訊息，以指出記錄檔是否為空白。

### 错误修复 {#ctt-bug-fixes}

* 如果移轉集包含的路徑具有部分相似的檔案名稱，「內容轉移工具」會略過內容檔案。 此问题已得到修复。

## Best Practices Analyzer {#best-practices-analyzer}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer的發行日期為2020年11月13日。

### [!DNL Best Practices Analyzer] 的新增功能 {#what-is-new-bpa}

* Cloud Readiness Analyzer現在更名為Best Practices Analyzer (BPA)。 BPA會評估您目前AEM實作的最佳實務，並協助您評估從現有AEM執行個體移至AEMas a Cloud Service的準備程度。

* 已新增新的偵測器來偵測以下專案的使用： `java.io.InputStream`，若在AEMas a Cloud Service中使用可能會造成問題。

### 错误修复 {#bpa-bug-fixes}

* 造成與相關的正面效果的錯誤 *textfield foundation* 元件已修正。
