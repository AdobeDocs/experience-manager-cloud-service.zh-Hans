---
title: 通知
description: 了解如何使用Adobe Experience Cloud通知系统接收有关管道部署的信息。
exl-id: c1c740b0-c873-45a8-9518-a856db2be75b
source-git-commit: 0de041211c8257d920bcf354593b3caa2db43572
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 1%

---


# 通知 {#notifications}

了解Cloud Manager如何通知您重要事件。

## Cloud Manager中的通知 {#cloud-manager-notifications}

[!UICONTROL Cloud Manager] 当生产管道在生产部署开始时开始并完成（成功或失败）时，会向您发送通知。

这些通知通过 [!UICONTROL Experience Cloud] 通知系统 **业务所有者**, **项目经理**&#x200B;和 **部署管理器** 角色。

通知显示在 [!UICONTROL Cloud Manager] 和整个Adobe [!UICONTROL Experience Cloud]. 当您有新通知时，标题中的铃铛图标会出现标记。

![“通知”图标](assets/notifications-bell-badged.png)

单击铃铛图标以打开侧栏并查看通知。 的 **通知** 选项卡，其中列出了最新的通知，如部署确认。 通知与您的环境有关。

![通知侧栏](assets/notifications-activities.png)

的 **公告** 选项卡包括Adobe产品公告。 公告涉及产品。

![通知侧栏](assets/notificaitons-announcements.png)

单击通知或公告可查看其详细信息。 链接到活动（如管道部署）的通知会将您转到该活动的详细信息，如管道执行窗口。

单击 **查看全部** 选项来查看收件箱中的所有公告。

单击 **全部标记为已读** 选项，将所有未读通知标记为已读，并清除铃铛图标标记。

## 通知配置 {#configuration}

您可以自定义接收通知的方式以及接收的通知。

单击通知侧栏顶部的齿轮图标。

![“通知设置”图标](assets/notifications-configuration.png)

这将打开 **Experience Cloud首选项** 窗口，您可以在此处定义通知订阅以及接收通知的方式。

### 订阅 {#subscriptions}

订阅可定义您接收通知的产品和通知。

![通知订阅](assets/notifications-subscriptions.png)

默认情况下，您将收到所有产品的所有通知。 单击 **自定义** 定义您为该产品接收的通知类型。

![通知订阅自定义](assets/notifications-subscriptions-customize.png)

### 优先级 {#priority}

优先级警报将标有 **高** 标记，并且可以配置为仅作为警报接收。 在 **优先级** 部分，您可以定义哪些类别符合优先级通知的条件。

![通知优先级](assets/notifications-priority.png)

使用下拉列表将符合优先级的类别添加到列表中。 单击类别名称旁边的X可删除这些名称。

### 警报 {#alerts}

警报会在窗口的右上角显示几秒钟。 使用 **警报** 部分，以定义接收警报的通知。

![通知警报](assets/notifications-alerts.png)

您可以定义警报的行为。

* **显示警报**  — 定义触发警报的通知类型
* **警报应会一直保留在屏幕中，直到我将其取消为止**  — 控制警报是否应持续存在，除非您主动取消它们
* **持续时间**  — 定义警报在屏幕上停留的时间（如果您未选择警报应停留在屏幕上）。

## 电子邮件 {#emails}

可在Web用户界面中跨Adobe获取通知 [!UICONTROL Experience Cloud] 解决方案。 您还可以在 **电子邮件** 中。

![通知电子邮件](assets/notifications-emails.png)

默认情况下，不会发送任何电子邮件。 您可以选择以下形式接收电子邮件：

* 立即
* 每日
* 每周

When **即时通知** 选择后，会立即发送每个通知的电子邮件。 对于 **每日摘要** 和 **每周摘要** 您可以选择发送每日摘要的时间、发送日期和每周摘要的时间。