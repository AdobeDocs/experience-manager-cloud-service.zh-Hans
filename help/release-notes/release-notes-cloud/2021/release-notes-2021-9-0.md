---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.9.0 版的发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.9.0 版的发行说明。'
exl-id: 8c12ff09-fbc8-42dd-87c0-46e509604f36
source-git-commit: cc6565121a76f70b958aa9050485e0553371f3a3
workflow-type: tm+mt
source-wordcount: '1572'
ht-degree: 38%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明 {#release-notes}

以下部分概述了当前（最新）版本的 [!DNL Experience Manager] as a Cloud Service 的一般发行说明。

>[!NOTE]
>
>您可以在此部分中导航到早期版本的发行说明；例如，2020 版、2021 版等的发行说明。

>[!NOTE]
>
>有关未与版本直接相关的文档更新的详细信息，请参阅[最新文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)。

## 发布日期 {#release-date}

的發行日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 目前版本(2021.9.0)為2021年10月6日。
以下版本(2021.10.0)將於2021年11月4日發行。

## 发布视频 {#release-video}

請檢視 [2021年9月版本總覽](https://video.tv.adobe.com/v/337381) 影片以瞭解新增功能的摘要。

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### 中的新功能 [!DNL Sites] 發行前通道 {#sites-prerelease-features}

* 內容片段模型現在會在發佈後自動設定為唯讀狀態，以避免重新發佈已編輯的模型後無意間中斷即時API查詢。 嘗試編輯已發佈的模型時，系統會提示使用者警告。 接受警告後即可進行編輯。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新增功能 {#assets-features}

* 使用者現在可以在「欄」和「卡片」檢視中排序搜尋結果內所顯示的資產。 排序功能適用於「名稱」、「已建立」、「已修改」或「無」欄。

   ![將搜尋結果排序於 [!DNL Assets] 在欄和卡片檢視中](/help/assets/assets/sort-searched-assets.png)
   *圖：將搜尋結果排序於 [!DNL Assets] 在欄和卡片檢視中。*

* 為了以程式設計方式使用資產微服務叫用處理，我們引進了新的API。 開發人員現在可以將現有的檔案夾層級處理設定檔套用至檔案夾中一個或多個特定資產。 處理設定檔會根據自訂中繼資料屬性更新而套用。 另請參閱 `AssetProcessor` 在 [[!DNL Experience Manager] API參考](https://www.adobe.io/experience-manager/reference-materials/). 和以前一樣，可以 [從使用者介面使用資產微服務](/help/assets/asset-microservices-configure-and-use.md).

<!-- Leave this commented.

### New feature in the [!DNL Assets] prerelease channel {#assets-prerelease-features}

Apparently, no new Assets features in Sep beta channel.
A/V transcription feature via CQ-4303854 has moved to Oct beta now.

### Bugs fixed in [!DNL Assets] {#assets-bugs-fixed}

No customer-reported bugs fixed in Sep release.
CQ-4328183 was not reported on CS so not documented here.
-->

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 的新增功能 {#what-is-new-forms-sep-2021}

* **在自适应表单中使用 Adobe Sign 角色**：用于商业和企业服务级别的 Adobe Sign 可让您选择扩展协议接收者的角色（不仅限于签名者），以便更好地匹配他们的工作流要求。您现在可以[允许每个协议接收者在自适应表单中配置自己的角色](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/use-adobe-sign/working-with-adobe-sign.html#addsignerstoanadaptiveform)，签名者是默认角色。

* **Analytics for Adaptive Forms**：您现在可以通过 Adobe Analytics for Adaptive Forms 捕获和跟踪最终用户行为，从而收集最终用户洞察。这有助于根据数据做出明智的决策，从而改善最终用户体验。

* **轻松地将 AEM Forms 与 Microsoft Dynamics 和 Salesforce 连接**：此服务为 Microsoft Dynamics 和 Salesforce 提供现成的数据源配置和数据模型，使得[开发人员可以更快、更轻松地配置 Microsoft Dynamics 和 Salesforce 作为自适应表单的数据源](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-msdynamics-salesforce.html?lang=en)。

* **使用 DocuSign 对自适应表单进行电子签名：**&#x200B;您可以使用 DocuSign 对自适应表单进行电子签名。此服务提供了自定义提交操作，可将 DocuSign 与自适应表单结合使用。您可以安裝Software Distribution上可用的套件，以匯入提交動作。

### [!DNL Forms] 的 Beta 版功能 {#sep-what-is-new-forms-prerelease}

* **统一存储连接器：**&#x200B;使用统一存储连接器将客户管理的存储库中的进程内数据外部化。例如，您可以
   * 启用 Forms Portal 的保存和恢复功能，将自适应表单草稿存储到客户管理的数据存储库中。
   * 将包含敏感个人数据 (SPD) 的进程内 AEM Workflow 数据（AEM Workflow 变量数据）存储在客户管理的存储库中。

* **[!DNL AEM Forms as a Cloud Service - Communications]**：[通信 API](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications.html) 帮助您组合 XDP 模板和 XML 数据以生成各种格式的打印文档。该服务允许您以同步模式生成文档。API 使您能够创建应用程序，这些应用程序允许您：
   * 使用 XML 数据填充模板文件来生成文档。
   * 生成各种格式的输出表单，包括非交互式 PDF 打印流。
   * 利用 XFA 表单 PDF 和 Adobe Acrobat 表单生成打印版 PDF 文件。

您可以将电子邮件发送到 [!DNL formscsbeta@adobe.com] 以注册 Beta 项目。

## CIF 加载项 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* Sites編輯器中新的「相關商務內容」索引標籤透過快速存取目前內容的相關AEM產品內容來提高作者效率

   ![關聯的商務內容](/help/assets/CIF/associated-commerce-content.png)

* 改善產品選擇器UI，提供更佳的使用者體驗、更高的效率，以及支援複雜的產品目錄

   ![新的產品選取器](/help/assets/CIF/product-picker.png)

* 在導覽元件中遵循「include_in_menu」屬性

### 错误修复 {#bug-fixes-cif}

* 功能表快取排清未按預期運作

* AEM CS部署步驟期間以及未使用使用者端元件時的JS錯誤

* 無法在具有sling：configs節點的資料夾中建立CIF雲端設定

## [!DNL Experience Manager Screens] as a [!DNL Cloud Service] {#screens}

### 新增功能 {#what-is-new-screens}

* Screensas a Cloud Service現在支援基本播放監控。 播放器現在會報告每次ping （預設為30秒）的各種播放量度。 根據量度，它提供偵測各種邊緣情況（停滯體驗、空白熒幕、排程問題等）的能力。 此功能可讓團隊從遠端監控播放器是否正確播放內容、改善對空白熒幕或現場中斷體驗的反應性，並降低向一般使用者顯示中斷體驗的風險。
另請參閱 [基本播放監視](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/manage-player-registration/installing-screens-cloud-player.html?lang=en#playback-monitoring) 以取得更多詳細資料。

* Screensas a Cloud Service現在支援影片的縮圖支援。 內容作者可以定義影片的縮圖，以便在適當的團隊正在完成實際影片時，影像可以當做預留位置並正確測試內容播放和目標定位。 如果影片播放失敗，也可以使用該影像。
另請參閱 [影片的縮圖支援](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/core-product-features/thumbnail-support-videos.html) 以取得更多詳細資料。

### 错误修复 {#bug-fixes-screens}

* 播放器無法顯示內嵌頁面的內容，此問題現已修正。

* 成功登入後，導覽至預設頁面（管道）最後會進入內部伺服器錯誤頁面。

* 移除播放清單時未移除關聯的標籤專案。

## [!DNL Experience Manager as a Cloud Service] Foundation {#foundation}

### [!DNL Experience Manager as a Cloud Service] 中的新增功能 {#foundation-features}

**進階網路**

>[!INFO]
>
>進階網路功能是2021.9.0版本的一部分，將於10月中旬為客戶啟用。

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 現在提供數種進階網路功能，包括：

* 彈性的連線埠輸出可讓流量從非標準連線埠輸出。 現在無需連絡Adobe支援即可使用。
* 專用輸出IP位址，可讓流量從唯一IPas a Cloud Service輸出AEM，現在支援所有連線埠。
* VPN可保護您的基礎結構與AEMas a Cloud Service之間的流量。

閱讀 [檔案](/help/security/configuring-advanced-networking.md) 如需詳細資訊，包括如何使用Cloud Manager API自助布建進階網路。

**索引最佳化**

為了改善搜尋查詢和索引的效能，全文檢索lucene-2不再用於 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 此版本中的。 為了根據AEM客戶在AEM環境中移除此全文索引，Adobe工程團隊會與客戶個別並主動合作，以溫和且可持續的方式移除Lucene全文索引。 請造訪 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] [檔案](/help/operations/indexing.md#index-optimizations) 若您有任何問題，請直接連絡我們的支援以取得詳細資訊。

## Cloud Manager {#cloud-manager}

本節概述AEM as a Cloud Service 2021.9.0和2021.8.0中Cloud Manager的發行說明

## 发布日期 {#release-date-cm-sept}

AEM as a Cloud Service 2021.9.0 中的 Cloud Manager 的发布日期是 2020 年 9 月 9 日。下一版本計畫於2021年10月7日發行。

### 新增功能 {#what-is-new-cm-sept}

* Cloud Manager 使用的 AEM 项目原型的版本已更新到版本 30。

* Cloud Manager 登陆页面上的程序信息卡和相关体验都已更新。

* 代码质量步骤日志现在包括有关 OakPal 扫描过程的详细日志信息。

* 活动页面菜单选项现在包括一个选项，用于&#x200B;**下载已完成的代码生成器执行的日志**。 选择此选项，将下载构建步骤的日志。

* 現在直接按一下計畫卡片將瀏覽至Cloud Manager總覽頁面。

### 错误修复 {#bug-fixes-sept}

* 现在，当用户尝试在已达到可配置的最大允许 IP 允许列表数的程序中添加新的 IP 允许列表时，将看到更容易理解的消息。

* 从存储库屏幕选择复制 URL 菜单选项时复制了错误的 URL。

## Cloud Acceleration Manager {#cam}

### 发布日期 {#release-date-october-cam}

Cloud Acceleration Manager的發行日期為2021年10月4日。

### 新增功能 {#what-is-new-cam}

* Cloud Acceleration Manager現在可讓使用者在可列印的預覽中檢視BPA報告，以便進行簡單的列印或列印，以PDF輕鬆共用。 請參閱中的步驟6和7 [使用最佳做法分析卡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=en#best-practices-analysis).

## 内容转移工具 {#content-transfer-tool}

### 发布日期 {#release-date-ctt-latest}

內容轉移工具v1.6.0的發行日期為2021年10月4日。

### 新增功能 {#what-is-new-ctt}

* 透過簡化的使用者體驗改善使用者對應，包括以下列出的功能。 如需詳細資訊，請參閱 [使用使用者對應工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#using-user-mapping-tool).
   * 在執行使用者對應之前測試與使用者管理API的連線
   * 正常略過錯誤，並繼續使用者對應活動
   * 如果存取Token過期（24小時後），使用者對應不再失敗。 可以從上次停止的位置重新執行使用者對應。

* 為了提高CTT的穩健性，內容可以一次擷取到作者執行個體或發佈執行個體。

* 包含版本時，路徑 `/var/audit` 自動包含以移轉稽核事件。

## Best Practices Analyzer {#best-practices-analyzer}

### 发布日期 {#release-date-bpa-latest}

Best Practices Analyzer v2.1.18的發行日期為2021年9月2日。

### 新增功能 {#what-is-new}

* 可偵測節點總數並製作報表。

* 能夠偵測並報告節點存放區型別和大小。

### 错误修复 {#bug-fixes-bpa}

* BPA誤判偵測到Commerce Integration Framework的存在。
