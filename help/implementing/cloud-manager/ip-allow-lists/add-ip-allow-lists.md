---
title: 添加 IP 允许列表
description: 了解如何使用 Cloud Manager 添加您自己的 IP 允许列表。
exl-id: 769be71f-5c11-4f98-8906-7a5667a25aee
source-git-commit: 97a6a7865f696f4d61a1fb4e25619caac7b68b51
workflow-type: ht
source-wordcount: '193'
ht-degree: 100%

---


# 添加 IP 允许列表 {#add-ip-allow-list}

了解如何使用 Cloud Manager 添加您自己的 IP 允许列表。

具有&#x200B;**业务负责人**&#x200B;或&#x200B;**部署管理员**&#x200B;角色的用户可以按照这些步骤添加 IP 允许列表。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上登录到 Cloud Manager 并选择适当的组织和项目。

1. 从&#x200B;**概述**&#x200B;页面，导航到&#x200B;**环境**&#x200B;屏幕。

1. 从&#x200B;**环境**&#x200B;屏幕，导航到 **IP 允许列表**&#x200B;页面。

   ![侧面板中的“IP 允许列表”选项](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create.png)

1. 单击&#x200B;**添加 IP 允许列表**。

   ![“添加 IP 允许列表”对话框](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create02.png)

1. 在&#x200B;**添加 IP 允许列表**&#x200B;对话框中，在 **IP 允许列表名称**&#x200B;字段中输入要用于引用允许列表的名称。

   * 该名称仅用作提供信息，且应该提供描述，帮助您识别列表。

1. 在 **IP 地址/CIDR** 字段中输入 IP 或 IP CIDR 块。

   * 多个块可以用逗号或制表符分隔。

1. 单击&#x200B;**保存**。

保存后，新创建的 IP 允许列表作为一行出现在 **IP 允许列表**&#x200B;页面的表格中。
