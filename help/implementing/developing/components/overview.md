---
title: 组件概述
description: 组件是模块化单元，可以实现在网站上显示内容的特定功能
exl-id: 0fdc99e7-2103-448d-8217-d5d52c94acea
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 6%

---

# 组件概述 {#components-overview}

本页概述Adobe Experience Manager(AEM)组件，例如 [用于页面创作](/help/sites-cloud/authoring/fundamentals/components.md).

## 什么是组件？ {#what-are-components}

AEM中的组件包括：

* 模块化单元，可实现在网站上呈现内容的特定功能。
* 可重复使用。
* 开发为存储库一个文件夹内的自含单元。
* 没有隐藏的配置文件。
* 可以包含其他组件。
* 可以在任何AEM系统内的任意位置运行，也可以限制在特定组件下运行。
* 拥有标准化的用户界面。
* 具有可配置的编辑行为。
* 使用使用基于Granite UI组件的子元素构建的对话框。
* 使用 [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/using/overview.html?lang=zh-Hans).
* 可以开发以创建可扩展默认功能的自定义组件。

由于组件是模块化的，因此您可以：

* 在本地实例上开发新组件。
* 将其部署到测试环境。
* 将其部署到实时创作环境，在该环境中，作者和/或管理员可以添加和配置内容。
* 将其部署到实时发布环境，在该环境中，访客可使用这些环境向网站的访客呈现内容。

每个AEM组件：

* 是资源类型。
* 是完全实现特定功能的脚本集合。
* 可以单独运行，即在AEM或门户中运行。

## AEM 核心组件 {#aem-core-components}

[AEM核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans) 是一套适用于AEM的标准化Web内容管理(WCM)组件，可加快开发时间并降低网站维护成本。

核心组件提供了AEMas a Cloud Service，并且 [WKND教程](/help/implementing/developing/introduction/develop-wknd-tutorial.md) 说明了如何实施和使用组件。 这些组件提供了所有源代码，可以按原样使用，也可以用作修改或扩展组件的起点。

### 查看可用组件 {#viewing-available-components}

要概述AEM实例中的所有可用组件，请使用 [组件控制台](/help/sites-cloud/authoring/features/components-console.md).

或者，您还可以使用CRXDE Lite获取存储库中所有可用组件的列表。

1. 在 **[!UICONTROL CRXDE Lite]**，选择 **[!UICONTROL 工具]** ，然后 **[!UICONTROL 查询]**，以打开 **[!UICONTROL 查询]** 选项卡。

1. 在 **[!UICONTROL 查询]** 选项卡，选择 `XPath` as **[!UICONTROL 类型]**.

1. 在&#x200B;**[!UICONTROL 查询]**&#x200B;输入字段中，输入以下字符串：

   `//element(*, cq:Component)`

1. 单击 **[!UICONTROL 执行]** 和组件列出。
