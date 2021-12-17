---
title: 站点主题
description: 了解如何使用AEM网站主题自定义网站的样式和设计。
feature: Administering
role: Admin
source-git-commit: 0b00d579886a106f5f66cfc54d90eab9563724cd
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 1%

---


# 站点主题 {#site-themes}

了解如何使用AEM网站主题自定义网站的样式和设计。

## 概述 {#overview}

AEM网站主题是包含CSS、JavaScript和静态资源的包，用于定义AEM网站的样式并符合AEM网站主题的结构。

使用AEM站点模板创建的站点允许轻松下载、自定义和重新部署主题。

>[!NOTE]
>
>AEM网站主题不应与 [AEM网站模板。](site-templates.md) AEM网站主题仅包含AEM网站的样式信息。 AEM网站模板可定义网站结构和初始内容，并包含AEM网站主题，以便允许 [快速创建网站。](create-site.md)

## 使用网站主题 {#using-themes}

网站主题的使用方式有两种：

* 在 [创建网站。](create-site.md)
* 在基于网站模板创建网站后，会下载这些内容，以便前端开发人员可以进一步自定义样式。

>[!TIP]
>
>有关从模板创建网站并自定义其主题的过程的端到端描述，请参阅 [快速创建网站历程。](/help/journey-sites/quick-site/overview.md)

## 网站主题结构 {#structure}

网站主题只是具有明确反映资源包内容用途的逻辑结构的资源包。 站点主题具有以下前端项目的典型结构。

* `src/main.ts`:JS和CSS主题的主要入口点
* `src/site`:应用于整个网站的JS和CSS文件
* `src/components`:特定于AEM组件的JS和CSS文件
* `src/resources`:静态文件，如图标、徽标和字体

## 标准网站主题 {#standard-site-theme}

Adobe提供了最佳实践参考主题，您可以将其用作创建自己主题的基础。 [GitHub上提供了标准网站主题。](https://github.com/adobe/aem-site-template-standard-theme-e2e)

## 开发网站主题 {#developing-themes}

Adobe将AEM网站主题生成器作为一组用于创建新网站主题的脚本。

[提供了AEM Site Theme Builder以及GitHub上的使用文档。](https://github.com/adobe/aem-site-theme-builder) 自定义主题需要具备前端开发体验。
