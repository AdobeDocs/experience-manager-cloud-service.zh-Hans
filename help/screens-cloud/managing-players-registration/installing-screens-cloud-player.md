---
title: 在Screens中安装和配置播放器as a Cloud Service
description: 本页介绍如何在Screensas a Cloud Service中安装和配置播放器。
exl-id: a022738a-c543-4629-a244-f70fa294fe7f
feature: Developing Screens
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 1%

---

# 在Screens中安装和配置播放器as a Cloud Service {#installing-players-screens-cloud}

本节介绍如何安装注册到内部部署AEM实例的AEM Screens播放器。 此外，您必须在工厂重置现有播放器，然后针对AEM Screens as a Cloud Service注册新播放器。

## 目标 {#objective}

本文档可帮助您了解如何在注册播放器之前设置播放器。 阅读本文档后，您应该能够了解以下内容：

* 播放器的安装位置
* 如何将播放器更新为云模式

## 将播放器设置为云模式的步骤 {#cloud-mode-setup}

从[AEM Screens播放器下载](https://download.macromedia.com/screens/)下载最新的播放器后，您现在就可以将播放器更新为云模式了。

请按照以下步骤更新您的播放器：

1. 打开AEM Screens播放器。

   >[!NOTE]
   >您可以选择使用专用硬件设备或您自己的播放器上的Web扩展进行测试。

1. 单击“**配置**”选项卡，然后单击“**重置**”选项下的“**到工厂**”按钮。

   ![图像](/help/screens-cloud/assets/player/installplayer-2.png)

1. 单击&#x200B;**确认**&#x200B;以重置播放器。

1. 再次从&#x200B;**配置**&#x200B;选项卡单击&#x200B;**切换运行模式**&#x200B;选项下的&#x200B;**更改为云模式**&#x200B;按钮。

   ![图像](/help/screens-cloud/assets/player/installplayer-1.png)

1. 单击&#x200B;**确认**&#x200B;在切换到云模式时提示取消注册播放器。

## 基本回放监控 {#playback-monitoring}

播放器报告每个`ping`的各种回放指标，其默认值为30秒。 根据这些指标，Adobe可以检测各种边缘情况，例如卡住体验、空白屏幕和计划问题。 此检测使我们能够了解设备问题并对其进行故障排除，因此可加快为您提供调查及纠正措施。

AEM Screens播放器中的基本回放监控允许我们：

* 远程监控（如果播放器正在正确播放内容）。

* 改善对空白屏幕或现场中断体验的反应性。

* 减少向用户显示中断体验的风险。

### 了解属性 {#understand-properties}

每个`ping`中包含以下属性：

| 属性 | 描述 |
|---|---|
| ID {string} | 播放器标识符 |
| activeChannel {string} | 当前播放渠道路径，如果未计划任何内容，则返回null |
| activeElements {string} | 以逗号分隔的字符串，当前所有播放序列渠道中的可见元素（如果有多区域布局，则为多个） |
| isDefaultContent {boolean} | 如果播放频道被视为默认或备用频道（即，优先级为1且无计划），则返回true |
| hasContentChanged {boolean} | 如果内容在过去5分钟内发生更改，则返回true；否则返回false |
| lastContentChange {string} | 上次内容更改的时间戳 |

>[!NOTE]
>或者，您也可以从播放器首选项启用更高级的属性（启用回放监控）：
>|属性|描述|
>|—|—|
>|isContentRendering {boolean}|如果GPU可以确认它正在播放实际内容（基于像素分析），则为true|

### 限制 {#limitations}

下面列出了基本回放监视的一些限制：

* 播放器会向服务器报告自身的播放状态，因此需要活动连接。

* 用于检查GPU的`isContentRendering`属性过度占用资源，默认情况下将启用，并且需要从播放器首选项中明确选择加入。 建议不要将其用于生产中的视频。

* 仅序列渠道支持此功能，并且尚不涵盖交互式渠道(SPA)用例。

* 这些量度尚未完全向客户公开；Adobe正在努力尽快启用类似功能板的报告和警报机制。

## 后续内容 {#whats-next}

现在您已安装播放器并将其配置为云模式，请继续您的Screensas a Cloud Service之旅。 请参阅[在Screensas a Cloud Service中注册播放器](/help/screens-cloud/managing-players-registration/registering-players-screens-cloud.md)(来自Screens服务提供商)。
