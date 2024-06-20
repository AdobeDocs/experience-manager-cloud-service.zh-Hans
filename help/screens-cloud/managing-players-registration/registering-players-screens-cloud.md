---
title: 在Screensas a Cloud Service注册播放器
description: 本页介绍如何在Screensas a Cloud Service中注册播放器。
exl-id: 1a0d6b22-71b1-4f3c-acaa-82d8d9c0f81a
feature: Developing Screens
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 13%

---

# 在Screensas a Cloud Service注册播放器 {#registering-players-screens-cloud}

安装并配置用于Screensas a Cloud Service的播放器后，必须注册播放器。

## 目标 {#objective}

本文档可帮助您了解如何在Screens服务提供商中注册播放器。 阅读本文档后，您应该能够：

* 了解如何注册播放器
* 如何从Screens Services Provider完成注册流程

## 注册Screens播放器的步骤 {#register-players}

将播放器安装到Screensas a Cloud Service后，即可从Screens服务提供商处注册播放器。

请按照以下步骤注册您的播放器：

1. 登录到Screens服务提供商。

1. 导航到 **注册码** 下 **播放器管理** 从左侧导航面板中单击 **创建代码**.

   >[!NOTE]
   >如果不存在有效的/未过期的代码，请单击“创建代码”并输入代码的名称，然后根据您的要求选择到期设置。

   ![图像](/help/screens-cloud/assets/player/register-player1.png)

1. 在中填充以下字段 **创建注册码** 对话框：

   ![图像](/help/screens-cloud/assets/player/register-player2.png)

   1. **注册码名称**：注册码的名称
   1. **注册码过期**：注册码的到期日期
   1. **限制使用情况**：切换按钮以关闭注册代码的使用限制。 默认情况下，“限制使用情况”选项处于禁用状态。
   1. **使用限制**：选择使用限制的数字

1. 单击 **创建** 以创建注册码。 您可以在列表中看到带有注册码的播放器。

   ![图像](/help/screens-cloud/assets/player/register-player3.png)

1. 单击列下的值 **注册码**  以将该值复制到剪贴板。

1. 将此值粘贴到 **输入代码** 中的字段 **播放器注册** AEM Screens选项卡，然后单击 **注册**.

   ![图像](/help/screens-cloud/assets/player/register-player4.png)


1. 添加该代码后，您可以看到播放器现在已从播放器的管理员UI中注册。

   ![图像](/help/screens-cloud/assets/player/register-player5.png)

1. 您应该会看到此播放器现在显示于 **播放器** 从左侧导航面板中。 Screens Services Provider中显示的代码与 **系统信息** 面板，位于管理员UI中的“播放器代码”下。

   ![图像](/help/screens-cloud/assets/player/register-player6.png)

   >[!IMPORTANT]
   >**使用注册码时的安全最佳实践建议**
   >作为最佳实践，您可以限制注册码的使用。如果注册码已泄露，但注册次数上限为 100，则攻击者最多只能注册这个次数，而不能注册更多。在创建注册码且已注册部分客户播放器后，始终能够更新使用限制。如果客户发现特定注册代码的异常注册活动，他们可以在调查时实时降低限制，如果出现误报，还可以增加数量，而不会影响已注册的播放器。


## 后续内容 {#whats-next}

现在，您已安装播放器并将其配置为云模式，接下来应查看文档以继续Screensas a Cloud Service之旅， [将播放器分配给Screensas a Cloud Service中的显示](/help/screens-cloud/managing-players-registration/assigning-player-display.md) 来自Screens Services Provider。
