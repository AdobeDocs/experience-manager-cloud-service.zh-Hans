---
title: 在屏幕中安装和配置播放器as a Cloud Service
description: 本页介绍如何在Screensas a Cloud Service安装和配置播放器。
exl-id: a022738a-c543-4629-a244-f70fa294fe7f
source-git-commit: 3367977496d3edad0f6f1e27e98eac95c791e870
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 1%

---

# 在屏幕中安装和配置播放器as a Cloud Service {#installing-players-screens-cloud}

本节介绍如何安装已注册到内部部署AEM实例的AEM Screens播放器。 此外，您还必须对现有播放器进行工厂重置，然后针对AEM Screens as a Cloud Service注册新播放器。

## 目标 {#objective}

本文档可帮助您了解在注册播放器之前如何设置播放器。 读完之后，您应该能够理解：

* 从何处安装播放器
* 如何将播放器更新为云模式

## 将播放器设置为云模式的步骤 {#cloud-mode-setup}

从下载最新播放器后 [AEM Screens Player下载](https://download.macromedia.com/screens/)，您现在可以将播放器更新为云模式。

请按照以下步骤更新您的播放器：

1. 打开AEM Screens播放器。

   >[!NOTE]
   >您可以选择使用专用硬件设备或在您自己的播放器上使用Web扩展进行测试。

1. 单击 **配置** 选项卡，单击 **到工厂** 按钮 **重置** 选项。

   ![图像](/help/screens-cloud/assets/player/installplayer-2.png)

1. 单击 **确认** 来重置您的播放器。

1. 再次从 **配置** 选项卡，单击 **更改为云模式** 按钮 **切换运行模式** 选项。

   ![图像](/help/screens-cloud/assets/player/installplayer-1.png)

1. 单击 **确认** 切换到云模式时，将会提示取消注册播放器。

## 基本播放监控 {#playback-monitoring}

播放器会根据每个 `ping` 默认为30秒。 根据这些量度，我们可以检测各种边缘情况，如体验卡住、空白屏幕和计划问题。 这样，我们便可以了解设备上的问题并排除其故障，从而加快调查和纠正措施的实施。

AEM Screens播放器中的基本播放监控允许我们：

* 如果播放器正确播放了内容，则进行远程监视。

* 提高对字段中空白屏幕或损坏体验的反应性。

* 降低向最终用户显示损坏的体验的风险。

### 了解属性 {#understand-properties}

每个 `ping`:

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

* 播放器会向服务器报告其自身的播放状态，因此需要活动连接。

* 的 `isContentRendering` 默认情况下，用于检查GPU的属性当前占用的资源太多，无法启用，并且需要从播放器首选项明确选择加入。 建议不要将其与生产中的视频结合使用。

* 此功能仅支持序列渠道，尚不涵盖交互式渠道(SPA)用例。

* 这些量度尚未完全向我们的客户公开，我们正在努力在不久的将来启用类似功能板的报告和警报机制。

## 下一步 {#whats-next}

现在，您已将播放器安装并配置为云模式，接下来应该通过审阅文档来继续您的Screensas a Cloud Service历程， [在屏幕中注册播放器as a Cloud Service](/help/screens-cloud/managing-players-registration/registering-players-screens-cloud.md) 从Screens服务提供商。
