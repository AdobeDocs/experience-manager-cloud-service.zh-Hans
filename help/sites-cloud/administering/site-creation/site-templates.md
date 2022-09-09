---
title: 站点模板
description: 了解如何使用 AEM 站点模板来预定义站点结构和初始内容，以便您快速创建站点。
feature: Administering
role: Admin
exl-id: 42eec922-b02e-4f2c-8107-7336192919c7
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 100%

---

# 站点模板 {#site-templates}

了解如何使用 AEM 站点模板来预定义站点结构和初始内容，以便您快速创建站点。

## 概述 {#overview}

使用预定义的结构可以方便地根据一组现有标准快速部署新站点。站点模板是一种将基本站点内容组合成方便且可重用的包的方法。

站点模板通常包含基本站点内容和结构以及站点样式信息（称作[站点主题](site-themes.md)），以便快速启动新站点。管理员可以在[站点创建过程中](create-site.md)选择站点模板作为站点的基础。

模板具有强大的功能，因为它们可重用和自定义。由于您可以在 AEM 安装中使用多个模板，因此可以灵活地创建不同的站点来满足各种业务需求。

>[!NOTE]
>
>不应混淆 AEM 站点模板与[页面模板。](/help/sites-cloud/authoring/features/templates.md)站点模板定义了站点的整体结构。页面模板定义了单个页面的结构和初始内容。
>
>不应混淆 AEM 站点模板与 [AEM 站点主题。](site-themes.md)AEM 站点主题仅包含 AEM 站点的样式信息。AEM 站点模板定义站点结构和初始内容，并包含 AEM 站点主题，以便[快速创建站点](create-site.md)。

## 将站点模板添加到 AEM {#adding}

您可以将多个模板添加到 AEM，然后将其用于[创建站点](create-site.md)。

1. 登录您的 AEM 创作环境并导航到站点控制台

   * `https://<your-author-environment>.adobeaemcloud.com/sites.html/content`

1. 点按或单击屏幕右上方的&#x200B;**创建**，然后从下拉菜单中选择&#x200B;**从模板创建站点**。

   ![从模板创建站点](../assets/create-site-from-template.png)

1. 在创建站点向导中，点按或单击左栏顶部的&#x200B;**导入**。

   ![站点创建向导](../assets/site-creation-wizard.png)

1. 在文件浏览器中，找到要使用的模板并点按或单击&#x200B;**上传**。

1. 上传模板后，该模板将显示在可用模板列表中。

您的模板将上传，并且可用于[创建新站点](create-site.md)。

在选择现有模板时，它在右栏中显示有关模板的信息。

![选择模板](../assets/select-site-template.png)

## 站点模板结构 {#structure}

站点模板只是带有逻辑结构的包，它清楚地反映了包内容的目的。站点模板具有以下结构。

* `files`：包含 UI 套件、XD 文件和可能的其他文件的文件夹
* `previews`：包含站点模板的屏幕截图的文件夹
* `site`：为从此模板创建的每个站点复制的内容的内容包，例如页面模板、页面等
* `theme`：用于修改站点外观的[站点主题](site-themes.md)的来源，包括 CSS、JavaScript 等

## 标准站点模板 {#standard-site-template}

Adobe 提供了一个最佳实践参考模板，您可以基于此模板创建自己的模板。[GitHub 上提供了标准站点模板](https://github.com/adobe/aem-site-template-standard)。

可以下载[最新版本的标准站点模板](https://github.com/adobe/aem-site-template-standard/releases)，并可直接使用它[创建新站点](create-site.md)。

## 开发站点模板 {#developing-templates}

Adobe 提供 AEM 站点模板生成器作为一组用于创建新站点模板的脚本。

[GitHub 上提供了 AEM 站点模板生成器与使用文档。](https://github.com/adobe/aem-site-template-builder)自定义[站点主题](site-themes.md)需要前端开发人员经验，自定义站点结构和内容需要 AEM 开发人员知识。
