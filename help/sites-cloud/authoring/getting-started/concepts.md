---
title: 创作概念
description: 在 AEM 中进行创作的概念
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# 创作 概念 {#authoring-concepts}

AEM安装通常至少包含两个环境：

* 创作
* 发布

这些交互使您能够在网站上提供内容，以便您的访客能够访问它。

创作环境提供了在实际发布内容之前创建、更新和审阅此内容的机制：

* 作者创建和审阅内容。 内容可以有许多不同的类型，如页面、资产、出版物等。
* 此内容将在某个时候发布到您的网站。

![作者、发布者和调度员示意图](/help/sites-cloud/authoring/assets/author-publish.png)

在创作环境中，AEM的功能通过AEM的创作UI提供。 对于发布环境，可以设计提供给用户使用的界面的整体外观。

>[!NOTE]
>
>AEM本身用于发布AEM文档。

## 创作环境 {#author-environment}

作者在称为创作环境的环境 **中工作**。这为创建内容提供了易于使用的界面(图形用户界面（GUI或UI）)。 它要求作者使用分配了相应访问权限的帐户登录。

>[!NOTE]
>
>您的帐户需要适当的访问权限才能创建、编辑或发布内容。

根据您的实例和个人访问权限的配置方式，您可以对内容执行许多任务，其中包括（但不限于）：

* 生成新内容或编辑页面上的现有内容
* 使用预定义的模板创建新内容页面
* 创建、编辑和管理资产和收藏集
* 移动、复制和删除内容页面、资产等。
* 发布（或取消发布）页面、资产等。

此外，还有一些管理任务可帮助管理内容：

* 控制更改管理方式的工作流，如在发布前强制执行审阅
* 协调单个任务的项目

>[!NOTE]
>
>AEM也通过创作环境进行管理。

## 发布环境 {#publish-environment}

When ready, your site&#39;s content is published to the **publish environment**. 此处，根据设计界面的外观和风格，网站页面可供目标受众使用。

有关发布和取消发布页面的详细信息，请参阅文档发 [布页面。](/help/sites-cloud/authoring/fundamentals/publishing-pages.md)

## Dispatcher {#dispatcher}

To optimize performance for visitors to your website, the **[dispatcher](/help/implementing/dispatcher/overview.md)**implements load balancing and caching.
