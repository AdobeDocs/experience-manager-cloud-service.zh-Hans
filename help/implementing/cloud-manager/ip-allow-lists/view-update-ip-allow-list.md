---
title: 查看和更新 — Cloud Manager中的IP允许列表
description: 查看和更新 — Cloud Manager中的IP允许列表
exl-id: 9f9aebcd-b6d0-497a-b262-0a24b4938b45
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 2%

---

# 查看和更新 IP 允许列表 {#view-update}

您可以在以下情况下查看和更新IP允许列表:

* 查看和更新菜单，以便仅查看一个或多个IP允许列表的详细信息。
* 要编辑以下一项或多项：
   * 规则名称定义中的IP范围
   * IP允许列表规则的友好名称

## 更新IP允许列表 {#update-ip-allow-lists}


必须登录具有业务所有者或部署管理员角色的用户，才能更新IP允许列表。

>[!NOTE]
>查看和更新向导将显示定义规则的名称、IP或IP范围。 此外，它还将显示应用规则的环境和服务。

请按照以下步骤更新IP允许列表:

1. 导航到 **IP允许列表** 页面 **环境** 屏幕。
1. 确定要查看/更新的IP允许列表规则所在的行。
1. 选择 **...** 菜单。
1. 选择 **查看和更新** 选项。
1. 更改名称或IP，并确认您的提交。

## 添加、更新或删除IP允许列表的重要注意事项 {#considerations}

* 向IP允许列表添加新IP范围将自动将其应用到所有相应的环境服务。
* 从IP允许列表中删除IP范围将自动从所有相应的环境服务中取消应用该范围。
* 在进行先前更新且未完成时，无法对IP允许列表进行更新。
* 如果之前的更新中存在任何错误，则无法对IP允许列表进行更新。 必须通过尝试重试更新来清除任何错误。
请参阅 [检查IP允许列表状态](/help/implementing/cloud-manager/ip-allow-lists/check-ip-allow-list-status.md) 以了解更多。
