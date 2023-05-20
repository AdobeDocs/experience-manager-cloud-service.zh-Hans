---
title: 实施阶段
description: 確定您的程式碼和內容已準備好移轉至雲端
exl-id: d124f9a5-a754-4ed0-a839-f2968c7c8faa
source-git-commit: fedaa9b8a7baf707c71acd0535ad890254b6793a
workflow-type: tm+mt
source-wordcount: '2353'
ht-degree: 9%

---

# 实施阶段 {#implementation-phase}

在歷程的實作階段，您將探索可用來讓程式碼和內容準備好移至AEMas a Cloud Service的工具。

## 迄今为止的故事 {#story-so-far}

在歷程的上一部分中，您已完成 [熟悉AEMas a Cloud Service中的變更](/help/journey-migration/getting-started.md)，並判斷您的部署是否已準備好透過移至雲端。 [整備階段](/help/journey-migration/readiness.md).

本文繼續就如何使用Adobe提供的工具以確保您的程式碼和內容準備好移至雲端提供建議。

## 目标 {#objective}

本檔案旨在：

* 向您介紹Cloud Manager，AEM持續整合和傳送架構，用於部署計畫碼到AEMas a Cloud Service
* 透過內容轉移工具，讓您快速上手
* 說明為了將您的程式碼現代化，以便用於AEMas a Cloud Service而必須使用的程式碼重構工具

## 使用 Cloud Manager {#using-cloud-manager}

開始之前，您必須熟悉Cloud Manager，因為這是將程式碼部署到AEMas a Cloud Service的唯一機制。

Cloud Manager 使组织能够在云中自行管理 AEM。它包含一个持续集成和持续交付 (CI/CD) 框架，使 IT 团队和实施合作伙伴能够在不影响性能或安全性的情况下快速交付自定义或更新。

您可以參閱以下資源以熟悉使用Cloud Manager：

* [入門歷程](/help/journey-onboarding/overview.md) 瞭解有關Experience Manageras a Cloud Service入門的自助資源。

* [将 Git 与 Adobe Cloud Manager 集成](/help/implementing/cloud-manager/managing-code/integrating-with-git.md)，了解使用 Single Git 存储库来部署代码的相关信息。

* [Adobe Experience as a Cloud Service 配置](/help/security/ims-support.md#aem-configuration)，了解有关在 Admin Console 中管理产品和用户访问权限的信息。

## 使用Adobe提供的工具，讓您的內容和程式碼雲端做好準備 {#use-tools-to-make-code-and-content-cloud-ready}

轉換至Cloud Service的確切步驟取決於您所購買的系統，以及所遵循的軟體開發生命週期作法。

下圖顯示階段中涉及的主要步驟，其中涉及轉換程式碼和內容以用於AEMas a Cloud Service：

![图像](/help/journey-migration/assets/exec-image1.png)

我們將在以下章節中開始詳細說明您需要使用的工具，以便達成此目標。

## 内容迁移 {#content-migration}

若要將內容從您目前的AEM執行個體移轉至Cloud Service執行個體，您可以使用Adobe的「內容轉移工具」。

利用此工具，您可以指定要从源 AEM 实例传输到 AEM 云服务实例的所需内容子集。

內容移轉是多步驟的程式，需要規劃、追蹤以及不同團隊之間的共同作業。

如需有關工具運作方式以及我們建議您使用方式的相關完整詳細資訊，請參閱 [內容轉移工具檔案](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md).

## 代码重构 {#code-refactor}

### 為開發設定 {#set-up-for-development}

現在應該開始重構現有功能，使其與Cloud Services相容。

為了執行此操作，您需要檢視檔案，詳細說明您將需要開始重構程式碼的基本工具：


* 在規劃期間，建議您列出必須重構才能與AEMas a Cloud Service相容的區域。 您可以檢閱 [開發准則](/help/implementing/developing/introduction/development-guidelines.md) 瞭解更多有關如何重構和最佳化程式碼以進行Cloud Service的詳細資訊。
* 詳閱如何 [管理設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/configurations.html?lang=en#what-is-a-configuration) 在AEMas a Cloud Service中。
* 瞭解如何下載以下載來設定本機開發環境 [AEMAS A CLOUD SERVICESDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en)
* 最後，請熟悉 [AEMas a Cloud ServiceJava API](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html).

此外，您也可以：

* 觀看此影片以瞭解如何在本機安裝Dispatcher SDK：

   >[!VIDEO](https://video.tv.adobe.com/v/30601)

* 觀看此影片以瞭解如何設定Dispatcher SDK：

   >[!VIDEO](https://video.tv.adobe.com/v/30602)

### 心態改變 {#a-change-in-mindset}

在AEMas a Cloud Service中開發及執行程式碼時，必須要改變心態。 需要注意的是，代码必须是可复原的，尤其是在实例可能随时停止时。在云服务中运行的代码必须意识到它始终在群集中运行这一事实。这意味着始终会有多个实例在运行。

AEM Maven專案必須進行某些變更，才能與雲端相容。 AEMas a Cloud Service需要分隔 *內容* 和 *程式碼* 放入不同的套件，以部署至AEM：

* `/apps` 和 `/libs` 會視為AEM的不可變區域，因為這些區域在AEM啟動後（即執行階段）無法變更。 這包括建立、更新或刪除作業。 运行时对不可改变区域所做的任何更改尝试都将失败。

* 存放庫中的所有其他專案(例如， `/content` ， `/conf` ， `/var` ， `/home` ， `/etc` ， `/oak:index` ， `/system` ， `/tmp`)都是可變區域，這表示可在執行階段變更這些區域。

您可以參閱 [建議的封裝結構](/help/implementing/developing/introduction/aem-project-content-package-structure.md#recommended-package-structure) 說明檔案。


### 雲端移轉工具 {#cloud-migration-tools}

Adobe提供數種工具，可協助您加速某些程式碼重構任務。 瞭解這些工具及其解決的問題將降低移轉的複雜性和時間。

* [資產工作流程移轉](/help/journey-migration/moving-to-aem-assets/asset-workflow-migration-tool.md)，此工具可用來自動移轉資產處理工作流程
* [Dispatcher轉換工具](/help/journey-migration/refactoring-tools/dispatcher-transformation-utility-tools.md)，此工具會將您現有的Dispatcher設定轉換為可供AEMas a Cloud Service使用的格式。
* [Repository Modernizer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/moving/refactoring-tools/repo-modernizer.html?lang=en)，此工具會將AEM多模式專案當作輸入，並將其轉換為AEMas a Cloud Service專案
* [索引轉換器](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/moving/refactoring-tools/index-converter.html?lang=en)，此工具會將索引轉換為與AEMas a Cloud Service相容的表單
* [現代化工具](/help/journey-migration/refactoring-tools/aem-modernization-tools.md)，這是一套公用程式，可用來將舊版AEM功能轉換為AEMas a Cloud Service的現代化且受支援的功能。

AEM as a Cloud Service設定本機開發環境後，請透過參閱 [檔案](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md).

### 排程程式碼凍結 {#schedule-a-code-freeze}

若要管理您正在作用中AEM上開發的程式碼，以及轉換過程中的程式碼重構任務，我們建議您排程程式碼凍結期，直到完成Maven專案的重新建構以與AEMas a Cloud Service相容為止。

專案重新建構完成後，您可以根據此新結構繼續新的程式碼開發。 這可減少Cloud Manager管道在程式碼部署和測試期間的故障。

>[!NOTE]
>「內容轉移」和「程式碼重構」任務不必依序完成。 这些任务可以相互独立地完成。但是，需要使用正确的项目结构来确保内容在云服务环境中成功呈现。

## 代码部署和测试的最佳实践 {#best-practices}

Cloud Manager管道支援執行針對預備環境執行的測試。

遵循以下檔案中有關程式碼品質測試的最佳實務：

* [程式碼品質測試](/help/implementing/cloud-manager/code-quality-testing.md)，說明測試指令碼編寫程式的檔案，並說明建議涵蓋範圍至少50%的概念。
* [瞭解自訂程式碼品質規則](/help/implementing/cloud-manager/custom-code-quality-rules.md) 旨在說明Cloud Manager根據AEM Engineering最佳作法建立並執行的自訂程式碼品質規則。

## 準備上線 {#preparing-for-go-live}

準備來源系統以進行移轉涉及系統和AEM管理員層級的任務。 您可以先檢查「 」，確認內容存放庫是否處於維護良好的狀態， [修訂清除](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html) 和 [資料存放區垃圾收集](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/data-store-garbage-collection.html) 任務狀態。 如果您執行AEM 6.3版（因為「內容轉移工具」與6.3版以後相容），建議執行離線壓縮，然後執行資料存放區垃圾收集。

[資料一致性檢查](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/consistency-check.html) 建議在所有AEM版本中使用，以確保內容存放庫處於良好狀態，可以起始移轉活動。

需要系統管理員層級的存取權才能安裝和設定 [AZCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md)

此外，建議您檢閱任何未使用的資產、頁面、AEM專案、使用者和群組，以節省移轉時間。 請參閱 [內容存放庫健康狀況](#repository-health) 區段。

### 內容存放庫健康狀況 {#repository-health}

存取一次 [生產原地複製](#proof-of-migration) 建立後，繼續檢查存放庫的健康狀態。 如上一節所述，目標是在開始移轉之前，清理並壓縮來源上的存放庫。 此步驟可能會節省大量時間，否則會在移轉開始時用於疑難排解問題。

| 行動專案 | 重要技巧 |
|---------|----------|
| 使用者、群組和許可權 | 您需要瞭解成員資格的使用者數量、群組和複雜性。 尋找機會，以在移轉前清理來源中未使用的使用者和群組。 |
| 資產處理不完整 | 嘗試在開始移轉前完成來源系統中的資產處理，以避免移轉後AEMas a Cloud Service的潛在問題。 |
| 內容健康狀態 | 建議您在開始移轉前查詢並清除不良內容。 例如，尋找沒有原始轉譯或卡在工作流程處理中的資產或頁面。 另請參閱 [資產健康狀態](#asset-health). |

## 正在收集資料 {#gathering-data}

>[!NOTE]
> 此 [內容移轉策略和時間表](#content-strategy-and-timeline) 本節進一步詳細說明如何推斷收集的資料並建立移轉計畫。

收集資料可協助您規劃移轉活動和相關工作。 擷取和內嵌時間特別有用，因為資料點可以與移轉集的特定大小相關聯。 因此，這些資料點可外推以得出計畫：

* 花費的總時間 [摘取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md)
* 花費的總時間 [內嵌](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md)
* 追加花費的總時間 [摘取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process)
* 追加花費的總時間 [內嵌](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process)


<!-- Alexandru: hiding this for now

One more important datapoint is the amount of time it takes to complete the [user mapping](/help/journey-migration/content-transfer-tool/user-mapping-tool/overview-user-mapping-tool.md), if this is coupled with the content migration. You can take this data point into consideration for more realistic estimates, since it will be added to the overall extraction timeline and it may not be required to run it during top-ups.

-->

這些資料點也可協助您 [建立KPI](/help/journey-migration/readiness.md#establish-kpis) 和其他移轉相關工作。

### 移轉計畫 {#migration-plan}

根據您收集的資料點（請參閱上文），您可以建立可整合至巨集專案計畫的移轉計畫。 此步驟可讓所有主要利害關係人針對移轉活動進行視覺化和規劃。

下表說明典型的移轉計畫：

| 移轉反複專案 | 开始日期 | 預估結束日期 | 依赖项 | 估計持續時間（以天為單位） | 其他明細/行動專案 |
|---|---|---|---|---|---|
| PRDCLONE-AUTHOR-INITIAL-USRMAP-CSSTAGE-AUTHOR |  |  |  |  |  |
| PRDCLONE-PUBLISH-TOP-UP-CSSTAGE-AUTHOR |  |  |  |  |  |

如上表所示，遵循特定命名格式來識別移轉反複專案很有幫助，例如： **PRDCLONE** 對於來源AEM環境， **AUTHOR/PUBLISH** 針對AEMas a Cloud Service環境， **CSSTAGE-AUTHOR** AEMas a Cloud Service執行個體，依此類推。

影響移轉計畫的一些重要細節：

**所需的擷取總數**

* 特定環境中的作者和發佈擷取會視為兩個平行擷取，因為它們彼此獨立。
* 根據特定時段內存放庫成長情況追加擷取的次數。

**所需的內嵌總數**

* 請務必將此專案擷取至計畫中，因為擷取的集合可內嵌至多個Cloud Service環境中。
* 追加擷取次數。
* 將內容從來源作者移轉至Cloud Service作者例項，以及從來源發佈移轉至Cloud Service發佈是避免將所有作者內容擷取到Cloud Service發佈的最佳做法。

### 移轉追蹤器 {#migration-tracker}

您可以使用移轉追蹤器來記錄初始和追加執行的時間。 這些資料點將幫助您在最終追加之前制定現實的內容凍結要求。

追蹤器也可協助您：

* 識別與供需規劃員之間需要調整計畫或上線時間表的任何偏差
* 提供可用於所有必要通訊的真實狀態
* 規劃初始或未來的追加移轉

下表說明功能移轉追蹤器：

| 來源（環境/執行個體/URL） | 目的地（環境/執行個體/URL） | 移轉集名稱、型別（初始或追加） | 移轉集大小(MB) | 使用者對應（是/否） | 擷取持續時間（開始、結束、所用時間） | 擷取持續時間（開始、結束、花費時間） | 問題/解決方案/詳細資料 |
|---|---|---|---|---|---|---|---|
|  |  |  |  |  |  |  |  |

## 內容移轉策略和時間表 {#content-strategyand-timeline}

下節顯示可用於制定內容移轉策略和時間表的重要步驟和相關工作。

![图像](/help/journey-migration/assets/content-migration2.png)

### 彎管頭 {#fitment}

* 執行修訂清理、資料存放區垃圾收集和資料一致性檢查。 另請參閱 [準備上線](#preparing-for-go-live)
* [收集統計資料](#gathering-data) 關於AEM來源存放庫：
   * 區段存放區大小
   * 索引存放區大小
   * 頁數
   * 資產數量
   * 使用者和群組數目
* 瞭解AEM來源上是否啟用下列功能(AEMas a Cloud Service也需要)：
   * 智慧標籤
   * 相似性搜尋
   * 搜尋包含Word和PDF檔案中的文字
* 收集Best Practice Analyzer [報告](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md)
* 將匯入 [Cloud Acceleration Manager](/help/journey-migration/cloud-acceleration-manager/introduction/overview-cam.md)
   * 請檢閱自我分析建議，以確定AEMas a Cloud Service可以處理儲存需求。
* 繼續移轉計畫之前，請先建立Adobe支援票證以取得任何說明。

### 移轉證明 {#proof-of-migration}

* 要求符合以下條件的生產複製：
   * 位於相同的網路區域
   * 將提供使用者和群組等生產內容
   * 復製作者和發佈 — 若是叢集或發佈伺服器陣列，則各一個節點
* 選擇要移轉的內容子集，以便：
   * 它是所有可用內容型別的組合
   * 包含所有使用者和群組
* 包含25%的內容或最高1 TB的內容（以較少者為準）。
* 至少執行一個完整和 [追加](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) 從生產複製移轉至AEMas a Cloud Service非生產環境
* 解決任何潛在問題，例如：
   * AEM來源上的磁碟空間
   * AEM來源和AEMas a Cloud Service之間的連線
   * 任何 [內嵌相關限制](go-live.md#known-limitations).
* 記錄以下專案所花的時間： [擷取和擷取](#gathering-data)：
   * 瞭解每週新增多少內容
   * 根據移轉證明所測量的時間推算出來，建立 [移轉計畫](#migration-plan).

## 后续内容 {#what-is-next}

在您完全瞭解如何評估您的AEM安裝是否已準備好移至雲端後，當我們瞭解如何使用所需的工具讓安裝準備就緒時，您可以繼續前往 [上線階段](/help/journey-migration/go-live.md).
