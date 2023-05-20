---
title: 重大變更 [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service]
description: 重大變更 [!DNL Adobe Experience Manager Assets] 在 [!DNL Experience Manager] as a [!DNL Cloud Service] 與 [!DNL Adobe Experience Manager] 6.5.
feature: Release Information
role: User,Leader,Architect,Admin
exl-id: 93e7dbcd-016e-4ef2-a1cd-c554efb5ad34
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 11%

---

# 重大變更 [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#notable-changes}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 提供許多管理Experience Manager專案的新功能，並帶來許多可能性。 兩者之間有許多差異 [!DNL Experience Manager Assets] 內部部署或作為Adobe託管服務託管，而非 [!DNL Experience Manager] as a [!DNL Cloud Service]. 本文章著重介紹以下各項的重要差異： [!DNL Assets] 功能。

和以下專案的主要差異： [!DNL Experience Manager] 6.5包含以下幾個方面：

* [資產擷取、上傳和處理](#asset-ingestion).
* [適用於雲端原生處理的資產微服務](#asset-microservices).
* [删除了经典 UI](#classic-ui).

## 資產擷取、處理和分發 {#asset-ingestion-distribution}

資產上傳透過實現更好的內嵌縮放、更快的上傳、使用微服務的更快處理和大量內嵌，以最佳化效率。 產品功能（網頁使用者介面、案頭使用者端）已更新。 此外，這可能會影響某些現有的自訂。

* [!DNL Experience Manager] 使用直接二進位存取原則上傳和下載資產，並使用資產微服務處理資產。 另請參閱 [微服務概觀](/help/assets/asset-microservices-overview.md).
   * 資產上傳 [直接二進位存取](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access).
   * 如需技術詳細資訊，請參閱 [直接二進位上傳通訊協定和API](/help/assets/developer-reference-material-apis.md#upload-binary).
   * 如需基本CRUD作業可用API方法的比較，請參閱 [API和資產作業](/help/assets/developer-reference-material-apis.md#use-cases-and-apis).
*  早期版本中的默认工作流程 **[!UICONTROL DAM 资产更新]**&#x200B;不再可用。[!DNL Experience Manager]相反，資產微服務提供可擴充、現成可用的服務，涵蓋大部分預設資產處理（轉譯、中繼資料擷取和索引文字擷取）。
   * 另請參閱 [設定和使用資產微服務](/help/assets/asset-microservices-configure-and-use.md)
   * 若要在處理中有自訂的工作流程步驟， [後處理工作流程](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) 可使用。

* 在不進行任何轉換的情況下傳送二進位檔案的網站元件可使用直接下載。 SlingGETServlet已更新，讓開發人員可依預設執行此操作。 在轉換後傳送二進位的網站元件（例如透過servlet調整大小）可以繼續正常運作。

透過資產微服務產生的標準轉譯會使用相同的命名慣例，以向後相容的方式儲存在資產存放庫節點中。

## 開發和測試資產微服務 {#asset-microservices}

资源微服务使用云服务来对资源进行可扩展的弹性处理。Adobe 管理云服务以实施对不同的资源类型和处理选项的最优处理。資產微服務有助於避免使用協力廠商的轉譯工具和方法(例如 [!DNL ImageMagick])並簡化設定，同時為常見檔案型別提供現成可用的功能。 您現在可以處理 [廣泛的檔案型別](/help/assets/file-format-support.md) 比舊版Experience Manager更多的現成可用格式。 例如，現在可以提取PSD和PSB格式的縮圖，而之前需要第三方解決方案，例如 [!DNL ImageMagick]. 您不能使用的複雜設定 [!DNL ImageMagick] 的 [!UICONTROL 處理設定檔] 設定。 使用 [!DNL Dynamic Media] 用於進階FFmpeg影片轉碼，並使用處理設定檔用於 [MP4視訊的基本轉碼](/help/assets/manage-video-assets.md#transcode-video).

資產微服務是雲端原生服務，會自動布建並連線至 [!DNL Experience Manager] 在Cloud Manager中管理的客戶計畫和環境中。 若要延伸或自訂 [!DNL Experience Manager]，開發人員可以使用現有內容或資產，以及雲端環境中產生的轉譯，以使用、顯示、下載資產來測試及驗證其程式碼。

若要對程式碼和流程進行端對端驗證（包括資產擷取和處理），請使用將程式碼變更部署到雲端開發環境 [管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) 和測試，以完全執行資產微服務處理。

## 功能同位，與 [!DNL Experience Manager] 6.5 {#cloud-service-feature-status}

[!DNL Experience Manager] as a [!DNL Cloud Service] 推出許多新功能，以及更優異的效能方式，讓現有功能發揮作用。 不過，從移出時 [!DNL Experience Manager] 6.5至 [!DNL Experience Manager] as a [!DNL Cloud Service]，您可能會注意到某些功能的運作方式不同、無法使用或部分可用。 以下是這類功能的清單。 此外，請參閱 [過時和移除的功能](/help/release-notes/deprecated-removed-features.md).

| 功能或使用案例 | 中的狀態 [!DNL Experience Manager] as a [!DNL Cloud Service] | 评论 |
|-----|-----|-----|
| [重複資產偵測](/help/assets/manage-digital-assets.md#detect-duplicate-assets) | 運作方式不同 | 另請參閱 [運作方式 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/duplicate-detection.html). |
| [僅供刊登(FPO)轉譯](/help/assets/configure-fpo-renditions.md) | 運作方式不同 | 處理設定檔使用資產微服務來產生FPO轉譯。 在Experience Manager6.5中，協力廠商解決方案如 [!DNL ImageMagick] 可用來產生轉譯。 |
| 中繼資料回寫 | 運作方式不同 | 默认为已禁用. 視需要啟用對應的工作流程啟動器。 回寫由資產微服務處理。 |
| 處理使用封裝管理程式上傳的資產 | 需要手動介入 | 使用手動重新處理 **[!UICONTROL 重新處理資產]** 動作。 |
| mime型別偵測 | 不受支持. | 如果您上傳的數位資產沒有副檔名或副檔名不正確，可能無法如期處理。 使用者仍然可以在DAM中儲存副檔名為的二進位檔案。 另請參閱 [中的MIME型別偵測 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/detect-asset-mime-type-with-tika.html). |
| 為複合資產產生子資產 | 不受支持. | 可能無法完成附註等相依使用案例。 另請參閱 [在中建立子資產 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/managing-linked-subassets.html#generate-subassets). 某些檔案型別的PDF預覽可從 [2021.7.0版](/help/release-notes/release-notes-cloud/release-notes-current.md). |
| 编辑图像 | 不受支持 | Experience Manageras a Cloud Service不支援編輯資產。 另請參閱 [在Experience Manager6.5中如何運作](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.html#editing-images). |
| 主页 | 不受支持 | 另請參閱 [[!DNL Assets] Home Page experience in [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-home-page.html) |
| 從ZIP封存擷取資產 | 不受支持 | 另請參閱 [中的壓縮解壓縮 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.html#extractzip). |
| 資產評等 | 不受支持 | 不支援中繼資料結構編輯器中的評等Widget。 |
| 內容處置篩選 | 不受支持 | 熱門的使用案例 `ContentDispositionFilter` 是讓管理員設定 [!DNL Experience Manager] 提供HTML檔案，並內嵌開啟PDF檔案，而非下載這些檔案。 在Publish執行個體上，您可以使用Dispatcher設定來管理處置。 在作者執行個體上，Adobe不建議修改內容處置標頭。 另請參閱 [中的內容處置篩選器 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/content-disposition-filter.html). |
| 產品拍照範本 | 不受支持 | 另請參閱 [中的產品拍照範本 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/projects/managing-product-information.html). |
| 智慧型翻譯 | 不受支持 | [智慧型翻譯](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/translation/smart-translation-search-feature-video-use.html) 不支援 [!DNL Experience Manager] as a [!DNL Cloud Service]. |
| WebDAV | 不受支持 | 如需其他選擇，請參閱 [[!DNL Creative Cloud] 整合](/help/assets/aem-cc-integration-best-practices.md) 或 [開發人員參考資料](/help/assets/developer-reference-material-apis.md). |
| 经典 UI | 不受支持 | 僅提供觸控式使用者介面。 |

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
>下列資源適用於 [!DNL Experience Manager] as a [!DNL Cloud Service]：
>
>* [已棄用和已移除的功能清單](/help/release-notes/deprecated-removed-features.md)
>* [簡介](/help/overview/introduction.md)
>* [新增功能和不同功能](/help/overview/what-is-new-and-different.md)
>* [架構](/help/overview/architecture.md)
>* [重要更改](/help/release-notes/aem-cloud-changes.md)
>* [重要更改 [!DNL Sites]](/help/sites-cloud/sites-cloud-changes.md)
>* [教學影片](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html?lang=zh-Hans)

