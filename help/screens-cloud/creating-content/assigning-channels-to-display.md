---
title: 将渠道分配给Screensas a Cloud Service中的显示
description: 本页介绍如何在Screensas a Cloud Service中为显示分配渠道。
exl-id: ba001c18-7b05-4ae2-aa7f-9ebb320fedd0
feature: Authoring Screens
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 2%

---

# 将渠道分配给Screensas a Cloud Service中的显示 {#assign-channel-displays-screens-cloud}

项目设置完成后，必须将渠道分配给显示区，以查看内容。

## 目标 {#objective}

本文档可帮助您了解如何在显示准备就绪且已将内容添加到渠道并进行发布后，将渠道分配给显示。 阅读本文档后，您应该能够从Screens服务提供商那里了解如何将渠道分配给显示。

## 先决条件 {#prerequisites}

在执行以下步骤以将渠道分配给显示之前，您必须完成学习：

* 创建和管理显示区
* 创建和管理渠道

## 将渠道分配给显示的步骤 {#assign-channel-to-display}

请按照以下步骤将渠道分配给显示：

1. 导航到Screens服务提供程序并选择 **显示** 从左侧导航面板中。

1. 单击 **分配渠道** 到显示区。

   ![图像](/help/screens-cloud/assets/display/assignchannel-1.png)

1. 从填充以下字段 **分配渠道** 对话框。

   ![图像](/help/screens-cloud/assets/display/assignchannel-2.png)

   1. 从下拉列表中选择渠道名称。
   1. 选择优先级。

      >[!NOTE]
      >优先级用于对分配进行排序，以防多个分配符合播放标准。 值最高的总是优先于较低的值。 例如，如果存在两个渠道A和B。A的优先级为1，B的优先级为2，然后显示信道B，因为它优先级高于A。

   1. 选择开始日期和结束日期 **激活**.

1. 单击 **+添加重复项** 为渠道添加周期性计划。

   ![图像](/help/screens-cloud/assets/create-content/recurrence-1.png)

   >[!NOTE]
   >您可以向渠道添加多个周期性计划。 周期性时间表引入了“日时段分割”，该功能允许您设置全局时间表，并在一天中的特定时间运行多个渠道，同时重用对所有显示设置的全局时间表。

   您可以设置以下选项：

   * **名称**：周期性计划的标题。
   * **重复**：选择计划是每天、每周、每月还是每年运行。
   * **开始**：计划的开始时间。
   * **结束**：计划的结束时间。 您可以按时间或持续时间进行设置。
   * **时间**：计划将在指定时间结束。
   * **持续时间**：计划在特定时间段内运行，以小时或分钟为单位。

1. 单击&#x200B;**创建**。您可以看到已为该显示分配了渠道，如下图所示。

   ![图像](/help/screens-cloud/assets/display/assignchannel-3.png)


## 后续内容 {#whats-next}

现在，您已经将渠道分配给显示，接下来查看文档时应继续您的Screensas a Cloud Service历程 [安装和配置适用于AEM的Screens播放器as a Cloud Service](/help/screens-cloud/managing-players-registration/installing-screens-cloud-player.md).
