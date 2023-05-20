---
title: 构建产品体验
description: 瞭解如何建立產品體驗。
exl-id: 4ae70e40-fdf1-4a37-b4dd-0c4882d77908
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1155'
ht-degree: 4%

---

# 构建产品体验 {#building-experiences}

瞭解如何管理產品體驗。

## 迄今为止的故事 {#story-so-far}

在AEM Content and Commerce歷程的上一個檔案中， [管理分階段產品目錄體驗](staged-catalog.md)，您已瞭解如何管理分階段的產品目錄體驗。

## 目标 {#objective}

本檔案可協助您瞭解如何建立產品內容和體驗。

## 產品體驗管理 {#management}

「產品體驗管理」是在AEM中將產品資料（由PIM或商務解決方案擁有）與行銷內容搭配使用的學科。 然後，這種包含內容的豐富產品資料可用於各種管道，以建立沈浸式購物體驗。

在AEM中，您可以建立各種型別的內容，並將其連結至產品目錄。 可輕鬆探索及使用相關內容，進而提高生產力。

### Assets {#assets}

基本上，有兩種資產型別與產品相關：產品與行銷。 產品資產通常由商家管理，並專注於顯示產品（大多在中性背景前）。 資產可在商務解決方案或AEM Assets中管理（透過與商務/pim解決方案的Assets整合）。

行銷資產與促銷及使用通常由行銷擁有的產品有關。 例如，顯示特定內容（「戶外秋季系列」）中的多種產品（「商店外觀」）或操作說明檔案。 CIF可讓您輕鬆將任何AEM資產與產品目錄物件連結。

開啟資產屬性並切換至 **商務** 標籤。 此索引標籤可讓您管理與產品的關聯。 選取器下方的表格會提供連結物件的其他資訊（只有選取範圍能看見）。 按一下詳細資訊圖示，即可完整檢視產品駕駛艙。 若要關聯新物件，請按一下產品選擇器圖示（資料夾圖示）、選取物件並關閉選擇器。

![pem資產](assets/pem-assets.png)

### 体验片段 {#experience-fragments}

體驗片段是大規模建立可重複使用或個別產品內容的絕佳方式。 關聯的運作方式與資產類似。 開啟屬性並切換至 **商務** 標籤。 此索引標籤可讓您管理與產品和類別的關聯。 選取器下方的表格會提供連結物件的其他資訊（只有選取專案才可見）。 按一下詳細資訊圖示，即可完整檢視產品駕駛艙。 若要關聯新物件，請按一下產品選擇器圖示（資料夾圖示）、選取物件並關閉選擇器。

![pem xf](assets/pem-xf.png)

### 内容片段 {#content-fragments}

內容片段是任何結構化內容的最佳內容型別。 這可用來使用其他行銷資料來增強外部產品資料，或是以Headless方式建立內容。 內容片段與產品目錄物件的關聯是透過內容片段模式編輯器中的產品或類別參考型別進行。 只需在模型上拖放正確的參考型別並設定欄位即可。 這些型別支援單一或多重選取。

![pem cf模型](assets/pem-cf-model.png)

如果您根據此模型建立新的內容片段，這些參考型別會提供使用各自選擇器來選取正確物件的簡單方法。

![pem cf](assets/pem-cf.png)

### 产品 Cockpit {#product-cockpit}

我們已將產品Cockpit （或主控台）引入前幾個模組中。 駕駛艙不僅可讓您輕鬆瀏覽產品目錄，還可在一個位置檢視所有相關的AEM內容。 前往產品主控台，並開啟具有關聯內容之產品的屬性。 切換到個別標籤以檢視相關聯的內容。

![pem駕駛艙](assets/pem-cockpit.png)

按一下動作圖示即可在新的瀏覽器分頁中開啟該內容片段。

## 豐富個別產品和類別頁面 {#enrich}

在前面的單元中，您已瞭解如何使用多個產品目錄範本。 多個範本是建立不同範本的絕佳方式，但在許多情況下並不需要。 在許多情況下，個別內容的相同範本可以與預留位置結合使用。 cif支援內容片段和體驗片段的預留位置。

讓我們從體驗片段預留位置開始。 在AEM編輯器中開啟產品範本。 拖放 **Commerce體驗片段** 元件，然後開啟「設定」對話方塊。

![pem預留位置](assets/pem-placeholder.png)

開啟元件的對話方塊，並輸入此預留位置的名稱。 需要預留位置名稱，可讓您視需要新增任意數量的預留位置。

![pem XF對話方塊](assets/pem-dialog-xf.png)

開啟您在上一步中與產品相關聯的體驗片段。 開啟屬性並切換至商務標籤。 在下方輸入相同的預留位置名稱 **目錄預留位置位置**.

![pem xf](assets/pem-xf.png)

現在拖放 **Commerce內容片段** 元件並開啟「設定」對話方塊。

![pem CF對話方塊](assets/pem-dialog-cf.png)

此對話方塊正在重複使用核心元件內容片段對話方塊。 在其他資源底下尋找更多資訊。 唯一的區別是 **連結元素** 屬性，可設定內容片段模式中的識別碼欄位（產品SKU或類別UID）。

現在預覽具有關聯內容片段和/或體驗片段的產品頁面。 AEM轉譯頁面時，會根據型別（內容或體驗片段）、識別碼和體驗片段的預留位置名稱查詢每個預留位置。 AEM會使用URL解析器來取得識別碼（產品為SKU，類別為UID）。 如果傳回體驗或內容片段，則會呈現至預留位置位置，否則會忽略預留位置。

![pem結果](assets/pem-result.png)

## 讓內容可供購買 {#making-shoppable}

也可以透過新增商務元件讓一般AEM頁面可供購買。 在AEM中建立新內容頁面，並在編輯器中開啟空白頁面。

![pem空白頁面](assets/pem-page-empty.png)

首先，將產品詳細資料元件拖放至頁面上。 然後切換至Assets側欄，切換至products並選取產品。 將該產品拖放至產品元件上。 這會在內容頁面上顯示一般產品元件。

![pem產品頁面](assets/pem-page-product.png)

如果您已為該產品建立關聯內容，請在「資產」側邊欄中切換至 **關聯的商務內容**. 此索引標籤會顯示與此產品相關聯的所有AEM內容。 這可讓您現在使用任何關聯內容來快速修飾頁面。

![擴充pem頁面](assets/pem-page-enriched.png)

## 历程结束？ {#end-of-journey}

恭喜！您已完成AEM Content and Commerce開發人員歷程！ 您现在应：

* 瞭解如何將任何AEM內容與產品目錄物件建立關聯
* 使用預留位置來個別豐富產品和類別頁面
* 瞭解如何讓內容可供購買，並使用關聯內容索引標籤

您現在可以使用AEM Content and Commerce管理產品體驗。 不過，AEM Content and Commerce有許多其他可用選項。 查看[“其他资源”部分](#additional-resources)中的一些其他资源，详细了解您在此历程中看到的功能。

## 其他资源 {#additional-resources}

* [編寫Commerce體驗](/help/commerce-cloud/authoring/authoring-commerce-experiences.md)
* [产品 Cockpit](/help/commerce-cloud/authoring/product-cockpit.md)
* [內容片段元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=en)
