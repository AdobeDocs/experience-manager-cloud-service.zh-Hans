---
title: 在Screens中创建和管理渠道作为Cloud Service
description: 本页介绍如何在Screens中作为Cloud Service创建和管理渠道。
hide: true
hidefromtoc: true
index: false
source-git-commit: ece3fae8b65b4dbdc38e63a211a3f55f4eb91333
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 7%

---


# 在Screens中创建和管理渠道作为Cloud Service{#creating-channels-screens-cloud}

创建AEM Screens项目后，必须创建渠道。
***渠道***、显示一系列内容（图像和视频）、网站或单页应用程序。

## 目标 {#objective}

本文档可帮助您在Screens内容提供商中了解如何为AEM Screens项目创建和管理渠道。 阅读后，您应该：

* 了解如何创建Screens内容提供商的渠道。
* 能够在AEM Screens项目中管理渠道（范围）。

## 在Screens中作为Cloud Service创建新序列渠道的步骤{#create-new-channel}

>[!NOTE]
>**前提条件**
>在开始本指南的此部分之前，请查看[在Screens中作为Cloud Service创建和管理项目](/help/screens-cloud/creating-content/creating-projects-screens-cloud.md)。

请按照以下步骤在Screens中作为Cloud Service创建新序列渠道：

1. 导航到Screens内容提供商。

1. 导航到您的AEM Screens项目，如&#x200B;*FirstDigitalExperience*。

1. 从项目中选择&#x200B;**渠道**&#x200B;文件夹，如&#x200B;**FirstDigitalExperience** —> **渠道**，然后单击操作栏中的&#x200B;**创建**。

   ![](/help/screens-cloud/assets/create-content/channel-create1.png)

1. 从&#x200B;**创建**&#x200B;向导中选择模板，例如&#x200B;**序列渠道**，然后单击&#x200B;**下一步**。

   ![](/help/screens-cloud/assets/create-content/channel-create2.png)
   >[!NOTE]
   > 创建渠道时， **创建**&#x200B;向导会提供不同类型的模板。 有关更多详细信息，请参阅创建向导中的可用模板一节。

1. 输入序列渠道的名称，如&#x200B;**LoopingChannelOne** ，然后单击&#x200B;**Create**。

   ![](/help/screens-cloud/assets/create-content/channel-create3.png)

   现在，您将在AEM Screens项目的“渠道”文件夹中看到&#x200B;**LoopingChannelOne**。

1. 创建渠道后，您现在可以向渠道中添加内容。 请参阅[向渠道添加内容](#add-content) ，了解如何向渠道添加资产（图像/视频）。

## 管理渠道{#managing-channels}

您可以编辑、复制、预览和删除渠道，以及查看渠道属性和功能板。

从您的项目导航到渠道，然后选择渠道，如下图所示。 现在，您可以从操作栏中选择以下选项：编辑渠道、查看属性、预览内容、管理发布或删除渠道。

![](/help/screens-cloud/assets/create-content/channelprop1.png)

### 向渠道{#add-content}添加内容

要在渠道中添加或编辑内容，请按照以下步骤操作：

1. 选择要编辑的渠道，如下图所示。 单击操作栏左上角的&#x200B;**编辑**&#x200B;以打开编辑器。

   ![](/help/screens-cloud/assets/create-content/edit-channel1.png)

1. 利用编辑器，可向要发布的渠道中添加资产/组件。

1. 从左侧窗格拖放资产，并将其添加到编辑器中。

   ![](/help/screens-cloud/assets/create-content/edit-channel2.png)

   >[!NOTE]
   >单击&#x200B;**预览**以预览渠道的内容。
   >![](/help/screens-cloud/assets/create-content/edit-channelpreview.png)

## 创建向导{#available-templates}中的可用模板

使用&#x200B;**创建**&#x200B;渠道向导时，可以使用以下模板，例如：

| 可用模板 | 描述 |
|--- |--- |
| 渠道文件夹 | 允许创建一个文件夹来存储渠道的集合。 |
| 序列渠道 | 允许创建按顺序（在幻灯片放映中逐个播放组件）播放组件的渠道。 |
| 左或右L条分屏渠道 | 允许内容作者在大小适当的区域中查看不同类型的资产。 |


## 下一步是什么{#whats-next}

现在，您已在项目中设置AEM Screens渠道，因此需要发布渠道。 在从Screens服务提供商管理您的播放器之前，请参阅[以Cloud Service身份发布Screens中的渠道](/help/screens-cloud/creating-content/manage-publish.md)。