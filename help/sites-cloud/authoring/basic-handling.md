---
title: 基本处理
description: 轻松自如地导航 AEM 及其基本用法
exl-id: ae87a63a-c6d3-4220-ab3d-07a20b21b93b
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 9a700e9eb3116252f42bb08db9dadc0e8a6adbf7
workflow-type: tm+mt
source-wordcount: '954'
ht-degree: 61%

---


# 基本处理 {#basic-handling}

本文档旨在概述使用AEM创作环境时的基本操作。

>[!TIP]
>
>用户在整个AEM环境中都可以使用键盘快捷键。 特别是当[使用站点控制台](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md)和[页面编辑器](/help/sites-cloud/authoring/page-editor/keyboard-shortcuts.md)时。

## 触屏优化 UI {#a-touch-enabled-ui}

AEM 启用了针对触屏的用户界面。触屏界面允许您使用触屏，通过点按、点按并按住和轻扫之类的手势与软件进行交互。 由于 AEM UI 支持触控，因此您可以在手机或平板电脑等触控设备上使用触控手势。但是，您也可以使用传统桌面设备上的鼠标操作，灵活地选择创作内容的方式。

## 首要步骤 {#first-steps}

登录后，您将立即转到[“导航”面板](#navigation-panel)。选择其中一个选项会打开相应的控制台。

![“导航”面板](assets/basic-handling-navigation.png)

为了使您更好地了解 AEM 的基本用法，本文档基于&#x200B;**Sites**&#x200B;控制台进行了介绍。在&#x200B;**站点**&#x200B;上选择以开始。

## 产品导航 {#product-navigation}

每当用户首次访问某个控制台时，都会启动一个产品导航教程。请花上一分钟时间来选择，了解有关AEM基本处理方式的详尽概述。

![导航教程](assets/basic-handling-tutorial.png)

选择&#x200B;**下一步**&#x200B;以前进到概述的下一页。 选择&#x200B;**关闭**&#x200B;或在概述对话框之外选择关闭。

该概述将在您下次访问控制台时重新启动，除非您查看所有幻灯片或者选中&#x200B;**不再显示此对话框**&#x200B;选项。

## 全局导航 {#global-navigation}

您可以使用全局导航面板在控制台之间导航。当您选择屏幕左上角的&#x200B;**Adobe Experience Manager**&#x200B;链接时，这会触发为全屏下拉列表。

通过单击或点按&#x200B;**关闭**&#x200B;可关闭全局导航面板，以返回到您之前所在的位置。

![导航面板顶栏](assets/basic-handling-navigation-options.png)

全局导航有两个面板，它们由屏幕左侧的图标来表示：

* **[导航](#navigation-panel)** — 登录到AEM时由指南针和默认面板表示
* **[工具](#tools-panel)** – 由一个锤子图标来表示

这些面板中的可用选项如下所述。

### “导航”面板 {#navigation-panel}

**导航**&#x200B;面板：

![导航面板](assets/basic-handling-navigation.png)

当您在控制台和内容中导航时，浏览器选项卡的标题将更新以反映您的位置。

在“导航”中，可用的控制台有：

| 控制台 | 用途 |
|---|---|
| 项目 | 通过“项目”控制台，您可以直接访问您的项目。[项目是虚拟功能板](/help/sites-cloud/authoring/projects/overview.md)，可用于组建团队。然后，您可以为该团队提供对资源、工作流和任务的访问权限，从而让人们朝着一个共同目标努力。 |
| Sites | [站点控制台](/help/sites-cloud/authoring/sites-console/introduction.md)允许您创建、查看和管理在AEM实例上运行的站点。 通过此，您可以创建、编辑、复制、移动和删除页面、启动工作流以及发布页面。 |
| 体验片段 | [体验片段](/help/sites-cloud/authoring/fragments/content-fragments.md)是独立的体验，可以跨渠道重复使用，也可以具有变体，从而避免反复地复制和粘贴体验或体验的部分内容。 |
| 资源 | 通过“资源”控制台，您可以导入和管理[数字资源，如图像、视频、文档和音频文件](/help/assets/overview.md)。随后，这些资源便可由同一 AEM 实例上运行的任何站点使用。您还可以从 Assets 控制台创建和管理[内容片段](/help/assets/content-fragments/content-fragments.md)。 |
| 个性化 | 此控制台为[创作目标内容和呈现个性化体验](/help/sites-cloud/authoring/personalization/overview.md)提供了一个工具框架。 |
| 内容片段 | 您可使用[内容片段](/help/sites-cloud/administering/content-fragments/overview.md)设计、创建、管理和发布独立于页面的内容。它们允许您准备结构化内容，以准备在多个位置/多个渠道上使用，非常适合于页面创作和 headless 投放。 |
| 生成变体 | [生成变体](/help/generative-ai/generate-variations.md)使用生成人工智能(AI)根据提示创建内容变体；这些提示由Adobe提供或由用户创建和管理。 |

## “工具”面板 {#tools-panel}

**工具**&#x200B;面板有一个侧面板，其中包含一系列类别，这些类别将相似的控制台组合在一起。 **工具**&#x200B;控制台提供对几个专用工具和控制台的访问权限，这些工具和控制台可帮助您管理网站、数字资产及内容存储库的其他方面。

![“工具”面板](assets/basic-handling-tools.png)

## 标题 {#the-header}

标题始终显示在屏幕顶部。无论您位于系统中的何处，标题中的大部分选项都将保持不变，但也有一些选项是特定于上下文的。

![导航标题](/help/sites-cloud/authoring/assets/basic-handling-navigation-bar.png)

* [全局导航](#global-navigation) — 选择&#x200B;**Adobe Experience Manager**&#x200B;链接可在各控制台之间导航。

  ![全局导航](/help/sites-cloud/authoring/assets/basic-handling-global-navigation.png)

* 反馈

  ![反馈按钮](/help/sites-cloud/authoring/assets/basic-handling-feedback.png)

* 您的IMS组织 — 根据需要选择进行更改。

* [解决方案](https://www.adobe.com/cn/cn/experience-cloud.html) — 选择此项可访问您的其他Adobe解决方案。

  ![“解决方案”按钮](/help/sites-cloud/authoring/assets/basic-handling-solutions.png)

* [搜索](/help/sites-cloud/authoring/search.md) — 您还可以使用[快捷键](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md) `/`（正斜杠）从任何控制台调用搜索。

  ![“搜索”图标](/help/sites-cloud/authoring/assets/basic-handling-search-icon.png)

* [帮助](#accessing-help)

  ![“帮助”按钮](/help/sites-cloud/authoring/assets/basic-handling-help-icon.png)

* [通知](/help/sites-cloud/authoring/inbox.md) -   此图标带有当前分配的未完成通知的编号。

  ![“通知”按钮](/help/sites-cloud/authoring/assets/basic-handling-notifications.png)

* [用户属性](/help/sites-cloud/authoring/account-environment.md) — 选择此项可更改您的用户设置。

  ![“用户属性”按钮](/help/sites-cloud/authoring/assets/basic-handling-user-properties.png)

## 访问帮助 {#accessing-help}

有许多可用的帮助资源以及几种访问帮助资源的方法。

* **工具栏** — 根据您的位置，**帮助**&#x200B;图标将打开相应的资源：

  ![“帮助”图标](assets/basic-handling-help.png)

* **控制台** — 第一次导航系统时，[一连串幻灯片将介绍AEM导航](#product-navigation)。

  ![教程](assets/basic-handling-console-tutorial.png)

* **页面编辑器** — 首次编辑页面时，会有一系列幻灯片介绍该页面编辑器。

  ![编辑器教程](assets/basic-handling-editor-tutorial.png)

   * 与在首次访问任何控制台时浏览[产品导航概述](#product-navigation)一样，浏览此概述。
   * 在&#x200B;[**页面信息**&#x200B;菜单中，可以随时通过选择&#x200B;**帮助**](#accessing-help)&#x200B;来再次显示这些幻灯片。

* **工具控制台** — 您也可以从&#x200B;**工具**&#x200B;控制台访问外部&#x200B;**资源**：

   * **文档** – 查看 Web 体验管理文档
   * **开发人员资源** – 开发人员资源和下载

>[!TIP]
>
>在控制台中，您可以随时使用热键 `?`（问号）访问提供的快捷键概述。
>
>有关所有键盘快捷键的概述，请参阅以下文档：
>
>* [用于编辑页面的键盘快捷键](/help/sites-cloud/authoring/page-editor/keyboard-shortcuts.md)
>* [控制台的键盘快捷键](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md)
