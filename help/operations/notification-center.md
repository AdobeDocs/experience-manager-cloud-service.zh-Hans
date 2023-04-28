---
title: 通知中心
description: 利用通知中心可方便地针对问题和其他重要信息采取行动
hidefromtoc: true
exl-id: d5a95ac4-aa88-44d5-ba02-7c9702050208
source-git-commit: b72d22e8788c04ab4faa3616a4a0ce5e6d8ce991
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 36%

---

# 通知中心 {#notification-center}

>[!NOTE]
>此功能尚未发布。

AEM as Cloud Service在发生需要立即采取行动的关键事件时发送通知，并主动提出优化建议。 示例包括阻止的队列或过期的一组凭据；可以在 [下表](#supported-notification-types)，会随着时间的推移而扩展。

这些通知可配置为通过电子邮件和通知小组件下方接收，通过单击Adobe Experience Cloud右上角的铃铛图标可访问该小组件。

收到通知后，单击该通知可打开AEMas a Cloud Service的通知中心，其中有一个弹出窗口，其中显示了说明客户所采取操作的其他上下文。

除了显示有关刚刚点击的通知的信息外，通知中心还充当一个中心，您可以在其中查看和管理当前和以前的通知集。 <!-- It can be accessed directly at the url TBD (Alexandru: I'm intentionally keeping it TBD for now so customers don't find it) -->

通知中心中显示了两个高级别的通知类别：

1. 操作事件 — 发生了一个事件，通常需要迅速解决。 例如，解决锁定队列.
1. 主动建议 — Adobe建议客户在不久的将来应采取的操作。 例如，停止引用已弃用的 UI。

有关当前支持的通知，请参阅[下表](#supported-notification-types)。

从通知中心，您可以选择具有该范围过滤效果的特定程序和环境。

## 配置 {#configuration}

请按照以下步骤配置接收通知：

1. 按照所述创建以下产品配置文件 [在本文中](/help/journey-onboarding/notification-profiles.md)，还会将您组织中的相应AdobeID分配给这些用户档案。 这允许管理员确定哪些用户有资格接收这些通知。
1. 在上一步中分配的每个已分配用户都可以配置他们接收通知的方式。 在 [Experience Cloud首选项页](https://experience.adobe.com/preferences/notification-section)，请确保启用了Experience Manager订阅，并且 **操作事件** 和 **主动建议** 复选框。 此外，建议将“电子邮件”部分设置为 **即时通知** 因此，在发生事件时会立即收到通知。

>[!NOTE]
>通知在组织级别起作用，这样订阅者将收到这些程序内所有程序和环境的通知。

## 详细的用户流程 {#detailed-user-flow}

单击电子邮件会将您转至通知中心，这将出现一个弹出窗口，其中显示您单击的通知的上下文，在某些情况下，还会显示指向描述如何采取纠正措施的其他信息的链接。

![问题详细信息](/help/operations/assets/incident-details.png)

单击&#x200B;**了解更多**&#x200B;链接可将用户导航至本文，可参考下表中的通知，其中提供了有关执行哪项操作的指南。

在通知中心，您可以查看其他最新通知的列表。建议使用“操作”列表来确认通知，以便向 Adobe 表明您的组织已了解该任务，并稍后在采取纠正措施后解决该通知。

![通知列表](/help/operations/assets/notification-list.png)

在大多数情况下，通知应提供解决问题所需的所有必要上下文。不过，如果您要向 Adobe 支持部门提出问题，可以单击通知弹出窗口中的&#x200B;**联系支持人员**&#x200B;链接。这将显示一个表格，您可以在其中描述问题并提交它以创建支持票证，该表格还将包含对特定通知的引用，以便Adobe支持工程师具有相关上下文。

![联系支持人员 1](/help/operations/assets/contact-support1.png)

![联系支持人员 2](/help/operations/assets/contact-support2.png)

与所有支持工单一样，它将出现在 [Adobe Admin Console 的“支持案例”选项卡](https://helpx.adobe.com/enterprise/using/support-for-enterprise.html)中，您可以在其中跟踪它并添加其他评论。

![Admin Console 支持](/help/operations/assets/admin-console-support.png)

## 哪些通知会显示？ {#which-notification}

AEMas a Cloud Service有多种类型的通知，但通知中心中只显示一个子集，如下表所示。

| 通知类型 | 描述 | 如何配置 | 显示在通知中心中 |
|---|---|---|---|
| 操作事件 | 需要立即采取行动的重大事件 | 分配给“事件通知 — Cloud Service”产品配置文件的用户，选中了“操作事件”复选框 [Experience Cloud首选项](https://experience.adobe.com/preferences) | X |
| 主动建议 | 应计划的优化 | 分配给“主动通知 — Cloud Service”产品配置文件的用户，选中“主动推荐”复选框(位于 [Experience Cloud首选项](https://experience.adobe.com/preferences) | X |
| Cloud Manager管道状态 | 有关管道状态的信息 | 在 [Experience Cloud首选项](https://experience.adobe.com/preferences) |  |

## 支持的通知类型 {#supported-notification-types}

下表列出了当前支持的通知类型。

| 通知类型 | 相关产品配置文件 | 纠正措施 |
|---|---|---|
| 已锁定的复制队列 | 问题 | 按照[复制文档](/help/operations/replication.md#troubleshooting)中的说明执行操作来解锁队列 |
| 到期的 S2S 证书 | 主动 | 参阅[为服务器端 API 生成访问令牌](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials)文档，了解如何刷新凭据 |

