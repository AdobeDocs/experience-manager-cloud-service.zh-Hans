---
title: 在屏幕中将播放器注册为Cloud Service
description: 本页介绍如何在Screens中将播放器注册为Cloud Service。
source-git-commit: b9b27c09b1f4a1799a8c974dfb846295664be998
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 1%

---


# 在屏幕中将播放器注册为Cloud Service {#registering-players-screens-cloud}

为Screens安装并配置播放器作为Cloud Service后，您必须注册播放器。

## 目标 {#objective}

本文档可帮助您了解在Screens服务提供商中注册播放器的情况。 阅读后，您应该能够：

* 了解如何注册播放器
* 如何从Screens服务提供商处完成注册流程

## 注册Screens播放器的步骤 {#register-players}

将播放器作为Cloud Service安装到Screens后，您便可以从Screens服务提供商处注册您的播放器。

请按照以下步骤注册您的播放器：

1. 登录到Screens服务提供商。

1. 从左侧导航面板中导航到位于&#x200B;**播放器管理**&#x200B;下的&#x200B;**注册代码**，然后单击&#x200B;**创建代码**。

   >[!NOTE]
   >如果不存在有效/未过期的代码，请单击创建代码并输入代码的名称，然后根据您的要求选择到期设置。

   ![图像](/help/screens-cloud/assets/player/register-player1.png)

1. 在&#x200B;**创建注册代码**&#x200B;对话框中填充以下字段：

   ![图像](/help/screens-cloud/assets/player/register-player2.png)

   1. **注册代码名称**:注册代码的名称
   1. **注册代码到期**:注册代码的到期日期
   1. **限制使用**:切换按钮以关闭注册代码的使用限制。默认情况下，“限制使用情况”选项处于关闭状态。
   1. **使用限制**:选择使用限制的数字

1. 单击&#x200B;**创建**&#x200B;以创建注册代码。 您将在列表中看到具有注册代码的播放器。

   ![图像](/help/screens-cloud/assets/player/register-player3.png)

1. 单击列&#x200B;**REGISTRATION CODE**&#x200B;下的值，将值复制到剪贴板。

1. 将此值粘贴到AEM Screens播放器管理员UI的&#x200B;**Enter code**&#x200B;选项卡的&#x200B;**Player Registration**&#x200B;字段中，然后单击&#x200B;**Register**。

   ![图像](/help/screens-cloud/assets/player/register-player4.png)


1. 添加代码后，您将看到播放器现在已从播放器的管理员UI中注册。

   ![图像](/help/screens-cloud/assets/player/register-player5.png)

1. 此时，您应该会看到左侧导航面板的&#x200B;**播放器**&#x200B;中显示此播放器。 Screens服务提供程序中显示的代码与播放器代码下管理员UI中的&#x200B;**系统信息**&#x200B;面板相匹配。

   ![图像](/help/screens-cloud/assets/player/register-player6.png)

## 下一步 {#whats-next}

现在，您已经安装并配置了播放器以云模式，您应该继续将Screens作为Cloud Service历程，方法是接下来查看文档[将播放器分配给屏幕中的显示屏，作为Screens服务提供商的Cloud Service](/help/screens-cloud/managing-players-registration/assigning-player-display.md)。