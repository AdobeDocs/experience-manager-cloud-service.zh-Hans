---
title: 参与工作流
description: 工作流程通常包括需要人員在頁面或資產上執行活動的步驟。
exl-id: 62192da9-0b5b-4997-9c2b-d1aee04b01f9
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '1545'
ht-degree: 45%

---

# 参与工作流 {#participating-in-workflows}

工作流程通常包括需要人員在頁面或資產上執行活動的步驟。 工作流程會選取要執行活動的使用者或群組，並將工作專案指派給該人員或群組。 使用者會收到通知，然後可以採取適當的動作：

* [查看通知](#notifications-of-available-workflow-actions)
* [完成参与者步骤](#completing-a-participant-step)
* [委派参与者步骤](#delegating-a-participant-step)
* [对参与者步骤执行回退](#performing-step-back-on-a-participant-step)
* [打开工作流项目查看详细信息（并执行操作）](#opening-a-workflow-item-to-view-details-and-take-actions)
* [查看工作流有效负载（多个资源）](#viewing-the-workflow-payload-multiple-resources)

## 可用工作流程動作的通知 {#notifications-of-available-workflow-actions}

为您分配了工作项（例如，**批准内容**）后，将显示各种警报和/或通知：

* 您的 [通知](/help/sites-cloud/authoring/getting-started/inbox.md) 指標（工具列）將遞增：

   ![通知工具栏](/help/sites-cloud/authoring/assets/workflows-notifications.png)

* 该工作项将在您的通知[收件箱](/help/sites-cloud/authoring/getting-started/inbox.md)中列出：

   ![收件箱中的通知](/help/sites-cloud/authoring/assets/workflows-inbox.png)

* 使用頁面編輯器時，狀態列將顯示：
   * 套用至頁面的工作流程名稱；例如「請求啟用」。
   * 目前使用者在工作流程目前步驟中可用的任何動作；例如，完成、委派、檢視詳細資訊。
   * 頁面須遵守的工作流程數量。 您可以：
      * 使用左/右箭頭，導覽各種工作流程的狀態資訊。
      * 按一下/點選實際數字，以開啟所有適用工作流程的下拉式清單，然後選取您要顯示在狀態列中的工作流程。

   ![带多个工作流的页面](/help/sites-cloud/authoring/assets/workflows-multiple.png)

   >[!NOTE]
   >
   >状态栏只对拥有工作流权限的用户可见；例如，`workflow-users` 组的成员。
   >
   >
   >當目前使用者直接參與工作流程的目前步驟時，會顯示動作。

* 当打开资源的&#x200B;**时间线**&#x200B;时，将会显示工作流步骤。當您按一下/點選警報橫幅時，也會顯示可用的動作：

   ![时间线中的工作流](/help/sites-cloud/authoring/assets/workflows-timeline.png)

### 完成參與者步驟 {#completing-a-participant-step}

您可以完成專案以允許工作流程進行到下一個步驟。

在此動作中，您可以指出：

* **下一步**：下一個要採取的步驟；您可以從提供的清單中選取
* **註解**：如有需要

您可以透過下列任一方式完成參與者步驟：

* [收件箱](#completing-a-participant-step-inbox)
* [页面编辑器](#completing-a-participant-step-page-editor)
* [时间线](#completing-a-participant-step-timeline)
* [打开工作流项目查看详细信息](#opening-a-workflow-item-to-view-details-and-take-actions)时。

#### 完成參與者步驟 — 收件匣 {#completing-a-participant-step-inbox}

使用以下程式完成工作專案：

1. 打开 **[AEM 收件箱](/help/sites-cloud/authoring/getting-started/inbox.md)**。
1. 選取您要對其執行動作的工作流程專案（點選/按一下縮圖）。
1. 从工具栏中选择&#x200B;**完成**。
1. 此时将打开&#x200B;**完成工作项**&#x200B;对话框。从下拉选择器中选择&#x200B;**下一步**，并根据需要添加&#x200B;**评论**。
1. 单击&#x200B;**确定**&#x200B;完成该步骤（或者单击&#x200B;**取消**&#x200B;中止该操作）。

#### 完成參與者步驟 — 頁面編輯器 {#completing-a-participant-step-page-editor}

使用以下程式完成工作專案：

1. 開啟 [要編輯的頁面](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#opening-a-page-for-editing).
1. 从顶部的状态栏中选择&#x200B;**完成**。
1. 此时将打开&#x200B;**完成工作项**&#x200B;对话框。从下拉选择器中选择&#x200B;**下一步**，并根据需要添加&#x200B;**评论**。
1. 单击&#x200B;**确定**&#x200B;以完成该步骤（或者单击&#x200B;**取消**&#x200B;以中止该操作）。

#### 完成参与者步骤 - 时间线 {#completing-a-participant-step-timeline}

您也可以使用时间线来完成并推进步骤：

1. 选择所需的页面，然后打开&#x200B;**时间线**（或者先打开&#x200B;**时间线**，然后再选择页面）：

   ![完成步骤](/help/sites-cloud/authoring/assets/workflows-timeline-completing.png)

1. 按一下/點選警報橫幅以顯示可用動作。 選取 **前進**：

   ![推进步骤](/help/sites-cloud/authoring/assets/workflows-timeline-advance.png)

1. 根据工作流，您可以选择下一步：

   ![选择下一步](/help/sites-cloud/authoring/assets/workflows-next-step.png)

1. 選取 **前進** 以確認動作。

### 委派參與者步驟 {#delegating-a-participant-step}

如果步驟已指派給您，但由於任何原因您無法採取行動，則您可以將該步驟委派給其他使用者或群組。

可委派的使用者取決於工作專案的指派者：

* 如果工作專案已指派給群組，則群組成員可供使用。
* 如果将工作项分配给某个组，然后该组又将其委派给某个用户，则可以向该组的成员和该组进行委派。
* 如果工作專案指派給單一使用者，則無法委派工作專案。

在此動作中，您可以指出：

* **使用者**：您要委派給的使用者；您可以從提供的清單中選取
* **註解**：如有需要

您可以從下列任一項中委派參與者步驟：

* [收件箱](#delegating-a-participant-step-inbox)
* [页面编辑器](#delegating-a-participant-step-page-editor)
* [时间线](#delegating-a-participant-step-timeline)
* [打开工作流项目查看详细信息](#opening-a-workflow-item-to-view-details-and-take-actions)时。

#### 委派參與者步驟 — 收件匣 {#delegating-a-participant-step-inbox}

使用下列程式來委派工作專案：

1. 打开 **[AEM 收件箱](/help/sites-cloud/authoring/getting-started/inbox.md)**。
1. 選取您要對其執行動作的工作流程專案（點選/按一下縮圖）。
1. 从工具栏中选择&#x200B;**委派**。
1. 此时将打开一个对话框。从下拉选择器中指定 **用户**（也可以是组），并根据需要添加&#x200B;**评论**。
1. 单击&#x200B;**确定**&#x200B;完成该步骤（或者单击&#x200B;**取消**&#x200B;中止该操作）。

#### 委派參與者步驟 — 頁面編輯器 {#delegating-a-participant-step-page-editor}

使用下列程式來委派工作專案：

1. 開啟 [要編輯的頁面](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#opening-a-page-for-editing).
1. 从顶部的状态栏中选择&#x200B;**委派**。
1. 此时将打开一个对话框。从下拉选择器中指定 **用户**（也可以是组），并根据需要添加&#x200B;**评论**。
1. 单击&#x200B;**确定**&#x200B;完成该步骤（或者单击&#x200B;**取消**&#x200B;中止该操作）。

#### 委派参与者步骤 - 时间线 {#delegating-a-participant-step-timeline}

您也可以使用时间线来委派和/或分配步骤：

1. 选择所需的页面，然后打开&#x200B;**时间线**（或者先打开&#x200B;**时间线**，然后再选择页面）。
1. 按一下/點選警報橫幅以顯示可用動作。 選取 **變更被指定者**：

   ![委派步骤](/help/sites-cloud/authoring/assets/workflows-delegate.png)

1. 指定新的被分派人：

   ![更改被分派人](/help/sites-cloud/authoring/assets/workflows-assignee.png)

1. 选择&#x200B;**分配**，确认操作。

### 對參與者步驟執行後退 {#performing-step-back-on-a-participant-step}

如果您發現某個步驟或一系列步驟需要重複，您可以後退。 這可讓您選取工作流程中先前發生的步驟，以便重新處理。 工作流程會回到您指定的步驟，然後從那裡繼續進行。

在此動作中，您可以指出：

* **上一步**：要傳回到的步驟；您可以從提供的清單中選取
* **註解**：如有需要

您可以在參與者步驟上執行下列任一項步驟執行回退：

* [收件箱](#performing-step-back-on-a-participant-step-inbox)
* [页面编辑器](#performing-step-back-on-a-participant-step-page-editor)
* [时间线](#performing-step-back-on-a-participant-step-timeline)
* [打开工作流项目查看详细信息](#opening-a-workflow-item-to-view-details-and-take-actions)时。

#### 對參與者步驟執行後退 — 收件匣 {#performing-step-back-on-a-participant-step-inbox}

請使用下列程式來後退：

1. 打开 **[AEM 收件箱](/help/sites-cloud/authoring/getting-started/inbox.md)**。
1. 選取您要對其執行動作的工作流程專案（點選/按一下縮圖）。
1. 选择&#x200B;**回退**，打开对话框。
1. 指定&#x200B;**上一步**，并根据需要添加&#x200B;**评论**。
1. 单击&#x200B;**确定**&#x200B;完成该步骤（或者单击&#x200B;**取消**&#x200B;中止该操作）。

#### 對參與者步驟執行回退 — 頁面編輯器 {#performing-step-back-on-a-participant-step-page-editor}

請使用下列程式來後退：

1. 開啟 [要編輯的頁面](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#opening-a-page-for-editing).
1. 从顶部的状态栏中选择&#x200B;**回退**。
1. 指定&#x200B;**上一步**，并根据需要添加&#x200B;**评论**。
1. 单击&#x200B;**确定**&#x200B;完成该步骤（或者单击&#x200B;**取消**&#x200B;中止该操作）。

#### 对参与者步骤执行回退 - 时间线 {#performing-step-back-on-a-participant-step-timeline}

您也可以使用时间线来回滚（回退）到上一步：

1. 选择所需的页面，然后打开&#x200B;**时间线**（或者先打开&#x200B;**时间线**，然后再选择页面）。
1. 按一下/點選警報橫幅以顯示可用動作。 選取 **回覆**：

   ![回滚步骤](/help/sites-cloud/authoring/assets/workflows-roll-back.png)

1. 指定工作流应返回到的步骤：

   ![指定步骤](/help/sites-cloud/authoring/assets/workflows-roll-back-step.png)

1. 选择&#x200B;**回滚**，确认操作。

### 開啟工作流程專案以檢視詳細資訊（並執行動作） {#opening-a-workflow-item-to-view-details-and-take-actions}

檢視工作流程工作專案的詳細資訊，並採取適當的動作。

工作流程詳細資訊會顯示在標籤中，而工具列中會顯示適當的動作：

* **工作项**&#x200B;选项卡：

   ![“工作项”选项卡](/help/sites-cloud/authoring/assets/workflows-work-item.png)

* **工作流信息**&#x200B;选项卡：

   ![“工作流”选项卡](/help/sites-cloud/authoring/assets/workflows-workflow-info.png)

   如果为该模型配置了工作流暂存，则可以根据以下内容查看进度：<!--If [Workflow Stages](/help/sites-developing/workflows.md#workflow-stages) have been configured for the model, you can view the progress according to these:-->

   ![工作流暂存](/help/sites-cloud/authoring/assets/workflows-workflow-stages.png)

* **评论**&#x200B;选项卡：

   ![“评论”选项卡](/help/sites-cloud/authoring/assets/workflows-comments.png)

您可以通过以下任一方式打开工作项详细信息：

* [收件箱](#performing-step-back-on-a-participant-step-inbox)
* [页面编辑器](#performing-step-back-on-a-participant-step-page-editor)

#### 開啟工作流程詳細資料 — 收件匣 {#opening-workflow-details-inbox}

若要開啟工作流程專案並檢視明細，請執行下列步驟：

1. 打开 **[AEM 收件箱](/help/sites-cloud/authoring/getting-started/inbox.md)**。
1. 選取您要對其執行動作的工作流程專案（點選/按一下縮圖）。
1. 选择&#x200B;**打开**，打开信息选项卡。
1. 如果需要，选择相应的操作，提供任何详细信息，然后单击&#x200B;**确定**&#x200B;进行确认（或单击&#x200B;**取消**）。
1. 单击&#x200B;**保存**&#x200B;或&#x200B;**取消**&#x200B;以退出。

#### 開啟工作流程詳細資料 — 頁面編輯器 {#opening-workflow-details-page-editor}

若要開啟工作流程專案並檢視明細，請執行下列步驟：

1. 開啟 [要編輯的頁面](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#opening-a-page-for-editing).
1. 从状态栏中选择&#x200B;**查看详细信息**&#x200B;以打开信息选项卡。
1. 如果需要，选择相应的操作，提供任何详细信息，然后单击&#x200B;**确定**&#x200B;进行确认（或单击&#x200B;**取消**）。
1. 单击&#x200B;**保存**&#x200B;或&#x200B;**取消**&#x200B;以退出。

### 檢視工作流程裝載（多個資源） {#viewing-the-workflow-payload-multiple-resources}

您可以檢視與工作流程例項相關聯的裝載詳細資料。 一開始會顯示封裝中的資源，然後您可以向下展開以顯示個別頁面。

若要檢視工作流程例項的裝載和資源：

1. 打开 **[AEM 收件箱](/help/sites-cloud/authoring/getting-started/inbox.md)**。
1. 選取您要對其執行動作的工作流程專案（點選/按一下縮圖）。
1. 从工具栏中选择&#x200B;**查看有效负载**&#x200B;以打开对话框。
   * 由於Workflow封裝只是存放庫內路徑的指標集合，您可以在此處新增/移除/修改專案，以調整Workflow封裝參照的內容。 使用 **資源定義** 元件以新增專案。
1. 這些連結可用來開啟個別頁面。
