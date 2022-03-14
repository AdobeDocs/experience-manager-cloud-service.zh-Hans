---
title: 启用前端管道
description: Learn how you can enable the front-end pipeline for existing sites to leverage site themes to more quickly customize your site.
feature: Administering
role: Admin
exl-id: 55d54d72-f87b-47c9-955f-67ec5244dd6e
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---

# 启用前端管道 {#enable-front-end-pipeline}

Learn how you can enable the front-end pipeline for existing sites to leverage site themes to more quickly customize your site.

## 概述 {#overview}

The front-end pipeline is a mechanism that can quickly deploy just the front-end code of your websites based on [site themes](site-themes.md) and [site templates.](site-templates.md)

此管道不部署全栈，而是仅处理前端代码，从而加快了处理过程，并且前端开发人员无需了解AEM即可轻松、快速地自定义您的网站。

Sites based on site templates can leverage the front-end pipeline by default. 本文档介绍如何调整现有站点以利用前端管道。

>[!TIP]
>
>If you are not familiar with the front-end pipeline and how to quickly deploy sites using it and site templates, please review the [Quick Site Creation journey](/help/journey-sites/quick-site/overview.md) for an introduction.

If you have not created your existing site based on site templates and themes, AEM can configure your site to load the themes that are deployed with the Front End Pipeline on top of the existing client libraries.

## 技术详细信息 {#technical-details}

在激活站点的前端管道时，AEM会对您的站点结构进行以下更改。

* All pages of the site will include one additional CSS and JS file, which can be modified by deploying updates through a dedicated Cloud Manager front-end pipeline.
* 添加的CSS和JS文件最初将为空，但可以下载“主题源”文件夹以引导文件夹结构，该结构允许通过该管道部署CSS和JS代码更新。
* 此更改只能由开发人员通过删除 `SiteConfig` 和 `HtmlPageItemsConfig` 此操作将在下面创建的节点 `/conf/<site-name>/sling:configs`.

>[!NOTE]
>
>此操作不会自动转换站点的现有客户端库以使用字体端管道。 Moving these sources from the client library folder to the front-end pipeline folder is a task that requires manual work by a front-end developer.

## 要求 {#requirements}

AEM can automatically adapt your existing site to use the front-end pipeline. To be able to do this, your site must use [v2 or newer of the Page Component of the Core Components.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/page.html)

## 启用前端管道 {#enabling}

Enabling your site is done from the Sites console using the [Site rail.](site-rail.md)

1. Log into AEM and navigate to your site via **Global Navigation** > **Sites**.
1. Select your site in the console. You must select the root of the site and not any child pages.
1. With your site selected, open the [rail selector](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector) at the left and choose **Site**.
1. In the **Site** rail, click the button **Enable Front End Pipeline**.

   ![启用前端管道](/help/sites-cloud/administering/assets/enable-front-end-pipeline.png)

1. AEM会提示您进行确认，并概述将要进行的更改。 确认并调整您的网站。

现在，您的站点已准备好使用前端管道。 要了解有关前端管道和管理站点主题的更多信息，请参阅：

* [使用站点边栏管理站点主题](site-rail.md)
* [快速网站创建历程](/help/journey-sites/quick-site/overview.md)  — 此文档历程从头到尾概述了使用前端管道和快速站点创建工具快速部署站点的过程。
* [CI/CD管线](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end)  — 本文档介绍全栈和Web层管道上下文中的前端管道。
