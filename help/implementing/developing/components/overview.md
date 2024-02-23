---
title: 组件概述
description: 组件是模块化单元，可实施特定功能以在您的网站上展示您的内容
exl-id: 0fdc99e7-2103-448d-8217-d5d52c94acea
source-git-commit: bbd845079cb688dc3e62e2cf6b1a63c49a92f6b4
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 100%

---

# 组件概述 {#components-overview}

此页面概述了 Adobe Experience Manager (AEM) 组件，例如那些[用于页面创作](/help/sites-cloud/authoring/page-editor/components.md)的组件。

## 什么是组件？ {#what-are-components}

* 实现特定功能以在网站上展示内容的模块化单元。
* 可重用。
* 作为存储库的一个文件夹中的独立单元开发。
* 没有隐藏的配置文件。
* 它们可以包含其他组件。
* 它们可在任何 AEM 系统中的任何位置运行，也可仅限在特定组件下运行。
* 拥有标准化的用户界面。
* 具有可配置的编辑行为。
* 使用通过基于 Granite UI 组件的子元素构建的对话框。
* 使用 [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html) 开发的它们。
* 它们经过开发，可创建扩展默认功能的自定义组件。

由于组件是模块化的，因此您可以：

* 在本地实例上开发新组件。
* 将它部署到测试环境。
* 将它部署到实时创作环境，作者和/或管理员可在该环境中添加和配置内容。
* 将它部署到实时发布环境，其中使用它为您网站的访客呈现内容。

每个 AEM 组件：

* 是一种资源类型。
* 是一个完全实施特定功能的脚本的集合。
* 可以单独运行，也就是说可在 AEM 或门户中运行。

## AEM 核心组件 {#aem-core-components}

[AEM 核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)是一组用于 AEM 的标准化网站内容管理 (WCM) 组件，可加快开发速度并降低网站的维护成本。

核心组件随 AEM as a Cloud Service 提供，[WKND 教程](/help/implementing/developing/introduction/develop-wknd-tutorial.md)说明了如何实施和使用这些组件。这些组件随所有源代码一起提供，可以按原样使用或用作已修改或扩展的组件的起点。

### 查看可用组件 {#viewing-available-components}

有关 AEM 实例中的所有可用组件的概述，请使用[组件控制台](/help/sites-cloud/authoring/components-console.md)。

或者，您也可以使用 CRXDE Lite 获取存储库中所有可用组件的列表。

1. 在 **[!UICONTROL CRXDE Lite]** 中，从工具栏中选择&#x200B;**[!UICONTROL 工具]**，然后选择&#x200B;**[!UICONTROL 查询]**，这将打开&#x200B;**[!UICONTROL 查询]**&#x200B;选项卡。

1. 在&#x200B;**[!UICONTROL 查询]**&#x200B;选项卡中，选择 `XPath` 作为&#x200B;**[!UICONTROL 类型]**。

1. 在&#x200B;**[!UICONTROL 查询]**&#x200B;输入字段中，输入以下字符串：

   `//element(*, cq:Component)`

1. 单击&#x200B;**[!UICONTROL 执行]**，随后将列出这些组件。
