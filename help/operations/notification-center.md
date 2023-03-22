---
title: 通知中心
description: 利用通知中心方便地对事件和其他重要信息采取行动
hidefromtoc: true
source-git-commit: 55ecd685afa28226974f3415b550bd2e8d05e2e6
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 0%

---


# 通知中心 {#notification-center}

>[!NOTE]
>此功能尚未发布。

配置完成后，AEM as Cloud Service会发送有关客户应采取措施的重要信息的通知。 通知示例包括阻止的队列或过期的一组凭据。 可以在 [下表](#current-notification-types)，和会随着时间的推移而扩展。 通知通过电子邮件和通知小组件下的新条目接收，可通过单击Adobe Experience Cloud右上角的铃铛图标访问该小组件。 可以配置通知设置。

收到通知后，单击该通知可打开AEMas a Cloud Service的通知中心，其中有一个弹出窗口，其中显示了说明建议客户采取的操作的其他上下文。

除了显示有关刚刚点击的通知的信息外，通知中心还充当一个中心，您可以在其中查看和管理当前和旧通知集。 <!-- It can be accessed directly at the url TBD (Alexandru: I'm intentionally keeping it TBD for now so customers don't find it) -->

通知分为两个高级别：

1. 事件 — 发生了事件，通常需要及时解决。 例如，解析阻止的队列
1. 主动 — Adobe建议客户在不久的将来应采取某项操作。 例如，停止引用已弃用的UI。

请参阅 [下表](#current-notification-types) ，用于当前支持的通知。

从“通知中心”屏幕中，您可以选择对该范围进行筛选的特定程序和环境。

## 配置 {#configuration}

您可以按照以下步骤配置接收通知：

1. 按照所述创建以下产品配置文件 [在本文中](/help/journey-onboarding/notification-profiles.md)，将您组织中的相应AdobeID分配给这些用户档案。
1. 确定通知配置设置。 [在此页面上](https://experience.adobe.com/preferences/notification-section)，请确保已启用Experience Manager订阅，并且 **其他** 复选框。 此外，建议将“电子邮件”部分设置为 **即时通知** 这样，您就会在事件发生后立即收到通知。

>[!NOTE]
>订阅在组织级别起作用，因此订阅者将收到这些计划内所有计划和环境的通知。

## 详细的用户流程 {#detailed-user-flow}

单击电子邮件将会转到通知中心，弹出窗口显示您所点击通知的上下文，在某些情况下，还会显示说明如何采取纠正措施的其他信息的链接。

![事件详细信息](/help/operations/assets/incident-details.png)

单击 **了解更多** 链接会将用户导航到本文，下表中可引用该通知，该链接提供了有关采取哪些操作的指导。

在“通知中心”中，您可以看到其他最近通知的列表。 建议您使用“操作”列表确认通知，以指示Adobe您的组织知道该任务，并在以后采取纠正措施时解决通知。

![通知列表](/help/operations/assets/notification-list.png)

在大多数情况下，通知应提供解决该问题的所有必要上下文。 但是，如果Adobe支持存在问题，您可以单击 **联系支持人员** 链接。 这将显示一个表格，您可以在其中描述问题并提交它以创建支持票证，该表格还将包含对特定通知的引用，以便Adobe支持工程师具有相关上下文。

![联系支持1](/help/operations/assets/contact-support1.png)

![联系支持2](/help/operations/assets/contact-support2.png)

与所有支持票证一样，它将显示在 [Adobe Admin Console的支持案例选项卡](https://helpx.adobe.com/enterprise/using/support-for-enterprise.html)，您可以在其中跟踪并添加其他注释。

![Admin Console支持](/help/operations/assets/admin-console-support.png)

## 当前通知类型 {#current-notification-types}

下表列出了当前支持的通知类型

| 通知类型 | 相关产品配置文件 | 更正操作 |
|---|---|---|
| 阻止的复制队列 | 事件 | 按照 [复制文档](/help/operations/replication.md#troubleshooting) |
| 过期的S2S证书 | 主动 | 了解如何在 [为服务器端API文档生成访问令牌](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials) |
