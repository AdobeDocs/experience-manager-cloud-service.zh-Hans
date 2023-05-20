---
title: 將頻道指派給Screens中的顯示as a Cloud Service
description: 本頁面說明如何將頻道指派給Screensas a Cloud Service的顯示器。
exl-id: ba001c18-7b05-4ae2-aa7f-9ebb320fedd0
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 1%

---

# 將頻道指派給Screens中的顯示as a Cloud Service {#assign-channel-displays-screens-cloud}

專案設定完成後，您必須將頻道指派給顯示區，才能檢視內容。

## 目标 {#objective}

當您的顯示器準備就緒，且您已新增內容至頻道並發佈後，此檔案可協助您瞭解如何將頻道指派給顯示器。 閱讀本檔案後，您應該能夠瞭解如何從Screens Services Provider將頻道指派給顯示器。

## 前提条件 {#prerequisites}

您必須先完成下列學習，才能執行下列步驟來指派頻道給顯示區：

* 建立和管理顯示區
* 建立和管理管道

## 指派頻道給顯示區的步驟 {#assign-channel-to-display}

請依照下列步驟，將頻道指派給顯示器：

1. 導覽至Screens服務提供者，然後選取 **顯示區** 從左側導覽面板。

1. 按一下 **指派頻道** 以顯示。

   ![图像](/help/screens-cloud/assets/display/assignchannel-1.png)

1. 從填入下列欄位 **指派管道** 對話方塊。

   ![图像](/help/screens-cloud/assets/display/assignchannel-2.png)

   1. 從下拉式清單中選取管道名稱。
   1. 選擇優先順序。

      >[!NOTE]
      >「優先順序」可用來對指派進行排序，以防多個指派符合播放條件。 值最高的總是優先於較低的值。 例如，如果有兩個管道A和B。A的優先順序為1，而B的優先順序為2，則會顯示管道B，因為其優先順序高於A。
   1. 選取開始日期和結束日期 **啟用**.

1. 按一下 **+新增週期** 以新增頻道的週期性排程。

   ![图像](/help/screens-cloud/assets/create-content/recurrence-1.png)

   >[!NOTE]
   >您可以將多個週期性排程新增至您的頻道。 遞回排程引入DayParting，可讓您設定在一天中的特定時間執行多個管道的全域排程，並一次重複使用該設定來顯示所有顯示器。

   您可以設定下列選項：

   * **名稱**：週期性排程的標題。
   * **重複**：選擇排程是每日、每週、每月或每年執行。
   * **開始**：排程的開始時間。
   * **結束**：排程的結束時間。 您可以依時間或持續時間設定時間。
   * **時間**：排程將在指定的時間結束。
   * **持續時間**：排程會在特定期間執行，以小時或分鐘為單位。

1. 按一下 **建立** 現在您會看到已為該顯示指派管道，如下圖所示。

   ![图像](/help/screens-cloud/assets/display/assignchannel-3.png)


## 后续内容 {#whats-next}

現在您已將頻道指派給顯示區，接下來應該檢閱檔案以繼續您的Screensas a Cloud Service歷程 [安裝和設定AEMas a Cloud Service的Screens播放器](/help/screens-cloud/managing-players-registration/installing-screens-cloud-player.md).
