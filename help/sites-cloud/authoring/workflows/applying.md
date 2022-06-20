---
title: 将工作流应用于页面
description: 进行创作时，您可以调用工作流以在页面上执行操作；也可以应用多个工作流。
exl-id: 86e71f0e-e53e-40bc-901d-2a1ab347bd0a
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: ht
source-wordcount: '662'
ht-degree: 100%

---

# 将工作流应用于页面 {#applying-workflows-to-pages}

进行创作时，您可以调用工作流以在页面上执行操作；也可以应用多个工作流。

在应用工作流时，您需要指定以下信息：

* 要应用的工作流。
   * 您可以应用任何工作流（您有权访问，由 AEM 管理员分配）。
* （可选）有助于在用户收件箱中识别工作流实例的标题。
* 工作流有效负荷；这可以是一个或多个页面。

可以从以下位置启动工作流：

* [站点控制台](#starting-a-workflow-from-the-sites-console)。
* [编辑页面时，从“页面信息”](#starting-a-workflow-from-the-page-editor)启动。

>[!NOTE]
>
>另请参阅：
>
>* 如何将工作流应用于 DAM 资产。
>* [使用项目工作流](/help/sites-cloud/authoring/projects/workflows.md)。


<!-- 
>* [How to apply workflows to DAM assets](/help/assets/assets-workflow.md).
>* [Working with Project Workflows](/help/sites-cloud/authoring/projects/workflows.md).
-->

>[!NOTE]
>
>AEM 管理员可以使用其他几种方法来启动工作流。

<!-- 
>AEM administrators can [start workflows using several other methods](/help/sites-administering/workflows-starting.md).
-->

## 从“站点”控制台启动工作流 {#starting-a-workflow-from-the-sites-console}

您可以从以下任一项中启动工作流：

* [“站点”工具栏的“创建”选项](#starting-a-workflow-from-the-sites-toolbar)。
* [“站点”控制台的时间线边栏](#starting-a-workflow-from-the-timeline)。

在这两种情况下，您都将需要：

* [在“创建工作流”向导中指定工作流详细信息](#specifying-workflow-details-in-the-create-workflow-wizard)。

### 从“站点”工具栏启动工作流 {#starting-a-workflow-from-the-sites-toolbar}

您可以从&#x200B;**站点**&#x200B;控制台的工具栏中启动工作流：

1. 导航到所需的页面并选择该页面。

1. 现在，您可以从工具栏的&#x200B;**创建**&#x200B;选项中选择&#x200B;**工作流**。

   ![从工具栏创建工作流](/help/sites-cloud/authoring/assets/workflows-create-from-toolbar.png)

1. **创建工作流**&#x200B;向导将帮助您[指定工作流详细信息](#specifying-workflow-details-in-the-create-workflow-wizard)。

### 从时间线启动工作流 {#starting-a-workflow-from-the-timeline}

您可以从&#x200B;**时间线**&#x200B;中启动要应用于所选资源的工作流。

1. [选择资源](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)，然后打开[时间线](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)（或打开时间线，然后选择资源）。
1. 可以使用评论字段中的箭头显示&#x200B;**启动工作流**：

   ![从时间线创建工作流](/help/sites-cloud/authoring/assets/workflows-create-from-timeline.png)

1. **创建工作流**&#x200B;向导将帮助您[指定工作流详细信息](#specifying-workflow-details-in-the-create-workflow-wizard)。

### 在“创建工作流”向导中指定工作流详细信息 {#specifying-workflow-details-in-the-create-workflow-wizard}

**创建工作流**&#x200B;向导将帮助您选择工作流并指定所需的详细信息。

从以下任一项中打开&#x200B;**创建工作流**&#x200B;向导后：

* [“站点”工具栏的“创建”选项](#starting-a-workflow-from-the-sites-toolbar)。
* [“站点”控制台的时间线边栏](#starting-a-workflow-from-the-timeline)。

您可以指定详细信息：

1. 在&#x200B;**属性**&#x200B;步骤中，定义了工作流的基本选项：

   * **工作流模型**
   * **工作流标题**

      * 您可以指定此实例的标题，以帮助您在以后对其进行识别。

   根据工作流模型，还可以使用以下选项。这些选项允许在工作流完成后保留创建为有效负荷的包。

   * **保留工作流包**
   * **包标题**

      * 您可以指定包标题以便进行识别。
   >[!NOTE]
   >
   >为多资源支持配置了工作流并选择了多个资源时，**保留工作流包**&#x200B;选项可用。

   <!--
   >The **Keep workflow package** option is available when the workflow has been configured for [Multi Resource Support](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support) and multiple resources have been selected.
   -->

   完成后，单击&#x200B;**下一步**&#x200B;继续。

   ![指定工作流属性](/help/sites-cloud/authoring/assets/workflows-properties.png)

1. 在&#x200B;**范围**&#x200B;步骤中，您可以选择：

   * **添加内容**&#x200B;以打开[路径浏览器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#path-browser)并选择其他资源；在浏览器中，单击/点按&#x200B;**选择**&#x200B;以将内容添加到工作流实例。

   * 现有资源以查看其他操作：

      * **包括子项**，指定将该资源的子项包含在工作流中。
系统将打开一个对话框，允许您根据以下各项优化选择：

         * 仅包括下级子项。
         * 仅包括已修改的页面。
         * 仅包括已发布的页面。

         指定的任何子项都会添加到将应用工作流的资源列表中。

      * **删除选择**，从工作流中删除该资源。

   ![定义工作流范围](/help/sites-cloud/authoring/assets/workflows-scope.png)

   >[!NOTE]
   >
   >如果添加其他资源，则可以使用&#x200B;**返回**，在&#x200B;**属性**&#x200B;步骤中调整&#x200B;**保留工作流包**&#x200B;的设置。

1. 使用&#x200B;**创建**&#x200B;关闭向导并创建工作流实例。“站点”控制台中随即会显示一则通知。

## 从页面编辑器启动工作流 {#starting-a-workflow-from-the-page-editor}

编辑页面时，您可以从工具栏中选择&#x200B;**页面信息**。下拉菜单中包含&#x200B;**启动工作流**&#x200B;选项。此选项将打开一个对话框，您可以在其中指定所需的工作流，如果需要，还可以指定标题：

![从页面编辑器启动工作流](/help/sites-cloud/authoring/assets/workflows-create-page-editor.png)
