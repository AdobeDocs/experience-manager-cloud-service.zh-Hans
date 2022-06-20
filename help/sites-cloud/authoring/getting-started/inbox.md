---
title: 您的收件箱
description: 使用收件箱管理您的任务
exl-id: 37d0cf43-192f-4a50-b174-42d7dced3b63
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: ht
source-wordcount: '913'
ht-degree: 100%

---

# 您的收件箱 {#your-inbox}

您可以接收来自 AEM 各个区域的通知，包括工作流和项目。例如，您可能会收到有关以下内容的通知：

* 任务：
   * 这些任务也可以在 AEM UI 的不同位置创建，例如在&#x200B;**项目**&#x200B;下创建。
   * 这些任务可以是&#x200B;**创建任务**&#x200B;工作流或&#x200B;**创建项目任务**&#x200B;步骤的产物。
* 工作流：
   * 表示您需要对页面内容执行的操作的工作项
      * 这些项目是工作流&#x200B;**参与者**&#x200B;步骤的产物。
   * 失败项目，允许管理员重试失败的步骤

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
1. 默认视图为“列 [表视图](#inbox-list-view)”，但您也可以切换到“日历 [视图”](#inbox-calendar-view)。 这是通过视图选择器（工具栏，右上方）完成的。

   对于这两个视图，您还可以定义[视图设置](#inbox-view-settings)。可用选项取决于当前视图。

   ![收件箱视图设置](/help/sites-cloud/authoring/assets/inbox-view-settings.png)

>[!NOTE]
>
>收件箱作为控制台运行，因此当您完成操作后，可使用[全局导航](/help/sites-cloud/authoring/getting-started/basic-handling.md#global-navigation)或[搜索](/help/sites-cloud/authoring/getting-started/search.md)导航到其他位置。

### 收件箱 – 列表视图 {#inbox-list-view}

该视图可列出所有项目以及相关信息：

![收件箱列表视图](/help/sites-cloud/authoring/assets/inbox-list-view.png)

### 收件箱 – 日历视图 {#inbox-calendar-view}

此视图根据项目在日历中的位置显示项目：

![收件箱日历视图](/help/sites-cloud/authoring/assets/inbox-calendar-view.png)

您可以：

* 选择一个具体视图：**时间线**、**列**、**列表**
* 根据&#x200B;**计划**&#x200B;指定要显示的任务：**全部**、**已计划**、**进行中**、**即将到期**、**已过期**
* 向下展开以深入了解项目的更多详细信息
* 选择日期范围以集中显示视图：

![收件箱日历视图日期范围](/help/sites-cloud/authoring/assets/inbox-calendar-range.png)

### 收件箱 – 视图设置 {#inbox-view-settings}

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

   您还可以将日历委派给其他用户，向其他用户请求委派以及管理您的委派。

   ![收件箱列表视图委派设置](/help/sites-cloud/authoring/assets/inbox-delegation.png)

## 对某个项目执行操作 {#taking-action-on-an-item}

>[!NOTE]
>
>尽管可以选择多个项目，但一次只能对一个项目执行操作。

1. 要对某个项目执行操作，请选择相应项目的缩略图。工具栏中将显示适用于该项目的操作图标：

   ![选择收件箱项目](/help/sites-cloud/authoring/assets/inbox-select-item.png)

   这些操作适用于该项目，具体包括：

   * **完成**&#x200B;操作
   * **委派**&#x200B;项目
   * **打开**&#x200B;项目，根据项目类型，此操作可以：

      * 显示项目属性
      * 打开相应的功能板或向导以进一步执行操作
      * 打开相关文档
   * **回退**&#x200B;到上一步
   * 查看工作流的有效负荷
   * 从该项目创建一个项目

   >[!NOTE]
   >
   >有关更多信息，请参阅：
   >
   >* 工作流项目 - [参与工作流](/help/sites-cloud/authoring/workflows/participating.md)


2. 根据所选项目，将会启动相应的操作；例如：

   * 将打开与操作对应的对话框
   * 将启动操作向导
   * 将打开文档页面

   例如，**委派**&#x200B;操作将打开一个对话框：

   ![委派收件箱任务](/help/sites-cloud/authoring/assets/inbox-assign-task.png)

   根据是否已打开对话框、向导和文档页面，您可以：

   * 确认相应的操作，例如重新分配。
   * 取消操作
   * 选择“上一步”箭头可返回到收件箱，例如，如果操作向导或文档页面已打开，则可返回收件箱。


## 创建任务 {#creating-a-task}

您可以从收件箱中创建任务：

1. 选择&#x200B;**创建**，然后选择&#x200B;**任务**。
1. 填写&#x200B;**基本**&#x200B;和&#x200B;**高级**&#x200B;选项卡中的必需字段（只有&#x200B;**标题**&#x200B;是必填项，所有其他字段都是选填项）：

   * **基本**:

      * **标题**
      * **项目**
      * **被分派人**
      * **内容**，与“有效负荷”类似，这是从任务到存储库中的位置的引用
      * **描述**
      * **任务优先级**
      * **开始日期**
      * **到期日期**

   ![收件箱添加任务](/help/sites-cloud/authoring/assets/inbox-create-task.png)

   * **高级**

      * **名称**：这将用于组建 URL，如果留空，URL 将会基于&#x200B;**标题**。

   ![收件箱添加任务高级选项](/help/sites-cloud/authoring/assets/inbox-add-task-advanced.png)

1. 选择&#x200B;**提交**。

## 创建项目 {#creating-a-project}

对于某些任务，您可以创建一个基于该任务的[项目](/help/sites-cloud/authoring/projects/overview.md)：

1. 通过点按/单击缩略图选择相应的任务。

   >[!NOTE]
   >
   >只有使用&#x200B;**收件箱**&#x200B;的&#x200B;**创建**&#x200B;选项创建的任务才能用于创建项目。
   >
   >不能使用工作项（来自工作流）创建项目。

1. 从工具栏中选择“**创建项目**”以打开向导。
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

## 筛选 AEM 收件箱中的项目 {#filtering-items-in-the-aem-inbox}

您可以筛选列出的项目：

1. 打开 **AEM 收件箱**。

1. 打开过滤器选择器：

   ![收件箱搜索](/help/sites-cloud/authoring/assets/inbox-search.png)

1. 您可以根据一系列条件筛选所列项目，其中许多条件可以进行细化；例如：

   ![收件箱搜索过滤器](/help/sites-cloud/authoring/assets/inbox-search-filter.png)

   >[!NOTE]
   >
   >通过[视图设置](#inbox-view-settings)，您还可以在使用[列表视图](#inbox-list-view)时配置排序顺序。
