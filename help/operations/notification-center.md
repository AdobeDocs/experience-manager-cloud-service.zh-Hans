---
title: 通知中心
description: 利用通知中心可方便地针对问题和其他重要信息采取行动
hidefromtoc: true
source-git-commit: 55ecd685afa28226974f3415b550bd2e8d05e2e6
workflow-type: ht
source-wordcount: '638'
ht-degree: 100%

---


# 通知中心 {#notification-center}

>[!NOTE]
>此功能尚未发布。

配置后，AEM as Cloud Service 会发送有关重要信息的通知，客户将根据这些重要信息采取行动。通知的示例包括锁定队列或一组到期的凭据。可以在[下表](#current-notification-types)中查看完整通知类型集，该集将随着时间的推移而扩展。通知既可以通过电子邮件接收，也可以作为通知构件下的新条目接收，在整个 Adobe Experience Cloud 中单击右上角的铃铛图标即可访问该构件。可以配置通知设置。

收到通知后，可以单击它以打开 AEM as a Cloud Service 的通知中心，这将出现一个弹出窗口，其中显示的附加上下文对建议客户执行的操作进行了说明。

除了显示有关刚刚单击的通知信息外，通知中心还充当可供查看和管理一组当前和过往通知的中心。<!-- It can be accessed directly at the url TBD (Alexandru: I'm intentionally keeping it TBD for now so customers don't find it) -->

有两种高级类别的通知：

1. 问题 – 已发生事件，通常需要及时予以解决。 例如，解决锁定队列
1. 主动 – Adobe 对客户在不久的将来应采取的行动提出了建议。例如，停止引用已弃用的 UI。

有关当前支持的通知，请参阅[下表](#current-notification-types)。

从通知中心屏幕中，您可以选择特定的程序和环境，这将对范围有筛选效果。

## 配置 {#configuration}

您可以执行以下步骤来配置接收通知：

1. 创建以下产品配置文件，如[本文](/help/journey-onboarding/notification-profiles.md)中所述，并将来自您组织的适当 Adobe ID 分配给这些配置文件。
1. 确定通知配置设置。[在此页面上](https://experience.adobe.com/preferences/notification-section)，确保已启用 Experience Manager 订阅并选中&#x200B;**其他**&#x200B;复选框。此外，建议将电子邮件部分设置为&#x200B;**即时通知**，以便您在问题发生后立即收到通知。

>[!NOTE]
>订阅在组织级别运行，因此，订阅者将收到有关所有程序以及这些程序中环境的通知。

## 详细的用户流程 {#detailed-user-flow}

单击电子邮件会将您转至通知中心，这将出现一个弹出窗口，其中显示您单击的通知的上下文，在某些情况下，还会显示指向描述如何采取纠正措施的其他信息的链接。

![问题详细信息](/help/operations/assets/incident-details.png)

单击&#x200B;**了解更多**&#x200B;链接可将用户导航至本文，可参考下表中的通知，其中提供了有关执行哪项操作的指南。

在通知中心，您可以查看其他最新通知的列表。建议使用“操作”列表来确认通知，以便向 Adobe 表明您的组织已了解该任务，并稍后在采取纠正措施后解决该通知。

![通知列表](/help/operations/assets/notification-list.png)

在大多数情况下，通知应提供解决问题所需的所有必要上下文。不过，如果您要向 Adobe 支持部门提出问题，可以单击通知弹出窗口中的&#x200B;**联系支持人员**&#x200B;链接。这将弹出一个表单，您可以在其中描述问题并提交它以创建支持工单，它还将包含对特定通知的引用，以便 Adobe 支持工程师了解相关情况。

![联系支持人员 1](/help/operations/assets/contact-support1.png)

![联系支持人员 2](/help/operations/assets/contact-support2.png)

与所有支持工单一样，它将出现在 [Adobe Admin Console 的“支持案例”选项卡](https://helpx.adobe.com/enterprise/using/support-for-enterprise.html)中，您可以在其中跟踪它并添加其他评论。

![Admin Console 支持](/help/operations/assets/admin-console-support.png)

## 当前通知类型 {#current-notification-types}

下表列出了当前支持的通知类型

| 通知类型 | 相关产品配置文件 | 纠正措施 |
|---|---|---|
| 已锁定的复制队列 | 问题 | 按照[复制文档](/help/operations/replication.md#troubleshooting)中的说明执行操作来解锁队列 |
| 到期的 S2S 证书 | 主动 | 参阅[为服务器端 API 生成访问令牌](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials)文档，了解如何刷新凭据 |
