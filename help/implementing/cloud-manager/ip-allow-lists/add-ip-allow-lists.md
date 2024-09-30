---
title: 添加IP允许列表
description: 了解如何使用Cloud Manager添加您自己的IP允许列表。
exl-id: 769be71f-5c11-4f98-8906-7a5667a25aee
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 1902e9b237adbdaff172535d0904d0faa615e9d1
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# 添加 IP 允许列表 {#add-ip-allow-list}

了解如何使用Cloud Manager添加您自己的IP允许列表。

具有&#x200B;**业务负责人**&#x200B;或&#x200B;**部署管理员**&#x200B;角色的用户可以按照这些步骤添加IP允许列表。

{{add-cm-allowlist-frontend-pipeline}}

{{ip-allow-lists-ue}}

**添加IP允许列表：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台上，选择该程序。

1. 从&#x200B;**程序概述**&#x200B;页面，使用侧面板（您可能需要单击左上角的![显示菜单图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg)来查看面板），单击![任务列表图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_TaskList_18_N.svg) **IP允许列表**。

   侧面板中的![IP允许列表选项](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create.png)

1. 在“IP允许列表”页面的右上角附近，单击&#x200B;**添加IP允许列表**。

   ![“添加 IP 允许列表”对话框](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create02.png)

1. 在&#x200B;**添加IP允许列表**&#x200B;对话框的&#x200B;**IP允许列表名称**&#x200B;字段中，输入要用于引用IP允许列表的名称。 此名称仅供参考。 请确保其描述性足以帮助您识别列表。

1. 在&#x200B;**IP地址/ CIDR**&#x200B;字段中，输入IP或IP CIDR块。 用逗号或制表符分隔多个块。

1. 单击&#x200B;**保存**。

保存后，新创建的IP允许列表将在&#x200B;**IP允许列表**&#x200B;页的表中显示为一行。

