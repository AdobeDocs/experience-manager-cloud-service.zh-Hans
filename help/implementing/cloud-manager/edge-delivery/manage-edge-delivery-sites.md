---
title: 在Cloud Manager中管理Edge Delivery站点
description: 了解如何将CDN配置添加到Edge Delivery站点或删除Edge Delivery站点。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: b222b4384b1c2a21ecbb244d149ce7e51cc7990f
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# 在Cloud Manager中管理Edge Delivery站点 {#manage-edge-delivery-sites}

了解如何通过将CDN配置添加到现有站点来管理Cloud Manager中的Edge Delivery站点。 或者，删除Edge Delivery站点。

## 将CDN配置添加到现有Edge Delivery站点 {#add-cdn-to-edge-delivery-site}

请参阅[添加CDN配置](/help/implementing/cloud-manager/cdn-configurations/add-cdn-config.md)。

## 删除Edge Delivery站点 {#delete-edge-delivery-site}

如果删除Edge Delivery Services站点，则任何关联的CDN配置也会被删除。 此操作中断自定义域与站点之间的连接。 有关详细信息，请参阅CDN配置。<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2024.9.0+Release -->

**删除Edge Delivery站点：**

1. 在[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)登录Cloud Manager并选择适当的程序。
1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台上，选择已配置Edge Delivery Services的程序，并从中添加Edge Delivery站点。
1. 执行以下任一操作：
   * 从&#x200B;**项目概述**&#x200B;页面，单击&#x200B;**Edge Delivery**选项卡。 在Edge Delivery站点表中，单击要删除其站点的行末尾的省略号。
单击“**删除**”，然后再次单击“**删除**”以确认移除网站。

     ![从Edge Delivery选项卡添加Edge Delivery站点](/help/implementing/cloud-manager/assets/cm-eds-delete1.png)

   * 在页面的左上角，单击汉堡图标以显示左侧导航菜单。 在&#x200B;**服务**&#x200B;标题下，单击&#x200B;**Edge Delivery站点**。
在Edge Delivery站点表中，单击要删除其站点的行末尾的省略号。 单击“**删除**”，然后再次单击“**删除**”以确认移除网站。


     ![从Edge Delivery站点添加Edge Delivery站点按钮](/help/implementing/cloud-manager/assets/cm-eds-delete2.png)