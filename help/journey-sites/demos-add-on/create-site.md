---
title: 创建演示站点
description: 在AEM中根据预配置模板库创建演示网站。
exl-id: e76fd283-12b2-4139-9e71-2e145b9620b1
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '844'
ht-degree: 2%

---

# 创建演示站点 {#creating-a-site}

在AEM中根据预配置模板库创建演示网站。

## 迄今为止的故事 {#story-so-far}

在AEM参考演示附加组件历程的上一文档中， [创建程序、](create-program.md) 您执行了第一个配置步骤以创建用于测试的程序，并使用管道部署附加内容。 您现在应该：

* 了解如何使用Cloud Manager创建新项目。
* 了解如何激活新计划的参考演示附加组件。
* 能够运行管道以部署附加内容。

本文介绍了此过程的下一步：根据参考演示加载项的模板，在AEM中创建新站点或AEM Screens项目。

## 目标 {#objective}

本文档可帮助您了解如何根据参考演示加载项的模板创建新站点。 阅读后，您应该：

* 了解如何访问AEM创作环境。
* 了解如何根据模板创建网站。
* 了解导航网站结构和编辑页面的基础知识。

## 创建演示网站或Screens项目 {#create-site}

管道部署参考演示加载项后，您可以访问AEM创作环境，以根据附加内容创建演示网站。

1. 在Cloud Manager的项目概述页面中，点按或单击指向AEM创作环境的链接。

   ![访问创作环境](assets/access-author.png)

1. 在AEM的主菜单中，点按或单击 **站点**.

   ![访问站点](assets/access-sites.png)

1. 在站点控制台中，点按或单击 **创建** ，然后选择 **模板中的网站** 中。

   ![从模板创建站点](assets/create-site-from-template.png)

1. 将启动站点创建向导。 在左列中，您可以看到已将管道部署到创作实例的演示模板。 点按或单击一个以将其选中，并在右列中显示详细信息。 如果要测试或演示AEM Screens，请务必选择 **We.Cafe网站模板**. 单击或点按&#x200B;**下一步**。

   ![站点创建向导](assets/site-creation-wizard.png)

1. 在下一个屏幕中，为您的网站或Screens项目提供标题。 如果忽略，则可以提供或将从标题生成网站名称。 点击或单击&#x200B;**创建**。

   * 网站标题会显示在浏览器标题栏中。
   * 网站名称将成为URL的一部分。
   * 网站名称必须符合AEM页面命名约定，其详细信息可在 [其他资源](#additional-resources) 中。

   ![网站详细信息](assets/site-details.png)

1. 通过对话框确认网站的创建。 点按或单击 **完成**.

   ![网站创建完成](assets/site-creation-complete.png)

您现在已创建自己的演示网站！

## 使用演示网站 {#use-site}

现在，您已创建演示网站，接下来可以导航并使用该网站，就像在AEM中使用任何其他网站一样。

1. 现在，网站会显示在站点控制台中。

   ![站点控制台中的新演示站点](assets/new-demo-site.png)

1. 在屏幕的右上角，确保将控制台视图设置为 **列视图**.

   ![列视图](assets/column-view.png)

1. 点按或单击网站以浏览其结构和内容。 当您导航演示网站的内容树时，列视图会不断展开。

   ![网站结构](assets/site-structure.png)

1. 点按或单击某个页面以将其选中，然后点按或单击 **编辑** 中。

   ![选择页面](assets/select-page.png)

1. 您可以作为任何其他AEM内容页面来编辑该页面，如添加或编辑组件或资产，并测试AEM的功能。

   ![编辑页面](assets/edit-page.png)

恭喜！ 您现在可以进一步浏览演示网站的内容，并通过参考演示加载项的最佳实践内容发现AEM必须提供的所有内容。

根据其他模板创建其他站点，以探索更多AEM功能。

## 下一步 {#what-is-next}

现在，您已完成AEM参考演示附加组件历程的这一部分，接下来您应该：

* 了解如何访问AEM创作环境。
* 了解如何根据模板创建网站。
* 了解导航网站结构和编辑页面的基础知识。

您现在可以使用附加内容测试AEM的功能。 要继续您的历程，有两个选项：

* 如果您希望完全演示和测试AEM Screens内容，请确保您已基于 **We.Cafe网站模板** 如前面所述并继续 [为演示网站启用AEM Screens。](screens.md)
* 如果您只查看演示站点内容，请继续 [管理演示网站，](manage.md) 您将在此处了解可用于帮助您管理演示网站的工具以及如何删除这些工具。

## 其他资源 {#additional-resources}

* [Cloud Manager文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html)  — 如果您希望了解有关Cloud Manager功能的更多详细信息，则可能需要直接查阅深入的技术文档。
* [创建网站](/help/sites-cloud/administering/site-creation/create-site.md)  — 了解如何使用AEM通过网站模板创建网站，以定义网站的样式和结构。
* [AEM页面命名约定。](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#page-name-restrictions-and-best-practices)  — 请参阅本页以了解组织AEM页面的惯例。
* [AEM基本操作](/help/sites-cloud/authoring/getting-started/basic-handling.md)  — 如果您是初次了解AEM以了解导航和控制台组织等基本概念，请浏览本文档。
