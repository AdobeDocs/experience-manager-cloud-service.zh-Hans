---
title: 为AEM Screens配置时间轴视图
description: 本页介绍如何在Screensas a Cloud Service中配置时间线视图。
source-git-commit: eb71ea3a1a739b08fb3154a5f41a0706bd81488c
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
1. 打开 **时间线** 列。
1. 添加您的评论并按 **输入**.

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
1. 打开 **时间线** 列。
1. 单击页面底部评论字段旁边的按钮（三个圆点）。

   ![添加评论](/help/screens-cloud/assets/configure/screens-timeline5.jpg)

1. 选择&#x200B;**保存为版本**。
1. 输入 **标签** 和 **注释** 用于版本。

   ![添加评论](/help/screens-cloud/assets/configure/screens-timeline6.jpg)

1. 通过选择确认新版本 **创建**&#x200B;时间轴中的信息会更新以指示新版本。

#### 还原到某个版本 {#revertversion}

要将所选页面还原到先前版本，请执行以下操作：

1. 导航到渠道以添加评论。
1. 选择渠道。
1. 打开 **时间线** 列。
1. 选择 **显示全部** 或 **版本** 过滤器下拉列表中的值。 将列出所选渠道的渠道版本。
1. 选择要还原到的版本。显示可能的选项：

   ![添加评论](/help/screens-cloud/assets/configure/screens-timeline7.jpg)

1. 选择&#x200B;**还原到此版本**。恢复所选版本，并更新时间线中的信息。

#### 预览版本 {#previewversion}

您可以预览特定版本：

1. 导航到渠道以添加评论。
1. 选择渠道。
1. 打开 **时间线** 列。
1. 选择 **显示全部** 或 **版本** 过滤器下拉列表中的值。 将列出所选渠道的渠道版本。
1. 选择要预览的版本。 显示可能的选项：

   ![预览版本](/help/screens-cloud/assets/configure/screens-timeline8.jpg)

1. 选择&#x200B;**预览**。该渠道将显示在新选项卡中。

#### 将版本与当前版本进行比较 {#compareversion}

您可以将特定版本与当前版本进行比较：

1. 导航到要为其添加评论的渠道。
1. 选择渠道。
1. 打开 **时间线** 列
1. 选择 **显示全部** 或 **版本** 过滤器下拉列表中的值。 将列出所选渠道的渠道版本。
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
1. 打开 **时间线** 列。
1. 单击底部评论字段旁边的按钮（三个点）。

   ![启动工作流](/help/screens-cloud/assets/configure/screens-timeline10.jpg)

1. 选择 **启动工作流**.
1. 此时将打开创建工作流向导，以指定工作流详细信息。
1. 选择 **工作流模型** 从下拉列表中输入“工作流”标题。

   ![启动工作流](/help/screens-cloud/assets/configure/screens-timeline11.jpg)

1. 单击 **下一个**.
1. 在范围步骤中，您可以：
   * **添加内容** 向工作流添加其他资源。
   * **包括子项** 以指定将该资源的子项包含在工作流中。
   * **删除选择**，从工作流中删除该资源。

   ![启动工作流](/help/screens-cloud/assets/configure/screens-timeline12.jpg)

1. 选择 **创建** 以关闭向导并创建工作流实例。
1. 您可能需要执行一些其他操作来完成工作流，具体取决于所选的工作流模型。

   ![启动工作流](/help/screens-cloud/assets/configure/screens-timeline13.jpg)
