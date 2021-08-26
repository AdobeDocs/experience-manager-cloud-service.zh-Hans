---
title: 在屏幕中安装和配置播放器作为Cloud Service
description: 本页介绍如何在Screens中作为Cloud Service安装和配置播放器。
source-git-commit: 1fc06f987bb40d940bbec9c37e6d58c2c1ca9266
workflow-type: tm+mt
source-wordcount: '555'
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

## 基本播放监控 {#playback-monitoring}

播放器会报告各种播放量度，每个量度的默认值为30秒。 `ping`根据这些量度，您可以检测各种边缘情况，如体验卡住、空白屏幕和计划问题。 这样，您便可以了解设备上的问题并排除故障，从而加快调查和纠正措施。

通过AEM Screens播放器中的基本播放监控，您可以：

* 远程监视播放器是否正确播放内容

* 提高对字段中空白屏幕或损坏体验的反应性

* 降低向最终用户显示损坏的体验的风险

### 了解属性 {#understand-properties}

每个`ping`中包含以下属性：

| 属性 | 描述 |
|---|---|
| id {string} | 播放器标识符 |
| activeChannel {string} | 当前正在播放渠道路径；或者，如果没有计划，则为空 |
| activeElements {string} | 以逗号分隔的字符串，所有播放序列渠道中的当前可见元素（多区域布局中存在多个元素） |
| isDefaultContent {boolean} | 如果播放渠道被视为默认或回退渠道（即，具有优先级1且无计划），则为true |
| hasContentChanged {boolean} | 如果内容在过去5分钟内发生更改，则为true；否则为false |
| lastContentChange {string} | 上次内容更改的时间戳 |

>[!NOTE]
>或者，也可以从播放器首选项（启用播放监控）中启用更高级的属性，该属性为：
>|属性|描述|
>|—|—|
>|isContentRendering {boolean}|true(如果GPU能确认它正在播放实际内容（基于像素分析）|

### 限制 {#limitations}

下面列出了基本播放监控的一些限制：

* 由于播放器向服务器报告了自己的播放状态，因此它需要一个活动连接。

* 检查GPU的`isContentRendering`属性当前占用大量资源，默认情况下将启用该属性，并且需要从播放器首选项中明确选择加入。 建议不要将其与视频结合使用。

* 支持序列渠道。

## 下一步 {#whats-next}

现在，您已安装播放器并将其配置为云模式，接下来应继续将Screens作为Cloud Service历程，方法是：接下来查看文档[从Screens服务提供商将Screens中的播放器注册为Cloud Service](/help/screens-cloud/managing-players-registration/registering-players-screens-cloud.md)。