---
title: 設定Workfront和Experience Manager Assets之間的資產中繼資料對應
description: 在Adobe Workfront和Experience Manageras a Cloud Service應用程式之間對應資產中繼資料欄位。 對應中繼資料欄位後，當您從Workfront傳送資產至Experience Manager Assets時，可以在Experience Manager Assets中檢視對應的資產中繼資料。
exl-id: 71400769-b2bc-4f5d-8b6b-a73598e837b4
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '1025'
ht-degree: 4%

---

# 設定Adobe Workfront和Experience Manager Assets之間的資產中繼資料對應 {#asset-metadata-mapping-workfront-aem-assets}

您可以在Adobe Workfront和Experience Manageras a Cloud Service應用程式之間對應資產中繼資料欄位。 對應中繼資料欄位後，當您從Workfront傳送資產至Experience Manager Assets時，可以在Experience Manager Assets中檢視對應的資產中繼資料。

例如，將影像傳送至Experience Manager Assets時，如果您需要保留影像的中繼資料欄位，例如名稱、說明及其在Workfront中的專案，請設定這些欄位，並將其對應至Experience Manager Assets屬性。

**用例**

影像 `add-users-workfront.png` 存在於 `Metadata Syncs` Adobe Workfront應用程式中的專案。 您需要將該影像傳送至Experience Manager Assetsas a Cloud Service，並提供下列中繼資料：

* 项目名称

* 檔名稱

* 檔案說明

## 前提条件 {#prerequisites}

* 擁有Workfront和Experience Manager Assetsas a Cloud Service應用程式的管理員存取權。

* 以下兩者之間的整合： [Workfront和Experience Manager Assetsas a Cloud Service應用程式](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FDocuments%2FAdobe_Workfront_for_Experience_Manager_Assets_Essentials%2Fsetup-asset-essentials.htm&amp;_LANG=enus).

## 在Workfront中設定中繼資料對應 {#set-up-metadata-mapping}

若要為Workfront中的「專案名稱」、「檔名稱」和「檔案描述」欄位設定中繼資料對應：

1. 按一下主要功能表圖示 ![顯示功能表](assets/show-menu.svg) 可在Adobe Workfront應用程式的右上角取得，然後按一下 **[!UICONTROL 設定]**.

1. 選取 **[!UICONTROL 檔案]** 在左側面板中，然後選取 **[!UICONTROL Experience Manager Assets]**.

1. 選取Experience Manager Assets整合，然後按一下 **[!UICONTROL 編輯]**.

1. 按一下 **[!UICONTROL 中繼資料]**. 在 **[!UICONTROL 資產]** 標籤，對應 [!UICONTROL 專案] > [!UICONTROL 名稱] 的Workfront欄位 `wm:projectName` Experience Manager Assets欄位。 如果您找不到完全相符的專案，Adobe建議尋找最符合的專案來對應Workfront和Experience Manager Assets欄位。 您可以避免對應不同資料型別的欄位。 例如，將日期Workfront欄位對應到說明Assets欄位。
1. 對應 [!UICONTROL 檔案] > [!UICONTROL 名稱] 的Workfront欄位 `wm:documentName` Experience Manager Assets欄位。

   ![Workfront中的對應](assets/workfront-metadata-mapping.png)

1. 對應 [!UICONTROL 檔案] > [!UICONTROL 說明] 的Workfront欄位 `dc:description` Experience Manager Assets欄位。

   >[!VIDEO](https://video.tv.adobe.com/v/344255)

## 將影像從Workfront傳送至Experience Manager Assets {#send-image-workfront-assets}

若要將影像從Workfront傳送至Experience Manager Assets：

1. 按一下主要功能表圖示 ![顯示功能表](assets/show-menu.svg) 可在Adobe Workfront應用程式的右上角取得，然後按一下 **[!UICONTROL 專案]**.

1. 按一下 **[!UICONTROL 新增專案]** 以建立新專案。

1. 按一下 **[!UICONTROL 檔案]** 左側窗格中可用的選項，拖曳並選取您需要傳送至Experience Manager Assets的影像。

1. 按一下 **[!UICONTROL 傳送至]**，然後選擇Experience Manager Assets Essentials整合名稱。

   ![发送到 AEM](assets/send-to-aem.png)

1. 選擇資產的目的地資料夾，然後按一下 **[!UICONTROL 選取資料夾]**.

1. 单击“**[!UICONTROL 保存]**”。

## 在Experience Manageras a Cloud Service中設定資產中繼資料對應 {#metadata-mapping-aem}

晚於 [在Adobe Workfront中設定資產中繼資料對應](#set-up-metadata-mapping)，您必須在Experience Manager Assetsas a Cloud Service應用程式中使用相同的對應，才能顯示影像的適當中繼資料結果。

使用Experience Manager Assets中的中繼資料結構描述來執行中繼資料對應。 您可以編輯新新增或現有的中繼資料結構表單。 中繼資料結構表單包含索引標籤和索引標籤內的表單專案。 您可以將這些表單專案對應/設定到CRX存放庫中中繼資料節點內的欄位。 您可以將索引標籤或表單專案新增到中繼資料結構表單。 如需詳細資訊，請參閱 [中繼資料結構](metadata-schemas.md).

若要使用Experience Manager Assetsas a Cloud Service中的新中繼資料表單設定中繼資料對應：

1. 導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 中繼資料結構]**.

1. 按一下 **[!UICONTROL 建立]** （從工具列）。 在對話方塊中，提供結構表單的標題並按一下 **[!UICONTROL 建立]** 以完成表單建立程式。

1. 選取結構表單，然後按一下 **[!UICONTROL 編輯]**.

1. （選用）在中繼資料結構表單編輯器上，按一下 `+` 為Workfront欄位建立新索引標籤。

1. 按一下 **[!UICONTROL 建置表單]** 定位並拖曳 **[!UICONTROL 單行文字]** 元件至表單。 按一下表單中的元件。 在 **[!UICONTROL 建置表單]** 標籤：

   1. 指定 `Project Name` 在 **[!UICONTROL 欄位標籤]** 欄位。

   1. 指定 `./jcr:content/metadata/wm:projectName` 在 **[!UICONTROL 對應至屬性]** 欄位。 建議使用以下範本，在Experience Manger Assets中定義欄位對應：
      `./jcr:content/metadata/<mapping defined for the field in workfront>`。

      在Workfront中設定對應時，您已對應 `wm:projectName` Experience Manager Assets欄位至專案>命名Workfront欄位。

      `wm` 是指名稱空間名稱和 `projectName` 是指屬性標題。 使用 `namespace:propertyTitle` 定義中繼資料欄位對應的格式。

      ![发送到 AEM](assets/metadata-schema-mapping.png)

1. 按一下 **[!UICONTROL 建置表單]** 定位並拖曳 **[!UICONTROL 單行文字]** 元件至表單。 按一下表單中的元件。 在 **[!UICONTROL 建置表單]** 標籤：

   1. 指定 `Document Name` 在 **[!UICONTROL 欄位標籤]** 欄位。

   1. 指定 `./jcr:content/metadata/wm:documentName` 在 **[!UICONTROL 對應至屬性]** 欄位。
在Workfront中設定對應時，您已對應 `wm:documentName` 「檔案>命名Experience Manager Assets」欄位中的「Workfront」欄位。

1. 按一下 **[!UICONTROL 建置表單]** 定位並拖曳 **[!UICONTROL 多行文字]** 元件至表單。 按一下表單中的元件。 在 **[!UICONTROL 建置表單]** 標籤：

   1. 指定 `Document Description` 在 **[!UICONTROL 欄位標籤]** 欄位。

   1. 指定 `./jcr:content/metadata/dc:description` 在 **[!UICONTROL 對應至屬性]** 欄位。
在Workfront中設定對應時，您已對應 `dc:description` 「檔案>說明」Workfront欄位的「Experience Manager Assets」欄位。

1. 按一下 **[!UICONTROL 儲存]** 以儲存變更。

   >[!VIDEO](https://video.tv.adobe.com/v/344314)

## 將中繼資料設定套用至影像資料夾 {#apply-metadata-settings-image-folder}

在Experience Manageras a Cloud Service應用程式中設定中繼資料設定後，將這些設定套用至 [包含從Workfront應用程式傳送之影像的資料夾](#send-image-workfront-assets).

若要將中繼資料設定套用至影像資料夾：

1. 導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 中繼資料結構]**.

1. 從可用清單中選取中繼資料結構，然後按一下 **[!UICONTROL 套用至資料夾]**.

1. 選取目標資料夾 [影像是從Adobe Workfront應用程式傳送](#send-image-workfront-assets) 並按一下 **[!UICONTROL 套用]**.

您可以導覽至Experience Manager Assets中的影像，並檢視與影像相關聯的中繼資料。 選取影像並按一下 **[!UICONTROL 屬性]** 以檢視影像中繼資料。

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
