---
title: 在Screens中创建和管理渠道as a Cloud Service
description: 本页介绍如何在Screens中创建和管理渠道as a Cloud Service。
exl-id: 3b0bae7a-4a45-485a-ab04-604510ff6578
source-git-commit: afcee8019c9b59f3eb1fdcabd569272eeea76dab
workflow-type: tm+mt
source-wordcount: '1116'
ht-degree: 4%

---

# 在Screens中创建和管理渠道as a Cloud Service {#creating-channels-screens-cloud}

创建AEM Screens项目后，必须创建渠道。
***渠道***、显示内容序列（图像和视频）、网站或单页应用程序。

## 目标 {#objective}

本文档可帮助您在Screens内容提供商中了解如何为AEM Screens项目创建和管理渠道。 阅读后，您应该：

* 了解如何创建Screens内容提供商的渠道
* 管理和编辑渠道中的内容
* 渠道的激活计划

## 在Screens中创建新序列渠道的步骤as a Cloud Service {#create-new-channel}

>[!NOTE]
>**前提条件**
>在开始本指南的本节之前，请查阅 [在Screens中创建和管理项目as a Cloud Service](/help/screens-cloud/creating-content/creating-projects-screens-cloud.md).

请按照以下步骤在Screens中as a Cloud Service创建新序列渠道：

1. 导航到Screens内容提供商。

1. 导航到您的AEM Screens项目，例如 *FirstDigitalExperience*.

1. 选择 **渠道** 文件夹，例如 **FirstDigitalExperience** —> **渠道** 单击 **创建** 中。

   ![](/help/screens-cloud/assets/create-content/channel-create1.png)

1. 选择模板，例如 **序列渠道** 从 **创建** 向导，单击 **下一个**.

   ![](/help/screens-cloud/assets/create-content/channel-create2.png)
   >[!NOTE]
   > 的 **创建** 向导在创建渠道时提供不同类型的模板。 请参阅章节 [可用模板](#available-templates) ，以了解更多详细信息。

1. 输入序列渠道的名称，例如 **LoopingChannelOne** 单击 **创建**.

   ![](/help/screens-cloud/assets/create-content/channel-create3.png)

   您现在将看到 **LoopingChannelOne** 的渠道文件夹中。AEM Screens项目。

   创建渠道后，您现在可以向渠道中添加内容。 请参阅 [向渠道添加内容](#add-content) 了解如何将资产（图像/视频）添加到渠道。

## 管理渠道 {#managing-channels}

您可以编辑、复制、预览和删除渠道，以及查看渠道属性和功能板。

从您的项目导航到渠道，然后选择渠道，如下图所示。 现在，您可以从操作栏中选择以下选项：编辑渠道、查看属性、预览内容、管理发布或删除渠道。

![](/help/screens-cloud/assets/create-content/channelprop1.png)

### 向渠道添加内容 {#add-content}

要在渠道中添加或编辑内容，请按照以下步骤操作：

1. 选择要编辑的渠道，如下图所示。 单击 **编辑** 从操作栏的左上角打开编辑器。

   ![](/help/screens-cloud/assets/create-content/edit-channel1.png)

1. 利用编辑器，可向要发布的渠道中添加资产/组件。

1. 从左侧窗格拖放资产，并将其添加到编辑器中。

   ![](/help/screens-cloud/assets/create-content/edit-channel2.png)

   >[!NOTE]
   >单击 **预览** 以预览渠道的内容。
   >![](/help/screens-cloud/assets/create-content/edit-channelpreview.png)

## 创建向导中的可用模板 {#available-templates}

使用 **创建** 渠道向导：

| 可用模板 | 描述 |
|--- |--- |
| 渠道文件夹 | 允许创建一个文件夹来存储渠道的集合。 |
| 序列渠道 | 允许创建按顺序（在幻灯片放映中逐个播放组件）播放组件的渠道。 |
| 左或右L条分屏渠道 | 允许内容作者在大小适当的区域中查看不同类型的资产。 |

## 为渠道使用默认分配详细信息 {#default-channels}

此功能允许您为渠道定义默认激活计划，并在默认情况下将其用于显示屏的每个分配。 这提供了一种方法，以便不必重复繁琐的计划定义。

### 为渠道创建默认分配详细信息 {#create-default}

1. 导航到要配置的渠道的详细信息页面。
1. 找到 **默认分配详细信息** 图块。

   ![图像](/help/screens-cloud/assets/display/Assignment1.png)

1. 单击 **设置默认详细信息**.
1. 配置渠道的默认分配详细信息（包括优先级、开始和结束日期以及重复模式），然后单击 **分配**.

   ![图像](/help/screens-cloud/assets/display/Assignments2.png)

1. 请注意，分配的详细信息显示在 **默认分配详细信息** 拼贴：

   ![图像](/help/screens-cloud/assets/display/Assignments3.png)

此拼贴显示以下信息：
* 显示屏中渠道的默认优先级。
* 计划播放渠道时的激活开始和结束日期。
* 循环的综合视图（每小时/每日/每周/每月/每年，以及给定该循环的名称）。

### 在分配到显示屏时使用默认分配详细信息 {#default-display}

可以将具有默认分配详细信息的渠道分配到的显示方式与常规渠道相同，添加了一个选项来利用默认分配详细信息，而不是每次手动定义自定义渠道。

1. 导航到要将渠道分配到的显示详细信息页面，然后单击 **分配渠道**.
或者，在库存视图中选择所需的显示，然后单击 **分配渠道**.
1. 随即会打开渠道分配对话框。

   ![图像](/help/screens-cloud/assets/display/Assignments4.png)

1. 从渠道选取器中选择具有默认分配详细信息的所需渠道。
1. 请注意，渠道分配对话框发生了更改，允许您选择默认分配详细信息或选择自定义分配详细信息：

   ![图像](/help/screens-cloud/assets/display/Assignments5.png)

1. 单击 **分配** 完成分配，或单击 **设置自定义分配详细信息** 如果您希望在该特定显示的上下文中使用其他一些值覆盖默认值。

   ![图像](/help/screens-cloud/assets/display/Assignments6.png)

1. 请注意 **分配的渠道** 磁贴已更新为新分配：

   ![图像](/help/screens-cloud/assets/display/Assignments7.png)

1. 请注意，渠道将具有不同的图标，具体取决于它们是使用自定义计划（时钟图标）还是继承默认详细信息（世界时钟图标），单击这些渠道将显示计划详细信息。
1. 另请注意，每种类型的可用操作都会有所不同。

   ![图像](/help/screens-cloud/assets/display/Assignments8.png)

**注意：** 利用默认分配详细信息的渠道分配在显示内容中将不可编辑。

* 如果您需要将其更改为自定义分配，则必须先将其删除，然后使用 **设置自定义分配详细信息** 选项。
* 如果您需要更改默认分配详细信息的属性，则必须直接从渠道详细信息页面执行此操作。

### 从渠道中删除默认分配详细信息 {#remove-display}

1. 导航到要删除默认分配详细信息的渠道的详细信息页面。
1. 找到 **默认分配详细信息** 页面中的拼贴
1. 单击 **删除默认**.

   ![图像](/help/screens-cloud/assets/display/Assignments9.png)

1. 将显示确认对话框，其详细信息将与以下条件之一匹配：
   **a.** 渠道不用于任何显示屏。

   ![图像](/help/screens-cloud/assets/display/Assignments10.png)

**b.** 渠道用于单个显示屏。

![图像](/help/screens-cloud/assets/display/Assignment11.png)

**c.** 渠道用于多个显示屏。

![图像](/help/screens-cloud/assets/display/Assignments12.png)

1. 单击 *删除* 以验证更改。

**注意：** 从渠道中删除默认分配详细信息将删除使用该渠道的所有显示屏上的匹配分配。
因此，如果这些显示屏上没有要播放的替代内容，则这可能会导致出现空白屏幕。

## 下一步 {#whats-next}

现在，您已在项目中设置AEM Screens渠道，因此需要发布渠道。 请参阅 [在屏幕中发布渠道as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/create-content/manage-publish.html?lang=en) 从Screens服务提供商管理您的播放器之前，请执行以下操作：
