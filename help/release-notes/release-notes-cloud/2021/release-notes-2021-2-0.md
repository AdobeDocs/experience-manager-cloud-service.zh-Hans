---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.2.0 版的发行说明。'
description: '"[!DNL Adobe Experience Manager] 2021.2.0版as a Cloud Service發行說明」。'
exl-id: 88dac54b-cc12-44a0-b429-6e691221f806
source-git-commit: bc4da79735ffa99f8c66240bfbfd7fcd69d8bc13
workflow-type: tm+mt
source-wordcount: '1237'
ht-degree: 35%

---


# [!DNL Adobe Experience Manager]as a Cloud Service 版的发行说明 {#release-notes}

以下區段會概述以下專案的一般發行說明： [!DNL Experience Manager] as a Cloud Service。

## 发布日期 {#release-date}

的發行日期 [!DNL Adobe Experience Manager] as a Cloud Service2021.2.0為2021年2月25日。
下列版本(2021.3.0)將於2021年3月25日發行。

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### Headless內容管理 {#headless}

* **[用於內容片段傳送的GraphQL API](/help/headless/graphql-api/content-fragments.md)**：能夠使用GraphQL語法和根據內容片段模型的結構描述查詢內容片段，以產生JSON格式的輸出。

* **[GraphQL API要求的驗證支援](/help/headless/security/authentication.md)**：能夠使用伺服器端API的存取權杖來驗證GraphQL API請求。

* **[RemotePage元件](/help/implementing/developing/hybrid/remote-page.md)**：新增在AEM中檢視和編輯外部SPA的支援。

* **[在AEM內編輯外部SPA](/help/implementing/developing/hybrid/editing-external-spa.md)**：已新增將獨立單頁應用程式上傳至AEM執行個體、新增可編輯的內容區段及啟用編寫的功能。

* 增強GraphQL API的JSON輸出，包括輸出JSON格式和地區設定的豐富文字的功能。

* 對巢狀內容片段模型的支援，允許透過專用內容片段參考資料型別或內嵌在多行文字欄位中的內容片段參考來建立巢狀內容片段結構。

* 內容片段模式資料型別中可用的其他驗證規則，包括「唯一」、「必要」和「可翻譯」。

* 標籤內容片段模型，以及允許在包含原則（依標籤或路徑）的資料夾中建立內容片段的功能。

* 內容片段編輯器中的可用性增強，包括發佈動作和顯示片段所依據的模型。

* 直接在內容片段編輯器中預覽JSON輸出的功能。

<!--
### Progressive Web Apps (PWAs) {#pwa}

* [A Progressive Web App (PWA) version of a site](/help/sites-cloud/authoring/features/enable-pwa.md)  can now be enabled at the project level via simple configuration.
-->

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

## [!DNL Assets] 的新增功能 {#what-is-new-assets}

* 資產來源可透過 [!DNL Experience Manager Assets Brand Portal]. 它有助於從機構使用者獲得資產以用於新的行銷活動、攝影和專案。

* [!DNL Experience Manager Assets] as a [!DNL Cloud Service] 有權預先設定 [!DNL Brand Portal] 執行個體。 此 [!DNL Cloud Manager] 使用者可以啟動 [!DNL Brand Portal] 於 [!DNL Experience Manager Assets] as a [!DNL Cloud Service]. 另請參閱 [啟動Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/brand-portal/configure-aem-assets-with-brand-portal.html?lang=zh-Hans).

* 企業現在可以使用以下專案取得資產： [!DNL Brand Portal]. 資產來源功能運用 [!DNL Brand Portal] 協助客戶與代理商使用者互動，以取得資產用於新的行銷活動、攝影和專案。 另請參閱 [中的資產來源 [!DNL Brand Portal]](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html?lang=zh-Hans).

* 此 [!DNL Brand Portal] 使用情況報告現在僅顯示作用中的使用者。 現在不會顯示非作用中的使用者。 作用中的使用者是指其帳戶已指派至產品設定檔的使用者。 [!DNL Admin Console]. 另請參閱 [[!DNL Brand Portal] 報告](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/admin-tools/brand-portal-reports.html).

* 在 [!DNL Brand Portal]，推出新的下載設定，讓您在下載資料夾、集合等專案時，為每個資產建立個別的資料夾。 另請參閱 [下載設定](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html).

## [!DNL Assets] 中的错误修复 {#bug-fixes-assets}

* 選取多個資產以更新屬性時，有時會發生錯誤或取消選取資產的屬性會更新。 (CQ-4316532)
* 嘗試開啟時 [!UICONTROL 資產管理搜尋邊欄]，頁面會保持空白並按一下 [!UICONTROL 編輯] > [!UICONTROL 設定] 會產生錯誤。 (CQ-4315079)
* 解決命名衝突後建立現有資產的新版本時，會覆寫原始資產的中繼資料。 (CQ-4313594)
* 列印具有長註釋文字的資產時，即使有可用空間，也會裁剪註釋文字。 (CQ-4314101)

## Adobe Experience Manager Commerceas a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 產品體驗管理：使用體驗片段個別豐富產品目錄頁面。

* 擴充產品主控台屬性，以顯示連結的資產和體驗片段，包括快速導覽至相關內容的動作。

* 已發行CIF Venia Reference Site - 2021.02.24，其中包含最新CIF Core Components v1.8.0版。請參閱 [CIF Venia參考網站](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.02.24) 以取得更多詳細資料。

* 已發行CIF Core Components v1.8.0。請參閱 [CIF Core Components](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.8.0) 以取得更多詳細資料。

## Cloud Manager {#cloud-manager}

### 发布日期 {#release-date-cm}

AEM as a Cloud Service 2021.2.0 中的 Cloud Manager 的发布日期是 2021 年 2 月 11 日。

### 新增功能 {#what-is-new-cloud-manager}


* Assets 客户现在可以通过 Cloud Manager UI 以自助方式选择何时何地部署其 Brand Portal 实例。 对于具有 Assets 解决方案的常规（非沙盒）计划，现在可以在生产环境中配置 Brand Portal。 在生产环境中只能进行一次资源调配。

* 项目和沙盒创建中使用的 AEM 项目原型已更新至版本 25。

* 代码扫描期间确定的不推荐使用的 API 列表已经过优化，现包括最新 Cloud Service SDK 版本中不推荐的其他类和方法。

* 已更新 Cloud Manager 的 SonarQube 配置文件，移除 Sonar 规则 squid:S2142。 这将不再与“会话中断”检查冲突。

* Cloud Manager UI 将通知暂时无法添加/更新域名的用户，因为关联的环境已连接正在运行的管道，或者当前正在等待批准步骤。

* 以 Sonar 为前缀的客户 `pom.xml` 文件中设置的属性现已动态移除，以避免构建和质量扫描失败。

* 如果 SSL 证书正由当前部署的域名使用，Cloud Manager UI 将通知暂时无法选择该证书的用户。

* 添加了其他代码质量规则，涵盖 Cloud Service 兼容性问题。

### 错误修复 {#bug-fixes-cloud-manager}

* 根据域名匹配 SSL 证书不再区分大小写。

* 如果证书私钥不符合 2048 位限制，Cloud Manager UI 将通知用户并显示相应的错误消息。

* 如果 SSL 证书正由当前部署的域名使用，Cloud Manager UI 将通知暂时无法选择该证书的用户。

* 在某些情况下，内部问题可能会导致环境删除被卡住。

* 某些管道故障被错误地报告为管道错误。

## 内容转移工具 {#content-transfer-tool}

### 发布日期 {#release-date-ctt}

内容转移工具版本 1.2.4 的发布日期为 2021 年 2 月 10 日。

### 错误修复 {#bug-fixes-ctt}

* 對應多個使用者時，部分使用者的IMS ID對應不正確。 此问题已得到修复。

### 发布日期 {#release-date-ctt-feb}

内容转移工具版本 1.2.2 的发布日期为 2021 年 2 月 01 日。

### 內容轉移工具的新增功能 {#what-is-new-ctt}

* 內容轉移工具新增功能和UI — 使用者對應工具。 此功能會在內容移轉活動中，自動將現有的使用者和群組對應至其AdobeIdentity Management系統ID。
請參閱 [使用使用者對應工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html) 以取得更多詳細資料。
* 內容轉移工具現在會移轉在移轉集內參考的所有群組和使用者（包括子項）。
* 允許使用者選取底下的特定路徑 `/etc` 建立移轉集時。

## Best Practices Analyzer {#best-practices-analyzer}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer v2.1.2的發行日期為2021年2月18日。

### Best Practices Analyzer新增功能 {#what-is-new-bpa}

* 能夠偵測使用AEM Forms和AEM Forms實作，並指出與移轉至AEM Formsas a Cloud Service相關的區域。
* 能夠偵測並報告自訂元件和範本的使用量和計數。
* 能夠偵測使用的節點存放區和資料存放區型別。
* 能夠偵測Dynamic Media的使用情況。
* 可偵測使用的Java版本。

## 代码重构工具 {#code-refactoring-tools}

### 程式碼重構工具的新增功能 {#what-is-new-crt}

* 新版AIO-CLI外掛程式已發行。 此外掛程式的最新版本包含Repository Modernizer的多項錯誤修正。
請參閱 [整合式體驗](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits) 以進一步瞭解此外掛程式。

### 错误修复 {#bug-fixes-crt}

* 對Repository Modernizer進行數項錯誤修正。
請參閱 [GitHub資源： aem-cloud-service-source-migration](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) 以取得更多詳細資料。
