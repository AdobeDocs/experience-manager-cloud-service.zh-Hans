---
title: 在 Cloud Manager 中管理 Edge Delivery Sites
description: 了解如何将 CDN 配置添加到 Edge Delivery 网站或删除 Edge Delivery 网站。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f64a551bc18b53d0026736ece2a44e48cd0cfb4c
workflow-type: ht
source-wordcount: '538'
ht-degree: 100%

---

# 在 Cloud Manager 中管理 Edge Delivery 网站 {#manage-edge-delivery-sites}

了解如何通过向现有网站添加 CDN 配置来管理 Cloud Manager 中的 Edge Delivery 网站。或删除 Edge Delivery 网站。

## 将 CDN 配置添加到现有的 Edge Delivery 网站 {#add-cdn-to-edge-delivery-site}

请参阅[添加 CDN 配置](/help/implementing/cloud-manager/cdn-configurations/add-cdn-config.md)。

## 重命名 Edge Delivery 网站 (#rename-edge-delivery-site)

在 Adobe Cloud Manager 中，您可能需要重命名 Edge Delivery 网站，原因有几个：

* **清晰度和组织性**：更好地描述网站的目的或其相关环境（例如，生产、阶段）。
* **避免混淆**：如果使用多个网站，重命名可以帮助轻松区分它们，减少将配置或更新应用于错误网站的可能性。
* **标准化**：遵循与组织指导方针一致的命名惯例，以便于管理和审核。

**若要重命名 Edge Delivery 网站：**

1. 登录 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上的 Cloud Manager，然后选择合适的程序。
1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台中，选择配置了 Edge Delivery Services 的程序，您要在其中添加 Edge Delivery 网站。
1. 执行以下任一操作：

   * 从&#x200B;**程序概览**&#x200B;页面，单击 **Edge Delivery** 选项卡。 在 Edge Delivery 网站表中，单击要重命名其网站的行末尾的省略号。单击&#x200B;**重命名**。
   * 在页面左上角，单击![显示菜单图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg)以显示左侧菜单。在&#x200B;**服务**&#x200B;标题下，单击![网页图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) **Edge Delivery 网站**。
在 Web pages 网站表中，单击要重命名其网站的行末尾的![更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。单击&#x200B;**重命名**。

1. 在&#x200B;**编辑 Edge Delivery 网站**&#x200B;对话框中的&#x200B;**网站名称**&#x200B;文本字段内，输入网站的新名称。

1. 单击&#x200B;**编辑**。

## 删除 Edge Delivery 网站 {#delete-edge-delivery-site}

如果删除 Edge Delivery Services 网站，则任何相关的 CDN 配置也会被删除。此操作会断开自定义域与网站之间的连接。有关详细信息，请参阅 CDN 配置。<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2024.9.0+Release -->

**要删除 Edge Delivery 网站：**

1. 登录 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上的 Cloud Manager，然后选择合适的程序。
1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台中，选择配置了 Edge Delivery Services 的程序，您要在其中添加 Edge Delivery 网站。
1. 执行以下任一操作：

   * 从&#x200B;**程序概览**&#x200B;页面，单击 **Edge Delivery** 选项卡。 在 Edge Delivery 网站表中，单击要删除其网站的行末尾的![更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。
点击![删除 Edge Delivery 网站](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Delete_18_N.svg)**删除**，然后再次点击&#x200B;**删除**&#x200B;以确认移除该网站。

     ![从 Edge Delivery 选项卡添加 Edge Delivery 网站](/help/implementing/cloud-manager/assets/cm-eds-delete1.png)

   * 在页面左上角，单击![显示菜单图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg)以显示左侧菜单。在&#x200B;**服务**&#x200B;标题下，单击 ![Edge Delivery 网站的网页](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) **Edge Delivery 网站**。
在 Edge Delivery 网站表中，单击要移除其网站的行末尾的![更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。单击![删除 Edge Delivery 网站](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Delete_18_N.svg)**删除**，然后再次单击&#x200B;**删除**&#x200B;以确认移除该网站。

     ![通过 Edge Delivery 网站按钮添加 Edge Delivery 网站](/help/implementing/cloud-manager/assets/cm-eds-delete2.png)

## 记录支持工单 {#eds-support-ticket}

{{support-ticket}}


