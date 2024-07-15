---
title: 在Screens中注册播放器as a Cloud Service
description: 本页介绍如何在Screensas a Cloud Service中注册播放器。
exl-id: 1a0d6b22-71b1-4f3c-acaa-82d8d9c0f81a
feature: Developing Screens
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 13%

---

# 在Screens中注册播放器as a Cloud Service {#registering-players-screens-cloud}

安装并配置Screensas a Cloud Service的播放器后，必须注册这些播放器。

## 目标 {#objective}

本文档可帮助您了解如何在Screens服务提供商中注册播放器。 阅读本文档后，您应该能够：

* 了解如何注册播放器
* 如何从Screens服务提供商处完成注册流程

## 注册Screens播放器的步骤 {#register-players}

将播放器安装到Screensas a Cloud Service后，即可从Screens服务提供商处注册播放器。

请按照以下步骤注册您的播放器：

1. 登录到Screens服务提供商。

1. 从左侧导航面板导航到&#x200B;**播放器管理**&#x200B;下的&#x200B;**注册码**，然后单击&#x200B;**创建代码**。

   >[!NOTE]
   >如果不存在有效的/未过期的代码，请单击“创建代码”并输入代码的名称，然后根据您的要求选择到期设置。

   ![图像](/help/screens-cloud/assets/player/register-player1.png)

1. 在&#x200B;**创建注册码**&#x200B;对话框中填充以下字段：

   ![图像](/help/screens-cloud/assets/player/register-player2.png)

   1. **注册码名称**：您的注册码名称
   1. **注册码过期**：您的注册码的过期日期
   1. **限制使用**：切换按钮以关闭注册码的使用限制。 默认情况下，“限制使用情况”选项处于禁用状态。
   1. **使用限制**：选择使用限制的数字

1. 单击&#x200B;**创建**&#x200B;以创建注册码。 您可以在列表中看到带有注册码的播放器。

   ![图像](/help/screens-cloud/assets/player/register-player3.png)

1. 单击&#x200B;**注册码**&#x200B;列下的值以将该值复制到剪贴板。

1. 从AEM Screens播放器的管理员UI将此值粘贴到&#x200B;**播放器注册**&#x200B;选项卡的&#x200B;**输入代码**&#x200B;字段中，然后单击&#x200B;**注册**。

   ![图像](/help/screens-cloud/assets/player/register-player4.png)


1. 添加该代码后，您可以看到播放器现在已从播放器的管理员UI中注册。

   ![图像](/help/screens-cloud/assets/player/register-player5.png)

1. 您应该会看到此播放器现在显示在左侧导航面板的&#x200B;**播放器**&#x200B;中。 Screens Services Provider中显示的代码与播放器代码下管理UI中的&#x200B;**系统信息**&#x200B;面板匹配。

   ![图像](/help/screens-cloud/assets/player/register-player6.png)

   >[!IMPORTANT]
   >使用注册码时&#x200B;**安全最佳实践建议**
   >作为最佳实践，您可以限制注册码的使用。如果注册码已泄露，但注册次数上限为 100，则攻击者最多只能注册这个次数，而不能注册更多。在创建注册码且已注册部分客户播放器后，始终能够更新使用限制。如果客户发现特定注册代码的异常注册活动，他们可以在调查时实时降低限制，如果出现误报，还可以增加数量，而不会影响已注册的播放器。


## 后续内容 {#whats-next}

现在，您已安装播放器并将其配置为云模式，接下来应通过查看文档[将播放器分配给Screens服务提供商的Screensas a Cloud Service](/help/screens-cloud/managing-players-registration/assigning-player-display.md)中的显示来继续您的Screensas a Cloud Service之旅。
