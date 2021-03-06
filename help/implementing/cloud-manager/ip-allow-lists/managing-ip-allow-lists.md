---
title: 管理 IP 允许列表
description: 了解如何在Cloud Manager中查看、编辑、删除和检查IP允许列表的状态。
source-git-commit: 878381f9c5780864f218a00a272b1600d578dcca
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 1%

---


# 管理 IP 允许列表 {#manage-ip-allow-lists}

了解如何在Cloud Manager中查看、编辑、删除和检查IP允许列表的状态。

## 查看和更新IP允许列表 {#update-ip-allow-lists}

中的用户 **业务所有者** 或 **部署管理器** 角色可以按照以下步骤查看和更新IP允许列表。

1. 登录Cloud Manager(位于 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 并选择相应的组织和程序。
1. 导航到 **环境** 屏幕 **概述** 页面。
1. 导航到 **IP允许列表** 页面 **环境** 屏幕。
1. 确定您要查看或更新的IP允许列表的行。
1. 单击行右端的省略号按钮。
1. 选择 **查看和更新** 选项。
1. 的 **查看和更新** 向导将显示定义规则的名称、IP地址（或范围）以及应用规则的环境和服务。
1. 更改名称或IP地址，并确认您的提交。

向IP允许列表添加或删除新IP范围时，会自动将其应用/取消应用到之前应用到的所有相应环境/服务。

在进行先前更新且未完成时，无法对IP允许列表进行更新。

## 检查IP允许列表的状态 {#check-allow-list-status}

请按照以下步骤检查IP允许列表的状态。

1. 登录Cloud Manager(位于 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 并选择相应的组织和程序。

1. 导航到 **环境** 屏幕 **概述** 页面。

1. 单击 **状态** 图标，用于从 **环境** 屏幕并选择 **IP允许列表** 页面。

1. Cloud Manager将显示允许列表的状态，如所述 [在以下部分中。](#status)

### IP允许列表的状态 {#status}

[检查IP允许列表的状态时，](#check-allow-list-status) 它们可以具有以下值之一。

* **已应用** - IP允许列表已成功应用于一个或多个环境。

* **更新**  — 正在对IP允许列表进行更新，该更新可能包括一个或多个应用程序或取消应用列表。

   * 每个应用程序/取消应用程序都会列出，并且其自身的状态为 **未启动**, **正在进行**, **完成**&#x200B;或 **失败**.

* **失败**  — 更新的一个或多个应用程序或未应用程序进程失败。
   * 每个应用程序和未应用程序都与其状态一起列出。
      * 状态为 **失败** 如果更新中的一个应用程序/取消应用程序失败。
      * 状态将保持为 **失败** 直到所有故障都被清除。
         * 您必须选择 **重试** 图标以清除失败。
      * 您无法使用 **失败** 状态。

* **删除**  — 正在删除IP允许列表。
   * 删除操作涉及从所有服务中取消应用列表。
   * 每个未应用程序都会列出，并且其自身的状态为 **未启动**, **正在进行**, **完成**&#x200B;或 **失败**.
   * 删除操作完成后，IP允许列表将：
      * IP允许列表表中不再显示。
      * 不再应用于Cloud Manager中程序中的任何服务。

* **删除失败**  — 在删除操作期间，一个或多个取消应用程序失败。

   * 每个未应用程序都会与状态一起列出 **完成** 或 **失败**.
   * 状态将为 **删除失败** 如果一个取消应用程序失败。
   * 状态将保持为 **删除失败** 直到所有故障都被清除。
      * 您必须选择 **删除** 从表行最右侧的省略号菜单中清除任何失败。
   * 当状态为 **失败**.

## 删除 IP 允许列表 {#delete-allow-list}

中的用户 **业务所有者** 或 **部署管理器** 角色可以按照以下步骤查看和更新IP允许列表。

1. 登录Cloud Manager(位于 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 并选择相应的组织和程序。
1. 导航到 **环境** 屏幕 **概述** 页面。
1. 导航到 **IP允许列表** 页面 **环境** 屏幕。
1. 确定要删除的IP允许列表的行。
1. 选择行最右端的省略号菜单。
1. 单击&#x200B;**删除**。
1. 确认您的提交。

删除IP允许列表会自动从所有服务中取消应用该IP服务，并从表中删除该IP服务。

## 预先存在的CDN配置 {#pre-existing-cdn}

如果您的IP允许列表已预先拥有CDN配置，则 **IP允许列表** 页面，鼓励您通过UI添加这些配置，以便它们在Cloud Manager中可见且可配置。

使用UI迁移所有预先存在的环境配置后，该消息会消失。 消息可能需要1-2个工作日才能消失。

请参阅该文档 [添加IP允许列表](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md) 以了解更多详细信息。

在 **SSL证书** 和 **环境** 页面，适用于对SSL证书或自定义域名预先存在CDN配置的环境。
