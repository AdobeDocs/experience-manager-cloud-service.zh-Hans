---
title: 提升启动项
description: 您必須提升啟動頁面，才能在發佈前將內容移回來源（生產環境）。
exl-id: 5f5ed17c-43db-4ef6-ab79-c491326fa01c
source-git-commit: 47910a27118a11a8add6cbcba6a614c6314ffe2a
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 42%

---

# 提升启动项 {#promoting-launches}

您必須提升啟動頁面，才能在發佈前將內容移回來源（生產環境）。 提升啟動頁面時，來源頁面的對應頁面會取代為提升頁面的內容。 提升啟動頁面時，有以下選項可供使用：

* 僅提升目前頁面還是整個啟動。
* 是否要升級目前頁面的子頁面。
* 是提升完整啟動項，還是僅提升已變更的頁面。
* 升級後是否要刪除啟動。

>[!NOTE]
>
>將啟動頁面升級至目標之後(**生產**)，則您可啟動 **生產** 以圖元形式顯示頁面（以加快處理速度）。 將頁面新增至Workflow封裝，並當做啟動頁面封裝的Workflow的裝載。 在提升啟動項之前，您需要建立工作流程套件。 另請參閱 [使用AEM工作流程處理提升頁面](#processing-promoted-pages-using-aem-workflow).

>[!CAUTION]
>
>無法同時提升單一啟動。 这意味着，对同一个启动项同时执行两次提升操作可能会导致出现以下错误：`Launch could not be promoted`（同时还会导致日志中出现冲突错误）。

>[!CAUTION]
>
>提升啟動時 *已修改* 頁面，會同時考慮來源分支和啟動分支中的修改。

## 提升啟動頁面 {#promoting-launch-pages}

>[!NOTE]
>
>當只有一個啟動層級時，這會涵蓋提升啟動頁面的手動動作。 请参阅：
>
>* [提升巢狀啟動](#promoting-a-nested-launch) 當結構中有多個啟動項時。
>* [啟動 — 事件順序](/help/sites-cloud/authoring/launches/overview.md#launches-the-order-of-events) 以取得有關自動促銷和發佈的更多詳細資訊。
>


您可以透過以下任一項提升啟動： **網站** 主控台或 **啟動** 主控台：

1. 打开：
   * **站点**&#x200B;控制台（导航源页面时）：
      1. 打开[引用边栏](/help/sites-cloud/authoring/fundamentals/environment-tools.md#references)，然后使用[选择模式](/help/sites-cloud/authoring/getting-started/basic-handling.md)选择所需的源页面（或者先进行选择，然后再打开引用边栏，顺序不重要）。此时将显示所有引用。
      1. 选择&#x200B;**启动项**（例如“启动项 (1)”），可显示特定启动项的列表。
      1. 選取特定啟動項以顯示可用的動作。
      1. 选择&#x200B;**提升启动项**&#x200B;以打开向导。
   * **站点**&#x200B;控制台（导航启动页面时）：
      1. 使用[选择模式](/help/sites-cloud/authoring/getting-started/basic-handling.md)选择所需的启动页面。
      1. **提升**&#x200B;操作将在工具栏中可用。
   * **启动项**&#x200B;控制台：
      1. 選取您的啟動項（點選/按一下縮圖）。
      1. 選取 **提升**.
1. 在第一個步驟中，您可以指定：
   * **目标**
      * **提升后删除发布内容**
   * **范围**
      * **提升整个发布内容**
      * **提升已修改的页面**
      * **提升批准的页面** – 取决于启动项批准工作流
      * **提升当前页面**
      * **提升当前页面和子页面**

      例如，当选择仅提升已修改的页面时：

      ![启动项提升](/help/sites-cloud/authoring/assets/launches-promote.png)

      >[!NOTE]
      >
      >這涵蓋單一啟動（如果您有巢狀啟動），請參閱 [提升巢狀啟動](#promoting-a-nested-launch).
1. 選取 **下一個** 以繼續進行。
1. 您可以查看要提升的页面，具体页面取决于您选择的页面范围：

   ![查看提升](/help/sites-cloud/authoring/assets/launches-promote-review.png)

1. 選取 **提升**.

## 編輯時提升啟動頁面 {#promoting-launch-pages-when-editing}

編輯啟動頁面時， **提升啟動** 動作也可從 **頁面資訊**. 这将打开相应向导来收集所需的信息。

![从站点信息提升启动项](/help/sites-cloud/authoring/assets/launches-promote-page-info.png)

>[!NOTE]
>
>這適用於單一和 [巢狀啟動](#promoting-a-nested-launch).

## 提升巢狀啟動 {#promoting-a-nested-launch}

建立巢狀啟動後，您可以將其升級回任何來源，包括根來源（生產）。

![嵌套启动项](/help/sites-cloud/authoring/assets/launches-promoting-nested.png)

1. 与创建嵌套启动项一样，在&#x200B;**启动项**&#x200B;控制台或&#x200B;**引用**&#x200B;边栏中导航到所需的启动项并将其选中。
1. 选择&#x200B;**提升启动项**&#x200B;以打开向导。
1. 输入所需的详细信息：
   * **目标**
      * **提升目标** – 您可以提升到任意源。
      * **提升后删除启动项** – 提升后，将删除所选启动项以及嵌套在其中的所有启动项。
   * **范围** – 在此处，您可以选择是提升整个启动项，还是仅提升已实际编辑的页面。如果是後者，您就可以選取包含/排除子頁面。 預設設定為僅提升目前頁面的頁面變更：
      * **提升整个发布内容**
      * **提升已修改的页面**
      * **提升批准的页面** – 取决于启动项批准工作流
      * **提升当前页面**
      * **提升当前页面和子页面**

   ![提升启动设置](/help/sites-cloud/authoring/assets/launches-promote-settings.png)

1. 选择&#x200B;**下一步**。
1. 在选择&#x200B;**提升**&#x200B;之前查看提升详细信息：

   ![查看提升设置](/help/sites-cloud/authoring/assets/launches-promote-review-2.png)

   >[!NOTE]
   >
   >列出的頁面取決於 **範圍** 已定義，且可能包括實際編輯的頁面。

1. 您的變更將會提升並反映在 **啟動** 主控台：

   ![在启动项控制台中](/help/sites-cloud/authoring/assets/launches-console.png)

## 使用 AEM 工作流处理提升的页面 {#processing-promoted-pages-using-aem-workflow}

使用工作流程模型來大量處理提升的「啟動」頁面：

1. 建立工作流程封裝。
1. 作者提升Launch頁面時，會將頁面儲存在Workflow套件中。
1. 使用封裝作為裝載啟動工作流程模型。

要在提升页面时自动启动工作流，请为包节点配置工作流启动器。<!--To start a workflow automatically when pages are promoted, [configure a workflow launcher](/help/sites-administering/workflows-starting.md#workflows-launchers) for the package node.-->

例如，您可以在作者提升啟動頁面時自動產生頁面啟用請求。 設定工作流程啟動器，以便在修改封裝節點時啟動「請求啟用」工作流程。

![提升工作流](/help/sites-cloud/authoring/assets/launches-create-workflow.png)
