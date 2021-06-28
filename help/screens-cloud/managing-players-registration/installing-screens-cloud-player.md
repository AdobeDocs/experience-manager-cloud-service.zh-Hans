---
title: 在屏幕中安装和配置播放器作为Cloud Service
description: 本页介绍如何在Screens中作为Cloud Service安装和配置播放器。
source-git-commit: b9b27c09b1f4a1799a8c974dfb846295664be998
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 1%

---


# 在屏幕中安装和配置播放器作为Cloud Service {#installing-players-screens-cloud}

本节介绍如何安装已注册到内部部署AEM实例的AEM Screens播放器。 此外，您还必须对现有播放器进行工厂重置，然后针对AEM Screens注册新播放器作为Cloud Service。

## 目标 {#objective}

本文档可帮助您了解在注册播放器之前如何设置播放器。 读完之后，您应该能够理解：

* 从何处安装播放器
* 如何将播放器更新为云模式

## 将播放器设置为云模式的步骤 {#cloud-mode-setup}

从[AEM Screens Player Downloads](https://download.macromedia.com/screens/)下载最新播放器后，您现在可以将播放器更新为云模式。

请按照以下步骤更新您的播放器：

1. 打开AEM Screens播放器。

   >[!NOTE]
   >您可以选择使用专用硬件设备或在您自己的播放器上使用Web扩展进行测试。

1. 单击&#x200B;**配置**&#x200B;选项卡，然后单击&#x200B;**重置**&#x200B;选项下的&#x200B;**工厂**&#x200B;按钮。

   ![图像](/help/screens-cloud/assets/player/installplayer-2.png)

1. 单击&#x200B;**Confirm**&#x200B;以重置播放器。

1. 再次从&#x200B;**配置**&#x200B;选项卡中，单击&#x200B;**切换运行模式**&#x200B;选项下的&#x200B;**更改为云模式**&#x200B;按钮。

   ![图像](/help/screens-cloud/assets/player/installplayer-1.png)

1. 单击&#x200B;**Confirm**，在切换到云模式时，会提示取消注册播放器。

## 下一步 {#whats-next}

现在，您已安装播放器并将其配置为云模式，接下来应继续将Screens作为Cloud Service历程，方法是：接下来查看文档[从Screens服务提供商将Screens中的播放器注册为Cloud Service](/help/screens-cloud/managing-players-registration/registering-players-screens-cloud.md)。