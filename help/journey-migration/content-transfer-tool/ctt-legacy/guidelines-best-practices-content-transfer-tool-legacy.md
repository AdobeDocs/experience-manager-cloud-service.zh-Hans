---
title: 使用內容轉移工具的准則和最佳實務（舊版）
description: 使用內容轉移工具的准則和最佳實務
hide: true
hidefromtoc: true
exl-id: 03449606-0fb4-4a9f-9abb-6b17c27a6046
source-git-commit: eadcf71aa96298383b05e61251dfeb5f345df6b9
workflow-type: tm+mt
source-wordcount: '1476'
ht-degree: 15%

---

# 使用內容轉移工具的准則和最佳實務（舊版） {#guidelines}

## 准则和最佳实践 {#best-practices}

请阅读以下章节，以了解有关使用内容传输工具的准则和最佳实践。

* 執行 [修訂清除](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html) 和 [資料存放區一致性檢查](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-16550.html?lang=zh-Hans) 於 **source** 存放庫以找出潛在問題並降低存放庫大小。

* 如果AEM雲端製作內容傳遞網路(CDN)已設定好IP允許清單，請確定來源環境IP也已新增到允許清單中。 這麼做可確保來源環境和AEM雲端環境可互相通訊。

* 使用執行內嵌 *擦去* 已啟用模式，其中將刪除目標AEM Cloud Service環境中的現有存放庫（作者或發佈），然後使用移轉集資料進行更新。 应用此模式的摄取速度比非划出模式快得多，在非划出模式下，迁移集将应用在当前内容至上。

* 内容传输活动完成后，需要在云服务环境中使用正确的项目结构，才能确保内容在云服务环境中成功呈现。

* 运行内容传输工具之前，必须确保源 AEM 实例的 `crx-quickstart` 子目录中有足够的磁盘空间。这是因为内容传输工具会创建存储库的本地副本，以便稍后将其上传到迁移集。計算所需可用磁碟空間的一般公式如下：
   `data store size + node store size * 1.5`

   * *数据存储大小*：内容传输工具使用 64 GB，即使实际数据存储更大也是如此。
   * *节点存储大小*：区段存储目录大小或 MongoDB 数据库大小。因此，对于 20 GB 的区段存储大小，所需的可用磁盘空间将为 94 GB。

* 必須在整個內容轉移活動中維護移轉集，以支援內容追加。 由於在內容轉移活動期間，一次最多可以建立並維護10個移轉集，因此建議相應地分組內容存放庫。 這麼做可確保移轉集不會用完。

## 使用內容轉移工具前的重要考量 {#important-considerations}

请阅读以下章节，以了解运行内容传输工具时的重要注意事项：

* 「內容轉移工具」的最低系統需求為AEM 6.3 +和Java™ 8。 如果您使用較舊的AEM版本，您必須將內容存放庫升級至AEM 6.5才能使用內容轉移工具。

* 必須在AEM環境中設定Java™，以便 `java` 命令可由啟動AEM的使用者執行。

* 安裝1.3.0版時，請解除安裝舊版「內容轉移工具」，因為工具的結構有重大變更。 在1.3.0中，您也應該建立移轉集，並對新的移轉集重新執行擷取和擷取。

* 內容轉移工具可與下列型別的資料存放區一起使用：檔案資料存放區、S3資料存放區、共用的S3資料存放區和Azure Blob存放區資料存放區。

* 如果您使用 *沙箱環境*，確定您的環境為最新版本且已升級至最新版本。 如果您使用的是“生产环境”**，则会自动更新。

* 若要使用「內容轉移工具」，您必須是來源執行個體的管理員使用者，且屬於本機AEM **管理員** 群組(在您要轉移內容的Cloud Service例項中)。 未獲授權的使用者無法擷取存取Token來使用「內容轉移工具」。

* 如果設定 **在內嵌之前擦除雲端例項上的現有內容** 選項已啟用，則會刪除整個現有存放庫並建立存放庫以內嵌內容。 此工作流程表示它會重設所有設定，包括目標Cloud Service執行個體的許可權。 即使管理員使用者已新增至「 」，也是如此 **管理員的** 群組。 必須將使用者重新導向至 **管理員的** 群組以擷取內容轉移工具的存取Token。

* 如果來自兩個來源的內容移動到目標上的相同路徑，則「內容轉移工具」不支援將來自多個來源的內容合併到目標Cloud Service例項中。 若要將多個來源的內容移至單一目標Cloud Service例項，您需要確保來源的內容路徑沒有重疊。

* 存取Token可在特定時段後或Cloud Service環境升級後定期到期。 如果存取權杖已過期，則無法連線至Cloud Service執行個體。 在這種情況下，您需要擷取新的存取Token。 與現有移轉集關聯的狀態圖示會變更為紅色雲端，且當您將游標停留在雲端上時會顯示訊息。

* 內容轉移工具(CTT)在將內容從來源例項轉移到目標例項之前，不會執行任何型別的內容分析。 例如，將內容擷取至發佈環境時，CTT不會區分已發佈和未發佈的內容。 移轉集中指定的任何內容都會擷取到所選的目標例項。 使用者可以將移轉集內嵌至作者執行個體或Publish執行個體，或兩者兼而有之。 將內容移動到生產執行個體時，請在來源製作執行個體上安裝CTT以將內容移動到目標製作執行個體。 同樣地，請在來源發佈執行個體上安裝CTT，以將內容移動到目標發佈執行個體。 另請參閱 [在發佈執行個體上執行內容轉移工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en#running-tool) 以取得更多詳細資料。

* 「內容轉移工具」轉移的「使用者與群組」只是內容滿足許可權所需的使用者與群組。 此 *摘取* 程式會複製整個 `/home` 移入移轉集和 *內嵌* 程式會複製已移轉內容ACL中參照的所有使用者和群組。 若要自動將現有使用者和群組對應至其IMS ID，請參閱 [使用使用者對應工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/legacy-user-mapping-tool/using-user-mapping-tool-legacy.html?lang=en).

* 在提取阶段，内容传输工具将在活动 AEM 源实例上执行。

* 完成 *摘取* 內容轉移程式階段及開始 *擷取階段* 將內容內嵌至您的AEMas a Cloud Service *階段* 或 *生產* 執行個體，記錄支援票證。 通知Adobe您打算執行 *內嵌* 以便Adobe可確保在 *內嵌* 程式。 在計畫的前一週記錄支援票證 *內嵌* 日期。 在您提交支援票證後，支援團隊會提供後續步驟的指引。 登入支援票證，並提供下列詳細資料：

   * 計劃開始的確切日期和估計時間（以您的時區表示） *內嵌* 階段。
   * 您打算將資料內嵌到的環境型別（中繼或生產）。
   * 方案ID。

* 此 *擷取階段* 對於作者，會縮小整個作者部署。 此程式表示在整段擷取程式中，無法使用製作AEM。 也請確保在您執行 *內嵌* 階段。

* 使用時 `Amazon S3` 或 `Azure` 做為來源AEM系統上的資料存放區，資料存放區應進行設定，以便無法刪除已儲存的blob （垃圾收集）。 這樣可確保索引資料的完整性，如果無法以這種方式設定，可能會導致擷取失敗，因為此索引資料缺乏完整性。

* 如果您使用自訂索引，您必須確保設定自訂索引時具有 `tika` 節點（在執行內容轉移工具之前）。 請參閱 [準備新的索引定義](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html?lang=en#preparing-the-new-index-definition) 以取得更多詳細資料。

* 如果您打算進行追加提取，請確定現有內容的內容結構從初次提取時到執行追加提取時沒有變更。 追加無法對自初始提取以來結構已變更的內容執行。 請務必在移轉程式期間限制此專案。

* 如果您打算將版本納入移轉集，並使用執行追加功能 `wipe=false`，則由於「內容轉移工具」的目前限制，您必須停用版本清除。 如果您偏好啟用版本整個清除，並且要在移轉集中執行追加作業，則必須依照以下方式執行內嵌 `wipe=true`.

## 后续内容 {#whats-next}

瞭解使用內容轉移工具的准則、最佳實務和重要考量後，您就可以開始安裝和使用工具，從建立移轉集開始。 另請參閱 [內容轉移工具快速入門](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=zh-Hans) 以深入瞭解。
