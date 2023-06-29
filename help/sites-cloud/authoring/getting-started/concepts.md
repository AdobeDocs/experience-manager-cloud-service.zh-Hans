---
title: 创作概念
description: 在 AEM 中进行创作的概念
exl-id: ee9e4952-e075-4398-b31f-d7886153efff
source-git-commit: 1473c1ffccc87cb3a0033750ee26d53baf62872f
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 39%

---

# 创作概念 {#authoring-concepts}

AEM 安装通常至少包含两个环境：

* 创作
* 发布

这些环境进行交互以使内容在您的网站上可用，以便您的访客可以访问该内容。

创作环境提供了用于在实际发布内容前创建、更新和审核该内容的机制：

* 作者创建和审阅内容。内容可以包含许多不同类型，包括页面、资源和出版物。
* 这些内容将在某一时刻发布到您的网站。

![作者、发布者和调度程序示意图](/help/sites-cloud/authoring/assets/author-publish.png)

在创作环境中，AEM的功能通过AEM创作用户界面提供。 对于发布环境，您可以设计提供给用户使用的界面的整体外观。

## 创作环境 {#author-environment}

作者在称为 **创作环境**. 此环境提供了用于创建内容的易于使用的界面(图形用户界面（GUI或UI）)。 它要求作者使用分配了相应访问权限的帐户登录。

>[!NOTE]
>
>您的帐户需要具有相应的访问权限才能创建、编辑或发布内容。

根据实例和个人访问权限的配置方式，您可以对内容执行多项任务，包括（其中包括）：

* 在页面上生成新内容或编辑现有内容
* 使用预定义模板创建内容页面
* 创建、编辑和管理资产和收藏集
* 移动、复制和删除内容页面和资产。
* 发布（或取消发布）页面和资产。

此外，还有一些管理任务可帮助您管理内容：

* 控制更改的管理方式的工作流，例如，在发布之前实施审核
* 协调各个任务的项目

>[!NOTE]
>
>AEM 也可通过创作环境进行管理。

## 预览内容 {#previewing-content}

AEM还提供站点预览服务，允许开发人员和内容作者在网站到达发布环境并公开使用之前预览网站的最终体验。

有关更多详细信息，请参阅[预览内容](/help/sites-cloud/authoring/fundamentals/previewing-content.md)。

## 发布环境 {#publish-environment}

准备就绪后，站点的内容会被发布到&#x200B;**发布环境**。在该环境中，根据设计界面的具体观感，目标受众可以使用网站页面。

有关发布和取消发布页面的更多信息，请参阅文档 [发布页面](/help/sites-cloud/authoring/fundamentals/publishing-pages.md).

## Dispatcher {#dispatcher}

要优化网站访客体验，请 **[调度程序](/help/implementing/dispatcher/overview.md)** 实施负载平衡和缓存。
