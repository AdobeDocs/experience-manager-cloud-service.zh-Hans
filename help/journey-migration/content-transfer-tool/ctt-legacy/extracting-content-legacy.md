---
title: 從來源擷取內容（舊版）
description: 从源中提取内容
hide: true
hidefromtoc: true
exl-id: 9f43356c-ba51-48bc-97f5-f1f5db81e7f3
source-git-commit: 3c8035e4db5729f58bae29136a32a0b9944d6a2f
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 34%

---

# 從來源擷取內容（舊版） {#extracting-content}

## 內容轉移工具中的提取程式 {#extraction-process}

请按照以下步骤从内容传输工具中提取迁移集：
>[!NOTE]
>如果使用Amazon S3或Azure資料存放區作為資料存放區型別，您可以執行選用的預先複製步驟，以顯著加快擷取階段。 若要這麼做，您需要設定 `azcopy.config` 執行擷取之前的檔案。 請參閱 [處理大型內容存放庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) 以取得更多詳細資料。

>[!IMPORTANT]
>從來源擷取內容之前，您應該先執行使用者對應工具。 另請參閱 [使用使用者對應工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/legacy-user-mapping-tool/using-user-mapping-tool-legacy.html?lang=en) 以取得更多詳細資料。

1. 選取移轉集來源 **內容轉移** 精靈並按一下 **Extract** 以開始擷取。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-01.png)

1. 此 **移轉集擷取** 對話方塊顯示並按一下 **Extract** 以開始提取階段。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-02.png)

   >[!NOTE]
   >您可以選擇在提取階段期間覆寫預備容器。

   >[!IMPORTANT]
   >如果從來源擷取內容之前，尚未在此移轉集上執行使用者對應，您會看到顯示「使用者對應」步驟擱置的警告，如下圖所示。 選取 **對應使用者** 以執行「使用者對應」工具。
   >![图像](/help/journey-migration/content-transfer-tool/assets-ctt/user-mapping-extract.png)

1. 此 **摘取** 欄位現在顯示 **執行中** 狀態，表示擷取正在進行中。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-03.png)

   提取完成后，迁移集的状态将更新为&#x200B;**已完成**，而且&#x200B;**信息**&#x200B;字段下会显示一个&#x200B;*纯绿色*&#x200B;的云朵图标。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-04.png)

   >[!IMPORTANT]
   >UI具有自動重新載入功能，可重新載入 **內容轉移** 精靈每30秒執行一次。
   >提取阶段启动后，将创建写锁定并在 *60* 秒后将其释放。因此，如果停止提取，则需要等待一分钟以便释放锁定，之后才能再次开始提取。

## 增补提取 {#top-up-extraction-process}

内容传输工具具备支持差异内容增补的功能，借助该功能，您可以仅传输自上次内容传输活动以来所做的更改。

>[!NOTE]
>初始内容传输完成后，建议在云服务上线之前，经常对差异内容进行增补，以缩短最终差异内容传输的内容冻结期。
>此外，請確定現有內容的內容結構從初次擷取的時間到執行追加擷取的時間沒有變更。 追加無法對自初始提取以來結構已變更的內容執行。 請務必在移轉程式期間限制此專案。

完成提取流程后，可以使用增补提取方法传输增量内容。

应遵循以下步骤：

1. 導覽至 **內容轉移** 精靈並選取您要執行追加提取的移轉集。 单击&#x200B;**提取**&#x200B;以开始增补提取。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-05.png)

1. 此 **移轉集擷取** 對話方塊隨即顯示。按一下 **Extract**.

   >[!IMPORTANT]
   >您应该禁用&#x200B;**在提取期间覆盖暂存容器**选项。
   >![图像](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-06.png)


## 后续内容 {#whats-next}

在您已瞭解「內容轉移工具」中的「從來源擷取內容」後，現在已準備好在「內容轉移工具」中學習擷取程式。 另請參閱 [將內容擷取至Target](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) 以瞭解如何從「內容轉移工具」內嵌移轉集。
