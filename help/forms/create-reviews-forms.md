---
title: 在表單中建立和管理稽核
seo-title: Creating and managing reviews in forms
description: 檢閱是一種機制，可讓一個或多個檢閱者對表單中可用的資產進行評論。
seo-description: A Review is a mechanism that allows one or more reviewers to comment on an asset that is available in a form.
topic-tags: forms-manager
exl-id: 378049f8-bf21-4595-819d-ba5fba7023c0
source-git-commit: 9cff6e94b38016f008fd8177be2e071a530d80b6
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 0%

---

# 建立和管理表單中資產的稽核{#creating-and-managing-reviews-for-assets-in-forms}

## 审核 {#review}

稽核是一種機制，可讓一個或多個稽核者對表單中可用的資產進行評論。

## 設定稽核 {#setting-up-a-review}

1. 導覽至Forms索引標籤並選取表單。
1. 如果表單沒有正在進行的稽核，則開始稽核 ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) 圖示會出現在「動作」列中。 按一下開始複查 ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) 圖示。
1. 輸入下列資訊：

   * 標題：必要，可包含英數字元、連字型大小或底線。
   * 說明：選用，說明複查的目的/內容。
   * 截止日期：選用，稽核結束的日期。 超過截止日期時，任務會顯示為「過期」。
   * 稽核者：至少必須有一個。 輸入群組名稱或使用者名稱會列出服務使用者群組以外的所有相符名稱。 選取名稱並按一下「新增」。

1. 按一下「開始」以開始複查。

>[!NOTE]
>
>* 管理員可以存取與表單使用者相關聯的任何群組。
>* 服務使用者群組無法供選取檢閱。


### 設定稽核時發生的動作 {#actions-that-occur-when-a-review-is-set-up}

本節說明建立或設定稽核時會發生什麼情況。

1. 會建立新的稽核任務並指派給所選的稽核者。
1. 所有稽核者都會被指派稽核任務。 任務會出現在其通知區段中。 檢閱者可以按一下通知，或前往「收件匣」檢視工作。 稽核者可以按一下以開啟稽核任務、檢視表單並開始新增註釋。

   ![檢閱者通知警報](assets/review-notification-img.png)

   檢閱者通知警報

1. 註解方塊可供表單的檢閱者使用。 其他人可以檢視註解，但無法寫入註解。

## 管理評論 {#managing-a-review}

>[!NOTE]
>
>只能修改正在進行的稽核。 無法修改已完成的稽核。

1. 導覽至Forms索引標籤並選取表單。

1. 如果資產正在進行檢閱，而您是檢閱的發起人，則需執行「管理檢閱」 ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) 圖示會出現在「動作」列中。 只有稽核發起人可以管理（更新/結束）稽核。

   按一下「管理檢閱」 ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png)圖示。

   對於啟動器以外的使用者，管理檢閱圖示會停用。

1. 您會看到一個顯示資訊的畫面：

   * **標題**：無法編輯。

   * **說明**：可供編輯。

   * **期限**：可供編輯。 您可以將截止日期修改為目前日期及時間之後的任何日期及時間。

   * **檢閱者名稱**：可供編輯。 您可以新增或移除稽核者。 如果任務過期，您只能在截止日期延長至目前日期之後新增稽核者。

1. 編輯必要的欄位，然後按一下「完成」。

   ![在任務管理員中檢閱更新的狀態](assets/manage-review-img.png)

   在任務管理員中檢閱更新的狀態

1. 若要結束檢閱，請按一下「結束檢閱」。

### 修改稽核時發生的動作 {#actions-that-occur-when-a-review-is-modified}

本節說明檢閱更新/結束時的作業：

1. 如果修改了「稽核」描述，則會更新稽核者和發起者的相應任務。
1. 如果修改了稽核截止日期，稽核者的對應任務會以新日期更新。

1. 如果移除稽核者：

   ![移除稽核者](assets/removeduser.png)

   移除稽核者

   1. 如果未完成，則指派的任務會終止。
   1. 稽核者無法再對表單發表評論。

1. 如果新增稽核者：

   ![新增稽核者](assets/addedreviewer.png)

   新增稽核者

   1. 稽核任務已建立並指派給新加入的稽核者。
   1. 新加入的稽核者可新增表單相關註解。

1. 當稽核結束時：

   1. **檢閱者**：對於每個稽核者，與稽核相關的未完成任務會終止。 任務在檢閱者的「通知」區段中不再顯示為「待定」。
   1. **發起人**：指派給檢閱發起人的任務已標籤為完成。 任務會從稽核發起人的Notification區段中移除。
   1. **全部**：評論會顯示在「先前的評論」區段中。 無法新增更多註解。
      ![檢閱完成](assets/review-complete-imgg.png)
