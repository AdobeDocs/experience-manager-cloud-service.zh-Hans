---
title: as a Cloud Service在Screens中建立和管理頻道
description: 本頁面說明如何在Screens中以as a Cloud Service方式建立和管理頻道。
exl-id: 3b0bae7a-4a45-485a-ab04-604510ff6578
source-git-commit: 9db22dca0fd6debaff0d93e1958e59536efabad8
workflow-type: tm+mt
source-wordcount: '1107'
ht-degree: 1%

---

# 在Screens中建立和管理頻道as a Cloud Service {#creating-channels-screens-cloud}

建立AEM Screens專案後，您必須建立管道。
***頻道***，顯示一系列內容（影像和影片）、網站或單頁應用程式。

## 目标 {#objective}

本檔案可協助您瞭解如何在Screens內容提供者中建立和管理您AEM Screens專案的管道。 閱讀本檔案後，您應該：

* 瞭解如何建立Screens內容提供者的管道
* 管理和編輯您的頻道中的內容
* 頻道的啟用排程

## 在Screens中建立新序列頻道的步驟as a Cloud Service {#create-new-channel}

>[!NOTE]
>**前提条件**
>在開始本指南的本節之前，請檢閱 [在Screens中建立和管理專案as a Cloud Service](/help/screens-cloud/creating-content/creating-projects-screens-cloud.md).

請依照下列步驟，在Screensas a Cloud Service中建立新的序列頻道：

1. 導覽至Screens內容提供者。

1. 導覽至您的AEM Screens專案，例如 *第一數位體驗*.

1. 選取 **頻道** 來自您專案的資料夾，例如 **第一數位體驗** —> **頻道** 並按一下 **建立** 動作列中的。

   ![](/help/screens-cloud/assets/create-content/channel-create1.png)

1. 選取範本，例如 **序列頻道** 從 **建立** 精靈並按一下 **下一個**.

   ![](/help/screens-cloud/assets/create-content/channel-create2.png)
   >[!NOTE]
   > 此 **建立** 精靈會在建立管道時提供不同型別的範本。 請參閱區段 [可用的範本](#available-templates) 在建立精靈中取得詳細資訊。

1. 輸入序列管道的名稱，例如 **LoopingChannelOne** 並按一下 **建立**.

   ![](/help/screens-cloud/assets/create-content/channel-create3.png)

   您現在會看到 **LoopingChannelOne** (位於您的AEM Screens專案的「頻道」資料夾中)。

   建立管道後，您現在可以將內容新增到管道中。 請參閱 [新增內容至頻道](#add-content) 以瞭解如何將資產（影像/影片）新增至您的頻道。

## 管理管道 {#managing-channels}

您可以編輯、檢視屬性和控制面板，複製、預覽和刪除管道。

從您的專案導覽至頻道，然後選取頻道，如下圖所示。 您現在可以選取選項，例如編輯頻道、檢視屬性、預覽內容、管理出版物，或從動作列刪除頻道。

![](/help/screens-cloud/assets/create-content/channelprop1.png)

### 新增內容至頻道 {#add-content}

若要新增或編輯管道中的內容，請遵循下列步驟：

1. 選取您要編輯的頻道，如下圖所示。 按一下 **編輯** 從動作列的左上角開啟編輯器。

   ![](/help/screens-cloud/assets/create-content/edit-channel1.png)

1. 編輯器可讓您將資產/元件新增至您要發佈的管道。

1. 從左側窗格拖放資產，並將其新增至編輯器。

   ![](/help/screens-cloud/assets/create-content/edit-channel2.png)

   >[!NOTE]
   >按一下 **預覽** 以預覽您的頻道內容。
   >![](/help/screens-cloud/assets/create-content/edit-channelpreview.png)

## 建立精靈中的可用範本 {#available-templates}

使用時，可使用下列範本 **建立** 頻道精靈：

| 可用的範本 | 描述 |
|--- |--- |
| 渠道文件夹 | 允許建立資料夾以儲存管道集合。 |
| 序列渠道 | 允許建立依序播放元件的色版（在投影片放映中逐一播放）。 |
| 左或右L列拆分畫面頻道 | 可讓內容作者在適當大小的區域中檢視不同型別的資產。 |

## 使用管道的預設指派詳細資料 {#default-channels}

此功能可讓您定義頻道的預設啟用排程，並預設用於顯示的每個指派。 此方法可讓繁瑣的排程定義不需要重複。

### 建立管道的預設指派詳細資料 {#create-default}

1. 導覽至您要設定之頻道的詳細資訊頁面。
1. 找到 **預設指派詳細資料** 並排顯示。

   ![图像](/help/screens-cloud/assets/display/Assignment1.png)

1. 按一下 **設定預設詳細資料**.
1. 設定預設指派詳細資料，包括頻道的優先順序、開始和結束日期以及循環模式，然後按一下 **指派**.

   ![图像](/help/screens-cloud/assets/display/Assignments2.png)

1. 請注意，指派的詳細資訊會顯示在 **預設指派詳細資料** 圖磚：

   ![图像](/help/screens-cloud/assets/display/Assignments3.png)

此圖磚會顯示下列資訊：
* 頻道在顯示中的預設優先順序。
* 頻道排程播放時的啟用開始和結束日期。
* 週期的綜合檢視（每小時/每日/每週/每月/每年，以及該週期的名稱）。

### 指派給顯示區時，使用預設指派詳細資料 {#default-display}

可將具有預設指派詳細資料的管道指派給以與一般管道相同的顯示方式，新增的選項可運用預設指派詳細資訊，而不是每次都手動定義自訂指派詳細資訊。

1. 導覽至您要指派該頻道的顯示詳細資訊頁面，然後按一下 **指派管道**.
或者，在「詳細目錄檢視」中選取所需的顯示，然後按一下 **指派管道**.
1. 管道指派對話方塊開啟。

   ![图像](/help/screens-cloud/assets/display/Assignments4.png)

1. 從管道選擇器中選取具有預設指派詳細資訊的所需管道。
1. 請注意頻道指派對話方塊變更，以讓您選擇預設指派詳細資料，或選取自訂指派詳細資料：

   ![图像](/help/screens-cloud/assets/display/Assignments5.png)

1. 按一下 **指派** 完成指派，或按一下 **設定自訂指派詳細資料** 如果您偏好以該特定顯示內容中的某些其他值來覆寫預設值。

   ![图像](/help/screens-cloud/assets/display/Assignments6.png)

1. 請注意 **已指派的管道** 圖磚會以新指派更新：

   ![图像](/help/screens-cloud/assets/display/Assignments7.png)

1. 請注意，視頻道使用自訂排程（「時鐘」圖示）或繼承預設詳細資訊（「世界時鐘」圖示）而定，頻道會有不同的圖示，按一下這些圖示會顯示排程詳細資訊。
1. 另請注意，每種型別的可用動作會有所不同。

   ![图像](/help/screens-cloud/assets/display/Assignments8.png)

**注意：** 使用預設指派詳細資訊的頻道指派在顯示的內容中將不可編輯。

* 如果您需要將其變更為自訂指派，您必須先將其移除，然後使用 **設定自訂指派詳細資料** 選項。
* 如果您需要變更預設指派詳細資訊的屬性，您必須直接從管道詳細資訊頁面執行此操作。

### 從頻道移除預設指派詳細資料 {#remove-display}

1. 瀏覽至您要移除預設指派詳細資訊之管道的詳細資訊頁面。
1. 找到 **預設指派詳細資料** 在頁面中拼貼
1. 按一下 **移除預設值**.

   ![图像](/help/screens-cloud/assets/display/Assignments9.png)

1. 確認對話方塊將會顯示，詳細資訊將會符合以下條件之一：
   **答：** 管道未用於任何顯示區。

   ![图像](/help/screens-cloud/assets/display/Assignments10.png)

**b.** 管道用於單一顯示器。

![图像](/help/screens-cloud/assets/display/Assignment11.png)

**c.** 頻道用於數個顯示器。

![图像](/help/screens-cloud/assets/display/Assignments12.png)

1. 按一下 *移除* 以驗證變更。

**注意：** 從管道中移除預設指派詳細資料將會移除正在使用它的所有顯示器上的相符指派。
因此，如果沒有其他可播放的內容，可能會導致空白熒幕。

## 后续内容 {#whats-next}

現在，您已在專案中設定AEM Screens頻道，您需要發佈頻道。 請參閱 [以as a Cloud Service方式在Screens中發佈頻道](manage-publish.md) 從Screens服務提供者管理您的播放器之前。
