---
title: 在Screens中创建和管理显示as a Cloud Service
description: 本页介绍如何在Screensas a Cloud Service中创建和管理显示。
exl-id: 0f9faa4b-b50e-40f8-a8ed-280f8bd0a9b8
feature: Authoring Screens
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 3%

---

# 在Screens中创建和管理显示as a Cloud Service {#create-displays-screens-cloud}

发布渠道后，现在就可以在Screens服务提供商中创建显示区了。

“显示”是一组虚拟屏幕，通常位于彼此旁边。 对于安装而言，显示通常是永久性的。 此对象内容是作者使用并始终引用的逻辑显示内容，而不是其物理计数器部分。

## 目标 {#objective}

本文档可帮助您了解如何在Screens服务提供商中创建和管理显示。 阅读本文档后，您应：

* 了解如何创建和删除显示区
* 了解如何将您的显示组织到文件夹中

## 创建显示的步骤 {#create-display}

请按照以下步骤从Screens服务提供商中创建显示区：

1. 从AEM Cloud Service实例导航到Screens服务提供商。
1. 从左侧导航面板中选择&#x200B;**显示**，然后单击屏幕右上角的&#x200B;**创建**。

   ![图像](/help/screens-cloud/assets/display/disp-1.png)

1. 从操作栏中选择&#x200B;**显示**。

   ![图像](/help/screens-cloud/assets/display/disp-2.png)

1. 在&#x200B;**显示名称**&#x200B;中输入标题为&#x200B;**LoopingChannelDisplay**，然后单击&#x200B;**创建**。

   ![图像](/help/screens-cloud/assets/display/disp3.png)

1. 标题为&#x200B;**LoopingChannelDisplay**&#x200B;的显示将显示在显示列表中。

   ![图像](/help/screens-cloud/assets/display/disp-4.png)

### 删除显示区 {#deleting-display}

您可以从Screens服务提供商中删除显示区。

选择显示，然后单击面板底部的&#x200B;**删除**，如下图所示。

![图像](/help/screens-cloud/assets/display/disp-5.png)

## 将显示组织到文件夹中的步骤 {#organize-display}

## 如何切换文件夹边栏 {#toggle-rail}

您可以将文件夹边栏从显示所有文件夹切换到特定文件夹：

1. 单击下面高亮显示的按钮以导航到显示清单视图：

   ![图像](/help/screens-cloud/assets/display/display-inventory.png)

1. 将显示文件夹侧边栏。

   ![图像](/help/screens-cloud/assets/display/toggle-rail.png)

1. 选择&#x200B;**隐藏文件夹**&#x200B;以再次将其关闭。

## 如何创建文件夹 {#create-folder}

您可以创建文件夹以更好地组织显示。

1. 定位至显示的库存视图。
1. 确保您当前不在文件夹中，您应会看到以下内容：

   ![图像](/help/screens-cloud/assets/display/verify-view.png)

   注意：应在文件夹侧边栏中选择&#x200B;**所有显示区**，并且痕迹导航应仅显示&#x200B;**显示区**。

1. 单击右上方的“创建”按钮，然后选择&#x200B;**文件夹**&#x200B;选项。

   ![图像](/help/screens-cloud/assets/display/Createfolder.png)

1. 填写新文件夹的标题，然后单击&#x200B;**创建**。

   ![图像](/help/screens-cloud/assets/display/Createfolder2.png)

## 如何创建嵌套文件夹 {#nested-folder}

1. 定位至显示的库存视图。

1. 从文件夹侧边栏中或通过在清单视图中浏览来选择所需的父文件夹。
1. 验证是否选择了所需的父文件夹。

   ![图像](/help/screens-cloud/assets/display/Nestedview.png)

   * 应在文件夹侧边栏中选择文件夹。
   * 痕迹导航应在&#x200B;**Displays**&#x200B;旁显示当前文件夹名称。

1. 单击右上方的&#x200B;**创建**&#x200B;并选择&#x200B;**文件夹**&#x200B;选项。

   ![图像](/help/screens-cloud/assets/display/Createfolder.png)

1. 填写新文件夹的标题，然后单击&#x200B;**创建**。

   ![图像](/help/screens-cloud/assets/display/Createfolder2.png)

## 如何将内容移动到新文件夹 {#move-folder}

您可以将内容移动到新文件夹以更好地组织显示。

1. 定位至显示的库存视图。

1. 从文件夹侧边栏中选择所需的父文件夹，或从库存视图中进行选择。

1. 验证是否选择了所需的父文件夹。

![图像](/help/screens-cloud/assets/display/movetofolder.png)

**注意**：应在文件夹侧边栏中选择该文件夹。 此外，痕迹导航应在&#x200B;**Displays**&#x200B;旁显示当前文件夹名称。

## 如何从文件夹中删除内容 {#delete-folder}

可通过清单视图中的选择操作栏访问所有文件夹操作。

1. 导航到父文件夹或从侧边栏中选择它。

1. 在清单视图中，选择要删除的子文件夹并确保该子文件夹为空。

1. 单击选择操作栏中的&#x200B;**删除**&#x200B;操作。 如果文件夹不为空，将禁用该操作。


## 后续内容 {#whats-next}

现在，您已了解如何为项目创建和管理显示，接下来应该通过查看文档[将渠道分配到Screens中的显示](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/create-content/assigning-channels-to-display.html?lang=zh-Hans)，继续您的Screensas a Cloud Service之旅as a Cloud Service。
