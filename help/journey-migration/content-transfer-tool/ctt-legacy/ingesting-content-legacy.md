---
title: 將內容擷取至Target （舊版）
description: 将内容提取到目标
hide: true
hidefromtoc: true
exl-id: 326b3e98-5055-49b5-a005-63fd3ca35202
source-git-commit: 22bbf15e33ab3d5608dc01ed293bb04b07cb6c8c
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 27%

---

# 將內容擷取至Target （舊版） {#ingesting-content}

## 內容轉移工具中的擷取程式 {#ingestion-process}

请按照以下步骤从内容传输工具中摄取迁移集：
>[!NOTE]
>您可以執行選用的預先複製步驟，以大幅加快擷取階段。 請參閱 [使用AzCopy擷取](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en#ingesting-azcopy) 以取得更多詳細資料。

1. 選取移轉集來源 **內容轉移** 頁面並按一下 **擷取** 以開始內嵌。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-01.png)

1. 此时将显示&#x200B;**迁移集摄取**&#x200B;对话框。內容一次可以內嵌到作者執行個體或發佈執行個體。 選取要擷取內容的例項。 按一下 **擷取** 以開始內嵌階段。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-02.png)

   >[!IMPORTANT]
   >如果使用預先複製擷取（用於S3或Azure資料存放區），建議先單獨執行作者擷取。 稍後執行發佈擷取時，這會加快擷取速度。

   >[!IMPORTANT]
   >當 **在內嵌之前擦除雲端例項上的現有內容** 選項已啟用，則會刪除整個現有存放庫並建立新存放庫以內嵌內容。 這表示它會重設所有設定，包括目標Cloud Service執行個體的許可權。 對於新增至的管理員使用者也是如此 **管理員** 群組。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-03.png)

   此外，按一下 **客戶服務** 以記錄票證，如下圖所示。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-04.png)

   另外，請參閱 [使用內容轉移工具的重要考量](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=en#important-considerations) 以深入瞭解。

1. 擷取一旦完成，狀態就會位於 **作者內嵌** 更新 **已完成**.

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-05.png)

## 增补摄取 {#top-up-ingestion-process}

内容传输工具具备支持差异内容&#x200B;*增补*&#x200B;的功能，借助该功能，您可以仅传输自上次内容传输活动以来所做的更改。

>[!NOTE]
>初始内容传输完成后，建议在云服务上线之前，经常对差异内容进行增补，以缩短最终差异内容传输的内容冻结期。

完成摄取流程后，可以使用增补摄取方法传输增量内容。应遵循以下步骤：

1. 導覽至 **內容轉移** 精靈並選取您要執行追加擷取的移轉集。 单击&#x200B;**摄取**&#x200B;以开始增补提取。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/topup-ingest1.png)


1. 此时将显示&#x200B;**迁移集摄取**&#x200B;对话框。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/topup-ingest2.png)

   >[!IMPORTANT]
   >您應停用 **在內嵌之前擦除雲端例項上的現有內容** 選項，以防止從先前的擷取活動中刪除現有內容。 此外，按一下 **客戶服務** 以記錄票證，如上圖所示。

## 后续内容 {#whats-next}

在內容轉移工具中學習了將內容擷取至目標後，您可以在完成每個步驟（擷取和擷取）時檢視記錄並尋找錯誤。 另請參閱 [檢視移轉集記錄](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/viewing-logs.html?lang=en) 以深入瞭解。
