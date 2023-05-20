---
title: CIF 创作快速入门
description: CIF 创作快速入门
exl-id: 0bef4d8c-0ad3-4ec8-ab08-8c83203b3b68
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 2%

---

# AEM CIF製作快速入門 {#getting-started}

瞭解AEM CIF編寫。

## 迄今为止的故事 {#story-so-far}

在此AEM Content and Commerce歷程的上一份檔案中， [瞭解AEM內容與商務](/help/commerce-cloud/introduction.md)您已瞭解Headless CMS的基本理論，現在應瞭解AEM內容與商務的基本概念。

本文基於這些基礎之上。

## 目标 {#objective}

本檔案可協助您瞭解如何使用CIF進行內容與商務特定編寫。 閱讀本檔案後，您應該：

* 瞭解使用Universal Editor編寫CIF的概念
* 如何使用產品和類別選擇器存取AEM中的產品目錄資料
* 如何使用產品駕駛艙和AEM Omnisearch存取內容和商務資料

## 在通用編輯器中編寫CIF {#cif-authoring}

CIF擴充了Universal Editor，提供在不離開內容的情況下存取即時產品資料的功能：

開啟側面板，然後從下拉式清單中選取「產品」。
![選取產品型別](assets/asset-finder-overview.png)

您可以瀏覽產品目錄或使用全文檢索搜尋欄位來尋找產品。
![產品型別](assets/asset-finder-search.png)

產品可放置在支援產品放置的元件上（例如產品Teaser、產品輪播），而頁面會自動建立產品Teaser元件。

## 產品和類別選擇器 {#pickers}

如果Commerce元件或AEM後台對話方塊中需要產品和類別資料，AEM作者可以使用作為UI元素的選擇器，輕鬆搜尋和選取產品目錄資料。

### 产品选取器

按一下資料夾圖示會開啟選取器強制回應視窗UI （例如產品Teaser）
![產品選取器](assets/product-picker-open.png)

瀏覽左側的目錄結構或搜尋，即可找到產品。 全文檢索搜尋將會遵循所選的類別，並將搜尋結果限制在此類別。
![產品選取器資料夾](assets/product-picker-folders.png)

具有變異的產品會以資料夾圖示標籤，可以按一下該圖示顯示所有變異。
![產品選取器變體](assets/product-picker-variants.png)
![產品選取器變體已開啟](assets/product-picker-variants-open.png)

### 類別選取器

像產品選擇器一樣運作。 按一下資料夾圖示會開啟選取器強制回應UI （例如類別輪播）
![類別選取器](assets/category-picker-open.png)

瀏覽左側的目錄結構並選取類別。
![類別選取器](assets/category-picker-folders.png)

## 产品 Cockpit {#cockpit}

產品駕駛艙是快速存取產品目錄及其所有豐富內容的中心位置。 您將在接下來的其中一個單元中學習如何使用內容擴充產品資料。 現在，讓我們專注於存取產品資料。

從主功能表中按一下商務，以檢視所有附加產品目錄的清單。
![商務功能表專案](assets/commerce-menu-item.png)

這會顯示所有連線產品目錄的清單。
![駕駛艙整合式目錄](assets/cockpit-Integrated-catalogs.png)

產品目錄依預設會顯示所有產品的全部第一級類別。 按一下類別會開啟該類別，其中包含所有相關產品和子類別，包括其產品。
![駕駛艙產品目錄](assets/cockpit-product-catalog.png)

您可以按一下屬性圖示來開啟產品屬性。 將滑鼠游標停留在產品圖磚上會顯示圖示。
![駕駛艙產品屬性](assets/cockpit-properties.png)

所有產品屬性都是唯讀的，因為資料會從連線的後端即時載入。 變更產品屬性必須在後端系統（記錄系統）中完成。 索引標籤 **變數** 只有在產品有變化時才會出現。 按一下標籤會顯示所有變數及其屬性。
![駕駛艙產品變體](assets/cockpit-properties-variants.png)

其餘標籤會顯示與產品相關聯的所有AEM內容。 我們將在下一個模組中討論這些標籤。

## AEM Omnisearch {#omnisearch}

使用Omnisearch是一種透過全文搜尋來尋找AEM內容的簡單方法。 CIF延伸Omnisearch，以全文搜尋產品目錄及其相關AEM內容。
![商務功能表專案](assets/omnisearch.png)

Omnisearch會在商務後端執行全文檢索搜尋，以尋找所有相關產品。 結果會列在底下 **檢視所有產品**. Omnisearch也會搜尋AEM中與搜尋到的產品相關聯的內容。 結果將列在各自的AEM類別下。 在此範例中，一個內容片段與產品相關。

## 后续内容 {#what-is-next}

現在您已完成此部分歷程，您應：

* 瞭解使用Universal Editor編寫CIF的概念
* 如何使用產品和類別選擇器存取AEM中的產品目錄
* 如何使用產品駕駛艙和AEM Omnisearch存取內容和商務資料

在此知識的基礎上繼續您的歷程，接下來檢視檔案 [管理產品目錄頁面和範本](catalog-templates.md)，瞭解如何建立及自訂您的第一個產品目錄體驗。

## 其他资源 {#additional-resources}

我們建議您檢閱檔案，繼續下一段歷程 [管理產品目錄頁面和範本](catalog-templates.md)，以下是一些其他可選資源，這些資源對本文檔中提到的一些概念進行了更深入的探究，但並非繼續此歷程所必需的。

* [設定存放區和目錄](/help/commerce-cloud/getting-started.md#catalog)
