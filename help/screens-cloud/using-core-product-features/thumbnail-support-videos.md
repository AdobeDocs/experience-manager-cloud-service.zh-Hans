---
title: Screensas a Cloud Service提供影片的縮圖支援
description: 本頁面說明如何在Screensas a Cloud Service新增影片的縮圖支援。
index: true
exl-id: 7b15d7cc-f089-4008-9039-5f48343a0f20
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 1%

---

# 视频的缩略图支持 {#thumbnail-support-videos}

## 简介 {#introduction}

內容作者可以定義影片的縮圖，以便在適當的團隊正在完成實際影片時，影像可以當做預留位置並正確測試內容播放和目標定位。 如果影片播放失敗，也可以使用該影像。

在視訊元件上新增對縮圖影像的支援，可讓客戶在管道中正確新增包含實際內容的有效元件，以及在實際傳送視訊之前執行任何目標定位設定。

>[!NOTE]
>如果在視訊元件上設定縮圖影像，當播放器上的視訊播放失敗時，就會播放縮圖影像。 這可讓您傳遞所需訊息給對象（透過播放內容），而不是完全略過。

縮圖支援可讓您：

* 影片尚未準備就緒，或您不一定要測試播放器上的大型資產下載時，請準備管道體驗

* 設定遞補機制，以防裝置上發生播放問題。

## 在視訊中使用縮圖 {#using-thumbnails}

>[!IMPORTANT]
>**前提条件**
>在您瞭解如何使用影片的縮圖之前，請務必先瞭解如何在Screensas a Cloud Service專案中為頻道建立影片轉譯。 另請參閱 [此處](/help/screens-cloud/configuring/creating-screens-video-renditions-cloud-service.md) 以取得更多詳細資料。

請依照下列步驟，在視訊中使用縮圖：

1. 導覽至現有的Screens頻道或建立新頻道。

   >[!NOTE]
   >若要瞭解如何建立管道及新增內容至管道，請參閱 [在Screens中建立和管理頻道as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/create-content/creating-channels-screens-cloud.html?lang=en).

1. 選取管道並按一下 **編輯** 以開啟編輯器。

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-1.png)

1. 新增或編輯現有的視訊元件，如下圖所示。

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-2.png)

1. 選取視訊並按一下 *扳手* 圖示以開啟視訊屬性。

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-3.png)

1. 此 **視訊** 對話方塊開啟，您將在其中檢視 **縮圖** 拖放區域。

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-4.png)

1. 將影像從資產選擇器拖放至 **縮圖** 拖放區域並按一下 **完成**.

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-5.png)

1. 按一下 **預覽**.

1. 如果元件上設定了視訊，則視訊將會播放。 如果沒有，且縮圖已設定，則會播放縮圖。 否則，會視為未設定元件，並將略過該元件。

## 在視訊中使用縮圖時支援的使用案例 {#understand-use-case}

影片中的縮圖支援下列使用案例：

* 未設定任何專案的視訊元件將被跳過。

* 只有縮圖集的視訊元件將會播放縮圖。

* 同時具有視訊（如果視訊具有正確的轉譯）和縮圖集的視訊元件將會播放視訊。

* 若發生播放錯誤，包含視訊集的視訊元件將會播放縮圖，如果未設定縮圖，則直接跳至下一個專案。
