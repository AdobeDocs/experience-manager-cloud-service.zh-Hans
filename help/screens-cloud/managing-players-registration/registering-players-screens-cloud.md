---
title: 在屏幕中注册播放器as a Cloud Service
description: 本页介绍如何在Screens中as a Cloud Service注册播放器。
exl-id: 1a0d6b22-71b1-4f3c-acaa-82d8d9c0f81a
source-git-commit: 489cc9963910ba9f94d30906127beb75f9ad37df
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 1%

---

# 在屏幕中注册播放器as a Cloud Service {#registering-players-screens-cloud}

为Screensas a Cloud Service安装和配置播放器后，必须注册播放器。

## 目标 {#objective}

本文档可帮助您了解在Screens服务提供商中注册播放器的情况。 阅读后，您应该能够：

* 了解如何注册播放器
* 如何从Screens服务提供商处完成注册流程

## 注册Screens播放器的步骤 {#register-players}

将播放器安装到Screensas a Cloud Service后，您便可以从Screens服务提供商处注册播放器。

请按照以下步骤注册您的播放器：

1. 登录到Screens服务提供商。

1. 导航到 **注册代码** 在 **播放器管理** 在左侧导航面板中，单击 **创建代码**.

   >[!NOTE]
   >如果不存在有效/未过期的代码，请单击创建代码并输入代码的名称，然后根据您的要求选择到期设置。

   ![图像](/help/screens-cloud/assets/player/register-player1.png)

1. 在 **创建注册代码** 对话框：

   ![图像](/help/screens-cloud/assets/player/register-player2.png)

   1. **注册代码名称**:注册代码的名称
   1. **注册代码到期**:注册代码的到期日期
   1. **限制使用**:切换按钮以关闭注册代码的使用限制。 默认情况下，“限制使用情况”选项处于关闭状态。
   1. **使用限制**:选择使用限制的数字

1. 单击 **创建** 创建注册代码。 您将在列表中看到具有注册代码的播放器。

   ![图像](/help/screens-cloud/assets/player/register-player3.png)

1. 单击列下的值 **注册代码**  将值复制到剪贴板。

1. 将此值粘贴到 **输入代码** 字段 **播放器注册** 选项卡，然后单击AEM Screens播放器的管理员UI **注册**.

   ![图像](/help/screens-cloud/assets/player/register-player4.png)


1. 添加代码后，您将看到播放器现在已从播放器的管理员UI中注册。

   ![图像](/help/screens-cloud/assets/player/register-player5.png)

1. 此时您应会看到此播放器显示在 **播放器** 中。 Screens服务提供商中显示的代码与 **系统信息** 面板。

   ![图像](/help/screens-cloud/assets/player/register-player6.png)

>[!IMPORTANT]
>**使用注册代码时的安全最佳实践建议
>作为最佳实践，您可以限制注册代码的使用。 如果注册代码被攻破，但注册数量限制为100个，则攻击者只能注册到该号码，但注册数量不能超过该号码。 您始终可以在创建注册代码并且已注册客户的某些播放器后更新使用限制。 如果客户发现特定注册代码存在异常注册活动，则他们可以在调查时实时降低该限制，如果是虚警，则可以增加返回数量，而不会影响已注册的播放器。


## 下一步 {#whats-next}

现在，您已将播放器安装并配置为云模式，接下来应该通过审阅文档来继续您的Screensas a Cloud Service历程， [在屏幕中将播放器分配给显示屏as a Cloud Service](/help/screens-cloud/managing-players-registration/assigning-player-display.md) 从Screens服务提供商。
