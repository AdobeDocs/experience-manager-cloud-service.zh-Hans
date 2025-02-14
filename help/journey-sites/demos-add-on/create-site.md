---
title: 创建演示 Site
description: 基于预配置的模板库在 AEM 中创建演示 Site。
exl-id: e76fd283-12b2-4139-9e71-2e145b9620b1
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: ht
source-wordcount: '809'
ht-degree: 100%

---

# 创建演示 Site {#creating-a-site}

基于预配置的模板库在 AEM 中创建演示 Site。

## 迄今为止的故事 {#story-so-far}

在 AEM 参考演示加载项历程的上一个文档[创建程序](create-program.md)中，您执行了第一个配置步骤来创建程序以进行测试并使用管道来部署加载项内容。现在应：

* 了解如何使用 Cloud Manager 创建程序。
* 了解如何为新程序激活参考演示加载项。
* 能够运行管道以部署加载项内容。

本文描述了此过程的下一步，即基于参考演示加载项的模板在 AEM 中创建 Site 或 AEM Screens 项目。

## 目标 {#objective}

本文档有助于您了解如何基于参考演示加载项的模板创建 Site。阅读本文档后，您应：

* 了解如何访问 AEM 创作环境。
* 了解如何基于模板创建 Site。
* 了解导航 Site 结构和编辑页面的基础知识。

## 创建演示 Site 或 Screens 项目 {#create-site}

在管道部署参考演示加载项后，您可以访问 AEM 创作环境以基于加载项内容创建演示 Site。

1. 从 Cloud Manager 中的程序概述页面，选择指向 AEM 创作环境的链接。

   ![访问创作环境](assets/access-author.png)

1. 从 AEM 的主菜单中，选择 **Site**。

   ![访问 Site](assets/access-sites.png)

1. 从 Site 控制台中，在屏幕的右上角选择&#x200B;**创建**，然后在下拉菜单中选择&#x200B;**从模板创建 Site**。

   ![从模板创建 Site](assets/create-site-from-template.png)

1. Site 创建向导随即启动。在左栏中，您可以看到由管道部署到创作实例的演示模板。选择一个演示模板以选择它并在右栏中显示详细信息。如果要测试或演示 AEM Screens，请确保选择 **We.Cafe Site 模板**。选择&#x200B;**下一步**。

   ![Site 创建向导](assets/site-creation-wizard.png)

1. 在下一个屏幕中，为您的 Site 或 Screens 项目提供标题。可以提供 Site 名称，也可以从标题生成 Site 名称（如果被忽略）。选择&#x200B;**创建**。

   * Site 标题显示在浏览器标题栏中。
   * Site 名称会成为 URL 的一部分。
   * Site 名称必须符合 AEM 的页面命名惯例，可参阅[其他资源](#additional-resources)部分了解详细信息。

   ![Site 详细信息](assets/site-details.png)

1. 通过对话框确认 Site 创建。选择&#x200B;**完成**。

   ![Site 创建模板](assets/site-creation-complete.png)

您现在已创建自己的演示 Site！

## 使用演示 Site {#use-site}

现已创建您的演示 Site，您可以像在 AEM 中导航和使用任何其他 Site 一样导航和使用您的 Site。

1. Site 现在显示在 Site 控制台中。

   ![ Site 控制台中的新演示 Site](assets/new-demo-site.png)

1. 在屏幕的右上角，确保控制台视图设置为&#x200B;**列视图**。

   ![列视图](assets/column-view.png)

1. 选择 Site 以浏览其结构和内容。当您浏览演示 Site 的内容树时，列视图会不断扩展。

   ![Site 结构](assets/site-structure.png)

1. 选择一个页面以选择它，然后在工具栏中选择&#x200B;**编辑**。

   ![选择页面](assets/select-page.png)

1. 您可以像编辑任何其他 AEM 内容页面一样编辑该页面，例如添加或编辑组件/资源以及测试 AEM 的功能。

   ![编辑页面](assets/edit-page.png)

恭喜！您现在可以进一步浏览演示 Site 的内容，并通过参考演示加载项的最佳实践内容来发现 AEM 必须提供的一切。

基于其他模板创建额外的 Site 以探究更多 AEM 功能。

## 后续内容 {#what-is-next}

现在您已完成 AEM 参考演示加载项历程的这一部分，您应：

* 了解如何访问 AEM 创作环境。
* 了解如何基于模板创建 Site。
* 了解导航 Site 结构和编辑页面的基础知识。

您现在可以使用加载项内容测试 AEM 的功能。为您提供了两个选项以继续历程：

* 如果要完全演示和测试 AEM Screens 内容，请确保已部署基于 **We.Cafe Site 模板**&#x200B;的 Site（如前所述），并继续[为演示 Site 启用 AEM Screens](screens.md)。
* 如果仅需演示 Site 内容，请继续[管理您的演示 Site](manage.md)，了解可用于帮助您管理演示 Site 的工具以及如何删除它们。

## 其他资源 {#additional-resources}

* [Cloud Manager 文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html) – 如果您想了解有关 Cloud Manager 功能的更多详细信息，您可能需要直接参阅深入的技术文档。
* [创建 Site](/help/sites-cloud/administering/site-creation/create-site.md) – 了解如何使用 AEM 创建 Site，并使用 Site 模板定义 Site 的样式和结构。
* [AEM 的页面命名惯例。](/help/sites-cloud/authoring/sites-console/organizing-pages.md#page-name-restrictions-and-best-practices) – 请参阅此页面，了解用于组织 AEM 页面的惯例。
* [AEM 基本操作](/help/sites-cloud/authoring/basic-handling.md) – 如果您不熟悉 AEM，请参阅本文档，了解导航和控制台组织等基本概念。
