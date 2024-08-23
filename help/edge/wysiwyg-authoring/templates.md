---
title: 将页面模板与通用编辑器一起使用
description: 了解如何通过Universal Editor创建和使用页面模板。
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 773ce75975f4dcc2c5310422bcc377b487ebec25
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 2%

---


# 将页面模板与通用编辑器一起使用 {#page-templates}

了解如何通过Universal Editor创建和使用页面模板。

>[!NOTE]
>
>此功能将在即将发布的AEM as a Cloud Service中提供。

## 什么是页面模板？ {#what-are}

品牌推广和营销指南通常会为您的内容页面规定特定的布局。 实际上，许多页面将共享相同的结构和布局。 为了节省内容作者时间，可以从模板创建页面。

页面模板用作页面布局的主副本。 从模板创建页面时，模板的内容会复制到新页面，这有助于为内容作者预定义页面的布局和初始内容，从而节省他们的时间。

## 创建页面模板 {#creating}

可以通过创建新页面或使用现有页面作为模板来创建页面模板。 在这两种情况下，您都使用&#x200B;[**站点**&#x200B;控制台。](/help/sites-cloud/authoring/sites-console/introduction.md)

### 创建新模板 {#create-new}

1. 使用&#x200B;**站点**&#x200B;控制台导航到您希望创建新页面的位置，该页面将用作您的模板，[像创建任何其他页面一样创建页面。](/help/sites-cloud/authoring/sites-console/creating-pages.md)

1. 创建页面并返回到控制台后，请选择该页面，然后点按或单击工具栏中的&#x200B;[**属性**&#x200B;图标](/help/sites-cloud/authoring/sites-console/page-properties.md)。

1. 在&#x200B;**模板设置**&#x200B;部分下的“属性”对话框的&#x200B;**高级**&#x200B;选项卡上，选择切换&#x200B;**用作模板**。

1. 在&#x200B;**模板名称**&#x200B;字段中，提供描述性名称。

   * 这是将显示创建新内容页面以及选择新页面所基于的模板的名称。

1. 点按或单击&#x200B;**保存并关闭**。

创建新页面时，您的新页面现在可以用作模板。

### 使用现有页面作为模板 {#existing-page}

1. 使用&#x200B;**站点**&#x200B;控制台[导航到要用作模板的页面](/help/sites-cloud/authoring/sites-console/introduction.md#selecting-resources)的位置。

1. 选择页面，然后点按或单击工具栏中的&#x200B;[**属性**&#x200B;图标](/help/sites-cloud/authoring/sites-console/page-properties.md)。

1. 在&#x200B;**模板设置**&#x200B;部分下的“属性”对话框的&#x200B;**高级**&#x200B;选项卡上，选择切换&#x200B;**用作模板**。

1. 在&#x200B;**模板名称**&#x200B;字段中，提供描述性名称。

   * 这是将显示创建新内容页面以及选择新页面所基于的模板的名称。

1. 点按或单击&#x200B;**保存并关闭**。

现在，创建新页面时，所选页面可用作模板。

## 从模板创建页面 {#creating-from-template}

从模板中创建用于通用编辑器的页面与[创建该页面时的工作流程相同。](/help/sites-cloud/authoring/sites-console/creating-pages.md)

1. 使用&#x200B;**站点**&#x200B;控制台[导航到要创建新页面的位置](/help/sites-cloud/authoring/sites-console/introduction.md#selecting-resources)。

1. 点击或单击&#x200B;**创建**-> **页面**。

1. 在&#x200B;**创建页面**&#x200B;向导的&#x200B;**模板**&#x200B;选项卡上，您可以选择新页面要基于的模板。 点按或单击所需的模板以将其选定，然后点按或单击&#x200B;**下一步**。

完成向导，操作方法与完成任何其他页面一样，并且您已根据所选模板创建了新页面。

## 通用编辑器和页面编辑器 {#page-vs-universal}

通用编辑器的页面模板解决了与AEM页面编辑器](/help/sites-cloud/authoring/page-editor/templates.md)的[页面模板相同的问题，从而能够重用内容以基于一组预定义布局快速创建页面。 然而，他们解决这个问题的方式却大不相同。 如果您是页面编辑器的用户，请注意这些差异。

* 从通用编辑器的页面模板创建的页面是模板的独立副本。
* 因此，如果模板发生更改，则生成的页面不会更改。
* 内容作者可以根据需要修改和更新生成页面的内容，不受模板限制。
