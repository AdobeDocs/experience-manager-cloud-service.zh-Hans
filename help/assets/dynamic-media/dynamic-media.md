---
title: 使用 Dynamic Media
description: 瞭解如何使用Dynamic Media傳送資產，以便在網路、行動裝置和社交網站上使用。
contentOwner: Rick Brough
role: Admin,User
exl-id: 3ec3cb85-88ce-4277-a45c-30e52c75ed42
source-git-commit: b37ff72dbcf85e5558eb3421b5168dc48e063b47
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 6%

---

# 使用 Dynamic Media {#working-with-dynamic-media}

[Dynamic Media](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html) 協助提供豐富的視覺化銷售和行銷資產（隨選提供），可自動調整規模，以因應網路、行動裝置和社交網站的使用需求。 Dynamic Media使用一組主要來源資產，透過其全球性、可擴充、效能最佳化的網路，即時產生並傳送多種多樣的豐富內容。

Dynamic Media提供互動式檢視體驗，包括縮放、360度旋轉和視訊。 Dynamic Media以獨特方式整合Adobe Experience Manager數位資產管理(Assets)解決方案的工作流程，以簡化及簡化數位行銷活動管理流程。

<!-- >[!NOTE]
>
>A Community article is available on [Working with Adobe Experience Manager and Dynamic Media](https://helpx.adobe.com/experience-manager/using/aem_dynamic_media.html). -->

## 您可以使用Dynamic Media做什麼 {#what-you-can-do-with-dynamic-media}

Dynamic Media可讓您在發佈資產之前先管理資產。 中會詳細說明如何使用一般資產 [使用數位資產](/help/assets/manage-digital-assets.md). 一般主題包括上傳、下載、編輯和發佈資產；檢視和編輯屬性，以及搜尋資產。

僅限Dynamic Media的功能包括下列專案：

* [传送横幅](carousel-banners.md)
* [图像集](image-sets.md)
* [交互式图像](interactive-images.md)
* [交互式视频](interactive-videos.md)
* [混合媒体集](mixed-media-sets.md)
* [全景图像](panoramic-images.md)

* [旋转集](spin-sets.md)
* [视频](video.md)
* [傳遞Dynamic Media資產](delivering-dynamic-media-assets.md)
* [管理資產](managing-assets.md)
* [使用快速檢視建立自訂快顯視窗](custom-pop-ups.md)

另請參閱 [設定Dynamic Media](administering-dynamic-media.md).

<!-- 

OBSOLETE UNTIL INTEGRATING SCENE7 TOPIC GETS A MAJOR UPDATE
>[!NOTE]
>
>To understand the differences between using Dynamic Media and integrating Dynamic Media Classic with AEM, see [Dynamic Media Classic integration versus Dynamic Media](/help/sites-cloud/administering/integrating-scene7.md#aem-scene-integration-versus-dynamic-media).

-->

## 啟用Dynamic Media與停用Dynamic Media {#dynamic-media-on-versus-dynamic-media-off}

您可以透過下列特性來判斷是否已啟用（開啟） Dynamic Media：

* 下載或預覽資產時，可使用動態轉譯。
* 影像集、迴轉集、混合媒體集可供使用。
* 已建立PTIFF轉譯。

當您按一下影像資產時，啟用Dynamic Media的資產檢視會有所不同。 Dynamic Media使用隨選HTML5檢視器。

### 動態轉譯 {#dynamic-renditions}

動態轉譯，例如影像和檢視器預設集(在 **[!UICONTROL 動態]**)在啟用Dynamic Media時可供使用。

![chlimage_1-358](assets/chlimage_1-358.png)

### 影像集、旋轉集、混合媒體集 {#image-sets-spins-sets-mixed-media-sets}

如果啟用Dynamic Media，則可使用影像集、迴轉集和混合媒體集。

![chlimage_1-359](assets/chlimage_1-359.png)

### PTIFF轉譯 {#ptiff-renditions}

啟用Dynamic Media的資產包括 `pyramid.tiffs`.

![chlimage_1-360](assets/chlimage_1-360.png)

### 資產檢視變更 {#asset-views-change}

啟用Dynamic Media後，您可以按一下 `+` 和 `-` 按鈕。 您也可以按一下/點選以放大特定區域。 「回覆」會將您帶至原始版本，您可以按一下對角線箭頭，使影像變成全熒幕。 Dynamic Media啟用顯示如下：

![chlimage_1-361](assets/chlimage_1-361.png)

停用Dynamic Media後，您可以放大和縮小並還原為原始大小：

![chlimage_1-362](assets/chlimage_1-362.png)
