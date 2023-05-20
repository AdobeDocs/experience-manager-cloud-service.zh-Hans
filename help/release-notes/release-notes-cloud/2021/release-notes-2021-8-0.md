---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.8.0 版的发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.8.0 版的发行说明。'
exl-id: 8b041934-1c4a-4670-9b03-d38f683b99e5
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 51%

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

[!DNL Adobe Experience Manager][!DNL Cloud Service] 当前版本 (2021.8.0) 的发布日期为 2021 年 26 月 8 日。以下版本(2021.9.0)的發佈日期為2021年10月6日。

## 发布视频 {#release-video}

請檢視 [2021年8月版本總覽](https://video.tv.adobe.com/v/336277) 影片以瞭解新增功能的摘要。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新增功能 {#assets-features}

* 以連結形式共用數位資產時，使用者可以立即將URL複製到剪貼簿。 此增強功能可讓您以更快、更方便的方式共用資產。 此功能可讓您更快、更方便地共用資產。

   ![以連結形式共用資產時複製URL選項](/help/assets/assets/link-share-copy-URL-option.png)
   *圖：以連結形式共用資產時，您現在可以複製URL來分別共用。*

* 當您上傳TXT檔案時，資產微服務會自動產生縮圖。 PNG縮圖是TXT檔案的轉譯，可幫助使用者在一定程度上識別內容或檔案，而不需要開啟檔案。 依預設，此功能不需要任何設定即可運作。

   ![TXT檔案的轉譯會由自動產生 [!DNL Assets] PNG格式](/help/assets/assets/thumbnail-rendition-txt-file.png)
   *圖：會自動產生TXT檔案的轉譯，以協助您識別檔案而不需要開啟。*

### 中的新功能 [!DNL Assets] 發行前通道 {#assets-prerelease-features}

* 使用者現在可以在「欄」和「卡片」檢視中排序搜尋結果內所顯示的資產。 排序功能適用於「名稱」、「已建立」、「已修改」或「無」欄。

   ![將搜尋結果排序於 [!DNL Assets] 在欄和卡片檢視中](/help/assets/assets/sort-searched-assets.png)
   *圖：將搜尋結果排序於 [!DNL Assets] 在欄和卡片檢視中。*

### [!DNL Assets] 中修复的错误 {#assets-bugs-fixed}

* 當投稿人群組成員導覽至 [!DNL Assets] 主控台，額外的 `POST` 會產生要求以嘗試建立集合。 此請求不是必要請求，它會因許可權問題而失敗，並在記錄中建立許多錯誤。 (CQ-4328856)
* 使用者檢視資產並選取 [!UICONTROL 時間表] 從左側面板的躍現式選單中會顯示錯誤。 在記錄中，由於查詢錯誤，會記錄許多警告。 (CQ-4328919)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 的新增功能 {#what-is-new-forms}

* automated forms conversion服務可以 [轉換義大利文和葡萄牙文的PDF forms](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model) 最適化Forms。

* **基于 Acroform 的记录文档**：除了基于 XFA 的表单模板，AEM Forms as a Cloud Service 还支持使用 [Adobe Acrobat Form PDF (Acroform PDF)](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/generate-document-of-record-for-non-xfa-based-adaptive-forms.html) 作为记录文档的模板。

* **Microsoft Azure 数据存储连接器**：您现在可以[将表单数据模型连接到 Microsoft Azure Storage](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-azure-storage.html)。它可让您检索自适应表单数据并将这些数据作为 BLOB 存储到 Microsoft Azure Storage。

### [!DNL Forms] 预发行渠道中提供的新功能 {#prerelease-features-forms}

* **在自适应表单中使用 Adobe Sign 角色**：用于商业和企业服务级别的 Adobe Sign 可让您选择扩展协议接收者的角色（不仅限于签名者），以便更好地匹配他们的工作流要求。您现在可以允许每个协议接收者在自适应表单中配置自己的角色，签名者是默认角色。

* **Analytics for Adaptive Forms**：您现在可以通过 Adobe Analytics for Adaptive Forms 捕获和跟踪最终用户行为，从而收集最终用户洞察。这有助于根据数据做出明智的决策，从而改善最终用户体验。

* **輕鬆將AEM Forms連線至Microsoft Dynamics和Salesforce.com**：此服務會提供Microsoft Dynamics和Salesforce.com適用的現成資料來源設定和資料模型，好讓開發人員更快且更輕鬆地將Microsoft Dynamics和Salesforce.com設定為最適化表單的資料來源。

## CIF 加载项 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 新的類別選擇器UI可改善使用者體驗、提高效率，以及更好地支援複雜的產品目錄

   ![新增類別選取器](/help/assets/CIF/category-picker.png)

* CIF核心元件更好的A11Y支援

## Cloud Manager {#cloud-manager}

本節概述AEMas a Cloud Service2021.8.0和2021.7.0中Cloud Manager的發行說明

## 发布日期 {#release-date-cm-aug}

AEM as a Cloud Service 2021.8.0 中的 Cloud Manager 的发布日期是 2021 年 8 月 12 日。下一版本計畫於2021年9月9日發行。

### 新增功能 {#what-is-new-aug}

* Cloud Service 客户现在可以在 Cloud Manager 中查看服务水平协议 (SLA) 报告。 该功能将在未来几个月逐步推出。
请参阅 [SLA 报告](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/sla-reporting.html)了解详情。

* IndexType 和 `IndexDamAssetLucene` 质量规则的类型和严重性已更改。 两者均为 Blocker *级别*&#x200B;错误。

* 引入新的 Oak 索引质量规则以涵盖异步和 Tika 配置。

* 将每个程序的最大 SSL 证书数增加到 50。

* 借助自助服务功能，用户可通过 Cloud Manager UI 创建和管理多个存储库。

* SonarQube 未成功读取 Git 历史数据。 在大代码库情况下，这可能会导致出现不必要的构建性能损失。

* 现在有一个 API 可用于使每个管道的 Maven 依赖项缓存失效。

* Cloud Manager 使用的 AEM 项目原型的版本已更新到版本 29。

### 错误修复 {#bug-fixes-aug}

* 当最新版本低于当前版本时，不应显示“更新可用”状态。

* 对于名字很长的新组织，初始登录失败。

* 有时，当管道由于某种原因被触发两次时，会导致其中一个执行失败，并出现&#x200B;*无法更新管道执行状态*&#x200B;错误。

## 内容转移工具 {#content-transfer-tool}

### 发布日期 {#release-date-ctt-latest}

內容轉移工具v1.5.6的發行日期為2021年8月11日。

### 错误修复 {#bug-fixes-ctt}

* 在某些情況下，並非所有使用者都已移轉至目標執行個體。 若要取得此修正，目標AEMas a Cloud Service執行個體上需要CTT v1.5.6以及aem-ethos-tools 1.2.354或更新版本。

* 此 **停止內嵌** 按鈕在內嵌至發佈執行個體期間被停用。 這並非必要，因為發佈內嵌期間沒有mongo還原步驟。

* CTT未清除 `/tmp` 成功擷取後的目錄。 這有時會導致磁碟空間問題。
