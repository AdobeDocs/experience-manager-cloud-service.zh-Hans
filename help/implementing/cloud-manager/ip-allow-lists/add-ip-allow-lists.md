---
title: 添加 IP 允许列表
description: 允许列表了解如何使用Cloud Manager添加您自己的IP。
exl-id: 769be71f-5c11-4f98-8906-7a5667a25aee
source-git-commit: 7260649eaab303ba5bab55ccbe02395dc8159949
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 40%

---


# 添加 IP 允许列表 {#add-ip-allow-list}

允许列表了解如何使用Cloud Manager添加您自己的IP。

中的用户 **业务负责人** 或 **部署管理员** 允许列表角色可以按照以下步骤添加IP。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织和程序。

1. 从&#x200B;**概述**&#x200B;页面导航到&#x200B;**环境**&#x200B;屏幕。

1. 从&#x200B;**环境**&#x200B;页面导航到 **IP 允许列表**&#x200B;页面。

   ![侧面板中的 IP 允许列表选项](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create.png)

1. 单击 **添加IP允许列表** 以打开 **添加IP允许列表** 对话框。

   ![“添加IP允许列表”对话框](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create02.png)

1. 允许列表输入您想要用于引用中的名称 **IP允许列表名称** 字段。

   * 此名称仅供参考，应该是描述性的，以帮助您识别列表。

1. 在 **IP 地址/CIDR** 字段中输入 IP 或 IP CIDR 块。

   * 多个块可以用逗号或制表符分隔。

1. 单击&#x200B;**保存**，并确认您的提交。

保存后，新创建的IP允许列表在的表格中显示为一行。 **IP允许列表** 页面。
