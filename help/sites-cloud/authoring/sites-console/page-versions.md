---
title: 处理页面版本
description: 了解如何在 AEM 中创建、比较和恢复页面的版本。
exl-id: 33d8e43c-594d-4bba-9631-b2c42a1e910f
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1516'
ht-degree: 97%

---

# 处理页面版本 {#working-with-page-versions}

版本控制可创建页面在特定时间点的“快照”。使用版本控制，您可以执行下列操作：

* 创建页面的版本。
* 恢复一个或多个页面的先前版本以：
   * 还原对页面所做的更改。
   * 恢复已删除的页面。
   * 恢复树（在指定的日期和时间）。
* 预览版本。
* 将页面的当前版本与之前的版本进行比较。
   * 突出显示文本和图像的差异。
* 时间扭曲功能使用页面版本来确定发布环境的状态。

## 创建新版本 {#creating-a-new-version}

您可以通过以下方式创建某个版本的资源：

* [时间线边栏](#creating-a-new-version-timeline)
* [创建](#creating-a-new-version-create-with-a-selected-resource)选项（在选择某资源时）

### 创建新版本 – 时间线 {#creating-a-new-version-timeline}

1. 导航以显示要为其创建版本的页面。
1. 在[选择模式](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources)中选择页面。
1. 打开&#x200B;**时间线**&#x200B;边栏。
1. 选择评论字段旁边的省略号以显示以下选项：

   ![时间线边栏中的版本](/help/sites-cloud/authoring/assets/versions-timeline-rail.png)

1. 选择&#x200B;**保存为版本**。
1. 根据需要输入&#x200B;**标签**&#x200B;和&#x200B;**评论**。

   ![为版本添加标签](/help/sites-cloud/authoring/assets/versions-add-label.png)

1. 通过&#x200B;**创建**&#x200B;确认新版本。

   时间线中的信息会进行更新以指示该新版本。

### 创建新版本 – 通过选定的资源创建 {#creating-a-new-version-create-with-a-selected-resource}

1. 导航以显示要为其创建版本的页面。
1. 在[选择模式](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources)中选择页面。
1. 从工具栏中选择&#x200B;**创建**。
1. 相同的对话框会打开。您可以根据需要输入&#x200B;**标签**&#x200B;和&#x200B;**评论**。
1. 通过&#x200B;**创建**&#x200B;确认新版本。

时间线会打开，并且其信息会更新以指示新版本。

## 恢复版本 {#reinstating-versions}

创建页面的版本后，可通过多种方法恢复以前的版本：

* [时间线](/help/sites-cloud/authoring/basic-handling.md#timeline)边栏中的&#x200B;**恢复到此版本**&#x200B;选项

  恢复所选页面的先前版本。

* 顶部[操作工具栏](/help/sites-cloud/authoring/basic-handling.md#actions-toolbar)中的&#x200B;**恢复**&#x200B;选项

   * **恢复版本**

     恢复当前选定文件夹中指定页面的版本。它还可以包括恢复先前已删除的页面。

   * **恢复树**

     在指定的日期和时间恢复整个树的版本。它还可以包括先前已删除的页面。

>[!NOTE]
>
>恢复页面时，创建的版本会包含在新分支中。
>
>举例说明：
>
>1. 为任意页面创建版本。
>1. 初始的标签和版本节点名称会表示为 1.0、1.1、1.2，以此类推。
>1. 恢复第一个版本；即 1.0。
>1. 再次创建版本。
>1. 此时生成的标签和节点名称会表示为 1.0.0、1.0.1、1.0.2 等。

### 恢复到某个版本 {#revert-to-a-version}

要将选定页面&#x200B;**恢复**&#x200B;到先前版本，请执行以下操作：

1. 导航以显示要还原到之前版本的页面。
1. 在[选择模式](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources)中选择页面。
1. 打开&#x200B;**时间线**&#x200B;列，然后选择&#x200B;**显示全部**&#x200B;或&#x200B;**版本**。所选页面的页面版本会予以列出。
1. 选择要还原到的版本。显示可能的选项：

   ![恢复到此版本](/help/sites-cloud/authoring/assets/versions-revert.png)

1. 选择&#x200B;**还原到此版本**。恢复到所选版本，并在时间线中更新信息。

### 恢复版本 {#restore-version}

此方法可用于恢复当前文件夹中指定页面的版本。它还可以包括恢复先前已删除的页面：

1. 导航到并[选择](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources)所需文件夹。

1. 选择&#x200B;**恢复**，然后从顶部[操作工具栏](/help/sites-cloud/authoring/basic-handling.md#actions-toolbar)中选择&#x200B;**恢复版本**。

   >[!NOTE]
   >
   >如果您：
   >
   >* 选择了一个从未具有任何子页面的页面，
   >* 或者文件夹中的所有页面都没有版本，
   >
   >则显示将为空，因为没有适用的版本。

1. 可用版本会列出：

   ![恢复版本 – 文件夹中所有页面的列表](/help/sites-cloud/authoring/assets/versions-restore-version-01.png)

1. 对于特定页面，使用&#x200B;**恢复到版本**&#x200B;下的下拉选择器来选择该页面的所需版本。

   ![恢复版本 – 选择版本](/help/sites-cloud/authoring/assets/versions-restore-version-02.png)

1. 在主显示中，选择要恢复的页面：

   ![恢复版本 – 选择页面](/help/sites-cloud/authoring/assets/versions-restore-version-03.png)

1. 对于要恢复为当前版本的选定页面的所选版本，选择&#x200B;**恢复**。

>[!NOTE]
>
>所需页面和相关版本的选择顺序可以互换。

### 恢复树 {#restore-tree}

可使用此方法将树恢复到指定的日期和时间的版本。这可以包括之前已删除的页面：

1. 导航到并[选择](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources)所需文件夹。

1. 选择&#x200B;**恢复**，然后从顶部[操作工具栏](/help/sites-cloud/authoring/basic-handling.md#actions-toolbar)中选择&#x200B;**恢复树**。树的最新版本如下所示：

   ![恢复树](/help/sites-cloud/authoring/assets/versions-restore-tree-01.png)

1. 使用&#x200B;**最新版本(日期)**&#x200B;上的日期和时间选择器来选择树的其他版本 – 要恢复的版本。

1. 根据需要设置标志&#x200B;**保留的非版本化页面**：

   * 如果处于活动状态（选中），则任何非版本化页面都会得到维护并且不受恢复的影响。

   * 如果处于非活动状态（未选中），则会删除任何非版本化页面，因为它们在版本化树中不存在。

1. 对于要恢复为&#x200B;*当前*&#x200B;版本的树的所选版本，选择&#x200B;**恢复**。

## 预览版本 {#previewing-a-version}

您可以预览特定版本：

1. 导航以显示要进行比较的页面。
1. 在[选择模式](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources)中选择页面。
1. 打开&#x200B;**时间线**&#x200B;列，然后选择&#x200B;**显示全部**&#x200B;或&#x200B;**版本**。
1. 页面版本会列出。选择要预览的版本：

   ![预览版本](/help/sites-cloud/authoring/assets/versions-revert.png)

1. 选择&#x200B;**预览**。该页面会显示在新选项卡中。

   >[!CAUTION]
   >
   >如果页面发生移动，将无法再对移动前制作的任何版本执行预览。
   >
   >如果您遇到问题，请检查页面的[时间线](/help/sites-cloud/authoring/basic-handling.md#timeline)以查看页面是否已被移动。

## 将页面的某个版本与当前版本进行比较 {#comparing-a-version-with-current-page}

要将页面的之前版本与当前版本进行比较，请执行以下操作：

1. 导航以显示要进行比较的页面。
1. 在[选择模式](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources)中选择页面。
1. 打开&#x200B;**时间线**&#x200B;列，然后选择&#x200B;**显示全部**&#x200B;或&#x200B;**版本**。
1. 页面版本会列出。选择要进行比较的版本：

   ![比较版本](/help/sites-cloud/authoring/assets/versions-revert.png)

1. 选择&#x200B;**与当前比较**。此时会打开[页面差异](/help/sites-cloud/authoring/sites-console/page-diff.md)，并显示存在的差异。

## 时间扭曲 {#timewarp}

时间扭曲是一项功能，旨在模拟过去特定时间某个页面的&#x200B;*已发布*&#x200B;状态。

>[!TIP]
>
>[时间扭曲也可以与启动项一起使用来预览未来情况](/help/sites-cloud/authoring/launches/preview.md)。

由于内容创建是一个持续的协作过程，因此时间扭曲旨在允许作者随时间跟踪已发布的网站，以了解内容的更改情况。此功能使用页面版本来确定发布环境的状态。

要使用此功能：

* 系统会查找在选定时间处于活动状态的页面版本。
* 这表示显示的版本是在“时间扭曲”中选择的时间点&#x200B;*之前*&#x200B;创建/激活的。
* 当浏览到已经删除的页面时，也会呈现相应的页面版本 - 只要该页面的旧版本仍然在存储库中即可。
* 如果没有找到发布的版本，则时间扭曲会还原到该页面在创作环境中的当前状态（这是为了防止出现错误/404 页面，此页面将阻止您进行浏览）。

### 使用时间扭曲 {#using-timewarp}

时间扭曲是页面编辑器的一种[模式](/help/sites-cloud/authoring/page-editor/introduction.md#page-modes)。要启动此模式，只需像切换任何其他模式一样切换此模式即可。

1. 启动要从中启动Timewarp的页面的编辑器，然后在模式选择中选择&#x200B;**Timewarp**。

   ![时间扭曲模式](/help/sites-cloud/authoring/assets/versions-timewarp-mode.png)

1. 在对话框中设置目标日期和时间，然后单击&#x200B;**设置日期**。如果不选择时间，则会默认使用当前的时间。

   ![时间扭曲目标日期](/help/sites-cloud/authoring/assets/versions-timewarp-target.png)

1. 将根据设置的日期显示该页面。时间扭曲模式通过窗口顶部的蓝色状态栏来指示。使用该状态栏中的链接可选择新的目标日期，或退出时间扭曲模式。

   ![在时间扭曲模式下](/help/sites-cloud/authoring/assets/versions-timewarp.png)

### 时间扭曲限制 {#timewarp-limitations}

时间扭曲会尽量在选定的时刻重现页面。但是，由于在 AEM 中连续创作内容的过程非常复杂，并非总能实现这种复制。在使用时间扭曲时，应考虑这些限制。

* **时间扭曲基于已发布的页面工作** – 仅当您之前已发布页面时，时间扭曲才会完全正常工作。如果没有，时间扭曲会在创作环境显示当前页面。
* **时间扭曲使用页面版本** – 当您浏览到的页面已从存储库删除时，如果该页面的旧版本仍然位于存储库中，则该页面会正常呈现。
* **已删除的版本会影响时间扭曲** – 如果从存储库从删除了版本，那么时间扭曲无法显示正确的视图。
* **时间扭曲为只读** – 您无法编辑页面的旧版本。旧版本仅供查看。如果要恢复旧版本，则必须使用[恢复](#revert-to-a-version)功能手动恢复。
* **时间扭曲基于页面内容** – 如果用于呈现网站的元素发生了更改（如代码、css 和资源），则视图会与最初的视图不同。存储库中没有对这些项目进行版本控制。

>[!CAUTION]
>
>时间扭曲旨在作为一种可帮助作者理解和创建其内容的工具，而不是用作审查日志或用于法律目的。
