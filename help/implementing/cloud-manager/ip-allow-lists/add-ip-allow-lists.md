---
title: 添加IP允许列表
description: 了解如何使用Cloud Manager添加您自己的IP允许列表。
exl-id: 769be71f-5c11-4f98-8906-7a5667a25aee
source-git-commit: 378ff582435f1ab3db431a0c9c3e80a4661cccc4
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 3%

---


# 添加 IP 允许列表 {#add-ip-allow-list}

了解如何使用Cloud Manager添加您自己的IP允许列表。

中的用户 **业务所有者** 或 **部署管理器** 角色可以按照以下步骤添加IP允许列表。

1. 登录Cloud Manager(位于 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 并选择相应的组织和程序。

1. 导航到 **环境** 屏幕 **概述** 页面。

1. 导航到 **IP允许列表** 页面 **环境** 屏幕。

   ![侧面板中的IP允许列表选项](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create.png)

1. 单击 **添加IP允许列表** 打开 **添加IP允许列表** 对话框。

   ![添加IP允许列表对话框](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create02.png)

1. 输入要在 **IP允许列表名称** 字段。

   * 这仅供参考，应具有描述性，可帮助您识别列表。

1. 在 **IP地址/CIDR** 字段。

   * 多个块可以用逗号或制表符分隔。

1. 单击 **保存** 确认提交。

保存后，新创建的IP允许列表将在 **IP允许列表** 页面。
