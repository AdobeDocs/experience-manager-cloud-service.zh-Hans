---
title: 为 Edge Delivery Services 发布内容
description: 了解内容发布如何与 Edge Delivery Services 配合使用，以及如何使用 Edge Delivery Services 发布 AEM 内容。
feature: Edge Delivery Services
exl-id: 32fbb144-9175-47a9-bb5a-ca15f3fcd2d8
source-git-commit: 3ee1ba83518c3d4fba59b0c98b31e5c63a2eb6ab
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 66%

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
>每天最多允许从创作 UI 或工作流程发布 5000 个路径。不支持创建批量发布工作负载的集成。

![从 AEM 发布到 Edge Delivery Services 时的信息流](assets/publishing-flow.png)

1. 内容作者在通用编辑器中发布 AEM 内容。
1. 发布事件将推送到Adobe管道队列。
1. Edge Delivery Services发布服务将相关事件转发到Edge Delivery Services管理API。
1. Edge交付从AEM作者中提取并引入语义HTML。
1. AEM 已更新发布状态。

>[!NOTE]
>
>默认情况下，Edge Delivery Services管理API不受保护，并且可用于发布或取消发布文档而不进行身份验证。 为了配置管理员API的身份验证，如中所述 [为作者配置身份验证](https://www.aem.live/docs/authentication-setup-authoring)，您的项目必须配置API_KEY，以授予对发布服务的访问权限。 [请联系Adobe团队以了解Slack](/help/edge/docs/slack.md) 作为指导。

## 如何开始使用 {#how-to-get-started}

请联系您的 Adobe 代表以访问此功能。
