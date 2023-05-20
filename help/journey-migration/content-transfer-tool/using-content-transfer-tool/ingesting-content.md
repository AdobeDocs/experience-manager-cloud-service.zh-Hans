---
title: 将内容提取到目标
description: 将内容提取到目标
exl-id: d8c81152-f05c-46a9-8dd6-842e5232b45e
source-git-commit: addfa18ed8fa45b1cfc17d4e35cbdde47b491507
workflow-type: tm+mt
source-wordcount: '1753'
ht-degree: 12%

---

# 将内容提取到目标 {#ingesting-content}

## 內容轉移工具中的擷取程式 {#ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion"
>title="内容引入"
>abstract="引入是指将内容从迁移集引入到目标云服务实例中。内容传输工具具备支持差异内容增补的功能，借助该功能，您可以仅传输自上次内容传输活动以来所做的更改。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html#top-up-ingestion-process" text="增补摄取"

请按照以下步骤从内容传输工具中摄取迁移集：

>[!NOTE]
>您記得為此擷取記錄支援票證嗎？ 另請參閱 [使用內容轉移工具前的重要考量](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html#important-considerations) 以及有助於成功擷取的其他考量事項。

1. 前往Cloud Acceleration Manager。 按一下您的專案卡，然後按一下「內容轉移」卡。 導覽至 **內嵌工作** 並按一下 **新內嵌**

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-01.png)

1. 檢閱擷取檢查清單，並確保已完成所有步驟。 這些是確保成功擷取的必要步驟。 您將能夠繼續前往 **下一個** 只有在檢查清單完成時才會執行此步驟。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/Ingestion-checklist.png)

1. 提供建立新內嵌所需的資訊。

   * 選取包含擷取資料的移轉集作為來源。
      * 移轉集將在長時間不活動後過期，因此預期擷取會在執行擷取後不久發生。 檢閱 [移轉集到期](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry) 以取得詳細資訊。
   * 選取目標環境。 這是將會擷取移轉集內容的位置。 選取階層。 （作者/發佈）。 不支援快速開發環境。

   >[!NOTE]
   >下列附註適用於擷取內容：
   > 如果來源是Author，建議將其擷取到目標上的Author層級。 同樣地，如果來源是Publish，則目標也應該是Publish。
   > 如果目標層為 `Author`，作者執行個體會在擷取期間關閉，且將讓使用者（例如，作者或執行維護的任何人等）無法使用。 這是為了保護系統，並防止任何可能遺失或造成內嵌衝突的變更。 請確定您的團隊知道這個事實。 另請注意，環境在作者擷取期間似乎處於休眠狀態。
   > 您可以執行選用的預先複製步驟，以大幅加快擷取階段。 請參閱 [使用AzCopy擷取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#ingesting-azcopy) 以取得更多詳細資料。
   > 如果使用預先複製擷取（用於S3或Azure資料存放區），建議先單獨執行作者擷取。 稍後執行發佈擷取時，這會加快擷取速度。
   > 內嵌不支援快速開發環境(RDE)目的地。 它們不會顯示為可能的目的地選擇，即使使用者擁有存取權。

   >[!IMPORTANT]
   > 下列重要通知適用於擷取內容：
   > 只有當您屬於本機時，才能起始內嵌至目的地環境的作業 **AEM管理員** 目的地Cloud Service作者服務上的群組。 如果您無法開始內嵌，請參閱 [無法開始內嵌](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#unable-to-start-ingestion) 以取得更多詳細資料。
   > 如果設定 **擦去** 在內嵌之前啟用，會刪除整個現有存放庫並建立新存放庫以內嵌內容。 這表示它會重設所有設定，包括目標Cloud Service執行個體的許可權。 對於新增至的管理員使用者也是如此 **管理員** 群組。 您必須重新新增至管理員群組，才能開始內嵌。

1. 按一下 **擷取**

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam22.png)

1. 然後，您可以從「內嵌工作」清單檢視中監視內嵌階段，並在內嵌進行時使用內嵌的動作功能表來檢視記錄。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23.png)

1. 按一下 **(i)** 按鈕來取得有關擷取作業的詳細資訊。 您可以按一下「 」，在執行或完成擷取時檢視每個步驟的持續時間 **...** 然後開啟 **檢視持續時間**. 擷取的資訊也會顯示出來，以瞭解正在擷取的內容。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23b.png)

<!-- Alexandru: hiding temporarily, until it's reviewed 

1. The **Migration Set ingestion** dialog box displays. Content can be ingested to either Author instance or Publish instance at a time. Select the instance to ingest content to. Click on **Ingest** to start the ingestion phase. 

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-02.png)

   >[!IMPORTANT]
   >If ingesting with pre-copy is used (for S3 or Azure Data Store), it is recommended to run Author ingestion first alone. This will speed up the Publish ingestion when it is run later. 

   >[!IMPORTANT]
   >When the **Wipe existing content on Cloud instance before ingestion** option is enabled, it deletes the entire existing repository and creates a new repository to ingest content into. This means that it resets all settings including permissions on the target Cloud Service instance. This is also true for an admin user added to the **administrators** group.

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-03.png)

   Additionally, click on **Customer Care** to log a ticket, as shown in the figure below. 

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-04.png)
   
   Also, refer to [Important Considerations for Using Content Transfer Tool](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html#important-considerations) to learn more.

1. Once the ingestion is complete, the status under **Author ingestion** updates to **FINISHED**.

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-05.png) -->

## 增补摄取 {#top-up-ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion_topup"
>title="增补摄取"
>abstract="使用增补功能移动自上次内容转移活动以来修改的内容。引入完毕后，检查日志中是否有任何错误/警告。应立即通过处理所报告的问题或联系 Adobe 客户服务而纠正任何错误。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/viewing-logs.html" text="查看日志"

内容传输工具具备支持差异内容&#x200B;*增补*&#x200B;的功能，借助该功能，您可以仅传输自上次内容传输活动以来所做的更改。

>[!NOTE]
>初始内容传输完成后，建议在云服务上线之前，经常对差异内容进行增补，以缩短最终差异内容传输的内容冻结期。如果您已使用預先複製步驟進行第一次完整擷取，您可以略過後續追加擷取的預先複製（如果追加移轉集大小小於200GB），因為這樣可能會增加整個程式的時間。

擷取程式完成後，若要擷取差異內容，您必須執行 [追加提取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process) 然後使用追加擷取方法。

您可以建立新的擷取工作來完成此操作，並確保 **擦去** 會在擷取階段期間停用，如下所示：

![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam24.png)

## 疑难解答 {#troubleshooting}

### CAM無法擷取移轉權杖 {#cam-unable-to-retrieve-the-migration-token}

自動擷取移轉權杖可能會因不同原因而失敗，包括您 [透過Cloud Manager設定IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) 在目標Cloud Service環境中。 在這種情況下，當您嘗試開始內嵌時，將會看到下列對話方塊：

![图像](/help/journey-migration/content-transfer-tool/assets-ctt/troubleshooting-token.png)

您必須按一下對話方塊上的「取得代號」連結，以手動擷取移轉代號。 這將會開啟另一個顯示權杖的標籤。 然後，您可以複製權杖並將其貼到 **移轉權杖輸入** 欄位。 現在，您應該能夠開始內嵌。

>[!NOTE]
>
>權杖將可供屬於本機的使用者使用 **AEM管理員** 目的地Cloud Service作者服務上的群組。

### 無法開始內嵌 {#unable-to-start-ingestion}

只有當您屬於本機時，才能起始內嵌至目的地環境的作業 **AEM管理員** 目的地Cloud Service作者服務上的群組。 如果您不屬於AEM管理員群組，當您嘗試開始內嵌時，將會看到如下所示的錯誤。 您可以要求管理員將您新增至本機 **AEM管理員** 或要求代號本身，然後您可將它貼到 **移轉權杖輸入** 欄位。

![图像](/help/journey-migration/content-transfer-tool/assets-ctt/error_nonadmin_ingestion.png)

### 無法連線至移轉服務 {#unable-to-reach-migration-service}

請求內嵌後，可能會向使用者顯示類似以下訊息：「目的地環境中的移轉服務目前無法連線。 請稍後再試，或聯絡Adobe支援。」

![图像](/help/journey-migration/content-transfer-tool/assets-ctt/error_cannot_reach_migser.png)

這表示Cloud Acceleration Manager無法連線到目標環境的移轉服務來開始內嵌。 發生此情況有多種原因。

>[!NOTE]
> 
> 顯示「移轉權杖」欄位，因為在少數情況下，實際上不允許擷取該權杖。 透過允許手動提供，這可讓使用者無需任何其他協助即可快速開始內嵌。 如果提供Token，但訊息仍會顯示，則擷取Token不是問題。

* AEMas a Cloud Service會維護環境狀態，偶爾可能由於一些正常原因需要重新啟動移轉服務。 如果服務正在重新啟動，則無法連線，但很快便可使用。
* 執行個體上可能正在執行另一個處理序。 例如，如果Release Orchestrator套用更新，系統可能會忙碌中，移轉服務會定期無法使用。 再加上可能會損毀中繼或生產執行個體，因此強烈建議在內嵌期間暫停更新。
* 如果 [已套用IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) 透過Cloud Manager，它會封鎖Cloud Acceleration Manager，使其無法到達移轉服務。 無法新增用於內嵌的IP位址，因為其位址非常動態。 目前，唯一的解決方案是在執行內嵌時停用IP允許清單。
* 可能有其他原因需要調查。 如果內嵌仍持續失敗，請聯絡Adobe客戶服務。

### 仍可透過Release Orchestrator自動更新

Release Orchestrator會自動套用更新，讓環境保持最新狀態。 如果在執行內嵌時觸發更新，可能會導致無法預測的結果，包括環境損毀。 這是開始內嵌前應記錄支援票證的原因之一（請參閱上述「附註」），以便可以排程暫時停用Release Orchestrator。

如果在開始內嵌時Release Orchestrator仍在執行，UI會顯示此訊息。 您仍然可以選擇繼續，接受風險，方法是檢查欄位並再次按按鈕。

>[!NOTE]
>
> Release Orchestrator現在已部署至開發環境，因此暫停更新這些環境也應完成。

![图像](/help/journey-migration/content-transfer-tool/assets-ctt/error_releaseorchestrator_ingestion.png)

### 追加擷取失敗

造成問題的常見原因 [追加擷取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) 失敗是節點id中的衝突。 若要識別此錯誤，請使用Cloud Acceleration Manager UI下載擷取記錄，並尋找類似以下的專案：

>java.lang.RuntimeException： org.apache.jackrabbit.oak.api.CommitFailedException： OakConstraint0030：違反唯一性條件約束 [jcr：uuid] 具有值a1a1a1a1-b2b2-c3c3-d4d4-e5e5e5e5e5： /some/path/jcr：content， /some/other/path/jcr：content

AEM中的每個節點都必須有唯一的uuid。 此錯誤表示正在擷取的節點具有與目標執行個體上不同路徑中已存在的節點相同的uuid。
如果在來源上的節點在擷取和後續之間移動，就可能發生這種情況 [追加提取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process).
如果目標上的節點在擷取和後續追加擷取之間移動，也可能發生這種情況。

此衝突必須手動解決。 熟悉內容的人必須決定必須刪除兩個節點中的哪一個，並牢記參考該內容的其他內容。 解決方案可能要求再次完成追加提取，而不需要違反規定的節點。

## 后续内容 {#whats-next}

完成將內容擷取至Target後，您可以檢視每個步驟（擷取和擷取）的記錄並尋找錯誤。 另請參閱 [檢視移轉集記錄](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/viewing-logs.html) 以深入瞭解。
