---
title: 为 Edge Delivery Services 发布内容
description: 了解内容发布如何与 Edge Delivery Services 配合使用，以及如何使用 Edge Delivery Services 发布 AEM 内容。
feature: Edge Delivery Services
exl-id: 32fbb144-9175-47a9-bb5a-ca15f3fcd2d8
role: User
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: ht
source-wordcount: '294'
ht-degree: 100%

---


# 为 Edge Delivery Services 发布内容 {#publishing-edge}

利用 Edge Delivery Services，无论内容源如何，都可以无缝发布内容：

* 基于文档的内容 - 请参阅 Edge Delivery Services 文档的[发布部分](/help/edge/docs/authoring.md)。
* AEM 内容 - 请参阅下面的详细信息。

## 来自 AEM 的发布流程 {#publishing-flow}

使用通用编辑器创作 AEM 内容时，发布任务就像单击通用编辑器中的&#x200B;**发布**&#x200B;按钮一样简单。请参阅文档[使用通用编辑器发布内容。](/help/sites-cloud/authoring/universal-editor/publishing.md)

发布时的信息流程如下。当作者开始发布时，此流程就会自动进行，并会在此处进行说明以供参考。

>[!NOTE]
>
>每天最多允许从创作 UI 或工作流程发布 5000 个路径。不支持创建批量发布工作负载的集成。如果您的项目需要更高的产能，请建议加入 [VIP 项目](https://www.aem.live/vip/intake)。

![从 AEM 发布到 Edge Delivery Services 时的信息流](assets/publishing-flow.png)

1. 内容作者在通用编辑器中发布 AEM 内容。
1. 发布事件被推送到 Adobe 管道队列。
1. Edge Delivery Services 发布服务将相关事件转发到 Edge Delivery Services 管理员 API。
1. Edge Delivery 从 AEM 作者处提取和吸收语义 HTML。
1. AEM 已更新发布状态。

>[!NOTE]
>
>默认情况下，Edge Delivery Services 管理员 API 不受保护，可用于在未经身份验证的情况下发布或取消发布文档。如[配置作者身份验证](https://www.aem.live/docs/authentication-setup-authoring)中所述，为了配置管理员 API 的身份验证，您的项目必须配置 API_KEY，它授予对发布服务的访问权限。[请联系 Slack 上的 Adobe 团队](/help/edge/docs/slack.md)寻求指导。

