---
title: 创作和发布概念
description: 了解在AEM中使用创作、预览和发布环境进行创作的概念。
exl-id: ee9e4952-e075-4398-b31f-d7886153efff
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 29%

---


# 创作和发布概念 {#authoring-publishing}

对于内容作者，可以将AEM as a Cloud Service安装视为其最基础级别的三个主要层

* 创作层
* 预览层
* Publish层

这些层进行交互以使内容在您的网站上可用，以便您的访客可以访问该内容。 基本的工作流程是：

1. 内容作者使用创作层创建其内容。
1. 内容作者可使用预览层来预览其内容，以供审阅人预览。
1. 内容可供公众使用后，作者将使用发布层发布内容。

内容可以包含多种类型，包括页面、资源和出版物。 根据作者的决定，可以跳过预览内容。

![作者、发布者和调度程序示意图](assets/author-publish.jpg)

有关AEM as a Cloud Service技术架构的更多详细信息，请参阅文档[Adobe Experience Manager as a Cloud Service架构简介。](/help/overview/architecture.md)

{{edge-delivery-authoring}}

## 创作内容 {#author-environment}

创作层的创作环境为创建内容提供了一个易于使用的图形用户界面。 它要求作者使用分配了相应访问权限的帐户登录。

根据您的实例和个人访问权限的配置方式，您可以对内容执行许多任务，其中包括（但不限于）：

* 在页面上生成新内容或编辑现有内容
* 使用预定义模板来创建内容页面
* 创建、编辑和管理资源和收藏集
* 移动、复制和删除内容页面和资源。
* 发布（或取消发布）页面和资源。

此外，还有一些管理任务可帮助管理内容：

* 控制更改的管理方式的工作流程，例如，在发布之前实施审核
* 协调各个任务的项目

AEM 也可通过创作环境进行管理。

有关创作过程的概述，请参阅文档[创作快速入门指南](/help/sites-cloud/authoring/quick-start.md)。

## 预览内容 {#previewing-content}

AEM还提供了预览服务，可让开发人员和内容作者在网站到达发布环境并公开使用之前预览网站的最终体验。

有关详细信息，请参阅文档[预览内容](/help/sites-cloud/authoring/sites-console/previewing-content.md)。

## 发布环境 {#publish-environment}

准备就绪后，站点的内容会被发布到发布层的发布环境。 在此，根据内容模板的外观，目标受众可以使用网站页面。

有关发布和取消发布页面的详细信息，请参阅文档[发布页面](/help/sites-cloud/authoring/sites-console/publishing-pages.md)。

## Dispatcher {#dispatcher}

为了优化网站访问性能，**[Dispatcher](/help/implementing/dispatcher/overview.md)**&#x200B;为发布层和预览层实施了负载平衡和缓存。
