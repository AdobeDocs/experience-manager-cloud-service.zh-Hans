---
title: 以下專案的開發人員參考： [!DNL Assets]
description: '"[!DNL Assets] API和開發人員參考內容可讓您管理資產，包括二進位檔案、中繼資料、轉譯、註解和 [!DNL Content Fragments].」'
contentOwner: AG
feature: APIs,Assets HTTP API
role: Developer,Architect,Admin
exl-id: c75ff177-b74e-436b-9e29-86e257be87fb
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '1899'
ht-degree: 6%

---

# [!DNL Adobe Experience Manager Assets] 開發人員使用案例、API和參考資料 {#assets-cloud-service-apis}

本文包含適用於開發人員之建議、參考資料和資源， [!DNL Assets] as a [!DNL Cloud Service]. 其中包括新的資產上傳模組、API參考資料，以及有關後處理工作流程中提供的支援資訊。

## [!DNL Experience Manager Assets] API和作業 {#use-cases-and-apis}

[!DNL Assets] as a [!DNL Cloud Service] 提供數個API，以程式設計方式與數位資產互動。 每個API都支援特定使用案例，如下表所述。 此 [!DNL Assets] 使用者介面， [!DNL Experience Manager] 案頭應用程式和 [!DNL Adobe Asset Link] 支援所有或部分作業。

>[!CAUTION]
>
>有些API持續存在，但主動不受支援(以×表示)。 請儘量不要使用這些API。

| 支援等級 | 描述 |
| ------------- | --------------------------- |
| ✓ | 支持 |
| × | 不受支持. 請勿使用。 |
| - | 不可用 |

| 使用案例 | [aem-upload](https://github.com/adobe/aem-upload) | [Experience Manager/Sling/JCR](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html) Java API | [asset compute服務](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html) | [[!DNL Assets] HTTP API](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/mac-api-assets.html#create-an-asset) | Sling [GET](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) / [POST](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html) servlet | [GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) |
| ----------------|:---:|:---:|:---:|:---:|:---:|:---:|
| **原始二進位** |  |  |  |  |  |  |
| 建立原始檔案 | ✓ | × | - | × | × | - |
| 讀取原始檔案 | - | × | ✓ | ✓ | ✓ | - |
| 更新原始檔案 | ✓ | × | ✓ | × | × | - |
| 刪除原始檔案 | - | ✓ | - | ✓ | ✓ | - |
| 複製原始檔案 | - | ✓ | - | ✓ | ✓ | - |
| 移動原始檔案 | - | ✓ | - | ✓ | ✓ | - |
| **元数据** |  |  |  |  |  |  |
| 建立中繼資料 | - | ✓ | ✓ | ✓ | ✓ | - |
| 讀取中繼資料 | - | ✓ | - | ✓ | ✓ | - |
| 更新元数据 | - | ✓ | ✓ | ✓ | ✓ | - |
| 刪除中繼資料 | - | ✓ | ✓ | ✓ | ✓ | - |
| 複製中繼資料 | - | ✓ | - | ✓ | ✓ | - |
| 移動中繼資料 | - | ✓ | - | ✓ | ✓ | - |
| **內容片段(CF)** |  |  |  |  |  |  |
| 建立CF | - | ✓ | - | ✓ | - | - |
| 讀取CF | - | ✓ | - | ✓ | - | ✓ |
| 更新CF | - | ✓ | - | ✓ | - | - |
| 刪除Cf | - | ✓ | - | ✓ | - | - |
| 複製CF | - | ✓ | - | ✓ | - | - |
| 移動CF | - | ✓ | - | ✓ | - | - |
| **版本** |  |  |  |  |  |  |
| 建立版本 | ✓ | ✓ | - | - | - | - |
| 讀取版本 | - | ✓ | - | - | - | - |
| 刪除版本 | - | ✓ | - | - | - | - |
| **文件夹** |  |  |  |  |  |  |
| 创建文件夹 | ✓ | ✓ | - | ✓ | - | - |
| 讀取資料夾 | - | ✓ | - | ✓ | - | - |
| 刪除資料夾 | ✓ | ✓ | - | ✓ | - | - |
| 複製資料夾 | ✓ | ✓ | - | ✓ | - | - |
| 行動資料夾 | ✓ | ✓ | - | ✓ | - | - |

## 資產上傳 {#asset-upload}

在 [!DNL Experience Manager] as a [!DNL Cloud Service]，即可使用HTTP API直接將資產上傳至雲端儲存空間。 上傳二進位檔案的步驟如下。 在外部應用程式中執行這些步驟，而不是在 [!DNL Experience Manager] JVM。

1. [提交HTTP要求](#initiate-upload). 它會通知 [!DNL Experience Manage]或部署您打算上傳新二進位檔的動作。
1. [PUT二進位檔的內容](#upload-binary) 初始化請求提供的一或多個URI。
1. [提交HTTP要求](#complete-upload) 通知伺服器已成功上傳二進位檔的內容。

![直接二進位上傳通訊協定概觀](assets/add-assets-technical.png)

>[!IMPORTANT]
在外部應用程式中而不是在內部執行上述步驟 [!DNL Experience Manager] JVM。

方法提供可擴充且效能更高的資產上傳處理方式。 相較於的差異 [!DNL Experience Manager] 6.5為：

* 二進位檔不會通過 [!DNL Experience Manager]，現在只需使用為部署設定的二進位雲端儲存空間，來協調上傳程式。
* 二進位雲端儲存空間可與內容傳遞網路(CDN)或Edge網路搭配使用。 CDN會選取距離使用者端較近的上傳端點。 當資料傳輸至附近端點的距離較短時，上傳效能和使用者體驗會有所改善，尤其是地理上分散的團隊。

>[!NOTE]
請參閱使用者端代碼，以在開放原始碼中實作此方法 [aem-upload資料庫](https://github.com/adobe/aem-upload).
[!IMPORTANT]
在某些情況下，由於Cloud Service中的儲存最終具有一致的性質，變更可能不會在對Experience Manager的請求之間完全傳播。 這會導致404個回應起始或完成上傳呼叫，因為必要的資料夾建立未傳播。 使用者端應該會收到404個回應，並透過實作附有後退策略的重試來處理這些回應。

### 啟動上傳 {#initiate-upload}

將HTTPPOST請求提交到所需的資料夾。 在此資料夾中建立或更新資產。 包含選取器 `.initiateUpload.json` 表示要求要開始上傳二進位檔案。 例如，應建立資產的資料夾的路徑為 `/assets/folder`. POST請求是 `POST https://[aem_server]:[port]/content/dam/assets/folder.initiateUpload.json`.

請求內文的內容型別應為 `application/x-www-form-urlencoded` 表單資料，包含下列欄位：

* `(string) fileName`: 必填. 資產出現的名稱 [!DNL Experience Manager].
* `(number) fileSize`: 必填. 正在上傳之資產的檔案大小（位元組）。

只要每個二進位檔案都包含必要欄位，就可以使用單一要求來起始多個二進位檔案的上傳。 如果成功，請求會以回應 `201` 狀態代碼和包含JSON資料的內文，格式如下：

```json
{
    "completeURI": "(string)",
    "folderPath": "(string)",
    "files": [
        {
            "fileName": "(string)",
            "mimeType": "(string)",
            "uploadToken": "(string)",
            "uploadURIs": [
                "(string)"
            ],
            "minPartSize": (number),
            "maxPartSize": (number)
        }
    ]
}
```

* `completeURI` （字串）：當二進位檔完成上傳時，呼叫此URI。 URI可以是絕對URI或相對URI，使用者端應該能夠處理任一個。 也就是說，值可以是 `"https://[aem_server]:[port]/content/dam.completeUpload.json"` 或 `"/content/dam.completeUpload.json"` 另請參閱 [完成上傳](#complete-upload).
* `folderPath` （字串）：上傳二進位檔案的資料夾完整路徑。
* `(files)` （陣列）：其長度和順序符合起始請求中提供的二進位資訊清單長度和順序的元素清單。
* `fileName` （字串）：對應二進位檔的名稱，如起始請求中所提供。 此值應包含在完整請求中。
* `mimeType` （字串）：對應二進位檔的mime型別，如起始請求中所提供。 此值應包含在完整請求中。
* `uploadToken` （字串）：對應二進位檔的上傳權杖。 此值應包含在完整請求中。
* `uploadURIs` （陣列）：字串清單，其值是二進位內容應上傳到的完整URI (請參閱 [上傳二進位檔](#upload-binary))。
* `minPartSize` （數字）：可提供給任一項的資料長度（位元組），以位元組為單位。 `uploadURIs`，如果有超過一個URI。
* `maxPartSize` （數字）：可提供給任一個的資料長度上限（位元組）。 `uploadURIs`，如果有超過一個URI。

### 上傳二進位檔 {#upload-binary}

起始上傳的輸出包含一或多個上傳URI值。 如果提供了多個URI，使用者端可以依序將二進位檔分割成多個部分，並向提供的上傳URI提出每個部分的PUT請求。 如果您選擇將二進位檔案分割成零件，請遵循下列准則：

* 除了最後一個零件外，每個零件的大小都必須大於或等於 `minPartSize`.
* 每個零件的大小必須小於或等於 `maxPartSize`.
* 如果二進位檔案的大小超過 `maxPartSize`，將二進位檔分割為多個部分以上傳。
* 您不需要使用所有URI。

如果二進位檔的大小小於或等於 `maxPartSize`，您可以改為將整個二進位檔案上傳至單一上傳URI。 如果提供了多個上傳URI，請使用第一個上傳URI並忽略其餘上傳URI。 您不需要使用所有URI。

CDN邊緣節點有助於加速要求的二進位檔上傳。

最簡單的方法是使用 `maxPartSize` 作為零件尺寸。 如果您使用此值作為零件大小，API合約可確保有足夠的上傳URI來上傳您的二進位檔。 若要這麼做，請將二進位分割成大小部分 `maxPartSize`，依序為每個零件使用一個URI。 最終零件的大小可小於或等於 `maxPartSize`. 例如，假設二進位檔案的總大小為20,000個位元組， `minPartSize` 為5,000位元組， `maxPartSize` 為8,000位元組，而且上傳URI的數量為5。 執行以下步驟：

* 使用第一個上傳URI上傳二進位的前8,000個位元組。
* 使用第二個上傳URI上傳第二個8,000位元組的二進位檔案。
* 使用第三個上傳URI上傳二進位檔的最後4,000個位元組。 由於這是最後部分，因此它不必大於 `minPartSize`.
* 您不需要使用最後兩個上傳URI。 您可以忽略它們。

常見的錯誤是根據API提供的上傳URI數量計算零件大小。 API合約無法保證此方法有效，而且實際上可能會導致零件大小超出兩者之間的範圍 `minPartSize` 和 `maxPartSize`. 這可能會導致二進位上傳失敗。

同樣地，最簡單且最安全的方法是隻使用大小等於 `maxPartSize`.

如果上傳成功，伺服器會以回應每個要求 `201` 狀態代碼。

>[!NOTE]
如需上傳演演算法的詳細資訊，請參閱 [正式功能檔案](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html#Upload) 和 [API檔案](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/api/binary/BinaryUpload.html) Apache Jackrabbit Oak專案中的。

### 完成上傳 {#complete-upload}

上傳二進位檔案的所有部分後，將HTTPPOST請求提交至初始化資料提供的完整URI。 請求內文的內容型別應為 `application/x-www-form-urlencoded` 表單資料，包含下列欄位。

| 字段 | 类型 | 必要與否 | 描述 |
|---|---|---|---|
| `fileName` | 字符串 | 必填 | 資產名稱，由初始資料提供。 |
| `mimeType` | 字符串 | 必填 | 起始資料所提供的二進位檔的HTTP內容型別。 |
| `uploadToken` | 字符串 | 必填 | 上傳二進位的Token，如起始資料所提供。 |
| `createVersion` | 布尔值 | 可选 | 若 `True` 且具有指定名稱的資產存在，則 [!DNL Experience Manager] 建立資產的新版本。 |
| `versionLabel` | 字符串 | 可选 | 如果建立了新版本，則會提供與資產新版本相關聯的標籤。 |
| `versionComment` | 字符串 | 可选 | 如果建立了新版本，則會有與該版本相關聯的註解。 |
| `replace` | 布尔值 | 可选 | 若 `True` 而且具有指定名稱的資產已存在， [!DNL Experience Manager] 刪除資產，然後重新建立資產。 |
| `uploadDuration` | 数字 | 可选 | 檔案完整上傳的總時間，以毫秒為單位。 如果指定，上傳持續時間會包含在系統的記錄檔中，以進行傳輸率分析。 |
| `fileSize` | 数字 | 可选 | 檔案的大小（位元組）。 如果已指定，檔案大小會包含在系統的記錄檔中，以進行傳輸速率分析。 |

>[!NOTE]
如果資產存在，但兩者皆非 `createVersion` 也不 `replace` 已指定，則 [!DNL Experience Manager] 以新的二進位檔案更新資產的目前版本。

如同初始程式，完整的請求資料可能包含多個檔案的資訊。

直到叫用檔案的完整URL後，才會完成上傳二進位檔的程式。 資產會在上傳程式完成後處理。 即使資產的二進位檔案已完全上傳，但上傳程式尚未完成，處理作業也不會開始。 如果上傳成功，伺服器會以回應 `200` 狀態代碼。

### 开源上传库 {#open-source-upload-library}

若要進一步瞭解上傳演演算法或建立您自己的上傳指令碼和工具，Adobe提供開放原始碼程式庫和工具：

* [開放原始碼aem-upload資料庫](https://github.com/adobe/aem-upload).
* [开源命令行工具](https://github.com/adobe/aio-cli-plugin-aem).

>[!NOTE]
aem-upload程式庫和命令列工具都會使用 [node-httptransfer程式庫](https://github.com/adobe/node-httptransfer/)

### 過時的資產上傳API {#deprecated-asset-upload-api}

<!-- #ENGCHECK review / update the list of deprecated APIs below. -->

只有以下專案才支援新的上傳方法 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service]. 來自的API [!DNL Adobe Experience Manager] 6.5已過時。 下列API已棄用與上傳或更新資產或轉譯（任何二進位上傳）相關的方法：

* [EXPERIENCE MANAGER ASSETS HTTP API](mac-api-assets.md)
* `AssetManager` Java API，類似 `AssetManager.createAsset(..)`

>[!MORELIKETHIS]
* [開放原始碼aem-upload資料庫](https://github.com/adobe/aem-upload).
* [开源命令行工具](https://github.com/adobe/aio-cli-plugin-aem).
* [直接上傳的Apache Jackrabbit Oak檔案](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html#Upload).


## 資產處理和後續處理工作流程 {#post-processing-workflows}

在 [!DNL Experience Manager]，資產處理會根據 **[!UICONTROL 處理設定檔]** 使用的設定 [資產微服務](asset-microservices-configure-and-use.md#get-started-using-asset-microservices). 處理不需要開發人員擴充功能。

對於後處理工作流程設定，請使用帶有擴充功能的標準工作流程以及自訂步驟。

## 後處理工作流程中工作流程步驟的支援 {#post-processing-workflows-steps}

如果您從舊版升級 [!DNL Experience Manager]，您可以使用資產微服務來處理資產。 雲端原生資產微服務設定及使用都較為簡單。 中使用的幾個工作流程步驟 [!UICONTROL DAM更新資產] 不支援舊版的工作流程。 如需支援類別的詳細資訊，請參閱 [Java API參考或Javadocs](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html).

以下技術工作流程模型已由資產微服務取代，或無法提供支援：

* `com.day.cq.dam.cameraraw.process.CameraRawHandlingProcess`
* `com.day.cq.dam.core.process.CommandLineProcess`
* `com.day.cq.dam.pdfrasterizer.process.PdfRasterizerHandlingProcess`
* `com.day.cq.dam.core.process.AddPropertyWorkflowProcess`
* `com.day.cq.dam.core.process.CreateSubAssetsProcess`
* `com.day.cq.dam.core.process.DownloadAssetProcess`
* `com.day.cq.dam.word.process.ExtractImagesProcess`
* `com.day.cq.dam.word.process.ExtractPlainProcess`
* `com.day.cq.dam.ids.impl.process.IDSJobProcess`
* `com.day.cq.dam.indd.process.INDDMediaExtractProcess`
* `com.day.cq.dam.indd.process.INDDPageExtractProcess`
* `com.day.cq.dam.core.impl.lightbox.LightboxUpdateAssetProcess`
* `com.day.cq.dam.pim.impl.sourcing.upload.process.ProductAssetsUploadProcess`
* `com.day.cq.dam.core.process.SendDownloadAssetEmailProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.StartTrainingProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.TransferTrainingDataProcess`
* `com.day.cq.dam.switchengine.process.SwitchEngineHandlingProcess`
* `com.day.cq.dam.core.process.GateKeeperProcess`
* `com.day.cq.dam.s7dam.common.process.DMEncodeVideoWorkflowCompletedProcess`
* `com.day.cq.dam.core.process.DeleteImagePreviewProcess`
* `com.day.cq.dam.video.FFMpegTranscodeProcess`
* `com.day.cq.dam.core.process.ThumbnailProcess`
* `com.day.cq.dam.video.FFMpegThumbnailProcess`
* `com.day.cq.dam.core.process.CreateWebEnabledImageProcess`
* `com.day.cq.dam.core.process.CreatePdfPreviewProcess`
* `com.day.cq.dam.s7dam.common.process.VideoUserUploadedThumbnailProcess`
* `com.day.cq.dam.s7dam.common.process.VideoThumbnailDownloadProcess`
* `com.day.cq.dam.s7dam.common.process.VideoProxyServiceProcess`
* `com.day.cq.dam.scene7.impl.process.Scene7UploadProcess`
* `com.day.cq.dam.s7dam.common.process.S7VideoThumbnailProcess`
* `com.day.cq.dam.core.process.MetadataProcessorProcess`
* `com.day.cq.dam.core.process.AssetOffloadingProcess`
* `com.adobe.cq.dam.dm.process.workflow.DMImageProcess`

<!-- Commenting the previous list documented at the time of GA. Replacing it with the updated list via cqdoc-18231.

* `com.day.cq.dam.core.process.DeleteImagePreviewProcess`
* `com.day.cq.dam.s7dam.common.process.DMEncodeVideoWorkflowCompletedProcess`
* `com.day.cq.dam.core.process.GateKeeperProcess`
* `com.day.cq.dam.core.process.AssetOffloadingProcess`
* `com.day.cq.dam.core.process.MetadataProcessorProcess`
* `com.adobe.cq.dam.dm.process.workflow.DMImageProcess`
* `com.day.cq.dam.s7dam.common.process.S7VideoThumbnailProcess`
* `com.day.cq.dam.scene7.impl.process.Scene7UploadProcess`
* `com.day.cq.dam.s7dam.common.process.VideoProxyServiceProcess`
* `com.day.cq.dam.s7dam.common.process.VideoThumbnailDownloadProcess`
* `com.day.cq.dam.s7dam.common.process.VideoUserUploadedThumbnailProcess`
* `com.day.cq.dam.core.process.CreatePdfPreviewProcess`
* `com.day.cq.dam.core.process.CreateWebEnabledImageProcess`
* `com.day.cq.dam.video.FFMpegThumbnailProcess`
* `com.day.cq.dam.core.process.ThumbnailProcess`
* `com.day.cq.dam.cameraraw.process.CameraRawHandlingProcess`
* `com.day.cq.dam.core.process.CommandLineProcess`
* `com.day.cq.dam.pdfrasterizer.process.PdfRasterizerHandlingProcess`
* `com.day.cq.dam.core.process.AddPropertyWorkflowProcess`
* `com.day.cq.dam.core.process.CreateSubAssetsProcess`
* `com.day.cq.dam.core.process.DownloadAssetProcess`
* `com.day.cq.dam.word.process.ExtractImagesProcess`
* `com.day.cq.dam.word.process.ExtractPlainProcess`
* `com.day.cq.dam.video.FFMpegTranscodeProcess`
* `com.day.cq.dam.ids.impl.process.IDSJobProcess`
* `com.day.cq.dam.indd.process.INDDMediaExtractProcess`
* `com.day.cq.dam.indd.process.INDDPageExtractProcess`
* `com.day.cq.dam.core.impl.lightbox.LightboxUpdateAssetProcess`
* `com.day.cq.dam.pim.impl.sourcing.upload.process.ProductAssetsUploadProcess`
* `com.day.cq.dam.core.process.ScheduledPublishBPProcess`
* `com.day.cq.dam.core.process.ScheduledUnPublishBPProcess`
* `com.day.cq.dam.core.process.SendDownloadAssetEmailProcess`
-->

<!-- PPTX source: slide in add-assets.md - overview of direct binary upload section of
https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
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
* [[!DNL Experience Cloud] as a [!DNL Cloud Service] SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md).

