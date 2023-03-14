---
title: 通知中心
description: 利用通知中心方便地对事件和其他重要信息采取行动
hidefromtoc: true
source-git-commit: a5977c667d831c47d41cd86b68e9196fbe726899
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 0%

---


# 通知中心 {#notification-center}

>[!NOTE]
>此功能尚未发布。

配置完毕后，AEM as Cloud Service将发送有关客户应采取行动的重要信息的通知。 通知的示例包括受阻队列或一组即将过期的凭据。 要查看完整的通知类型集，请访问 [下表](#current-notification-types)，和会随着时间的推移而扩展。 通知将通过电子邮件接收，并作为通知小组件下的新条目接收，单击整个Adobe Experience Cloud右上角的铃铛图标可访问该小组件。 可以配置通知设置。

当收到通知时，可以单击该通知以打开AEMas a Cloud Service的通知中心，此时会显示一个弹出窗口，其中显示了说明客户可采取之建议操作的附加上下文。

除了显示有关刚刚点击的通知的信息外，“通知中心”还可用作查看和管理当前通知集和旧通知集的中心。 <!-- It can be accessed directly at the url TBD (Alexandru: I'm intentionally keeping it TBD for now so customers don't find it) -->

通知有两种高级类别：

1. 事件 — 已发生事件，通常需要立即解决。 例如，解决阻塞的队列
1. 主动 — Adobe建议客户在不久的将来应采取的操作。 例如，停止引用已弃用的UI。

请参阅 [下表](#current-notification-types) 当前支持的通知。

从“通知中心”屏幕中，您可以选择特定的程序和环境，这将筛选该范围的程序和环境。

## 配置 {#configuration}

您可以按照以下步骤配置接收通知：

1. 创建以下产品配置文件，如所述 [本文章节](/help/journey-onboarding/user-groups.md)，将适当的AdobeID从您的组织分配给这些配置文件。
1. 确定通知配置设置。 [在此页面上](https://experience.adobe.com/preferences/notification-section)，确保已启用Experience Manager订阅并且 **其他** 复选框处于选中状态。 此外，建议将电子邮件部分设置为 **即时通知** 因此，您会在事件发生后立即收到通知。

>[!NOTE]
>订阅在组织级别运行，因此订阅者将收到这些程序中所有程序和环境的通知。

## 详细用户流程 {#detailed-user-flow}

单击电子邮件会将您带到通知中心，此时会显示一个弹出窗口，其中显示您单击的通知的上下文，在某些情况下，还会显示描述如何采取纠正措施的其他信息的链接。

![事件详细信息](/help/operations/assets/incident-details.png)

单击 **了解详情** 链接会将用户导航到本文，下面的表中可引用通知，该表提供了有关要采取的操作的指导。

在通知中心，您可以看到其他最近通知的列表。 建议您使用“操作”列表确认通知，以便向Adobe表明您的组织已了解此任务，并在以后采取纠正操作后解决此通知。

![通知列表](/help/operations/assets/notification-list.png)

在大多数情况下，通知应提供解决问题所需的所有必要上下文。 但是，如果Adobe支持存在问题，您可以单击 **联系支持人员** 通知弹出窗口中的链接。 这将显示一个表格，您可以在其中描述问题并提交它以创建支持工单，该表格还包括对特定通知的引用，以便Adobe支持工程师具有相关上下文。

![联系支持人员1](/help/operations/assets/contact-support1.png)

![联系支持人员2](/help/operations/assets/contact-support2.png)

与所有支持工单一样，它将显示在 [Adobe Admin Console的“支持案例”选项卡](https://helpx.adobe.com/enterprise/using/support-for-enterprise.html)，您可以在其中跟踪和添加其他注释。

![Admin Console支持](/help/operations/assets/admin-console-support.png)

## 当前通知类型 {#current-notification-types}

下表列出了当前支持的通知类型

| 通知类型 | 相关产品配置文件 | 更正操作 |
|---|---|---|
| 已阻止的复制队列 | 事件 | 按照 [复制文档](/help/operations/replication.md#troubleshooting) |
| 即将过期的S2S证书 | 主动 | 了解如何在中刷新凭据 [为服务器端API文档生成访问令牌](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials) |
