---
title: 为AEM Screens配置时间轴视图
description: 本页介绍如何在Screensas a Cloud Service中配置时间线视图。
exl-id: 53afe1f5-8f0b-4cca-a819-d3e9375cbe37
feature: Administering Screens
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '813'
ht-degree: 11%

---

# 为AEM Screens配置时间轴视图 {#configuring-timelineview-screens}

## 简介 {#introduction}

本节介绍如何为AEM Screens创建时间线视图。

AEM提供了一套功能，允许组织中的多个组人员协作创建、管理和使用渠道。
时间轴位于左栏，可及时描述渠道、位置或任何屏幕文件夹的生命周期，以传达其整个生命周期中发生的情况。 这可以按类型过滤。
除了生命周期日志之外，时间线边栏还提供以下功能。

![将配置文件应用到文件夹](/help/screens-cloud/assets/configure/Screens-timeline1.jpg)

![将配置文件应用到文件夹](/help/screens-cloud/assets/configure/screens-timeline2.jpg)

要创建AEM Screens的时间线视图，请完成以下步骤：

1. 添加评论
1. 保存版本
1. 启动工作流

以下各节详细介绍了这些步骤。

### 添加评论 {#addcomment}

通过时间线提供评论，可让用户创建集中式和历史记录，以便进行有关渠道、位置或屏幕中任何文件夹的讨论。
评论为AEM用户提供了一个很好的整合方式，用于讨论可以保留的方式，从而让其他人了解关键决策。

1. 导航到要为其添加评论的渠道。
1. 选择渠道。
1. 打开&#x200B;**时间线**&#x200B;列。
1. 添加您的评论并按&#x200B;**Enter**。

![添加评论](/help/screens-cloud/assets/configure/screen-timeline3.jpg)

时间轴中的信息会更新以指示已添加评论。

![添加评论](/help/screens-cloud/assets/configure/screens-timeline4.jpg)

### 保存版本 {#saveversion}

版本控制可在特定的时间点创建通道的“快照”。 使用版本控制，您可以执行下列操作：
* 创建渠道版本。
* 将渠道恢复为以前的版本；例如：
   * 撤消对页面所做的更改。
* 将渠道的当前版本与以前的版本进行比较：
   * 以突出显示渠道内容中的差异。


#### 创建新版本 {#createnewversion}

1. 导航到要为其添加评论的渠道。
1. 选择渠道。
1. 打开&#x200B;**时间线**&#x200B;列。
1. 单击页面底部评论字段旁边的按钮（三个圆点）。

   ![添加评论](/help/screens-cloud/assets/configure/screens-timeline5.jpg)

1. 选择&#x200B;**保存为版本**。
1. 输入版本的&#x200B;**标签**&#x200B;和&#x200B;**注释**。

   ![添加评论](/help/screens-cloud/assets/configure/screens-timeline6.jpg)

1. 选择&#x200B;**创建**&#x200B;以确认新版本。时间轴中的信息将更新以指示新版本。

#### 还原到某个版本 {#revertversion}

要将所选页面还原到先前版本，请执行以下操作：

1. 导航到渠道以添加评论。
1. 选择渠道。
1. 打开&#x200B;**时间线**&#x200B;列。
1. 从筛选器下拉列表中选择&#x200B;**显示所有**&#x200B;或&#x200B;**版本**。 将列出所选渠道的渠道版本。
1. 选择要还原到的版本。显示可能的选项：

   ![添加评论](/help/screens-cloud/assets/configure/screens-timeline7.jpg)

1. 选择&#x200B;**还原到此版本**。恢复所选版本，并更新时间线中的信息。

#### 预览版本 {#previewversion}

您可以预览特定版本：

1. 导航到渠道以添加评论。
1. 选择渠道。
1. 打开&#x200B;**时间线**&#x200B;列。
1. 从筛选器下拉列表中选择&#x200B;**显示所有**&#x200B;或&#x200B;**版本**。 将列出所选渠道的渠道版本。
1. 选择要预览的版本。 显示可能的选项：

   ![预览版本](/help/screens-cloud/assets/configure/screens-timeline8.jpg)

1. 选择&#x200B;**预览**。该渠道将显示在新选项卡中。

#### 将版本与当前版本进行比较 {#compareversion}

您可以将特定版本与当前版本进行比较：

1. 导航到要为其添加评论的渠道。
1. 选择渠道。
1. 打开&#x200B;**时间线**&#x200B;列
1. 从筛选器下拉列表中选择&#x200B;**显示所有**&#x200B;或&#x200B;**版本**。 将列出所选渠道的渠道版本。
1. 选择要比较的版本。 显示可能的选项：

   ![比较版本](/help/screens-cloud/assets/configure/screens-timeline9.jpg)

1. 选择&#x200B;**与当前比较**。此时将打开一个弹出窗口以显示差异。

### 启动工作流 {#workflowstart}

在创作时，您可以调用工作流以在渠道上执行操作；也可以应用多个工作流。
在应用工作流时，您需要指定以下信息：

* 要应用的工作流。
* （可选）帮助标识用户收件箱中的工作流实例的标题。
* 工作流有效负载。

#### 启动工作流

1. 导航到要为其添加评论的渠道。
1. 选择渠道。
1. 打开&#x200B;**时间线**&#x200B;列。
1. 单击底部评论字段旁边的按钮（三个点）。

   ![启动工作流](/help/screens-cloud/assets/configure/screens-timeline10.jpg)

1. 选择&#x200B;**启动工作流**。
1. 此时将打开创建工作流向导，以指定工作流详细信息。
1. 从下拉列表中选择&#x200B;**工作流模型**&#x200B;并输入工作流标题。

   ![启动工作流](/help/screens-cloud/assets/configure/screens-timeline11.jpg)

1. 单击&#x200B;**下一步**&#x200B;继续。
1. 在范围步骤中，您可以：
   * **添加内容**&#x200B;以向工作流中添加其他资源。
   * **包括子项**&#x200B;以指定该资源的子项将包括在工作流中。
   * **删除选择**，从工作流中删除该资源。

   ![启动工作流](/help/screens-cloud/assets/configure/screens-timeline12.jpg)

1. 选择&#x200B;**创建**&#x200B;以关闭向导并创建工作流实例。
1. 您可能需要执行一些其他操作来完成工作流，具体取决于所选的工作流模型。

   ![启动工作流](/help/screens-cloud/assets/configure/screens-timeline13.jpg)
