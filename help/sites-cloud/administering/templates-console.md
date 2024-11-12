---
title: 模板控制台
description: 了解模板控制台如何充当查看和管理页面模板的中心位置。
solution: Experience Manager Sites
feature: Administering
role: User
source-git-commit: 993f81e0ff2b71ce2edf59a2c74398db3abe8f06
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 1%

---


# 模板控制台 {#templates-console}

了解模板控制台如何充当查看和管理页面模板的中心位置。

## 概述 {#overview}

创建页面时，需要选择模板。 页面模板用作新页面的基础。 [AEM可编辑模板](/help/implementing/developing/components/templates.md)可以定义生成页面的结构、任何初始内容以及可以使用的组件（设计属性）。

内容作者在站点控制台中[创建新页面时，会看到一系列可用的模板。](/help/sites-cloud/authoring/sites-console/creating-pages.md)模板可用于创建可通过以下方式编辑的页面：

* [页面编辑器](/help/sites-cloud/authoring/page-editor/templates.md)或
* [通用编辑器](/help/sites-cloud/authoring/universal-editor/templates.md)

通过“模板”控制台，管理员可以在一个中心位置查看和管理所有页面模板。

## 访问“模板”控制台 {#accessing}

1. 登录AEM as a Cloud Service。
1. 打开全局导航并选择&#x200B;**工具**&#x200B;面板，然后选择&#x200B;**常规** -> **模板**。

## 方向 {#orientation}

模板控制台被组织到具有每个[配置](/help/implementing/developing/introduction/configurations.md)的一个文件夹的文件夹中，这些文件夹中已为配置激活可编辑的模板。

![模板控制台](assets/templates-console/templates-console.png)

[控制台的默认视图](/help/sites-cloud/authoring/quick-start.md)是卡片视图。 点击或单击文件夹可浏览其内容。

![模板控制台中模板文件夹的内容](assets/templates-console/templates-console-templates.png)

选择模板以显示工具栏中可用的选项。

![模板控制台工具栏](assets/templates-console/templates-console-toolbar.png)

* [编辑](#edit-edit)
* [属性](#properties)
* [禁用/启用](#enable-disable)
* [发布](#publish)
* [复制](#copy)
* [删除](#delete)

## 编辑 {#edit}

编辑模板会打开用于创建模板的编辑器。 可以任选其一：

* [模板编辑器](/help/sites-cloud/authoring/page-editor/templates.md)
* [通用编辑器](/help/sites-cloud/authoring/universal-editor/templates.md)

无论使用哪个编辑器，您都可以对模板进行必要的更改。 请注意，编辑正在使用的模板可能会影响您的作者。

* 对于使用模板编辑器创建的模板，所做的更改可能会影响基于所选模板的实时页面。
* 对于使用通用编辑器创建的模板，所做的更改仅影响作者根据所选模板创建的新页面。

如果作者开始使用已启用的模板编辑器创建的模板，则会显示警告。

>[!TIP]
>
>在控制台中选择模板后，使用热键`e`编辑所选模板。

## 属性 {#properties}

您可以像编辑[页面属性一样编辑模板](/help/sites-cloud/authoring/page-editor/templates.md)的[属性。](/help/sites-cloud/authoring/sites-console/page-properties.md)模板属性包括：

* 模板标题
* 描述
* 图像

>[!TIP]
>
>在控制台中选择模板后，使用热键`p`打开所选模板的属性。

## 启用和禁用 {#enable-disable}

模板可以具有以下三种状态之一：

* **草稿** — 模板仍在创建中，无法用于创建新页面。
* **已启用** — 模板已完成，可用于创建新页面。
* **已禁用** — 模板已完成，但无法用于创建新页面。

创建模板时，其默认处于&#x200B;**草稿**&#x200B;状态（对于使用[模板编辑器](/help/sites-cloud/authoring/page-editor/templates.md)创建的模板）或&#x200B;**已启用**&#x200B;状态（对于使用[通用编辑器](/help/sites-cloud/authoring/universal-editor/templates.md)创建的模板）。

必须先启用模板，内容作者才能使用模板创建页面。 如果不再需要某个模板，可以禁用该模板，使其不再显示在页面创建向导中。

* 选择模板，然后单击或点按&#x200B;**禁用**&#x200B;以禁用模板。
* 选择模板并单击或点按&#x200B;**启用**&#x200B;以启用该模板。

## 发布 {#publish}

使用模板编辑器创建的模板仅在发布后才能使用。 选择模板并单击或点按&#x200B;**Publish**&#x200B;以进行发布。

使用通用编辑器创建的模板无需发布即可使用。

## 正在复制 {#copy}

如果您的许多页面的结构相似，则可以使用&#x200B;**复制**&#x200B;按钮来创建模板范围，然后根据您的需求更改该副本。 如果您要在其他网站上使用模板，这也很有用。

1. 选择模板，然后点按或单击&#x200B;**复制**&#x200B;以创建副本。
1. 导航到要创建副本的位置。
1. 点按或单击工具栏中的&#x200B;**粘贴**。

粘贴后，您可以：

* [编辑模板](#edit)以根据需要对其进行调整。
* [使用属性窗口](#properties)更新模板标题。
* [启用模板](#enable-disable)，以便使用该模板创建页面。
* 如果需要，[Publish模板](#publish)。

>[!TIP]
>
>在控制台中选择模板后，使用热键`Command+c`或`ctrl+c`复制所选模板。

## 正在删除 {#delete}

如果不再需要某个模板，可以将其删除，前提是它未被任何页面引用。

选择模板，然后点按或单击&#x200B;**删除**&#x200B;以将其删除。

>[!TIP]
>
>在控制台中选择模板后，使用热键`Backspace`删除所选模板。

## 创建模板 {#create}

使用控制台中的&#x200B;**创建**&#x200B;按钮，在当前位置创建新模板。 有关创建模板的详细信息，请参阅文档[用于创建可通过页面编辑器编辑的页面的模板。](/help/sites-cloud/authoring/page-editor/templates.md)

**创建**&#x200B;按钮仅用于创建可通过页面编辑器编辑的模板。 请参阅文档[创建可通过通用编辑器编辑的页面的模板](/help/sites-cloud/authoring/universal-editor/templates.md)，了解如何基于使用通用编辑器创建的页面创建模板。
