---
title: 从站点控制台发布页面
description: 了解如何使用站点控制台发布和取消发布页面。
exl-id: 89f2363c-7922-4ca5-92cb-cbee6a393ee3
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 5ad91a32d705ef61e8b9799bf7fb1e136bb8bfa0
workflow-type: tm+mt
source-wordcount: '1635'
ht-degree: 74%

---


# 从站点控制台发布页面 {#publishing-pages}

在创作环境中创建并审核内容后，接下来的目标就是[让内容在您的公共网站（发布环境）中可供使用](/help/sites-cloud/authoring/author-publish.md)。

这称为“发布页面”。当您要从发布环境中删除页面时，此过程称为“取消发布”。发布和取消发布时，该页面在删除之前仍可在创作环境中用于进一步更改。

您可以使用&#x200B;[**站点**&#x200B;控制台](/help/sites-cloud/authoring/sites-console/introduction.md)立即发布/取消发布页面，或者在预定义的将来日期/时间发布/取消发布页面。

>[!TIP]
>
>您可以从站点控制台以外的位置发布。
>
>* 页面编辑器中的[&#128279;](/help/sites-cloud/authoring/page-editor/publishing.md)
>* 从通用编辑器[&#128279;](/help/sites-cloud/authoring/universal-editor/publishing.md)
>* 从体验片段[&#128279;](/help/sites-cloud/authoring/fragments/experience-fragments.md)控制台或编辑器中
>
>从这些位置发布提供了不同的选项，但遵循了此处所述的类似过程和一般想法。

## 术语 {#terminology}

在使用 Adobe Experience Manager (AEM) as a Cloud Service 时，您可能会遇到与发布相关的不同术语。

* **发布/取消发布**
   * 这些是在发布和/或预览环境中公开提供（或不公开提供）您的内容的主要操作术语。
   * 这些是 AEM 文档中使用的术语。
* **激活／取消激活**
   * 这两个术语与发布/取消发布同义。
   * 这些术语在 AEM 的早期版本中使用。
* **复制**
   * 这些是技术术语，用于描述发布页面（例如，从作者到预览）时数据（例如，页面内容、文件、代码、用户评论）从一个服务移动到另一个服务。
   * 这些术语主要由开发人员使用。

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
>
>* 如果只选择子页面进行发布（因为订单信息保存在父页面上）
>* 如果父页面和子页面是在单独的操作中发布的

## 从站点控制台发布页面 {#publishing-from-the-sites-console}

在&#x200B;**站点**&#x200B;控制台中，有两个发布选项：

* [快速发布](#quick-publish)
* [管理发布](#manage-publication)

### 快速发布 {#quick-publish}

**快速发布**&#x200B;适用于一些简单的情况，可立即发布选定的页面，而无需进行任何进一步的交互。正因为这一点，任何未发布的引用也将被自动发布。

要使用“快速发布”发布页面，请执行以下操作：

1. 在站点控制台中选择一个或多个页面，然后单击&#x200B;**快速发布**&#x200B;按钮。

   ![选择要发布的页面](/help/sites-cloud/authoring/assets/publishing-select-pages.png)

1. 在“快速发布”对话框中，单击&#x200B;**发布**&#x200B;以确认发布，或单击&#x200B;**取消**&#x200B;以取消发布。请记住，任何未发布的引用也将被自动发布。

   ![快速发布确认](/help/sites-cloud/authoring/assets/publishing-quick-publish.png)

1. 在发布页面时，将显示确认发布的警报。

>[!NOTE]
>
>“快速发布”是一种简单的发布方式，即只会发布选定的一个或多个页面，而不会发布任何子页面。

### 管理发布 {#manage-publication}

**管理发布**&#x200B;提供的选项比&#x200B;**快速发布**&#x200B;多，允许包含子页面、自定义引用、发布到预览服务（如果可用）和启动任何适用的工作流，并提供在以后的日期发布的选项。

要使用“管理发布”发布或取消发布页面，请执行以下操作：

1. 在站点控制台中选择一个或多个页面，然后单击&#x200B;**管理发布**&#x200B;按钮。

   ![选择要发布的页面](/help/sites-cloud/authoring/assets/publishing-select-pages.png)

1. 此时会启动&#x200B;**管理发布**&#x200B;向导。第一步，**选项**，让你：

   * **操作**

     选择发布或取消发布选定的页面。

   * **目标**

     选择您希望发布到发布服务（默认）还是预览服务。 仅当您配置了[预览服务时可用。](/help/sites-cloud/authoring/sites-console/previewing-content.md)

   * **计划**

     选择立即还是在以后的日期执行该操作。

     稍后发布会启动一个在指定时间发布选定的一个或多个页面的工作流程。相反，稍后取消发布则会启动一个在指定时间取消发布选定的一个或多个页面的工作流程。

     >[!TIP]
     >
     >如果您要稍后撤消发布/取消发布页面，请转到[“工作流程”控制台](/help/sites-cloud/administering/workflows-administering.md#suspending-resuming-and-terminating-a-workflow-instance)以终止相应的工作流程。

     >[!TIP]
     >
     >计划发布的内容会复制内容并遵循发布工作流程。 如果要临时隐藏已发布的内容而不取消发布，请考虑在页面属性中提供&#x200B;[**开始时间**&#x200B;和&#x200B;**结束时间**。](/help/sites-cloud/authoring/sites-console/page-properties.md#basic)

   ![管理发布选项](/help/sites-cloud/authoring/assets/publishing-manage-publication-options.png)

1. 单击&#x200B;**下一步**&#x200B;以继续。

1. 在“管理发布”向导的下一个步骤&#x200B;**范围**&#x200B;中，您可以定义发布/取消发布的范围，如包括子页面和/或包括引用。

   ![管理发布范围](/help/sites-cloud/authoring/assets/publishing-manage-publication-scope.png)

   **添加内容**

   如果您因一时疏忽而忘记在启动“管理发布”向导之前选择某个页面，则可以使用&#x200B;**添加内容**&#x200B;按钮将其他页面添加到要发布的页面列表中。

   选择&#x200B;**添加内容**&#x200B;按钮会启动[路径浏览器](/help/sites-cloud/authoring/path-selection.md)以供选择内容。

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

取消发布页面会将其从您的发布或[预览](/help/sites-cloud/authoring/sites-console/previewing-content.md)环境中移除，因此不再将其提供给您的读者。

正如[使用“管理发布”选项发布页面](#manage-publication)一样，也可以使用它来取消发布页面。

1. 在站点控制台中选择一个或多个页面，然后单击&#x200B;**管理发布**&#x200B;按钮。
1. 此时会启动&#x200B;**管理发布**&#x200B;向导。在第一个步骤&#x200B;**选项**&#x200B;中，选择&#x200B;**取消发布**，而不是默认选项&#x200B;**发布**。

   ![取消发布 – 选项](/help/sites-cloud/authoring/assets/publishing-unpublish.png)

   正如稍后发布会启动一个工作流程，以在指定时间发布此版本页面一样，稍后取消激活也会启动一个工作流程，以在指定时间取消发布选定的一个或多个页面。

   >[!NOTE]
   >
   >如果您要稍后撤消发布/取消发布页面，请转到[“工作流程”控制台](/help/sites-cloud/administering/workflows-administering.md#suspending-resuming-and-terminating-a-workflow-instance)以终止相应的工作流程。

   >[!NOTE]
   >如果您有一个[预览](/help/sites-cloud/authoring/sites-console/previewing-content.md)环境，您可以在管理发布期间选择&#x200B;**目标**。

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

* 在[ Sites 控制台上的资源概述信息](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources)中

  ![信息卡视图中的发布状态](/help/sites-cloud/authoring/assets/publishing-status-console-card.png)

  Sites 控制台的[信息卡](/help/sites-cloud/authoring/basic-handling.md#card-view)、[列](/help/sites-cloud/authoring/basic-handling.md#column-view)和[列表](/help/sites-cloud/authoring/basic-handling.md#list-view)视图中将显示发布状态。

* 在[时间线](/help/sites-cloud/authoring/basic-handling.md#timeline)中

  ![时间线视图中的发布状态](/help/sites-cloud/authoring/assets/publishing-status-timeline.png)

* 在[“页面信息”菜单](/help/sites-cloud/authoring/page-editor/introduction.md#page-information)中（编辑页面时）

  ![“页面信息”菜单中的发布状态](/help/sites-cloud/authoring/assets/publishing-status-page-information.png)
