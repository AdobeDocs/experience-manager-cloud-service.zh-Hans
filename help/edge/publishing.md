---
title: 发布Edge Delivery Services内容
description: 了解内容发布如何与Edge Delivery Services配合使用以及如何使用Edge Delivery Services发布AEM内容。
feature: Edge Delivery Services
source-git-commit: 166525b6987215a64521d1ff63a222187376ba65
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---


# 发布Edge Delivery Services内容 {#publishing-edge}

使用Edge Delivery Services，无论您的内容来源如何，都可以无缝发布内容：

* 基于文档的内容 — 请参阅 [发布部分](/help/edge/docs/authoring.md) 的Edge Delivery Services文档。
* AEM内容 — 请查看以下详细信息。

## 从AEM发布流 {#publishing-flow}

使用通用编辑器创作AEM内容时，发布就像单击 **Publish** 按钮。 请参阅文档 [使用通用编辑器发布内容。](/help/implementing/universal-editor/publishing.md)

发布时的信息流如下所示。 作者开始发布后，此流程将自动完成，此处进行了说明以供参考。

![从AEM发布到Edge Delivery Services时的信息流](assets/publishing-flow.png)

1. 内容作者在通用编辑器中发布AEM内容。
1. 发布事件将推送到Adobe管道队列。
1. 边缘交付发布服务将相关事件转发到边缘交付管理员API。
1. Edge交付从AEM Author中提取并引入语义HTML。
1. AEM更新了发布状态。

## 如何入门 {#how-to-get-started}

请联系您的Adobe代表以获取此功能的访问权限。
