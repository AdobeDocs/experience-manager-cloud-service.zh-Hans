---
title: 用于创建可使用通用编辑器编辑的页面的模板
description: 了解如何创建模板，这些模板可用于创建可通过通用编辑器编辑的页面，从而节省时间并确保一致的品牌化。
solution: Experience Manager Sites
feature: Authoring
role: User
exl-id: f0d60086-e92e-4492-ad50-bef84fed2a82
source-git-commit: 33eb71b2828314ee2c75206ef7034313e2638360
workflow-type: tm+mt
source-wordcount: '778'
ht-degree: 2%

---


# 用于创建可使用通用编辑器编辑的页面的模板 {#page-templates}

了解如何创建模板，这些模板可用于创建可通过通用编辑器编辑的页面，从而节省时间并确保一致的品牌化。

>[!NOTE]
>
>此功能将在即将发布的AEM as a Cloud Service中提供。

>[!NOTE]
>
>[模板也可用于创建可通过页面编辑器编辑的页面。](/help/sites-cloud/authoring/page-editor/templates.md)

## 什么是页面模板？ {#what-are}

品牌推广和营销指南通常会为您的内容页面规定特定的布局。 实际上，许多页面将共享相同的结构和布局。 为了节省内容作者时间，可以从模板创建页面。

页面模板用作页面布局的主副本。 从模板创建页面时，模板的初始内容会复制到新页面，这有助于为内容作者预定义页面的基本布局和内容，从而节省时间。

## 启用页面模板 {#enabling-templates}

要使用模板创建可通过通用编辑器编辑的页面，必须启用该选项。

首先为您的站点配置启用可编辑模板。

1. 使用&#x200B;**站点**&#x200B;控制台和[选择站点的根。](/help/sites-cloud/authoring/sites-console/introduction.md#selecting-resources)
1. 选择站点根后，点按或单击工具栏中的&#x200B;[**属性**&#x200B;图标](/help/sites-cloud/authoring/sites-console/page-properties.md)。
1. 在属性对话框的&#x200B;**高级**&#x200B;选项卡上，记下&#x200B;**云配置**&#x200B;字段中的值。
1. 从主导航中选择&#x200B;**工具** -> **常规** -> **配置浏览器**。
1. 在&#x200B;**[配置浏览器](/help/implementing/developing/introduction/configurations.md)**&#x200B;中，选择您在上一步中注意到的配置，然后点按或单击工具栏中的&#x200B;**属性**。
1. 在&#x200B;**配置属性**&#x200B;窗口中，选中选项&#x200B;**可编辑模板**。
1. 点按或单击&#x200B;**保存并关闭**。

启用配置后，必须为站点允许模板。

1. 使用&#x200B;**站点**&#x200B;控制台和[选择站点的根。](/help/sites-cloud/authoring/sites-console/introduction.md#selecting-resources)
1. 选择站点根后，点按或单击工具栏中的&#x200B;[**属性**&#x200B;图标](/help/sites-cloud/authoring/sites-console/page-properties.md)。
1. 在&#x200B;**模板设置**&#x200B;部分下的“属性”对话框的&#x200B;**高级**&#x200B;选项卡上，点按或单击&#x200B;**添加**&#x200B;按钮。
1. 在&#x200B;**允许的模板**&#x200B;下显示的新空字段中，添加路径`/conf/<site>/settings/wcm/templates/.*`。
1. 点按或单击&#x200B;**保存并关闭**。

您现在可以使用模板为网站创建页面。 此任务必须仅在创建可使用通用编辑器编辑的页面时，对您希望使用模板的每个站点/配置执行一次。

## 创建新模板 {#create-new}

您可以[创建新页面](/help/sites-cloud/authoring/sites-console/creating-pages.md)以用作模板，或者使用现有页面作为模板的基础。

1. 使用&#x200B;**站点**&#x200B;控制台可[导航到要用作模板的新页面或现有页面](/help/sites-cloud/authoring/sites-console/introduction.md#selecting-resources)，然后点按或单击该页面以将其选定。

1. 选择页面后，点按或单击工具栏中的&#x200B;[**属性**&#x200B;图标](/help/sites-cloud/authoring/sites-console/page-properties.md)。

1. 在&#x200B;**模板设置**&#x200B;部分下的属性对话框的&#x200B;**高级**&#x200B;选项卡上，选择切换&#x200B;**将页面用作模板**。

1. 点按或单击&#x200B;**保存并关闭**。

创建新页面时，您的新页面现在可以用作模板。

## 从模板创建页面 {#creating-from-template}

使用通用编辑器可编辑的模板创建页面的工作流程与[创建任何其他页面的工作流程相同。](/help/sites-cloud/authoring/sites-console/creating-pages.md)

1. 使用&#x200B;**站点**&#x200B;控制台[导航到要创建新页面的位置](/help/sites-cloud/authoring/sites-console/introduction.md#selecting-resources)。

1. 点击或单击&#x200B;**创建**-> **页面**。

1. 在&#x200B;**创建页面**&#x200B;向导的&#x200B;**模板**&#x200B;选项卡上，您可以选择新页面要基于的模板。 点按或单击所需的模板以将其选定，然后点按或单击&#x200B;**下一步**。

完成向导，操作方法与完成任何其他页面一样，并且您已根据所选模板创建了新页面。

## 页面和模板 {#pages-vs-templates}

页面模板仅定义页面的初始内容。 然后，可以使用通用编辑器完全编辑页面。

* 从页面模板创建的页面是模板的独立副本。
* 如果模板发生更改，则基于该模板的现有页面不会发生更改。
* 内容作者可以根据需要修改和更新生成页面的内容，不受模板限制。

## 可编辑模板 {#editable-templates}

使用[页面编辑器](/help/sites-cloud/authoring/page-editor/introduction.md)创建的页面也可以基于模板。 用于为通用编辑器和页面编辑器创建页面的模板都利用AEM的[可编辑模板。](/help/implementing/developing/components/templates.md)

用于创建可通过页面编辑器编辑的页面的模板利用了可编辑模板的所有功能。 用于创建可通过通用编辑器编辑的页面的模板仅使用初始内容功能。
