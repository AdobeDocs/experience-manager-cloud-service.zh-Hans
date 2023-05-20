---
title: 您的收件箱
description: 使用收件匣管理您的工作
exl-id: 37d0cf43-192f-4a50-b174-42d7dced3b63
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 76%

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

您會在自己的收件匣中收到這些通知，您可以在其中檢視通知並採取行動。

>[!NOTE]
>
>如需有關料號型態的進一步資訊，另請參閱：
>
>* [项目](/help/sites-cloud/authoring/projects/overview.md)
>* [專案 — 使用任務](/help/sites-cloud/authoring/projects/tasks.md)
>* [工作流](/help/sites-cloud/authoring/workflows/overview.md)


## 标题中的收件箱 {#inbox-in-the-header}

從任何控制檯中，收件匣中目前的專案數量會顯示在標題中。 指標也可以開啟，以提供對需要動作的頁面的快速存取權或收件匣的存取權：

![标题中的收件箱概述](/help/sites-cloud/authoring/assets/inbox-header.png)

>[!NOTE]
>
>某些動作也會顯示於 [適當資源的卡片檢視](/help/sites-cloud/authoring/getting-started/basic-handling.md#card-view).

## 開啟收件匣 {#opening-the-inbox}

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

對於這兩個檢視（「清單」和「行事曆」），您可以定義設定：

* **日历视图**

   對象 **行事曆檢視** 您可以設定：

   * **分組依據**
   * **计划**&#x200B;或&#x200B;**无**
   * **卡片大小**

   ![收件箱日历视图设置](/help/sites-cloud/authoring/assets/inbox-calendar-settings.png)

* **列表视图**

   對象 **清單檢視** 您可以設定排序機制：

   * **排序依據**
   * **排序顺序**

   ![收件箱列表视图设置](/help/sites-cloud/authoring/assets/inbox-list-settings.png)

   您还可以将日历委派给其他用户，向其他用户请求委派以及管理您的委派。

   ![收件箱列表视图委派设置](/help/sites-cloud/authoring/assets/inbox-delegation.png)

## 对某个项目执行操作 {#taking-action-on-an-item}

>[!NOTE]
>
>尽管可以选择多个项目，但一次只能对一个项目执行操作。

1. 若要對專案執行動作，請選取適當專案的縮圖。 適用於該專案的動作圖示將顯示在工具列中：

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
   >* 工作流程專案 —  [參與工作流程](/help/sites-cloud/authoring/workflows/participating.md)


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

您可以從收件匣建立任務：

1. 選取 **建立**，則 **任務**.
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

1. 選取 **提交**.

## 创建项目 {#creating-a-project}

您可以針對特定工作建立 [專案](/help/sites-cloud/authoring/projects/overview.md) 根據該任務：

1. 點選/按一下縮圖，選取適當的工作。

   >[!NOTE]
   >
   >只有使用&#x200B;**收件箱**&#x200B;的&#x200B;**创建**&#x200B;选项创建的任务才能用于创建项目。
   >
   >不能使用工作项（来自工作流）创建项目。

1. 从工具栏中选择“**创建项目**”以打开向导。
1. 選取適當的範本，然後 **下一個**.
1. 指定必要的屬性：

   * **基本**

      * **标题**
      * **描述**
      * **开始日期**
      * **到期日期**
      * **使用者** 和角色
   * **高级**

      * **名称**
   >[!NOTE]
   >
   >另請參閱 [建立專案](/help/sites-cloud/authoring/projects/managing.md#creating-a-project) 以取得完整資訊。

1. 選取 **建立** 以確認動作。

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
