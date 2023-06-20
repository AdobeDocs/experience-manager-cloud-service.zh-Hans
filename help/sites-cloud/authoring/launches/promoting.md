---
title: 提升启动项
description: 您需要提升启动页面，以便在发布之前将内容移回源（生产）。
exl-id: 5f5ed17c-43db-4ef6-ab79-c491326fa01c
source-git-commit: 635f4c990c27a7646d97ebd08b453c71133f01b3
workflow-type: tm+mt
source-wordcount: '814'
ht-degree: 38%

---

# 提升启动项 {#promoting-launches}

您需要提升启动页面，以便在发布之前将内容移回源（生产）。 提升启动页面时，源页面的相应页面将被提升页面的内容替换。 提升启动页面时，可以使用以下选项：

* 是仅提升当前页面还是整个启动项。
* 是否提升当前页面的子页面。
* 是提升整个启动项，还是仅提升已更改的页面。
* 提升后是否删除启动项。

>[!NOTE]
>
>将启动页面提升到目标后(**生产**)，您可以激活 **生产** 页面作为图元（以加快处理速度）。 将页面添加到工作流包，并将其用作激活页面包的工作流的负载。 在提升启动项之前，您需要创建工作流包。 参见 [使用AEM工作流处理提升的页面](#processing-promoted-pages-using-aem-workflow).

>[!CAUTION]
>
>无法同时提升单个启动项。 这意味着，对同一个启动项同时执行两次提升操作可能会导致出现以下错误：`Launch could not be promoted`（同时还会导致日志中出现冲突错误）。

>[!CAUTION]
>
>提升启动项时 *修改时间* 页面，会考虑源分支和启动分支中的修改。

## 提升启动页面 {#promoting-launch-pages}

>[!NOTE]
>
>这涵盖了在只有一个启动级别时提升启动页面的手动操作。 请参阅：
>
>* [提升嵌套启动项](#promoting-a-nested-launch) 当结构中有多个启动项时。
>* [启动次数 — 事件的顺序](/help/sites-cloud/authoring/launches/overview.md#launches-the-order-of-events) 有关自动升级和发布的更多详细信息。
>

您可以通过以下任一方式提升启动项： **站点** 控制台或 **启动次数** 控制台：

1. 打开：
   * **站点**&#x200B;控制台（导航源页面时）：
      1. 打开[引用边栏](/help/sites-cloud/authoring/fundamentals/environment-tools.md#references)，然后使用[选择模式](/help/sites-cloud/authoring/getting-started/basic-handling.md)选择所需的源页面（或者先进行选择，然后再打开引用边栏，顺序不重要）。将显示所有引用。
      1. 选择&#x200B;**启动项**（例如“启动项 (1)”），可显示特定启动项的列表。
      1. 选择特定启动项以显示可用的操作。
      1. 选择&#x200B;**提升启动项**&#x200B;以打开向导。
   * **站点**&#x200B;控制台（导航启动页面时）：
      1. 使用[选择模式](/help/sites-cloud/authoring/getting-started/basic-handling.md)选择所需的启动页面。
      1. 此 **提升** 操作在工具栏中可用。
   * **启动项**&#x200B;控制台：
      1. 选择您的启动项（点按/单击缩略图）。
      1. 选择 **提升**.
1. 在第一步中，您可以指定：
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
     >这涵盖单个启动项（如果您具有嵌套启动项），请参阅 [提升嵌套启动项](#promoting-a-nested-launch).
1. 选择 **下一个** 以继续。
1. 您可以查看要提升的页面，具体页面取决于您选择的页面范围：

   ![查看提升](/help/sites-cloud/authoring/assets/launches-promote-review.png)

1. 选择 **提升**.

## 编辑时提升启动页面 {#promoting-launch-pages-when-editing}

编辑启动页面时， **提升启动项** 操作也可从 **页面信息**. 这将打开相应向导来收集所需的信息。

![从站点信息提升启动项](/help/sites-cloud/authoring/assets/launches-promote-page-info.png)

>[!NOTE]
>
>这适用于单个和 [嵌套启动项](#promoting-a-nested-launch).

## 提升嵌套启动项 {#promoting-a-nested-launch}

创建嵌套启动项后，您可以将其提升回任何源，包括根源（生产）。

![嵌套启动项](/help/sites-cloud/authoring/assets/launches-promoting-nested.png)

1. 与创建嵌套启动项一样，在&#x200B;**启动项**&#x200B;控制台或&#x200B;**引用**&#x200B;边栏中导航到所需的启动项并将其选中。
1. 选择&#x200B;**提升启动项**&#x200B;以打开向导。
1. 输入所需的详细信息：
   * **目标**
      * **提升目标** – 您可以提升到任意源。
      * **提升后删除启动项**  — 提升后，将删除选定的启动项以及嵌套在其中的任何启动项。
   * **范围** – 在此处，您可以选择是提升整个启动项，还是仅提升已实际编辑的页面。如果是后者，则可以选择包含/排除子页面。 默认配置是仅提升当前页面的页面更改：
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
   >列出的页面取决于 **范围** 已定义，可能还包括实际编辑的页面。

1. 您的更改将提升并反映在 **启动次数** 控制台：

   ![在启动项控制台中](/help/sites-cloud/authoring/assets/launches-console.png)

## 使用 AEM 工作流处理提升的页面 {#processing-promoted-pages-using-aem-workflow}

使用工作流模型可对提升的启动项页面执行批量处理：

1. 创建工作流包。
1. 作者提升Launch页面时，会将它们存储在工作流包中。
1. 使用包作为有效负载启动工作流模型。

要在提升页面时自动启动工作流，请为包节点配置工作流启动器。<!--To start a workflow automatically when pages are promoted, [configure a workflow launcher](/help/sites-administering/workflows-starting.md#workflows-launchers) for the package node.-->

例如，您可以在作者提升启动项页面时自动生成页面激活请求。 配置工作流启动器，以便在修改包节点后启动“请求激活”工作流。

![提升工作流](/help/sites-cloud/authoring/assets/launches-create-workflow.png)
