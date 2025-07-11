---
title: 站点主题
description: 了解如何使用 AEM 站点主题来自定义站点的样式和设计。
feature: Administering
role: Admin
exl-id: 53d4afb3-d091-47a1-ba12-5bcec99f46b9
solution: Experience Manager Sites
source-git-commit: 34c2604c7dcc2a1b27f617fe2d88eeb7496b3456
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 86%

---

# 站点主题 {#site-themes}

{{traditional-aem}}

了解如何使用 AEM 站点主题来自定义站点的样式和设计。

## 概述 {#overview}

AEM 站点主题是一个包，其中包含的 CSS、JavaScript 和静态资源定义了 AEM 站点样式并符合 AEM 站点主题结构。

使用 AEM 站点模板创建的站点允许轻松下载、自定义和重新部署主题。

>[!NOTE]
>
>不应混淆 AEM 站点主题与 [AEM 站点模板。](site-templates.md)AEM 站点主题仅包含 AEM 站点的样式信息。AEM 站点模板定义站点结构和初始内容，并包含 AEM 站点主题，以便[快速创建站点。](create-site.md)

## 使用站点主题 {#using-themes}

通过两种不同的方式使用站点主题：

* 它们在[创建站点](create-site.md)时用作站点模板的一部分来定义样式。
* 它们是在基于站点模板创建站点后下载的，因此，前端开发人员可以进一步自定义样式。

>[!TIP]
>
>可以在[快速站点创建历程](/help/journey-sites/quick-site/overview.md)中找到从模板创建站点并自定义其主题的过程的端到端描述。

## 站点主题结构 {#structure}

站点主题只是带有逻辑结构的包，它清楚地反映了包内容的目的。对于典型的前端项目，Adobe建议为站点主题使用以下结构：

* `src/theme.ts`：JS &amp; CSS 主题的主要入口点
* `src/site`：应用于整个 Site 的 JS &amp; CSS 文件
* `src/components`：特定于 AEM 组件的 JS &amp; CSS 文件
* `src/resources`：图标、徽标和字体等静态文件

根据特定项目需求，只要保留主入口点`src/theme.ts`，您的主题结构可能会有所不同。

## 标准站点主题 {#standard-site-theme}

Adobe 提供了一个最佳实践参考主题，您可以基于此主题创建自己的主题。[标准站点主题可在 GitHub 上找到](https://github.com/adobe/aem-site-template-standard/tree/main/theme)。

## 开发站点主题 {#developing-themes}

Adobe 提供 AEM 站点主题生成器作为一组用于创建新站点主题的脚本。

[GitHub 上提供了 AEM 站点主题生成器与使用文档。](https://github.com/adobe/aem-site-theme-builder)需要前端开发经验才能自定义主题。
