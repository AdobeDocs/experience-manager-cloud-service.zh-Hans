---
title: 发布页面
description: 了解如何使用 AEM 中的各种机制发布和取消发布页面。
exl-id: 89f2363c-7922-4ca5-92cb-cbee6a393ee3
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '1927'
ht-degree: 87%

---

# 发布页面 {#publishing-pages}

在创作环境中创建并审核内容后，接下来的目标就是[让内容在您的公共网站（发布环境）中可供使用](/help/sites-cloud/authoring/getting-started/concepts.md)。

这称为“发布页面”。当您要从发布环境中删除页面时，此过程称为“取消发布”。在发布和取消发布时，页面会保留在创作环境中以供进一步更改，直到将其删除为止。

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

根据您所在的位置，可以通过下列方式发布：

* [从页面编辑器中](#publishing-from-the-editor)
* [从 Sites 控制台中](#publishing-from-the-console)

>[!NOTE]
>
>如果您没有必要的权限来发布特定页面：
>
>* 会触发一个工作流程，向相应的人员通知您的发布请求。
>* 您的开发团队可能已自定义此工作流程。
>* 短暂显示一条简短的消息，通知您工作流程已经触发。

>[!NOTE]
>
>如果要保留页面顺序，则必须使用[管理发布](#manage-publication)在单个操作中将父页面与任何子页面一起发布。
>
>不保证页面顺序：
>* 只选择要发布的子页面（因为订单信息保存在父页面上）
>* 如果父页面和子页面是在单独的操作中发布的

>[!NOTE]
>
> 有关其他可能性，请参阅[页面属性的“基本”选项卡](/help/sites-cloud/authoring/fundamentals/page-properties.md#basic)中的&#x200B;**开启时间**&#x200B;和&#x200B;**关闭时间**。

### 从编辑器中发布 {#publishing-from-the-editor}

如果您在编辑页面，则可以直接从编辑器中发布该页面。

1. 选择&#x200B;**页面信息**&#x200B;图标以打开相应的菜单，然后选择&#x200B;**发布页面**&#x200B;选项。

   ![通过页面选项发布页面](/help/sites-cloud/authoring/assets/publishing-page-options.png)

1. 根据页面是否包含需要发布的引用：

   * 如果不包含要发布的引用，则会直接发布页面。
   * 如果页面包含需要发布的引用，则会在&#x200B;**发布**&#x200B;向导中列出该内容，从该向导中可以：
      * 指定要与页面一起发布的资产或标记等，然后使用&#x200B;**Publish**&#x200B;完成该过程。
      * 使用&#x200B;**取消**&#x200B;中止操作。

   ![使用页面发布引用](/help/sites-cloud/authoring/assets/publishing-references.png)

1. 选择&#x200B;**发布**&#x200B;会将页面复制到发布环境。在页面编辑器中，会显示一个确认发布操作的信息横幅。

   ![发布状态信息横幅](/help/sites-cloud/authoring/assets/publishing-info.png)

   当在控制台中查看同一页面时，将显示更新的发布状态。

   ![Sites 控制台列视图中的页面发布状态](/help/sites-cloud/authoring/assets/publishing-status-console-column.png)

>[!NOTE]
>
>从编辑器中发布是一种简单的发布方式，即只会发布选定的一个或多个页面，而不会发布任何子页面。

>[!NOTE]
>
>无法发布编辑器中按[别名](/help/sites-cloud/authoring/fundamentals/page-properties.md#advanced)处理的页面。编辑器中的发布选项仅适用于通过其实际路径访问的页面。

### 从控制台中发布 {#publishing-from-the-console}

Sites 控制台中有两个用于发布的选项：

* [快速发布](#quick-publish)
* [管理发布](#manage-publication)

#### 快速发布 {#quick-publish}

**快速发布**&#x200B;适用于一些简单的情况，可立即发布选定的页面，而无需进行任何进一步的交互。正因为这一点，任何未发布的引用也将被自动发布。

要使用“快速发布”发布页面，请执行以下操作：

1. 在站点控制台中选择一个或多个页面，然后单击&#x200B;**快速Publish**&#x200B;按钮。

   ![选择要发布的页面](/help/sites-cloud/authoring/assets/publishing-select-pages.png)

1. 在“快速发布”对话框中，单击&#x200B;**发布**&#x200B;以确认发布，或单击&#x200B;**取消**&#x200B;以取消发布。请记住，任何未发布的引用也将被自动发布。

   ![快速发布确认](/help/sites-cloud/authoring/assets/publishing-quick-publish.png)

1. 在发布页面时，将显示确认发布的警报。

>[!NOTE]
>
>“快速发布”是一种简单的发布方式，即只会发布选定的一个或多个页面，而不会发布任何子页面。

#### 管理发布 {#manage-publication}

与&#x200B;**快速发布**&#x200B;相比，**管理发布**&#x200B;提供了更多选项，允许包含子页面、自定义引用和启动任何适用的工作流程，并且还提供了在以后的日期发布的选项。

>[!NOTE]
>
>如果要保留页面顺序，则必须使用&#x200B;**管理发布**&#x200B;在单个操作中将父页面与任何子页面一起发布。
>
>不保证页面顺序：
>* 只选择要发布的子页面（因为订单信息保存在父页面上）
>* 如果父页面和子页面是在单独的操作中发布的

要使用“管理发布”发布或取消发布页面，请执行以下操作：

1. 在站点控制台中选择一个或多个页面，然后单击&#x200B;**管理发布**&#x200B;按钮。

   ![选择要发布的页面](/help/sites-cloud/authoring/assets/publishing-select-pages.png)

1. 此时会启动&#x200B;**管理发布**&#x200B;向导。第一步，**选项**，让你：

   * **操作**

     选择发布或取消发布选定的页面。

   * **计划**

     选择立即还是在以后的日期执行该操作。

     稍后发布会启动一个在指定时间发布选定的一个或多个页面的工作流程。相反，稍后取消发布则会启动一个在指定时间取消发布选定的一个或多个页面的工作流程。

     >[!NOTE]
     >
     >如果您要稍后撤消发布/取消发布页面，请转到[“工作流程”控制台](/help/sites-cloud/administering/workflows-administering.md#suspending-resuming-and-terminating-a-workflow-instance)以终止相应的工作流程。

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

   **已发布引用**&#x200B;对话框将显示选定内容的引用。默认情况下，这些引用全部处于选中状态并会进行发布/取消发布，但您可以取消选择它们，以便将它们排除在操作之外。

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

   返回到 Sites 控制台后，将显示一条确认发布的通知消息。

1. 如果发布的页面与工作流程相关联，则这些工作流程可能会显示在发布向导的最后一个步骤&#x200B;**工作流程**&#x200B;中。

   ![管理发布选择页面](/help/sites-cloud/authoring/assets/publishing-manage-publication-workflow.png)

   >[!NOTE]
   >
   >根据用户可能拥有或可能没有的权限显示&#x200B;**工作流程**&#x200B;步骤。有关详细信息，请参阅此页面前面部分与发布权限有关的注释以及管理工作流程的访问权限和[将工作流程应用到页面](/help/sites-cloud/authoring/workflows/applying.md)。

   资源将按触发的工作流程分组，并且每组都提供了用于执行以下操作的选项：

   * 定义工作流程的标题。
   * 保留工作流程包，前提是工作流程具有多资源支持。
   * 在选择保留工作流程包的选项时，定义工作流程包的标题。

1. 单击&#x200B;**发布**&#x200B;或&#x200B;**稍后发布**&#x200B;以完成发布。

## 取消发布页面 {#unpublishing-pages}

取消发布页面会将其从您的发布或[预览](/help/sites-cloud/authoring/fundamentals/previewing-content.md)环境中移除，因此不再将其提供给您的读者。

以类似于发布 [ 的 ](#publishing-pages) 方式，可以从所需目标取消发布一个或多个页面：

* [从页面编辑器中](#unpublishing-from-the-editor)
* [从 Sites 控制台中](#unpublishing-from-the-console)

### 从编辑器中取消发布 {#unpublishing-from-the-editor}

在编辑页面时，如果要取消发布该页面，请在&#x200B;**页面信息**&#x200B;菜单中选择&#x200B;**取消发布页面**，操作方式与[发布页面](#publishing-from-the-editor)类似。

>[!NOTE]
>
>无法取消发布编辑器中按[别名](/help/sites-cloud/authoring/fundamentals/page-properties.md#advanced)处理的页面。编辑器中的发布选项仅适用于通过其实际路径访问的页面。

### 从控制台中取消发布 {#unpublishing-from-the-console}

正如[使用“管理发布”选项发布页面](#manage-publication)一样，也可以使用它来取消发布页面。

1. 在站点控制台中选择一个或多个页面，然后单击&#x200B;**管理发布**&#x200B;按钮。
1. 此时会启动&#x200B;**管理发布**&#x200B;向导。在第一个步骤&#x200B;**选项**&#x200B;中，选择&#x200B;**取消发布**，而不是默认选项&#x200B;**发布**。

   ![取消发布 – 选项](/help/sites-cloud/authoring/assets/publishing-unpublish.png)

   正如稍后发布会启动一个工作流程，以在指定时间发布此版本页面一样，稍后取消激活也会启动一个工作流程，以在指定时间取消发布选定的一个或多个页面。

   >[!NOTE]
   >
   >如果您要稍后撤消发布/取消发布页面，请转到[“工作流程”控制台](/help/sites-cloud/administering/workflows-administering.md#suspending-resuming-and-terminating-a-workflow-instance)以终止相应的工作流程。

   >[!NOTE]
   >如果您有一个[预览](/help/sites-cloud/authoring/fundamentals/previewing-content.md)环境，您可以在管理发布期间选择&#x200B;**目标**。

1. 要完成取消发布，请按照与[发布页面](#manage-publication)类似的过程继续完成向导。

   ![取消发布 – 范围](/help/sites-cloud/authoring/assets/publishing-unpublish-scope.png)

## 发布和取消发布树 {#publishing-and-unpublishing-a-tree}

如果输入或更新了大量内容页面（所有内容页面都位于同一根页面下），则可以更轻松地通过一个操作来发布整个树。

您可以使用 Sites 控制台上的[管理发布](#manage-publication)选项来完成此操作。

1. 在站点控制台中，选择要发布或取消发布的树的根页面，然后选择&#x200B;**管理发布**。
1. 此时会启动&#x200B;**管理发布**&#x200B;向导。选择发布或取消发布以及应在何时开始，然后选择&#x200B;**下一步**&#x200B;以继续。
1. 在&#x200B;**范围**&#x200B;步骤中，选择根页面，然后选择&#x200B;**包括子项**。

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

* 在[ Sites 控制台上的资源概述信息](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)中

  ![信息卡视图中的发布状态](/help/sites-cloud/authoring/assets/publishing-status-console-card.png)

  Sites 控制台的[信息卡](/help/sites-cloud/authoring/getting-started/basic-handling.md#card-view)、[列](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view)和[列表](/help/sites-cloud/authoring/getting-started/basic-handling.md#list-view)视图中将显示发布状态。

* 在[时间线](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)中

  ![时间线视图中的发布状态](/help/sites-cloud/authoring/assets/publishing-status-timeline.png)

* 在[“页面信息”菜单](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information)中（编辑页面时）

  ![“页面信息”菜单中的发布状态](/help/sites-cloud/authoring/assets/publishing-status-page-information.png)
