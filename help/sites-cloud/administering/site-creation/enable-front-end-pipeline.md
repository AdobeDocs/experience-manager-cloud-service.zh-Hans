---
title: 启用前端管道
description: 了解如何通过发布交付为现有传统AEM创作站点启用前端管道，以使用站点主题更快地自定义您的站点。
feature: Administering
role: Admin
exl-id: 55d54d72-f87b-47c9-955f-67ec5244dd6e
solution: Experience Manager Sites
recommendations: display, noCatalog
source-git-commit: 0a458616afad836efae27e67dbe145fc44bee968
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 24%

---


# 启用前端管道 {#enable-front-end-pipeline}

{{traditional-aem}}

了解如何通过发布交付为现有传统AEM创作站点启用前端管道，以使用站点主题更快地自定义您的站点。

## 概述 {#overview}

前端管道是用于具有[发布投放](/help/sites-cloud/authoring/author-publish.md)的传统AEM创作项目的机制，它可以根据[站点主题](site-themes.md)和[站点模板快速部署网站的前端代码。](site-templates.md)

此管道仅处理前端代码，这使得部署过程比全栈部署更快。 它允许前端开发人员轻松自定义您的站点，而无需了解AEM。

默认情况下，基于站点模板的站点可以利用前端管道。本文档描述了如何调整现有站点以利用前端管道。

>[!TIP]
>
>如果您不熟悉前端管道以及如何结合使用此管道和站点模板来快速部署站点，请参阅[快速站点创建历程](/help/journey-sites/quick-site/overview.md)以了解简介。

AEM可以将站点配置为加载使用前端管道部署的主题，即使您的站点不是使用站点模板和主题创建的，方法是将其叠加到现有客户端库上。

## 技术详细信息 {#technical-details}

在激活站点的前端管道时，AEM 会对站点结构进行以下更改。

* 站点的所有页面都包含一个额外的CSS和JS文件，可以通过专用的Cloud Manager前端管道部署更新来修改这些文件。
* 添加的CSS和JS文件最初是空的。 但是，您可以下载“主题源”文件夹以设置通过管道部署CSS和JS代码更新所需的文件夹结构。
* 只有开发人员可以通过删除此操作在`SiteConfig`下创建的`HtmlPageItemsConfig`和`/conf/<site-name>/sling:configs`节点来撤消更改。

>[!NOTE]
>
>此操作不会自动将站点的现有客户端库转换为使用前端管道。 将这些源从客户端库文件夹移至前端管道文件夹是一项需要前端开发人员手动执行的任务。

## 要求 {#requirements}

AEM 可以自动调整您的现有站点以使用前端管道。若要执行此工作流，您的网站必须使用核心组件[的](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/wcm-components/page)v2或更高版本页面组件。

## 启用前端管道 {#enabling}

{{add-cm-allowlist-frontend-pipeline}}

使用[站点边栏](site-rail.md)从站点控制台启用您的站点。

1. 登录 AEM，然后通过&#x200B;**全局导航** > **站点**&#x200B;来导航到您的站点。
1. 在控制台中选择您的站点。选择站点的根，而不是任何子页面。
1. 选择您的站点后，打开左侧的[边栏选择器](/help/sites-cloud/authoring/basic-handling.md#rail-selector)，然后选择&#x200B;**站点**。
1. 在&#x200B;**站点**&#x200B;边栏中，单击&#x200B;**启用前端管道**&#x200B;按钮。

   ![启用前端管道](/help/sites-cloud/administering/assets/enable-front-end-pipeline.png)

1. AEM会提示您确认所做的更改概述。 确认并调整您的网站。

现在，您的站点已准备好使用前端管道。 要了解有关前端管道和管理站点主题的更多信息，请参阅：

* [使用站点边栏管理站点主题](site-rail.md)
* [快速站点创建历程](/help/journey-sites/quick-site/overview.md) – 本文档历程为您详尽概述了使用前端管道和快速站点创建工具来快速部署站点的过程。
* [CI/CD 管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) – 本文档描述了全栈和 Web 层管道上下文中的前端管道。

## 前端管道和自定义域 {#custom-domains}

前端管道可以与[Cloud Manager的自定义域功能](/help/implementing/cloud-manager/custom-domain-names/introduction.md)一起使用，但将这两项功能一起使用时，请注意以下要求。

### 静态前端文件 {#static-files}

默认情况下，通过Front-End Pipeline部署的静态前端资源将由Adobe的预定义静态域提供服务。

如果前端资源需要自定义域，则可以在发布层上安装自定义域，并配置Dispatcher以将特定路径（如`/static/`）路由到Adobe的静态托管位置。 此方法需要更新您的[Dispatcher规则](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-dispatcher/using/dispatcher)，以正确转发和缓存静态资源的请求。

配置自定义域和Dispatcher后，您可以配置AEM以从静态域为前端资源提供服务。

### 配置 {#configuration}

如[技术详细信息](#technical-details)部分中所述，为站点激活前端管道功能会在`SiteConfig`下创建`HtmlPageItemsConfig`和`/conf/<site-name>/sling:configs`节点。

如果您希望将适用于您的站点的Cloud Manager自定义域功能与用于状态资源的前端管道结合使用，则必须将其他属性添加到这些节点。

1. 在`customFrontendPrefix`中为站点设置`SiteConfig`属性。
   1. 导航到 `/conf/<site-name>/sling:configs/com.adobe.aem.wcm.site.manager.config.SiteConfig`。
   1. 添加或更新属性`customFrontendPrefix = "https://your-custom-domain.com/static/"`。
1. 这会使用自定义域更新`prefixPath`的`HtmlPageItemsConfig`值。
   1. 导航到 `/conf/<site-name>/sling:configs/com.adobe.cq.wcm.core.components.config.HtmlPageItemsConfig`。
   1. 验证`prefixPath`是否反映了您的自定义域，如`prefixPath = "https://your-custom-domain.com/static/<hash>/..."`。
   * 需要时也可以手动覆盖此值。
1. 验证设置。
   1. 部署后，检查页面是否正确引用了自定义域中的主题工件。
   1. 打开浏览器的开发人员工具并检查`theme.css`和`theme.js`文件路径以确认它们是从正确的域加载的。

站点的页面，然后引用该更新URL中的主题工件。 然后，Dispatcher将这些资源的请求路由到静态域。

## 面向前端开发人员的最佳实践 {#best-practices}

如果在通过前端管道进行部署之前需要在本地开发和测试前端资产，请考虑以下方法：

* 使用[站点主题生成器的代理模式](https://github.com/adobe/aem-site-theme-builder?tab=readme-ov-file#proxy)在本地覆盖主题工件以进行测试。
* 从本地开发服务器手动提供主题文件并更新`prefixPath`中的`HtmlPageItemsConfig`以匹配本地服务器地址。
* 确保在测试期间禁用浏览器缓存以查看实时更新。

有关本地前端开发的更多详细信息，请参阅[站点主题生成器文档。](https://github.com/adobe/aem-site-theme-builder)
