---
title: as a Cloud Service在Screens中安裝和設定播放器
description: 本頁面說明如何在Screensas a Cloud Service安裝及設定播放器。
exl-id: a022738a-c543-4629-a244-f70fa294fe7f
source-git-commit: 3367977496d3edad0f6f1e27e98eac95c791e870
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 1%

---

# as a Cloud Service在Screens中安裝和設定播放器 {#installing-players-screens-cloud}

本節說明如何安裝註冊至內部部署AEM例項的AEM Screens播放器。 此外，您必須在工廠重設現有播放器，然後針對AEM Screensas a Cloud Service註冊新播放器。

## 目标 {#objective}

本檔案可協助您瞭解在註冊播放器之前如何設定播放器。 閱讀本檔案後，您應能瞭解：

* 播放器的安裝來源：
* 如何將播放器更新至雲端模式

## 將播放器設定為雲端模式的步驟 {#cloud-mode-setup}

從下載最新的播放器後 [AEM Screens播放器下載](https://download.macromedia.com/screens/)，您現在已準備好將播放器更新至雲端模式。

請依照下列步驟更新您的播放器：

1. 開啟AEM Screens播放器。

   >[!NOTE]
   >您可以選擇使用專用的硬體裝置或您自己的播放器上的Web擴充功能進行測試。

1. 按一下 **設定** 標籤並按一下 **至工廠** 按鈕於 **重設** 選項。

   ![图像](/help/screens-cloud/assets/player/installplayer-2.png)

1. 按一下 **確認** 以重設您的播放器。

1. 再次從 **設定** 標籤並按一下 **變更為雲端模式** 按鈕於 **切換執行模式** 選項。

   ![图像](/help/screens-cloud/assets/player/installplayer-1.png)

1. 按一下 **確認** 在切換到雲端模式時提示將取消註冊播放器。

## 基本播放監視 {#playback-monitoring}

播放器會報告各種播放量度，每種 `ping` 預設為30秒。 根據這些量度，我們可以偵測各種邊緣情況，例如停滯體驗、空白畫面和排程問題。 這可讓我們瞭解裝置上的問題並加以疑難排解，進而加快與您進行調查和採取修正措施。

AEM Screens播放器中的基本播放監視可讓我們：

* 遠端監視（如果播放器正確播放內容）。

* 改善對空白畫面或欄位中中斷體驗的反應性。

* 降低向一般使用者顯示中斷體驗的風險。

### 瞭解屬性 {#understand-properties}

下列屬性包含在每個 `ping`：

| 属性 | 描述 |
|---|---|
| ID {string} | 播放器識別碼 |
| activeChannel {string} | 目前播放頻道路徑，或若未排程則為空值 |
| activeElements {string} | 以逗號分隔的字串，目前所有播放順序頻道中可見的元素（如果是多區域配置，則為多個） |
| isDefaultContent {boolean} | 如果播放頻道被視為預設或備援頻道（即優先順序為1且無排程），則為true |
| hasContentChanged {boolean} | 如果內容在過去5分鐘內變更，則為真，否則為假 |
| lastContentChange {string} | 上次內容變更的時間戳記 |

>[!NOTE]
>或者，您也可以從播放器偏好設定（啟用播放監視）啟用更進階的屬性，即：
>|屬性|說明|
>|—|—|
>|isContentRendering {boolean}|true (如果GPU能確認它正在播放實際內容（根據畫素分析）|

### 限制 {#limitations}

基本播放監視的少數限制列於下方：

* 播放器會向伺服器報告自己的播放狀態，因此需要使用中的連線。

* 此 `isContentRendering` 檢查GPU的屬性目前資源過於密集，預設無法啟用，且需要從播放器偏好設定中明確選擇加入。 建議不要在生產環境中與影片結合使用。

* 此功能僅支援序列頻道，尚未涵蓋互動式頻道(SPA)使用案例。

* 這些量度尚未完全開放給我們的客戶，我們正在努力在不久的將來啟用類似控制面板的報告和警報機制。

## 后续内容 {#whats-next}

現在您已安裝播放器並設定為雲端模式，接下來應該檢閱檔案以繼續Screensas a Cloud Service歷程。 [以as a Cloud Service方式在Screens中註冊播放器](/help/screens-cloud/managing-players-registration/registering-players-screens-cloud.md) 從Screens Services Provider取得。
