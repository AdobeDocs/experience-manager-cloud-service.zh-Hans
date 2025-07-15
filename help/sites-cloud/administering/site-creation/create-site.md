---
title: 创建站点
description: 了解如何使用 AEM 创建站点，并使用站点模板定义站点的样式和结构。
feature: Administering
role: Admin
exl-id: 9c71c167-2934-4210-abd9-ab085b36593b
solution: Experience Manager Sites
source-git-commit: 4d45e7ef626ad0b46f5323263cca791b14f9732f
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 55%

---


# 创建站点 {#creating-site}

了解如何使用 AEM 创建站点，并使用站点模板定义站点的样式和结构。

## 概述 {#overview}

必须先创建站点，之后内容作者才能创建包含内容的页面。这通常由定义初始站点结构的 AEM 管理员执行。使用站点模板可以使非开发人员快速灵活地创建站点。

## 规划站点结构 {#structure}

花点时间提前考虑您站点的目的以及规划的内容。这将改善站点结构的设计方式。良好的站点结构支持站点访客轻松导航和发现内容，并支持各种AEM功能，如[多站点管理和翻译。](/help/sites-cloud/administering/msm-and-translation.md)

## 站点模板 {#site-templates}

由于站点结构对于站点的成功非常重要，因此使用预定义的结构可以方便地根据一组现有标准快速部署新站点。站点模板是一种将基本站点内容组合成方便且可重用的包的方法。

站点模板通常包含基本站点内容和结构以及站点样式信息，以便快速启动新站点。模板具有强大的功能，因为它们可重用和自定义。由于您可以在 AEM 安装中使用多个模板，因此可以灵活地创建不同的站点来满足各种业务需求。

>[!TIP]
>
>有关站点模板的更多详细信息，请参阅文档[站点模板。](site-templates.md)

>[!NOTE]
>
>不要将站点模板与[页面模板混淆。](/help/sites-cloud/authoring/page-editor/templates.md)站点模板定义了站点的整体结构。页面模板定义了单个页面的结构和初始内容。

### Adobe提供的站点模板 {#adobe-templates}

{{adobe-templates}}

## 创建站点 {#create-site}

可以使用模板轻松创建站点。

1. 登录到您的 AEM 创作环境，并导航到 Site 控制台

   * `https://<your-author-environment>.adobeaemcloud.com/sites.html/content`

1. 在屏幕的右上角选择&#x200B;**创建**，然后从下拉菜单中选择&#x200B;**从模板创建 Site**。

   ![从模板创建站点](../assets/create-site-from-template.png)

1. 在“创建站点”向导中，在左面板中选择现有模板，或选择左列顶部&#x200B;**导入**&#x200B;以导入新模板。

   ![Site 创建向导](../assets/site-creation-wizard.png)

   1. 如果您已选择导入，请在文件浏览器中，找到要使用的模板并选择&#x200B;**上传**。

   1. 上传模板后，该模板将显示在可用模板列表中。

1. 在选择模板时，它在右栏中显示有关模板的信息。选择所需的模板后，选择&#x200B;**下一步**。

   ![选择模板](../assets/select-site-template.png)

1. 为 Site 提供标题。可以提供站点名称，也可以从标题生成站点名称（如果被忽略）。

   * Site 标题显示在浏览器标题栏中。
   * Site 名称会成为 URL 的一部分。
   * 站点名称必须遵循 [AEM 的页面命名惯例。](/help/sites-cloud/authoring/sites-console/organizing-pages.md#page-name-restrictions-and-best-practices)

1. 提供站点模板所需的其他站点详细信息。

   * 不同的模板可能需要其他详细信息。
   * 例如，[Edge Delivery Services项目](https://www.aem.live/developer/ue-tutorial)的模板需要您项目的GitHub存储库。

1. 选择&#x200B;**创建**&#x200B;并从站点模板创建站点。

   ![新 Site 的详细信息](../assets/create-site-details.png)

1. 在显示的确认对话框中，选择&#x200B;**完成**。

   ![“成功”对话框](../assets/success.png)

1. 在 Sites 控制台中，新站点是可见的，并且可供导航以探索其由模板定义的基本结构。

   ![新站点结构](../assets/new-site.png)

内容作者现在可以开始创作！

## 站点自定义 {#site-customization}

模板有助于快速设置网站的基本结构和样式。 但是，大多数项目需要额外的样式和自定义。 站点模板有助于消除站点样式的影响，以便前端开发人员无需了解AEM即可设置站点的样式，并且可以
独立于内容创建者工作并与内容创建者并行工作。 根据项目类型，这可以采用两种形式。

* 对于使用Universal Editor创作AEM页面并通过[Edge交付的项目，](/help/edge/overview.md)所有样式设置都在GitHub项目中完成。
   * 有关详细信息，请参阅文档[快速入门 — Universal Editor开发人员教程](https://www.aem.live/developer/ue-tutorial)。
* 对于通过[发布交付进行传统AEM页面创作和交付的项目，](/help/sites-cloud/authoring/author-publish.md)AEM管理员只需下载站点主题并将其提供给前端开发人员，后者会使用他们喜欢的工具对其进行自定义，然后将更改提交到AEM代码存储库，随后进行部署。
   * 有关详细信息，请参阅文档[AEM快速站点创建历程](/help/journey-sites/quick-site/overview.md)。
