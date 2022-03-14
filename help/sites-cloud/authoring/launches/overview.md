---
title: 启动项
description: 使用启动项，您可以有效地开发内容的将来版本。它们允许您进行更改以准备将来发布，同时保留当前页面
exl-id: 3e410120-d08f-4d05-932f-07bc4440af2b
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '907'
ht-degree: 81%

---

# 启动项 {#launches}

使用启动项，您可以有效地开发内容的将来版本。

通过创建启动项，您可以进行更改以准备将来发布（同时保留当前页面）。编辑和更新启动页面后，需将其提升回源，然后激活源页面（顶层）。提升会将启动项内容复制回源页面，此操作可以手动或自动完成（具体取决于创建和编辑启动项时设置的字段）。

例如，您的在线商店上的季节性产品页面会每季更新，这样就能保证特色产品符合当季需求。要准备下一季度的更新，您需要创建相应网页的启动项。在整个季度期间，启动副本中会累积以下更改：

* 对因为执行常规维护任务而对源页面做出的更改。这些更改会自动复制到启动页面中。
* 为下一季度做准备而在启动页面上直接执行的编辑。

您也可以:

* 在启动分支中导航内容；根据需要添加或删除页面。
* 预览已发布内容在将来的特定日期/时间的显示情况。

当下一季度到来时，您需要提升启动页面，以便发布源页面（包含更新的内容）。您可以提升所有页面，也可以仅提升已修改的页面。

此外，您也可以：

* 为多个根目录分支创建启动项。虽然您可以为整个站点创建启动项（并从中做出更改），但由于需要复制整个站点，因此这可能不切实际。当涉及数百甚至数千个页面时，系统要求和性能会受到复制操作以及后续提升任务所需的比较操作的影响。
* 嵌套启动项（一个启动项嵌套在另一个启动项中），以便能够从现有启动项中创建启动项，这样作者便可以利用已经做出的更改，而不必反复地为每个启动项执行相同的更改。

本节将介绍如何创建、编辑和提升（如有必要） [删除](/help/sites-cloud/authoring/launches/creating.md#deleting-a-launch))从站点控制台中启动页面，或 [启动项控制台](#the-launches-console):

* [创建启动项](/help/sites-cloud/authoring/launches/creating.md)
* [编辑启动项](/help/sites-cloud/authoring/launches/editing.md)
* [在启动项中管理页面](/help/sites-cloud/authoring/launches/managing-pages.md)
* [使用时间扭曲根据启动项预览内容](/help/sites-cloud/authoring/launches/preview.md)
* [提升启动项](/help/sites-cloud/authoring/launches/promoting.md)

## 启动项 - 事件的顺序 {#launches-the-order-of-events}

启动项允许您有效地为将来发布的一个或多个激活网页开发内容。

它们允许您：

* 创建源页面的副本：
   * 副本是您的启动项。
   * 顶级源页面称为&#x200B;**生产**。
      * 源页面可以从多个（不同的）分支中获取。

   ![启动项的操作顺序](/help/sites-cloud/authoring/assets/launches-order.png)

* 编辑启动配置：
   * 在启动项中添加或删除页面和/或分支。
   * 编辑启动项属性；如标 **题**、启 **动日期**、生 **产就绪标记** 。
* 您可以手动或自动提升和发布内容：
   * 手动：
      * 准备好发布时，将您的启动项内容提升回&#x200B;**目标**（源页面）。
      * 发布源（在提升回后）页面中的内容。
      * 提升所有页面或仅提升已修改的页面。
   * 自动 - 这涉及以下各项：
      * **启动**（**起始**）**日期**&#x200B;字段：可在创建或编辑启动项时设置此字段。
      * **生产就绪**&#x200B;标记：只能在编辑启动项时设置此标记。
      * 如果&#x200B;**生产就绪**&#x200B;标记已设置，则启动项将于指定的&#x200B;**启动**（**起始**）**日期**&#x200B;自动提升到生产页面。升级后，生产页面会自动发布。\
         如果未设置日期，该标记将不起作用。
* 并行更新源页面和启动页面：
   * 对源页面所做的更改会自动体现在启动副本中（如果进行了继承设置，即设置为 Live Copy）。
   * 可以在不中断这些自动更新或源页面的情况下对启动副本进行更改。

   ![并行操作](/help/sites-cloud/authoring/assets/launches-parallel.png)

* [创建嵌套启动项](/help/sites-cloud/authoring/launches/creating.md#creating-a-nested-launch) - 一个启动项嵌套在另一个启动项中：
   * 源是现有的启动项。
   * 您可以将[嵌套启动项提升](/help/sites-cloud/authoring/launches/promoting.md#promoting-a-nested-launch)到任何目标；该目标可以是父启动项或顶层源页面（生产）。

   ![嵌套启动项](/help/sites-cloud/authoring/assets/launches-nested.png)

   >[!CAUTION]
   >
   >删除启动项时，将会删除该启动项本身及其所有下级嵌套启动项。

>[!NOTE]
>
>创建和编辑启动项时，需要具有 `/content/launches`  — 与默认组一样 `content-authors`.
>
>如果您遇到任何问题，请联系您的系统管理员。

## “引用”（“站点”控制台）中的启动项 {#launches-in-references-sites-console}

1. 在&#x200B;**站点**&#x200B;控制台中，导航到启动项的源。
1. 打开&#x200B;**引用**&#x200B;边栏并选择源页面。
1. 选择 **启动项**，则会列出现有的启动项，以及对 **启动项控制台**:

   ![站点控制台中启动项的引用](/help/sites-cloud/authoring/assets/launches-references.png)

1. 点按/单击相应的启动项，此时将显示可执行的操作列表：

   ![在站点控制台中对启动项执行的操作](/help/sites-cloud/authoring/assets/launches-references-actions.png)

## “启动项”控制台 {#the-launches-console}

“启动项”控制台提供了启动项的概览，并允许您对列出的启动项执行操作。该控制台可以通过以下方式访问：

* **工具**&#x200B;控制台：**工具**、**站点**、**启动项**。

* **启动项控制台** 在 **启动项** 部分 **引用** 在站点控制台中导航源内容时进行边栏。

   ![“站点”控制台中启动项引用的启动项控制台](/help/sites-cloud/authoring/assets/launches-references.png)

* 的 **启动项** 按钮，在站点控制台中导航启动项内容时：

   ![站点控制台中的启动项选项](/help/sites-cloud/authoring/assets/launches-console-navigate-launch-content.png)

* 或者直接；例如，使用：
   `https://<host>:<port>/libs/launches/content/launches.html`
