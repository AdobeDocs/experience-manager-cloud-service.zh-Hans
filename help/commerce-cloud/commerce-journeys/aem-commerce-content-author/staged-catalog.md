---
title: 管理分阶段的产品目录体验
description: 了解如何管理分阶段的产品目录体验。
exl-id: 1db18818-b8e0-4127-8a65-dc3dea1f2927
feature: Commerce Integration Framework
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 10%

---

# 构建分阶段的产品目录体验 {#building-experiences}

了解如何管理分阶段的产品目录体验。

## 迄今为止的故事 {#story-so-far}

在AEM Content and Commerce历程的上一个文档中， [管理产品目录页面和模板](catalog-templates.md)您已了解如何基于模板管理和构建产品目录体验。

本文基于这些基础之上。

## 目标 {#objective}

本文档可帮助您了解如何根据分阶段的产品数据和AEM启动次数来管理产品目录体验。 很多时候，作者必须同时准备即将推出的产品（如新的服装系列）。 这需要访问暂存的产品数据（尚未启用）以及准备内容的能力。 此新内容将在产品发布时上线。

    >[！注意]
    >
    >此功能仅适用于支持基于令牌的身份验证的Adobe Commerce或Cloud Edition以及第三方连接器。 有关更多信息，请参阅[快速入门](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content-and-commerce/storefront/getting-started.html)。

首先，我们来了解作者如何使用CIF访问暂存的产品数据。

## 使用暂存的产品数据 {#staged-product-data}

访问暂存产品数据的一种方法是使用产品驾驶舱。 单击主AEM菜单中的Commerce图标以打开产品目录。 这将授予您访问实时产品数据的权限。 打开左侧的过滤器选项卡并展开 **暂存目录**. 现在，您可以使用预览数据访问任何时间点的暂存产品数据。 暂存数据包括新类别、产品或更新的字段，如价格。

![阶段驾驶舱](assets/staged-cockpit.png)

使用时间扭曲视图，可以预览包含暂存数据的店面。 打开编辑器并将模式切换为时间扭曲。 选择任何未来的日期。 请注意编辑器顶部显示的信息，即您正在查看特定日期的页面。

![阶段时间扭曲](assets/staged-timewarp.png)

您现在可以浏览包含暂存数据的目录。 如果打开暂存类别或产品页面，编辑器将显示一个可视指示器。

![阶段计划](assets/staged-plp.png)

    >[！注意]
    >
    >Omnisearch没有上下文，因此将只返回实时产品目录数据

## AEM 启动项 {#launches}

AEM启动项允许您为暂存的产品数据创建内容。 如果您不熟悉Launch，请查阅 [其他资源部分](#additional-resources). 然后，使用启动日期访问暂存的产品数据。

![暂存启动](assets/staged-launch.png)

请注意，选取器采用右侧带暂存指示器的启动日期。

![阶段选取器](assets/staged-picker.png)

## 后续内容 {#what-is-next}

现在您已完成此历程的这一部分，您应：

* 通过启动项了解分阶段产品目录和内容的概念
* 能够通过产品驾驶舱和编辑器访问暂存的产品目录数据

您现在已准备好管理 [产品体验](product-experience-management.md). 但是，AEM Content和Commerce提供了许多其他选项。 查看[“其他资源”部分](#additional-resources)中的一些其他资源，详细了解您在此历程中看到的功能。

## 其他资源 {#additional-resources}

* [产品 Cockpit](/help/commerce-cloud/authoring/product-cockpit.md)
* [快速入门](/help/commerce-cloud/getting-started.md)
* [启动项](/help/sites-cloud/authoring/launches/overview.md)
