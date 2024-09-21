---
title: 在Cloud Manager中管理Edge Delivery站点
description: 了解如何将CDN配置添加到Edge Delivery站点或删除Edge Delivery站点。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f684a52ca3b51d1aa4412122f7ad28dde3e2672f
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---

# 在Cloud Manager中管理Edge Delivery站点 {#manage-edge-delivery-sites}

了解如何通过将CDN配置添加到现有站点来管理Cloud Manager中的Edge Delivery站点。 或者，删除Edge Delivery站点。

## 将CDN配置添加到现有Edge Delivery站点 {#add-cdn-to-edge-delivery-site}

请参阅[添加CDN配置](/help/implementing/cloud-manager/cdn-configurations/add-cdn-config.md)。

## 重命名Edge Delivery站点(#rename-edge-delivery-site)

在AdobeCloud Manager中，出于以下几种原因，您可能想要重命名Edge Delivery站点：

* **清晰明了，井然有序**：更好地描述站点的目的或其相关环境（例如，生产、暂存）。
* **避免混淆**：如果正在使用多个网站，则重命名有助于轻松区分它们，减少将配置或更新应用到错误网站的机会。
* **标准化**：遵循一致的命名约定，该约定与贵组织的准则保持一致，以便更轻松地管理和审核。

**要重命名Edge Delivery网站：**

1. 在[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)登录Cloud Manager并选择适当的程序。
1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台上，选择已配置Edge Delivery Services的程序，并从中添加Edge Delivery站点。
1. 执行以下任一操作：

   * 从&#x200B;**项目概述**&#x200B;页面，单击&#x200B;**Edge Delivery**选项卡。 在Edge Delivery站点表中，单击要重命名其站点的行末尾的省略号。
单击**重命名**。
   * 在页面的左上角，单击汉堡图标以显示左侧导航菜单。 在&#x200B;**服务**&#x200B;标题下，单击&#x200B;**Edge Delivery站点**。
在Edge Delivery站点表中，单击要重命名其站点的行末尾的省略号。 单击**重命名**。

1. 在&#x200B;**编辑Edge Delivery站点**&#x200B;对话框的&#x200B;**站点名称**&#x200B;文本字段中，输入站点的新名称。

1. 单击&#x200B;**编辑**。

## 删除Edge Delivery站点 {#delete-edge-delivery-site}

如果删除Edge Delivery Services站点，则任何关联的CDN配置也会被删除。 此操作中断自定义域与站点之间的连接。 有关详细信息，请参阅CDN配置。<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2024.9.0+Release -->

**删除Edge Delivery站点：**

1. 在[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)登录Cloud Manager并选择适当的程序。
1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台上，选择已配置Edge Delivery Services的程序，并从中添加Edge Delivery站点。
1. 执行以下任一操作：

   * 从&#x200B;**项目概述**&#x200B;页面，单击&#x200B;**Edge Delivery**选项卡。 在Edge Delivery站点表中，单击要删除其站点的行末尾的省略号。
单击![删除Edge Delivery站点](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Delete_18_N.svg) **删除**，然后再次单击&#x200B;**删除**&#x200B;以确认删除该站点。

     ![从Edge Delivery选项卡添加Edge Delivery站点](/help/implementing/cloud-manager/assets/cm-eds-delete1.png)

   * 在页面的左上角，单击![显示或隐藏侧面导航](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg)以显示侧面导航菜单。 在&#x200B;**服务**&#x200B;标题下，单击![Edge Delivery网站的网页](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg)**Edge Delivery网站**。
在Edge Delivery站点表中，单击要删除其站点的行末尾的省略号。 单击![删除Edge Delivery站点](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Delete_18_N.svg) **删除**，然后再次单击&#x200B;**删除**&#x200B;以确认删除该站点。

     ![从Edge Delivery站点添加Edge Delivery站点按钮](/help/implementing/cloud-manager/assets/cm-eds-delete2.png)

## 记录支持票证 {#eds-support-ticket}

{{support-ticket}}


