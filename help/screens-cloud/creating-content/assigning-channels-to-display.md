---
title: 将渠道分配给屏幕中的显示屏as a Cloud Service
description: 本页介绍如何在Screens中将渠道分配给显示屏as a Cloud Service。
exl-id: ba001c18-7b05-4ae2-aa7f-9ebb320fedd0
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 19%

---

# 将渠道分配给屏幕中的显示屏as a Cloud Service {#assign-channel-displays-screens-cloud}

项目设置完成后，必须将渠道分配给显示屏来查看内容。

## 目标 {#objective}

本文档可帮助您了解在显示屏准备就绪并向渠道添加内容并将其发布后，如何将渠道分配给显示屏。 阅读后，您应该能够了解如何从Screens服务提供商将渠道分配给显示屏。

## 前提条件 {#prerequisites}

在执行以下步骤为显示屏分配渠道之前，您必须完成以下学习：

* 创建和管理显示屏
* 创建和管理渠道

## 将渠道分配给显示屏的步骤 {#assign-channel-to-display}

请按照以下步骤为显示屏分配渠道：

1. 导航到Screens服务提供商，然后选择 **显示** 中。

1. 单击 **分配渠道** 显示。

   ![图像](/help/screens-cloud/assets/display/assignchannel-1.png)

1. 从以下字段填充 **分配渠道** 对话框。

   ![图像](/help/screens-cloud/assets/display/assignchannel-2.png)

   1. 从下拉列表中选择渠道名称。
   1. 选择优先级。

      >[!NOTE]
      >优先级用于在多个分配匹配播放条件时对分配进行排序。具有最高值的分配将始终优先于具有较低值的分配。例如，如果有两个渠道 A 和 B。A 的优先级为 1，B 的优先级为 2，则会显示渠道 B，因为它的优先级高于 A。
   1. 选择开始日期和结束日期 **激活**.

1. 单击 **+添加循环** 添加渠道的重复计划。

   ![图像](/help/screens-cloud/assets/create-content/recurrence-1.png)

   >[!NOTE]
   >您可以向渠道中添加多个循环计划。 重复计划引入了分时段功能，利用该功能，您可以设置一个全局计划，并在一天中的特定时间运行多个渠道，然后一次为所有显示屏重复使用该设置。

   您可以设置以下选项：

   * **名称**:定期计划的标题。
   * **重复**:选择计划是运行每日、每周、每月还是每年。
   * **开始**:计划的开始时间。
   * **结束**:计划的结束时间。 您可以按时间或持续时间设置此参数。
   * **时间**:计划将在指定时间结束。
   * **持续时间**:计划以小时或分钟为单位在特定时间段内运行。

1. 单击 **创建** 现在，您将看到已为该显示屏分配了渠道，如下图所示。

   ![图像](/help/screens-cloud/assets/display/assignchannel-3.png)


## 下一步 {#whats-next}

现在，您已将渠道分配给显示屏，接下来应该审阅文档以继续您的Screensas a Cloud Service历程 [为AEM Screensas a Cloud Service安装和配置Screens播放器](/help/screens-cloud/managing-players-registration/installing-screens-cloud-player.md).
