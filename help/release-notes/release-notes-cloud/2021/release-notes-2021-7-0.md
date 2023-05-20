---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.7.0 版的发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.7.0 版的发行说明。'
exl-id: 848f6a29-2e0f-4976-8ed7-6b7f69408c1b
source-git-commit: cc6565121a76f70b958aa9050485e0553371f3a3
workflow-type: tm+mt
source-wordcount: '1316'
ht-degree: 50%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明 {#release-notes}

以下部分概述了当前（最新）版本的 [!DNL Experience Manager] as a Cloud Service 的一般发行说明。

>[!NOTE]
>
>從這裡，您可以瀏覽至舊版的發行說明；例如，2020、2021等版本。

>[!NOTE]
>
>有关未与版本直接相关的文档更新的详细信息，请参阅[最新文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)。

## 发布日期 {#release-date}

的發行日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 目前版本(2021.7.0)為2021年7月29日。
以下版本(2021.8.0)的發佈日期為2021年8月26日。

## 发布视频 {#release-video}

請檢視 [2021年7月版本總覽](https://video.tv.adobe.com/v/335580) 影片以瞭解新增功能的摘要。

## Experience Manager Foundationas a Cloud Service {#foundation}

### 新增功能 {#what-is-new-foundation}

* 更靈活的Dispatcher設定：更輕鬆地組織專案。 例如，您現在可以包含反映網站結構的多個重寫規則檔案。 [瞭解](/help/implementing/dispatcher/disp-overview.md#validation-debug) 此彈性模式，包括如何建構您的Dispatcher設定，以妥善運用。
* 在復寫代理程式的「散發」標籤下方的樹狀結構復寫UI應視為不建議使用，並計畫於9月30日後移除。 [瞭解](/help/operations/replication.md#tree-activation) 替代復寫策略。
* 組合 `org.apache.sling.datasource-1.0.4.jar` 的Sling資料來源支援已移除，因為其功能已過時且未由客戶使用。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新增功能 {#assets-features}

* 內容自動化功能可讓 [!DNL Experience Manager Assets] 善用 [!DNL Adobe Creative Cloud] API可大規模自動化資產的製作。 它大幅減少建立相同資產變體所需的時間和反複工作，進而加快內容速度。 此功能不需要從DAM中進行任何程式設計和工作。 另請參閱 [使用Creative Cloud整合產生資產的變體](/help/assets/cc-api-integration.md).

* [!DNL Experience Manager Assets] 包含 [!DNL Document Cloud] PDF檢視器以原生方式預覽PDF檔案。 此功能可讓使用者預覽多頁PDF檔案，而不需進行任何檔案處理或轉換。 此功能可改善 [!DNL Experience Manager] 6.5.檢視器中可用的控制項包括縮放、瀏覽至頁面、取消固定控制項，以及全熒幕檢視。 使用者案例也可預覽和跳至頁面和書籤。 支援檔案本身的註解，未來版本會新增對PDF檔案內內容的註解和附註。

   ![在中預覽PDF檔案 [!DNL Experience Manager] 使用PDF檢視器](/help/assets/assets/preview-pdf-file-viewer.png)

* Linkshare下載功能會使用可提高下載速度的非同步下載。 另請參閱 [下載使用連結共用所共用的資產](/help/assets/download-assets-from-aem.md#link-share-download).

   ![下載收件匣](/help/assets/assets/download-inbox.png)

* 已增強檢視設定，讓使用者可選擇預設檢視和預設排序引數。

   ![設定預設檢視於 [!UICONTROL 檢視設定]](/help/assets/assets/view-settings-for-defaults.png)

* 使用者可以根據屬性述詞搜尋和篩選資料夾。

   ![使用搜尋述詞篩選搜尋資料夾](/help/assets/assets/search-folders-via-predicates.png)

### 中可用的新功能 [!DNL Assets] 發行前通道 {#assets-prerelease-features}

<!-- TBD: Not sure about GA of these enh. Shall check with the team.

* A user experience enhancements displays the number of assets present in a folder. For more than 1000 assets in a folder, [!DNL Assets] displays 1000+.

  ![Number of assets in a folder are displayed on the interface](/help/assets/assets/browse-folder-number-of-assets.png)

* You can directly apply a metadata schemas to a folder in its [!UICONTROL Properties].

  ![Add metadata schema from folder properties](/help/assets/assets/metadata-schema-folder-properties.png)
-->

* 當您以連結形式共用數位資產時，使用者可以將URL複製到剪貼簿。 此增強功能可讓您以更快、更方便的方式共用資產。

### [!DNL Assets] 中修复的错误 {#assets-bugs-fixed}

API `com.day.cq.dam.api.collection.SmartCollection` 不可用於 [!DNL Experience Manager] as a [!DNL Cloud Service]. (CQ-4326322)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 的新增功能 {#what-is-new-forms}

* 您现在可以使用 Automated Forms Conversion Service 将[法语、德语和西班牙语版本的 PDF 表单](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model)转换为自适应表单。
* 已向模板编辑器添加一个单独的面板，以显示与自适应表单组件相关的错误。它有助于在一个位置整合所有自适应表单错误并减少解决时间。

### [!DNL Forms] 预发行渠道中提供的新功能 {#beta-features-forms}

* **[!DNL AEM Forms as a Cloud Service - Communications]**：[通信 API](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications.html) 帮助您组合 XDP 模板和 XML 数据以生成各种格式的打印文档。此服務可讓您以同步模式產生檔案。 API 使您能够创建应用程序，这些应用程序允许您：
   * 使用 XML 数据填充模板文件来生成文档。
   * 生成各种格式的输出表单，包括非交互式 PDF 打印流。
   * 利用 XFA 表单 PDF 和 Adobe Acrobat 表单生成打印版 PDF 文件。

* **变量数据外部化程序**：您可以将 AEM Workflow 变量的数据保存在由组织管理的外部存储系统上。

* **基于 Acroform 的记录文档**：除了基于 XFA 的表单模板，您还可以[使用 Adobe Acrobat Form PDF (Acroform PDF)](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/generate-document-of-record-for-non-xfa-based-adaptive-forms.html) 作为记录文档的模板。

* **Microsoft Azure 数据存储连接器**：您现在可以[将表单数据模型连接到 Microsoft Azure Storage](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-azure-storage.html)。它可让您检索自适应表单数据并将这些数据作为 BLOB 存储到 Microsoft Azure Storage。

## CIF 加载项 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* CIF Core Components v2
   * 簡化並改善PDP/PLP URL和SEO的設定
   * 在製作模式中暫存產品資料的視覺指標，可更清楚顯示即將發生的變更
   * 內容和商務頁面的新Sitemap元件

* 支援 [Adobe Commerce Sensei產品推薦，由Adobe Sensei提供技術支援](https://business.adobe.com/products/magento/product-recommendations.html) 在AEM Storefront中使用預先定義或即時建立的建議

## [!DNL Experience Manager Screens] as a [!DNL Cloud Service] {#screens}

### 错误修复 {#bug-fixes-screens}

* 內容提供者設定現在會在建立或更新期間進行驗證。

* 所有顯示檢視都有資料夾欄。

* 您可以展開Screens內容結構。

* `bulk-offline-update-service` 缺少某些環境的所有許可權。

* 更新說明連結以符合新的screens cloud檔案。

* 現在可以取消指派播放清單並禁止移除已指派播放器的播放清單。

* 「全部」快取清除後，播放器現在會重新下載資產。

* 重複排程現在有效，如果 *結束時間* 設為隔天。

* `Back&Forward` 現在適用於Screensas a Cloud ServiceUI。

* 無法更早建立具有相同名稱但不同名稱空間的標籤。

## Experience Manageras a Cloud Service的XML Documentation {#xml-documentation}

### 新增功能 {#what-is-new-xml-documentation}

適用於Experience Manageras a Cloud Service的XML Documentation現已正式推出。 它可讓Experience Manageras a Cloud Service的客戶取得XML Documentation附加元件，以跨多個管道(包括Experience Manager Sites)匯入、建立、管理和傳遞技術內容。

## Cloud Manager {#cloud-manager}

此部分概述了 AEM as a Cloud Service 2021.7.0 中的 Cloud Manager 的发行说明。

### 发布日期 {#release-cm-july}

AEM as a Cloud Service 2021.7.0 中的 Cloud Manager 的发布日期是 2021 年 7 月 15 日。下一版本計畫於2021年8月12日發行。

### 新增功能 {#what-is-new-cm-july}

* 客户现在可以将 Azul 8 和 11 JDK 用于其 Cloud Manager 构建过程，并且可以选择将这些 JDK 之一用于与工具链兼容的 Maven 插件&#x200B;*或*&#x200B;整个 Maven 流程执行。

* 出站出口 IP 现在将记录在构建步骤日志文件中。

* 运行旧版本的 AEM 的暂存环境和生产环境现在将报告&#x200B;**更新可用**&#x200B;状态。

* 每个程序支持的 SSL 证书的最大数量已增至 20。

* 每个环境可配置的域的最大数量已增至 500。

* **管理 Git** 按钮已更名为&#x200B;**访问 Git 信息**，并且对话框的外观已更新。

* Cloud Manager 使用的 AEM 项目原型的版本已更新到版本 28。

### 错误修复 {#bug-fixes-cm-july}

* 在某些情况下，将 IP 允许列表绑定到环境时，“预览”选项不可用。

* 手动导航到不存在的执行的执行详细信息页面并没有显示错误，只显示了一个无休止的加载屏幕。

* 当达到 SSL 证书的最大数量时显示的错误消息没有帮助。

* 在某些情况下，**概述**&#x200B;页面上的管道信息卡中显示的版本可能存在差异。

* 添加程序向导错误地指出，创建后无法更改名称。

### 已知问题 {#known-issues-cm-july}

改用 Azul JDK 的客户应该知道，并非所有现有应用程序都能在 Azul JDK 上编译无误。 强烈建议在切换前进行本地测试。

## Cloud Acceleration Manager {#cam}

### 发布日期 {#release-date-july-cam}

Cloud Acceleration Manager的發行日期為2021年7月15日。

### 新增功能 {#what-is-new-cam}

Cloud Acceleration Manager 是一个基于云的应用程序，旨在指导您的 IT 团队在 Cloud Service 上完成从规划到上线的过渡过程。使用 Adobe 推荐的最佳实践、技巧、文档和工具在迁移到 AEM as Cloud Service 的历程中的每个阶段提供帮助，让您的团队成功完成迁移。瞭解更多 [此處](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/getting-started-cam.html?lang=en).

>[!NOTE]
>
> 檢查此 [Cloud Acceleration Manager示範影片](https://video.tv.adobe.com/v/335547).
