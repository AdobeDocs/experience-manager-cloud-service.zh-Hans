---
title: Dynamic Media 中的视频
description: 瞭解如何在Dynamic Media中使用影片。 檢閱編碼視訊、將視訊發佈至YouTube、檢視視訊報表，以及將隱藏式字幕、字幕或章節標籤新增至視訊的最佳作法。
contentOwner: Rick Brough
feature: Video Profiles
role: User
exl-id: 0d5fbb3e-b763-415f-8c69-ea36445f882b
source-git-commit: 124b363fe341199fdc9b25d25bbf2a9bc8f87d87
workflow-type: tm+mt
source-wordcount: '5868'
ht-degree: 2%

---

# 视频 {#video}

本節說明如何在Dynamic Media中使用視訊。

## 快速入門：影片 {#quick-start-videos}

下列逐步工作流程說明可協助您快速上手並執行Dynamic Media中的最適化視訊集。 每個步驟之後，都有主題標題的互動參照，您可以在其中找到更多資訊。

>[!NOTE]
>
>在Dynamic Media中處理視訊之前，請確定您的Adobe Experience Manager管理員已啟用並設定Dynamic MediaCloud Services。
>
>* 另請參閱 [設定Dynamic MediaCloud Services](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services) 在設定Dynamic Media和 [疑難排解Dynamic Media](/help/assets/dynamic-media/troubleshoot-dm.md).
>


1. **上傳您的Dynamic Media影片** 方法是執行下列動作：

   * 建立您自己的視訊編碼設定檔。 或者，您只需使用預先定義的 _自我調整視訊編碼_ Dynamic Media隨附的設定檔。

      * [建立視訊編碼設定檔](/help/assets/dynamic-media/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming).
      * 進一步瞭解 [視訊編碼的最佳作法](#best-practices-for-encoding-videos).
   * 將視訊處理設定檔與您要上傳主要來源視訊的一或多個資料夾建立關聯。

      * [將視訊設定檔套用至資料夾](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders).
      * 進一步瞭解 [組織數位資產](/help/assets/organize-assets.md).
   * 將您的主要來源視訊上傳至資料夾。 將視訊新增至資料夾時，會根據您指派至資料夾的視訊處理設定檔來編碼視訊。

      * Dynamic Media主要支援長度上限為30分鐘，最小解析度大於25 x 25的短影片。
      * 您可以上傳每個檔案最多15 GB的視訊檔案。
      * [上傳您的影片](/help/assets/manage-video-assets.md#upload-and-preview-video-assets).
      * 進一步瞭解 [支援的輸入檔案格式](/help/assets/file-format-support.md).
   * 監視方式 [視訊編碼正在進行](#monitoring-video-encoding-and-youtube-publishing-progress) 從資產或工作流程檢視。




1. **管理您的Dynamic Media影片** 執行下列任一項作業：

   * 組織、瀏覽和搜尋視訊資產

      * [組織數位資產](/help/assets/organize-assets.md)
      * [搜尋視訊資產](/help/assets/search-assets.md#custompredicates) 或 [搜尋資產](/help/assets/manage-digital-assets.md#search-assets)
   * 預覽和發佈視訊資產

      * 檢視視訊的來源視訊和已編碼轉譯專案及其相關縮圖：
         [預覽影片](/help/assets/manage-video-assets.md#upload-and-preview-video-assets) 或 [預覽資產](/help/assets/dynamic-media/previewing-assets.md)
         [管理視訊轉譯](/help/assets/manage-digital-assets.md#managing-renditions)

      * [管理檢視器預設集](/help/assets/dynamic-media/managing-viewer-presets.md)
      * [發佈資產](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)
   * 使用視訊中繼資料

      * 編輯視訊的屬性，例如標題、說明和標籤、自訂中繼資料欄位：
         [編輯視訊屬性](/help/assets/manage-digital-assets.md#editing-properties)

      * [管理數位資產的中繼資料](/help/assets/manage-metadata.md)
      * [元数据架构](/help/assets/metadata-schemas.md)
   * 檢閱、核准和註釋視訊，並維持完整的版本控制

      * [為影片加上註釋](/help/assets/manage-video-assets.md#annotate-video-assets) 或 [為資產加上註釋](/help/assets/manage-digital-assets.md#annotating)

      * [建立版本](/help/assets/manage-digital-assets.md#asset-versioning)
      * [在資產上啟動工作流程](/help/assets/manage-digital-assets.md#starting-a-workflow-on-an-asset)

      * [檢閱資料夾資產](/help/assets/bulk-approval.md)
      * [项目](/help/sites-cloud/authoring/projects/overview.md)




1. **發佈您的Dynamic Media影片** 執行下列任一項作業：

   * 如果您使用Experience Manager做為WCM （網頁內容管理）系統，可以直接將視訊新增至網頁。

      * [新增視訊至您的網頁](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).
   * 如果您使用協力廠商網站內容管理系統，您可以將影片連結或內嵌至網頁。

      * 使用URL整合視訊：
         [将 URL 关联到您的 Web 应用程序](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md).

      * 使用網頁上的內嵌程式碼整合視訊：
         [將視訊檢視器內嵌在網頁上](/help/assets/dynamic-media/embed-code.md).
   * [產生視訊報表](#viewing-video-reports).

   * [新增註解至視訊](#adding-captions-to-video).



## 在Dynamic Media中使用視訊 {#working-with-video-in-dynamic-media}

Dynamic Media中的視訊是端對端解決方案，可讓您輕鬆發佈高品質的最適化視訊，以便在多個熒幕（包括桌上型電腦、平板電腦和行動裝置）上串流。 「自我調整視訊集」會將使用不同位元速率和格式（例如400 kbps、800 kbps和1000 kbps）編碼的相同視訊版本分組。 桌上型電腦或行動裝置會偵測到可用的頻寬。

例如，在iOS行動裝置上，它會偵測3G、4G或Wi-Fi等頻寬。 之後，它會從「自我調整視訊集」內的各種視訊位元速率中，自動選取正確的編碼視訊。 影片會串流至桌上型電腦、行動裝置或平板電腦。

此外，如果桌上型電腦或行動裝置上的網路狀況改變，視訊品質會自動動態切換。 此外，如果客戶在桌上型電腦進入全熒幕模式，Adaptive Video Set會使用更好的解析度來回應，以改善客戶的觀看體驗。 對於在多個熒幕和裝置上播放Dynamic Media視訊的客戶，使用「最適化視訊集」可提供最佳播放方式。

視訊播放器用來決定要播放或播放期間要選取已編碼視訊的邏輯，是根據下列演演算法：

1. 視訊播放器會根據位元速率（最接近在播放器本身中為「初始位元速率」設定的值）載入初始視訊片段。
1. 視訊播放器會根據使用下列條件的頻寬速度變更進行切換：

   1. 播放器會挑選低於或等於預估頻寬的最高頻寬資料流。
   1. 播放器只考慮80%的可用頻寬。 不過，如果調高，則比較保守的設定是70%，以避免高估並立即調回。

如需演演算法的詳細技術資訊，請參閱 [https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp](https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp)

若用於管理單一視訊和自我調整視訊集，支援下列專案：

* 從多種支援的視訊格式和音訊格式上傳視訊，並將視訊編碼為MP4 H.264格式，以便跨多個熒幕播放。 您可以使用預先定義的自我調整視訊預設集、單一視訊編碼預設集，或自訂您自己的編碼來控制視訊的品質和大小。

   * 產生最適化視訊集時，其中會包含MP4視訊。
   * **注意**：主要/來源視訊未新增至最適化視訊集。

* 所有HTML5視訊檢視器中的視訊字幕。
* 使用完整的中繼資料支援來組織、瀏覽和搜尋視訊，以有效管理視訊資產。
* 將最適化視訊集傳送至網頁版、桌上型電腦、平板電腦和行動裝置。

各種iOS平台均支援最適化視訊串流。 另請參閱 [Dynamic Media檢視器參考指南](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/c-html5-video-reference.html).

<!-- OUTDATED 2/28/22 BASED ON CQDOC-18692 Dynamic Media supports mobile video playback for MP4 H.264 video. You can find BlackBerry&reg; devices that support this video format at the following: [Supported video formats on BlackBerry&reg;](https://support.blackberry.com/kb/articleDetail?ArticleNumber=000005482).

OUTDATED 2/28/22 BASED ON CQDOC-18692 You can find Windows&reg; devices that support this video format at the following [Supported video formats on Windows&reg; Phone](https://docs.microsoft.com/en-us/windows/uwp/audio-video-camera/supported-codecs). -->

* 使用Dynamic Media視訊檢視器預設集播放視訊，包括下列專案：

   * 單一視訊檢視器。
   * 結合視訊和影像內容的混合媒體檢視器。

* 設定視訊播放器以符合您的品牌需求。
* 使用簡單URL或內嵌程式碼將視訊整合至您的網站、行動網站或行動應用程式。

另請參閱 [動態視訊播放](https://s7d9.scene7.com/s7/uvideo.jsp?asset=GeoRetail/Mop_AVS&amp;config=GeoRetail/Universal_Video1&amp;stageSize=640,480) 範例。

另請參閱 [Experience Manager Assets和Dynamic Media Classic的檢視器](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/c-html5-s7-aem-asset-viewers.html#viewers-aem-assets-dmc) 和 [僅適用於Experience Manager Assets的檢視器](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers.html#viewers-for-aem-assets-only) 在 [Dynamic Media檢視器參考指南](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html).

## 最佳實務：使用HTML5視訊檢視器 {#best-practice-using-the-html-video-viewer}

Dynamic Media HTML5視訊檢視器預設集是強大的視訊播放器。 您可以使用它們來避免許多與HTML5視訊播放相關的常見問題，以及與行動裝置相關的問題。 例如，缺乏最適化位元速率串流傳送，且桌上型電腦瀏覽器的觸及範圍有限。

在播放器的設計方面，您可以使用標準Web開發工具來設計視訊播放器的功能。 例如，您可以使用HTML5和CSS來設計按鈕、控制項和自訂海報影像背景，以幫助您透過自訂外觀觸及客戶。

在檢視器的播放端，會自動偵測瀏覽器的視訊功能。 然後它會使用HLS或DASH （也稱為最適化視訊串流）提供視訊。 或者，如果這些傳送方法不存在，則改用HTML5 progressive。

>[!NOTE]
>
>若要在視訊中使用DASH，必須先由您帳戶上的Adobe技術支援啟用。 另請參閱 [在您的帳戶上啟用DASH](#enable-dash).

您可以使用HTML5和CSS將設計播放元件的功能結合到單一播放器中。 它可以內嵌播放，並根據瀏覽器的功能使用最適化和漸進式串流。 這項功能意味著，您可以將多媒體內容延伸至桌上型電腦和行動使用者，並確保簡化的視訊體驗。

另請參閱 [僅適用於Experience Manager Assets的檢視器](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers.html#viewers-for-aem-assets-only) 在 [Dynamic Media檢視器參考指南](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html).


### 使用HTML5視訊檢視器在桌上型電腦和行動裝置上播放視訊 {#playback-of-video-on-desktop-computers-and-mobile-devices-using-the-html-video-viewer}

就桌上型電腦和行動最適化視訊串流而言，用於位元速率切換的視訊均以最適化視訊集中的所有MP4視訊為基礎。

使用HLS或DASH或漸進式視訊下載進行視訊播放。 在舊版Experience Manager（例如6.0、6.1和6.2）中，影片會透過HTTP進行串流處理。

不過，在Experience Manager6.3及更新版本中，視訊現在會透過HTTPS （亦即HLS或DASH）進行串流，因為DM閘道服務URL也一律使用HTTPS。 此預設行為不會影響客戶。 也就是說，除非瀏覽器不支援，否則視訊串流一律會透過HTTPS進行。 （請參閱下表）。

因此，

* 如果您的HTTPS網站有HTTPS視訊串流，則資料流沒有問題。
* 如果您的HTTP網站具有HTTPS視訊串流，則串流沒有問題，而且網頁瀏覽器中沒有混合式內容問題。

DASH是國際標準，HLS是Apple標準。 兩者都用於自我調整視訊串流。 此外，這兩種技術都會根據網路頻寬容量自動調整播放。 它也可讓客戶「搜尋」視訊中的任何位置，而不需要等候視訊的其餘部分下載。

漸進式視訊的傳送方式，是將視訊下載並儲存在使用者的案頭系統或行動裝置上。

下表說明在桌上型電腦和行動裝置上使用視訊的裝置、瀏覽器和播放方法。 [Dynamic Media HTML5視訊檢視器](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video.html#interactive-video).

<table>
 <tbody>
  <tr>
   <td><strong>设备</strong></td>
   <td><strong>浏览器</strong></td>
   <td><strong>視訊播放模式</strong></td>
  </tr>
  <tr>
   <td>桌面</td>
   <td>Internet Explorer 9和10</td>
   <td>漸進式下載。</td>
  </tr>
  <tr>
   <td>桌面</td>
   <td>Internet Explorer 11+</td>
   <td>在Windows® 8和Windows® 10上 — 只要要求DASH或HLS，就強制使用HTTPS。 已知限制：DASH或HLS上的HTTP在此瀏覽器/作業系統組合中無法運作<br /> <br /> 在Windows® 7上 — 漸進式下載。 使用標準邏輯來選取HTTP與HTTPS通訊協定。</td>
  </tr>
  <tr>
   <td>桌面</td>
   <td>Firefox 23-44</td>
   <td>漸進式下載。</td>
  </tr>
  <tr>
   <td>桌面</td>
   <td>Firefox 45或更新版本</td>
   <td>HLS或DASH*最適化位元速率串流</td>
  </tr>
  <tr>
   <td>桌面</td>
   <td>鉻黃</td>
   <td>HLS或DASH*最適化位元速率串流</td>
  </tr>
  <tr>
   <td>桌面</td>
   <td>Safari (Mac)</td>
   <td>HLS最適化位元速率串流</td>
  </tr>
  <tr>
   <td>移动设备</td>
   <td>Chrome (Android™ 6或更舊版本)</td>
   <td>漸進式下載。</td>
  </tr>
  <tr>
   <td>移动设备</td>
   <td>Chrome (Android™ 7或更新版本)</td>
   <td>HLS或DASH*最適化位元速率串流/td&gt;
  </tr>
  <tr>
   <td>移动设备</td>
   <td>Android™ （預設瀏覽器）</td>
   <td>漸進式下載。</td>
  </tr>
  <tr>
   <td>移动设备</td>
   <td>Safari (iOS)</td>
   <td>HLS最適化位元速率串流</td>
  </tr>
  <tr>
   <td>移动设备</td>
   <td>Chrome (iOS)</td>
   <td>HLS最適化位元速率串流</td>
  </tr>
 </tbody>
</table>

>[!IMPORTANT]
>
>*若要在視訊中使用DASH，必須先由您帳戶上的Adobe技術支援啟用。 另請參閱 [在您的帳戶上啟用DASH](#enable-dash).)

<!--  THIS LINE WAS REMOVED FROM THE TABLE ABOVE ON FEB 28, 2022 BASED ON CQDOC 18692 -RSB <tr>
   <td>Mobile</td>
   <td>BlackBerry&reg;</td>
   <td>HLS or DASH</td>
  </tr>
 -->

## Dynamic Media視訊解決方案的架構 {#architecture-of-dynamic-media-video-solution}

下圖顯示透過DMGateway (在Dynamic Media混合模式)上傳及編碼且可供公眾使用的影片整體製作工作流程。

![chlimage_1-427](assets/chlimage_1-427.png)

## 視訊的混合式發佈架構 {#hybrid-publishing-architecture-for-videos}

![chlimage_1-428](assets/chlimage_1-428.png)

## 視訊編碼最佳作法 {#best-practices-for-encoding-videos}

此 **Dynamic Media編碼影片** 如果您已啟用Dynamic Media並設定視訊Cloud Services，工作流程會對視訊進行編碼。 此工作流会捕获工作流进程历史记录和失败信息。如果您已啟用Dynamic Media並設定視訊Cloud Services， **[!UICONTROL Dynamic Media編碼影片]** 上傳視訊時，工作流程會自動生效。 (如果您沒有使用Dynamic Media，請 **[!UICONTROL DAM更新資產]** 工作流程會生效。)

以下是編碼來源視訊檔案的最佳實務提示。

<!-- For advice about video encoding, see the following:

* [Streaming 101: The Basics — Codecs, Bandwidth, Data Rate, and Resolution](https://www.adobe.com/go/learn_s7_streaming101_en).
* [Video Encoding Basics](https://www.adobe.com/go/learn_s7_encoding_en). -->

### 來源視訊檔案 {#source-video-files}

編碼視訊檔案時，請使用最高品質的來源視訊檔案。 避免使用先前編碼的視訊檔案，因為這些檔案已經壓縮，進一步編碼會建立品質不佳的視訊。

* Dynamic Media主要支援長度上限為30分鐘，最小解析度大於25 x 25的短影片。
* 您可以上傳每個最多15 GB的主要來源視訊檔案。

下表說明編碼來源視訊檔案之前，其建議大小、外觀比例和最低位元速率等設定：

| 大小 | 宽高比 | 最小位元速率 |
|--- |--- |--- |
| 1024 X 768 | 4:3 | 大多數影片為4500 kbps。 |
| 1280 X 720 | 16:9 | 3000 - 6000 kbps （視視訊中的移動量而定）。 |
| 1920 X 1080 | 16:9 | 6000 - 8000 kbps （視視訊中的移動量而定）。 |

### 取得檔案的中繼資料 {#obtaining-a-file-s-metadata}

您可以使用視訊編輯工具檢視檔案的中繼資料，或使用專為取得中繼資料而設計的應用程式來取得檔案的中繼資料。 以下是使用MediaInfo （協力廠商應用程式）來取得視訊檔案中繼資料的指示：

1. 前往 [MediaInfo下載](https://mediaarea.net/en/MediaInfo/Download).
1. 選取並下載GUI版本的安裝程式，然後依照安裝指示操作。
1. 安裝後，請以滑鼠右鍵按一下視訊檔案(僅限Windows®)並選取MediaInfo，或開啟MediaInfo並將視訊檔案拖曳到應用程式中。 您會看到與視訊檔案相關的所有中繼資料，包括其寬度、高度和FPS。

### 宽高比 {#aspect-ratio}

當您選擇或建立主要來源視訊檔案的視訊編碼預設集時，請確定預設集具有與主要來源視訊檔案相同的外觀比例。 外觀比例是視訊的寬度與高度的比例。

若要判斷視訊檔案的外觀比例，請取得檔案的中繼資料，並注意檔案的寬度和高度（請參閱上述取得檔案的中繼資料）。 然後使用此公式來決定長寬比：

寬度/高度=外觀比例

下表說明公式結果如何轉換成常見的外觀比例選擇：

| 公式結果 | 宽高比 |
|--- |--- |
| 1.33 | 4:3 |
| 0.75 | 3:4 |
| 1.78 | 16:9 |
| 0.56 | 9:16 |

例如，1440寬度x 1080高度的視訊外觀比例為1440/1080，即1.33。在這種情況下，您可以選擇長寬比為4:3的視訊編碼預設集，來編碼視訊檔案。

### 比特率 {#bitrate}

Bitrate是經過編碼，構成視訊播放一秒的資料量。 位元速率是以每秒千位元(Kbps)來測量。

>[!NOTE]
>
>由於所有轉碼器都使用有失真壓縮，因此位元速率是視訊品質中最重要的因素。 有失真壓縮越是壓縮視訊檔案，品質就越會降低。 因此，其他所有特性（解析度、影格速率和轉碼器）相等時，位元速率越低，壓縮檔案的品質就越低。

選取位元速率編碼時，您可以選擇兩種型別：

* **[!UICONTROL 固定位元速率編碼]** (CBR) — 在CBR編碼期間，位元速率或每秒位元數在整個編碼過程中都會保持相同。 CBR編碼會在整個視訊中將設定的資料速率儲存至您的設定。 此外，CBR編碼不會最佳化媒體檔案的品質，但會節省儲存空間。
如果您的視訊在整個視訊中包含類似的移動層級，請使用CBR。 CBR最常用於串流視訊內容。 另請參閱 [使用自訂新增的視訊編碼引數](/help/assets/dynamic-media/video-profiles.md#using-custom-added-video-encoding-parameters).

* **[!UICONTROL 變數位元速率編碼]** (VBR) - VBR編碼會根據壓縮器所需的資料，向下調整資料速率，並調整至您設定的上限。 此功能表示在VBR編碼程式期間，媒體檔案的位元速率會根據媒體檔案的位元速率需求動態增加或減少。
VBR花較長的時間進行編碼，但會產生最有利的結果；媒體檔案的品質優異。 VBR最常用於http漸進式傳送視訊內容。

何時使用VBR或CRB？
選取VBR與CBR時，幾乎總是建議您使用VBR處理媒體檔案。 VBR以具競爭力的位元速率提供更高品質的檔案。 使用VBR時，請務必使用兩階段編碼，並將最大位元速率設定為目標視訊位元速率的1.5倍。

當您選擇視訊編碼預設集時，請務必說明目標使用者的連線速度。 選擇資料速率為該速度80%的預設集。 例如，如果目標使用者的連線速度是1000 Kbps，則最佳預設集是視訊資料速率為800 Kbps的預設集。

此表格說明一般連線速度的資料速率。

| 速度(Kbps) | 連線型別 |
|--- |--- |
| 256 | 撥號連線。 |
| 800 | 一般行動連線。 針對此連線，針對3G體驗將資料速率目標定在400到800之間。 |
| 2000 | 典型的寬頻案頭連線。 針對此連線，將資料速率目標設定在800到2000 Kbps範圍內，大部分目標平均為1200到1500 Kbps。 |
| 5000 | 典型的高寬頻連線。 不建議在此上限範圍內進行編碼，因為大多數消費者無法使用此速度的視訊傳送。 |

### 解决方法 {#resolution}

**解析度** 說明視訊檔案的高度和寬度（畫素）。 大部分的來源視訊都是以高解析度儲存（例如1920 x 1080）。 為了串流用途，來源視訊會壓縮成較小的解析度（640 x 480或更小）。

解析度和資料速率是決定視訊品質的兩個整合因素。 若要維持相同的視訊品質，視訊檔案中的畫素數越高（解析度越高），資料速率就必須越高。 例如，假設320 x 240解析度和640 x 480解析度視訊檔案的每幀畫素數：

| 解决方法 | 每個影格的畫素 |
|--- |--- |
| 320 x 240 | 76,800 |
| 640 x 480 | 307,200 |

640 x 480檔案的每個影格畫素會多出4倍。 若要在這兩個範例解析度上達到相同的資料速率，您可以對640 x 480檔案套用4倍的壓縮，這會降低視訊品質。 因此，250 Kbps的視訊資料速率可以320 x 240的解析度提供高品質的觀賞效果，但無法以640 x 480的解析度提供。

一般而言，您使用的資料速率越高，視訊的顯示效果就越好，而且您使用的解析度越高，您必須維持檢視品質的資料速率就越高（與解析度較低相比）。

由於解析度和資料速率是相互關聯的，因此在編碼視訊時，您有兩個選項：

* 選擇資料速率，然後以您選擇之資料速率顯示的最佳解析度編碼。
* 選擇解析度，然後以您選擇的解析度進行必要的資料速率編碼，以獲得高品質的視訊。

當您選擇（或建立）主要來源視訊檔案的視訊編碼預設集時，請使用此表格來鎖定正確的解析度：

| 解决方法 | 高度(像素) | 熒幕大小 |
|--- |--- |--- |
| 240p | 240 | 超小熒幕 |
| 300p | 300 | 通常適用於行動裝置的小熒幕 |
| 360p | 360 | 小熒幕 |
| 480p | 480 | 中熒幕 |
| 720p | 720 | 大熒幕 |
| 1080p | 1080 | 高解析度大熒幕 |

### Fps （每秒影格數） {#fps-frames-per-second}

在美國和日本，大部分的影片是以每秒29.97幀(fps)的速率拍攝；在歐洲，大部分的影片是以每秒25fps的速率拍攝。 電影的拍攝速度為24 fps。

選擇符合主要來源視訊檔案的fps速率的視訊編碼預設集。 例如，如果您的主要來源視訊是25 fps，請選擇具有25 fps的編碼預設集。 依預設，所有自訂編碼都會使用主要來源視訊檔案的fps。 因此，當您建立視訊編碼預設集時，不需要明確指定fps設定。

### 視訊編碼維度 {#video-encoding-dimensions}

為了獲得最佳結果，請選取編碼維度，使來源視訊是所有已編碼視訊的整數倍。

若要計算此比率，請將來源寬度除以編碼的寬度，得出寬度比率。 然後，將來源高度除以編碼的高度來得到高度比率。

如果產生的比例是整數，表示影片會最佳地調整比例。 如果產生的比率不是整數，則會藉由在顯示器上留下多餘的畫素不自然感來影響視訊品質。 當視訊中含有文字時，此效果最為明顯。

例如，假設您的來源視訊是1920 x 1080。 在下表中，三個已編碼的視訊提供要使用的最佳編碼設定。

| 視訊型別 | 寬度x高度 | 宽度比例 | 高度比例 |
|--- |--- |--- |--- |
| 源 | 1920x1080 | 1 | 1 |
| 已編碼 | 960 x 540 | 2 | 2 |
| 已編碼 | 640 x 360 | 3 | 3 |
| 已編碼 | 480 x 270 | 4 | 4 |

### 編碼的視訊檔案格式 {#encoded-video-file-format}

Dynamic Media建議使用MP4 H.264視訊編碼預設集。 由於MP4檔案使用H.264視訊轉碼器，因此可提供高品質的視訊，但採用壓縮檔案大小。

### 在您的帳戶上啟用DASH {#enable-dash}

DASH (Digital Adaptive Streaming over HTTP)是視訊串流的國際標準，被廣泛採用於不同的視訊檢視器中。 當您的帳戶啟用DASH時，您可以選擇使用DASH或HLS進行最適化視訊串流。 或者，您可以在以下情況下選擇兩個選項，並在播放器之間自動切換： **[!UICONTROL 自動]** 在檢視器預設集中選取為播放型別。

在您的帳戶上啟用DASH的一些主要優點包括：

* 封裝DASH串流視訊，以進行最適化位元速率串流。 此方法可帶來更高的傳遞效率。 最適化串流可確保為客戶提供最佳檢視體驗。
* 使用Dynamic Media播放器將瀏覽器最佳化的串流在HLS和DASH串流之間切換，以確保最佳的服務品質。 使用Safari瀏覽器時，視訊播放器會自動切換至HLS。
* 您可以編輯視訊檢視器預設集，以設定您偏好的串流方法（HLS或DASH）。
* 最佳化的視訊編碼可確保啟用DASH功能時不會使用額外的儲存空間。 系統會為HLS和DASH建立單一視訊編碼集，以最佳化視訊儲存成本。
* 協助讓客戶更容易存取視訊傳送。
* 也透過API取得串流URL。

您起始使用DASH的要求，但不會在您的帳戶上自動啟用。

若要在您的帳戶上啟用DASH，請建立客戶支援案例，如下所述。 在您的支援案例中，指定您要在您的Dynamic Media帳戶和Experience Manager上啟用DASH。

**若要在您的帳戶上啟用DASH：**

1. [使用Admin Console開始建立新的支援案例](https://helpx.adobe.com/cn/enterprise/using/support-for-experience-cloud.html).
1. 若要建立支援案例，請遵循指示，同時確保您提供下列資訊：

   * 主要連絡人姓名、電子郵件、電話。
   * 您的Dynamic Media帳戶名稱。
   * 指定您希望在Dynamic Media帳戶和Experience Manager上啟用DASH。

1. Adobe客戶支援會根據提交請求的順序，將您新增至DASH客戶等候清單。
1. 當Adobe準備好處理您的請求時，客戶支援會聯絡您以協調並設定DASH啟用的目標日期。
1. 客戶支援會在完成後通知您。
1. 建立您的 [視訊檢視器預設集](/help/assets/dynamic-media/managing-viewer-presets.md#creating-a-new-viewer-preset) 一如既往。

## 檢視視訊報表 {#viewing-video-reports}

>[!NOTE]
>
>視訊報表僅適用於執行Dynamic Media — 混合模式時。

視訊報表會顯示指定時段內的數個彙總量度，以幫助您監視 *已發佈* 個別和彙總影片如預期般執行。 系統會針對您整個網站的所有已發佈影片，彙總下列排名在前的量度資料：

* 视频开始
* 完成率
* 視訊平均逗留時間
* 影片花費的總時間
* 每次造訪的視訊數

全部的表格 *已發佈* 也會列出影片，讓您能根據影片開始播放總數，追蹤網站上最常檢視的影片。

當您在清單中選取視訊名稱時，會以折線圖的形式顯示視訊的對象保留率（流失）報表。 此圖表顯示視訊播放期間任何指定時間的檢視次數。 當您播放視訊時，垂直列會與播放器中的時間指示器同步追蹤。 折線圖資料中的下降會指出您的對象因不感興趣而消失的位置。

如果影片是在Adobe Experience Manager Dynamic Media之外編碼，則無法使用表格中的對象保留率（流失）圖表和播放百分比資料。

>[!NOTE]
>
>追蹤和報告資料完全以Dynamic Media自己的視訊播放器及相關聯的視訊播放器預設集為基礎。 因此，您無法追蹤和報告透過其他視訊播放器播放的視訊。

依預設，第一次輸入「視訊報表」時，報表會顯示從目前月份的第一天開始，到目前月份的日期結束的視訊資料。 不過，您可以指定自己的日期範圍來覆寫預設日期範圍。 下次輸入「視訊報表」時，系統會使用您指定的日期範圍。

為了讓視訊報表正常運作，設定Dynamic MediaCloud Services時會自動建立報表套裝ID。 同時，報表套裝ID會推送至發佈伺服器，以便您在預覽資產時可用於複製URL功能。 不過，此功能需要已經設定發佈伺服器。 如果發佈伺服器未設定，您仍可以發佈以檢視視訊報表。 不過，您必須返回Dynamic Media雲端設定並選取 **[!UICONTROL 確定]**.

**若要檢視視訊報表：**

1. 在Experience Manager的左上角，選取Experience Manager標誌，然後在左側邊欄中導覽至 **[!UICONTROL 工具]** （槌子圖示） > **[!UICONTROL 資產]** > **[!UICONTROL 視訊報表]**.
1. 在「視訊報表」頁面上，執行下列任一項作業：

   * 在右上角附近，選取 **[!UICONTROL 重新整理視訊報表]** 圖示。
只有在報表的結束日期為當天時，才使用「重新整理」。 此功能可確保您看到自上次執行報表後發生的視訊追蹤。

   * 在右上角附近，選取 **[!UICONTROL 日期選擇器]** 圖示。
指定您要視訊資料的開始和結束日期範圍，然後選取 **[!UICONTROL 執行報告]**.

   「排名在前的量度」群組方塊可識別所有量度的各種彙總測量 *已發佈* 您網站上的影片。

1. 在列出最常發佈影片的表格中，選取要播放影片的影片名稱，並參閱影片的「對象保留率（流失）」報表。

<!-- OBSOLETE CONTENT OBSOLETE CONTENT - SDK ONLY AVAILABLE INTERNALLY NOW 
### Viewing video reports based on a video viewer that you created using the Dynamic Media HTML5 Viewer SDK {#viewing-video-reports-based-on-a-video-viewer-that-you-created-using-the-scene-hmtl-viewer-sdk}

If you are using an out-of-box video viewer provided by Dynamic Media, or if you created a custom viewer preset based off of an out-of-box video viewer, then no additional steps are required to view video reports. However, if you have created your own video viewer based off the Dynamic Media HTML5 Viewer SDK, then use the following steps to ensure the your video viewer is sending tracking events to Dynamic Media Video Reports.

Use the Dynamic Media Viewers Reference and the Dynamic Media HTML5 Viewers SDK to create your own video viewers.

See [Dynamic Media Viewers Reference Guide](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/home.html).

Download the Scene7 HTML Viewer SDK from Adobe Developer Connection.

See [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html).

**To view Video Reports based on a video viewer that you created using the Dynamic Media HTML5 Viewer SDK:**

1. Navigate to any published video asset.
1. Near the upper-left corner of the asset's page, from the drop-down list, select **[!UICONTROL Viewers]**.
1. Select any video viewer preset and copy the embed code.
1. In the embed code, find the line with the following:

   `videoViewer.setParam("config2", "<value>");`

   The `config2` parameter enables tracking in HTML5 Viewers. It is also a company-specific preset that contains the configuration information for Video Reporting, and for customer-specific Adobe Analytics configurations.

   The correct value for the config2 parameter is found in both the **[!UICONTROL Embed Code]** and in the copy **[!UICONTROL URL]** function. In the URL from the copy **[!UICONTROL URL]** command, the parameter to look for is `&config2=<value>` . The value is almost always `companypreset`, but in some instances it can also be `companypreset-1`, `companypreset-2`, and so forth.

1. In your custom video viewer code, add AppMeasurementBridge .jsp to the viewer page by doing the following:

    * First, determine if you need the `&preset` parameter.
      If the `config2` parameter is `companypreset`, you do *not *need `&preset=parameter`.
      If `config2` is anything else, set the preset parameter the same as the `config2` parameter. For example, if `config2=companypreset-2`, add `&param2=companypreset-2` to the AppMeasurmentBridge.jsp URL.

    * Then, add the AppMeasurementBridge.jsp script:
      `<script language="javascript" type="text/javascript" src="https://s7d1.scene7.com/s7viewers/AppMeasurementBridge.jsp?company=robindallas&preset=companypreset-2"></script>`

1. Create the TrackingManager component by doing the following:

    * After calling `s7sdk.Utils.init();` create a TrackingManager instance to track events by adding the following:
      `var trackingManager = new s7sdk.TrackingManager();`

    * Connect components to TrackingManager by doing the following:
      In the `s7sdk.Event.SDK_READY` event handler, attach the component you want to track to the TrackingManager.
      For example, if the component is `videoPlayer`, add
      `trackingManager.attach(videoPlayer);`
      to attach the component to the trackingManager. To track multiple viewers on a page, use multiple tracking mangaer components.

    * Create the AppMeasurementBridge object by adding the following:

      ```
      var appMeasurementBridge = new AppMeasurementBridge(); appMeasurementBridge.setVideoPlayer(videoPlayer);
      ```

    * Add the tracking function by adding the following:

      ```
      trackingManager.setCallback(appMeasurementBridge.track,
       appMeasurementBridge);
      ```

   The appMeasurementBridge object has a built-in track function. OBSOLETE However, you can provide your own to support multiple tracking systems or other functionality.

   For more information, see *Using the TrackingManager Component* in the *Scene7 HTML5 Viewer SDK User Guide* available for download from [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html).
 -->

## 新增隱藏式字幕或字幕至視訊 {#adding-captions-to-video}

您可以將隱藏式字幕新增至單一視訊或「最適化視訊集」，將視訊觸及全球市場。 藉由新增隱藏式字幕，您無需對音訊進行配音，或需要使用母語者重新錄製每種不同語言的音訊。 視訊是以其錄製語言播放。 出現外文字幕，讓不同語言的人仍可瞭解音訊部分。

隱藏式字幕也讓耳聾或聽力缺佳的人更容易使用。

>[!NOTE]
>
>您使用的視訊播放器必須支援隱藏式字幕的顯示。

另請參閱 [Dynamic Media中的協助工具](/help/assets/dynamic-media/accessibility-dm.md).

Dynamic Media可以將註解檔案轉換為JSON （JavaScript物件標籤法）格式。 此轉換表示您可以將JSON文字內嵌至網頁，做為隱藏但完整的視訊轉錄。 搜尋引擎接著可以編目/索引內容，讓視訊更容易被發現，並為客戶提供更多有關視訊內容的詳細資訊。

另請參閱 [提供靜態（非影像）內容](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/c-serving-static-nonimage-contents.html#image-serving-api) 以取得在URL中使用JSON函式的詳細資訊。

**若要在視訊中新增註解或字幕：**

1. 使用協力廠商應用程式或服務來建立您的視訊標題/字幕檔案。

   確保您建立的檔案遵循WebVTT （網頁視訊文字追蹤）標準。 字幕副檔名為.VTT。 您可以進一步瞭解WebVTT字幕標準。

   另請參閱 [WebVTT：網頁視訊文字追蹤格式](https://w3c.github.io/webvtt/).

   您可以在Dynamic Media外部使用免費和優質的工具和服務來撰寫註解/字幕檔案。 例如，若要建立不含樣式的簡單視訊註解檔案，您可以使用下列免費線上註解製作與編輯工具：

   [WebVTT註解製作器](https://testdrive-archive.azurewebsites.net/Graphics/CaptionMaker/Default.html)

   為達到最佳效果，請在Internet Explorer 9或更新版本、Google Chrome或Safari中使用工具。

   在工具中，在 **[!UICONTROL 輸入視訊檔案的URL]** 欄位，貼上視訊檔案的複製URL，然後選取 **[!UICONTROL 載入]**. 另請參閱 [取得資產的URL](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset) 以取得視訊檔案本身的URL，然後您可將它貼入 **[!UICONTROL 輸入視訊檔案欄位的URL]**. 随后，Internet Explorer、Chrome 或 Safari 可以本机播放视频。

   現在請依照網站熒幕上的指示，製作並儲存您的WebVTT檔案。 完成後，複製註解檔案內容並將其貼到純文字編輯器中，並以VTT副檔名儲存。

   >[!NOTE]
   >
   >為了在全球支援多種語言的視訊字幕，WebVTT標準要求您建立個別的.vtt檔案，並針對您想要支援的每種語言呼叫。

   通常，您會想要將註解VTT檔案命名為與視訊檔案相同的名稱，然後附加語言地區設定，例如 — EN、-FR或 — DE。 如此一來，便可協助您使用現有的網頁內容管理系統，自動化視訊URL的產生。

1. 在Experience Manager中，將您的WebVTT插圖示題檔案上傳至DAM。
1. 導覽至 *已發佈* 您想要與您上傳的註解檔案相關聯的視訊資產。

   请注意，只有在首次&#x200B;*发布*&#x200B;资产&#x200B;*后*，才可复制 URL。

   另請參閱 [發佈資產](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

1. 执行下列操作之一：

   * 若要取得快顯視訊檢視器體驗，請選取「 」 **[!UICONTROL URL]**. 在URL對話方塊中，選取URL並複製到剪貼簿，然後將URL通過簡單文字編輯器。 使用以下語法附加複製的視訊URL：

      `&caption=<server_path>/is/content/<path_to_caption.vtt_file,1>`

      請注意 `,1` 註解路徑結尾處。 在路徑中的VTT副檔名後面緊接著可以選擇性啟用（開啟）或停用（關閉）視訊播放器列上的隱藏式字幕按鈕，方法是設定為 `,1` 或 `,0`（分別）。

   * 若要內嵌視訊檢視器體驗，請選取「 」 **[!UICONTROL 內嵌程式碼]**. 在「內嵌程式碼」對話方塊中，選取「 」，並將內嵌程式碼複製到剪貼簿，然後將程式碼貼到簡單的文字編輯器中。 使用下列語法附加複製的內嵌程式碼：

      `videoViewer.setParam("caption","<path_to_caption.vtt_file,1>");`

      請注意 `,1` 註解路徑結尾處。 在路徑中的VTT副檔名後面緊接著可以選擇性啟用（開啟）或停用（關閉）視訊播放器列上的隱藏式字幕按鈕，方法是設定為 `,1` 或 `,0`（分別）。

## 將章節標籤新增至視訊 {#adding-chapter-markers-to-video}

您可以將章節標籤新增至單一視訊或「最適化視訊集」，讓長格式視訊更易於觀看和導覽。 使用者播放視訊時，可以在視訊時間軸上選取章節標籤（也稱為視訊筆畫壓感器）。 他們可以輕鬆導覽至興趣點，或立即跳至新內容、培訓和示範。

>[!NOTE]
>
>使用的視訊播放器必須支援使用章節標籤。 Dynamic Media影片播放器不支援章節標籤，但使用協力廠商影片播放器可能不支援。

<!-- OBSOLETE CONTENT OBSOLETE CONTENT If desired, you can create and brand your own custom video viewer with chapters instead of using a video viewer preset. For instructions on creating your own HTML5 viewer with chapter navigation, in the Adobe Scene7 Viewer SDK for HTML5 guide, reference the heading "Customizing Behavior Using Modifiers" under the classes `s7sdk.video.VideoPlayer` and `s7sdk.video.VideoScrubber`. The Adobe Scene7 Viewer SDK is available as a download from [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html). -->

您建立視訊章節清單的方式與建立註解的方式大致相同。 也就是說，您會建立WebVTT檔案。 但請注意，此檔案必須與任何WebVTT註解檔案分開。 您無法將字幕和章節合併到一個WebVTT檔案中。

您可以使用以下範例作為使用章節導覽來建立WebVTT檔案的格式範例：

### 具有視訊章節導覽的WebVTT檔案 {#webvtt-file-with-video-chapter-navigation}

```xml {.line-numbers}
WEBVTT
Chapter 1
00:00.000 --> 01:04.364
The bicycle store behind it all.
Chapter 2
01:04.364 --> 02:00.944
Creative Cloud.
Chapter 3
02:00.944 --> 03:02.937
Ease of management for a working solution.
Chapter 4
03:02.937 --> 03:35.000
Cost-efficient access to rapidly evolving technology.
```

在上述範例中， `Chapter 1` 是提示識別碼，且為選用。 的提示時間 `00:00:000 --> 01:04:364` 指定章節的開始時間和結束時間，單位為 `00:00:000` 格式。 最後三位數為毫秒，可保留為 `000`，若建議使用。 的章節標題 `The bicycle store behind it all` 是章節內容的實際說明。 當使用者將其滑鼠指標停留在時間軸中的視覺提示點上時，提示識別碼、開始提示時間和章節標題都會顯示在視訊播放器的快顯視窗中。

由於您使用的是HTML5視訊檢視器，請確定您建立的章節檔案遵循WebVTT （網頁視訊文字追蹤）標準。 章節副檔名為.VTT。 您可以進一步瞭解WebVTT字幕標準。

另請參閱 [WebVTT：網頁視訊文字追蹤格式](https://w3c.github.io/webvtt/).

**若要將章節標籤新增至視訊：**

1. 將VTT檔案儲存為UTF8編碼，以避免章節標題文字中的字元轉譯發生問題。

   通常，您會想要將章節VTT檔案命名為與視訊檔案相同的名稱，並附加章節。 如此一來，便可協助您使用現有的網頁內容管理系統，自動化視訊URL的產生。
1. 在Experience Manager中，上傳您的WebVTT章節檔案。

   另請參閱 [上傳資產](/help/assets/manage-digital-assets.md#uploading-assets).

1. 执行下列操作之一：

   <table>
     <tbody>
      <tr>
       <td>適用於快顯視訊檢視器體驗</td>
       <td>
       <ol>
       <li>導覽至 <i>已發佈 </i>您想要與您上傳的章節檔案建立關聯的視訊資產。 请注意，只有在首次<i>发布</i>资产<i>后</i>，才可复制 URL。另請參閱 <a href="/help/assets/dynamic-media/publishing-dynamicmedia-assets.md">正在發佈資產。</a></li>
       <li>從下拉式功能表中，選取 <strong>檢視者</strong>.</li>
       <li>在左側欄中，選取視訊檢視器預設集名稱。 視訊的預覽會在另一個頁面中開啟。</li>
       <li>在左側欄的底部，選取 <strong>URL</strong>.</li>
       <li>在URL對話方塊中，選取URL並複製到剪貼簿，然後將URL通過至簡單的文字編輯器。</li>
       <li>使用以下語法附加複製的視訊URL，以便將其與複製的章節檔案URL建立關聯：<br /> <br /> <code>&navigation=<<i>full_copied_URL_path_to_chapter_file</i>.vtt></code><br /> </li>
       </ol> </td>
      </tr>
      <tr>
       <td>適用於內嵌視訊檢視器體驗<br /> </td>
       <td>
       <ol>
       <li>導覽至 <i>已發佈 </i>您想要與您上傳的章節檔案建立關聯的視訊資產。 请注意，只有在首次<i>发布</i>资产<i>后</i>，才可复制 URL。另請參閱 <a href="/help/assets/dynamic-media/publishing-dynamicmedia-assets.md">正在發佈資產。</a></li>
       <li>從下拉式功能表中，選取 <strong>檢視者</strong>.</li>
       <li>在左側欄中，選取視訊檢視器預設集名稱。 視訊的預覽會在另一個頁面中開啟。</li>
       <li>在左側欄的底部，選取 <strong>內嵌</strong>.</li>
       <li>在「內嵌程式碼」對話方塊中，選取「 」，並將整個程式碼複製到剪貼簿，然後貼到簡單的文字編輯器中。</li>
       <li>使用以下語法附加視訊的內嵌程式碼，以便將其與複製的URL關聯至章節檔案：<br /> <br /> <code>videoViewer.setParam("navigation","&lt;<i>full_copied_URL_path_to_chapter_file</i>.vtt>"</code></li>
       </ol> </td>
      </tr>
     </tbody>
   </table>

<!--

## About video thumbnails {#about-video-thumbnails}

A video thumbnail is a reduced-size version of a video frame or an image asset representing the video to the customer. The thumbnail should serve to encourage a customer to select the video.

All videos in Experience Manager must have an associated thumbnail; you cannot delete a thumbnail without replacing it. By default, when you upload a video to Experience Manager, the first frame is used as the thumbnail. However, you can customize the thumbnail for branding purposes or visual search, for example. When you customize a video thumbnail, you can either play the video and pause on the frame you want to use, or you can select an image asset that you have already uploaded and *published* in your digital asset manager.

Note that a custom video thumbnail image that you select from a video is not extracted and saved in the DAM as a separate and distinct asset. However, a custom video thumbnail that you select from an existing image asset is saved to the JCR. The path of the selected asset gets stored under the video asset's node as in the following example path:

`/content/dam/*<folder_name*>/<*video_name*>/jcr:content/manualThumbnail`

The ability to customize a video thumbnail is only available after you have applied a video profile to the folder where the video is located.

### Adding a custom video thumbnail {#adding-a-custom-video-thumbnail}

1. Be sure you have already done the following:

    * Created a folder for your video assets.
    * [Applied a video profile to the folder](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders).

    * [Uploaded your videos to the folder](/help/assets/manage-video-assets.md#upload-and-preview-video-assets).

1. Navigate to an uploaded video asset whose thumbnail image you want to change.
1. In asset selection mode either from **[!UICONTROL List View]** or **[!UICONTROL Card View]**, select the video asset.
1. On the toolbar, select the **[!UICONTROL Properties** icon (a circle with an "i" in it).
1. On the video's Properties page, select **[!UICONTROL Change Thumbnail]**.
1. On the Change Thumbnail page, do one of the following:

    * To use a frame from the video as the new thumbnail:

        * On the toolbar, select **[!UICONTROL Select Frame from video]**.
        * Select the Play button, then select the Pause button on the frame you want to capture as the video's new thumbnail.

    * To use an image asset as the new thumbnail:

        * On the toolbar, select **[!UICONTROL Select Thumbnail from Assets]**.
        * Select **[!UICONTROL Select Thumbnail]**.
        * Navigate to a previously uploaded and published image asset you want to use. Note that the asset will automatically be resized to serve as a thumbnail image for the video.
        * Select the image asset, then select **[!UICONTROL Select]**.

1. On the Change Thumbnail page, select **[!UICONTROL Save Change]**.
1. On the video's Properties page, in the upper-right corner, select **[!UICONTROL Save & Close]**.

-->

<!--

## About video thumbnails in Dynamic Media Hybrid mode{#about-video-thumbnails-in-dynamic-media-hybrid-mode}

You can choose from one of ten thumbnail images automatically generated by Dynamic Media to add to your video. The video player displays your selected thumbnail when a video asset is used with the Dynamic Media component in the authoring environment of Experience Manager Sites, Experience Manager Mobile, or Experience Manager Screens. The thumbnail serves as a static picture that best represents the contents of your entire video and further encourages users to select the Play button.

Based on the total time of the video, Dynamic Media captures ten (default) thumbnail images at 1%, 11%, 21%, 31%, 41%, 51%, 61%, 71%, 81%, and 91% into the video. The ten thumbnails persist meaning that if you decide to choose a different thumbnail later on, you do not need to regenerate the series. You preview the ten thumbnail images and then select the one you want to use with your video. If you want to change to default you can use CRXDE Lite to configure the time interval that thumbnail images are generated. For example, if you only wanted to generate a series of four evenly spaced thumbnail images from your video, you can configure the interval time at 24%, 49%, 74%, and 99%.

Ideally, you can add a video thumbnail anytime after you upload your video but before you publish the video on your website.

If you prefer, you can choose to upload a custom thumbnail to represent your video instead of using a thumbnail generated by Dynamic Media. For example, you could create a custom thumbnail image that has the title of your video, an eye-catching opening image, or a very specific image captured from your video. The custom video thumbnail image that you upload should have a maximum resolution of 1280 x 720 pixels (minimum width of 640 pixels) and be no larger than 2MB.

See also [About video thumbnails](/help/assets/dynamic-media/video.md#about-video-thumbnails-in-dynamic-media-scene-mode).

-->

<!--

### Adding a video thumbnail {#adding-a-video-thumbnail}

1. Navigate to an uploaded video asset that you want to add a video thumbnail.
1. In asset selection mode either from the List View or the Card View, select the video asset.
1. On the toolbar, select the **[!UICONTROL View Properties]** icon (a circle with an "i" in it).
1. On the video's Properties page, select **[!UICONTROL Change Thumbnail]**.
1. On the Change Thumbnail page, on the toolbar, select **[!UICONTROL Select Frame]**.

   Dynamic Media generates a series thumbnail images from your video, based on the default time interval or time interval you customized.

1. Preview the generated thumbnail images, then select the one you want to add to your video.
1. Select **[!UICONTROL Save Change]**.

   The video's thumbnail image is updated to use the thumbnail you selected. If you later decide to change the thumbnail image, you can return to the **[!UICONTROL Change Thumbnail]** page and select a new one.

   If you configured new default time intervals, or you uploaded a new video to replace the existing video, you will need to have Dynamic Media regenerate the thumbnails.

   See [Configuring the default time interval that video thumbnails are generated](#configuring-the-default-time-interval-that-video-thumbnails-are-generated).

-->

<!--

#### Configuring the default time interval that video thumbnails are generated {#configuring-the-default-time-interval-that-video-thumbnails-are-generated}

When you configure and save the new default time interval, your change automatically applies only to videos that you upload in the future. It does not automatically apply the new default to videos that you previously uploaded. For existing videos, you must regenerate the thumbnails.

See [Adding a video thumbnail](#adding-a-video-thumbnail).

**To configure the default time interval that video thumbnails are generated,**

1. In Experience Manager, navigate to **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL CRXDE Lite]**.

1. In the CRXDE Lite page, in the directory panel on the left, navigate t `o etc/dam/imageserver/configuration/jcr:content/settings.`

   if the directory panel is not visible, you may need to select the >> icon to the left of the Home tab.

1. On the lower-right panel, in the Properties tab, double-tap `thumbnailtime`.
1. In the Edit thumbnailtime dialog box, use the text fields to enter interval values as percentages.

    * Select the plus sign (+) icon to add one or more interval value fields. You may need to scroll to the bottom of the dialog box to see the icon.
    * Select the minus sign (-) icon to the right of an interval value field to delete it from the list.
    * Select the up arrow icon and the down arrow icon to reorder the interval values.

1. Select **[!UICONTROL OK]** to return to the Properties tab.
1. Near the upper-left corner of the CRXDE Lite page, select **[!UICONTROL Save All]**, then select the Back Home icon in the upper-left corner to return to Experience Manager.

   See [Adding a video thumbnail](#adding-a-video-thumbnail).

-->

<!--

### Adding a custom video thumbnail {#adding-a-custom-video-thumbnail-1}

These steps apply only to Dynamic Media running in Hybrid mode.

T**o add a custom video thumbnail**,

1. Navigate to an uploaded video asset that you want to add a custom video thumbnail.
1. In asset selection mode either from the List View or the Card View, select the video asset.
1. On the toolbar, select the **[!UICONTROL View Properties]** icon (a circle with an "i" in it).
1. On the video's Properties page, select **[!UICONTROL Change Thumbnail]**.
1. On the Change Thumbnail page, on the toolbar, select **[!UICONTROL Upload New Thumbnail]**.
1. Navigate to a thumbnail image you want to use, select it, then select **[!UICONTROL Open]** to begin uploading the image into Experience Manager. Following the upload, be sure you publish the image.
1. After you have successfully uploaded and published the image, in the Change Thumbnail page, select **[!UICONTROL Save Changes]**.

   The custom thumbnail is added to your video.

-->

## 變更Dynamic Media資產的Dynamic Media URL

在Dynamic Media中處理的視訊可以透過開箱即用的檢視器使用，也可以直接存取資訊清單URL並通過您自己的自訂檢視器播放。 以下是擷取視訊資訊清單URL的API。

### 關於getVideoManifestURI API

此 `getVideoManifestURI`API透過c公開`q-scene7-api:com.day.cq.dam.scene7.api` 和可用來產生下列資訊清單URL：

```java
/**   
* Returns the manifest url for videos 
* @param resource video resource 
* @param manifestType type of video streaming manifest being requested 
* @param onlyIfPublished return a manifest only if the video is published 
* @return the manifest url for videos 
* 
* @throws Exception 
*/
@Nullable 
String getVideoManifestURI(Resource resource, ManifestType manifestType, boolean onlyIfPublished) throws Exception;
```

#### getVideoManifestURI API引數

此API會採用下列三個引數：

| 参数 | 描述 |
| --- | --- |
| `resource` | 與Dynamic Media已擷取的視訊對應的資源。 |
| `manifestType` | 可以是 `ManifestType.DASH` 或 `ManifestType.HLS` |
| `onlyIfPublished` | 如果資訊清單URI只有在發佈並在傳遞層級上可用時才會產生，則設為true。 |

若要使用上述方法擷取視訊的資訊清單URL，請新增 [視訊編碼設定檔](/help/assets/dynamic-media/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming) 移至「上傳影片」資料夾。 Dynamic Media會根據在指派給資料夾的視訊編碼檔案中找到的編碼，來處理這些視訊。 現在，您可以叫用上述API來擷取已上傳影片的資訊清單URL。

### 錯誤案例

如果發生錯誤，API會傳回null。 例外狀況會記錄在Experience Manager錯誤記錄檔中。 所有此類記錄錯誤的開頭為 `Could not generate Video Manifest URI`. 下列情況可能會導致此類錯誤發生：

* 一個 `IllegalArgumentException` 會針對下列任一專案進行記錄：

   * 此 `resource` 傳遞的引數為null。
   * 此 `resource` 傳遞的引數不是影片。
   * 此 `manifestType` 傳遞的引數為null。
   * 此 `onlyIfPublished` 引數會傳遞為true，但視訊不會發佈。
   * 未使用Dynamic Media中的最適化視訊集擷取視訊。

* `IOException` 在連線到Dynamic Media時發生問題時記錄。
* `UnsupportedOperationException` 於以下情況時記錄： `manifestType` 傳遞的引數為 `ManifestType.DASH`，而視訊尚未使用DASH格式處理。

<!-- THE REMAINING SECTION IS FOR 6.5 ONLY 

The following is an example of the above API using servlets written in *HTTPWhiteBoard* specification. Select each tab for the code syntax.

>[!BEGINTABS]

>[!TAB Add dependency in pom.xml]

+++**Add dependency in pom.xml** 

```java
dependency> 
     <groupId>com.day.cq.dam</groupId> 
     <artifactId>cq-scene7-api</artifactId> 
     <version>5.12.64</version> 
     <scope>provided</scope> 
</dependency> 
```

+++

>[!TAB Sample servlet]

+++**Sample servlet** 

```java
@Component
        service = Servlet.class 
) 
@HttpWhiteboardServletPattern(value = ManifestServlet.SERVLET_PATTERN) 
@HttpWhiteboardContextSelect(value = Constants.SERVLET_CONTEXT_SELECTOR) 
public class ManifestServlet extends HttpServlet { 

   private static final Logger LOGGER = LoggerFactory.getLogger(ManifestServlet.class); 

   private final ObjectMapper objectMapper; 

    @Reference 
    private Scene7Service scene7Service; 

   public static final String SERVLET_PATTERN = Constants.VIDEO_API_PREFIX + "/manifestUrl"; 

   public ManifestServlet() {
         this.objectMapper = new ObjectMapper(); 
         objectMapper.setSerializationInclusion(JsonInclude.Include.NON_NULL); 
   }

   @Override 

   protected void doGet(HttpServletRequest request, HttpServletResponse response) throws IOException {
        final ResourceResolver resolver = getResourceResolver(request); 
        String assetPath = request.getParameter("assetPath"); 
        String manifest = request.getParameter("manifestType"); 
        String onlyIfPublished = request.getParameter("onlyIfPublished"); 
        Resource resource = resolver.getResource(assetPath); 
        response.setCharacterEncoding(StandardCharsets.UTF_8.toString()); 
        response.setContentType("application/json"); 
        if(resource == null) { 
            LOGGER.info("could not retrieve the resource from JCR"); 
            error("could not retrieve the resource from JCR", response); 
            return; 
        }

        String manifestUri = null; 

        try{ 
            ManifestType manifestType =  ManifestType.DASH; 
            if(manifest != null) { 
                manifestType = ManifestType.valueOf(manifest); 
            } 
            manifestUri = scene7Service.getVideoManifestURI(resource, manifestType, onlyIfPublished != null); 
            objectMapper.writeValue(response.getWriter(), new ManifestUrl(manifestUri)); 
            response.setContentType("application/json"); 
        } catch (Exception e) { 
            LOGGER.error(e.getMessage(), e); 
            error(String.format("Unable to get the manifest url for %s. %s", assetPath, e.getMessage()), response); 
        } 
    } 

    private ResourceResolver getResourceResolver(HttpServletRequest request) { 
        Object rr = request.getAttribute(AuthenticationSupport.REQUEST_ATTRIBUTE_RESOLVER); 
        if (!(rr instanceof ResourceResolver)) { 
            throw new IllegalStateException( 
                    "The request does not seem to have been created via Apache Sling's authentication mechanism."); 
        } else { 
            return (ResourceResolver) rr; 
        } 
    } 

    private void error(String errorMessage, HttpServletResponse response) throws IOException { 
        ManifestUrl errorManifest = new ManifestUrl(null); 
        errorManifest.setErrorMessage(errorMessage); 
        response.setStatus(HttpServletResponse.SC_INTERNAL_SERVER_ERROR); 
        objectMapper.writeValue(response.getWriter(), errorManifest); 
    } 
} 
```

+++

>[!TAB Response Class for servlet]

+++**Response Class for servlet** 

```java
public class ManifestUrl extends VideoResponse { 
     String manifestUrl; 
     public ManifestUrl(String manifestUrl) { 
         this.manifestUrl = manifestUrl; 
     } 
     public String getManifestUrl() { 
         return manifestUrl; 
     } 
} 

public abstract class VideoResponse { 
     String errorString; 

     public String getErrorString() { 
         return errorString; 
     } 

     public void setErrorMessage(String errorString) { 
         this.errorString = errorString; 
     } 
} 
```

+++

>[!TAB Constants file referenced in servlet]

+++**Constants file referenced in servlet** 

```java
public final class Constants { 

     private Constants() { 
     } 

     public static final String VIDEO_API_PREFIX = "/dynamicmedia/video"; 
     public static final String SERVLET_CONTEXT_SELECTOR = "(" + HttpWhiteboardConstants.HTTP_WHITEBOARD_CONTEXT_NAME + "=" + 
             DMSampleApiHttpContext.CONTEXT_NAME + ")"; 

 } 
```

+++

>[!TAB ServletContext]

+++**ServletContext** 

Mount the above servlet using a `servletContext`. The following is an example of `servletContext`. 

```java
public class DMSampleApiHttpContext extends ServletContextHelper { 

 public static final String CONTEXT_NAME = "com.adobe.dmSample"; 
 public static final String CONTEXT_PATH = "/dmSample"; 

 private final MimeTypeService mimeTypeService; 

 private final AuthenticationSupport authenticationSupport; 

 /** 
  * Constructs a new context that will use the given dependencies. 
  * 
  * @param mimeTypeService Used when providing mime type of requests. 
  * @param authenticationSupport Used to authenticate requests with sling. 
  */ 
 @Activate 
 public DMSampleApiHttpContext(@Reference final MimeTypeService mimeTypeService, 
                               @Reference final AuthenticationSupport authenticationSupport) { 
     this.mimeTypeService = mimeTypeService; 
     this.authenticationSupport = authenticationSupport; 
 } 

 // ---------- HttpContext interface ---------------------------------------- 
 /** 
  * Returns the MIME type as resolved by the <code>MimeTypeService</code> or 
  * <code>null</code> if the service is not available. 
  */ 
 @Override 
 public String getMimeType(String name) { 
     MimeTypeService mtservice = mimeTypeService; 
     if (mtservice != null) { 
         return mtservice.getMimeType(name); 
     } 
     return null; 
 } 

 /** 
  * Returns the real context path that is used to mount this context. 
  * @param req servlet request 
  * @return the context path 
  */ 
 public static String getRealContextPath(HttpServletRequest req) { 
     final String path = req.getContextPath(); 
     if (path.equals(CONTEXT_PATH)) { 
         return ""; 
     } 
     return path.substring(CONTEXT_PATH.length()); 
 } 

 /** 
  * Returns a request wrapper that transforms the context path back to the original one 
  * @param req request 
  * @return the request wrapper 
  */ 
 public static HttpServletRequest createContextPathAdapterRequest(HttpServletRequest req) { 
     return new HttpServletRequestWrapper(req) { 

         @Override 
         public String getContextPath() { 
             return getRealContextPath((HttpServletRequest) getRequest()); 
         } 

     }; 

 } 

 /** 
  * Always returns <code>null</code> because resources are all provided 
  * through individual endpoint implementations. 
  */ 
 @Override 
 public URL getResource(String name) { 
     return null; 
 } 

 /** 
  * Tries to authenticate the request using the 
  * <code>SlingAuthenticator</code>. If the authenticator or the Repository 
  * is missing this method returns <code>false</code> and sends a 503/SERVICE 
  * UNAVAILABLE status back to the client. 
  */ 
 @Override 
 public boolean handleSecurity(HttpServletRequest request, 
                               HttpServletResponse response) throws IOException { 

     final AuthenticationSupport authenticator = this.authenticationSupport; 
     if (authenticator != null) { 
         return authenticator.handleSecurity(createContextPathAdapterRequest(request), response); 
     } 

     // send 503/SERVICE UNAVAILABLE, flush to ensure delivery 
     response.sendError(HttpServletResponse.SC_SERVICE_UNAVAILABLE, 
             "AuthenticationSupport service missing. Cannot authenticate request."); 
     response.flushBuffer(); 

     // terminate this request now 
     return false; 
 } 
}
```

+++

>[!ENDTABS]



### Use the sample servlet

You invoke the servlet by performing a `GET` operation at `/dmSample/dynamicmedia/video/manifestUrl`. The following query parameters are passed: 

| Query parameter | Description |
| --- | --- |
| `assetPath` | Mandatory. The path to the video for which `manifestUrl` is generated. |
| `manifestType` | Optional. Parameter can be DASH or HLS. If it is not passed, it defaults to DASH. |
| `onlyIfPublished` | Optional. If passed, the `manifestUrl` is returned only if the video is published.  |

In this example, let us assume the following setup: 

* The company is `samplecompany`.
* The authoring instance is `http://sample-aem-author.com`.
* The folder `/content/dam/video-example` has a video encoding profile applied to it. 
* The video `scenery.mp4` is uploaded to the folder `/content/dam/video-example`.

You can invoke the servlet in following ways: 
     
| Type | Description |
| :--- | --- |
| HLS | `http://sample-aem-author.com/dmSample/dynamicmedia/video/manifestUrl?manifestType=HLS&assetPath=/content/dam/video-example/scenery.mp4`<br><br>In case DASH delivery is enabled:<br>`{"manifestUrl":"https://s7d1.scene7.com/is/content/samplecompany/scenery-AVS.m3u8?packagedStreaming=true"}`<br><br>In case DASH delivery is disabled:<br>`{"manifestUrl":"https://s7d1.scene7.com/is/content/samplecompany/scenery-AVS.m3u8"}` |
| DASH | `http://sample-aem-author.com/dmSample/dynamicmedia/video/manifestUrl?manifestType=DASH&assetPath=/content/dam/video-example/scenery.mp4`<br><br>In case DASH delivery is enabled:<br>`{"manifestUrl":"https://s7d1.scene7.com/is/content/samplecompany/scenery-AVS.mpd"}`<br><br>In case DASH delivery is disabled:<br>`{}` |
| Error: asset path is wrong | `http://sample-aem-author.com/dmSample/dynamicmedia/video/manifestUrl?manifestType=DASH&assetPath=/content/dam/video-example/scennnnnnery.mp4`<br><br>`{"errorString":"could not retrieve the resource from JCR"}` |

-->





