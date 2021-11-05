---
title: 站点模板
description: 了解如何使用AEM网站模板来预定义网站结构和初始内容，以便快速创建网站。
feature: Administering
role: Admin
source-git-commit: 2dd35f1ea25f6bfc515d7b50fd53cf4638af4026
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 1%

---


# 站点模板 {#site-templates}

了解如何使用AEM网站模板来预定义网站结构和初始内容，以便快速创建网站。

>[!CAUTION]
>
>快速网站创建工具当前为技术预览。 它可用于测试和评估目的，并且除非与Adobe支持部门达成协议，否则不会用于生产。

## 概述 {#overview}

使用预定义的结构可以方便地根据一组现有标准快速部署新站点。 网站模板是将基本网站内容整合到方便、可重用的包中的一种方式。

网站模板通常包含基本网站内容和结构以及网站样式信息，称为 [网站主题，](site-themes.md) 快速启动新站点。 管理员选择站点的基础站点模板 [在网站创建过程中。](create-site.md)

模板功能强大，因为它们可重复使用且可自定义。 由于AEM安装中可以有多个模板，因此您可以灵活地创建不同的站点以满足各种业务需求。

>[!NOTE]
>
>AEM网站模板不应与 [页面模板。](/help/sites-cloud/authoring/features/templates.md) 网站模板可定义网站的整体结构。 页面模板可定义单个页面的结构和初始内容。
>
>AEM网站模板不应与 [AEM网站主题。](site-themes.md) AEM网站主题仅包含AEM网站的样式信息。 AEM网站模板可定义网站结构和初始内容，并包含AEM网站主题，以便允许 [快速创建网站。](create-site.md)

## 将网站模板添加到AEM {#adding}

您可以向AEM添加多个模板，然后这些模板可用于 [创建站点。](create-site.md)

1. 登录到AEM创作环境，然后导航到站点控制台

   * `https://<your-author-environment>.adobeaemcloud.com/sites.html/content`

1. 点按或单击 **创建** 从屏幕右上方的下拉菜单中选择 **模板中的网站**.

   ![从模板创建网站](../assets/create-site-from-template.png)

1. 在创建站点向导中，点按或单击 **导入** 列的顶部。

   ![站点创建向导](../assets/site-creation-wizard.png)

1. 在文件浏览器中，找到要使用的模板，然后点按或单击 **上传**.

1. 上传后，该模板会显示在可用模板列表中。

您的模板已上传，并可用于 [创建新站点。](create-site.md)

选择现有模板时，会在右列显示有关该模板的信息。

![选择模板](../assets/select-site-template.png)

## 网站模板结构 {#structure}

站点模板只是具有明确反映包内容用途的逻辑结构的包。 网站模板具有以下结构。

* `files`:包含UI包、XD文件的文件夹，可能还包含其他文件
* `previews`:包含网站模板屏幕截图的文件夹
* `site`:为从此模板创建的每个网站（如页面模板、页面等）复制的内容包。
* `theme`:来源 [网站主题](site-themes.md) 以修改网站的外观，包括CSS、JavaScript等。

## 标准网站模板 {#standard-site-template}

Adobe提供了最佳实践参考模板，您可以将其用作创建自己模板的基础。 [GitHub上提供了标准站点模板。](https://github.com/adobe/aem-site-template-standard)

[标准网站模板的最新版本](https://github.com/adobe/aem-site-template-standard/releases) 可直接下载和用于 [创建新站点。](create-site.md)

## 开发站点模板 {#developing-templates}

Adobe将和AEM网站模板生成器作为一组用于创建新网站模板的脚本。

[提供了AEM站点模板生成器以及GitHub上的使用文档。](https://github.com/adobe/aem-site-template-builder) 自定义 [网站主题](site-themes.md) 和AEM开发人员知识是自定义网站结构和内容所必需的。
