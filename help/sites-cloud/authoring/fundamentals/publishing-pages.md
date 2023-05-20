---
title: 发布页面
description: 如何使用 AEM 发布和取消发布页面
exl-id: 89f2363c-7922-4ca5-92cb-cbee6a393ee3
source-git-commit: 47910a27118a11a8add6cbcba6a614c6314ffe2a
workflow-type: tm+mt
source-wordcount: '1812'
ht-degree: 80%

---

# 发布页面 {#publishing-pages}

在作者環境中建立並檢閱您的內容後，目標是 [使其可在您的公開網站上使用](/help/sites-cloud/authoring/getting-started/concepts.md) （您的發佈環境）。

這稱為發佈頁面。 當您想要從發佈環境中移除頁面時，會稱為取消發佈。 發佈和取消發佈頁面時，作者環境仍會提供頁面以供進一步變更，直到您刪除為止。

您可以立即发布/取消发布页面，或者在某个预定义的未来日期/时间发布/取消发布页面。

>[!NOTE]
>
>发布体验片段的过程基本上与发布页面的过程相同，只是从体验片段控制台或编辑器中发布。

## 术语 {#terminology}

在使用 Adobe Experience Manager (AEM) as a Cloud Service 时，您可能会遇到与发布相关的不同术语。

* **发布/取消发布**
   * 这些是在发布环境中公开提供（或不公开提供）您的内容的主要操作术语。
   * 这些是 AEM 文档中使用的术语。
* **激活／取消激活**
   * 这两个术语与发布/取消发布同义。
   * 这些术语在 AEM 的早期版本中使用。
* **复制**
   * 这些是技术术语，用于描述发布页面时数据（例如，页面内容、文件、代码、用户评论）从一个环境移动到另一个环境。
   * 这些术语主要由开发人员使用。

## 发布页面 {#publishing-pages-1}

根據您的位置，您可以發佈：

* [从页面编辑器中](#publishing-from-the-editor)
* [从站点控制台中](#publishing-from-the-console)

>[!NOTE]
>
>如果您沒有發佈特定頁面所需的許可權：
>
>* 系統會觸發工作流程，將您要發佈的請求通知適當人員。
>* 您的开发团队可能已自定义此工作流。
>* 将显示一条简短的消息，通知您工作流已经触发。


>[!NOTE]
>
> 有关其他可能性，请参阅[页面属性的“基本”选项卡](/help/sites-cloud/authoring/fundamentals/page-properties.md#basic)中的&#x200B;**开启时间**&#x200B;和&#x200B;**关闭时间**。

### 从编辑器中发布 {#publishing-from-the-editor}

如果您在编辑页面，则可以直接从编辑器中发布该页面。

1. 选择&#x200B;**页面信息**&#x200B;图标以打开相应的菜单，然后选择&#x200B;**发布页面**&#x200B;选项。

   ![通过页面选项发布页面](/help/sites-cloud/authoring/assets/publishing-page-options.png)

1. 根据页面是否包含需要发布的引用：

   * 如果不包含要发布的引用，则将直接发布页面。
   * 如果页面包含需要发布的引用，则将在&#x200B;**发布**&#x200B;向导中列出该内容，从该向导中可以：
      * 指定要与页面一起发布的资产/标记/等，然后使用&#x200B;**发布**&#x200B;完成该过程。
      * 使用&#x200B;**取消**&#x200B;中止操作。

   ![使用页面发布引用](/help/sites-cloud/authoring/assets/publishing-references.png)

1. 选择&#x200B;**发布**&#x200B;会将页面复制到发布环境。在页面编辑器中，将显示一个确认发布操作的信息横幅。

   ![发布状态信息横幅](/help/sites-cloud/authoring/assets/publishing-info.png)

   当在控制台中查看同一页面时，将显示更新的发布状态。

   ![站点控制台列视图中的页面发布状态](/help/sites-cloud/authoring/assets/publishing-status-console-column.png)

>[!NOTE]
>
>从编辑器中发布是一种简单的发布方式，即只会发布选定的一个或多个页面，而不会发布任何子页面。

>[!NOTE]
>
>无法发布编辑器中按[别名](/help/sites-cloud/authoring/fundamentals/page-properties.md#advanced)处理的页面。编辑器中的发布选项仅适用于通过其实际路径访问的页面。

### 从控制台中发布 {#publishing-from-the-console}

在網站主控台中，有兩個發佈選項：

* [快速发布](#quick-publish)
* [管理发布](#manage-publication)

#### 快速发布 {#quick-publish}

**快速发布**&#x200B;适用于一些简单的情况，可立即发布选定的页面，而无需进行任何进一步的交互。因此，任何未發佈的參考也會自動發佈。

若要使用「快速發佈」功能發佈頁面：

1. 在站点控制台中选择一个或多个页面，然后单击&#x200B;**快速发布**&#x200B;按钮。

   ![选择要发布的页面](/help/sites-cloud/authoring/assets/publishing-select-pages.png)

1. 在“快速发布”对话框中，单击&#x200B;**发布**&#x200B;以确认发布，或单击&#x200B;**取消**&#x200B;以取消发布。请记住，任何未发布的引用也将被自动发布。

   ![快速发布确认](/help/sites-cloud/authoring/assets/publishing-quick-publish.png)

1. 發佈頁面時，畫面會顯示確認發佈的警報。

>[!NOTE]
>
>「快速發佈」是淺層發佈，即只會發佈選取的頁面/頁面，而不會發佈任何子頁面。

#### 管理发布 {#manage-publication}

与&#x200B;**快速发布**&#x200B;相比，**管理发布**&#x200B;提供了更多选项，允许包含子页面、自定义引用和启动任何适用的工作流，并且还提供了在以后的日期发布的选项。

要使用“管理发布”发布或取消发布页面，请执行以下操作：

1. 在站点控制台中选择一个或多个页面，然后单击&#x200B;**管理发布**&#x200B;按钮。

   ![选择要发布的页面](/help/sites-cloud/authoring/assets/publishing-select-pages.png)

1. 此时会启动&#x200B;**管理发布**&#x200B;向导。第一个步骤&#x200B;**选项**&#x200B;允许您：

   * **操作**

      选择发布或取消发布选定的页面。

   * **计划**

      選擇現在或稍後採取該動作。

      稍後發佈會啟動工作流程，以在指定時間發佈選取的一個或多個頁面。 反之，稍後取消發佈會啟動工作流程，以在特定時間取消發佈所選的一或多個頁面。

      >[!NOTE]
      >
      >如果您要稍后撤消发布/取消发布页面，请转到[“工作流”控制台](/help/sites-cloud/administering/workflows-administering.md#suspending-resuming-and-terminating-a-workflow-instance)以终止相应的工作流。
   ![管理发布选项](/help/sites-cloud/authoring/assets/publishing-manage-publication-options.png)

1. 单击&#x200B;**下一步**&#x200B;以继续。

1. 在“管理发布”向导的下一个步骤&#x200B;**范围**&#x200B;中，您可以定义发布/取消发布的范围，如包括子页面和/或包括引用。

   ![管理发布范围](/help/sites-cloud/authoring/assets/publishing-manage-publication-scope.png)

   **添加内容**

   如果您因一时疏忽而忘记在启动“管理发布”向导之前选择某个页面，则可以使用&#x200B;**添加内容**&#x200B;按钮将其他页面添加到要发布的页面列表中。

   选择&#x200B;**添加内容**&#x200B;按钮会启动[路径浏览器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#path-browser)以供选择内容。

   选择所需的页面，然后单击&#x200B;**选择**&#x200B;以将该内容添加到向导，或单击&#x200B;**取消**&#x200B;以取消所做的选择并返回到向导。

   **删除选择**

   返回向导，您可以在列表中选择一个项目以将其从选定内容中删除。

   ![管理发布选择页面](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

   **已发布引用**

   您可以通过选择页面，然后单击&#x200B;**已发布引用**&#x200B;按钮，来查看和修改该页面要发布或取消发布的引用。

   ![管理发布选项](/help/sites-cloud/authoring/assets/publishing-manage-publication-references.png)

   **已发布引用**&#x200B;对话框将显示选定内容的引用。默认情况下，这些引用全部处于选中状态并将进行发布/取消发布，但您可以取消选择它们，以便将它们排除在操作之外。

   单击&#x200B;**完成**&#x200B;以保存您所做的更改，或单击&#x200B;**取消**&#x200B;以取消所做的选择并返回到向导。

   返回到向导后，**引用**&#x200B;列将进行相应的更新，以反映您选择的要发布或取消发布的引用。

   ![管理发布选择页面](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

   **包括子项**

   >[!NOTE]
   >
   >请参阅[发布和取消发布树](#publishing-and-unpublishing-a-tree)

   单击&#x200B;**包括子项**&#x200B;会打开一个对话框，它允许您：

   * **包括子项**
   * **仅包括下级子项**
   * **仅包括已修改的页面**
   * **仅包括已发布的页面**

   激活所需选项，并单击&#x200B;**确定**&#x200B;以进行确认，根据选择选项将子页面添加到要发布或取消发布的页面列表中。单击&#x200B;**取消**&#x200B;可取消所做的选择并返回到向导。

   ![管理发布（包括子项）](/help/sites-cloud/authoring/assets/publishing-include-children.png)

1. 单击&#x200B;**发布**&#x200B;以完成。

   返回到站点控制台后，将显示一条确认发布的通知消息。

1. 如果发布的页面与工作流相关联，则这些工作流可能会显示在发布向导的最后一个步骤&#x200B;**工作流**&#x200B;中。

   ![管理发布选择页面](/help/sites-cloud/authoring/assets/publishing-manage-publication-workflow.png)

   >[!NOTE]
   >
   >将根据用户可能拥有也可能没有的权限显示&#x200B;**工作流**&#x200B;步骤。有关详细信息，请参阅此页面前面部分与发布权限有关的注释以及管理工作流的访问权限和[将工作流应用到页面](/help/sites-cloud/authoring/workflows/applying.md)。

   資源會依觸發的工作流程及每個指定選項分組，以便：

   * 定義工作流程的標題。
   * 保留工作流包，前提是工作流具有多资源支持。
   * 在选择保留工作流包的选项时，定义工作流包的标题。

1. 单击&#x200B;**发布**&#x200B;或&#x200B;**稍后发布**&#x200B;以完成发布。

## 取消发布页面 {#unpublishing-pages}

取消发布页面会将其从您的发布或[预览](/help/sites-cloud/authoring/fundamentals/previewing-content.md)环境中移除，因此不再将其提供给您的读者。

以类似于发布 [ 的 ](#publishing-pages) 方式，可以从所需目标取消发布一个或多个页面：

* [从页面编辑器中](#unpublishing-from-the-editor)
* [从站点控制台中](#unpublishing-from-the-console)

### 從編輯器中取消發佈 {#unpublishing-from-the-editor}

編輯頁面時，如果您要取消發佈該頁面，請選取 **取消發佈頁面** 在 **頁面資訊** 功能表，視需要而定 [發佈頁面](#publishing-from-the-editor).

>[!NOTE]
>
>无法取消发布编辑器中按[别名](/help/sites-cloud/authoring/fundamentals/page-properties.md#advanced)处理的页面。编辑器中的发布选项仅适用于通过其实际路径访问的页面。

### 從主控台取消發佈 {#unpublishing-from-the-console}

正如[使用“管理发布”选项发布页面](#manage-publication)一样，也可以使用它来取消发布页面。

1. 在站点控制台中选择一个或多个页面，然后单击&#x200B;**管理发布**&#x200B;按钮。
1. 此时会启动&#x200B;**管理发布**&#x200B;向导。在第一个步骤&#x200B;**选项**&#x200B;中，选择&#x200B;**取消发布**，而不是默认选项&#x200B;**发布**。

   ![取消发布 – 选项](/help/sites-cloud/authoring/assets/publishing-unpublish.png)

   正如稍后发布会启动一个工作流，以在指定时间发布此版本页面一样，稍后取消激活也会启动一个工作流，以在指定时间取消发布选定的一个或多个页面。

   >[!NOTE]
   >
   >如果您要稍后撤消发布/取消发布页面，请转到[“工作流”控制台](/help/sites-cloud/administering/workflows-administering.md#suspending-resuming-and-terminating-a-workflow-instance)以终止相应的工作流。

   >[!NOTE]
   >如果您有一个[预览](/help/sites-cloud/authoring/fundamentals/previewing-content.md)环境，您可以在管理发布期间选择&#x200B;**目标**。

1. 要完成取消发布，请按照与[发布页面](#manage-publication)类似的过程继续完成向导。

   ![取消发布 – 范围](/help/sites-cloud/authoring/assets/publishing-unpublish-scope.png)

## 发布和取消发布树 {#publishing-and-unpublishing-a-tree}

當您輸入或更新了大量內容頁面時 — 所有內容頁面都位於同一個根頁面下 — 可以更輕鬆地在一次動作中發佈整個樹狀結構。

您可以使用 [管理發布](#manage-publication) 選項（位於網站主控台上）來執行此動作。

1. 在網站主控台中，選取您要發佈或取消發佈之樹狀結構的根頁面，然後選取 **管理發布**.
1. 此时会启动&#x200B;**管理发布**&#x200B;向导。選擇發佈或取消發佈的時間及應發生的時間，然後選取 **下一個** 以繼續。
1. 在 **範圍** 步驟，選取根頁面並選取 **包含子項**.

   ![管理发布选择页面](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

1. 在&#x200B;**包括子项**&#x200B;对话框中：

   * 选择&#x200B;**包括子项**
   * 取消选择&#x200B;**仅包括下级子项**
   * 取消选择&#x200B;**仅包括已发布的页面**
   * 根据需要配置&#x200B;**仅包括已修改的页面**

   这些选项默认处于选中状态，因此您必须记得配置它们。单击&#x200B;**确定**&#x200B;以确认选择，将内容添加到发布/取消发布。

   ![包括树发布的子项](/help/sites-cloud/authoring/assets/publishing-include-children-tree.png)

1. 在&#x200B;**管理发布**&#x200B;向导中，您可以通过添加其他页面或删除所选页面来进一步自定义选择。

   请记住，您还可以通过&#x200B;**已发布引用**&#x200B;选项查看要发布的引用。

1. [照常继续执行“管理发布”向导](#manage-publication)，以完成发布或取消发布树的过程。

## 确定发布状态 {#determining-publication-status}

您可以确定页面的发布状态：

* 在[站点控制台上的资源概述信息](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)中

   ![信息卡视图中的发布状态](/help/sites-cloud/authoring/assets/publishing-status-console-card.png)

   站点控制台的[信息卡](/help/sites-cloud/authoring/getting-started/basic-handling.md#card-view)、[列](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view)和[列表](/help/sites-cloud/authoring/getting-started/basic-handling.md#list-view)视图中将显示发布状态。

* 在[时间线](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)中

   ![时间线视图中的发布状态](/help/sites-cloud/authoring/assets/publishing-status-timeline.png)

* 在[“页面信息”菜单](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information)中（编辑页面时）

   ![“页面信息”菜单中的发布状态](/help/sites-cloud/authoring/assets/publishing-status-page-information.png)
