---
title: 发布页面
description: 如何使用AEM发布和取消发布页面
translation-type: tm+mt
source-git-commit: e88a814a901d7fa0da2675fa6017c66d61a73445

---


# 发布页面 {#publishing-pages}

在创作环境中创建并审核内容后，接下来的目标就是[让内容在您的公共网站（发布环境）中可供使用](/help/sites-cloud/authoring/getting-started/concepts.md)。

这称为“发布页面”。当您要从发布环境中删除页面时，此过程称为“取消发布”。在发布和取消发布时，页面会保留在创作环境中以供进一步更改，直到将其删除为止。

您可以立即发布／取消发布页面，也可以在预定义的日期／时间在将来发布／取消发布页面。

## 术语 {#terminology}

在使用AEM时，您可能会遇到与发布相关的不同术语。

* **发布/取消发布**
   * 这些是使内容在发布环境中公开可用（或不公开）的主要操作条款。
   * 这些是AEM文档中使用的术语。
* **激活／取消激活**
   * 这些术语与发布／取消发布同义。
   * 这些术语在AEM的早期版本中使用。
* **复制**
   * 这些是描述在发布页面时数据（例如，页面内容、文件、代码、用户注释）从一个环境移动到另一个环境的技术术语。
   * 这些术语主要由开发人员使用。

## 发布页面 {#publishing-pages-1}

根据您所在的位置，可以通过下列方式发布：

* [从页面编辑器中](#publishing-from-the-editor)
* [从站点控制台中](#publishing-from-the-console)

>[!NOTE]
>
>如果您没有必要的权限来发布特定页面：
>
>* 将触发一个工作流，向相应的人员通知您的发布请求。
>* 您的开发团队可能已自定义此工作流。
>* 将显示一条简短的消息，通知您工作流已经触发。

<!--
>* This [workflow may have been customized](/help/sites-developing/workflows-models.md#main-pars-procedure-6fe6) by your development team.
>* A message will be displayed briefly to notify you that the workflow was triggered.
-->

### 从编辑器中发布 {#publishing-from-the-editor}

如果您在编辑页面，则可以直接从编辑器中发布该页面。

1. Select the **Page Information** icon to open the menu and then the **Publish Page** option.

   ![通过页面选项发布页面](/help/sites-cloud/authoring/assets/publishing-page-options.png)

1. 根据页面是否包含需要发布的引用：

   * 如果不包含要发布的引用，则将直接发布页面。
   * 如果页面包含需要发布的引用，则将在&#x200B;**发布**&#x200B;向导中列出该内容，从该向导中可以：
      * Specify which of the assets/tags/etc. you want to publish together with the page, then use **Publish** to complete the process.
      * 使用&#x200B;**取消**&#x200B;中止操作。
   ![发布页面引用](/help/sites-cloud/authoring/assets/publishing-references.png)

1. Selecting **Publish** will replicate the page to the publish environment. 在页面编辑器中，将显示一个确认发布操作的信息横幅。

   ![发布状态信息横幅](/help/sites-cloud/authoring/assets/publishing-info.png)

   当在控制台中查看同一页面时，将显示更新的发布状态。

   ![站点控制台中列视图中的页面发布状态](/help/sites-cloud/authoring/assets/publishing-status-console-column.png)

>[!NOTE]
>
>从编辑器发布是一个浅层发布，即只发布选定的页面／页面，而不发布任何子页面。

### 从控制台中发布 {#publishing-from-the-console}

站点控制台中有两个用于发布的选项：

* [快速发布](#quick-publish)
* [管理发布](#manage-publication)

#### 快速发布 {#quick-publish}

**“快速发布** ”适用于简单的情况，可立即发布选定的页面，无需进行任何进一步交互。 正因为这一点，任何未发布的引用也将被自动发布。

要使用“快速发布”发布页面，请执行以下操作：

1. Select the page or pages in the sites console and click on the **Quick Publish** button.

   ![选择要发布的页面](/help/sites-cloud/authoring/assets/publishing-select-pages.png)

1. In the Quick Publish dialog, confirm the publication by clicking on **Publish** or cancel by clicking on **Cancel**. 请记住，任何未发布的引用也将被自动发布。

   ![快速发布确认](/help/sites-cloud/authoring/assets/publishing-quick-publish.png)

1. 在发布页面时，将显示确认发布的警报。

>[!NOTE]
>
>“快速发布”是一种简单的发布方式，即只会发布选定的一个或多个页面，而不会发布任何子页面。

#### 管理发布 {#manage-publication}

**“管理出版物** ”提供的选项比“快速发布”更多，允许包含子页面、自定义引用、启动任何适用的工作流以及提供在以后的日期发布的选项。

要使用“管理发布”发布或取消发布页面，请执行以下操作：

1. Select the page or pages in the sites console and click on the **Manage Publication** button.

   ![选择要发布的页面](/help/sites-cloud/authoring/assets/publishing-select-pages.png)

1. The **Manage Publication** wizard starts. The first step, **Options**, allows you to:

   * 选择发布或取消发布选定的页面。
   * 选择立即还是在以后的日期执行该操作。
   稍后发布会启动一个在指定时间发布选定的一个或多个页面的工作流。相反，稍后取消发布则会启动一个在指定时间取消发布选定的一个或多个页面的工作流。

   If you want to cancel a publish/unpublish later, go to the Workflow Console to terminate the corresponding workflow. <!--If you want to cancel a publish/unpublish later, go to the [Workflow Console](/help/sites-administering/workflows.md) to terminate the corresponding workflow.-->

   ![管理发布选项](/help/sites-cloud/authoring/assets/publishing-manage-publication-options.png)

   单击&#x200B;**下一步**&#x200B;以继续。

1. In the next step of the Manage Publication wizard, **Scope**, you can define the scope of the publication/un-publication such as including to include child pages and/or including references.

   ![管理发布范围](/help/sites-cloud/authoring/assets/publishing-manage-publication-scope.png)

   You can use the **Add Content** button to add additional pages to the list of pages to be published in case you neglected to select one before starting the Manage Publication wizard.

   单击“添加内容”按钮会启动[路径浏览器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#path-browser)以供选择内容。

   Select the required pages and then click **Select** to add the content to the wizard or **Cancel **to cancel the selection and return to the wizard.

   返回到向导后，您可以选择列表中的项目以进一步配置其选项，例如：

   * 包括其子项。
   * 将其从选择中删除。
   * 管理其已发布的引用。
   ![管理发布选择页面](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

   Clicking **Include Children** opens a dialogue allowing you to:

   * 仅包括下级子项。
   * 仅包括已修改的页面。
   * 仅包括已发布的页面。
   Click **Add** to add the children pages to the list of pages to be published or unpublished based on the selection options. Click **Cancel** to cancel the selection and return to the wizard.

   ![管理出版物（包括子项）](/help/sites-cloud/authoring/assets/publishing-include-children.png)

   返回到向导后，您将看到根据您在“包括子项”对话框中选择的选项添加的页面。

   You can view and modify the references to be published or unpublished for a page by selecting it and then clicking the **Published References** button.

   ![管理发布选项](/help/sites-cloud/authoring/assets/publishing-manage-publication-references.png)

   The **Published References** dialog displays the references for the selected content. 默认情况下，它们都处于选中状态并将被发布／取消发布，但您可以取消选中以取消选中它们，以便不将其包含在操作中。

   Click **Done** to save your changes or **Cancel** to cancel the selection and return to the wizard.

   返回到向导后，**引用**&#x200B;列将进行相应的更新，以反映您选择的要发布或取消发布的引用。

   ![管理发布选择页面](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

1. Click **Publish** to complete.

   返回到站点控制台后，将显示一条确认发布的通知消息。

1. If the published pages are associated with workflows, they may be shown in a final **Workflows** step of the publication wizard.

   >[!NOTE]
   >
   >The **Workflows** step will be shown based on what rights your user may or may not have. See the previous note on this page regarding publishing privileges as well as Managing Access to Workflows and [Applying Workflows to Pages](/help/sites-cloud/authoring/workflows/applying.md) for details.
   <!--
   >The **Workflows** step will be shown based on what rights your user may or may not have. See the previous note on this page regarding publishing privileges as well as [Managing Access to Workflows](/help/sites-administering/workflows-managing.md) and [Applying Workflows to Pages](/help/sites-cloud/authoring/workflows/applying.md) for details.
   -->

   资源将按触发的工作流分组，并且每组都提供了用于执行以下操作的选项：

   * 定义工作流的标题。
   * Keep the workflow package, provided that the workflow has multi-resource support. <!--Keep the workflow package, provided that the workflow has [multi-resource support](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support).-->
   * 在选择保留工作流包的选项时，定义工作流包的标题。
   Click **Publish** or **Publish Later** to complete the publication.

## 取消发布页面 {#unpublishing-pages}

取消发布页面将从发布环境中删除该页面，以便不再将其提供给您的读者。

In a [manner similar to publishing](#publishing-pages), one or more pages can be unpublished:

* [从页面编辑器中](#unpublishing-from-the-editor)
* [从站点控制台中](#unpublishing-from-the-console)

### 从编辑器中取消发布 {#unpublishing-from-the-editor}

在编辑页面时，如果您希望取消发布该页面，请选择&#x200B;**页面信息**&#x200B;菜单中的&#x200B;**取消发布页面**，这与[发布页面](#publishing-from-the-editor)非常类似。

### 从控制台中取消发布 {#unpublishing-from-the-console}

正如[使用“管理发布”选项发布页面](#manage-publication)一样，也可以使用它来取消发布页面。

1. Select the page or pages in the sites console and click on the **Manage Publication** button.
1. The **Manage Publication** wizard starts. In the first step, **Options**, select to **Unpublish** instead of the default option of **Publish**.

   ![正在取消发布](/help/sites-cloud/authoring/assets/publishing-unpublish.png)

   正如稍后发布会启动一个工作流，以在指定时间发布此版本页面一样，稍后取消激活也会启动一个工作流，以在指定时间取消发布选定的一个或多个页面。

   If you want to cancel a publish/unpublish later, go to the Workflow Console to terminate the corresponding workflow. <!--If you want to cancel a publish/unpublish later, go to the [Workflow Console](/help/sites-administering/workflows.md) to terminate the corresponding workflow.-->

1. To complete the un-publication, continue through the wizard as you would to [publish the page](#manage-publication).

## 发布和取消发布树 {#publishing-and-unpublishing-a-tree}

如果输入或更新了大量内容页面（所有内容页面都位于同一根页面下），则可以更轻松地通过一个操作来发布整个树。

您可以使用站点控制台上的[管理发布](#manage-publication)选项来完成此操作。

1. 在站点控制台中，选择您希望发布或取消发布的树的根页面，然后选择&#x200B;**管理发布**。
1. The **Manage Publication** wizard starts. 选择发布或取消发布以及应在何时开始，然后选择&#x200B;**下一步**&#x200B;以继续。
1. 在&#x200B;**范围**&#x200B;步骤中，选择根页面，然后选择&#x200B;**包括子项**。

   ![管理发布选择页面](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

1. In the **Include Children** dialogue, un-check the options:

   * 仅包括下级子项
   * 仅包括已发布的页面
   这些选项默认处于选中状态，因此您必须记得取消选择它们。Click **Add** to confirm and add the content to the publication/un-publication.

   ![取消发布时包含子项](/help/sites-cloud/authoring/assets/publishing-tree-children.png)

1. **管理发布**&#x200B;向导将列出树内容以供查看。您可以通过添加其他页面或删除选定页面来进一步自定义所做的选择。

   ![管理发布选项](/help/sites-cloud/authoring/assets/publishing-tree-select.png)

   Remember that you can also review the references to be published via the **Published References** option.

1. [按正常方式继续“管理发布](#manage-publication) ”向导，以完成树的发布或取消发布。

## 确定发布状态 {#determining-publication-status}

您可以确定页面的发布状态：

* 在[站点控制台上的资源概述信息](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)中

   ![卡片视图中的发布状态](/help/sites-cloud/authoring/assets/publishing-status-console-card.png)

   站点控制台的[卡片](/help/sites-cloud/authoring/getting-started/basic-handling.md#card-view)、[列](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view)和[列表](/help/sites-cloud/authoring/getting-started/basic-handling.md#list-view)视图中将显示发布状态。

* In the [timeline](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)

   ![时间轴视图中的发布状态](/help/sites-cloud/authoring/assets/publishing-status-timeline.png)

* In the [Page Information menu](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information) when editing a page

   ![页面信息菜单中的发布状态](/help/sites-cloud/authoring/assets/publishing-status-page-information.png)
