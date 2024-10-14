---
title: 管理 IP 允许列表
description: 了解如何在Cloud Manager中查看、编辑、删除和检查IP允许列表的状态。
exl-id: 6efabe53-3f45-47d4-ac1f-979cae0ab33e
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 40a76e39750d6dbeb03c43c8b68cddaf515a2614
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 19%

---

# 管理 IP 允许列表 {#manage-ip-allow-lists}

了解如何在Cloud Manager中查看、编辑、删除和检查IP允许列表的状态。

## 查看和更新IP允许列表 {#update-ip-allow-lists}

具有&#x200B;**业务负责人**&#x200B;或&#x200B;**部署管理员**&#x200B;角色的用户可以按照这些步骤查看和更新IP允许列表。

**要查看和更新IP允许列表：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上登录到 Cloud Manager 并选择适当的组织和项目。
1. 在&#x200B;**概述**&#x200B;页面的左侧菜单的&#x200B;**服务**&#x200B;下，单击![任务列表图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_TaskList_18_N.svg) **IP允许列表**。
1. 标识要查看或更新的IP允许列表的行。
1. 单击行右端的![更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。
1. 从下拉菜单中，单击&#x200B;**查看和更新**。
**查看和更新IP允许列表**&#x200B;对话框显示定义规则的名称、IP地址（或范围）以及应用规则的环境和服务。
1. 根据需要更改名称或IP地址。

   向IP环境添加或删除新的IP范围会自动将其应用/取消应用到先前已应用它的所有相应允许列表/服务。

   当先前的更新正在进行且尚未完成时，无法对IP允许列表进行更新。

1. 单击&#x200B;**更新**。

## 检查IP允许列表的状态 {#check-allow-list-status}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上登录到 Cloud Manager 并选择适当的组织和项目。

1. 在&#x200B;**概述**&#x200B;页面的左侧菜单的&#x200B;**服务**&#x200B;下，单击![任务列表图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_TaskList_18_N.svg) **IP允许列表**。

1. 在IP允许列表表的&#x200B;**Status**&#x200B;列中，将鼠标指针悬停在绿色（正在使用）的IP允许列表上，以查看应用到它的一个或多个服务。

   表中显示的状态值具有以下含义：

   | IP允许列表的状态 | 描述 |
   | --- | --- |
   | 已应用 | IP允许列表已成功应用于一个或多个环境。 |
   | 正在更新 | 正在更新IP允许列表，可能包括列表的一个或多个应用或取消应用。 每个应用/取消应用都与其自己的状态一起列出：**未启动**、**进行中**、**完成**&#x200B;或&#x200B;**失败。** |
   | 失败 | 一个或多个应用或取消应用更新进程失败。<br>·列出每个应用和取消应用及其状态。<br>·如果更新中的一个应用/取消应用失败，则状态为&#x200B;**失败**。 在清除所有故障之前，状态会保持为&#x200B;**失败。**<br>·单击状态旁边的&#x200B;**重试**&#x200B;图标，以便清除故障。<br>·无法更新或删除状态为&#x200B;**失败**&#x200B;的IP允许列表。 |
   | 正在删除 | 正在删除IP允许列表。<br>·删除涉及从所有服务中取消应用列表。<br>·每个取消应用都与其自己的状态一起列出：**未启动**、**正在进行**、**完成**&#x200B;或&#x200B;**失败**。<br>·删除操作完成后，IP允许列表未出现在IP允许列表表中。 此外，IP允许列表不适用于Cloud Manager程序中的任何服务。 |
   | 删除失败 | 删除操作期间，一个或多个取消应用失败。<br>·每个取消应用都与状态&#x200B;**完成**&#x200B;或&#x200B;**失败**&#x200B;一起列出。<br>·如果一个取消应用失败，则状态变为&#x200B;**删除失败**。 在清除所有故障之前，状态将保持为&#x200B;**删除失败**。 在表格行的最右侧，单击![更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)，然后在下拉菜单中，单击&#x200B;**删除**&#x200B;以清除任何故障。<br>·当状态为&#x200B;**失败**&#x200B;时，无法更新IP允许列表。 |

## 删除IP允许列表 {#delete-allow-list}

删除IP允许列表时，会自动从所有服务中取消应用该列表，并将其从IP允许列表表中删除。

具有&#x200B;**业务负责人**&#x200B;或&#x200B;**部署管理员**&#x200B;角色的用户可以按照这些步骤查看和更新IP允许列表。

**删除IP允许列表：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上登录到 Cloud Manager 并选择适当的组织和项目。
1. 在&#x200B;**概述**&#x200B;页面的左侧菜单的&#x200B;**服务**&#x200B;下，单击![任务列表图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_TaskList_18_N.svg) **IP允许列表**。
1. 识别要删除的IP允许列表的行，然后单击该行右端的![更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)，然后单击&#x200B;**删除**。
1. 在&#x200B;**删除IP允许列表**&#x200B;对话框中，单击&#x200B;**删除**。

## 预先存在的CDN配置 {#pre-existing-cdn}

如果您的IP允许列表已有CDN （内容分发网络）配置，则&#x200B;**IP允许列表**&#x200B;页面上将显示一条信息性消息。 该消息鼓励您通过用户界面添加这些配置，以便它们在 Cloud Manager 中可见且可配置。

使用 UI 迁移所有预先存在的环境配置后，消息将消失。消息可能需要 1 – 2 个工作日才能消失。

有关详细信息，请参阅[添加IP允许列表](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md)。

**SSL 证书**&#x200B;和&#x200B;**环境**&#x200B;页面上也提供了类似的消息，这些环境具有 SSL 证书或自定义域名的预先存在的 CDN 配置。
