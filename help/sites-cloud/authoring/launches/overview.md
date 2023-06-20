---
title: 启动项
description: 通过启动项，您可以高效地为未来版本开发内容。 它们允许您进行更改，以便将来发布，同时维护当前页面
exl-id: 3e410120-d08f-4d05-932f-07bc4440af2b
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 41%

---

# 启动项 {#launches}

通过启动项，您可以高效地为未来版本开发内容。

创建启动项是为了允许您进行更改，以便将来发布（同时维护当前页面）。 编辑和更新启动页面后，您可以将其提升回源页面，然后激活源页面（顶级）。 提升会将启动项内容复制回源页面，并且可以手动或自动完成（取决于创建和编辑启动项时设置的字段）。

例如，在线商店的季节性产品页面每季度更新一次，以便特色产品与当前季节保持一致。 要准备下一次季度更新，您可以创建相应网页的启动项。 在整个季度，启动副本中累积了以下更改：

* 由于正常维护任务而发生的对源页面的更改。 这些更改将在启动页面中自动复制。
* 直接在启动页面上执行的编辑，为下一季度做准备。

您也可以：

* 在启动项分支中导航内容；根据需要添加或删除页面。
* 预览已发布内容在将来的特定日期/时间的外观。

当下一季度到来时，您需要提升启动页面，以便发布源页面（包含更新的内容）。您可以提升所有页面，也可以仅提升已修改的页面。

启动项还可以是：

* 为多个根分支创建。 虽然您可以为整个站点创建启动项（并在其中进行更改），但由于需要复制整个站点，此操作可能不切实际。 当涉及数百甚至数千个页面时，系统需求和性能会同时受到复制操作以及升级任务所需的比较的影响。
* 嵌套（启动项中的启动项），允许您从现有启动项创建启动项，以便作者可以利用已做出的更改，而不必对每个启动项多次进行相同的更改。

此部分介绍了如何从“站点”控制台或[“启动项”控制台](#the-launches-console)中创建、编辑和提升（以及在必要[删除](/help/sites-cloud/authoring/launches/creating.md#deleting-a-launch)）启动页面：

* [创建启动项](/help/sites-cloud/authoring/launches/creating.md)
* [编辑启动项](/help/sites-cloud/authoring/launches/editing.md)
* [管理启动项中的页面](/help/sites-cloud/authoring/launches/managing-pages.md)
* [使用时间扭曲功能预览基于启动项的内容](/help/sites-cloud/authoring/launches/preview.md)
* [提升启动项](/help/sites-cloud/authoring/launches/promoting.md)

## 启动次数 — 事件的顺序 {#launches-the-order-of-events}

通过启动项，您可以高效地为将来版本的一个或多个激活的网页开发内容。

启动项允许您：

* 创建源页面的副本：
   * 副本是您的启动项。
   * 顶级源页面称为&#x200B;**生产**。
      * 源页面可以从多个（单独的）分支获取。

  ![启动项操作顺序](/help/sites-cloud/authoring/assets/launches-order.png)

* 编辑启动项配置：
   * 在启动项中添加或删除页面和/或分支。
   * 编辑启动项属性；例如&#x200B;**标题**、**启动日期**、**生产就绪**&#x200B;标记。
* 您可以手动或自动提升和发布内容：
   * 手动:
      * 将启动项内容提升回 **Target** （源页面）。
      * 发布源页面中的内容（回调后）。
      * 提升所有页面，或仅提升已修改的页面。
   * 自动 – 这涉及以下各项：
      * **启动**（**起始**）**日期**&#x200B;字段：可在创建或编辑启动项时设置此字段。
      * 此 **生产就绪** 标志：此项只能在编辑启动项时设置。
      * 如果 **生产就绪** 设置标记后，启动项将自动升级到指定上的生产页面 **Launch**(**实时**) **日期**. 提升后，生产页面会自动发布。\
        如果未设置日期，该标记将不起作用。
* 并行更新源页面和启动页面：
   * 对源页面所做的更改会自动体现在启动副本中（如果进行了继承设置，即设置为 Live Copy）。
   * 可以在不中断这些自动更新或源页面的情况下对启动副本进行更改。

  ![并行操作](/help/sites-cloud/authoring/assets/launches-parallel.png)

* [创建嵌套启动项](/help/sites-cloud/authoring/launches/creating.md#creating-a-nested-launch)  — 启动项中的启动项：
   * 源是一个现有的启动项。
   * 您可以 [提升嵌套启动项](/help/sites-cloud/authoring/launches/promoting.md#promoting-a-nested-launch) 指向任何目标；这可以是父启动项或顶级源页面（生产）。

  ![嵌套启动项](/help/sites-cloud/authoring/assets/launches-nested.png)

  >[!CAUTION]
  >
  >删除启动项时，将会删除该启动项本身及其所有下级嵌套启动项。

>[!NOTE]
>
>要创建和编辑启动项，需要拥有 `/content/launches` 的访问权限 – 与默认组 `content-authors` 的权限相同。
>
>如果您遇到任何问题，请联系您的系统管理员。

## 引用中的启动项（站点控制台） {#launches-in-references-sites-console}

1. 在 **站点** 控制台中，导航到启动项的源。
1. 打开 **引用** 边栏并选择源页面。
1. 选择&#x200B;**启动项**，这将列出现有启动项以及对&#x200B;**启动项控制台**&#x200B;的访问：

   ![站点控制台中的启动项引用](/help/sites-cloud/authoring/assets/launches-references.png)

1. 点按/单击相应的启动项，此时将显示可执行的操作列表：

   ![要对站点控制台中的启动项执行的操作](/help/sites-cloud/authoring/assets/launches-references-actions.png)

## 启动项控制台 {#the-launches-console}

“启动项”控制台提供了启动项的概述，允许您对列出的启动项执行操作。 可以通过以下方式访问该控制台：

* **工具**&#x200B;控制台：**工具**、**站点**、**启动项**。

* **引用**&#x200B;边栏的&#x200B;**启动项**&#x200B;部分底部的&#x200B;**启动项控制台**（在站点控制台中导航源内容时）。

  ![站点控制台中的启动项引用中的启动项控制台](/help/sites-cloud/authoring/assets/launches-references.png)

* 右上方的&#x200B;**启动项**&#x200B;按钮（在站点控制台中导航启动项内容时）：

  ![站点控制台中的“启动项”选项](/help/sites-cloud/authoring/assets/launches-console-navigate-launch-content.png)

* 或直接访问，例如：
  `https://<host>:<port>/libs/launches/content/launches.html`
