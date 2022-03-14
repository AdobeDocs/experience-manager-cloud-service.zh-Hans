---
title: 管理分阶段产品目录体验
description: 了解如何管理分阶段产品目录体验。
exl-id: 1db18818-b8e0-4127-8a65-dc3dea1f2927
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 2%

---

# 构建分阶段的产品目录体验 {#building-experiences}

了解如何管理分阶段产品目录体验。

## 迄今为止的故事 {#story-so-far}

在AEM内容和商务历程的上一个文档中， [管理产品目录页面和模板](catalog-templates.md)，您学习了如何基于模板管理和构建产品目录体验。

本文以这些基本知识为基础。

## 目标 {#objective}

本文档可帮助您了解如何根据分阶段产品数据和AEM启动次数管理产品目录体验。 很多时候，作者必须同时准备即将推出的产品（例如新的服装系列）。 这需要访问暂存产品数据（尚未上线）并能够准备内容。 此新内容将随产品发布一起上线。

    >[!NOTE]
    >
    >此功能仅在Adobe Commerce或云版本以及支持基于令牌身份验证的第三方连接器中可用。 有关更多信息，请参阅[快速入门](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content-and-commerce/storefront/getting-started.html)。

首先，让我们看看作者如何通过CIF访问分阶段产品数据。

## 使用暂存产品数据 {#staged-product-data}

访问分阶段产品数据的一种方法是使用产品驾驶舱。 单击主AEM菜单中的商务图标以打开产品目录。 这将允许您访问实时产品数据。 打开左侧的过滤器选项卡并展开 **暂存目录**. 现在，使用预览数据，您可以访问任意时间点的分阶段产品数据。 暂存数据包括新类别、产品或更新的字段（如价格）。

![座舱](assets/staged-cockpit.png)

使用时间扭曲视图，可以预览包含暂存数据的店面。 打开编辑器并切换模式以进行时间扭曲。 选择任意未来日期。 请注意您在某个日期查看页面的编辑器顶部的信息。

![stage timewarp](assets/staged-timewarp.png)

您现在可以使用暂存数据浏览目录。 如果打开分阶段类别或产品页面，编辑器将显示可视指示器。

![阶段pl](assets/staged-plp.png)

    >[!NOTE]
    >
    >Omnisearch没有上下文，因此将只返回实时产品目录数据

## AEM启动项 {#launches}

AEM Launches允许您为暂存产品数据创建内容。 如果您不熟悉启动项，请访问 [“其他资源”部分](#additional-resources). 然后，使用启动日期访问分阶段产品数据。

![阶段启动](assets/staged-launch.png)

请注意，选取器在右侧使用暂存指示器来遵循启动日期。

![阶段选取器](assets/staged-picker.png)

## 下一步 {#what-is-next}

现在，您已完成历程的这一部分，接下来您应该：

* 了解Launch中的分阶段产品目录和内容的概念
* 能够通过产品驾驶舱和编辑器访问分阶段产品目录数据

您现在可以管理 [产品体验](product-experience-management.md). 但是，AEM内容和商务还有许多其他选项可用。 请查看 [“其他资源”部分](#additional-resources) 以进一步了解您在此历程中看到的功能。

## 其他资源 {#additional-resources}

* [产品 Cockpit](/help/commerce-cloud/authoring/product-cockpit.md)
* [快速入门](/help/commerce-cloud/getting-started.md)
* [启动项](/help/sites-cloud/authoring/launches/overview.md)
