---
title: Live Copy 概述控制台
description: 学习 Live Copy 概述控制台的基础知识，以快速了解 Live Copy 的状态以便同步内容。
feature: Multi Site Manager
role: Admin
exl-id: 3ef7fbce-10a1-4b21-8486-d3c3706e537c
source-git-commit: 24a4a43cef9a579f9f2992a41c582f4a6c775bf3
workflow-type: ht
source-wordcount: '735'
ht-degree: 100%

---

# Live Copy 概述控制台 {#live-copy-overview-console}

利用 **Live Copy 概述**&#x200B;控制台，您可以：

* 跨站点查看/管理继承。
   * 查看 Blueprint 树和相应的 Live Copy 结构，以及它们的继承状态
   * 更改暂停和恢复等继承状态
   * 查看 Blueprint 和 Live Copy 属性
* 执行转出操作。

## 打开 Live Copy 概述 {#opening-the-live-copy-overview}

您可以从以下位置打开 Live Copy 概述：

* [Blueprint 页面（站点控制台）的引用侧面板](#opening-live-copy-overview-references-for-a-blueprint-page)
* [Blueprint 页面的属性](#opening-live-copy-overview-properties-of-a-blueprint-page)

### 对 Blueprint 页面的引用 {#references-to-a-blueprint-page}

可以从&#x200B;**站点**&#x200B;控制台的&#x200B;**引用**&#x200B;侧面板打开 **Live Copy 概述**：

1. 在&#x200B;**站点**&#x200B;控制台中，[导航到您的 Blueprint 页面并将其选定。](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)
1. 打开&#x200B;**[引用](/help/sites-cloud/authoring/getting-started/basic-handling.md#references)**&#x200B;边栏并选择 **Live Copy**。

   ![引用边栏中的 Live Copy](../assets/live-copy-references.png)

   >[!TIP]
   >
   >您也可以先打开引用，然后选择 Blueprint。

1. 选择 **Live Copy 概述**&#x200B;以显示和使用与所选 Blueprint 相关的所有 Live Copy 的概述。
1. 使用&#x200B;**关闭**&#x200B;以退出，并返回到&#x200B;**站点**&#x200B;控制台。

### Blueprint 页面的属性 {#properties-of-a-blueprint-page}

可以在查看 Blueprint 页面的属性时打开 **Live Copy 概述**：

1. 打开相应的 Blueprint 页面的&#x200B;**属性**。
1. 打开 **Blueprint** 选项卡 – **Live Copy 概述**&#x200B;选项将显示在顶部工具栏中：

   ![Blueprint“属性”选项卡](../assets/live-copy-blueprint-tab.png)

1. 选择 **Live Copy 概述**&#x200B;以显示和使用与当前 Blueprint 相关的所有 Live Copy 的概述。

1. 使用&#x200B;**关闭**&#x200B;以退出，并返回到&#x200B;**站点**&#x200B;控制台。

## 使用 Live Copy 概述 {#using-the-live-copy-overview}

**Live Copy 概述**&#x200B;窗口提供了与所选页面相关的 Live Copy 的概述和状态。

![Live Copy 概述窗口](../assets/live-copy-overview.png)

转出取决于特定转出配置中定义的同步操作。某些操作取决于对内容的修改。但也有许多操作不依赖于对内容的修改，而是依赖于页面激活等事件。此类事件不修改内容，而是修改与内容相关的内部属性。

状态字段还取决于特定转出配置中定义的同步操作，并指示自上次成功转出以来是否对 Blueprint 或 Live Copy 执行了任何此类操作。状态字段将仅反映特定转出配置中的操作。如果从未对 Live Copy 成功执行转出，则状态将始终显示为最新。

例如，转出配置定义为 `targetActivate`。因此，转出将仅取决于激活事件。状态字段将仅指示自上次成功转出以来是否执行了任何激活事件。

**Live Copy 概述**&#x200B;也可用于对 Live Copy 执行操作：

1. 打开 **Live Copy 概述**。
1. 选择所需的 Blueprint 或 Live Copy 页面，工具栏将更新以显示可用操作。可用[操作](overview.md#terms-used)取决于您选择的是 [Blueprint](#actions-for-a-blueprint-page) 还是 [Live Copy](#actions-for-a-live-copy-page) 页面。

### 适用于 Blueprint 页面的操作 {#actions-for-a-blueprint-page}

在选择 Blueprint 页面时，以下操作可用：

![适用于 Blueprint 的 Live Copy 概述操作](../assets/live-copy-overview-actions-blueprint.png)

* **编辑** – 打开 Blueprint 页面以进行编辑。
* **[转出](overview.md#rollout-and-synchronize)** – 执行转出以将更改从源推送到 Live Copy。

### 适用于 Live Copy 页面的操作 {#actions-for-a-live-copy-page}

在选择 Live Copy 页面时，以下操作可用：

![适用于 Live Copy 的 Live Copy 概述操作](../assets/live-copy-overview-actions.png)

* **编辑** – 打开 Live Copy 页面以进行编辑。
* **[关系状态](#relationship-status)** – 查看有关状态和继承的信息。
* **[同步](overview.md#rollout-and-synchronize)** – 同步 Live Copy，将更改从源拉入 Live Copy。
* **[重置](creating-live-copies.md#resetting-a-live-copy-page)** – 重置 Live Copy 页面以删除所有继承取消，并使页面恢复到与源页面相同的状态。
* **[暂停](overview.md#suspending-and-cancelling-inheritance-and-synchronization)** – 暂时停用 Live Copy 与其 Blueprint 页面之间的实时关系。
* **[恢复](creating-live-copies.md#resuming-inheritance-for-a-page)** – 恢复允许您恢复暂停的关系。
* **[分离](overview.md#detaching-a-live-copy)** – 永久删除 Live Copy 与其 Blueprint 页面之间的实时关系。

## 关系状态 {#relationship-status}

**关系状态**&#x200B;控制台具有两个选项卡，提供了一系列功能。

* [关系状态](#relationship-status-tab)
* [Live Copy](#live-copy-tab)

### 关系状态 {#relationship-status-tab}

此选项卡提供有关 Blueprint 和 Live Copy 之间的关系状态的详细信息。

![“关系状态”选项卡](../assets/live-copy-relationship-status.png)

### Live Copy {#live-copy-tab}

此选项卡允许您查看和编辑 Live Copy 配置。

![“Live Copy”选项卡](../assets/live-copy-relationship-status-live-copy.png)
