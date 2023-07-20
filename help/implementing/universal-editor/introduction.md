---
title: Universal Visual Editor 简介
description: 了解 Universal Visual Editor（又名 Universal Editor）如何实现所见即所得 (what-you-see-is-what-you-get, WYSIWYG) 编辑任何 Headless 和 Headful 体验。 了解它如何帮助内容作者提供卓越的体验、提高他们的内容速度，以及如何提供最先进的开发人员体验。
exl-id: d4fc2384-a0f5-4a6f-9572-62749786be4c
source-git-commit: 0f62245d31074ab7a64d86b97ef3b1a8d7533001
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 97%

---


# Universal Visual Editor 简介 {#introduction}

了解 Universal Visual Editor（又名 Universal Editor）如何实现所见即所得 (what-you-see-is-what-you-get, WYSIWYG) 编辑任何 Headless 和 Headful 体验。 了解它如何帮助内容作者提供卓越的体验、提高他们的内容速度，以及如何提供最先进的开发人员体验。

## 背景 {#background}

页面编辑器一直都是可供 AEM 内容作者使用的最强大工具。页面编辑器提供了直观、可视化、上下文相关的 WYSIWYG 创作体验，只需最少培训，并且可向作者准确展示内容的显示方式。

但是，页面编辑器只能编辑 AEM 页面内容、结构和其中包含的组件。不过，现在的内容很少源自一个位置。Universal Editor 提供了与页面编辑器相同的就地编辑体验，但适用于任意实施中的任何内容的任何方面。

## 真正的通用 {#universal}

可对 Universal Editor 进行插桩以用于任意实施、任何内容以及内容的任何方面。

![使其通用的因素是什么](assets/universal.png)

### 任意实施 {#any-implementation}

由于可以通过多种不同方式构建体验，因此，任何实施都可以利用 Universal Editor，以便作者能够执行上下文编辑。

用户通常认为，Headless实施限制作者在基于表单的UI中编辑所有内容，但通用编辑器并非如此

利用 Universal Editor 的实施的要求非常直接，并且支持以下内容：

* **任何架构** – 服务器端呈现、边缘端呈现、客户端呈现等。
* **任何框架** – Vanilla AEM，或任何第三方框架，如 React、Next.js、Angular 等。
* **任何托管** – 可以本地托管到 AEM，或托管于远程域上

### 任何内容 {#any-content}

内容作者应拥有以前由 AEM 页面编辑器提供的同样强大的编辑体验。不过，Universal Editor 允许内容作者在上下文中可视化地编辑&#x200B;**任何**&#x200B;内容，并支持：

* **AEM 页面结构** – `cq:Pages` 的嵌套 `cq:Components`，包括体验片段
* **AEM 内容片段** – 编辑内容片段中的内容，因为它们将出现在体验的上下文中。
* **文档** – 概念验证表明 Word、Excel、Google 文档或 Markdown 文档也可以用相同的方式编辑（这是 WIP）。

### 任何方面 {#any-aspect}

对于内容作者来说，内容不仅仅与包含的信息有关，还与信息的呈现和接收方式有关。内容附带了额外的元数据和插桩规则，Universal Editor 可以理解这些规则并进行编辑，包括：

* **应用布局和样式** – 通过使用样式系统，营销从业者和内容作者可以将不同的样式应用于其内容并为内容创建不同的布局，例如列、轮播、选项卡、折叠等。

## 价值 {#value}

通过将内容编辑体验与任何特定的内容交付系统分离，编辑器变得真正通用而灵活，可让内容作者提供卓越的体验，提升内容速度并提供最先进的开发人员体验。

![Universal Editor 的价值](assets/value.png)

* **提供卓越的体验** – 为了使从业者能够为访客创造引人入胜的体验，Universal Editor 允许从业人员在预览上下文中创建和编辑内容。这使他们创建的内容既能适合体验设计，又能构成对访客有意义的历程。
* **提升内容速度** – 为了简化从业人员的管理工作流程，Universal Editor 允许在预览中编辑内容，通过仅显示与该上下文相关的选项来指导从业人员，并使工作流程独立于内容源。
* **最先进的开发人员体验** – 为了支持真实的异构应用环境，Universal Editor 完全解耦且与技术无关，允许开发人员使用他们喜欢的技术堆栈来实施体验。

## 内容片段编辑器中的 Universal Visual Editor {#universal-editor-content-fragment-editor}

乍一看，Universal Visual Editor 和内容片段编辑器似乎提供了类似的编辑功能。但这些编辑器却提供了完全不同的功能，并且它们为营销从业人员完成了不同的作业。

### 内容片段编辑器 {#content-fragment-editor}

营销从业人员希望创建内容而不必关注其布局，以便它能够在多种体验环境中重复使用。

* 要完成的基本作业是扩展内容策略。

### Universal Visual Editor {#universal-editor}

营销从业人员想创建根据给定上下文的布局定制的内容，以提供卓越的体验。

* 要完成的基本作业是与读者建立令人信服的联系。

## 路线图 {#road-map}

请务必注意，Universal Editor 正处于开发阶段，本文档中列出的一些功能是最终编辑器的愿景，而不一定表示是其当前功能。

请与您的 Adobe 联系人联系，了解有关为 Universal Editor 规划的即将推出的功能的详细信息.

## 其他资源 {#additional-resources}

要了解有关 Universal Editor 的更多信息，请参阅这些文档。

* [使用 Universal Editor 创作内容](authoring.md) – 了解内容作者使用 Universal Editor 创建内容是多么轻松和直观。
* [使用 Universal Editor 发布内容](publishing.md) – 了解 Universal Visual Editor 如何发布内容以及您的应用程序如何处理发布的内容。
* [AEM Universal Editor 快速入门 ](getting-started.md) – 了解如何获取 Universal Editor 访问权限以及如何对第一个 AEM 应用程序插桩以使用 Universal Editor。
* [Universal Editor 架构](architecture.md) – 了解 Universal Editor 的架构以及数据如何在其服务和层之间流动。
* [属性和类型](attributes-types.md) – 了解 Universal Editor 所需的数据属性和类型。
* [Universal Editor 身份验证](authentication.md) – 了解 Universal Editor 如何进行身份验证。
