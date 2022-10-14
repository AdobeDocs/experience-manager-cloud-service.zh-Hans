---
title: 添加 IP 允许列表
description: 了解如何使用 Cloud Manager 添加您自己的 IP 允许列表。
exl-id: 769be71f-5c11-4f98-8906-7a5667a25aee
source-git-commit: 378ff582435f1ab3db431a0c9c3e80a4661cccc4
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 100%

---


# 添加 IP 允许列表 {#add-ip-allow-list}

了解如何使用 Cloud Manager 添加您自己的 IP 允许列表。

具有&#x200B;**业务负责人**&#x200B;或&#x200B;**部署管理员**&#x200B;角色的用户可以按照这些步骤添加 IP 允许列表。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织和程序。

1. 从&#x200B;**概述**&#x200B;页面导航到&#x200B;**环境**&#x200B;屏幕。

1. 从&#x200B;**环境**&#x200B;页面导航到 **IP 允许列表**&#x200B;页面。

   ![侧面板中的 IP 允许列表选项](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create.png)

1. 单击&#x200B;**添加 IP 允许列表**，打开&#x200B;**添加 IP 允许列表**&#x200B;对话框。

   ![“添加 IP 允许列表”对话框](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create02.png)

1. 在 **IP 允许列表名称**&#x200B;字段中输入您想要用来引用允许列表的名称。

   * 该名称仅用作提供信息，且应该提供描述，帮助您识别列表。

1. 在 **IP 地址/CIDR** 字段中输入 IP 或 IP CIDR 块。

   * 多个块可以用逗号或制表符分隔。

1. 单击&#x200B;**保存**，并确认您的提交。

保存后，新创建的 IP 允许列表将在 **IP 允许列表**&#x200B;页面的表格中显示为一行。
