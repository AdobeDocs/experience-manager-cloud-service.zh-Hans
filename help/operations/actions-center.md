---
title: 操作中心
description: 利用操作中心方便地对事件和其他重要信息采取行动
hidefromtoc: true
hide: true
exl-id: d5a95ac4-aa88-44d5-ba02-7c9702050208
source-git-commit: ca7cad567a5f83cd1edc14def6d961b8ba3b7f1f
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 32%

---

# 操作中心 {#actions-center}

>[!NOTE]
>此功能尚未发布。

AEM as aCloud Service会在发生需要立即采取行动的严重事件时向操作中心发送电子邮件通知，并提供主动优化建议。 示例包括受阻队列或一组即将过期的凭据；可以在以下位置查看整组操作中心通知类型： [下表](#supported-notification-types)，它会随着时间的推移而扩展。

在收到操作中心电子邮件通知后，可以单击该通知以打开AEMas a Cloud Service的操作中心，此时会显示一个显示附加上下文的弹出窗口，说明客户要执行的操作。

除了显示有关刚刚点击的电子邮件通知的信息之外，操作中心还可用作中心，您可以在其中查看和管理当前通知集和早期通知集。 <!-- It can be accessed directly at the url TBD (Alexandru: I'm intentionally keeping it TBD for now so customers don't find it) -->

“操作中心”中显示两种高级类别的通知：

1. 操作问题 – 已发生事件，通常需要及时予以解决。例如，解决锁定队列。
1. 主动建议 – Adobe 对客户在不久的将来应采取的行动提出了建议。例如，停止引用已弃用的 UI。

请参阅 [下表](#supported-notification-types) 操作中心当前支持的通知。

从操作中心中，您可以选择特定的项目和环境，这将筛选该范围。

## 配置 {#configuration}

要配置接收操作中心电子邮件通知，请创建描述的产品配置文件 [本文章节](/help/journey-onboarding/notification-profiles.md)即事件通知 — Cloud Service和主动通知 — Cloud Service。 还将贵组织的相应AdobeID分配给这些配置文件。 这允许管理员确定哪些用户有资格接收这些电子邮件通知。

>[!NOTE]
>操作中心电子邮件通知在组织级别起作用，因此订阅者将收到这些程序中所有程序和环境的通知。

## 详细的用户流程 {#detailed-user-flow}

单击电子邮件即可进入“警报中心”，此时会显示一个弹出窗口，其中显示您单击的通知的上下文，在某些情况下，还会显示描述如何采取更正操作的其他信息的链接。

![问题详细信息](/help/operations/assets/incident-details.png)

单击 **了解详情** 链接会将用户导航到本文，其中通知类型可在 [支持的通知类型表](#supported-notification-types) ，其中提供了有关采取何种行动的指导。

在操作中心，您可以看到其他最近通知的列表。 建议使用“操作”列表来确认通知，以便向 Adobe 表明您的组织已了解该任务，并稍后在采取纠正措施后解决该通知。

![通知列表](/help/operations/assets/notification-list.png)

在大多数情况下，弹出窗口应提供解决问题所需的所有上下文。 但是，如果Adobe支持存在问题，您可以单击 **联系支持人员** 弹出窗口中的链接。 这将显示一个表格，您可以在其中描述问题并提交它以创建支持工单，该表格还包括对特定通知的引用，以便Adobe支持工程师具有相关上下文。

![联系支持人员 1](/help/operations/assets/contact-support1.png)

![联系支持人员 2](/help/operations/assets/contact-support2.png)

与所有支持工单一样，它将出现在 [Adobe Admin Console 的“支持案例”选项卡](https://helpx.adobe.com/cn/enterprise/using/support-for-enterprise.html)中，您可以在其中跟踪它并添加其他评论。

![Admin Console 支持](/help/operations/assets/admin-console-support.png)

## 将出现哪些通知？ {#which-notification}

AEMas a Cloud Service具有多种类型的通知，但“操作中心”中只显示一个子集，如下表所示。

| 通知类型 | 描述 | 如何配置 | 显示在警报中心 |
|---|---|---|---|
| 操作问题 | 需要立即采取行动的关键问题 | 分配给“事件通知 — Cloud Service”产品配置文件的用户 | X |
| 主动建议 | 应该计划的优化 | 分配给“主动通知 — Cloud Service”产品配置文件的用户 | X |
| Cloud Manager 管道状态 | 有关您的管道状态的信息 | 具有“业务负责人”、“项目经理”或“部署经理”角色的用户，在 [Experience Cloud 偏好设置](https://experience.adobe.com/preferences)中选中了“其他”， as [此处对此进行了说明](/help/implementing/cloud-manager/notifications.md). |  |

## 支持的通知类型 {#supported-notification-types}

下表列出了操作中心当前支持的通知类型。

| 通知类型 | 相关产品配置文件 | 纠正措施 |
|---|---|---|
| 已锁定的复制队列 | 问题 | 按照[复制文档](/help/operations/replication.md#troubleshooting)中的说明执行操作来解锁队列 |
| 到期的 S2S 证书 | 主动 | 参阅[为服务器端 API 生成访问令牌](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials)文档，了解如何刷新凭据 |

