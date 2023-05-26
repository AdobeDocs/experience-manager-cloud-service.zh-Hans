---
title: 参与工作流
description: 工作流通常包括需要人员在页面或资产上执行活动的步骤。
exl-id: 62192da9-0b5b-4997-9c2b-d1aee04b01f9
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '1545'
ht-degree: 45%

---

# 参与工作流 {#participating-in-workflows}

工作流通常包括需要人员在页面或资产上执行活动的步骤。 工作流会选择一个用户或组来执行活动，并将工作项分配给该人员或组。 用户会收到通知，然后可以采取相应的操作：

* [查看通知](#notifications-of-available-workflow-actions)
* [完成参与者步骤](#completing-a-participant-step)
* [委派参与者步骤](#delegating-a-participant-step)
* [对参与者步骤执行回退](#performing-step-back-on-a-participant-step)
* [打开工作流项目查看详细信息（并执行操作）](#opening-a-workflow-item-to-view-details-and-take-actions)
* [查看工作流有效负载（多个资源）](#viewing-the-workflow-payload-multiple-resources)

## 可用工作流操作通知 {#notifications-of-available-workflow-actions}

为您分配了工作项（例如，**批准内容**）后，将显示各种警报和/或通知：

* 您的 [通知](/help/sites-cloud/authoring/getting-started/inbox.md) 指示器（工具栏）将递增：

   ![通知工具栏](/help/sites-cloud/authoring/assets/workflows-notifications.png)

* 该工作项将在您的通知[收件箱](/help/sites-cloud/authoring/getting-started/inbox.md)中列出：

   ![收件箱中的通知](/help/sites-cloud/authoring/assets/workflows-inbox.png)

* 使用页面编辑器时，状态栏将显示：
   * 应用于页面的工作流的名称；例如“请求激活”。
   * 当前用户可用于工作流当前步骤的任何操作；例如，完成、委派、查看详细信息。
   * 页面所遵循的工作流的数量。 您可以：
      * 使用左/右箭头浏览各种工作流的状态信息。
      * 单击/点按实际数字以打开所有适用工作流的下拉列表，然后选择要在状态栏中显示的工作流。

   ![带多个工作流的页面](/help/sites-cloud/authoring/assets/workflows-multiple.png)

   >[!NOTE]
   >
   >状态栏只对拥有工作流权限的用户可见；例如，`workflow-users` 组的成员。
   >
   >
   >当当前用户直接参与工作流的当前步骤时，将显示操作。

* 当打开资源的&#x200B;**时间线**&#x200B;时，将会显示工作流步骤。单击/点按警报横幅时，也会显示可用的操作：

   ![时间线中的工作流](/help/sites-cloud/authoring/assets/workflows-timeline.png)

### 完成参与者步骤 {#completing-a-participant-step}

您可以完成一个项目，以允许工作流进入下一步。

在此操作中，您可以指示：

* **下一步**：要执行的下一步；您可以从提供的列表中选择
* **注释**：如果需要

您可以通过以下任一方式完成参与者步骤：

* [收件箱](#completing-a-participant-step-inbox)
* [页面编辑器](#completing-a-participant-step-page-editor)
* [时间线](#completing-a-participant-step-timeline)
* [打开工作流项目查看详细信息](#opening-a-workflow-item-to-view-details-and-take-actions)时。

#### 完成参与者步骤 — 收件箱 {#completing-a-participant-step-inbox}

请按下列步骤完成工作项目：

1. 打开 **[AEM 收件箱](/help/sites-cloud/authoring/getting-started/inbox.md)**。
1. 选择要对其执行操作的工作流项目（点按/单击缩略图）。
1. 从工具栏中选择&#x200B;**完成**。
1. 此时将打开&#x200B;**完成工作项**&#x200B;对话框。从下拉选择器中选择&#x200B;**下一步**，并根据需要添加&#x200B;**评论**。
1. 单击&#x200B;**确定**&#x200B;完成该步骤（或者单击&#x200B;**取消**&#x200B;中止该操作）。

#### 完成参与者步骤 — 页面编辑器 {#completing-a-participant-step-page-editor}

请按下列步骤完成工作项目：

1. 打开 [用于编辑的页面](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#opening-a-page-for-editing).
1. 从顶部的状态栏中选择&#x200B;**完成**。
1. 此时将打开&#x200B;**完成工作项**&#x200B;对话框。从下拉选择器中选择&#x200B;**下一步**，并根据需要添加&#x200B;**评论**。
1. 单击&#x200B;**确定**&#x200B;以完成该步骤（或者单击&#x200B;**取消**&#x200B;以中止该操作）。

#### 完成参与者步骤 - 时间线 {#completing-a-participant-step-timeline}

您也可以使用时间线来完成并推进步骤：

1. 选择所需的页面，然后打开&#x200B;**时间线**（或者先打开&#x200B;**时间线**，然后再选择页面）：

   ![完成步骤](/help/sites-cloud/authoring/assets/workflows-timeline-completing.png)

1. 单击/点按警报横幅以显示可用操作。 选择 **前进**：

   ![推进步骤](/help/sites-cloud/authoring/assets/workflows-timeline-advance.png)

1. 根据工作流，您可以选择下一步：

   ![选择下一步](/help/sites-cloud/authoring/assets/workflows-next-step.png)

1. 选择 **前进** 以确认操作。

### 委派参与者步骤 {#delegating-a-participant-step}

如果某个步骤已分配给您，但由于任何原因您无法执行操作，则可以将该步骤委派给其他用户或组。

可以委派的用户取决于分配给谁的工作项：

* 如果工作项已分配给组，则组成员可用。
* 如果将工作项分配给某个组，然后该组又将其委派给某个用户，则可以向该组的成员和该组进行委派。
* 如果工作项分配给单个用户，则无法委派该工作项。

在此操作中，您可以指示：

* **用户**：要委派给的用户；您可以从提供的列表中选择
* **注释**：如果需要

您可以通过以下任一方式委派参与者步骤：

* [收件箱](#delegating-a-participant-step-inbox)
* [页面编辑器](#delegating-a-participant-step-page-editor)
* [时间线](#delegating-a-participant-step-timeline)
* [打开工作流项目查看详细信息](#opening-a-workflow-item-to-view-details-and-take-actions)时。

#### 委派参与者步骤 — 收件箱 {#delegating-a-participant-step-inbox}

请按下列步骤委派工作项目：

1. 打开 **[AEM 收件箱](/help/sites-cloud/authoring/getting-started/inbox.md)**。
1. 选择要对其执行操作的工作流项目（点按/单击缩略图）。
1. 从工具栏中选择&#x200B;**委派**。
1. 此时将打开一个对话框。从下拉选择器中指定 **用户**（也可以是组），并根据需要添加&#x200B;**评论**。
1. 单击&#x200B;**确定**&#x200B;完成该步骤（或者单击&#x200B;**取消**&#x200B;中止该操作）。

#### 委派参与者步骤 — 页面编辑器 {#delegating-a-participant-step-page-editor}

请按下列步骤委派工作项目：

1. 打开 [用于编辑的页面](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#opening-a-page-for-editing).
1. 从顶部的状态栏中选择&#x200B;**委派**。
1. 此时将打开一个对话框。从下拉选择器中指定 **用户**（也可以是组），并根据需要添加&#x200B;**评论**。
1. 单击&#x200B;**确定**&#x200B;完成该步骤（或者单击&#x200B;**取消**&#x200B;中止该操作）。

#### 委派参与者步骤 - 时间线 {#delegating-a-participant-step-timeline}

您也可以使用时间线来委派和/或分配步骤：

1. 选择所需的页面，然后打开&#x200B;**时间线**（或者先打开&#x200B;**时间线**，然后再选择页面）。
1. 单击/点按警报横幅以显示可用操作。 选择 **更改被分派人**：

   ![委派步骤](/help/sites-cloud/authoring/assets/workflows-delegate.png)

1. 指定新的被分派人：

   ![更改被分派人](/help/sites-cloud/authoring/assets/workflows-assignee.png)

1. 选择&#x200B;**分配**，确认操作。

### 对参与者步骤执行回退 {#performing-step-back-on-a-participant-step}

如果您发现某个步骤或一系列步骤需要重复，则可以回退。 这允许您选择在工作流中较早发生的步骤进行重新处理。 工作流将返回到您指定的步骤，然后从此处继续。

在此操作中，您可以指示：

* **上一步**：要返回到的步骤；您可以从提供的列表中选择
* **注释**：如果需要

您可以通过以下任一方式对参与者步骤执行回退：

* [收件箱](#performing-step-back-on-a-participant-step-inbox)
* [页面编辑器](#performing-step-back-on-a-participant-step-page-editor)
* [时间线](#performing-step-back-on-a-participant-step-timeline)
* [打开工作流项目查看详细信息](#opening-a-workflow-item-to-view-details-and-take-actions)时。

#### 对参与者步骤执行回退 — 收件箱 {#performing-step-back-on-a-participant-step-inbox}

请按下列步骤回退：

1. 打开 **[AEM 收件箱](/help/sites-cloud/authoring/getting-started/inbox.md)**。
1. 选择要对其执行操作的工作流项目（点按/单击缩略图）。
1. 选择&#x200B;**回退**，打开对话框。
1. 指定&#x200B;**上一步**，并根据需要添加&#x200B;**评论**。
1. 单击&#x200B;**确定**&#x200B;完成该步骤（或者单击&#x200B;**取消**&#x200B;中止该操作）。

#### 对参与者步骤执行回退 — 页面编辑器 {#performing-step-back-on-a-participant-step-page-editor}

请按下列步骤回退：

1. 打开 [用于编辑的页面](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#opening-a-page-for-editing).
1. 从顶部的状态栏中选择&#x200B;**回退**。
1. 指定&#x200B;**上一步**，并根据需要添加&#x200B;**评论**。
1. 单击&#x200B;**确定**&#x200B;完成该步骤（或者单击&#x200B;**取消**&#x200B;中止该操作）。

#### 对参与者步骤执行回退 - 时间线 {#performing-step-back-on-a-participant-step-timeline}

您也可以使用时间线来回滚（回退）到上一步：

1. 选择所需的页面，然后打开&#x200B;**时间线**（或者先打开&#x200B;**时间线**，然后再选择页面）。
1. 单击/点按警报横幅以显示可用操作。 选择 **回滚**：

   ![回滚步骤](/help/sites-cloud/authoring/assets/workflows-roll-back.png)

1. 指定工作流应返回到的步骤：

   ![指定步骤](/help/sites-cloud/authoring/assets/workflows-roll-back-step.png)

1. 选择&#x200B;**回滚**，确认操作。

### 打开工作流项目以查看详细信息（并执行操作） {#opening-a-workflow-item-to-view-details-and-take-actions}

查看工作流工作项的详细信息并采取适当的措施。

工作流详细信息将显示在选项卡中，工具栏中提供了相应的操作：

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

#### 打开工作流详细信息 — 收件箱 {#opening-workflow-details-inbox}

要打开工作流项目并查看详细信息，请执行以下操作：

1. 打开 **[AEM 收件箱](/help/sites-cloud/authoring/getting-started/inbox.md)**。
1. 选择要对其执行操作的工作流项目（点按/单击缩略图）。
1. 选择&#x200B;**打开**，打开信息选项卡。
1. 如果需要，选择相应的操作，提供任何详细信息，然后单击&#x200B;**确定**&#x200B;进行确认（或单击&#x200B;**取消**）。
1. 单击&#x200B;**保存**&#x200B;或&#x200B;**取消**&#x200B;以退出。

#### 打开工作流详细信息 — 页面编辑器 {#opening-workflow-details-page-editor}

要打开工作流项目并查看详细信息，请执行以下操作：

1. 打开 [用于编辑的页面](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#opening-a-page-for-editing).
1. 从状态栏中选择&#x200B;**查看详细信息**&#x200B;以打开信息选项卡。
1. 如果需要，选择相应的操作，提供任何详细信息，然后单击&#x200B;**确定**&#x200B;进行确认（或单击&#x200B;**取消**）。
1. 单击&#x200B;**保存**&#x200B;或&#x200B;**取消**&#x200B;以退出。

### 查看工作流有效负载（多个资源） {#viewing-the-workflow-payload-multiple-resources}

您可以查看与工作流实例关联的有效负载的详细信息。 最初，显示资源包中的资源，然后您可以向下展开以显示各个页面。

要查看工作流实例的有效负荷和资源，请执行以下操作：

1. 打开 **[AEM 收件箱](/help/sites-cloud/authoring/getting-started/inbox.md)**。
1. 选择要对其执行操作的工作流项目（点按/单击缩略图）。
1. 从工具栏中选择&#x200B;**查看有效负载**&#x200B;以打开对话框。
   * 由于工作流包只是存储库中路径的指针集合，因此您可以在此处添加/删除/修改条目，以调整工作流包引用的内容。 使用 **资源定义** 组件以添加新条目。
1. 这些链接可用于打开各个页面。
