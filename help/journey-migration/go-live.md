---
title: 上线
description: 瞭解在程式碼和內容準備就緒後，如何執行移轉
exl-id: 10ec0b04-6836-4e26-9d4c-306cf743224e
source-git-commit: 30acb844ee4021b3e14011b548825c864de8903d
workflow-type: tm+mt
source-wordcount: '1727'
ht-degree: 4%

---

# 上线 {#go-live}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_prep"
>title="上线准备"
>abstract="为确保 AEM as a Cloud Service 顺利上线，您应该规划代码和内容冻结期、测试迭代、内容增补、性能测试、安全测试等。"

在歷程的這一部分，您將瞭解在程式碼和內容準備好移轉到AEMas a Cloud Service後，如何規劃和執行移轉。 此外，您將瞭解執行移轉時的最佳實務和已知限制。

## 迄今为止的故事 {#story-so-far}

在歷程的前幾個階段中：

* 您已瞭解如何在中開始移至AEMas a Cloud Service [快速入門](/help/journey-migration/getting-started.md) 頁面。
* 已判斷您的部署是否已準備好移至雲端。請閱讀 [整備階段](/help/journey-migration/readiness.md)
* 熟悉工具和流程，讓您透過 [實作階段](/help/journey-migration/implementation.md).

## 目标 {#objective}

熟悉歷程的先前步驟後，本檔案將幫助您瞭解如何執行移轉至AEMas a Cloud Service。 您將瞭解如何執行初始生產移轉，以及在移轉至AEMas a Cloud Service時遵循的最佳實務。

## 初始生產移轉 {#initial-migration}

在執行生產移轉之前，請遵循中概述的移轉步驟說明和證明 [內容移轉策略和時間表](/help/journey-migration/implementation.md##strategy-timeline) 部分 [實作階段](/help/journey-migration/implementation.md).

* 根據您在翻制上執行AEMas a Cloud Service階段移轉期間獲得的體驗，從生產環境啟動移轉：
   * Author-Author
   * Publish-Publish

* 驗證內嵌至AEMas a Cloud Service製作和發佈層級的內容。
* 指示內容製作團隊在內嵌完成前，避免同時在來源和目的地移動內容
* 可以新增、編輯或刪除新內容，但請避免移動。 這同時適用於來源和目的地。
* 記錄 [花費時間](/help/journey-migration/implementation.md#gathering-data) 完整擷取和內嵌，需要估計未來追加移轉時間表。
* 建立 [移轉規劃工具](/help/journey-migration/implementation.md#migration-plan) 適用於author和publish。

## 遞增增值 {#top-up}

從生產環境初次移轉後，您必須執行累加的追加，以確保您的內容在雲端例項上保持最新。 因此，建議您遵循下列最佳實務：

* 收集有關內容量的資料。 例如：每一週、兩週或一個月。
* 請務必避免超過48小時的內容擷取和擷取時間，藉此規劃追加費用。 建議使用此功能，讓內容追加可符合週末的時間範圍。
* 規劃所需的追加數量，並使用這些估計在上線日期進行規劃。

## 識別移轉的程式碼和內容凍結時間表 {#code-content-freeze}

如前所述，您必須排程程式碼和內容凍結期。 您可以使用下列問題來協助您計畫凍結期間：

* 我需要將內容製作活動凍結多久？
* 我應該要求我的傳送團隊停止新增功能多久？

若要回答第一個問題，您應考量在非生產環境中執行試用執行所花的時間。 若要回答第二個問題，您必須在新增功能的團隊和重構程式碼的團隊之間密切合作。 目標應該是確保新增到現有部署的所有程式碼也新增、測試並部署至雲端服務分支。 一般而言，這表示程式碼凍結的數量會較低。

此外，您還需要在排程最終追加內容時規劃內容凍結。

## 最佳实践 {#best-practices}

規劃或執行移轉時，您應考量下列准則：

* 從作者移轉至作者，再從發佈移轉至發佈
* 請求可用於下列作業的生產作業翻制：
   * 擷取儲存區域統計資料
   * 移轉活動證明
   * 準備移轉計畫
   * 識別內容凍結需求
   * 識別從生產環境執行移轉時，生產環境上的任何規模調整需求

**內容轉移工具最佳實務**

請確定上線時，您會在生產環境執行內容移轉，而非翻制。 一個好方法是使用 [AZCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) 進行初始移轉，然後經常（甚至每天）執行追加擷取，以擷取較小區塊，並避免來源AEM上的任何長期負載。

執行生產移轉時，您應該避免從複製品執行「內容轉移工具」，因為：

* 如果客戶在追加移轉期間需要移轉內容版本，則從複製執行內容轉移工具不會移轉版本。 即使經常從即時作者重新建立翻制，每次建立翻制時，「內容轉移工具」用來計算增量值的查核點也會重設。
* 由於複製無法重新整理為整體，因此必須使用ACL查詢套件來封裝和安裝從生產環境新增或編輯至複製環境的內容。 此方法的問題在於，除非從來源和翻制手動刪除，否則來源執行個體上任何已刪除的內容永遠無法進入翻制。 這可能會導致生產環境上已刪除的內容不會在翻制和AEMas a Cloud Service上刪除。

**在執行內容移轉時最佳化AEM來源的負載**

請記住，在提取階段期間，AEM來源的負載將會更大。 請留意：

* 內容轉移工具是外部Java程式，使用4 GB的JVM棧積
* 非AzCopy版本會下載二進位檔案，將其儲存在來源AEM作者的暫存空間中，消耗磁碟I/O，然後上傳到Azure容器，消耗網路頻寬
* [AzCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) 將blob直接從blob存放區傳輸至Azure容器，以儲存磁碟I/O和網路頻寬。 AzCopy版本仍會使用磁碟和網路頻寬，將資料從區段存放區擷取並上傳至Azure容器
* 內容轉移工具程式在擷取階段的系統資源上較輕，因為它只會串流擷取記錄，而且就磁碟I/O或網路頻寬而言，來源執行個體的負載並不大。

## 已知限制 {#known-limitations}

請考量，如果在擷取的移轉集中找到以下任何限制，則整個擷取會失敗：

* 名稱超過150個字元的JCR節點
* 大於16 MB的JCR節點
* 任何使用者/群組具有 `rep:AuthorizableID` 擷取已出現在AEMas a Cloud Service上的專案
* 如果任何擷取並擷取的資產在移轉的下一個反複專案之前，會移至來源或目的地的不同路徑。

## 資產健康狀態 {#asset-health}

與內嵌區段上方的區段比較 **不會** 失敗，因為有下列資產問題。 不過，強烈建議您在下列情況下採取適當的步驟：

* 遺失原始轉譯的任何資產
* 任何資料夾遺失 `jcr:content` 節點。

以上兩個專案將會在 [Best Practice Analyzer](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md) 報告。

## 上線檢查清單 {#Go-Live-Checklist}

請檢閱此活動清單，以確保您順利且成功地執行移轉。

* 執行具有功能和UI測試的端對端生產管道，以確保 **永遠最新** AEM產品體驗。 請參閱下列資源。
   * [AEM 版本更新](/help/implementing/deploying/aem-version-updates.md)
   * [自定义功能测试](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing)
   * [UI 测试](/help/implementing/cloud-manager/ui-testing.md)
* 將內容移轉至生產環境，並確保在測試時可使用相關的子集進行測試。
   * 請注意，AEM適用的DevOps最佳實務代表程式碼會從開發環境移至生產環境，而內容則會從生產環境下移。
* 排程程式碼和內容凍結期間。
   * 另請參閱區段 [移轉的程式碼和內容凍結時間表](#code-content-freeze)
* 執行最終追加內容。
* 驗證Dispatcher設定。
   * 使用本機Dispatcher驗證器，以利在本機設定、驗證和模擬Dispatcher
      * [設定本機Dispatcher工具](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html?lang=en#prerequisites)
   * 請仔細檢閱虛擬主機組態。
      * 最簡單（且預設）的解決方案是包含 `ServerAlias *` 虛擬主機檔案中的 `/dispatcher/src/conf.d/available_vhostsfolder`.
         * 這將允許產品功能測試、Dispatcher快取失效和複製使用的主機別名運作。
      * 但是，如果 `ServerAlias *` 不可接受，至少符合下列條件 `ServerAlias` 除了您的自訂網域外，還必須允許輸入專案：
         * `localhost`
         * `*.local`
         * `publish*.adobeaemcloud.net`
         * `publish*.adobeaemcloud.com`
* 設定CDN、SSL和DNS。
   * 如果您使用自己的CDN，請輸入支援票證以設定適當的路由。
      * 請參閱區段 [客戶CDN指向AEM Managed CDN](/help/implementing/dispatcher/cdn.md#point-to-point-cdn) 詳細資訊請參閱CDN檔案。
      * 您需要根據CDN供應商的檔案設定SSL和DNS。
   * 如果您未使用其他CDN，請依照以下檔案管理SSL和DNS：
      * 管理 SSL 证书
         * [管理 SSL 证书简介](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
         * [管理SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)
      * 管理自訂網域名稱(DNS)
         * 為了確保DNS轉換不會帶來非預期的問題，最好在您上線並進行一輪UAT測試之前，建立測試子網域以將您的生產執行個體連線到上。 因此，如果您的網域是example.com，您可以建立子網域test.example.com並將其套用至生產環境。 在網域的UAT測試期間，您將需要尋找適當的連結重新導向、快取和Dispatcher設定等。
         * [自定义域名简介](/help/implementing/cloud-manager/custom-domain-names/introduction.md)
         * [添加自定义域名](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)
         * [管理自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)
   * 請記得驗證DNS記錄的TTL集合。
      * TTL是在要求伺服器更新之前DNS記錄保留在快取中的時間。
      * 如果您的TTL非常高，您的DNS記錄更新將需要更長的時間才能傳播。
* 執行符合您業務需求和目標的效能和安全測試。
* 切斷，並確定實際上線是在沒有任何新部署或內容更新的情況下執行的。
* 建立Admin Console使用者通知設定檔。 另請參閱 [通知設定檔](/help/journey-onboarding/notification-profiles.md)

在執行移轉時，如果您需要重新校準工作，您可以隨時參考清單。

## 后续内容 {#what-is-next}

瞭解如何移轉至AEMas a Cloud Service後，您可以檢查 [上線後](/help/journey-migration/post-go-live.md) 頁面，讓您的執行個體順利運作。
