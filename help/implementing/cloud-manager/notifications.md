---
title: 通知
description: 了解如何使用 Adobe Experience Cloud 通知系统接收有关管道部署的信息。
exl-id: c1c740b0-c873-45a8-9518-a856db2be75b
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 85%

---


# 通知 {#notifications}

了解 Cloud Manager 如何向您通知重要事件。

## Cloud Manager 中的通知 {#cloud-manager-notifications}

[!UICONTROL Cloud Manager] 在生产部署开始时，当生产管道启动和完成（成功或失败）时向您发送通知。

这些通知通过 [!UICONTROL Experience Cloud] 通知系统发送给角色为&#x200B;**业务负责人**、**程序管理员**&#x200B;和&#x200B;**部署管理员**&#x200B;的用户。

通知显示在 [!UICONTROL Cloud Manager] 和整个 Adobe [!UICONTROL Experience Cloud] 侧边栏中。当您有新通知时，标题中的铃铛图标将被标记。

![“通知”图标](assets/notifications-bell-badged.png)

单击铃铛图标可打开侧边栏并查看通知。侧边栏中的&#x200B;**通知**&#x200B;选项卡列出了最近的通知，例如部署确认通知。通知涉及您的环境。

![通知侧边栏](assets/notifications-activities.png)

**公告**&#x200B;选项卡包括 Adobe 产品公告。公告涉及产品。

![通知侧边栏](assets/notificaitons-announcements.png)

单击通知或公告查看其详细信息。 链接到管道部署等活动的通知将带您了解该活动的详细信息，例如管道执行窗口。

单击 **查看全部** 面板底部的选项，用于查看收件箱中的所有公告。

单击 **将所有提醒标记为已读** 面板底部的选项，可将所有未读通知标记为已读取并清除铃铛图标标记。

## 通知配置 {#configuration}

您可以自定义接收通知的方式以及接收的通知。

单击通知侧边栏顶部的齿轮图标。

![通知设置图标](assets/notifications-configuration.png)

该操作将打开&#x200B;**Experience Cloud 偏好设置**&#x200B;窗口，您可以在其中定义通知订阅以及接收通知的方式。

### 订阅 {#subscriptions}

订阅定义了您收到通知的产品和通知。

![通知订阅](assets/notifications-subscriptions.png)

默认情况下，您将在应用程序中和通过电子邮件接收所有产品的全部通知。单击产品名称旁边的V形符号显示详细的选项，并定义您收到的该产品的通知类型。 或者，选中或取消选中产品级别的选项以选择/取消选择该产品的所有选项。

![通知订阅自定义](assets/notifications-subscriptions-customize.png)

### 优先级 {#priority}

优先警报标有&#x200B;**高**&#x200B;选项卡，并且可以配置为仅作为警报接收。在&#x200B;**优先级**&#x200B;分区，您可以定义哪些类别有资格作为优先通知。

![通知优先级](assets/notifications-priority.png)

使用下拉菜单添加到有资格作为优先级的类别列表中。单击类别名称旁边的 X 将其删除。

### 警报 {#alerts}

警报会在窗口右上角出现几秒钟。使用&#x200B;**警报**&#x200B;分区来定义您收到警报的通知。

![通知警报](assets/notifications-alerts.png)

您可以定义警报的行为。

* **显示警报** – 定义触发警报的通知类型
* **警报应该一直显示在屏幕上，直到我关闭它们** – 控制警报是否应该持续存在，除非您主动关闭它们
* **持续时间** – 定义如果您没有选择警报在屏幕上停留的时间，则警报应在屏幕上保持多长时间。

### 电子邮件 {#emails}

通知在 Adobe [!UICONTROL Experience Cloud] 解决方案的 Web 用户界面中提供。您也可以选择通过电子邮件在&#x200B;**电子邮件**&#x200B;分区发送这些通知。

![通知电子邮件](assets/notifications-emails.png)

默认情况下不发送电子邮件。您可以选择以以下方式接收电子邮件：

* 即刻
* 每日
* 每周

当选中&#x200B;**即时通知**&#x200B;后，每个通知都会立即发送电子邮件。对于&#x200B;**每日摘要**&#x200B;和&#x200B;**每周摘要**，您可以选择发送每日摘要的时间以及发送每周摘要的日期和时间。