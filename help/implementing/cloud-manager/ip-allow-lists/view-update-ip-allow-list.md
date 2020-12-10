---
title: 查看和更新- Could Manager中的IP允许列表
description: 查看和更新- Could Manager中的IP允许列表
translation-type: tm+mt
source-git-commit: 4635cb6360707d12cf512b0ee21f05169a153114
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---


# 查看和更新IP允许列表{#view-update}

您可以在以下情况下视图和更新IP允许列表:

* 视图和更新菜单，只需视图一个或多个IP允许列表的详细信息。
* 要编辑以下一项或多项：
   * 规则名称定义中的IP范围
   * IP允许列表规则的友好名称

## 更新IP允许列表{#update-ip-allow-lists}


必须登录“业务所有者”或“部署管理者”角色的用户，才能更新IP允许列表。

>[!NOTE]
>视图和更新向导将显示定义规则的名称、IP或IP范围。 此外，它还将显示应用规则的环境和服务。

请按照以下步骤更新IP允许列表:

1. 从&#x200B;**允许列表**&#x200B;屏幕导航到&#x200B;**IP环境**&#x200B;页。
1. 确定您希望允许列表/更新的IP视图规则所在的行。
1. 选择&#x200B;**...**&#x200B;菜单。
1. 选择&#x200B;**视图和更新**&#x200B;选项。
1. 更改名称或IP并确认您的提交。

## 添加、更新或删除IP允许列表{#considerations}时的重要注意事项

* 向IP允许列表添加新的IP范围将自动将其应用到所有相应的环境服务。
* 从IP允许列表删除IP范围将自动从所有相应环境服务中取消应用它。
* 在先前更新正在进行且尚未完成时，无法对IP允许列表进行更新。
* 如果先前更新中存在任何错误，则无法对IP允许列表进行更新。 必须通过尝试重试更新来清除任何错误。
请参阅[检查IP允许列表状态](/help/implementing/cloud-manager/ip-allow-lists/check-ip-allow-list-status.md)以了解更多信息。