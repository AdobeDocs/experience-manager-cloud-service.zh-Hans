---
title: 产品 Cockpit
description: 使用產品駕駛艙
exl-id: 6dbf039c-e040-48f1-88f3-ebbd70cdf94d
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 3%

---

# 产品 Cockpit {#product-cockpit}

## 概述 {#overview}

產品駕駛艙提供連結產品目錄和相關內容的統一總覽。 所有關聯內容都有連結，可從駕駛艙快速存取。

分階段產品資料包含未來的任何突變，例如新類別、產品或更新的屬性。

>[!NOTE]
>
>產品目錄一詞可與商務商店、商店檢視和類似運算式互換。

## 配置 {#configuration}

產品目錄需在AEM中設定。 另請參閱 [設定存放區和目錄](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content-and-commerce/storefront/getting-started.html?#catalog) 以取得詳細資訊。

啟用分階段目錄功能需要驗證。 另請參閱 [快速入門](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content-and-commerce/storefront/getting-started.html) 以取得詳細資訊。

>[!NOTE]
>
>只有支援權杖式驗證的Adobe Commerce和第三方聯結器才提供分階段目錄功能。

## 開啟產品駕駛艙 {#opening-product-cockpit}

存取產品駕駛艙最簡單的方式是透過AEM主功能表中的「商務」功能表。 也可以使用Omnisearch （搜尋商務）或opening `https://<yourAEMInstance>/commerce.html`.

![AEM功能表](../assets/aem-menu.png)

## 瀏覽產品目錄 {#browsing-product-catalogs}

產品駕駛艙會依產品目錄結構以階層式方式組織。 第一個層級顯示所有已設定產品目錄的目錄根層級，包括商務後端的中繼資訊。

![已設定的目錄](../assets/catalog-overview.png)

按一下類別時，會載入所點選類別的子系。

![類別子項](../assets/catalog-category-children.png)

如果可用，按一下產品將會載入產品變數。

![產品變數](../assets/catalog-product-variation.png)

>[!NOTE]
>
>AEM中的產品目錄資料是指透過設定的商務端點即時擷取的資料。 AEM中未儲存任何產品目錄資料。

## 搜尋產品目錄 {#searching-product-catalog}

左側篩選索引標籤中提供完整產品目錄的全文檢索搜尋，以快速尋找產品。

![搜索](../assets/search-cockpit.png)

## 瀏覽分階段產品目錄 {#staged-product-catalogs}

依預設，產品駕駛艙會顯示即時產品目錄資料。 使用左側篩選索引標籤中的「階段目錄」將會載入任何所選日期的產品目錄。

![暫存目錄](../assets/staged-cockpit.png)

## 產品目錄屬性 {#catalog-properties}

按一下產品或類別的屬性圖示會開啟所選物件的屬性檢視。 產品變體的開啟屬性等於開啟主要產品屬性。

### Commerce標籤 {#tabs}

一般和變體標籤會顯示來自商務後端的預先定義商務屬性。 此資料(包括 變體)是AEM中的唯讀資料，因為記錄系統是商務後端。 變體索引標籤只會針對具有變體的產品顯示，並顯示所有變體的清單。

![目錄屬性](../assets/catalog-properties.png)

### AEM內容標籤 {#content-tabs}

這些按AEM內容型別（體驗片段、內容片段、相關資產）分組的標籤會顯示與商業物件相關聯的AEM內容。 「檢視詳細資料」動作會開啟含有所選內容的新瀏覽器標籤。

![內容屬性](../assets/content-properties.png)
