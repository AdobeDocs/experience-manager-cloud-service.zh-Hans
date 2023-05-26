---
title: as a Cloud Service在Screens中安装和配置播放器
description: 本页介绍如何在Screensas a Cloud Service安装和配置播放器。
exl-id: a022738a-c543-4629-a244-f70fa294fe7f
source-git-commit: 3367977496d3edad0f6f1e27e98eac95c791e870
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 1%

---

# as a Cloud Service在Screens中安装和配置播放器 {#installing-players-screens-cloud}

本节介绍如何安装注册到内部部署AEM实例的AEM Screens播放器。 此外，您必须在出厂时重置现有播放器，然后针对AEM Screensas a Cloud Service注册新播放器。

## 目标 {#objective}

本文档可帮助您了解如何在注册播放器之前设置播放器。 阅读本文档后，您应该能够了解：

* 播放器的安装位置
* 如何将播放器更新为云模式

## 将播放器设置为云模式的步骤 {#cloud-mode-setup}

从下载最新的播放器后 [AEM Screens播放器下载](https://download.macromedia.com/screens/)，您现在可以将播放器更新为云模式。

请按照以下步骤更新您的播放器：

1. 打开AEM Screens播放器。

   >[!NOTE]
   >您可以选择使用专用硬件设备或您自己的播放器上的Web扩展进行测试。

1. 单击 **配置** 选项卡，然后单击 **到工厂** 按钮位于 **重置** 选项。

   ![图像](/help/screens-cloud/assets/player/installplayer-2.png)

1. 单击 **确认** 重置播放器。

1. 再次从 **配置** 选项卡，然后单击 **更改为云模式** 按钮位于 **切换运行模式** 选项。

   ![图像](/help/screens-cloud/assets/player/installplayer-1.png)

1. 单击 **确认** 在切换到云模式时提示将取消注册播放器。

## 基本回放监控 {#playback-monitoring}

播放器会报告每个播放器中的各种播放量度 `ping` 默认为30秒。 根据这些量度，我们可以检测各种边缘情况，例如卡住体验、空白屏幕和计划问题。 这让我们能够了解并排除设备上的问题，从而加快与您开展的调查和纠正措施。

AEM Screens播放器中的基本播放监视允许我们：

* 远程监控（如果播放器正在正确播放内容）。

* 改善对空白屏幕或现场中断体验的反应性。

* 降低向最终用户显示中断体验的风险。

### 了解属性 {#understand-properties}

每个报表包中包含以下属性 `ping`：

| 属性 | 描述 |
|---|---|
| id {string} | 播放器标识符 |
| activeChannel {string} | 当前播放渠道路径，如果未安排任何项目，则为空 |
| activeElements {string} | 以逗号分隔的字符串，当前所有播放序列渠道中的可见元素（如果是多区域布局，则为多个） |
| isDefaultContent {boolean} | 如果播放渠道被视为默认或备用渠道（即，优先级为1且无计划），则为true |
| hasContentChanged {boolean} | 如果内容在过去5分钟内发生更改，则返回true；否则返回false |
| lastContentChange {string} | 上次内容更改的时间戳 |

>[!NOTE]
>或者，也可以从播放器首选项（启用播放监视）启用更高级的属性，即：
>|属性|描述|
>|—|—|
>|isContentRendering {boolean}|true，如果GPU能够确认它正在播放实际内容（基于像素分析）|

### 限制 {#limitations}

下面列出了基本回放监视的一些限制：

* 播放器会向服务器报告自身的播放状态，因此需要活动连接。

* 此 `isContentRendering` 用于检查GPU的属性当前占用太多资源，默认情况下无法启用，并且需要从播放器首选项中明确选择加入。 建议不要将其与生产环境中的视频结合使用。

* 仅序列渠道支持此功能，尚未涵盖交互式渠道(SPA)用例。

* 这些指标尚未完全暴露给我们的客户，我们正在努力在不久的将来启用类似功能板的报告和警报机制。

## 后续内容 {#whats-next}

现在，您已安装播放器并将其配置为云模式，接下来应查看文档以继续Screensas a Cloud Service之旅， [as a Cloud Service在Screens中注册播放器](/help/screens-cloud/managing-players-registration/registering-players-screens-cloud.md) 来自Screens Services Provider。
