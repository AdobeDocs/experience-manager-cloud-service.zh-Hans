---
title: 在Screens中创建和管理渠道as a Cloud Service
description: 本页介绍如何在Screens中创建和管理渠道as a Cloud Service。
exl-id: 3b0bae7a-4a45-485a-ab04-604510ff6578
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 7%

---

# 在Screens中创建和管理渠道as a Cloud Service {#creating-channels-screens-cloud}

创建AEM Screens项目后，必须创建渠道。
***渠道***、显示内容序列（图像和视频）、网站或单页应用程序。

## 目标 {#objective}

本文档可帮助您在Screens内容提供商中了解如何为AEM Screens项目创建和管理渠道。 阅读后，您应该：

* 了解如何创建Screens内容提供商的渠道
* 管理和编辑渠道中的内容

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


## 下一步 {#whats-next}

现在，您已在项目中设置AEM Screens渠道，因此需要发布渠道。 请参阅 [在屏幕中发布渠道as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/create-content/manage-publish.html?lang=en) 从Screens服务提供商管理您的播放器之前，请执行以下操作：
