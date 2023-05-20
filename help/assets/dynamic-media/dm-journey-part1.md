---
title: Dynamic Media歷程，第一部分
description: Dynamic Media歷程涵蓋Dynamic Media的基礎知識、運作方式、可為您做的事情，以及可為您的工作和客戶帶來哪些價值。
contentOwner: Rick Brough
products: Experience Manager as a Cloud Service
topic-tags: introduction,administering
content-type: reference
feature: Image Profiles
role: User, Admin
mini-toc-levels: 4
hide: false
hidefromtoc: false
exl-id: f3472006-d5ae-4f70-af3e-44e73aee85cc
source-git-commit: 803c4dc44189d58ddbd2669b00dd8107b2a926ae
workflow-type: tm+mt
source-wordcount: '3708'
ht-degree: 1%

---

# Dynamic Media歷程：基礎知識，第一部分 {#dm-journey-part1}

歡迎使用Dynamic Media歷程。

此歷程涵蓋Dynamic Media的基礎知識、運作方式、可為您做的事情，以及可為您的工作和客戶帶來什麼價值。

**_前提条件_**

* 對影像和視訊格式的基本瞭解
* 對HTML和CSS的基本瞭解
* 基本瞭解Adobe Illustrator、Adobe Photoshop、Adobe XD等設計工具
* 在Experience Manager上存取Dynamic Media很有幫助，但不是必要操作

**_您可以期待瞭解的內容_**

_第一部分_

* 什麼是Dynamic Media以及它如何協助您？
* Dynamic Media的使用案例
* 資產如何流經Dynamic Media系統

_第二部分_

* Dynamic Media URL的剖析，以及Dynamic Media如何傳遞內容
* 建立影像預設集以轉譯資產的基礎知識
* 影像集、迴轉集和混合媒體集

**_對象_**
最適合此歷程讀者的Experience Manager對象是以下剛開始使用Dynamic Media的人：

* 管理员
* 業務分析人員
* 内容架构师
* 内容作者
* Designer
* 开发人员
* 行銷
* 產品經理/擁有者

>[!TIP]
>
>為達到最佳效果，Adobe建議您透過桌上型電腦閱讀及檢視此Dynamic Media歷程。

## 什麼是Dynamic Media以及它如何協助您？ {#dm-journey-a}

Dynamic Media可協助您隨選提供豐富的視覺化銷售和行銷資產。 它也能協助您建立並提供互動式檢視體驗，包括縮放、360度旋轉和視訊。 您的資產會動態調整規模，以因應網路、行動裝置和社交網站上的使用量。 使用影像、視訊和3D等一組主要來源資產，Dynamic Media會透過其全球性、可擴充、效能最佳化的CDN （內容傳遞網路），即時產生並傳遞這種豐富內容的多種變體。

Dynamic Media整合了Adobe Experience Manager Assets數位資產管理解決方案的工作流程，以簡化及簡化數位行銷活動管理流程。

### 單一檔案提供無限的可能性

Dynamic Media的其中一個要點是以下概念 _單一主要資產檔案，無限可能_.

若要更深入瞭解此概念，請思考您傳統上使用單一資產（例如影像或影片）的方式。 您通常會建立一個主要資產。 接著，您可以為每個體驗、所需的每個裝置、每個網頁以及使用資產的每個屬性，手動建立相同資產的版本。 隨著時間推移，該單一資產可成長至20個、30個或更多版本，且未附加任何版本記錄。 現在，想像一下對於您擁有的每個影像或影片都這樣做。 資產版本的數目將很快變得難以維護和更新，更不用說儲存成本的增加了。

不過，Dynamic Media與其他系統截然不同，因為您使用它來傳送媒體 _動態_ 來自單一、主要資產和URL呼叫。 您請求的Dynamic Media URL路徑包含指示，告知Adobe發佈伺服器如何在資產傳送至客戶的熒幕時顯示資產。 例如，使用相同的單一主要資產，您可以讓資產以無限制的轉譯立即傳送，並變更大小、格式、解析度、重量、顏色、裁切和縮放檢視等效果。

這種獨特的傳送方式可確保將一致的品質體驗傳送至任何畫面，無論畫面大小或頻寬為何。 全尺寸視訊也針對所有熒幕型別最佳化，並以彈性方式串流，以確保一致、高品質的使用者體驗。

<!-- As part of building and publishing assets with Dynamic Media, you visually configure the effects that you want to apply to assets. In so doing, you are literally building the URL that correctly tells the publish server how to deliver your primary asset to the screen.  -->

![Adobe Dynamic Media會將相同的主要影像提供給不同大小和格式的不同媒體。](/help/assets/dynamic-media/assets/dm-oneasset-multioutput.png)
_AdobeDynamic Media可確保為任何熒幕提供一致、高品質的體驗，無論熒幕大小或頻寬為何。_

隨著您深入瞭解，「單一主要資產檔案，無限可能性」的概念為何如此重要。

### 內容傳遞網路

當您準備好使用影像資產或視訊資產時，Dynamic Media的骨幹系統會提供支援，包括功能強大的頂層傳送網路。 該網路每天為全球數百個使用者端提供服務。 資產會分散在由Akamai託管的內容傳遞網路（或CDN）上。 CDN是一種以網路連線方式的電腦服務系統，能以透明的方式合作，將內容（尤其是大型多媒體內容）傳送給一般使用者。

在CDN系統中，網頁內容會儲存在網際網路上的網頁快取中。 然後它會從Web快取傳送給一般使用者，以加快傳送速度。 因此，第一次有人下載網頁時，他們看到的資產會傳送到CDN快取。 它們會儲存在伺服器上，以便下次同一區域中的某人存取網頁時，相同快取內容會傳送得更快。 因為位置更接近一般使用者，所以可更快速地提供內容。 CDN可讓網頁顯示速度更快，但會降低中央伺服器的頻寬需求，因為內容是透過快取網路傳送，而不是透過每個執行個體的中央伺服器傳送。 此最佳化的流程意味著更佳的使用者體驗，進而帶來更高的銷售額。

<!-- USE AN IMAGE HERE? ![Content delivery network](/help/assets/assets-dm/cdn.png) -->

過去，CDN每個月都會向客戶傳送3.5 PB的流量。 此系統在一天內可提供520億個資產。 這個數字相當於成功傳送給客戶的864,000張影像和影片， _每秒_.

### 智能成像

Dynamic Media在最佳化資產以及確保每個資產透過CDN在行動裝置和桌上型電腦系統上快速載入方面都做得很出色。 為了達到此目的，Dynamic Media會使用影像預設集來定義影像品質。 它們也會定義您要傳送的影像型別、其銳利度，以及體驗或頁面不同部分的其他片段。

但若要在影像預設集之外進一步增加Dynamic Media的價值，可使用 _智慧型影像_.

智慧型影像處理會根據客戶的瀏覽器功能，自動最佳化影像的格式和檔案大小，以提供更優異的影像資產傳送效能。 它可搭配您現有的影像預設集運作（此歷程第二部分將討論影像預設集），並在傳送時使用智慧。

此智慧功能可依據瀏覽器和網路連線速度，進一步縮小影像檔案大小。 由於影像資產佔頁面載入時間的大部分，因此效能改善會對關鍵業務指標產生徹底影響，例如：

* 較高的轉換
* 網站逗留時間
* 較低的網站跳出率

整體而言，使用智慧型影像處理，視您現有的影像預設集設定和特定的使用者特性而定，效能可望提升22%至47%。 同時保持影像品質，如同從未接觸過一樣。

![智慧型影像](/help/assets/dynamic-media/assets/dm-smart-imaging.png)
_智慧型影像可根據客戶的瀏覽器功能和網路速度，自動最佳化影像的格式和檔案大小。_

預設不會開啟智慧型影像處理，因為您需要與AdobeDynamic Media技術支援人員協調工作。 此外，啟用智慧型影像處理需要完全清除CDN快取，然後再重新填入時間。 如果您有興趣使用智慧型影像，可以透過提交技術支援票證來與Adobe合作，以將其開啟。 然後，技術支援會為您提供URL引數，讓您預先嘗試智慧型影像。 您可以在任何網頁或影像上試用，瞭解獲得的效能和省下的錢。 然後，您就可以為完整網站開啟智慧型影像處理。

### 最適化視訊集

當頁面上或主要頁面上出現影片時，您的客戶往往會更長時間與該內容互動，並在頁面上停留更久，這通常是好事。 Adobe已完成的分析會展示此行為。 不過，視訊可能會很複雜。 首先，您通常有一個大型的主要檔案。 要決定如何調整大小和傳送視訊，相當複雜，這都是為了確保體驗能順暢地執行，無論裝置上檢視了什麼，也不論頻寬為何。

為了解決此問題，Dynamic Media可讓您建立 _最適化視訊集_.

![最適化視訊集](/help/assets/dynamic-media/assets/dm-smart-imaging.png)
_「自我調整視訊集」會將使用不同位元速率和格式編碼的相同視訊版本分組。_

您先從上傳至系統的原始主要視訊開始。 Dynamic Media會自動調整大小，或 _轉碼_，即可將該視訊轉換為多個視訊。 然後，在傳送時，它會聰明地決定要使用的視訊畫面、品質和格式，並將它傳送至手機、平板電腦或桌上型電腦。

例如，在iOS行動裝置上，它會偵測4G、5G或Wi-Fi等頻寬。 之後，它會從「自我調整視訊集」內的各種視訊位元速率中，自動選取正確的編碼視訊。 影片會串流至行動裝置、平板電腦或桌上型電腦。

此外，視訊品質會在網路狀況變更時自動動態切換。 此外，如果客戶在桌上型電腦進入全熒幕模式，Adaptive Video Set會使用更好的解析度來回應，以改善客戶的觀看體驗。

使用自我調整視訊集可為客戶在多個熒幕和裝置上播放Dynamic Media視訊提供流暢、高品質的播放。 真正能省下視訊的複雜性。

## Dynamic Media的使用案例 {#dm-journey-b}

以下是Dynamic Media可協助您促進正面客戶參與、忠誠度、轉換和提高ROI的常見使用案例問題和解決方案。

### 使用案例：主要檔案方法

Dynamic Media最重要的使用案例之一，也是最明顯的使用案例之一。 也就是說，減少所傳送的頁面和體驗重量以及內容大小（無論是影像或影片）。

以下顯示典型的體驗或網頁。 一個頁面中約有90%是由豐富的媒體所組成，例如影像和視訊，這些通常是較重的檔案。

![內容頁面權數](/help/assets/dynamic-media/assets/dm-content-page-weight.png)
_典型網頁的內容頁面權數。_

其餘10%為HTML、CSS程式碼和特定標籤。 您想要最佳化該頁面90%的權重，Dynamic Media可協助您完成此工作。 在稍早的文章中，您瞭解到 _單一主要資產檔案，無限可能_. 此方法對於降低整體頁面重量相當重要。 能夠取得一個主要資產，並在產品詳細資料頁面、縮圖頁面、購物車和搜尋格線上使用它，是絕佳的節省時間。 此外，它也能確保體驗間的一致性。

![主要檔案方法](/help/assets/dynamic-media/assets/dm-onefile.png)
_手錶是一個主要資產檔案，但會即時建立多個轉譯（而非復本）。_

讓我們更詳細地瞭解Dynamic Media透過單一檔案解決的問題，以及這種方法的一些解決方案。

| **问题** | **Dynamic Media解決方案** |
|---|---|
| 建立並儲存每個資產。 | 使用單一影像檔案，僅在傳送時自動建立所需的轉譯。 |
| 高儲存成本。 | 無須建立和儲存資產的多個復本。 |
| 難以維護保管鏈。 | 保證提供裝置最佳化且一致的體驗。 |
| 沒有版本記錄。 |  |
| 跨裝置的不一致品牌體驗。 |  |
| 建立重複資產的不必要成本。 |  |

每當您思考一個檔案時，您會為各種體驗建立資產。 您可能有一個起始影像，然後您必須建立該影像的20、30或40種變體，最終必須儲存並支付儲存費用。

然後您必須確定使用正確的影像，這可能會影響您維持品牌一致性的能力。 此外，如果您找不到影像，則必須返回並複製這些資產。

Dynamic Media可讓您即時從該起始影像建立各種影像。 它可讓您使用該主要資產發揮創意，不必為了建立其他內容而與平面設計藝術家或像片工作室來回切換。 這樣就能節省金錢和時間。

使用單一檔案方法時，您會使用單一主要檔案。 然後建立網站、屬性和體驗所需的這些版本或轉譯，但僅限於客戶交付或看到這些版本或轉譯時。 如此的效率可大幅減少資產所需的儲存容量，並降低整體工作流程的複雜性。 透過Dynamic Media的傳送系統，可確保最佳化每個影像和視訊、快速載入，並在所有熒幕和裝置上呈現最佳效果。

### 使用案例：影片

Dynamic Media為解決的另一個使用案例是影片。 視訊很複雜。 很難管理。 視訊檔案因其本身的檔案大小而難以儲存和移動。

| **问题** | **Dynamic Media解決方案** |
|---|---|
| 難以管理和傳送針對各種裝置最佳化的視訊。 | 使用會為所有裝置自動調整大小的單一視訊。 |
| 視訊因使用者可用的頻寬而停頓或播放品質低。 | 透過自動偵測可用頻寬並調整品質的HTML播放器，提供視訊，以確保高傳真度並順暢播放。 |
| 手動建立所有視訊版本並只為了確保跨裝置顯示和播放良好，既不可行又耗時。 | 透過簡化的工作流程，省去數小時繁瑣的轉碼工作。 |
|  | 騰出時間進行價值更高的工作。 |

客戶來到Dynamic Media時，有以下是他們希望能解決的問題：

&quot;_我們有了影片，而且花了很多錢製作它。 但我們一直迴避將影片放在頁面上，或是進行傳送，因為從測試來看，我們真的無法保證影片品質，或是影片是否真的要播放。 最終，這會影響我們的品牌，甚至影響我們的角色轉換。_&quot;

Dynamic Media的解決方案是取用那個主要視訊檔案，讓Dynamic Media透過轉碼程式完成所有大小。 然後，再與Dynamic Media的智慧型視訊播放器配對。 此工作流程可保證您在主要登陸頁面、類別或產品詳細資料頁面上使用該影片，全程保持一致，並提供高品質。

以下是其他幾個需考慮的使用案例。

### 使用案例：單一信任來源

| **问题** | **Dynamic Media解決方案** |
|---|---|
| 分散在組織各處的數位資產，分別位於不同的團隊或業務部門。 | 在一個集中位置儲存和管理所有數位資產。 |
| 團隊成員下載並建立本機版本。 | 團隊成員使用單一主要檔案來建立 _和_ 提供各種熒幕大小和裝置的所有必要版本。 |
| 為每個體驗和裝置建立的一次性資產。 | 消除一次性使用的資產，節省建立資產的時間和金錢。 |

### 使用案例：適用於多媒體的AI支援智慧型裁切

| **问题** | **Dynamic Media解決方案** |
|---|---|
| 手動繪製、測量和剪下影像或視訊，以強調焦點並在所有熒幕大小和裝置上適當地顯示，既費時又費力。 | 使用Adobe Sensei AI功能Dynamic Media中的智慧型裁切功能，自動偵測任何影像或視訊中的焦點，並裁切以維持焦點。 |
| 可以更妥善地花在打造高影響力體驗上的時間損失。 | 擷取預期的興趣點，無論熒幕大小為何。 |
| 為每個體驗和裝置建立的一次性資產。 | 省去繁瑣的手動工作，並提供高品質、快速載入的影像和視訊，在任何裝置或熒幕上看起來都很好。 |

### 使用案例：互動式媒體製作

| **问题** | **Dynamic Media解決方案** |
|---|---|
| 無法參與、無法帶來忠誠度或促進轉換的固定和靜態客戶體驗。 | 可讓非技術使用者輕鬆且順暢地新增互動式元素，例如熱點、輪播和迴轉集，以獲得更動態且吸引人的體驗。 |
| 數位資產的投資回報有限，而客戶體驗乏善可陳。 | 推動多媒體體驗的轉換和投資報酬率。 |

## 資產如何流經Dynamic Media系統 {#dm-journey-c}

以下顯示Dynamic Media的典型工作流程。

![Dynamic Media工作流程](/help/assets/dynamic-media/assets/dm-workflow.png)
_資產如何流經Dynamic Media系統。_

從建立階段開始，主要目標是在結尾擁有主要資產。 這些主要資產可能來自像片拍攝、視訊廠商，或可能是您已建立的部分音訊檔案。 您可以使用Adobe的Creative Suite應用程式(例如Adobe InDesign、Adobe Photoshop、Adobe Illustrator)來協助您編寫內容。

建立部分完成後，您可以透過將資產上傳至Dynamic Media，將資產放入製作解決方案。 在Dynamic Media中，請確定您的網站上各種網頁都排齊了正確的影像預設集和檢視器。

最終，您可以最佳化所有內容，並將其發佈至Dynamic Media伺服器，以供網路、列印、電子郵件、桌上型電腦和行動裝置使用。

### 將資產上傳至Dynamic Media

完成建立主要資產後，可將其上傳至Dynamic Media。 您上傳的檔案型別、檔案的格式和大小是Dynamic Media的重要屬性。 您想在上傳時確定從單一檔案支援中獲得最大值。

例如，下方的觀看影像為4560 x 3020畫素。 雖然您絕不能使用這個大小的影像，但您仍可以上傳它。 影像越大，Dynamic Media提供的品質就越好，甚至包括縮圖轉譯。 記住：您可以輕鬆地 _減少_ 現有影像的解析度。 但如果您嘗試 _增加_ 影像的解析度，結果可能會令人不滿意。

![建議上傳至Dynamic Media的格式](/help/assets/dynamic-media/assets/dm-upload-formats.png)
_資產上傳的考量事項。_

Adobe建議您以無損格式上傳資產。 一般而言，最好避免JPEG，因為當您傳送JPEG或繼續儲存JPEG時，您會隨著時間開始失去影像品質。 您想要以無損格式從最高解析度的影像開始，以便隨時存取。 該格式通常是TIFF或PNG檔案。

關於色彩空間，當您思考數位頻道或網頁檢視時，通常會考慮RGB（紅色、綠色、藍色）。

大多數人永遠不會想用CMYK傳送某些內容，或是您為何可能想要用CMYK傳送。 原因是因為色域最常用於傳送列印專案。 但是，Dynamic Media可同時提供兩種色彩空間。

仍有許多客戶仍使用印刷品，例如倉儲批發俱樂部。 此外還有雜貨店，他們經常每週列印傳單。 這類客戶要求他們的影像同時位於兩個色域中。 傳統上，這需要兩個不同的影像：一個是RGB影像，一個是CMYK影像。 不過，您可以直接將CMYK資產上傳至Dynamic Media，並讓Dynamic Media透過影像預設集或色彩設定檔自動傳遞RGB資產。 不需要建立多個版本的檔案，因此維護以下概念： _單一主要資產檔案，無限可能_.

<!-- **The Value of Renditioning??? or Demo portion** -->

### 發佈和預覽資產

將資產上傳至Dynamic Media後，建議您將資產上傳至 _發佈_ 選取資產，然後按一下 **[!UICONTROL 發佈]** 或 **[!UICONTROL 快速發佈]** 在Dynamic Media中。 如果您想要在任何體驗中使用資產，則必須發佈資產。 發佈資產後，您可使用複製的由Dynamic Media產生的URL將資產加入網頁，或是在頁面上內嵌程式碼。

除了手動發佈資產外，您可以設定Dynamic Media，以便在上傳時立即發佈資產（無需任何使用者介入）。

上傳後，您可以在Dynamic Media中預覽資產的轉譯有不同的方式。 預覽轉譯可協助您瞭解客戶所看到的內容。 常見的預覽方法是選取資產，然後選取 _影像預設集_ 如下列所示。

![根據大型影像預設集預覽資產的轉譯](/help/assets/dynamic-media/assets/dm-image-preset-with-url.png)
_根據選取的「大」影像預設集預覽資產的轉譯。 已按一下URL按鈕。 產生的URL路徑包含「大」影像預設集名稱，且可用於網頁。_

上述URL為即時網址！ [試試看](http://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_28563982?$Large$){target="_blank"}.

另一種預覽資產的方法是選取影像資產，然後選取 _檢視者_ 預設集，如下所述。

![根據縮放垂直光源檢視器預設集預覽資產](/help/assets/dynamic-media/assets/dm-viewer-preset.png)
_根據選取的「ZoomVertical_light」檢視器預設集預覽資產。 滑鼠指標(`+`)移到手錶上放大顯示。 注意URL和內嵌按鈕。_

以上轉譯為即時轉譯！ [試試看](https://s7d1.scene7.com/s7viewers/html5/ZoomVerticalViewer.html?asset=jpearldemo/AdobeStock_28563982&amp;config=jpearldemo/ZoomVertical_light){target="_blank"}.

## 選擇性 — 瞭解更多

此歷程的第一部分涵蓋各種Dynamic Media主題的基礎知識。 如果您想進一步瞭解您剛剛閱讀的內容，請使用以下資料更詳細地探索概念。 否則，您可以繼續歷程的第二部分。 另請參閱 [此Dynamic Media歷程的下一步發展](#whats-next).

_Dynamic Media說明主題_

* [在Experience Manager中使用Dynamic Media](/help/assets/dynamic-media/dynamic-media.md)
* [關於智慧型影像](/help/assets/dynamic-media/imaging-faq.md)
* [如何建立最適化視訊集](/help/assets/dynamic-media/video.md)
* [优化图像质量的最佳实践](/help/assets/dynamic-media/best-practices-for-optimizing-the-quality-of-your-images.md)
* [如何上傳資產](/help/assets/add-assets.md#upload-assets)
* [如何預覽資產](/help/assets/dynamic-media/previewing-assets.md)
* [如何預覽3D資產](/help/assets/dynamic-media/previewing-3d-assets.md)
* [如何傳遞Dynamic Media資產](/help/assets/dynamic-media/delivering-dynamic-media-assets.md)
* [如何發佈資產](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)
* [使用 Dynamic Media 中的“选择性发布”功能](/help/assets/dynamic-media/selective-publishing.md)

_Dynamic Media教學課程_

* [使用Dynamic Media搭配Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-overview-feature-video-use.html)
* [Adobe Experience Manager內容庫](https://experienceleague.adobe.com/?lang=en#recommended/solutions/experience-manager) (搜尋依據 _Dynamic Media_)

_Dynamic Media檢視器_

* [即時示範](https://landing.adobe.com/zh-Hans/na/dynamic-media/ctir-2755/live-demos.html) 每個檢視者的

## 此Dynamic Media歷程的下一步發展 {#whats-next}

在此歷程的第二部分中，您會更進一步檢查Dynamic Media URL，以更清楚瞭解傳送資產時發生的情況。 您也會深入瞭解建立影像預設集以轉譯資產的基礎知識，並瞭解影像集、迴轉集和混合媒體集及其建立方式。

帶我前往 [Dynamic Media歷程：基礎知識，第二部分](/help/assets/dynamic-media/dm-journey-part2.md#dm-journey-d).

<!-- Live as of April 28 2022. LEAVE IN HERE https://landing.adobe.com/en/na/dynamic-media/ctir-2755/index.html -->