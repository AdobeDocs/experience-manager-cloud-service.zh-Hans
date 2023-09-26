---
title: 组件概述
description: 组件是模块化单元，可实施特定功能以在您的网站上展示您的内容
exl-id: 0fdc99e7-2103-448d-8217-d5d52c94acea
source-git-commit: 78ead5f15c2613d9c3bed3025b43423a66805c59
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 67%

---

# 组件概述 {#components-overview}

此页面概述了 Adobe Experience Manager (AEM) 组件，例如那些[用于页面创作](/help/sites-cloud/authoring/fundamentals/components.md)的组件。

## 什么是组件？ {#what-are-components}

* 模块化单元，可实施特定功能以在您的网站上展示您的内容。
* 可重复使用。
* 作为存储库的一个文件夹中的独立单元开发。
* 没有隐藏的配置文件。
* 它们可以包含其他组件。
* 它们可以在任何AEM系统中的任何位置运行，并且也可以限制为在特定组件下运行。
* 拥有标准化的用户界面。
* 具有可配置的编辑行为。
* 使用使用基于Granite UI组件的子元素构建的对话框。
* 它们使用以下方式开发 [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html).
* 对其进行开发可创建扩展默认功能的自定义组件。

由于组件是模块化的，因此您可以：

* 在本地实例上开发新组件。
* 将它部署到测试环境。
* 将它部署到实时创作环境，作者和/或管理员可在该环境中添加和配置内容。
* 将其部署到您的实时发布环境，其中使用它们为网站的访客呈现内容。

每个 AEM 组件：

* 是一种资源类型。
* 是一个完全实施特定功能的脚本的集合。
* 可以单独运行，也就是说可在 AEM 或门户中运行。

## AEM 核心组件 {#aem-core-components}

[AEM核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 是一组适用于AEM的标准化Web内容管理(WCM)组件，可加快开发速度并降低网站的维护成本。

核心组件随 AEM as a Cloud Service 提供，[WKND 教程](/help/implementing/developing/introduction/develop-wknd-tutorial.md)说明了如何实施和使用这些组件。这些组件随所有源代码一起提供，可以按原样使用或用作已修改或扩展的组件的起点。

### 查看可用组件 {#viewing-available-components}

有关AEM实例中所有可用组件的概述，请使用 [组件控制台](/help/sites-cloud/authoring/features/components-console.md).

或者，您也可以使用 CRXDE Lite 获取存储库中所有可用组件的列表。

1. 在 **[!UICONTROL CRXDE Lite]** 中，从工具栏中选择&#x200B;**[!UICONTROL 工具]**，然后选择&#x200B;**[!UICONTROL 查询]**，这将打开&#x200B;**[!UICONTROL 查询]**&#x200B;选项卡。

1. 在&#x200B;**[!UICONTROL 查询]**&#x200B;选项卡中，选择 `XPath` 作为&#x200B;**[!UICONTROL 类型]**。

1. 在 **[!UICONTROL 查询]** 输入字段，请输入以下字符串：

   `//element(*, cq:Component)`

1. 单击&#x200B;**[!UICONTROL 执行]**，这将列出组件。
