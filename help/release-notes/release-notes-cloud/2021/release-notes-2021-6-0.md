---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.6.0 版的发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.6.0 版的发行说明。'
exl-id: 2c72973b-5a51-4744-bf88-50da0013ba31
source-git-commit: 9a08514f11c86b783ae68940a0c3c58fcada3dc2
workflow-type: tm+mt
source-wordcount: '1440'
ht-degree: 48%

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

的發行日期 [!DNL Adobe Experience Manager] as a Cloud Service2021.6.0為2021年6月28日。
下列版本(2021.7.0)將於2021年7月29日發行。

## 发布视频 {#release-video}

請檢視 [2021年6月版本總覽](https://video.tv.adobe.com/v/334296) 影片以瞭解新增功能的摘要。

## AEM as a Cloud Service的XML Documentation {#xml-documentation}

### 新增功能 {#what-is-new-xml-documentation}

* 適用於AEMas a Cloud Service的XML Documentation現已正式推出。
* 這可讓現有AEM Cloud Service客戶取得XML Documentation附加元件，以便跨多個管道(包括AEM網站)匯入、建立、管理和傳遞技術內容

## Cloud Manager {#cloud-manager}

本節概述AEMas a Cloud Service2021.6.0和2021.5.0中Cloud Manager的發行說明

### 发布日期 {#release-date-june-cm}

AEM as a Cloud Service 2021.6.0 中的 Cloud Manager 的发布日期是 2021 年 6 月 10 日。下一版本計畫於2021年7月15日發行。

### 新增功能 {#what-is-new-junecm}

* “预览”服务将以滚动方式部署到了所有程序。为预览服务启用了客户的程序后，会在产品中通知客户。 有关详细信息，请参阅[访问预览服务](/help/implementing/cloud-manager/manage-environments.md#access-preview-service)。

* 现在，在管道执行之间将缓存构建步骤期间下载的 Maven 依赖项。在接下来的几周内，将为客户启用此功能。

* 现在可以通过编辑程序对话框编辑程序名称。

* 通过管理 Git 工作流在项目创建期间以及默认的推送命令中使用的默认分支名称已更改为 `main`。

* UI 中的编辑程序体验已刷新。

* 质量规则 `ImmutableMutableMixCheck` 已更新，以将 `/oak:index` 节点归类为永恒节点。

* 质量规则 `CQBP-84` 和 `CQBP-84--dependencies` 已合并为单一规则。 在此合并过程中，依赖项扫描可以更准确地识别部署到 AEM 运行时的第三方依赖项中的问题。

* 为避免混淆，合并了“环境详细信息”页面上的“发布 AEM”和“发布 Dispatcher”区段行。

   ![](/help/implementing/cloud-manager/release-notes/assets/aem-dispatcher.png)

* 添加了新代码质量规则来验证 `damAssetLucene` 索引的结构。 请参阅[自定义 DAM 资产 Lucene Oak 指数](/help/implementing/cloud-manager/custom-code-quality-rules.md#oakpal-damAssetLucene-sanity-check)，了解更多详细信息。

* “环境详细信息”页面现在将酌情显示发布和预览服务的多个域名。 请参阅[环境详情](/help/implementing/cloud-manager/manage-environments.md#viewing-environment)，了解更多详细信息。

### 错误修复 {#bug-fixes-junecm}

* 未正确分析根元素名称后包含换行符的 JCR 节点定义。

* 列表存储库 API 不会筛选已删除的存储库。

* 为计划步骤提供无效值时，显示错误消息。

* 有时，即使未部署配置，用户也会在 IP 允许列表旁边看到绿色的&#x200B;*活动*&#x200B;状态。

* 某些程序编辑序列可能导致无法创建或编辑生产管道。

* 某些程序编辑顺序可能会导致&#x200B;**概述**&#x200B;页面显示错误消息，重新执行程序设置。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新增功能 {#ga-features-assets}

* 內容自動化功能可讓 [!DNL Experience Manager Assets] 善用 [!DNL Adobe Creative Cloud] API可大規模自動化資產的製作。 它大幅減少建立相同資產變體所需的時間和反複工作，進而加快內容速度。 此功能不需要任何程式碼，並且可在DAM內運作。
* [!DNL Adobe Asset Link] v3.0用於 [!DNL Adobe Photoshop]， [!DNL Adobe Illustrator]、和 [!DNL Adobe InDesign] 和 [!DNL Adobe Asset Link] v2.0用於 [!DNL Adobe XD] 已發行。 它提供：

   * 支援 [!DNL Assets Essentials].
   * 能夠自動連線到 [!DNL Experience Manager] as a [!DNL Cloud Service] 或 [!DNL Assets Essentials].

<!-- TBD: Checking with PMs if AAE release should be mentioned here.
-->

### 中可用的新功能 [!DNL Assets] 發行前通道 {#beta-features-assets}

* 已增強檢視設定，讓使用者可選擇預設檢視和預設排序引數。
* Linkshare下載功能會使用可提高下載速度的非同步下載。
* 使用者可以根據屬性述詞搜尋和篩選資料夾。
* [!DNL Experience Manager Assets] 內嵌由提供支援的PDF檢視器 [!DNL Adobe Document Cloud] 以預覽支援的檔案。 此功能可讓使用者預覽PDF和其他多頁檔案，而不需要任何複雜的處理。 這可改善以下專案的功能對等性： [!DNL Experience Manager] 6.5.

### [!DNL Assets] 中修复的错误 {#bugs-fixed-assets}

* 將擁有者新增至子資料夾時， [!DNL Assets] 也會將相同的使用者新增為父資料夾的擁有者。 (CQ-4323737)
* 將資產新增至集合時，如果使用者對集合搜尋套用篩選器，則使用者無法在清單檢視中檢視集合。 (CQ-4323181)
* 搜尋檔案和資料夾時，如果使用者套用篩選器並選取 [!UICONTROL 檔案與資料夾]，只會顯示檔案，不會顯示資料夾。 (CQ-4319543)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites] 中的新增功能 {#ga-features-sites}

* 發佈到預覽層級現在會在網站管理UI中顯示為頁面狀態
* 「發佈至預覽層」現在會在動作結束時顯示預覽URL，並將該URL儲存在頁面屬性中以供稍後參考

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 的新增功能 {#what-is-new-forms}

* 添加了在 AEM 收件箱中筛选自定义列的功能。
* 添加了使用主题编辑器和自适应表单编辑器的样式层来设置验证码组件样式的功能。
* 提高了自动检测源 PDF 表单中的逻辑部分并将其转换为相应的自适应表单面板的速度和准确性。
* 添加了将 PDF 或 XDP 文件从一个文件夹移动到另一个文件夹的移动操作。

### [!DNL Forms] 的 Beta 版功能 {#what-is-new-forms-prerelease}

* **[!DNL AEM Forms as a Cloud Service - Communications]**：通信 API 可帮助您组合 XDP 模板和 XML 数据以生成各种格式的打印文档。该服务允许您以同步模式生成文档。API 使您能够创建应用程序，这些应用程序允许您：
   * 使用 XML 数据填充模板文件来生成最终表单文档。
   * 生成各种格式的输出表单，包括非交互式 PDF 打印流。
   * 利用 XFA 表单 PDF 和 Adobe Acrobat 表单 (AcroForm) 生成打印版 PDF。

* **变量数据外部化程序**：您可以将 AEM Workflow 变量的数据保存在由组织管理的外部存储系统上。

您可以将电子邮件发送到 [!DNL formscsbeta@adobe.com] 以注册 Beta 项目。

### [!DNL Forms] 中修复的错误 {#forms-bugs-fixed}

* 在通过表单数据模型 (FDM) 向后端服务提交数据之前验证字段时，验证成功，但表单数据模型服务无法调用后期验证。
* 在从 Apple iOS 设备提交包含标准 HTML 上传字段的表单时，有时不会发送文件内容，而在另一端会收到一个 0 字节的文件。這是Apple iOS中的已知問題。 [FB9117687](https://feedbackassistant.apple.com/feedback/9117687)

## [!DNL Experience Manager Screens] as a [!DNL Cloud Service] {#screens}

本節概述AEM Screensas a Cloud Service的發行說明。

### 发布日期 {#release-date-june-screens}

AEM Screensas a Cloud Service的發行日期為2021年6月24日。

### 新增功能 {#what-is-new-screens-june}

>[!NOTE]
>另請參閱 [AEM Screensas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/home.html?lang=en) 成功安裝、設定和執行Screensas a Cloud Service所需的基礎知識指南，以及指向詳細概念技術檔案的連結。

* 大量裝置註冊管理表示布建大量播放器裝置更快且更有效率。

* 改善每個裝置、顯示和管道詳細目錄檢視的搜尋和篩選選項。

* 裝置運作狀況快照藉由提供一目瞭然的關鍵狀態來節省時間。

* 「物件詳細資訊」頁面提供專案中每個物件最相關資訊的摘要。

## CIF 加载项 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 內容片段的新CIF產品和類別參考資料型別(包括 產品/類別選擇器UI支援)
* 新的Commerce內容片段核心元件
* AEM後端支援全文檢索商務搜尋
* Commerce核心元件支援Adobe Commerce Sensei Recs資料收集
* 改善類別頁面的SEO易記URL
* 支援每個網站/設定的自訂HTTP標頭

## 内容转移工具 {#content-transfer-tool}

### 发布日期 {#release-date-ctt-latest}

內容轉移工具v1.5.4的發行日期為2021年6月28日。

### 新增功能 {#what-is-new-ctt-latest}

* 支援選購的 [預先複製](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) 新增以搭配CTT使用的步驟。 當來源AEM例項設定為使用Amazon S3或Azure Blob儲存體資料存放區時，預先複製步驟可用來大幅加快內容轉移活動的擷取和擷取階段。

* CTT新增了護欄，以防止使用者停止擷取，並在資料在擷取階段達到關鍵點後可能損毀資料。

* 擷取記錄檔的描述性更高，以協助疑難排解。

* 在UI中新增更多描述性擷取狀態訊息。

### 错误修复 {#bug-fixes-ctt-latest}

* 在製作執行個體上停止內嵌時，UI會覆寫發佈執行個體上先前完成的內嵌至 `STOPPED` 從 `FINISHED`. 此问题已得到修复。

## Best Practices Analyzer {#best-practices-analyzer}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer v2.1.16的發行日期為2021年6月30日。

### 新增功能 {#what-is-new-bpa-latest}

* 能夠偵測及報告下資料夾中缺少的子節點 `/content/dam`.

* 可偵測和報告所使用Best Practices Analyzer版本。

### 错误修复 {#bug-fixes-bpa-latest}

* 已修正與不支援的存放庫結構(URS)相關的記錄錯誤。
