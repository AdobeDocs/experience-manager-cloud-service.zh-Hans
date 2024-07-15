---
title: 组织页面
description: 了解如何使用AEM整理您的网站。
exl-id: c57096ca-34fe-4b19-98e0-8f3cd43cf24e
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 67%

---


# 组织页面 {#creating-and-organizing-pages}

了解如何使用AEM整理您的网站。 了解如何组织页面后，您可以[创建新页面](/help/sites-cloud/authoring/sites-console/creating-pages.md)和[管理现有页面。](/help/sites-cloud/authoring/sites-console/managing-pages.md)

{{edge-delivery-authoring}}

## 组织您的站点 {#organizing-your-site}

作为作者，您需要在AEM中整理您的站点。 这包括创建和命名您的内容页面，因此：

* 您可以轻松地在创作环境中找到这些页面
* 您站点的访客可以方便地在发布环境中浏览这些页面

您还可以使用[文件夹](#creating-a-new-folder)来帮助组织内容。

网站的结构可被认为是保留您的内容页面的树。这些内容页面的名称用于组成 URL，而标题则会在查看页面内容时显示出来。

以下显示了[WKND教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=zh-Hans)网站上的一个示例，该网站上有一篇关于滑板场(`la-skateparks`)的文章：

`http://<host>:<port>/editor.html/content/wknd/en/sports/la-skateparks.html`

```xml
 /content
 /wknd
  /en
   /music
    /...
   /sports
    /la-skateparks
    /five-gyms-la
    /mountain-bike-routes
   /shopping
    /...
   /art
    /...
   /...
```

此结构可以从&#x200B;[**站点**&#x200B;控制台](/help/sites-cloud/authoring/sites-console/introduction.md)中查看，您可以在此控制台中导航浏览网站的各个页面，并对这些页面执行操作。

## 页面命名惯例 {#page-naming-conventions}

创建页面时，需填写以下两个关键字段：

* **[标题](#title)**：
   * 它会在控制台中向用户显示并在编辑中的页面内容顶部显示。
   * 此字段为必填字段。
* **[名称](#name)**：
   * 用于生成 URI。
   * 此字段的用户输入是可选的。如果未指定，名称会从标题派生。请参阅以下部分[页面名称限制和最佳实践](#page-name-restrictions-and-best-practices)，以获取详细信息。

### 页面名称限制和最佳实践 {#page-name-restrictions-and-best-practices}

页面&#x200B;**标题**&#x200B;和&#x200B;**名称**&#x200B;可以单独创建，但相互关联：

* 在创建页面时，只有&#x200B;**标题**&#x200B;字段是必需字段。如果未在创建页面时提供任何&#x200B;**名称**，那么 AEM 将通过标题的前 64 个字符生成名称（观察下面列出的验证）。仅使用前 64 个字符是为了支持短页面名称的最佳实践。
* 如果作者手动指定了页面名称，则 64 字符限制不适用，但有关页面名称长度的其他技术限制可能适用。

>[!TIP]
>
>在定义页面名称时，一个好的经验法则是保持页面名称简短，但尽可能表达到位且容易记忆，使读者容易理解。请参阅针对 `title` 元素的 [W3C 风格指南](https://www.w3.org/Provider/Style/TITLE.html)，以获取更多信息。
>
>另请注意，某些浏览器（例如旧版本的 IE）只能接受一定长度的 URL，因此还有技术原因需缩短页面名称。

创建页面时，AEM [将依据AEM和JCR实行的惯例](/help/implementing/developing/introduction/naming-conventions.md)验证页面名称。

允许使用的字符最少包括：

* `a` 至 `z`
* `A` 至 `Z`
* `0` 至 `9`
* `_`（下划线）
* `-`（连字符/减号）

有关允许使用的所有字符的完整详细信息，请参阅[命名惯例](/help/implementing/developing/introduction/naming-conventions.md)。

>[!NOTE]
>
>页面名称长度限制为 150 个字符。

### 标题 {#title}

如果您在创建页面时只提供页面&#x200B;**Title**，则AEM将从此字符串派生页面&#x200B;**Name**，然后[根据AEM和JCR实行的约定](/help/implementing/developing/introduction/naming-conventions.md)验证该名称。

虽然接受包含无效字符的&#x200B;**标题**&#x200B;字段，但派生的名称会将无效的字符替换掉。例如：

| 标题 | 派生的名称 |
|---|---|
| Schön | `schoen.html` |
| SC%&amp;&#42;ç+ | `sc---c-.html` |

### 名称 {#name}

当您在创建页面时提供页面&#x200B;**Name**&#x200B;时，AEM [将依据AEM和JCR实行的约定](/help/implementing/developing/introduction/naming-conventions.md)验证此名称。 您在&#x200B;**名称**&#x200B;字段中无法提交无效的字符。AEM 检测到无效字符时，该字段会突出显示，并提供有说明性消息。

![输入无效页面名称的示例](/help/sites-cloud/authoring/assets/organizing-invalid-name.png)

>[!TIP]
>
>应避免使用 ISO-639-1 定义的双字母代码作为页面名称，除非该页面是语言根页面。
>
>请参阅[准备翻译内容](/help/sites-cloud/administering/translation/preparation.md)以了解更多信息。

## 模板 {#templates}

在AEM中，[模板](/help/sites-cloud/authoring/sites-console/templates.md)是一种特殊类型的页面，用作正在创建的任何新页面的基础。

该模板定义了页面的结构，其中包括缩略图和其他属性。例如，您可能会有产品页面、站点地图和联系信息的单独模板。模板包括各个[组件](#components)。

AEM 附带了一些现成的模板。可用模板取决于单个网站。关键的字段如下：

* **标题** — 生成的网页上显示的标题
* **名称** — 在命名页面时使用
* **模板** — 可在生成新页面时使用的模板列表

## 组件 {#components}

[组件](/help/implementing/developing/components/overview.md)是AEM提供的元素，用于添加特定类型的内容。 AEM附带一系列开箱即用的组件，称为[核心组件，](/help/implementing/developing/components/overview.md#core-components)，它们提供了全面的功能。 组件的一些示例包括：

* 文本
* 图像
* 标题
* 轮播
* 及许多其他组件

在创建并打开页面后，您可以[使用组件添加内容](/help/sites-cloud/authoring/page-editor/edit-content.md#inserting-a-component)，这些组件可从[组件浏览器](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#components-browser)中获取。

>[!TIP]
>
>[组件控制台](/help/sites-cloud/authoring/components-console.md)提供了有关实例中相关组件的概述。
