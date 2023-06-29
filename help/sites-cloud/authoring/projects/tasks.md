---
title: 处理任务
description: 任务表示要在内容上完成的工作项，并在项目中用于确定当前任务的完整性级别
exl-id: 66f95a1f-34d0-4e2e-aa8c-addc2029a1d9
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 19%

---

# 处理任务 {#working-with-tasks}

任务表示需要对内容完成的工作项目。 为您分配了任务后，该任务会显示在“工作流收件箱”中。 任务项的“类型”列中任务的值为。

任务也用在项目中，以确定当前任务（包括工作流任务）的完整性级别。

## 跟踪项目进度 {#tracking-project-progress}

您可以通过查看由表示的项目中的活动/已完成任务来跟踪项目进度 **任务** 图块。 项目进度可以通过以下方式确定：

* **任务拼贴：**&#x200B;项目详细信息页面上的“任务拼贴”中描述了项目的整体进度。

* **任务列表：**&#x200B;单击“任务拼贴”时，将显示任务列表。此列表包含与项目相关的所有任务的详细信息。

两者都列出了工作流任务和您直接在中创建的任务 **任务** 图块。

### 任务拼贴 {#task-tile}

如果项目具有任何相关任务，则项目内将显示任务拼贴。 任务拼贴显示项目的当前状态。 这基于工作流中的现有任务，不包括将来随着工作流的进行而生成的任何任务。 以下信息在任务拼贴中可见：

* 已完成任务的百分比
* 活动任务的百分比
* 过期任务的百分比

![“任务”拼贴](/help/sites-cloud/authoring/assets/projects-tasks-breakdown.png)

### 查看或修改项目中的任务 {#viewing-or-modifying-the-tasks-in-a-project}

除了跟踪进度，您可能还希望查看有关项目的更多信息或修改它。

#### 任务列表 {#task-list}

单击“任务”拼贴中的省略号(...)以显示与项目相关的任务列表。 任务由父工作流划分。 任务详细信息与元数据一起显示，如到期日期、被分派人、优先级和状态。

![任务列表](/help/sites-cloud/authoring/assets/projects-task-list.png)

#### 任务详细信息 {#task-details}

有关特定任务的更多信息，请在任务列表中依次点按/单击该任务和&#x200B;**打开**。

![任务详细信息](/help/sites-cloud/authoring/assets/projects-task-details.png)

### 查看和修改任务注释 {#viewing-and-modifying-task-comments}

在“任务详细信息”中，您可以编辑或添加注释。 此外，项目中的所有注释在“注释”区域中均可见。

![有关任务的评论](/help/sites-cloud/authoring/assets/projects-tasks-comments.png)

### 添加任务 {#adding-tasks}

您可以将新任务添加到项目。 然后，这些任务会出现在“任务”拼贴中，并出现在“通知”收件箱中以便对其执行操作。

要添加任务，请执行以下操作：

1. 在项目的任务拼贴 **中** ，点按／单击+图标。 此时将 **打开“添加任务** ”窗口。
1. 输入有关任务的信息。 任务的标题以及任务被分配到哪个组是必需的。 附加信息（如内容路径、描述、任务优先级和到期日期）是可选的。 此外，您还可以选择 **高级** 选项卡输入任务的名称，该名称用于命名URL。

   ![添加任务](/help/sites-cloud/authoring/assets/projects-add-task.png)

1. 点按/单击&#x200B;**创建**。

## 处理收件箱中的任务 {#working-with-tasks-in-the-inbox}

访问任务的另一种方法是从“收件箱”。 从收件箱中，您可以打开内容以实施所需的更改。 完成后，将任务状态设置为“已完成”。 当任务被分配给您所属的用户组时，它们也会显示在您的收件箱中。 在这种情况下，组的任何成员都可以执行工作并完成任务。

![收件箱中的任务](/help/sites-cloud/authoring/assets/projects-task-inbox.png)

要完成任务，请选择该任务并单击 **完成**. 将信息添加到任务，然后单击 **完成**. 参见 [您的收件箱](/help/sites-cloud/authoring/getting-started/inbox.md) 了解更多信息。

![任务通知](/help/sites-cloud/authoring/assets/projects-task-notifications.png)
