---
title: 使用站点面板管理站点主题
description: 了解站点面板的强大功能，帮助您轻松自定义和管理站点主题。
feature: Administering
role: Admin
exl-id: 45785e5a-4fa2-4cf2-a300-f1865f6f5807
solution: Experience Manager Sites
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 31%

---


# 使用站点面板管理站点主题 {#site-panel}

了解站点面板的强大功能，帮助您轻松自定义和管理站点主题。

## 概述 {#overview}

站点面板允许您管理站点的主题和模板资源。 [与其他面板](/help/sites-cloud/authoring/sites-console/console-side-panel.md)（如“内容树”面板、“引用”面板或“时间轴”面板）一样，“站点”面板在站点控制台中显示为最左侧的面板，显示有关选定项的信息。 与其他面板不同，“站点”面板仅适用于站点根。

站点面板用于管理站点的主题和模板相关信息，包括：

* [下载主题源](#downloading-theme-sources)
* [下载模板资源，例如线框](#downloading-template-resources)
* [查看和更改主题版本](#theme-vrsions)
* [启用前端管道](#enabling-the-front-end-pipeline)

>[!TIP]
>
>查看[快速站点创建历程](/help/journey-sites/quick-site/overview.md)以熟悉快速站点创建工具和前端管道，从而轻松自定义站点主题。

## 下载主题源 {#downloading-theme-sources}

当您基于[站点模板](site-templates.md)在AEM中创建站点时，可以使用站点面板下载[站点主题](site-themes.md)。

利用站点控制台中显示的站点面板，选择站点的根以显示有关站点的主题信息。

![下载主题源](/help/sites-cloud/administering/assets/download-theme-wireframe.png)

选择&#x200B;**下载主题源**&#x200B;以将站点主题的本地副本下载为`.zip`文件以进行自定义。

## 下载模板资源 {#downloading-template-resources}

[站点模板](site-templates.md)可以包含信息以及站点内容结构和[站点主题](site-themes.md)。 例如，站点模板可以包含线框设计或其他与站点相关的文件。

如果站点基于站点模板，利用站点控制台中显示的站点面板，选择站点的根以显示有关站点的主题信息，包括其他站点资源。

![下载主题源](/help/sites-cloud/administering/assets/download-theme-wireframe.png)

选择标题&#x200B;**下载其他模板资源**&#x200B;下的一个或多个按钮以下载可用文件的本地副本。

## 查看和更改主题版本 {#them-versions}

如果您的站点基于站点模板，则其主题可能已由前端开发人员进行自定义。使用站点面板，您可以查看当前部署的站点主题的版本并切换到以前的版本。

利用站点控制台中显示的站点面板，选择站点的根以显示有关站点的主题信息。

面板中的![站点版本](/help/sites-cloud/administering/assets/theme-versions.png)

主题的当前版本连同其提交哈希以及上次更新时间戳一起显示。

选择&#x200B;**选择版本**&#x200B;以查看主题的早期版本。

![选择主题版本](/help/sites-cloud/administering/assets/select-theme-versions.png)

选择要更改为的版本，然后选择&#x200B;**应用**&#x200B;以进行更改。

如果 AEM 检测到较新版本的主题已通过前端管道部署但未应用于您的站点，则将显示一个通知图标。

![较新版本的主题指示符](/help/sites-cloud/administering/assets/new-theme-version.png)

您可以使用&#x200B;**选择版本**&#x200B;按钮以更新到新主题版本。

## 启用前端管道 {#enabling-front-end-pipeline}

如果您的站点不是使用站点模板创建的，则无法使用前端管道来自定义和部署其主题。

但是，您可以使用站点面板为站点启用前端管道。

利用站点控制台中显示的站点面板，选择站点的根以显示有关站点的主题信息，然后选择&#x200B;**启用前端管道**。

![启用前端管道](/help/sites-cloud/administering/assets/enable-fep.png)

有关详细信息，请参阅文档[启用前端管道](enable-front-end-pipeline.md)。
