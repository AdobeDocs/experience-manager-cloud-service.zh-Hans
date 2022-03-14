---
title: 管理演示网站
description: 了解可用于帮助您管理演示网站的工具以及如何删除它们。
exl-id: 988c6e09-c43e-415f-8d61-998c294c5a11
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 0%

---

# 管理演示网站 {#manage-demo-sites}

了解可用于帮助您管理演示网站的工具以及如何删除它们。

## 迄今为止的故事 {#story-so-far}

在AEM参考演示附加组件历程的上一文档中， [创建站点、](create-site.md) 您基于“参考演示加载项”的模板创建了一个新的演示网站。 您现在应该：

* 了解如何访问AEM创作环境。
* 了解如何根据模板创建网站。
* 了解导航网站结构和编辑页面的基础知识。

如果您还 [为您的演示网站启用AEM Screens,](screens.md) 您还应该：

* 了解AEM Screens的基础知识。
* 了解We.Cafe演示内容。
* 了解如何为We.Cafe配置AEM Screens。

现在，您有自己的演示网站可供浏览，本文介绍了可用于帮助您管理演示网站的工具以及如何删除这些工具。

## 目标 {#objective}

本文档可帮助您了解如何管理您创建的演示网站。 阅读后，您应该：

* 了解如何访问自助服务演示实用工具。
* 了解哪些实用工具可供您使用。
* 如何删除现有演示网站或模板。

## 访问自助演示实用工具 {#accessing-utilities}

现在，您拥有自己的演示网站，您可能希望了解如何管理这些网站。 该管道不仅部署了站点模板来提供演示站点内容，还部署了一组实用程序来管理这些站点。

1. 从AEM全局导航栏中，选择 **工具** -> **参考演示** -> **参考演示实用工具**.

   ![自助式演示实用程序](assets/demo-utilities.png)

1. 参考演示实用程序是一系列有用的功能，可帮助设置和监视Adobe Experience Manager环境。 初始视图是 **功能板**，用于检查环境及其演示功能的状态。

   ![功能板](assets/dashboard.png)

自助服务演示实用程序提供了许多工具。

* **删除站点**  — 选择要在此Adobe Experience Manager实例中删除的站点。 请记住，这是破坏性操作，一旦启动便无法撤消。
* **删除网站模板**  — 选择要在此Adobe Experience Manager实例中删除的网站模板。 在删除网站模板之前，请确保同时删除引用该模板的所有网站。 请记住，这是破坏性操作，一旦启动便无法撤消。
* **主作者缓存**  — 这将在Adobe Experience Manager实例内获取多个资源，从而加快获取时间。 可能需要几秒钟。
* **Android应用程序**  — 用于安装和启动Android演示应用程序的工具。 根据 **WKND单页应用程序** 来填充此页面。 从Android设备、模拟器或Bluestack中使用。
* **用户首选项**  — 关闭教程弹出对话框。
* **设置GraphQL**  — 快速设置全局GraphQL端点。

## 删除演示网站和模板 {#deleting}

在测试了一组AEM功能后，您可能不再需要演示网站，甚至不再需要该演示网站所基于的模板。 删除演示网站和网站模板非常容易。

1. 访问 **参考演示实用工具** 单击 **删除站点**.

   ![删除站点](assets/delete-sites.png)

1. 可用的站点列在列表中。 选中要删除的一个或多个网站，然后点按或单击 **删除**.

   >[!CAUTION]
   >
   >删除网站和模板是一种破坏性操作，一旦启动，便无法撤消。

1. 在对话框中确认删除网站。

   ![确认删除网站](assets/confirm-site-delete.png)

1. AEM会删除选定的一个或多个网站，并显示其进度 **删除** 按钮。

   ![删除进度](assets/delete-progress.png)

网站现已删除。

您可以以相同方式删除标题下的模板 **删除网站模板** 在 **参考演示实用工具**.

>[!CAUTION]
>
>在删除网站模板之前，请确保同时删除引用该模板的所有网站。

## 历程结束？ {#end-of-journey}

恭喜！ 您已完成AEM参考演示附加组件历程！ 您现在应该：

* 了解Cloud Manager的基本知识，并了解管道如何将内容和配置交付到AEM。
* 了解如何使用Cloud Manager创建新项目。
* 了解如何激活新计划的参考演示加载项，并能够运行管道以部署附加项内容。
* 了解如何访问AEM创作环境以基于模板创建网站。
* 了解如何访问自助服务演示实用工具。
* 了解如何删除现有演示网站或模板。

现在，您可以使用自己的演示网站探索AEM的功能。 但是，AEM是一款功能强大的工具，还有许多其他选项可供使用。 请查看 [“其他资源”部分](#additional-resources) 以进一步了解您在此历程中看到的功能。

## 其他资源 {#additional-resources}

* [Cloud Manager文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html)  — 如果您希望了解有关Cloud Manager功能的更多详细信息，则可能需要直接查阅深入的技术文档。
* [创建网站](/help/sites-cloud/administering/site-creation/create-site.md)  — 了解如何使用AEM通过网站模板创建网站，以定义网站的样式和结构。
* [AEM页面命名约定。](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#page-name-restrictions-and-best-practices)  — 请参阅本页以了解组织AEM页面的惯例。
* [AEM基本操作](/help/sites-cloud/authoring/getting-started/basic-handling.md)  — 如果您是初次了解AEM以了解导航和控制台组织等基本概念，请浏览本文档。
* [AEMas a Cloud Service技术文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html)  — 如果您已经对AEM有了很深的了解，则可能需要直接查阅深入的技术文档。
* [网站模板](/help/sites-cloud/administering/site-creation/site-templates.md)  — 如果您想进一步了解网站模板的结构以及如何使用它们来创建网站，请参阅此文档。
