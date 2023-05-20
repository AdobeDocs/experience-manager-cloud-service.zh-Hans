---
title: 处理大型内容存储库
description: 本節說明如何處理大型內容存放庫
exl-id: 21bada73-07f3-4743-aae6-2e37565ebe08
source-git-commit: cf09c7774b633ae2cf1c5b28fee2bd8191d80bb3
workflow-type: tm+mt
source-wordcount: '1846'
ht-degree: 8%

---

# 处理大型内容存储库 {#handling-large-content-repositories}

## 概述 {#overview}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_precopy"
>title="处理大型内容存储库"
>abstract="为了显著加快内容转移活动的提取和引入阶段，从而将内容移至 AEM as a Cloud Service，CTT 可利用 AzCopy 作为可选的复制前步骤。配置此前置步骤后，在提取阶段，AzCopy 将 blob 从 Amazon S3 或 Azure Blob 存储复制到迁移集 blob 存储。在引入阶段，AzCopy 将 blob 从迁移集 blob 存储复制到目标 AEM as a Cloud Service blob 存储。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html#setting-up-pre-copy-step" text="AzCopy 作为复制前步骤的快速入门"

使用內容轉移工具(CTT)複製大量Blob可能需要幾天時間。
為了大幅加快內容轉移活動的擷取和擷取階段，以將內容移至AEMas a Cloud Service，CTT可以善用 [AzCopy](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) 作為選擇性預先複製步驟。 當來源AEM執行個體設定為使用Amazon S3、Azure Blob儲存體資料存放區或檔案資料存放區時，可使用此預先複製步驟。 預先複製步驟對第1次完整擷取和擷取最為有效。 不過，不建議對後續追加使用預先複製（如果追加大小小於200GB），因為這樣可能會增加整個程式的時間。 設定此預先步驟後，在擷取階段，AzCopy會將Blob從Amazon S3、Azure Blob儲存體或檔案資料存放區複製至移轉集Blob存放區。 在引入阶段，AzCopy 将 blob 从迁移集 blob 存储复制到目标 AEM as a Cloud Service blob 存储。

## 開始前的重要考量 {#important-considerations}

請詳閱以下章節，瞭解在開始前的重要考量：

* 從CTT 2.0.16版開始，安裝套件組合時，會自動完成預先複製設定。 此外，如果移轉集大小大於200GB，擷取程式將自動利用預先複製功能。 azcopy.config檔案是在crx-quickstart/cloud-migration/目錄中建立。 如果您使用CTT 2.0.16版或更新版本，則不需要手動進行預先複製設定。

* 來源AEM版本必須是6.3 - 6.5。

* 來源AEM資料存放區已設定為使用Amazon S3或Azure Blob儲存體。 如需詳細資訊，請參閱 [在AEM 6中設定節點存放區和資料存放區](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html).

* 每個移轉集都會複製整個資料存放區，因此只應使用單一移轉集。

* 您需要存取權才能安裝 [AzCopy](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) 執行來源AEM執行個體上的執行個體（或VM）。

* 已在來源上的前7天內執行資料存放區垃圾收集。 如需詳細資訊，請參閱 [資料存放區垃圾收集](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html#data-store-garbage-collection).

### 如果來源AEM執行個體設定為使用Amazon S3或Azure Blob儲存體資料存放區，其他考量事項 {#additional-considerations-amazons3-azure}

* 由於從Amazon S3和Azure Blob儲存體傳輸資料會有相關成本，因此傳輸成本會與您現有儲存容器(無論是否在AEM中參照)中的資料總量相關。 請參閱 [Amazon S3](https://aws.amazon.com/s3/pricing/) 和 [Azure Blob儲存體](https://azure.microsoft.com/en-us/pricing/details/bandwidth/) 以取得更多詳細資料。

* 您需要現有來源Amazon S3貯體的存取金鑰和秘密金鑰組，或現有來源Azure Blob儲存體容器的SAS URI （唯讀存取權無妨）。

### 如果來源AEM執行個體設定為使用檔案資料存放區，其他考量事項 {#additional-considerations-aem-instance-filedatastore}

* 本機系統的可用空間必須嚴格大於來源資料存放區的1/256大小。 例如，如果資料存放區的大小為3 TB，則大於11.72 GB的可用空間必須存在於 `crx-quickstart/cloud-migration` AzCopy要運作的來源資料夾。 來源系統至少應有1 GB的可用空間。 可使用取得可用空間 `df -h` Linux執行個體上的command和Windows執行個體中的dir command。

* 每次在啟用AzCopy的情況下執行擷取時，整個檔案資料存放區都會平面化，並複製到雲端移轉容器。 如果您的移轉集明顯小於資料存放區的大小，則AzCopy擷取並非最佳方法。

* 使用AzCopy複製現有資料存放區後，請針對差異或追加擷取將其停用。

## 設定以使用AzCopy作為預先複製步驟 {#setting-up-pre-copy-step}

>[!NOTE]
>從CTT 2.0.16版開始，安裝套件組合時，會自動完成預先複製設定。 此外，如果移轉集大小大於200GB，擷取程式將自動利用預先複製功能。 azcopy.config檔案是在crx-quickstart/cloud-migration/目錄中建立。 如果您想要手動更新檔案的設定，請檢閱以下章節。

請詳閱本節，瞭解如何設定使用AzCopy作為內容轉移工具的預先複製步驟，將內容移轉至AEMas a Cloud Service：

### 0.決定資料存放區中所有內容的總大小 {#determine-total-size}

判斷資料存放區的大小總計很重要，原因有二：

* 如果來源AEM設定為使用檔案資料存放區，本機系統的可用空間必須嚴格大於來源資料存放區大小的1/256。

#### Azure Blob儲存體資料存放區 {#azure-blob-storage}

從Azure入口網站中的現有容器屬性頁面，使用 **計算大小** 按鈕來決定容器中所有內容的大小。 例如：

![图像](/help/journey-migration/content-transfer-tool/assets/Azure-blob-storage-data-store.png)

#### Amazon S3資料存放區 {#amazon-data}

您可以使用容器的「量度」標籤來判斷容器中所有內容的大小。 例如：


![图像](/help/journey-migration/content-transfer-tool/assets/amazon-s3-data-store.png)

#### 文件数据存储 {#file-data-store-determine-size}

* 對於mac、UNIX系統，請在資料存放區目錄上執行du命令以取得其大小：
   `du -sh [path to datastore on the instance]`. 例如，如果您的資料存放區位於 `/mnt/author/crx-quickstart/repository/datastore`，下列命令會為您取得其大小： `du -sh /mnt/author/crx-quickstart/repository/datastore`.

* 對於Windows，請使用資料存放區目錄上的dir命令來取得其大小：
   `dir /a/s [location of datastore]`。

### 1.安裝AzCopy {#install-azcopy}

[AzCopy](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) 是Microsoft提供的命令列工具，需要在來源執行個體上可用才能啟用此功能。

簡而言之，您最可能想要從 [AzCopy檔案頁面](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) 並將其解壓縮至/usr/bin之類的位置。

>[!IMPORTANT]
>記下您放置二進位檔的位置，因為您需要在稍後的步驟中取得該二進位檔的完整路徑。

### 2.安裝支援AzCopy的內容轉移工具(CTT)版本 {#install-ctt-azcopy-support}

>[!IMPORTANT]
>應使用最近發行的CTT版本。

最新CTT發行版本包含Amazon S3、Azure Blob儲存和檔案資料存放區的AzCopy支援。
您可以從以下網址下載最新版的CTT： [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) 入口網站。
請注意，僅支援2.0.0版及更高版本，建議您使用最新版本。

### 3.設定azcopy.config檔案 {#configure-azcopy-config-file}

在來源AEM例項中 `crx-quickstart/cloud-migration`，建立名為的新檔案 `azcopy.config`.

>[!NOTE]
>此設定檔案的內容會因您的來源AEM執行個體使用Azure、Amazon S3資料存放區或檔案資料存放區而有所不同。

#### Azure Blob儲存體資料存放區 {#azure-blob-storage-data}

您的azcopy.config檔案應包括下列屬性（請確定您執行個體使用正確的azCopyPath和azureSas）。

>[!NOTE]
>
> 如果您不想授予現有blob儲存容器的寫入許可權，您可以產生只具有讀取和清單許可權的新SAS URI。

```
azCopyPath=/usr/bin/azcopy
azureSas=https://example-resource.blob.core.windows.net/example-container?sig=--REDACTED--
```

#### Amazon S3資料存放區 {#amazon-sdata-store}

您的azcopy.config檔案應包含以下屬性（請確定為您的執行個體使用正確的值）。

>[!NOTE]
>
> 如果您的執行個體使用IAM角色來啟用AEM以存取S3，您將需要建立原則和使用者，並為S3儲存貯體啟用ListBucket和GetObject動作。 設定後，請使用此使用者的存取金鑰和秘密金鑰。

```
azCopyPath=/usr/bin/azcopy
s3Bucket=aem-63
s3Region=us-west-2
s3AccessKey=--REDACTED--
s3SecretKey=--REDACTED--
```

#### 文件数据存储 {#file-data-store-azcopy-config}

您的 `azcopy.config` 檔案必須包含azCopyPath屬性，以及指向檔案資料存放區位置的選用repository.home屬性。 為您的執行個體使用正確的值。
文件数据存储

```
azCopyPath=/usr/bin/azcopy
repository.home=/mnt/crx/author/crx-quickstart/repository/datastore
```

azCopyPath屬性必須包含azCopy命令列工具安裝在來源AEM執行個體上的位置的完整路徑。 如果缺少azCopyPath屬性，將不會執行blob預先複製步驟。

若 `repository.home` azcopy.config中缺少屬性，則為預設資料存放區位置 `/mnt/crx/author/crx-quickstart/repository/datastore` 將用於執行預先複製。

### 4.使用AzCopy擷取 {#extracting-azcopy}

設定好上述設定檔後，AzCopy預先複製階段就會隨著後續的擷取作業執行。 若要防止其執行，您可以重新命名此檔案或將其移除。

>[!NOTE]
>如果AzCopy未正確設定，您會在記錄中看到此訊息：
>`INFO c.a.g.s.m.c.a.AzCopyCloudBlobPreCopy - Blob pre-copy is not supported`。

1. 開始從CTT UI擷取。 請參閱 [內容轉移工具快速入門](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md) 和 [提取程式](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md) 以取得更多詳細資料。

1. 確認下列行已列印在擷取記錄中：

```
c.a.g.s.m.commons.ContentExtractor - *************** Beginning AzCopy Pre-Copy phase ***************
```

恭喜！此記錄專案表示您的設定被視為有效，且AzCopy目前正在將所有blob從來源容器複製到移轉容器。

來自AzCopy的記錄專案會出現在擷取記錄中，且會加上前置詞c.a.g.s.m.c.azcopy.AzCopyBlobPreCopy - [AzCopy預先複製]

>[!CAUTION]
>
> 在擷取的前幾分鐘，請密切注意擷取記錄，以瞭解是否有任何問題的跡象。 例如，如果找不到來源Azure容器，則會記錄以下內容：

```
[AzCopy pre-copy] failed to perform copy command due to error: cannot start job due to error: cannot list files due to reason -> github.com/Azure/azure-storage-blob-go/azblob.newStorageError, github.com/Azure/azure-storage-blob-go@v0.10.1-0.20210407023846-16cf969ec1c3/azblob/zc_storage_error.go:42
[AzCopy pre-copy] ===== RESPONSE ERROR (ServiceCode=ContainerNotFound) =====
[AzCopy pre-copy] Description=The specified container does not exist.
[AzCopy pre-copy] RequestId:5fb674b9-201e-001b-2a5b-527400000000
[AzCopy pre-copy] Time:2021-05-26T18:18:07.5931967Z, Details: 
[AzCopy pre-copy] Code: ContainerNotFound
```

在發生AzCopy問題的情況下，擷取將立即失敗，而擷取記錄將包含失敗的詳細資訊。

AzCopy在後續執行時將自動略過在錯誤發生前複製的任何Blob，而且不需要再次複製。

#### 針對檔案資料存放區 {#file-data-store-extract}

為來源檔案dataStore執行AzCopy時，您應該會在記錄中看到類似這些的訊息，指出正在處理資料夾：
`c.a.g.s.m.c.a.AzCopyFileSourceBlobPreCopy - [AzCopy pre-copy] Processing folder (1/24) crx-quickstart/repository/datastore/5d`

### 5.使用AzCopy擷取 {#ingesting-azcopy}

請參閱 [將內容擷取至Target](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md)
有關從Cloud Acceleration Manager (CAM)擷取內容到目標的一般資訊，包括在「新擷取」對話方塊中如何使用AzCopy （預先複製）或不使用的指示。

若要在內嵌期間妥善運用AzCopy，您需要使用2021.6.5561以上的AEMas a Cloud Service版本。

若要檢視進度，請參閱Cloud Acceleration Manager和擷取記錄中的「擷取工作」清單。  與成功的AzCopy工作相關的記錄專案將顯示如下（允許一些差異）。 偶爾檢查記錄可能會及早警示您問題，並協助您找到任何問題的快速解決方案。

```
*************** Beginning AzCopy pre-copy phase ***************
INFO: Scanning...
INFO: Failed to create one or more destination container(s). Your transfers may still succeed if the container already exists.
INFO: Any empty folders will not be processed, because source and/or destination doesn't have full folder support
INFO: azcopy: A newer version 10.11.0 is available to download
 
Job 419d98da-fc05-2a45-70cc-797fee632031 has started
Log file is located at: /root/.azcopy/419d98da-fc05-2a45-70cc-797fee632031.log
 
0.0 %, 0 Done, 0 Failed, 886 Pending, 0 Skipped, 886 Total,
 
Job 419d98da-fc05-2a45-70cc-797fee632031 summary
Elapsed Time (Minutes): 0.0334
Number of File Transfers: 886
Number of Folder Property Transfers: 0
Total Number of Transfers: 886
Number of Transfers Completed: 17
Number of Transfers Failed: 0
Number of Transfers Skipped: 869
TotalBytesTransferred: 248350
Final Job Status: CompletedWithSkipped
 
*************** Completed AzCopy pre-copy phase ***************
```

## 后续内容 {#whats-next}

在您學習了處理大型內容存放庫以大幅加快內容轉移活動的提取和擷取階段以將內容移動到AEMas a Cloud Service後，您現在就可以學習使用內容轉移工具的提取流程了。 另請參閱 [在內容轉移工具中從來源擷取內容](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md) 以瞭解如何從「內容轉移工具」擷取移轉集。
