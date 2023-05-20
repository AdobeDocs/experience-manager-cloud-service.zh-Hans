---
title: 將您的數位資產新增至 [!DNL Adobe Experience Manager].
description: 將您的數位資產新增至 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service].
feature: Asset Management,Upload
role: User,Admin
exl-id: 0e624245-f52e-4082-be21-13cc29869b64
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '3094'
ht-degree: 2%

---

# 新增數位資產至 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] [!DNL Assets] {#add-assets-to-experience-manager}

[!DNL Adobe Experience Manager Assets] 接受來自許多來源的多種數位資產。 它會儲存二進位檔和已建立的轉譯，並使用各種工作流程執行資產處理，以及 [!DNL Adobe Sensei] 服務，可跨許多介面透過許多管道進行分送。

[!DNL Adobe Experience Manager] 使用豐富的中繼資料、智慧標籤、轉譯和其他數位資產管理(DAM)服務，豐富上傳數位檔案的二進位內容。 您可以從本機資料夾或網路磁碟機將各種型別的檔案（例如影像、檔案和原始影像檔案）上傳到 [!DNL Experience Manager Assets].

除了最常用的瀏覽器上傳外，將資產新增至的其他方法也會 [!DNL Experience Manager] 存放庫存在，包括案頭使用者端，例如Adobe資產連結或 [!DNL Experience Manager] 案頭應用程式、上傳和客戶建立的內嵌指令碼，以及新增為的自動化內嵌整合 [!DNL Experience Manager] 擴充功能。

雖然您可以上傳和管理任何二進位檔案，但 [!DNL Experience Manager]，最常用的檔案格式支援其他服務，例如中繼資料擷取或預覽/轉譯產生。 請參閱 [支援的檔案格式](file-format-support.md) 以取得詳細資訊。

您也可以選擇對上傳的資產完成其他處理。 您可以在上傳資產的資料夾上設定許多資產處理設定檔，以新增特定中繼資料、轉譯或影像處理服務。 另請參閱 [上傳時處理資產](#process-when-uploaded).

[!DNL Assets] 提供下列上傳方法。 Adobe建議您先瞭解上傳選項的使用案例及適用性，然後再使用上傳選項。

| 上傳方法 | 何时使用? | 主要角色 |
|---------------------|----------------|-----------------|
| [Assets Console使用者介面](#upload-assets) | 偶爾上傳、輕鬆按壓和拖曳、尋找上傳。 請勿使用上傳大量資產。 | 所有使用者 |
| [上傳API](#upload-using-apis) | 適用於上傳期間的動態決策。 | 开发人员 |
| [[!DNL Experience Manager] 桌面应用程序](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) | 低流量資產擷取，但不適用於移轉。 | 管理員、行銷人員 |
| [[!DNL Adobe Asset Link]](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/adobe-asset-link.ug.html) | 當創意人員與行銷人員從支援內處理資產時相當實用 [!DNL Creative Cloud] 案頭應用程式。 | 創意人員、行銷人員 |
| [資產大量擷取器](#asset-bulk-ingestor) | 建議用於大規模移轉和偶爾的大量擷取。 僅適用於支援的資料存放區。 | 管理員、開發人員 |

## 上传资源 {#upload-assets}

<!-- #ENGCHECK do we support pausing? I couldn't get pause to show with 1.5GB upload.... If not, this should be removed#

   You can pause the uploading of large assets (greater than 500 MB) and resume it later from the same page. Tap the **[!UICONTROL Pause]** icon beside progress bar that appears when an upload starts.

   The size above which an asset is considered a large asset is configurable. For example, you can configure the system to consider assets above 1000 MB (instead of 500 MB) as large assets. In this case, **[!UICONTROL Pause]** appears on the progress bar when assets of size greater than 1000 MB are uploaded.

   The [!UICONTROL Pause] option does not show if a file greater than 1000 MB is uploaded with a file less than 1000 MB. However, if you cancel the less than 1000 MB file upload, the **[!UICONTROL Pause]** option appears.

   To modify the size limit, configure the `chunkUploadMinFileSize` property of the `fileupload` node in the CRX repository.

   When you click the **[!UICONTROL Pause]** icon, it toggles to a **[!UICONTROL Play]** icon. To resume uploading, click **[!UICONTROL Play]** option.
-->

<!-- #ENGCHECK do we support pausing? I couldn't get pause to show with 1.5GB upload.... If not, this should be removed#
   The ability to resume uploading is especially helpful in low-bandwidth scenarios and network glitches, where it takes a long time to upload a large asset. You can pause the upload operation and continue later when the situation improves. When you resume, uploading starts from the point where you paused it.
-->

<!-- #ENGCHECK assuming this is not relevant? remove after confirming#
   During the upload operation, [!DNL Experience Manager] saves the portions of the asset being uploaded as chunks of data in the CRX repository. When the upload completes, [!DNL Experience Manager] consolidates these chunks into a single block of data in the repository.

   To configure the cleanup task for the unfinished chunk upload jobs, go to `https://[aem_server]:[port]/system/console/configMgr/org.apache.sling.servlets.post.impl.helper.ChunkCleanUpTask`.
-->

若要上傳檔案（或多個檔案），您可以在案頭上選取檔案，然後在使用者介面（網頁瀏覽器）上拖曳至目的地資料夾。 或者，您也可以從使用者介面起始上傳作業。

1. 在 [!DNL Assets] 使用者介面，導覽至您要新增數位資產的位置。
1. 若要上傳資產，請執行下列任一項作業：

   * 在工具列上，按一下 **[!UICONTROL 建立]** > **[!UICONTROL 檔案]**. 如有需要，您可以在顯示的對話方塊中重新命名檔案。
   * 在支援HTML5的瀏覽器中，將資產直接拖曳至 [!DNL Assets] 使用者介面。 不會顯示重新命名檔案的對話方塊。

   ![create_menu](assets/create_menu.png)

   若要選取多個檔案，請選取 `Ctrl` 或 `Command` 鍵，並在「檔案選擇器」對話方塊中選取資產。 使用iPad時，您一次只能選取一個檔案。

1. 若要取消進行中的上傳，請按一下關閉(`X`)。 當您取消上傳作業時， [!DNL Assets] 刪除資產中部分上傳的部分。
如果您在上傳檔案之前取消上傳操作， [!DNL Assets] 停止上傳目前的檔案並重新整理內容。 不過，不會刪除已上傳的檔案。

1. 中的上傳進度對話方塊 [!DNL Assets] 顯示成功上傳的檔案數和無法上傳的檔案數。
此外， [!DNL Assets] 使用者介面會顯示您上傳的最新資產或您先建立的資料夾。

>[!NOTE]
>
>若要上傳巢狀資料夾階層，請參閱 [大量上傳資產](#bulk-upload).

<!-- #ENGCHECK I'm assuming this is no longer relevant.... If yes, this should be removed#

### Serial uploads {#serialuploads}

Uploading numerous assets in bulk consumes significant I/O resources, which may adversely impact the performance of [!DNL Assets]. In particular, if you have a slow internet connection, the time to upload drastically increases due to a spike in disk I/O. Moreover, your web browser may introduce additional restrictions to the number of POST requests [!DNL Assets] can handle for concurrent asset uploads. As a result, the upload operation fails or terminate prematurely. In other words, [!DNL Assets] may miss some files while ingesting a bunch of files or altogether fail to ingest any file.

To overcome this situation, [!DNL Assets] ingests one asset at a time (serial upload) during a bulk upload operation, instead of the concurrently ingesting all the assets.

Serial uploading of assets is enabled by default. To disable the feature and allow concurrent uploading, overlay the `fileupload` node in CRX-DE and set the value of the `parallelUploads` property to `true`.

### Streamed uploads {#streamed-uploads}

If you upload many assets to [!DNL Experience Manager], the I/O requests to server increase drastically, which reduces the upload efficiency and can even cause some upload task to time out. [!DNL Assets] supports streamed uploading of assets. Streamed uploading reduces the disk I/O during the upload operation by avoiding asset storage in a temporary folder on the server before copying it to the repository. Instead, the data is transferred directly to the repository. This way, the time to upload large assets and the possibility of timeouts is reduced. Streamed upload is enabled by default in [!DNL Assets].

>[!NOTE]
>
>Streaming upload is disabled for [!DNL Experience Manager] running on JEE server with servlet-api version lower than 3.1.
-->

### 資產已存在時處理上傳 {#handling-upload-existing-file}

您可以上傳與現有資產具有相同路徑（相同名稱和相同位置）的資產。 不過，會顯示警告對話方塊，其中包含下列選項：

* 取代現有資產：如果您取代現有資產，資產的中繼資料以及您先前對現有資產所做的任何修改（例如註解、裁切等）都會被刪除。

   >[!NOTE]
   >
   >如果資產已鎖定或出庫，則無法取得取代資產的選項。

* 建立其他版本：在存放庫中建立現有資產的新版本。 您可以在下列位置檢視這兩個版本： [!UICONTROL 時間表] 如有必要，和可以還原成先前的現有版本。
* 保留兩者：如果您選擇保留兩個資產，則新資產會重新命名。

若要在中保留重複資產 [!DNL Assets]，按一下 **[!UICONTROL 保留]**. 若要刪除您上傳的重複資產，請按一下 **[!UICONTROL 刪除]**.

### 檔案名稱處理和禁止使用的字元 {#filename-handling}

[!DNL Experience Manager Assets] 可防止您上傳其檔案名稱中包含禁止字元的資產。 如果您嘗試上傳檔案名稱包含不允許的字元以上的資產， [!DNL Assets] 顯示警告訊息並停止上傳，直到您移除這些字元或使用允許名稱上傳為止。

為了配合您組織的特定檔案命名慣例， [!UICONTROL 上傳資產] 對話方塊可讓您為上傳的檔案指定長名稱。 不支援下列（以空格分隔的）字元清單：

* 資產名稱的字元無效： `* / : [ \\ ] | # % { } ? &`
* 資產資料夾名稱的字元無效： `* / : [ \\ ] | # % { } ? \" . ^ ; + & \t`

## 大量上傳資產 {#bulk-upload}

大量資產擷取器可以有效地處理非常大量的資產。 不過，大規模內嵌並不僅僅是廣泛的檔案傾印或隨意移轉。 若要讓大規模內嵌成為符合您業務目的且有效率的有意義專案，請規劃移轉並組織資產組織。 所有內嵌都不同，因此不是歸納總結，而是將細微的存放庫構成和業務需求納入考量。 以下是一些規劃和執行大量擷取的總體建議：

* 組織資產：移除DAM中不需要的資產。 請考慮移除未使用、過時或重複的資產。 如此一來，即可減少傳輸資料和擷取的資產，進而加快擷取速度。
* 組織資產：請考慮以某種邏輯順序組織內容，例如檔案大小、檔案格式、使用案例或優先順序。 一般而言，大型複雜檔案需要更多處理。 您也可以考慮使用檔案大小篩選選項（如下所述）個別擷取大型檔案。
* 交錯擷取：請考慮將擷取分割為多個大量擷取專案。 這可讓您更快看到內容，並視需要更新您的內嵌。 例如，您可在非尖峰時間擷取處理密集的資產，或逐步在多個區塊中擷取這些資產。 不過，您可以一次擷取不需要太多處理的較小且較簡單的資產。

若要上傳大量檔案，請使用下列其中一種方法。 另請參閱 [使用案例和方法](#upload-methods-comparison)

* [資產上傳API](developer-reference-material-apis.md#asset-upload)：如有必要，請使用自訂上傳指令碼或工具，利用API新增資產的額外處理（例如，翻譯中繼資料或重新命名檔案）。
* [[!DNL Experience Manager] 案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)：對於從本機檔案系統上傳資產的創意專業人員和行銷人員非常有用。 用它來上傳本機可用的巢狀資料夾。
* [大量擷取工具](#asset-bulk-ingestor)：用於在部署時偶爾或最初擷取大量資產 [!DNL Experience Manager].

### 資產大量匯入工具 {#asset-bulk-ingestor}

此工具僅提供給管理員群組，用於從Azure或S3資料存放區大規模擷取資產。 觀看設定和擷取的影片逐步解說。

>[!VIDEO](https://video.tv.adobe.com/v/329680/?quality=12&learn=on)

下圖說明從資料存放區擷取資產以Experience Manager時的各個階段：

![大量擷取工具](assets/bulk-ingestion.png)

**前提条件**

使用此功能需要來自Azure或AWS的外部儲存體帳戶或貯體。

>[!NOTE]
>
>將儲存體帳戶容器或貯體建立為私人，並僅接受來自授權請求的連線。 但是，不支援對輸入網路連線的其他限制。

>[!NOTE]
>
>外部儲存體帳戶的檔案/資料夾名稱規則可能與「大量匯入」工具不同。 另請參閱 [在大量匯入期間處理檔案名稱](#filename-handling-bulkimport) 瞭解更多有關不允許/逸出名稱的詳細資訊。


### 設定大量匯入工具 {#configure-bulk-ingestor-tool}

若要設定「大量匯入」工具，請遵循下列步驟：

1. 導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 大量匯入]**. 選取 **[!UICONTROL 建立]** 選項。

1. 在中指定大量匯入設定的標題 **[!UICONTROL 標題]** 欄位。

1. 從中選擇資料來源型別 **[!UICONTROL 匯入來源]** 下拉式清單。

1. 提供值以建立與資料來源的連線。 例如，如果您選取 **Azure Blob儲存體** 做為資料來源，請指定Azure儲存體帳戶、Azure blob容器和Azure存取金鑰的值。

1. 從下拉式清單中選取所需的驗證模式。 **Azure存取金鑰** 提供對Azure儲存體帳戶的完整存取，而 **Azure SAS權杖** 可讓管理員使用許可權和到期原則來限制Token的功能。

1. 提供在的資料來源中包含資產的根資料夾名稱 **[!UICONTROL 來源資料夾]** 欄位。

1. （可選）提供資產的最小檔案大小（以MB為單位），以將其納入的擷取程式中 **[!UICONTROL 按最小大小篩選]** 欄位。

1. （可選）提供資產檔案大小上限（以MB為單位），以將其納入的擷取程式中 **[!UICONTROL 按最大大小篩選]** 欄位。

1. （選用）指定要從的擷取中排除的MIME型別清單（以逗號分隔）。 **[!UICONTROL 排除MIME型別]** 欄位。 例如， `image/jpeg, image/.*, video/mp4`. 另請參閱 [所有支援的檔案格式](/help/assets/file-format-support.md).

1. 指定要包含在內嵌專案中的MIME型別清單（以逗號分隔） **[!UICONTROL 包含MIME型別]** 欄位。 另請參閱 [所有支援的檔案格式](/help/assets/file-format-support.md).

1. 選取 **[!UICONTROL 匯入後刪除來源檔案]** 在檔案匯入到之後從來源資料存放區中刪除原始檔案的選項 [!DNL Experience Manager].

1. 選取 **[!UICONTROL 匯入模式]**. 選取 **略過**， **Replace**，或 **建立版本**. 略過模式為預設值，在此模式中，如果資產已存在，擷取器會略過以匯入資產。 瞭解 [取代和建立版本選項](#handling-upload-existing-file).

1. 指定路徑，以定義DAM中要使用 **[!UICONTROL 資產目標資料夾]** 欄位。 例如：`/content/dam/imported_assets`。

1. （選用）指定要匯入的中繼資料檔案（以CSV格式提供），位於 **[!UICONTROL 中繼資料檔案]** 欄位。 在來源blob位置中指定CSV檔案，並在設定「大量匯入」工具時參照路徑。 此欄位中參考的CSV檔案格式與您在以下情況下的CSV檔案格式相同： [大量匯入和匯出資產中繼資料](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/metadata-import-export.html). 如果您選取 **匯入後刪除來源檔案** 選項，使用 **排除** 或 **包含MIME型別** 或 **依路徑/檔案篩選** 欄位。 您可以使用規則運算式來篩選這些欄位中的CSV檔案。

1. 按一下 **[!UICONTROL 儲存]** 以儲存設定。

### 管理大量匯入工具設定 {#manage-bulk-import-configuration}

建立「大量匯入」工具組態後，您可以先執行工作以評估組態，然後再將資產大量擷取到Experience Manager執行個體。 選取以下位置可用的設定： **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 大量匯入]** 以檢視管理「大量匯入」工具組態的可用選項。

### 編輯設定 {#edit-configuration}

選取設定並按一下 **[!UICONTROL 編輯]** 以修改組態詳細資訊。 執行編輯操作時，您無法編輯設定和匯入資料來源的標題。

### 刪除設定 {#delete-configuration}

選取設定並按一下 **[!UICONTROL 刪除]** 刪除大量匯入組態。

### 驗證與資料來源的連線 {#validate-connection}

選取設定並按一下 **[!UICONTROL check]** 驗證與資料來源的連線。 如果連線成功，Experience Manager會顯示下列訊息：

![大量匯入成功訊息](assets/bulk-import-success-message.png)

### 為大量匯入工作叫用測試回合 {#invoke-test-run-bulk-import}

選取設定並按一下 **[!UICONTROL 練習]** 以叫用大量匯入工作的測試回合。 Experience Manager會顯示下列有關「大量匯入」工作的詳細資訊：

![练习结果](assets/dry-assets-result.png)

### 在大量匯入期間處理檔案名稱 {#filename-handling-bulkimport}

大量匯入資產或資料夾時， [!DNL Experience Manager Assets] 匯入匯入來源中存在的完整結構。 [!DNL Experience Manager] 會遵循資產和檔案夾名稱中特殊字元的內建規則，因此這些檔案名稱需要整理。 對於資料夾名稱和資產名稱，使用者定義的標題保持不變，並儲存在 `jcr:title`.

大量匯入期間， [!DNL Experience Manager] 尋找現有資料夾以避免重新匯入資產和資料夾，同時也驗證匯入發生的父資料夾中套用的清理規則。 如果清除規則套用至父資料夾，則相同的規則套用至匯入來源。 對於新的匯入，會套用以下清理規則來管理資產和資料夾的檔案名稱。

**大量匯入中不允許的名稱**

檔案和資料夾名稱中不允許下列字元：

* 控制與私人使用字元（0x00到0x1F、\u0081、\uE000）
* 以點(.)結尾的檔案或資料夾名稱

在匯入程式期間，會略過名稱符合這些條件的檔案或資料夾，並標示為失敗。

**處理大量匯入的資產名稱**

對於資產檔案名稱，會使用API來清除JCR名稱和路徑： `JcrUtil.escapeIllegalJcrChars`.

* Unicode字元不會變更
* 將特殊字元取代為其URL逸出代碼，例如， `new%asset.png` 已更新至 `new%25asset.png`：

   ```
                   URL escape code   
   
   "               %22
   %               %25
   '               %27
   *               %2A
   /               %2F
   :               %3A
   [               %5B
   \n              %0A
   \r              %0D
   \t              %09
   ]               %5D
   |               %7C
   ```

**處理大量匯入中的資料夾名稱**

針對資料夾檔案名稱，會使用API來清除JCR名稱和路徑： `DamUtil.getSanitizedFolderName`.

* 大寫字元轉換為小寫
* Unicode字元不會變更
* 以破折號(&#39;-&#39;)取代特殊字元，例如， `new folder` 已更新至 `new-folder`：

   ```
   "                           
   #                         
   %                           
   &                          
   *                           
   +                          
   .                           
   :                           
   ;                          
   ?                          
   [                           
   ]                           
   ^                         
   {                         
   }                         
   |                           
   /         It is used for split folder in cloud storage and is pre-handled, no conversion here.
   \         Not allowed in Azure, allowed in AWS.
   \t
   space     It is the space character.
   ```

<!-- 
[!DNL Experience Manager Assets] manages the forbidden characters in the filenames while you upload assets or folders. [!DNL Experience Manager] updates only the node names in the DAM repository. However, the `title` of the asset or folder remains unchanged.

Following are the file naming conventions that are applied while uploading assets or folders in [!DNL Experience Manager Assets]:

| Characters &Dagger; | When occurring in file names | When occurring in folder names | Example |
|---|---|---|---|
| `. / : [ ] | *` | Replaced with `-` (hyphen). | Replaced with `-` (hyphen). A `.` (dot) in the filename extension is retained as is. | Replaced with `-` (hyphen). | `myimage.jpg` remains as is and `my.image.jpg` changes to `my-image.jpg`. |
| `% ; # , + ? ^ { } "` and whitespaces | Whitespaces are retained | Replaced with `-` (hyphen). | `My Folder.` changes to `my-folder-`. |
| `# % { } ? & .` | Replaced with `-` (hyphen). | NA. | `#My New File.` changes to `-My New File-`. |
| Uppercase characters | Casing is retained as is. | Changed to lowercase characters. | `My New Folder` changes to `my-new-folder`. |
| Lppercase characters | Casing is retained as is. | Casing is retained as is. | NA. |

&Dagger; The list of characters is a whitespace-separated list.
-->

#### 排程一次性或循環的大量匯入 {#schedule-bulk-import}

若要排程一次性或循環的大量匯入，請執行下列步驟：

1. 建立大量匯入設定。
1. 選取設定並選取 **[!UICONTROL 排程]** （從工具列）。
1. 設定一次性擷取或排程為每小時、每天或每週排程。 按一下 **[!UICONTROL 提交]**.

   ![排程大量擷取器工作](assets/bulk-ingest-schedule1.png)


#### 檢視Assets目標資料夾 {#view-assets-target-folder}

選取設定並按一下 **[!UICONTROL 檢視資產]** 以檢視資產目標位置，即執行大量匯入工作後匯入資產的位置。

#### 執行大量匯入工具 {#run-bulk-import-tool}

晚於 [設定大量匯入工具](#configure-bulk-ingestor-tool) 和（可選） [管理大量匯入工具組態](#manage-bulk-import-configuration)，即可執行設定工作以開始大量擷取資產。

導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 大量匯入]**，選取 [大量匯入設定](#configure-bulk-ingestor-tool) 並按一下 **[!UICONTROL 執行]** 以啟動大量匯入程式。 按一下 **[!UICONTROL 執行]** 再次確認。

Experience Manager會將工作的狀態更新至 **處理中** 和 **已成功** 成功完成工作後。 按一下 **檢視資產** 以檢視以Experience Manager匯入的資產。

當工作進行中時，您也可以選取設定並按一下 **停止** 以停止大量擷取程式。 按一下 **執行** 以繼續此程式。 您也可以按一下 **練習** 以瞭解仍在等候匯入的資產詳細資訊。

#### 管理執行後的工作 {#manage-jobs-after-execution}

「Experience Manager」可讓您檢視大量匯入工作的歷史記錄。 工作歷史記錄包含工作狀態、工作建立者、記錄以及其他詳細資訊，例如開始日期和時間、建立日期和時間，以及完成日期和時間。

若要存取組態的工作記錄，請選取組態並按一下 **[!UICONTROL 工作歷史記錄]**. 選取工作並按一下 **開啟**.

![排程大量擷取器工作](assets/job-history-bulk-import.png)

Experience Manager會顯示工作歷史記錄。 您也可以在「大量匯入工作歷史記錄」頁面按一下 **刪除** 刪除大量匯入組態的工作。


## 使用案頭使用者端上傳資產 {#upload-assets-desktop-clients}

除了網頁瀏覽器使用者介面， [!DNL Experience Manager] 支援案頭上的其他使用者端。 它們也提供上傳體驗，而不需要前往網頁瀏覽器。

* [[!DNL Adobe Asset Link]](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html) 提供資產存取許可權，從 [!DNL Experience Manager] 在Adobe Photoshop、Adobe Illustrator和Adobe InDesign案頭應用程式中。 您可以將目前開啟的檔案上傳至 [!DNL Experience Manager] 直接從這些案頭應用程式中的Adobe Asset Link使用者介面。
* [[!DNL Experience Manager] 案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) 可簡化在案頭上使用資產的流程，不受其檔案型別或處理資產的原生應用程式影響。 從本機檔案系統上傳巢狀資料夾階層的檔案特別有用，因為瀏覽器上傳僅支援上傳一般檔案清單。

## 上傳時處理資產 {#process-when-uploaded}

若要對上傳的資產執行其他處理，您可以在上傳資料夾上套用處理設定檔。 設定檔位於 **[!UICONTROL 屬性]** 中的資料夾頁面 [!DNL Assets]. 沒有副檔名或副檔名不正確的數位資產不會視需要處理。 例如，上傳此類資產時，可能沒有任何反應，或資產可能適用錯誤的處理設定檔。 使用者仍可將二進位檔案儲存在DAM中。

![具有新增處理設定檔選項的資產資料夾屬性](assets/assets-folder-properties.png)

可使用下列標籤：

* [中繼資料設定檔](metadata-profiles.md) 可讓您將預設中繼資料屬性套用至上傳至該資料夾的資產。
* [處理設定檔](asset-microservices-configure-and-use.md) 讓您產生的轉譯數超過預設值。

此外，如果 [!DNL Dynamic Media] 已在您的部署中啟用，以下標籤可供使用：

* [[!DNL Dynamic Media] 影像設定檔](dynamic-media/image-profiles.md) 可讓您套用特定裁切(**[!UICONTROL 智慧型裁切]** 和畫素裁切)，以及對上傳的資產進行銳利化設定。
* [[!DNL Dynamic Media] 視訊設定檔](dynamic-media/video-profiles.md) 可讓您套用特定的視訊編碼設定檔（解析度、格式、引數）。

>[!NOTE]
>
>[!DNL Dynamic Media] 對資產執行裁切和其他操作是非破壞性的，也就是說，這些操作不會變更上傳的原始檔案。 而是提供引數，以便在傳送資產時裁切或轉換。

對於已指派處理設定檔的資料夾，設定檔名稱會出現在卡片檢視的縮圖上。 在清單檢視中，設定檔名稱會出現在 **[!UICONTROL 處理設定檔]** 欄。

## 使用API上傳或內嵌資產 {#upload-using-apis}

有關上傳API和通訊協定的技術細節，以及開放原始碼SDK和範例使用者端的連結，請參見 [資產上傳](developer-reference-material-apis.md#asset-upload) 部分。

## 提示、最佳實務和限制 {#tips-limitations}

* 直接二進位上傳是上傳資產的新方法。 產品功能和使用者端預設支援此功能，例如 [!DNL Experience Manager] 使用者介面， [!DNL Adobe Asset Link]、和 [!DNL Experience Manager] 案頭應用程式。 客戶技術團隊自訂或擴充的任何自訂程式碼都必須使用新的上傳API和通訊協定。

* Adobe建議您在每個資料夾中新增不超過1000個資產， [!DNL Experience Manager Assets]. 雖然您可以新增更多資產至資料夾，但您可能會遇到效能問題，例如導覽至這類資料夾的速度變慢。

* 當您選取 **[!UICONTROL Replace]** 在 [!UICONTROL 名稱衝突] 對話方塊中，會為新資產重新產生資產ID。 此ID與先前資產的ID不同。 若 [資產分析](/help/assets/assets-insights.md) 啟用以追蹤曝光次數或點按次數 [!DNL Adobe Analytics]，則重新產生的資產ID會使為資產擷取的資料於失效 [!DNL Analytics].

* 有些上傳方法不會阻止您上傳資產 [禁止使用的字元](#filename-handling) 檔案名稱中的。 字元已取代為 `-` 符號。

* 使用瀏覽器上傳資產僅支援一般檔案清單，不支援巢狀資料夾階層。 若要上傳巢狀資料夾內的所有資產，請考慮使用 [案頭應用程式](#upload-assets-desktop-clients).

* 大量匯入方法會匯入資料來源中存在的整個資料夾結構。 不過，只有非空白資料夾會建立於 [!DNL Experience Manager].


<!-- TBD: Link to file name handling in DA docs when it is documented. 
-->

**另请参阅**

* [翻译资源](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [资源支持的文件格式](file-format-support.md)
* [搜索资源](search-assets.md)
* [连接的资源](use-assets-across-connected-assets-instances.md)
* [资源报告](asset-reports.md)
* [元数据架构](metadata-schemas.md)
* [下载资源](download-assets-from-aem.md)
* [管理元数据](manage-metadata.md)
* [搜索 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [批量元数据导入](metadata-import-export.md)

>[!MORELIKETHIS]
>
>* [[!DNL Adobe Experience Manager] 桌面应用程序](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html)
>* [关于 [!DNL Adobe Asset Link]](https://www.adobe.com/cn/creativecloud/business/enterprise/adobe-asset-link.html)
>* [[!DNL Adobe Asset Link] 文档](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html)
>* [資產上傳的技術參考](developer-reference-material-apis.md#asset-upload)

