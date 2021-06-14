---
title: 将渠道作为Cloud Service分配到Screens中的显示屏
description: 本页介绍如何将渠道分配给Screens中的显示屏作为Cloud Service。
hide: true
hidefromtoc: true
index: false
source-git-commit: c65eeaf74ddfd81d37eb7090b84c8bf6f876dc72
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 19%

---


# 将渠道作为Cloud Service{#assign-channel-displays-screens-cloud}分配给Screens中的显示屏

项目设置完成后，必须将渠道分配给显示屏来查看内容。

## 目标 {#objective}

本文档可帮助您了解在显示屏准备就绪并向渠道添加内容并将其发布后，如何将渠道分配给显示屏。 阅读后，您应该能够了解如何从Screens服务提供商将渠道分配给显示屏。

## 前提条件 {#prerequisites}

在执行以下步骤为显示屏分配渠道之前，您必须完成以下学习：

* 创建和管理显示屏
* 创建和管理渠道

## 将渠道分配给显示屏{#assign-channel-to-display}的步骤

请按照以下步骤为显示屏分配渠道：

1. 导航到Screens服务提供商，然后从左侧导航面板中选择&#x200B;**显示**。

1. 单击&#x200B;**将渠道**&#x200B;分配给显示屏。

   ![图像](/help/screens-cloud/assets/display/assignchannel-1.png)

1. 在&#x200B;**分配渠道**&#x200B;对话框中填充以下字段。

   ![图像](/help/screens-cloud/assets/display/assignchannel-2.png)

   1. 从下拉列表中选择渠道名称。
   1. 选择优先级。

      >[!NOTE]
      >优先级用于在多个分配匹配播放条件时对分配进行排序。具有最高值的分配将始终优先于具有较低值的分配。例如，如果有两个渠道 A 和 B。A 的优先级为 1，B 的优先级为 2，则会显示渠道 B，因为它的优先级高于 A。
   1. 从&#x200B;**Activation**&#x200B;中选择开始日期和结束日期。

1. 单击&#x200B;**+添加循环**&#x200B;为渠道添加循环计划。

   ![图像](/help/screens-cloud/assets/create-content/recurrence-1.png)

   >[!NOTE]
   >您可以向渠道中添加多个循环计划。 重复计划引入了分时段功能，利用该功能，您可以设置一个全局计划，并在一天中的特定时间运行多个渠道，然后一次为所有显示屏重复使用该设置。

   您可以设置以下选项：

   * **名称**:定期计划的标题。
   * **重复**:选择计划是运行每日、每周、每月还是每年。
   * **开始**:计划的开始时间。
   * **结束**:计划的结束时间。您可以按时间或持续时间设置此参数。
   * **时间**:计划将在指定时间结束。
   * **持续时间**:计划以小时或分钟为单位在特定时间段内运行。

1. 单击&#x200B;**创建**，此时您将看到已为该显示屏分配了渠道，如下图所示。

   ![图像](/help/screens-cloud/assets/display/assignchannel-3.png)


## 下一步是什么{#whats-next}

现在，您已经将渠道分配给显示屏，接下来应继续将屏幕作为Cloud Service历程，方法是查看文档&#x200B;**安装和配置AEM的Screens播放器作为Cloud Service**。
