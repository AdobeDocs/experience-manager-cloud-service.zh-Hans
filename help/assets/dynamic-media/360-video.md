---
title: 360/VR影片
description: 瞭解如何在Dynamic Media中使用360和虛擬現實(VR)影片。
contentOwner: Rick Brough
feature: 360 VR Video
role: User
exl-id: ffd092d3-2188-47b0-a475-8bfa660c03c1
source-git-commit: b37ff72dbcf85e5558eb3421b5168dc48e063b47
workflow-type: tm+mt
source-wordcount: '989'
ht-degree: 0%

---

# 360/VR影片 {#vr-video}

360°影片會同時錄製每個方向的檢視。 它們使用全方位相機或一系列相機拍攝。 在播放期間，在平面顯示器上，使用者可以控制視角；在行動裝置上播放通常套用他們內建的陀螺儀控制。

Dynamic Media包含原生支援，可傳送360個視訊資產。 依預設，檢視或播放不需要額外的設定。 您會使用標準視訊副檔名（例如.mp4、.mkv和.mov）來傳送360視訊。 最常見的轉碼器是H.264。

您可以使用360/VR視訊檢視器來轉譯等角視訊。 如此一來，您就能在房間、屬性、位置、風景、醫療程式等各方面獲得身臨其境的觀賞體驗。

目前不支援空間音訊；如果音訊混合在立體聲中，平衡(L/R)不會隨著客戶變更相機視角而改變。

另請參閱 [透過AEM Assets使用Dynamic Media 360影片和自訂影片縮圖](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-360-video-custom-thumbnail-feature-video-use.html#dynamic-media).

另請參閱 [管理檢視器預設集](/help/assets/dynamic-media/managing-viewer-presets.md).

## 360影片運作中 {#video-in-action}

選取 [360號空間站](https://s7d1.scene7.com/s7viewers/html5/Video360Viewer.html?asset=Viewers/space_station_360-AVS) 開啟瀏覽器視窗並觀看360度影片。 在視訊播放期間，將指標拖曳至新位置以變更視角。

![來自空間站360視訊的視訊影格](assets/6_5_360videoiss_simplified.png)
*來自空間站360的視訊影格*

## 360/VR視訊與Adobe Premiere Pro {#vr-video-and-adobe-premiere-pro}

您可以使用AdobePremier Pro來檢視和編輯360/VR素材。 例如，您可以在場景中正確放置圖志和文字，並套用專為等矩形媒體設計的效果和轉場。

另請參閱 [編輯360/VR影片](https://helpx.adobe.com/premiere-pro/how-to/edit-360-vr-video.html).

## 上傳資產以與360視訊檢視器搭配使用 {#uploading-assets-for-use-with-the-video-viewer}

上傳至360個視訊資產 [!DNL Experience Manager] 標籤為 **多媒體** 資產頁面上，與一般視訊資產類似。

![在卡片檢視中看到的已上傳360視訊資產](assets/6_5_360video-selecttopreview.png)
*在卡片檢視中看到的已上傳360視訊資產。 資產標示為多媒體。*

**上傳資產以搭配360視訊檢視器使用：**

1. 已建立專用於您的360度影片資產的資料夾。
1. [將最適化視訊設定檔套用至資料夾](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders).

   與標準非360度視訊內容相比，轉譯360度視訊內容對來源視訊解析度和編碼轉譯解析度的需求更高。

   您可以使用隨Dynamic Media提供的現成最適化視訊設定檔。 不過，若使用非360視訊檢視器轉譯的相同設定進行編碼，會產生明顯較低的360視訊品質。 因此，如果需要高品質360視訊，請執行下列動作：

   * 理想情況下，您原本的360度影片內容具備下列其中一種解析度：

      * 1080p - 1920 x 1080，稱為Full HD或FHD解析度，或
      * 2160p - 3840 x 2160，稱為4k、UHD或UltraHD解析度。 這種大型顯示器解析度最常出現在高檔電視機和電腦顯示器上。 2160p解析度通常稱為「4k」，因為寬度接近4000畫素。 換句話說，它提供1080p畫素的四倍。
   * [建立自訂最適化視訊設定檔](/help/assets/dynamic-media/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming) 提供更高品質的轉譯。 例如，您可以建立包含下列三個設定的最適化視訊設定檔：

      * 寬度=自動；高度=720；位元速率=2500 kbps
      * Width=auto； Height=1080； Bit rate=5000 kbps
      * 寬度=自動；高度=1440；位元速率=6600 kbps
   * 處理360影片資產專屬資料夾中的360影片內容。

   此方法對使用者的網路和CPU提出了更高的要求。

1. [將視訊上傳至資料夾](/help/assets/manage-video-assets.md#upload-and-preview-video-assets).

<!--

## Overriding the default aspect ratio of 360 videos  {#overriding-the-default-aspect-ratio-of-videos}

For an uploaded asset to qualify as a 360 video that you intend to use with the 360 Video viewer, the asset must have an aspect ratio of 2.

By default, AEM detects video as "360" if its aspect ratio (width/height) is 2.0. If you are an Administrator, you can override the default aspect ratio setting of 2 by setting the optional `s7video360AR` property in CRXDE Lite at the following:

* `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

  * **Property type**: Double
  * **Value**: floating-point aspect ratio, default 2.0.

After you set this property, it takes effect immediately on both existing videos and newly uploaded videos.

The aspect ratio applies to 360 video assets for the asset details page and the [Video 360 Media WCM component](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#dynamic-media-components).

Start by uploading 360 Videos.

-->

## 預覽360度影片 {#previewing-video}

您可以使用「預覽」來檢視向客戶呈現的360影片外觀，並確保影片如預期般運作。

另請參閱 [編輯檢視器預設集](/help/assets/dynamic-media/managing-viewer-presets.md#editing-viewer-presets).

當您對360視訊感到滿意時，可以將其發佈。

另請參閱 [將視訊或影像檢視器內嵌在網頁上](/help/assets/dynamic-media/embed-code.md).
另請參閱 [將URL連結至您的網頁應用程式](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md). 如果您的互動式內容具有具有具有相對URL的連結，尤其是以下連結的連結，則無法連結URL型方法： [!DNL Experience Manager Sites] 頁面。
另請參閱 [將Dynamic Media資產新增至頁面](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

**若要預覽360部影片：**

1. 在 **[!UICONTROL 資產]**，導覽至您建立的現有360影片。 若要以預覽模式開啟，請選取360視訊資產。

   ![在Experience Manager的卡片檢視中看到的已上傳360視訊資產的熒幕擷圖。](assets/6_5_360video-selecttopreview-1.png)

   若要預覽視訊，請選取360度視訊資產。

1. 在預覽頁面頁面的左上角附近，選取下拉式清單，然後選取 **[!UICONTROL 檢視者]**.

   ![選取檢視器以檢視可用視訊檢視器清單的熒幕擷圖。](assets/6_5_360video-preview-viewers.png)

   從「檢視器」清單中選取 **[!UICONTROL Video360_social]**，然後執行下列任一項作業：

   * 若要改變靜態場景的視角，請在視訊上拖曳指標。
   * 若要開始播放，請選取視訊的 **[!UICONTROL 播放]** 按鈕。 播放視訊時，拖曳指標橫跨視訊以改變視角。

   ![使用者選取Video360_Social檢視器以預覽360度視訊的熒幕擷圖。](assets/6_5_360video-preview-video360-social.png)*360度影片截圖。*

   * 從「檢視器」清單中選取 **[!UICONTROL Video360VR]**.

      虛擬現實(VR)視訊是使用虛擬現實耳機存取的沈浸式視訊內容。 和一般視訊一樣，您一開始會使用360度攝影機錄製或擷取視訊，藉此建立VR視訊。
   ![將滑鼠指標暫留在Video360VR Viewer選項上的使用者熒幕擷圖。](assets/6_5_360video-preview-video360vr.png)
   *360 VR視訊熒幕擷圖。*

1. 在預覽頁面的右上角附近，選取 **[!UICONTROL 關閉]**.

## 發佈360度影片 {#publishing-video}

若要使用360視訊，您必須將其發佈。 發佈360影片會啟用URL和內嵌程式碼。 此外，該公司也會將360影片發佈至Dynamic Media雲端，此雲端已與CDN整合，提供可擴充且優異的傳送效能。

另請參閱 [發佈Dynamic Media資產](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md) 以取得發佈360度影片的詳細資訊。
另請參閱 [將視訊或影像檢視器內嵌在網頁上](/help/assets/dynamic-media/embed-code.md).
另請參閱 [將URL連結至您的網頁應用程式](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md). 如果您的互動式內容具有具有具有相對URL的連結，尤其是以下連結的連結，則無法連結URL型方法： [!DNL Experience Manager Sites] 頁面。
另請參閱 [將Dynamic Media資產新增至頁面](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).
