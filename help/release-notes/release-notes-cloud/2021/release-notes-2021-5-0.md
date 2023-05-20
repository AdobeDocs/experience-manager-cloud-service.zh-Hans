---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.5.0 版的发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.5.0 版的发行说明。'
exl-id: 3f9d7339-7e37-4702-821e-f2b03cd7e224
source-git-commit: af5eb5aeb34e2f0ead98e0a0acb412b19bcfe517
workflow-type: tm+mt
source-wordcount: '1355'
ht-degree: 50%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明 {#release-notes}

以下部分概述了当前（最新）版本的 [!DNL Experience Manager] as a Cloud Service 的一般发行说明。

>[!NOTE]
>從這裡，您可以瀏覽至舊版的發行說明；例如，2020、2021等版本。

>[!NOTE]
>
>有关未与版本直接相关的文档更新的详细信息，请参阅[最新文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)。

## 发布日期 {#release-date}

的發行日期 [!DNL Adobe Experience Manager] as a Cloud Service2021.5.0是2021年5月27日。
下列版本(2021.6.0)將於2021年6月28日發行。

## AEMas a Cloud Service基礎 {#foundation}

### AEMas a Cloud Service基礎的新增功能 {#what-is-new-foundation}

* [發行前通道](/help/release-notes/prerelease.md)：在即將上線的功能投入生產之前，先預覽整個月！

* [API淘汰](/help/release-notes/deprecated-apis.md)：提供適用於AEMas a Cloud Service的最新已棄用API清單。

* [AEMas a Cloud ServiceSDK建置分析器Maven外掛程式](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html)：將您的Maven專案更新至最新版本，其中包括已棄用的Java API檢查和其他改進。

## [!DNL Adobe Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites] 的新增功能 {#what-is-new-sites}

* 您很快就會能夠驗證新版本的內容 [預覽階層](/help/sites-cloud/authoring/fundamentals/previewing-content.md) 以模擬最終的體驗外觀，如同您在發佈層級上一樣。 這可由AEM Sites Managed Publication精靈啟用，現在可讓您在發佈或預覽之間選擇發佈目的地。 接著，您就可以透過專用的URL存取預覽體驗。 在「預覽」上進行驗證後，內容可以照常從「作者」發佈到「發佈」。 在AEMas a Cloud Service環境中啟用預覽服務將在未來幾週逐步推出。

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 的新增功能 {#what-is-new-assets}

* 您可以使用「連結共用」功能下載共用的資產。 此下載現在使用非同步服務，提供更快速且無中斷的下載，即使對於非常大型的下載亦然。 另請參閱 [下載資產](/help/assets/download-assets-from-aem.md#link-share-download).

   ![下載收件匣](/help/assets/assets/download-inbox.png)

### 發行前管道中可用的新功能 {#what-is-new-assets-prerelease}

* 中繼資料結構描述可直接套用至資料夾屬性。

   ![從資料夾屬性新增中繼資料結構](/help/assets/assets/metadata-schema-folder-properties.png)

* 資產大量擷取工具可讓您在大量擷取期間新增中繼資料。

* 使用者體驗增強功能會顯示資料夾中存在的資產數量。 若資料夾中有超過1000個資產， [!DNL Assets] 顯示1000+。

   ![介面中顯示的資料夾資產數量](/help/assets/assets/browse-folder-number-of-assets.png)

### [!DNL Assets] 中修复的错误 {#assets-bugs-fixed}

* 上傳超大型檔案會當機 [!DNL Experience Manager desktop app]. (CQ-4320942)
* 當從資料夾中選取相同的集合時，以及當從搜尋結果中選取集合時，工具列選項會不同。 (CQ-4321406)

#### Dynamic Media的新功能 {#what-is-new-dm}

* 智慧型影像DPR （裝置畫素比）和網路頻寬最佳化可讓您在具有高解析度顯示器且網路頻寬受限的裝置上，有效率地提供最佳品質影像。 如需詳細資訊，請參閱 [智慧型影像常見問題集](/help/assets/dynamic-media/imaging-faq.md) 和 [使用新一代影像格式WebP和AVIF進行影像最佳化。](https://medium.com/adobetech/image-optimisation-with-next-gen-image-formats-webp-and-avif-248c75afacc4)
* 在Dynamic Media傳送中推出對新一代影像格式AVIF的支援（fmt URL修飾元）。

## [!DNL Adobe Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 的新增功能 {#what-is-new-forms}

* **上下文帮助**：添加了自适应表单编辑器、模板编辑器和主题编辑器的上下文帮助，以帮助作者更好地了解各编辑器的各种功能。
* **属性浏览器中的错误消息**：在自适应表单属性浏览器中为每个属性添加了错误消息。这些消息有助于了解字段的允许值。

### 即将推出的 [!DNL Forms] Beta 版功能 {#what-is-new-forms-prerelease}

Output as a Cloud Service：Output 服务可帮助您组合 XDP 模板和 XML 数据以生成各种格式的打印文档。该服务允许您以同步和异步批处理模式生成文档。Output 服务使您能够创建应用程序，这些应用程序允许您：

* 使用 XML 数据填充模板文件来生成最终表单文档。
* 生成各种格式的输出表单，包括非交互式 PDF 打印流。
* 从 XFA 表单 PDF 生成打印 PDF。

您可以将电子邮件发送到 formscsbeta@adobe.com 以注册 Beta 项目。

### [!DNL Forms] 中修复的错误 {#forms-bugs-fixed}

* 在 AEM Forms Workflows 的“分配任务”步骤中，当您将操作按钮的默认图标替换为珊瑚色图标时，工作流将停止工作并记录异常。使用默认图标时，工作流按预期执行。
* 在版面层中，当您更改列数、打开编辑层并在面板中拖动某些组件时，自适应表单编辑器的内容区域中会开始显示蓝色方形框，并且编辑器将变得无响应。
* 与提供自适应或外部资产的 URL 相关的规则编辑器选项的错误消息太长，并且对用户不友好。


## Cloud Manager {#cloud-manager}

此部分概述了 AEM as a Cloud Service 2021.5.0 中的 Cloud Manager 的发行说明。

### 发布日期 {#release-date-cm-may}

AEM as a Cloud Service 2021.5.0 中的 Cloud Manager 的发布日期是 2021 年 5 月 6 日。下一个版本计划于 2021 年 6 月 03 日发布。

### 新增功能 {#what-is-new-may}

* PackageOverlaps 质量规则现在可检测多次部署同一个包的情况；即在同一个部署的包集中部署在多个嵌入位置。

* 公共 API 中的存储库端点现在包括 Git URL。

* Cloud Manager 用户下载的部署日志将更具实用价值，现在其中包括关于失败和成功情况的详细信息。

* 现已解决将代码推送到 Adobe git 时遇到的间歇性故障。

* 现在可在“编辑程序”工作流程中将商业加载项应用于沙盒程序。

* 已更新编辑程序体验。

* “环境详情”页面中的“域名”表将通过分页的方式显示最多 250 个域名。

* 「新增計畫」和「編輯計畫」工作流程中的「解決方案」索引標籤將顯示解決方案，即使該計畫只有一個解決方案可用。

* 当构建未生成任何部署的内容包时构建步骤日志中的错误消息不明确。

### 错误修复 {#bug-fixes-cm-may}

* 有时，即使未部署配置，用户也会在 IP 允许列表旁边看到绿色的“活动”状态。

* 管道变量 API 不会移除“已删除”变量，而只会将其标记为&#x200B;**已删除**&#x200B;状态。

* 一些代码气味类型的质量问题错误地影响了可靠性评级。

* 由于不支持通配符域，UI 将禁止用户提交通配符域名。

* 当管道执行在 UTC 午夜至凌晨 1 点之间启动时，Cloud Manager 生成的工件版本不能保证大于前一天创建的版本。

* 在沙盒程序设置过程中，一旦成功创建了带有示例代码的项目，“管理 Git”将作为主信息卡中的链接出现在”概述“页面中。

## 内容转移工具 {#content-transfer-tool}

### 发布日期 {#release-date-ctt-latest}

內容轉移工具v1.4.6的發行日期為2021年5月27日。

### 新增功能 {#what-is-new-ctt-latest}

* 如果使用者沒有Java可執行檔的執行許可權，則會將新的記錄陳述式新增至快速入門的錯誤記錄檔。

* 當使用者從執行擷取的CTT UI刪除移轉集時， `tmp` 將會刪除與該移轉集相關聯的資料夾以節省空間。

### 错误修复 {#bug-fixes-ctt-latest}

* 刪除移轉集時，CTT UI中偶爾會顯示無用的錯誤訊息。 此问题已得到修复。

* 執行使用者對應時，如果使用者在目標與主機上擁有相同的電子郵件地址，但使用者名稱不同，則整個擷取作業將會失敗。 此问题已得到修复。在此衝突情況下，使用者/群組會被略過，並在記錄檔中記錄為衝突。

### 发布日期 {#release-date-ctt}

內容轉移工具v1.4.0的發行日期為2021年5月11日。

### 新增功能 {#what-is-new-ctt-may}

* 此版本的「內容轉移工具」會為移轉至Cloud Service的資產建立文字轉譯。 需要文字轉譯才能支援對所擷取的資產進行全文搜尋。
* 使用者可建立的內容轉移工具移轉集數量上限已從4個增加到10個。

### 错误修复 {#bug-fixes-ctt-may}

* 與「內容轉移工具」UI中的自動重新整理功能相關的多項錯誤修正。
* 內容轉移工具，搭配 `wipe=true` 導致目標上的計數器索引不正確。 此问题已得到修复。

## Commerce附加元件 {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 產品主控台屬性中的相關內容支援分頁

### 错误修复 {#bug-fixes-commerce}

* 資產縮圖未顯示在產品屬性的「資產」標籤中

* 階層連結會在產品主控台中重設預覽資料
