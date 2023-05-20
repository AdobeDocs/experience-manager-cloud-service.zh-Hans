---
title: 內容轉移工具快速入門（舊版）
description: 内容转移工具快速入门
hide: true
hidefromtoc: true
exl-id: a6ee6996-510e-42d7-9a7c-f64732764f97
source-git-commit: 22bbf15e33ab3d5608dc01ed293bb04b07cb6c8c
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 24%

---

# 內容轉移工具快速入門（舊版） {#getting-started-content-transfer-tool}


## 可用性 {#availability}

可从软件分发门户下载 zip 文件形式的内容转移工具。您可以透過以下方式安裝套件 [封裝管理員](/help/implementing/developing/tools/package-manager.md) 在您的來源Adobe Experience Manager (AEM)例項上。 确保下载最新版本。有關最新版本的詳細資訊，請參閱 [發行說明](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/aem-cloud-changes.html?lang=zh-Hans).

>[!NOTE]
>从[软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)门户下载内容传输工具。

## 來源環境連線能力 {#source-environment-connectivity}

來源AEM執行個體可能在防火牆後面執行，而防火牆只能連線至已新增至允許清單的特定主機。 為了成功執行擷取，需要從執行AEM的執行個體存取以下端點：

* 目標AEMas a Cloud Service環境： `author-p<program_id>-e<env_id>.adobeaemcloud.com`
* Azure Blob儲存服務： `*.blob.core.windows.net`
* 使用者對應IO端點： `usermanagement.adobe.io`

若要測試與目標AEMas a Cloud Service環境的連線，請從來源執行個體的殼層發出以下cURL命令(取代 `program_id`， `environment_id`、和 `migration_token`)：

`curl -i https://author-p<program_id>-e<environment_id>.adobeaemcloud.com/api/migration/migrationSet -H "Authorization: Bearer <migration_token>"`

>[!NOTE]
>如果 `HTTP/2 200` 接收到，已成功連線到AEMas a Cloud Service。

## 运行内容传输工具 {#running-tool}

>[!VIDEO](https://video.tv.adobe.com/v/35460/?quality=12&learn=on)


请阅读以下章节，了解如何使用内容传输工具将内容迁移至 AEM as a Cloud Service （创作/发布）：

1. 選取Adobe Experience Manager並導覽至工具 — > **作業** -> **內容移轉**.

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/ctt01.png)

1. 選取 **內容轉移** 選項來源 **內容移轉** 精靈。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/ctt02.png)


1. 當您建立第一個移轉集時，將會出現下列主控台。 单击&#x200B;**创建迁移集**&#x200B;以创建新的迁移集。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/ctt03.png)

   >[!NOTE]
   >如果您有現有的移轉集，主控台將顯示現有移轉集清單及其目前狀態。


1. 填入欄位 **建立移轉集** 畫面，如下所述。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/ctt04.png)

   1. **名称**：输入迁移集的名称。
      >[!NOTE]
      >迁移集名称不允许使用特殊字符。

   1. **Cloud Service 配置**：输入目标 AEM as a Cloud Service 作者 URL。

      >[!NOTE]
      >在內容轉移活動期間，您一次最多可以建立並維護10個移轉集。
      >此外，您还必须为每个特定的环境（*暂存*、*开发*&#x200B;或&#x200B;*生产*）单独创建迁移。

   1. **访问令牌**：输入访问令牌。

      >[!NOTE]
      >您可以使用擷取存取權杖 **開啟存取權杖** 按鈕。 您需要確保您屬於目標Cloud Service執行個體中的「管理員」群組。

   1. **参数**：选择以下参数以创建迁移集：

      1. **包含版本**：根据需要选择。包含版本時，路徑 `/var/audit` 自動包含以移轉稽核事件。

         ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/ctt05.png)

         >[!NOTE]
         >如果您打算將版本納入移轉集，並使用執行追加功能 `wipe=false`，則由於「內容轉移工具」的目前限制，您必須停用版本清除。 如果您偏好啟用版本整個清除，並且要在移轉集中執行追加作業，則必須依照以下方式執行內嵌 `wipe=true`.


      1. **要包含的路径**：使用路径浏览器选择需要迁移的路径。路徑選擇器透過輸入或選取來接受輸入。

         >[!IMPORTANT]
         >创建迁移集时，以下路径受到限制：
         >* `/apps`
         >* `/libs`
         >* `/home`
         >* `/etc` (部分 `/etc` 允許在CTT中選取路徑)


1. 按一下 **儲存** 填入 **建立移轉集** 詳細資訊畫面。

1. 您將在以下連結中檢視您的移轉集： **內容轉移** 精靈，如下圖所示。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/ctt07.png)

   所有現有的移轉集都會顯示在 **內容轉移** 精靈及其目前狀態和狀態資訊。 您可能會看到下面描述的一些圖示。

   * *红色云*&#x200B;表示您无法完成提取流程。
   * A *綠色雲端* 表示您可以完成提取程式。
   * *黄色图标*&#x200B;表示您没有创建现有迁移集，而特定迁移集是由同一实例中的其他用户创建的。

1. 選取移轉集並按一下 **屬性** 以檢視或編輯移轉集屬性。 編輯屬性時，無法變更 **移轉集名稱** 或 **服務URL**.

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/ctt06.png)

### 決定移轉集大小和磁碟空間 {#migration-set-size}

建立移轉集後，強烈建議您在開始提取程式之前，對移轉集執行大小檢查。
透過對移轉集執行大小檢查，您將能夠：
* 判斷磁碟空間是否足夠 `crx-quickstart` 子目錄以成功完成擷取。
* 判斷移轉集大小是否在支援的產品限制內，並避免失敗的內容擷取。

請依照下列步驟執行大小檢查：

1. 選取移轉集並按一下 **檢查大小**.

   ![图像](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image1.png)

1. 這將會開啟 **檢查大小** 對話方塊。

   ![图像](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image2.png)

1. 按一下 **檢查大小** 以啟動程式。 然後，您會返回移轉集清單檢視，且應該會看到一則訊息，指出 **檢查大小** 執行中。

   ![图像](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image3.png)


1. 一次 **檢查大小** 程式已完成，狀態將變更為 **已完成**. 選取相同的移轉集，然後按一下 **檢查大小** 以檢視結果。

   ![图像](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image4.png)

   以下是 **檢查大小** 沒有警告的結果。

   ![图像](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image5.png)

1. 如果 **檢查大小** 結果指出磁碟空間不足和/或移轉集超過產品限制， **警告** 將顯示狀態。

![图像](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image6.png)

以下是 **檢查大小** 結果出現警告。

![图像](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image7.png)


## 后续内容 {#whats-next}

瞭解如何建立移轉集後，您現在就可以開始瞭解內容轉移工具中的擷取和擷取程式了。 在瞭解這些程式之前，您必須先檢閱 [處理大型內容存放庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) 以顯著加快內容轉移活動的擷取和擷取階段，將內容移至AEMas a Cloud Service。
