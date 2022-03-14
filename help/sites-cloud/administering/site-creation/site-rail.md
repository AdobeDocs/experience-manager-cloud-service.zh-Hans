---
title: 使用站点边栏管理站点主题
description: 了解网站边栏的强大功能，帮助您轻松自定义和管理网站主题。
feature: Administering
role: Admin
exl-id: 45785e5a-4fa2-4cf2-a300-f1865f6f5807
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 0%

---

# 使用站点边栏管理站点主题 {#site-rail}

了解网站边栏的强大功能，帮助您轻松自定义和管理网站主题。

## 概述 {#overview}

利用站点边栏，可管理站点的主题和模板资源。 [像其他导轨一样](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector) 如“内容树”、“引用”或“时间轴”边栏，“站点”边栏将显示为站点控制台中最左侧的面板，其中显示了有关选定项目的信息。 与其他边栏不同，站点边栏仅适用于站点根。

站点边栏用于管理网站的主题和模板相关信息，包括：

* [下载主题源](#downloading-theme-sources)
* [下载模板资源，如线框](#downloading-template-resources)
* [查看和更改主题版本](#theme-vrsions)
* [启用前端管道](#enabling-the-front-end-pipeline)

>[!TIP]
>
>查看 [快速网站创建历程](/help/journey-sites/quick-site/overview.md) 熟悉快速站点创建工具和前端管道，以便轻松自定义站点主题。

##  下载主题源 {#downloading-theme-sources}

在AEM中根据 [网站模板，](site-templates.md) 您可以下载 [网站主题](site-themes.md) 使用“站点”边栏。

站点控制台中显示站点边栏后，选择站点的根以显示有关站点的主题信息。

![下载主题源](/help/sites-cloud/administering/assets/download-theme-wireframe.png)

点按或单击 **下载主题源** 将网站主题的本地副本下载为 `.zip` 文件进行自定义。

##  下载模板资源 {#downloading-template-resources}

[网站模板](site-templates.md) 可包含网站内容结构和 [网站主题。](site-themes.md) 网站模板可以包含线框设计或其他与网站相关的文件。

如果您的网站基于站点模板，并且站点控制台中显示了站点边栏，请选择站点的根以显示有关站点的主题信息，包括其他站点资源。

![下载主题源](/help/sites-cloud/administering/assets/download-theme-wireframe.png)

点按或单击标题下方的按钮 **下载其他模板资源** 下载可用文件的本地副本。

## 查看和更改主题版本 {#them-versions}

如果您的网站基于网站模板，则其主题可能已经由前端开发人员自定义。 使用“站点”边栏，您可以查看当前部署的站点主题版本，并切换到以前的版本。

站点控制台中显示站点边栏后，选择站点的根以显示有关站点的主题信息。

![边栏中的网站版本](/help/sites-cloud/administering/assets/theme-versions.png)

主题的当前版本会显示其提交哈希及其上次更新的时间戳。

点按或单击 **选择版本** 查看主题的早期版本。

![选择主题版本](/help/sites-cloud/administering/assets/select-theme-versions.png)

点按或单击要更改的版本，然后点按或单击 **应用** 来做出改变。

如果AEM检测到已通过前端管道部署了较新版本的主题，但该主题未应用于您的网站，则会显示通知图标。

![较新版本的主题指示器](/help/sites-cloud/administering/assets/new-theme-version.png)

您可以使用 **选择版本** 按钮以更新到新主题版本。

## 启用前端管道 {#enabling-front-end-pipeline}

如果您的网站不是使用网站模板创建的，则无法使用前端管道来自定义和部署其主题。

但是，您可以使用站点边栏为站点启用前端管道。

在站点控制台中显示站点边栏时，选择站点的根以显示有关站点的主题信息，然后点按或单击 **启用前端管道**.

![启用前端管道](/help/sites-cloud/administering/assets/enable-fep.png)

有关详细信息，请参阅文档 [启用前端管道。](enable-front-end-pipeline.md)
