---
title: 创建站点
description: 了解如何使用 AEM 创建站点，并使用站点模板定义站点的样式和结构。
feature: Administering
role: Admin
exl-id: 9c71c167-2934-4210-abd9-ab085b36593b
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: ht
source-wordcount: '788'
ht-degree: 100%

---

# 创建站点 {#creating-site}

了解如何使用 AEM 创建站点，并使用站点模板定义站点的样式和结构。

## 概述 {#overview}

必须先创建站点，之后内容作者才能创建包含内容的页面。这通常由定义初始站点结构的 AEM 管理员执行。使用站点模板可以快速灵活地创建站点。

借助 AEM 快速站点创建工具，非开发人员可以使用站点模板从头开始快速创建新站点。

创建后，还可利用快速站点创建工具快速自定义 AEM 站点的主题和样式（JavaScript、CSS 和静态资源）。这样一来，无需了解 AEM 的前端开发人员既可独立于内容创建者工作，又可与内容创建者并行工作。AEM 管理员只需下载站点主题并将它提供给前端开发人员，后者会使用他们喜欢的工具来自定义站点主题，再将更改提交到 AEM 代码存储库，随后进行部署。

本文档重点介绍如何使用快速站点创建工具来创建站点。如果您想大致了解站点创建和自定义工作流，请参阅 [AEM 快速站点创建历程](/help/journey-sites/quick-site/overview.md)

## 规划站点结构 {#structure}

花点时间提前考虑您站点的目的以及规划的内容。这将改善站点结构的设计方式。良好的站点结构支持站点访客轻松导航和发现内容，并支持各种 AEM 功能，例如[多站点管理和翻译](/help/sites-cloud/administering/msm-and-translation.md)。

>[!TIP]
>
>[WKND 参考站点](https://wknd.site)提供功能齐全的户外体验品牌网站的最佳实践实施。探索该站点，了解构建良好的 AEM 站点的结构。

## 站点模板 {#site-templates}

由于站点结构对于站点的成功非常重要，因此使用预定义的结构可以方便地根据一组现有标准快速部署新站点。站点模板是一种将基本站点内容组合成方便且可重用的包的方法。

站点模板通常包含基本站点内容和结构以及站点样式信息，以便快速启动新站点。模板具有强大的功能，因为它们可重用和自定义。由于您可以在 AEM 安装中使用多个模板，因此可以灵活地创建不同的站点来满足各种业务需求。

>[!TIP]
>
>有关站点模板的更多详细信息，请查看[站点模板](site-templates.md)一文。

>[!NOTE]
>
>不要将站点模板与页面模板混淆。站点模板定义了站点的整体结构。页面模板定义了单个页面的结构和初始内容。

## 创建站点 {#create-site}

可以使用模板轻松创建站点。

1. 登录您的 AEM 创作环境并导航到站点控制台

   * `https://<your-author-environment>.adobeaemcloud.com/sites.html/content`

1. 点按或单击屏幕右上方的&#x200B;**创建**，然后从下拉菜单中选择&#x200B;**从模板创建站点**。

   ![从模板创建站点](../assets/create-site-from-template.png)

1. 在创建站点向导中，点按或单击左面板中的现有模板，或点按或单击左栏顶部的&#x200B;**导入**&#x200B;以导入新模板。

   ![站点创建向导](../assets/site-creation-wizard.png)

   1. 如果您已选择导入，请在文件浏览器中，找到要使用的模板并点按或单击&#x200B;**上传**。

   1. 上传模板后，该模板将显示在可用模板列表中。

1. 在选择模板时，它在右栏中显示有关模板的信息。在选定所需模板后，点按或单击&#x200B;**下一步**。

   ![选择模板](../assets/select-site-template.png)

1. 为站点提供标题。可以提供站点名称，也可以从标题生成站点名称（如果被忽略）。

   * 站点标题显示在浏览器标题栏中。
   * 站点名称会成为 URL 的一部分。
   * 站点名称必须遵循 [AEM 的页面命名惯例](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#page-name-restrictions-and-best-practices)。

1. 点按或单击&#x200B;**创建**，将从站点模板创建站点。

   ![新站点的详细信息](../assets/create-site-details.png)

1. 在显示的确认对话框中，点按或单击&#x200B;**完成**。

   ![“成功”对话框](../assets/success.png)

1. 在站点控制台中，新站点是可见的，并且可供导航以探索其由模板定义的基本结构。

   ![新站点结构](../assets/new-site.png)

内容作者现在可以开始创作！

## 站点自定义 {#site-customization}

如果您的站点需要在可用模板之外进行自定义，您将有很多选择。

* 如果需要调整站点结构或初始内容，[可以自定义站点模板以满足要求](site-templates.md)。
* 如果需要调整站点样式，[可以下载站点主题并对该主题进行自定义](/help/journey-sites/quick-site/overview.md)。
* 如果需要调整站点功能，[可以完全自定义站点](/help/implementing/developing/introduction/develop-wknd-tutorial.md)。

任何自定义都应在开发团队的支持下进行。
