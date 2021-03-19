---
title: Live Copy概述控制台
description: 了解Live Copy概述控制台的基础知识，快速了解Live Copy的状态，以便同步内容。
feature: 多站点管理器
role: 管理员
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 1%

---


# Live Copy概述控制台{#live-copy-overview-console}

使用&#x200B;**Live Copy概述**&#x200B;控制台，您可以：

* 视图/管理整个站点的继承。
   * 视图Blueprint树和相应的Live Copy结构，以及它们的继承状态
   * 更改继承状态，如挂起和恢复
   * 视图Blueprint和Live Copy属性
* 执行转出操作。

## 打开Live Copy概述{#opening-the-live-copy-overview}

您可以从以下位置打开Live Copy概述：

* [Blueprint页面的引用侧面板（“站点”控制台）](#opening-live-copy-overview-references-for-a-blueprint-page)
* [Blueprint页面的属性](#opening-live-copy-overview-properties-of-a-blueprint-page)

### 对Blueprint页面{#references-to-a-blueprint-page}的引用

可以从&#x200B;**站点**&#x200B;控制台的&#x200B;**引用**&#x200B;侧面板打开&#x200B;**Live Copy概述**:

1. 在&#x200B;**站点**&#x200B;控制台中，[导航到您的Blueprint页面并将其选中。](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)
1. 打开&#x200B;**[引用](/help/sites-cloud/authoring/getting-started/basic-handling.md#references)**&#x200B;边栏，然后选择&#x200B;**Live Copy**。

   ![引用边栏中的Live Copy](../assets/live-copy-references.png)

   >[!TIP]
   >
   >您还可以先打开引用，然后选择蓝图。

1. 选择&#x200B;**Live Copy概述**&#x200B;以显示和使用与选定蓝图相关的所有Live Copy的概述。
1. 使用&#x200B;**关闭**&#x200B;退出并返回到&#x200B;**站点**&#x200B;控制台。

### Blueprint页面{#properties-of-a-blueprint-page}的属性

在查看Blueprint页面的属性时，可以打开&#x200B;**Live Copy概述**:

1. 打开相应Blueprint页面的&#x200B;**属性**。
1. 打开&#x200B;**Blueprint**&#x200B;选项卡 — 顶部工具栏中将显示&#x200B;**Live Copy概述**&#x200B;选项：

   ![“Blueprint属性”选项卡](../assets/live-copy-blueprint-tab.png)

1. 选择&#x200B;**Live Copy概述**&#x200B;以显示和使用与当前Blueprint相关的所有Live Copy的概述。

1. 使用&#x200B;**关闭**&#x200B;退出并返回到&#x200B;**站点**&#x200B;控制台。

## 使用Live Copy概述{#using-the-live-copy-overview}

**Live Copy概述**&#x200B;窗口提供和概述与选定页面相关的Live Copy状态。

![“Live Copy概述”窗口](../assets/live-copy-overview.png)

转出取决于在特定转出配置中定义的同步操作。 某些操作取决于对内容的修改。 但是，也有许多操作不依赖于内容的修改，而取决于事件，如页面激活。 此类事件不会修改内容，而是会修改与内容相关的内部属性。

状态字段还取决于在特定转出配置中定义的同步操作，并指示自上次成功转出以来，Blueprint或Live Copy是否存在任何此类操作。 状态字段将仅反映特定转出配置中的操作。 如果尚未对Live Copy执行任何成功转出，则状态将始终显示为最新。

例如，转出配置定义为`targetActivate`。 因此，转出将仅取决于激活事件。 状态字段将仅指示自上次成功转出以来是否已发生任何激活事件。

**Live Copy概述**&#x200B;还可用于对Live Copy执行以下操作：

1. 打开&#x200B;**Live Copy概述**。
1. 选择所需的Blueprint或Live Copy页面，工具栏将更新以显示可用的操作。 可用的[操作](overview.md#terms-used)取决于您是选择[blueprint](#actions-for-a-blueprint-page)还是[ Live Copy](#actions-for-a-live-copy-page)页面。

### Blueprint页面{#actions-for-a-blueprint-page}的操作

选择Blueprint页面时，可执行以下操作：

![Blueprint的Live Copy概述操作](../assets/live-copy-overview-actions-blueprint.png)

* **编辑**  — 打开Blueprint页面进行编辑。
* **[转出](overview.md#rollout-and-synchronize)**  — 执行转出以将更改从源推送到Live Copy。

### Live Copy页面{#actions-for-a-live-copy-page}的操作

选择Live Copy页面时，可以执行以下操作：

![Live Copy的Live Copy概述操作](../assets/live-copy-overview-actions.png)

* **编辑**  — 打开Live Copy页面进行编辑。
* **[关系状态](#relationship-status)**  — 关于状态和继承的视图信息。
* **[同步](overview.md#rollout-and-synchronize)**  — 同步Live Copy以从源将更改拉入Live Copy。
* **[重置](creating-live-copies.md#resetting-a-live-copy-page)**  — 重置Live Copy页面可删除所有继承取消，并将页面返回到与源页面相同的状态。
* **[暂停](overview.md#suspending-and-cancelling-inheritance-and-synchronization)**  — 暂时停用Live Copy与其Blueprint页面之间的Live关系。
* **[恢复](creating-live-copies.md#resuming-inheritance-for-a-page)**  — 恢复允许您恢复已暂停的关系。
* **[分离](overview.md#detaching-a-live-copy)**  — 永久删除Live Copy与其Blueprint页面之间的Live关系。

## 关系状态 {#relationship-status}

**关系状态**&#x200B;控制台有两个选项卡，提供一系列功能。

* [关系状态](#relationship-status-tab)
* [Live Copy](#live-copy-tab)

### 关系状态 {#relationship-status-tab}

此选项卡提供有关Blueprint和Live Copy之间关系状态的详细信息。

![“关系状态”选项卡](../assets/live-copy-relationship-status.png)

### Live Copy {#live-copy-tab}

此选项卡允许您视图和编辑Live Copy配置。

![“Live Copy”选项卡](../assets/live-copy-relationship-status-live-copy.png)
