---
title: 操作中心
description: 利用行动中心方便地对事件和其他重要信息采取行动
exl-id: d5a95ac4-aa88-44d5-ba02-7c9702050208
feature: Operations
role: Admin
source-git-commit: 22d5975a0c4ee180bbcda906b035d306a352b752
workflow-type: tm+mt
source-wordcount: '1045'
ht-degree: 56%

---

# 操作中心 {#actions-center}

AEM as Cloud Service 在发生需要立即采取行动的关键事件时会发送“操作中心”电子邮件通知，并主动提出优化建议。示例包括阻塞队列或一组即将过期的凭据；可在[下表](#supported-notification-types)中查看完整的“操作中心”通知类型集，此表也会随着时间不断扩充。

在收到操作中心电子邮件通知后，可以单击该通知以打开AEM as a Cloud Service的操作中心，此时会显示一个弹出窗口，其中显示了说明客户应采取的操作的附加上下文。

除了显示有关刚刚单击的电子邮件通知的信息外，“操作中心”还充当可供查看和管理一组当前和过往通知的中心。<!-- It can be accessed directly at the url TBD (Alexandru: I'm intentionally keeping it TBD for now so customers do not find it) -->

“操作中心”中会显示两个高级类别的通知：

1. 操作问题 – 已发生事件，通常需要及时予以解决。例如，解决锁定队列。
1. 主动建议 – Adobe 对客户在不久的将来应采取的行动提出了建议。例如，停止引用已弃用的 UI。

有关“操作中心”当前支持的通知，请参阅[下表](#supported-notification-types)。

通过“操作中心”，您可以选择特定的程序和环境，这将对范围有筛选效果。

## 配置 {#configuration}

要配置接收“操作中心”电子邮件通知的功能，请创建[本文中](/help/journey-onboarding/notification-profiles.md)讲解的“产品配置文件”，即事件通知 - Cloud Service和主动通知 - Cloud Service。此外，还要将组织的相应 Adobe ID 分配给这些配置文件。这允许管理员确定哪些用户有资格接收这些电子邮件通知。

>[!NOTE]
>“操作中心”电子邮件通知在组织级别运行，因此，订阅者将收到有关所有程序以及这些程序中的环境的通知。

## 详细的用户流程 {#detailed-user-flow}

单击电子邮件即可进入“操作中心”，此时会出现一个弹出窗口，其中显示您单击的通知的上下文，在某些情况下，还会显示描述如何采取更正操作的其他信息的链接。 您也可以直接访问“操作中心”（网址为 [https://experience.adobe.com/aem/actions-center](https://experience.adobe.com/aem/actions-center/)），并且可在其中选择相关的程序和环境。

![问题详细信息](/help/operations/assets/incident-details.png)

单击&#x200B;**了解更多**&#x200B;链接可将用户导航至本文，可参考以下[受支持的通知类型列表](#supported-notification-types)中的通知类型，其中提供了有关执行哪项操作的指南。

在“操作中心”，您可以查看其他最新通知的列表。建议使用“操作”列表来确认通知，以便向 Adobe 表明您的组织已了解该任务，并稍后在采取纠正措施后解决该通知。

![通知列表](/help/operations/assets/notification-list.png)

在大多数情况下，弹出窗口应该提供解决问题所需的所有上下文。 但是，如果对Adobe支持存在疑问，您可以单击弹出窗口中的&#x200B;**联系支持人员**&#x200B;链接。 这将弹出一个表单，您可以在其中描述并提交问题，以创建支持工单，它还将包含对特定通知的引用，以便 Adobe 支持工程师能够了解相关情况。

![联系支持人员 1](/help/operations/assets/contact-support1.png)

![联系支持人员 2](/help/operations/assets/contact-support2.png)

与所有支持工单一样，它将出现在 [Adobe Admin Console 的“支持案例”选项卡](https://helpx.adobe.com/cn/enterprise/using/support-for-enterprise.html)中，您可以在其中跟踪它并添加其他评论。

![Admin Console 支持](/help/operations/assets/admin-console-support.png)

## 将出现哪些通知？ {#which-notification}

AEM as a Cloud Service 有多种类型的通知，但只有一部分会出现在“操作中心”，如下表中所示。

| 通知类型 | 描述 | 如何配置 | 出现在操作中心 |
|---------------------------------|-----------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------|
| 操作问题 | 需要立即采取行动的关键问题 | 分配给“事件通知 - Cloud Service”产品配置文件的用户 | X |
| 主动建议 | 应该计划的优化 | 分配给“主动通知 - Cloud Service”产品配置文件的用户 | X |
| Cloud Manager 管道状态 | 有关您的管道状态的信息 | 在[Experience Cloud首选项](https://experience.adobe.com/preferences)中选中了业务负责人、项目管理员或部署管理员角色的“其他”复选框的用户，如此处[所述](/help/implementing/cloud-manager/notifications.md)。 |                           |

## 支持的通知类型 {#supported-notification-types}

下表列出了“操作中心”当前支持的通知类型。通知目前仅适用于生产环境。

| 通知类型 | 相关产品配置文件 | 纠正措施 |
|---------------------------------|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 已锁定的复制队列 | 问题 | 按照[复制文档](/help/operations/replication.md#troubleshooting)中的说明执行操作来解锁队列 |
| 持久GraphQL查询无效 | 问题 | 通过引用[持久的GraphQL查询疑难解答文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/headless/graphql-api/persisted-queries-troubleshoot.html)修复无效的GraphQL查询 |
| 源头流量尖峰 | 问题 | 通过配置速率限制流量过滤器规则来Protect您的来源，这些规则在低于默认来源流量尖峰警报的阈值时触发。  请参阅引用了教程的流量过滤器规则文档中的[使用流量规则阻止DoS和DDoS攻击](/help/security/traffic-filter-rules-including-waf.md#blocking-dos-and-ddos-attacks-using-traffic-filter-rules)部分。 |
| 已触发CDN流量过滤器规则 | 问题 | 如果匹配的流量过滤器规则反映的是攻击，并且您的网站没有阻止该流量，请通过在阻止模式下配置流量过滤器规则来保护您的网站。 请参阅引用了教程的流量过滤器规则文档的[使用流量过滤器规则(包括WAF规则)保护网站](/help/security/traffic-filter-rules-including-waf.md#tutorial-protecting-websites)部分。 |
| 页面包含大量节点 | 主动 | 减少页面中的节点总数。 请参阅[页面复杂性文档](https://experienceleague.adobe.com/en/docs/experience-manager-pattern-detection/table-of-contents/pcx) | |
| 大量正在运行的工作流实例 | 主动 | 终止不再需要的正在运行的工作流。 了解如何[配置清除作业](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/operations/maintenance) |               |
| 到期的 S2S 证书 | 主动 | 参阅[为服务器端 API 生成访问令牌](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials)文档，了解如何刷新凭据 | 高连接数 | 主动 | 与高级联网文档](/help/security/configuring-advanced-networking.md#connection-pooling-advanced-networking)一起了解[连接池中的连接池 |
| 已弃用的服务用户映射 | 主动 | 了解如何使用新的Sling服务用户映射格式，如[Sling服务用户映射和服务用户定义的最佳实践](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/best-practices-for-sling-service-user-mapping-and-service-user-definition)中所述 |
| 高连接数 | 主动 | 在[高级联网文档](/help/security/configuring-advanced-networking.md#connection-pooling-advanced-networking)中了解连接池 |  |
| 直接添加到自定义组的用户 | 主动 | 需要将用户添加到相关的IMS组，并且这些IMS组需要添加为AEM组的成员。 与[IMS最佳实践保持一致](/help/security/ims-support.md) | |
| 缺少JCR内容 | 主动 | 添加缺失的JCR内容节点。 请参阅[Assets内容验证器文档](https://experienceleague.adobe.com/en/docs/experience-manager-pattern-detection/table-of-contents/acv) | |
| 未清除已完成的工作流 | 主动 | 通过清除已超过90天的工作流实例，最大程度地减少工作流实例数并提高性能。 了解如何[配置维护任务](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/operations/maintenance) | |
| 页面中缺少Sling资源类型 | 主动 | 添加缺少的Sling资源类型节点。 请参阅[Assets内容验证器文档](https://experienceleague.adobe.com/en/docs/experience-manager-pattern-detection/table-of-contents/acv) |
