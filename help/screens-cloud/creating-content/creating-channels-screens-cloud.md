---
title: 在Screens中创建和管理渠道as a Cloud Service
description: 本页介绍如何在Screens中创建和管理渠道as a Cloud Service。
exl-id: 3b0bae7a-4a45-485a-ab04-604510ff6578
feature: Authoring Screens
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '1103'
ht-degree: 1%

---

# 在Screens中创建和管理渠道as a Cloud Service {#creating-channels-screens-cloud}

创建AEM Screens项目后，必须创建渠道。
***渠道***，显示一系列内容（图像和视频）、网站或单页应用程序。

## 目标 {#objective}

本文档可帮助您了解如何在Screens Content Provider中为AEM Screens项目创建和管理渠道。 阅读本文档后，您应该：

* 了解如何创建通往Screens Content Provider的渠道
* 管理和编辑渠道中的内容
* 在[Screens服务提供商](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/configure-screens-cloud/navigating-to-screens-services-provider.html?lang=zh-Hans)中管理渠道的分配和激活计划

## 在Screens中创建新序列渠道的步骤as a Cloud Service {#create-new-channel}

>[!NOTE]
>**前提条件**
>在开始本指南的这一部分之前，请查看[在Screens中创建和管理项目as a Cloud Service](/help/screens-cloud/creating-content/creating-projects-screens-cloud.md)。

执行以下步骤，在Screens中创建序列渠道as a Cloud Service：

1. 导航到Screens Content Provider。

1. 导航到您的AEM Screens项目，如&#x200B;*FirstDigitalExperience*。

1. 从项目中选择&#x200B;**Channels**&#x200B;文件夹，如&#x200B;**FirstDigitalExperience** —> **Channels**，然后单击操作栏中的&#x200B;**创建**。

   ![channel-create1](/help/screens-cloud/assets/create-content/channel-create1.png)

1. 从&#x200B;**创建**&#x200B;向导中选择模板，如&#x200B;**序列频道**，然后单击&#x200B;**下一步**。

   ![channel-create2](/help/screens-cloud/assets/create-content/channel-create2.png)

   >[!NOTE]
   > 创建渠道时，**创建**&#x200B;向导提供不同类型的模板。 有关更多详细信息，请参阅创建向导中的[可用模板](#available-templates)。

1. 输入序列频道的名称，如&#x200B;**LoopingChannelOne**，然后单击&#x200B;**创建**。

   ![channel-create3](/help/screens-cloud/assets/create-content/channel-create3.png)

   现在，您将在AEM Screens项目的“渠道”文件夹中看到&#x200B;**LoopingChannelOne**。

   创建渠道后，您现在可以向渠道添加内容。 请参阅[将内容添加到渠道](#add-content)，了解如何将资产（图像/视频）添加到渠道。

## 管理渠道 {#managing-channels}

您可以编辑、查看属性和功能板，复制、预览和删除渠道。

导航到项目中的频道，然后选择该频道，如下图所示。 现在，您可以选择相应的选项，例如编辑渠道、查看属性、预览内容、管理出版物或删除操作栏中的渠道。

![channelprop1](/help/screens-cloud/assets/create-content/channelprop1.png)

### 向渠道添加内容 {#add-content}

要在渠道中添加或编辑内容，请执行以下步骤：

1. 选择要编辑的频道，如下图所示。 单击操作栏左上角的&#x200B;**编辑**&#x200B;以打开编辑器。

   ![edit-channel1](/help/screens-cloud/assets/create-content/edit-channel1.png)

1. 编辑器可让您将资产/组件添加到要发布的渠道。

1. 从左侧窗格中拖放资源并将其添加到编辑器。

   ![edit-channel2](/help/screens-cloud/assets/create-content/edit-channel2.png)

   >[!NOTE]
   >单击&#x200B;**预览**以预览渠道的内容。
   >![edit-channelpreview](/help/screens-cloud/assets/create-content/edit-channelpreview.png)

## 创建向导中的可用模板 {#available-templates}

使用&#x200B;**创建**&#x200B;渠道向导时，可以使用以下模板：

| 可用模板 | 描述 |
|--- |--- |
| 渠道文件夹 | 允许您创建用于存储渠道集合的文件夹。 |
| 序列渠道 | 允许您创建一个按顺序播放组件的渠道（在幻灯片放映中逐一播放）。 |
| 左或右L栏分屏渠道 | 允许内容作者在大小合适的区域中查看不同类型的资产。 |

## 为渠道使用默认分配详细信息 {#default-channels}

此功能允许您为渠道定义默认激活计划，并默认将其用于显示的每个分配。 这提供了一种方法，使得繁琐的计划定义不需要重复。

1. 从[此处](https://experience.adobe.com/screens)导航到Screens服务提供商。

### 为渠道创建默认分配详细信息 {#create-default}

1. 导航到要配置的渠道的详细信息页面。
1. 在页面上找到&#x200B;**默认分配详细信息**&#x200B;拼贴。

   ![图像](/help/screens-cloud/assets/display/Assignment1.png)

1. 单击&#x200B;**设置默认详细信息**。
1. 配置默认分配详细信息，包括渠道的优先级、开始和结束日期以及循环模式，然后单击&#x200B;**分配**。

   ![图像](/help/screens-cloud/assets/display/Assignments2.png)

1. 请注意，分配的详细信息显示在&#x200B;**默认分配详细信息**&#x200B;拼贴中：

   ![图像](/help/screens-cloud/assets/display/Assignments3.png)

此图块显示以下信息：
* 渠道在显示中的默认优先级。
* 计划播放渠道时的激活开始和结束日期。
* 周期的综合视图（每小时/每日/每周/每月/每年以及指定给该周期的名称）。

### 在分配给显示区时使用默认分配详细信息 {#default-display}

可以将具有默认分配详细信息的渠道分配给以与常规渠道相同的方式显示，添加了使用默认分配详细信息的选项，而不是每次都手动定义自定义信息。

1. 导航到要为其分配渠道的显示详细信息页面，然后单击&#x200B;**分配渠道**。
或者，在[库存](https://experience.adobe.com/screens/displays)视图中选择所需的显示，然后单击&#x200B;**分配渠道**。
1. 此时将打开渠道分配对话框。

   ![图像](/help/screens-cloud/assets/display/Assignments4.png)

1. 从渠道选择器中选择具有默认分配详细信息的所需渠道。
1. 请注意渠道分配对话框发生了更改，以便您可以选择默认分配详细信息，或选择自定义分配详细信息：

   ![图像](/help/screens-cloud/assets/display/Assignments5.png)

1. 单击&#x200B;**分配**&#x200B;以完成分配，或者，如果您希望使用该特定显示上下文中的某些其他值覆盖默认值，请单击&#x200B;**设置自定义分配详细信息**。

   ![图像](/help/screens-cloud/assets/display/Assignments6.png)

1. 请注意，**分配的渠道**&#x200B;拼贴已更新为新分配：

   ![图像](/help/screens-cloud/assets/display/Assignments7.png)

1. 请注意，根据渠道使用自定义计划（“时钟”图标）还是继承默认详细信息（“世界时钟”图标），渠道将具有不同的图标，单击这些图标将显示计划详细信息。
1. 另请注意，每种类型的可用操作将有所不同。

   ![图像](/help/screens-cloud/assets/display/Assignments8.png)

**注意：**&#x200B;使用默认分配详细信息的渠道分配在显示的上下文中将不可编辑。

* 如果必须将它更改为自定义分配，请先将其删除，然后使用&#x200B;**设置自定义分配详细信息**&#x200B;选项再次添加它。
* 如果必须更改默认分配详细信息的属性，请直接从渠道详细信息页面进行更改。

### 从渠道中删除默认分配详细信息 {#remove-display}

1. 导航到要删除默认分配详细信息的渠道的详细信息页面。
1. 在页面中找到&#x200B;**默认分配详细信息**&#x200B;拼贴
1. 单击&#x200B;**删除默认值**。

   ![图像](/help/screens-cloud/assets/display/Assignments9.png)

1. 将显示确认对话框，详细信息符合以下条件之一：
   **a.**&#x200B;频道未在任何显示区中使用。

   ![图像](/help/screens-cloud/assets/display/Assignments10.png)

**b.**&#x200B;频道用于单个显示。

![图像](/help/screens-cloud/assets/display/Assignment11.png)

**c.**&#x200B;频道已在多个显示区中使用。

![图像](/help/screens-cloud/assets/display/Assignments12.png)

1. 单击&#x200B;*删除*&#x200B;以验证更改。

**注意：**从渠道中删除默认分配详细信息将删除使用该渠道的所有显示器上的匹配分配。
因此，如果没有可播放的替代内容，这可能会导致出现空白屏幕。

## 后续内容 {#whats-next}

现在，您已在项目中设置AEM Screens渠道，接下来需要发布渠道。 在从Screens服务提供商管理播放器之前，请参阅[在Screensas a Cloud Service中发布渠道](manage-publish.md)。
