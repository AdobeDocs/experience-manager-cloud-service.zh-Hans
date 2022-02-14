---
title: 启用前端管道
description: 了解如何为现有网站启用前端管道，以便利用网站主题更快地自定义您的网站。
feature: Administering
role: Admin
source-git-commit: dc7e89c601bb02c78f65ca58eff34c15092b5561
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---


# 启用前端管道 {#enable-front-end-pipeline}

了解如何为现有网站启用前端管道，以便利用网站主题更快地自定义您的网站。

## 概述 {#overview}

前端管道是一种机制，可根据 [网站主题](site-themes.md) 和 [网站模板。](site-templates.md)

此管道不部署全栈，而是仅处理前端代码，从而加快了处理过程，并且前端开发人员无需了解AEM即可轻松、快速地自定义您的网站。

默认情况下，基于站点模板的站点可以利用前端管道。 本文档介绍如何调整现有站点以利用前端管道。

>[!TIP]
>
>如果您不熟悉前端管道以及如何使用前端管道和站点模板快速部署站点，请查看 [快速网站创建历程](/help/journey-sites/quick-site/overview.md) 介绍。

如果您尚未基于网站模板和主题创建现有网站，则AEM可以将您的网站配置为在现有客户端库的基础上加载通过前端管道部署的主题。

## 要求 {#requirements}

AEM可以自动调整您的现有站点以使用前端管道。 要执行此操作，您的网站必须使用 [核心组件的页面组件的v2或更高版本。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/page.html)

## 启用前端管道 {#enabling}

可从站点控制台中启用您的站点。

1. 登录AEM，然后通过 **全局导航** > **站点**.
1. 在控制台中选择您的站点。 必须选择站点的根，而不是任何子页面。
1. 选择您的网站后，打开 [边栏选择器](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector) 选择 **网站**.
1. 在 **网站** 边栏，单击按钮 **启用前端管道**.

   ![启用前端管道](/help/sites-cloud/administering/assets/enable-front-end-pipeline.png)

1. AEM会提示您进行确认，并概述将要进行的更改。 确认并调整您的网站。

现在，您的站点已准备好使用前端管道。 要了解有关前端管道的更多信息，请参阅：

* [快速网站创建历程](/help/journey-sites/quick-site/overview.md)  — 此文档历程从头到尾概述了使用前端管道和快速站点创建工具快速部署站点的过程。
* [CI/CD管线](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end)  — 本文档介绍全栈和Web层管道上下文中的前端管道。
