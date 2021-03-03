---
title: 编辑启动项
description: '在为您的一个页面（或一组页面）创建启动项后，您可以编辑页面启动副本中的内容。 '
translation-type: tm+mt
source-git-commit: ba7a8f5027b71ebdee7c84ed35d374fe22645a5a
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 78%

---


# 编辑启动项  {#editing-launches}

## 编辑启动页面 {#editing-launch-pages}

在为一个页面（或一组页面）创建启动项后，您可以编辑页面启动副本中的内容。

1. [从“引用”（“站点”控制台）中访问启动项](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console)以显示可用的操作。
1. 选择&#x200B;**转到页面**&#x200B;以打开要编辑的页面。

编辑页面时，顶部工具栏中将显示一个指示，以及&#x200B;**离开**&#x200B;和&#x200B;**导航**&#x200B;选项：

![从页面编辑器中离开和导航启动项](/help/sites-cloud/authoring/assets/launches-edit-01.png)

>[!NOTE]
>
>不允许您在启动项中移动页面。 尝试此操作将触发警告消息：
>
>* 警告：此页面是启动项的源。 不允许移动页面。


### 编辑基于 Live Copy 的启动页面 {#editing-launch-pages-subject-to-a-live-copy}

如果您的启动项基于[Live Copy](/help/sites-cloud/administering/msm/overview.md)，则您将：

* 请参阅编辑组件（内容和/或属性）时的锁符号（小挂锁）。
* 请参阅&#x200B;**页面属性**&#x200B;中的&#x200B;**Live Copy**&#x200B;选项卡

Live copy用于将源分 *支中的**内容同步到启动分支* （以使启动项与源中所做的更改保持最新）。

您可以按照编辑标准 Live Copy 的方式进行更改；例如：

* 单击已闭合的挂锁将会中断此同步，并允许您对启动项中的内容做出新的更新。解除锁定（打开挂锁）后，您的更改将不会被源分支中的相同位置所做的任何更改所覆盖。
* 特定页面的&#x200B;**暂停**（和&#x200B;**继续**）继承。

有关更多信息，请参阅[更改 Live Copy 内容](/help/sites-cloud/administering/msm/creating-live-copies.md)。

## 比较启动页面与其源页面  {#comparing-a-launch-page-to-its-source-page}

要跟踪您所做的更改，您可以在引用中查看启动项 **** ，并将启动项页面与其源页面进行比较：

1. 在&#x200B;**站点**&#x200B;控制台中，[导航到启动项的源页面并选择一个](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)。
1. 打开&#x200B;**[引用](/help/sites-cloud/authoring/getting-started/basic-handling.md#references)**&#x200B;面板，然后选择&#x200B;**启动项**。
1. 选择您的特定启动项，然后选择&#x200B;**和源比较**：

   ![比较启动项与源](/help/sites-cloud/authoring/assets/launches-compare.png)

1. 此时将并列打开两个页面（启动页面和源页面）。

   有关使用此功能的完整信息，请参阅[页面差异](/help/sites-cloud/authoring/features/page-diff.md)。

## 更改使用的源页面  {#changing-the-source-pages-used}

您可以随时向启动项的源页面范围中添加页面或从中删除页面：

1. 从以下任一位置访问并选择启动项：
   * [启动控制台](/help/sites-cloud/authoring/launches/overview.md#the-launches-console):
      * 选择&#x200B;**编辑**。
   * [“引用”（“站点”控制台）](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console)，以显示可用的操作：
      * 选择&#x200B;**编辑启动项**。
      * 此时将显示源页面。
1. 进行所需的更改，然后使用保存进行 **确认**。

>[!NOTE]
>
>要将页面添加到启动项，这些页面必须位于通用语言根目录下；即，在单个站点内。

## 编辑启动项配置  {#editing-a-launch-configuration}

您可以随时编辑启动项的属性：

1. 从以下任一位置访问并选择启动项：
   * [“启动项”控制台](/help/sites-cloud/authoring/launches/overview.md#the-launches-console)：
      * 选择&#x200B;**属性**。
   * [“引用”（“站点”控制台）](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console)，以显示可用的操作：
      * 选择&#x200B;**编辑属性**。
      * 此时将显示详细信息。
1. 进行所需的更改，然后使用保存进行 **确认**。
   * 有关&#x200B;**启动日期**&#x200B;和&#x200B;**生产就绪**&#x200B;字段的用途和交互的信息，请参阅[启动项 - 事件的顺序](/help/sites-cloud/authoring/launches/overview.md#launches-the-order-of-events)。

## 发现页面的启动状态  {#discovering-the-launch-status-of-a-page}

从“引用”选项卡中选择特定启动项时，将会显示状态（请参阅[“引用”（“站点”控制台）中的启动项](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console)）。

![发现启动状态](/help/sites-cloud/authoring/assets/launches-status.png)
