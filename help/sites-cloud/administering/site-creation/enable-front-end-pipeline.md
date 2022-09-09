---
title: 启用前端管道
description: 了解如何启用现有站点的前端管道，以利用站点主题更快地自定义您的站点。
feature: Administering
role: Admin
exl-id: 55d54d72-f87b-47c9-955f-67ec5244dd6e
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 100%

---

# 启用前端管道 {#enable-front-end-pipeline}

了解如何启用现有站点的前端管道，以利用站点主题更快地自定义您的站点。

## 概述 {#overview}

前端管道是一种机制，可以根据[站点主题](site-themes.md)和[站点模板](site-templates.md)快速部署网站的前端代码。

此管道仅处理前端代码，而不是进行全栈部署，这可加快流程速度，并使前端开发人员无需了解 AEM 即可轻松快速地自定义您的站点。

默认情况下，基于站点模板的站点可以利用前端管道。本文档描述了如何调整现有站点以利用前端管道。

>[!TIP]
>
>如果您不熟悉前端管道以及如何结合使用此管道和站点模板来快速部署站点，请查看[快速站点创建历程](/help/journey-sites/quick-site/overview.md)以大致了解。

如果您尚未基于站点模板和主题创建现有站点，则 AEM 会将您的站点配置为加载使用前端管道部署在现有客户端库之上的主题。

## 技术详细信息 {#technical-details}

在激活站点的前端管道时，AEM 会对站点结构进行以下更改。

* 站点的所有页面都将包含一个额外的 CSS 和 JS 文件，可以通过专用的 Cloud Manager 前端管道部署更新来修改这些文件。
* 添加的 CSS 和 JS 文件最初是空白文件，但可以下载“主题源”文件夹以引导文件夹结构，从而让允许通过该管道部署 CSS 和 JS 代码更新。
* 此更改只能由开发人员取消执行，方式是删除 `/conf/<site-name>/sling:configs` 下由此操作创建的 `SiteConfig` 和 `HtmlPageItemsConfig` 节点。

>[!NOTE]
>
>此操作不会自动将站点的现有客户端库转换为使用前端管道。将这些源从客户端库文件夹移至前端管道文件夹是一项需要前端开发人员手动执行的任务。

## 要求 {#requirements}

AEM 可以自动调整您的现有站点以使用前端管道。要做到这一点，您的站点必须使用 [v2 或更高版本的核心组件的页面组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/page.html)。

## 启用前端管道 {#enabling}

使用[站点边栏](site-rail.md)从站点控制台启用站点。

1. 登录 AEM，然后通过&#x200B;**全局导航** > **站点**&#x200B;来导航到您的站点。
1. 在控制台中选择您的站点。您必须选择站点的根，而不是任意子页面。
1. 选择您的站点后，打开左侧的[边栏选择器](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector)，然后选择&#x200B;**站点**。
1. 在&#x200B;**站点**&#x200B;边栏中，单击&#x200B;**启用前端管道**&#x200B;按钮。

   ![启用前端管道](/help/sites-cloud/administering/assets/enable-front-end-pipeline.png)

1. AEM 会提示您确认将进行的更改的概述。确认并调整您的网站。

现在您的站点已能够使用前端管道。要了解有关前端管道和管理站点主题的更多信息，请参阅：

* [使用站点边栏管理站点主题](site-rail.md)
* [快速站点创建历程](/help/journey-sites/quick-site/overview.md) – 本文档历程为您详尽概述了使用前端管道和快速站点创建工具来快速部署站点的过程。
* [CI/CD 管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) – 本文档描述了全栈和 Web 层管道上下文中的前端管道。
