---
title: 您的收件箱
description: 使用收件箱管理您的任务
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# 您的收件箱 {#your-inbox}

您可以接收来自AEM各个区域（包括工作流和项目）的通知。 例如，您可能会收到有关以下内容的通知：

* 任务：
   * These can also be created at various points within the AEM UI, for example, under **Projects**.
   * These can be the product of a workflow **Create Task** or **Create Project Task** step.
* 工作流：
   * 表示您需要对页面内容执行的操作的工作项
      * These are the product of workflow **Participant** steps.
   * 失败项，允许管理员重试失败的步骤

您可以在自己的收件箱中接收这些通知，以便查看并采取相应操作。

>[!NOTE]
>
>有关这些项目类型的更多信息，另请参阅：
>
>* [项目](/help/sites-cloud/authoring/projects/overview.md)
>* [项目 - 处理任务](/help/sites-cloud/authoring/projects/tasks.md)
>* [工作流](/help/sites-cloud/authoring/workflows/overview.md)


## 标题中的收件箱 {#inbox-in-the-header}

任何控制台的标题中都会显示收件箱中的当前项目数。还可以打开指示器以快速访问需要执行操作的页面或访问收件箱：

![标题中的收件箱概述](/help/sites-cloud/authoring/assets/inbox-header.png)

>[!NOTE]
>
>某些操作也将显示在[相应资源的卡片视图](/help/sites-cloud/authoring/getting-started/basic-handling.md#card-view)中。

## 打开收件箱 {#opening-the-inbox}

打开 AEM 通知收件箱：

1. 单击/点按工具栏中的指示器。

1. 选择&#x200B;**查看全部**。此时将打开 **AEM 收件箱**。收件箱会显示工作流、项目和任务中的项目。
1. 默认视图为[列表视图](#inbox-list-view)，但您也可以切换到[日历视图](#inbox-calendar-view)。可通过视图选择器（工具栏，右上角）执行此操作。

   For both views you can also define [View Settings](#inbox-view-settings). The options available are dependent on the current view.

   ![收件箱视图设置](/help/sites-cloud/authoring/assets/inbox-view-settings.png)

>[!NOTE]
>
>The Inbox operates as a console, so use [Global Navigation](/help/sites-cloud/authoring/getting-started/basic-handling.md#global-navigation) or [Search](/help/sites-cloud/authoring/getting-started/search.md) to navigate to another location when you are finished.

### 收件箱 - 列表视图 {#inbox-list-view}

此视图列出所有项目以及相关信息：

![收件箱列表视图](/help/sites-cloud/authoring/assets/inbox-list-view.png)

### 收件箱 - 日历视图 {#inbox-calendar-view}

此视图根据项目在日历中的位置显示项目：

![收件箱日历视图](/help/sites-cloud/authoring/assets/inbox-calendar-view.png)

您可以：

* Select a specific view: **Timeline**, **Column**, **List**
* Specify the tasks to display according to **Schedule**: **All**, **Planned**, **In Progress**, **Due Soon**, **Past Due**
* 向下展开以了解有关项目的更多详细信息
* 选择日期范围以集中查看：

![收件箱日历视图日期范围](/help/sites-cloud/authoring/assets/inbox-calendar-range.png)

### 收件箱 - 视图设置 {#inbox-view-settings}

对于这两个视图（列表和日历），您可以定义设置：

* **日历视图**

   对于&#x200B;**日历视图**，您可以配置：

   * **分组依据**
   * **计划**&#x200B;或&#x200B;**无**
   * **卡片大小**
   ![收件箱日历视图设置](/help/sites-cloud/authoring/assets/inbox-calendar-settings.png)

* **列表视图**

   对于&#x200B;**列表视图**，您可以配置排序机制：

   * **排序方式**
   * **排序顺序**
   ![收件箱列表视图设置](/help/sites-cloud/authoring/assets/inbox-list-settings.png)

   您还可以将日历委派给其他用户，并请求其他用户委派和管理您的委托。

   ![收件箱列表视图委派设置](/help/sites-cloud/authoring/assets/inbox-delegation.png)

## 对某个项目执行操作 {#taking-action-on-an-item}

1. 要对某个项目执行操作，请选择相应项目的缩略图。工具栏中将显示适用于该项目的操作图标：

   ![选择收件箱项目](/help/sites-cloud/authoring/assets/inbox-select-item.png)

   这些操作适用于该项目，具体包括：

   * **完整操作** (Complete action)
   * **委派** （项目）
   * **打开项** ，根据项的类型，此操作可以：

      * 显示项目属性
      * 打开相应的功能板或向导以执行进一步操作
      * 打开相关文档
   * **回退** 到上一步
   * 查看工作流的有效负荷
   * 从项目创建项目
   >[!NOTE]
   >
   >有关更多信息，请参阅：
   >
   >* 工作流项目 - [参与工作流](/help/sites-cloud/authoring/workflows/participating.md)


1. 根据所选项目，将启动一个操作，例如：

   * 将打开与操作对应的对话框
   * 将启动操作向导
   * 将打开文档页面
   For example, **Delegate** will open a dialog:

   ![委派收件箱任务](/help/sites-cloud/authoring/assets/inbox-assign-task.png)

   根据是否已打开对话框、向导和文档页面，您可以：

   * 确认相应的操作，例如重新分配。
   * 取消操作
   * 选择返回箭头可返回到收件箱，例如，如果操作向导或文档页面已打开，则可返回收件箱。


## 创建任务 {#creating-a-task}

您可以从收件箱中创建任务：

1. 选择&#x200B;**创建**，然后选择&#x200B;**任务**。
1. Complete the necessary fields in the **Basic** and **Advanced** tabs (only the **Title** is mandatory, all others are optional):

   * **基本**：

      * **标题**
      * **项目**
      * **被分派人**
      * **内容**（与“有效负荷”类似）是任务对存储库中某个位置的引用
      * **描述**
      * **任务优先级**
      * **开始日期**
      * **到期日期**
   ![收件箱添加任务](/help/sites-cloud/authoring/assets/inbox-create-task.png)

   * **高级**

      * **名称**：此选项将用于形成URL，如果为空，则将基于标 **题**。
   ![收件箱添加任务高级选项](/help/sites-cloud/authoring/assets/inbox-add-task-advanced.png)

1. 选择&#x200B;**提交**。

## 创建项目 {#creating-a-project}

对于某些任务，您可以创建一个基于该任务的[项目](/help/sites-cloud/authoring/projects/overview.md)：

1. 通过点按/单击缩略图选择相应的任务。

   >[!NOTE]
   >
   >Only tasks created using the **Create** option of the **Inbox** can be used to create a project.
   >
   >工作项（来自工作流）不能用于创建项目。

1. 从工具栏中选择&#x200B;**创建项目**&#x200B;以打开向导。
1. 选择相应的模板，然后选择&#x200B;**下一步**。
1. 指定所需属性：

   * **基本**

      * **标题**
      * **描述**
      * **开始日期**
      * **到期日期**
      * **用户**&#x200B;和角色
   * **高级**

      * **名称**
   >[!NOTE]
   >
   >有关完整信息，请参阅[创建项目](/help/sites-cloud/authoring/projects/managing.md#creating-a-project)。

1. 选择&#x200B;**创建**&#x200B;以确认操作。

## 筛选“AEM 收件箱”中的项目 {#filtering-items-in-the-aem-inbox}

您可以筛选列出的项目：

1. 打开 **AEM 收件箱**。

1. 打开筛选器选择器：

   ![收件箱搜索](/help/sites-cloud/authoring/assets/inbox-search.png)

1. 您可以根据一系列条件筛选列出的项目，其中许多条件可以细化。例如：

   ![收件箱搜索筛选器](/help/sites-cloud/authoring/assets/inbox-search-filter.png)

   >[!NOTE]
   >
   >通过[视图设置](#inbox-view-settings)，您还可以在使用[列表视图](#inbox-list-view)时配置排序顺序。
