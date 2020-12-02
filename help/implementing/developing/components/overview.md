---
title: 组件 概述
description: 组件是实现特定功能的模块化单元，用于在您的网站上展示您的内容
translation-type: tm+mt
source-git-commit: 83c27daae4e8ae2ae6a8f115c9da9527971c6ecb
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 7%

---


# 组件概述{#components-overview}

本页概述了Adobe Experience Manager(AEM)组件，如用于页面创作的[](/help/sites-cloud/authoring/fundamentals/components.md)。

## 什么是组件？{#what-are-components}

AEM中的组件包括：

* 模块化单元，可实现在网站上展示您的内容的特定功能。
* 可重用。
* 在存储库的一个文件夹中开发为独立单元。
* 没有隐藏的配置文件。
* 可以包含其他组件。
* 可以在任何AEM系统中运行，也可以限制在特定组件下运行。
* 拥有标准化的用户界面。
* 具有可配置的编辑行为。
* 使用使用基于Granite UI组件的子元素构建的对话框。
* 使用[HTL](https://docs.adobe.com/content/help/zh-Hans/experience-manager-htl/using/overview.html)进行开发。
* 可以进行开发以创建扩展默认功能的自定义组件。

由于组件是模块化的，您可以：

* 在本地实例上开发新组件。
* 将其部署到测试环境。
* 将其部署到实时创作环境，创作者和／或管理员可在该环境中添加和配置内容。
* 将其部署到实时发布环境，在实时发布访客中，用户将内容呈现给网站。

每个AEM组件：

* 是资源类型。
* 是完全实现特定功能的脚本的集合。
* 可以独立运行，即在AEM或门户中运行。

## AEM 核心组件 {#aem-core-components}

[AEM核心组](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/introduction.html) 件是一套标准化的Web内容管理(WCM)组件，用于AEM以加快开发时间并降低网站的维护成本。

核心组件以AEMCloud Service形式提供，[WKND教程](/help/implementing/developing/introduction/develop-wknd-tutorial.md)说明了如何实现和使用组件。 这些组件随所有源代码提供，并且可以按原样使用，也可以作为修改的或扩展组件的起点。

### 查看可用组件{#viewing-available-components}

有关AEM实例中所有可用组件的概述，请使用[组件控制台](/help/sites-cloud/authoring/features/components-console.md)。

或者，您也可以使用CRXDE Lite获取存储库中所有可用组件的列表。

1. 在&#x200B;**[!UICONTROL CRXDE Lite]**&#x200B;中，从工具栏中选择&#x200B;**[!UICONTROL 工具]**，然后选择&#x200B;**[!UICONTROL 查询]**，打开&#x200B;**[!UICONTROL 查询]**&#x200B;选项卡。

1. 在&#x200B;**[!UICONTROL 查询]**&#x200B;选项卡中，选择`XPath`作为&#x200B;**[!UICONTROL 类型]**。

1. 在&#x200B;**[!UICONTROL 查询]**&#x200B;输入字段中，输入以下字符串：

   `//element(*, cq:Component)`

1. 单击&#x200B;**[!UICONTROL 执行]**&#x200B;并列出组件。

