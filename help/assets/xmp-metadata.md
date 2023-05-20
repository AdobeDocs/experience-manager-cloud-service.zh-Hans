---
title: XMP 元数据
description: 瞭解用於中繼資料管理的XMP （可延伸中繼資料平台）中繼資料標準。 它可供Experience Manager用作建立、處理和交換中繼資料的標準化格式。
contentOwner: AG
feature: Metadata
role: User,Admin
exl-id: fd9af408-d2a3-4c7a-9423-c4b69166f873
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '1041'
ht-degree: 18%

---

# XMP 元数据 {#xmp-metadata}

XMP （可延伸中繼資料平台）是Experience Manager Assets用於所有中繼資料管理的中繼資料標準。 XMP為各種應用程式的中繼資料的建立、處理和交換提供標準格式。

除了提供可嵌入到所有檔案格式的通用中繼資料編碼之外，XMP還提供豐富的 [內容模型](#xmp-core-concepts) 和 [受Adobe支援](#advantages-of-xmp) 和其他公司，以便XMP的使用者能夠與 [!DNL Assets] 擁有強大的平台作為建置基礎。

## XMP概觀和生態系統 {#xmp-ecosystem}

[!DNL Assets] 原生支援XMP中繼資料標準。 XMP是在數位資產中處理和儲存標準化和專屬中繼資料的標準。 XMP的設計目的是作為允許多個應用程式有效使用中繼資料的通用標準。

例如，生產專業人員可使用Adobe應用程式內建的XMP支援，以跨多種檔案格式傳遞資訊。 此 [!DNL Assets] 存放庫會擷取XMP中繼資料，並使用它來管理內容生命週期，並提供建立自動化工作流程的功能。

XMP透過提供資料模型、儲存模型和結構描述，將中繼資料的定義、建立和處理標準化。 本章節將介紹所有這些概念。

來自EXIF、ID3或Microsoft Office的所有舊版中繼資料會自動轉譯為XMP，可延伸以支援客戶特定的中繼資料結構，例如產品目錄。

XMP中的中繼資料包含一組屬性。 這些屬性一律與稱為資源的特定實體相關聯；也就是說，屬性是「關於」資源的。 若是XMP，資源一律為資產。

XMP 定义了一个可与任何定义的元数据项集一起使用的[元数据](https://en.wikipedia.org/wiki/Metadata)模型。XMP 还为基本属性定义了一个特定的[架构[，这些基本属性可用于记录资源经过多个处理步骤的历史记录：从拍摄、](https://en.wikipedia.org/wiki/XML_schema)扫描](https://en.wikipedia.org/wiki/Image_scanner)或创作为文本，到照片编辑步骤（如[裁剪](https://en.wikipedia.org/wiki/Cropping_%28image%29)或颜色调整），再到组合到最终图像中。XMP 允许每个软件程序或设备向数字资源添加其自己的信息，该信息可保留在最终的数字文件中。

XMP 最常使用 [W3C](https://en.wikipedia.org/wiki/World_Wide_Web_Consortium) [资源描述框架](https://en.wikipedia.org/wiki/Resource_Description_Framework) (RDF) 的子集进行序列化和存储，该子集又以 [XML](https://en.wikipedia.org/wiki/XML) 形式表示。

### XMP的優點 {#advantages-of-xmp}

與其他編碼標準和結構描述相比，XMP具有以下優勢：

* XMP型中繼資料功能非常強大，且經過精細處理。
* XMP可讓您一個屬性有多個值。
* XMP已標準化編碼，讓您輕鬆交換中繼資料。
* XMP可擴充。 您可以將其他資訊新增至資產。

XMP標準設計為可擴充，可讓您將自訂的中繼資料型別新增到XMP資料中。 而EXIF則否 — 它有無法擴充的固定屬性清單。

>[!NOTE]
>
>XMP通常不允許內嵌二進位資料型別。 若要在XMP中攜帶二進位資料（例如縮圖影像），這些影像必須以XML易記格式編碼，例如 `Base64`.

### XMP核心概念 {#xmp-core-concepts}

**名稱空間和結構描述**

XMP結構描述是通用XML名稱空間中的一組屬性名稱，包括資料型別和描述性資訊。 XMP結構描述由其XML名稱空間URI識別。 使用名稱空間可防止名稱相同但含義不同的不同結構描述中的屬性之間發生衝突。

例如， **建立者** 兩個獨立設計結構描述中的屬性可能代表建立資產的人，也可能代表建立資產的應用程式(例如Adobe Photoshop)。

**XMP屬性和值**

XMP可能包含一或多個結構描述的屬性。 例如，許多Adobe應用程式使用的典型子集可能包括：

* 都柏林核心結構描述： `dc:title`， `dc:creator`， `dc:subject`， `dc:format`， `dc:rights`
* XMP基本結構描述： `xmp:CreateDate`， `xmp:CreatorTool`， `xmp:ModifyDate`， `xmp:metadataDate`
* XMP許可權管理綱要： `xmpRights:WebStatement`， `xmpRights:Marked`
* XMP媒體管理綱要： `xmpMM:DocumentID`

**替代語言**

XMP讓您能夠新增 `xml:lang` 屬性至文字屬性，以指定文字的語言。

## XMP回寫至轉譯 {#xmp-writeback-to-renditions}

中的此XMP回寫功能 [!DNL Adobe Experience Manager Assets] 會將中繼資料變更複製到原始資產的轉譯。
當您從內變更資產的中繼資料時 [!DNL Assets] 或者，在上傳資產時，變更最初會儲存在資產階層的中繼資料節點中。 回寫功能可讓您將中繼資料變更傳播至資產的所有或特定轉譯。 功能只會回寫那些使用的中繼資料屬性 `jcr` 名稱空間，也就是名為的屬性 `dc:title` 會寫回，但有一個屬性命名為 `mytitle` 不是。

例如，假設您修改了 [!UICONTROL 標題] 標題為的資產屬性 `Classic Leather` 至 `Nylon`.

![元数据](assets/metadata.png)

在這種情況下， [!DNL Assets] 將變更儲存至 **[!UICONTROL 標題]** 中的屬性 `dc:title` 資產階層中儲存的資產中繼資料引數。

![中繼資料儲存在儲存庫的asset節點中](assets/metadata_stored.png)

>[!IMPORTANT]
>
>預設不會在中啟用回寫功能 [!DNL Assets]. 瞭解如何 [啟用中繼資料回寫](#enable-xmp-writeback). 數位資產的MSM無法搭配啟用中繼資料回寫運作。 回寫時，繼承中斷。

### 啟用XMP回寫 {#enable-xmp-writeback}

[!UICONTROL DAM中繼資料回寫] 工作流程用於回寫資產的中繼資料。 若要啟用回寫，請遵循下列三種方法之一：

* 使用啟動器。
* 手動啟動 `DAM MetaData Writeback` 工作流程。
* 將工作流程設定為後處理的一部分。

若要使用「啟動器」，請遵循下列步驟：

1. 以管理員身分，存取 **[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 啟動器]**.
1. 選取 [!UICONTROL 啟動器] 對於 **[!UICONTROL 工作流程]** 欄顯示 **[!UICONTROL DAM中繼資料回寫]**. 按一下 **[!UICONTROL 屬性]** （從工具列）。

   ![選取DAM中繼資料回寫啟動器，以修改其屬性並加以啟動](assets/launcher-properties-metadata-writeback1.png)

1. 選取 **[!UICONTROL 啟動]** 於 **[!UICONTROL 啟動器屬性]** 頁面。 单击“**[!UICONTROL 保存并关闭]**”。

若要隻手動將工作流程套用至資產一次，請套用 [!UICONTROL DAM中繼資料回寫] 工作流程左側邊欄。

若要將工作流程套用至所有上傳的資產，請將工作流程新增至後期處理設定檔。

<!-- Commenting for now. Need to document how to enable metadata writeback. See CQDOC-17254.

### Enable XMP writeback {#enable-xmp-writeback}

To enable the metadata changes to be propagated to the renditions of the asset when uploading it, modify the **[!UICONTROL Adobe CQ DAM Rendition Maker]** configuration in Configuration Manager.

1. To open Configuration Manager, access `https://[aem_server]:[port]/system/console/configMgr`.
1. Open the **[!UICONTROL Adobe CQ DAM Rendition Maker]** configuration.
1. Select the **[!UICONTROL Propagate XMP]** option, and then save the changes.

### Enable XMP write-back for specific renditions {#enable-xmp-writeback-for-specific-renditions}

To let the XMP write-back feature propagate metadata changes to select renditions, specify these renditions to the [!UICONTROL XMP Writeback Process] workflow step of DAM Metadata WriteBack workflow. By default, this step is configured with the original rendition.

For the XMP write-back feature to propagate metadata to the rendition thumbnails 140.100.png and 319.319.png, perform these steps.

1. Tap/click the Experience Manager logo, and then navigate to **[!UICONTROL Tools]** &gt; **[!UICONTROL Workflow]** &gt; **[!UICONTROL Models]**.
1. From the Models page, open the **[!UICONTROL DAM Metadata Writeback]** workflow model.
1. In the **[!UICONTROL DAM Metadata Writeback]** properties page, open the **[!UICONTROL XMP Writeback Process]** step.
1. In the **[!UICONTROL Step Properties]** dialog box, tap/click the **[!UICONTROL Process]** tab.
1. In the **[!UICONTROL Arguments]** box, add `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`, and then tap/click **[!UICONTROL OK]**.

   ![step_properties](assets/step_properties.png)

1. Save the changes.
1. To regenerate the Pyramid TIFF (PTIFF) renditions for Dynamic Media images with the new attributes, add the **[!UICONTROL Dynamic Media Process Image Assets]** step to the DAM Metadata write-back workflow. PTIFF renditions are only created and stored locally in a Dynamic Media Hybrid implementation.

1. Save the workflow.

The metadata changes are propagated to the renditions renditions thumbnail.140.100.png and thumbnail.319.319.png of the asset, and not the others.
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
