---
title: 处理任务
description: 任務表示要在內容上完成的工作專案，並用於專案中確定目前任務的完整程度
exl-id: 66f95a1f-34d0-4e2e-aa8c-addc2029a1d9
source-git-commit: fef0aef0d440eaedbf1a88cba0640e1f98e85e3e
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 19%

---

# 处理任务 {#working-with-tasks}

任務表示需要對內容完成的工作專案。 當您被指派任務時，它會顯示在「工作流程收件匣」中。 任務專案在「型別」欄中的任務值為。

任務也用於專案中，以判斷目前任務（包括工作流程任務）的完整程度。

## 追蹤專案進度 {#tracking-project-progress}

您可以透過檢視專案內活動/已完成的任務來追蹤專案進度，該專案由以下專案表示： **任務** 圖磚。 專案進度可由下列專案決定：

* **任务拼贴：**&#x200B;项目详细信息页面上的“任务拼贴”中描述了项目的整体进度。

* **任务列表：**&#x200B;单击“任务拼贴”时，将显示任务列表。此列表包含与项目相关的所有任务的详细信息。

兩者都會列出工作流程任務以及您直接在中建立的任務 **任務** 圖磚。

### 任務拼貼 {#task-tile}

如果專案有任何相關任務，專案內會顯示任務表徵圖。 「任務表徵圖」會顯示專案的目前狀態。 這是以工作流程內的現有任務為基礎，不包括未來在工作流程進行時將產生的任何任務。 下列資訊會顯示在任務拼貼中：

* 已完成任务的百分比
* 作用中任務的百分比
* 逾期任務的百分比

![“任务”拼贴](/help/sites-cloud/authoring/assets/projects-tasks-breakdown.png)

### 檢視或修改專案中的任務 {#viewing-or-modifying-the-tasks-in-a-project}

除了追蹤進度，您也可能想檢視專案的詳細資訊或修改專案。

#### 任務清單 {#task-list}

按一下「任務」表徵圖中的省略符號(...)，以顯示與專案相關的任務清單。 任務由父工作流程劃分。 任務詳細資訊連同如到期日、受指派人、優先順序和狀態等中繼資料一起顯示。

![任务列表](/help/sites-cloud/authoring/assets/projects-task-list.png)

#### 任务详细信息 {#task-details}

有关特定任务的更多信息，请在任务列表中依次点按/单击该任务和&#x200B;**打开**。

![任务详细信息](/help/sites-cloud/authoring/assets/projects-task-details.png)

### 檢視和修改任務註解 {#viewing-and-modifying-task-comments}

在「任務」詳細資訊中，您可以編輯或新增註解。 此外，專案中的所有註解都會顯示在「註解」區域中。

![有关任务的评论](/help/sites-cloud/authoring/assets/projects-tasks-comments.png)

### 新增任務 {#adding-tasks}

您可以將新任務新增至專案。 然後，這些任務會出現在「任務」表徵圖中，並可在通知收件匣中對其執行操作。

若要新增任務：

1. 在项目的任务拼贴 **中** ，点按／单击+图标。 此时将 **打开“添加任务** ”窗口。
1. 輸入工作的相關資訊。 任務的標題及指派給哪個群組是必填欄位。 內容路徑、說明、工作優先順序和到期日等額外資訊為選用。 此外，您可以選取 **進階** 標籤來輸入工作的名稱，此名稱會用來命名URL。

   ![添加任务](/help/sites-cloud/authoring/assets/projects-add-task.png)

1. 点按/单击&#x200B;**创建**。

## 使用收件匣中的任務 {#working-with-tasks-in-the-inbox}

存取任務的另一種方式是從「收件匣」。 從收件匣中，您可以開啟內容以實作必要的變更。 完成時，您會將任務狀態設定為「已完成」。 當任務指派給您所屬的使用者群組時，也會顯示在您的收件匣中。 在這種情況下，群組的所有成員都可以執行工作並完成任務。

![收件箱中的任务](/help/sites-cloud/authoring/assets/projects-task-inbox.png)

若要完成任務，請選取任務並按一下 **完成**. 將資訊新增至工作，然後按一下 **完成**. 另請參閱 [您的收件匣](/help/sites-cloud/authoring/getting-started/inbox.md) 以取得詳細資訊。

![任务通知](/help/sites-cloud/authoring/assets/projects-task-notifications.png)
