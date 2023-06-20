---
title: SPA 简介和演练
description: 本文介绍了 SPA 的概念，演练了如何使用基本 SPA 应用程序进行创作，并展示了它与底层 AEM SPA Editor 的关系。
exl-id: 8dad48d5-fa90-467c-8bec-e4b76e057f80
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '2074'
ht-degree: 94%

---

# SPA 简介和演练 {#spa-introduction}

单页应用程序 (SPA) 可以为网站用户提供引人入胜的良好体验。开发人员希望能够使用 SPA 框架构建站点，而作者则希望能够在 AEM 中顺畅地为使用此类框架构建的站点编辑内容。

SPA 编辑器提供了一个全面的解决方案来支持 AEM 中的 SPA。本文演练了如何使用基本 SPA 应用程序进行创作，并展示了它与底层 AEM SPA Editor 的关系。

## 简介 {#introduction}

### 文章目标 {#article-objective}

本文先介绍了 SPA 的基本概念，然后使用简单 SPA 应用程序来演示基本内容编辑，从而引导完成浏览 SPA 编辑器演练。随后，深入探究了页面构造以及 SPA 应用程序如何与 AEM SPA Editor 相关并与之交互。

此简介和演练的目的是，向 AEM 开发人员说明 SPA 为何相关及其通常如何工作、AEM SPA Editor 如何处理 SPA，以及它与标准 AEM 应用程序的差异。

## 要求 {#requirements}

该演练基于标准 AEM 功能和示例 WKND SPA Project 应用程序。要完成本演练，您必须拥有以下资源。

* [AEMaaCS 的最新开发 SDK](/help/release-notes/release-notes-cloud/release-notes-current.md)
   * 它应作为本地开发环境运行。
   * 您必须拥有系统的管理员权限。
* [GitHub 上提供的示例 WKND SPA Project 应用程序](https://github.com/adobe/aem-guides-wknd-spa)
   * 下载具有与 `wknd-spa-react.all-X.Y.Z-SNAPSHOT.zip` 类似名称的 [React 应用程序的最新版本](https://github.com/adobe/aem-guides-wknd-spa/releases)。
   * 下载具有与 `wknd-spa-sample-images-X.Y.Z.zip` 类似名称的[应用程序的最新示例图像](https://github.com/adobe/aem-guides-wknd-spa/releases)。
   * [使用包管理器](/help/implementing/developing/tools/package-manager.md)安装这两个包，就像安装 AEM 中的任何其他包一样。
   * 在本演练中，无需使用 Maven 安装应用程序。

>[!CAUTION]
>
>本文档仅将 [WKND SPA Project 应用程序](https://github.com/adobe/aem-guides-wknd-spa)用于演示目的。不应将它用于任何项目工作。

>[!TIP]
>
>任何AEM项目都应使用 [AEM项目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)，支持使用React或Angular的SPA项目，并使用SPA SDK。

### 什么是 SPA？ {#what-is-a-spa}

单页应用程序 (SPA) 与传统页面的不同之处在于，它在客户端呈现且主要由 Javascript 驱动，并且依靠 Ajax 调用来加载数据和动态更新页面。大多数内容或所有内容在单个页面加载中检索一次，并基于用户与页面的交互按需异步加载其他资源。

这减少了页面刷新需求，并为用户提供了一种无缝、快速且更类似于本机应用程序体验的体验。

利用 AEM SPA Editor，前端开发人员可以创建可集成到 AEM 站点中的 SPA，从而允许内容作者像编辑任何其他 AEM 内容那样轻松地编辑 SPA 内容。

### 为什么使用 SPA？ {#why-a-spa}

SPA 的工作方式的特性使其更快、更流畅且更类似于本机应用程序，从而为网页访客以及营销人员和开发人员提供一种极具吸引力的体验。

![SPA 好处](assets/spa-benefits.png)

#### 访客 {#visitors}

* 访客希望在与内容交互时获得与本地体验类似的体验。
* 有数据明确表明，页面越快，转化几率就越高。

#### 营销人员 {#marketers}

* 营销人员希望提供丰富的、与本地体验类似的体验，以促使访客充分参与互动并与内容产生共鸣。
* 个性化可以使这些体验变得更具吸引力。

#### 开发人员 {#developers}

* 开发人员希望完全分离内容和表示形式之间的关注点。
* 完全分离可提高系统的可扩展性，并允许独立的前端开发。

### SPA 的工作原理是什么？ {#how-does-a-spa-work}

SPA的主要思想是，减少对服务器的调用和对服务器的依赖性，以最大限度地减少由服务器延迟导致的延迟，使SPA接近本机应用程序的响应能力。

在传统的连续网页中，仅加载即时页面所需的数据。这意味着，当访客移至另一个页面时，将调用服务器以获取其他资源。当访客与页面上的元素交互时，可能需要额外调用。由于页面必须与访客的请求同步，因此多次调用可能会给人一种滞后或延迟的感觉。

![连续体验与流畅体验](assets/spa-sequential-vs-fluid.png)

为了实现更流畅的体验以接近访客对移动本机应用程序的期望，SPA 会在首次加载时为访客加载所有必要的数据。虽然最初可能需要花费更长的时间，但随后便不再需要额外的服务器调用。

通过在客户端进行呈现，页面元素的响应速度更快，并且访客与页面的交互是即时的。将异步调用可能需要的任何其他数据以最大限度地提高页面速度。

>[!TIP]
>
>有关 SPA 在 AEM 中的工作方式的技术详细信息，请参阅文章：
>* [利用 React 在 AEM 中开始使用 SPA](getting-started-react.md)
>* [利用 Angular 在 AEM 中开始使用 SPA](getting-started-angular.md)
>
>要详细了解 SPA 编辑器的设计、架构和技术工作流，请参阅文章：
>* [SPA 编辑器概述](editor-overview.md)。

## SPA 的内容编辑体验 {#content-editing-experience-with-spa}

当构建SPA以使用AEM SPA编辑器时，内容作者注意到在编辑和创建内容时没有区别。 提供了常用 AEM 功能，而无需更改作者的工作流。

1. 在 AEM 中编辑 WKND SPA Project 应用程序。

   `http://localhost:4502/editor.html/content/wknd-spa-react/us/en/home.html`

   ![WKND SPA Project 主页](assets/wknd-home.png)

1. 与选择任何其他组件时一样，选择文本组件将显示一个工具栏。选择&#x200B;**编辑**。

   ![选择文本组件](assets/wknd-text.png)

1. 在 AEM 中正常编辑内容，会发现更改已保存。

   ![编辑文本](assets/wknd-edit-text.png)

1. 使用资产浏览器将新图像拖放到图像组件中。

   ![删除图像资产](assets/wkdn-drop-image.png)

1. 将保留更改。

   ![保留的图像](assets/wknd-change-persisted.png)

与在任何非 SPA AEM 应用程序一样，支持其他创作工具，例如在页面上拖放其他组件、重新排列组件和修改版面。

>[!NOTE]
>
>SPA 编辑器不修改应用程序的 DOM。SPA 本身负责 DOM。
>
>要了解其工作原理，请继续阅读本文的下一部分 [SPA 应用程序和 AEM SPA Editor](#spa-apps-and-the-aem-spa-editor)。

## SPA 应用程序和 AEM SPA Editor {#spa-apps-and-the-aem-spa-editor}

通过体验 SPA 对最终用户的行为方式并检查 SPA 页面，有助于更好地了解 SAP 应用程序如何与 AEM 中的 SPA 编辑器结合使用。

### 使用 SPA 应用程序 {#using-an-spa-application}

1. 在发布服务器上或使用页面编辑器中的&#x200B;**页面信息**&#x200B;菜单上的&#x200B;**以发布的形式查看**&#x200B;选项加载 WKND SPA Project 应用程序。

   `http://<host>:<port>/content/wknd-spa-react/us/en/home.html`

   ![WKND SPA Project 主页预览](assets/wknd-preview.png)

   请注意页面结构，包括子页面、菜单和文章信息卡的导航。

1. 使用菜单导航到子页面，可以看到页面将立即加载，而无需刷新。

   ![WKND SPA Project 页面 1](assets/wknd-page1.png)

1. 打开浏览器的内置开发人员工具，并在您浏览子页面时监控网络活动。

   ![网络活动](assets/wknd-network-activity.png)

   在应用程序中从一个页面移至另一个页面时，几乎不产生流量。不会重新加载页面，而只请求新图像。

   SPA 完全在客户端管理内容和路由。

那么，如果在子页面中导航时没有重新加载页面，如何加载页面呢？

在下一部分[加载 SPA 应用程序](#loading-a-spa-application)中，我们将深入探究 SPA 的加载机制以及如何以同步方式和异步方式加载内容。

### 加载 SPA 应用程序 {#loading-a-spa-application}

1. 如果未加载，请在发布服务器上或使用页面编辑器中的&#x200B;**页面信息**&#x200B;菜单上的&#x200B;**以发布的形式查看**&#x200B;选项加载 WKND SPA Project 应用程序。

   `http://<host>:<port>/content/wknd-spa-react/us/en/home.html`

   ![WKND SPA Project 预览](assets/wknd-preview.png)

1. 使用浏览器的内置工具可查看页面的源。
1. 请注意，源的内容是有限的。
   * 页面的正文中没有任何内容。它主要由样式表和对各种脚本（例如 `clientlib-react.min.js`）的调用构成。
   * 这些脚本是此应用程序的主要驱动程序，负责呈现所有内容。

1. 可以使用浏览器的内置工具检查页面。查看完全加载的 DOM 的内容。

   ![WKND SPA Project 的 DOM](assets/wknd-dom.png)

1. 切换到检查器中的“网络”选项卡并重新加载页面。

   忽略图像请求，请注意，为页面加载的主要资源包括页面本身、CSS、React Javascript、其依赖项以及页面的 JSON 数据。

   ![WKND SPA Project 网络活动](assets/wknd-network.png)

1. 在新选项卡中加载 `home.model.json`。

   `http://<host>:<port>/content/wknd-spa-react/us/en/home.model.json`

   ![WKND SPA Project 的 JSON 主页](assets/wknd-json.png)

   AEM SPA编辑器使用 [AEM内容服务](/help/sites-cloud/administering/content-fragments/content-fragments.md) 以JSON模型形式交付页面的整个内容。

   通过实施特定接口，Sling 模型为 SPA 提供了必要信息。将 JSON 数据的交付工作向下委派给每个组件（从页面到段落再到组件等）。

   每个组件选择它公开的内容及其呈现方式（在服务器端，使用 HTL；在客户端，使用 React 或 Angular）。本文重点介绍使用 React 进行客户端呈现。

1. 该模型还可以对页面进行分组以便同步加载它们，从而减少所需的页面重新加载次数。

   在 WKND SPA Project 应用程序示例中，`home`、`page-1`、`page-2` 和 `page-3` 页面将同步加载，因为访客通常会访问所有这些页面。

   此行为不是强制性的，而是完全可定义的。

   ![WKND SPA Project 项目分组](assets/wknd-pages.png)

1. 要查看此行为差异，请重新加载 `home` 页面并清除检查器的网络活动。导航到页面菜单中的 `page-1`，可以看到唯一的网络活动是请求 `page-1` 的图像。`page-1` 本身无需加载。

   ![WKND SPA Project page-1 网络活动](assets/wknd-page1-network.png)

### 与 SPA 编辑器进行交互 {#interaction-with-the-spa-editor}

通过使用示例 WKND SPA Project 应用程序，可以清楚地了解应用程序在发布时的行为和加载方式，如何使用内容服务进行 JSON 内容交付以及如何异步加载资源。

此外，对于内容作者而言，在 AEM 中使用 SPA 编辑器创建内容是无缝操作。

在下一部分中，我们将探究允许 SPA 编辑器将 SPA 中的组件与 AEM 组件相关联并实现此无缝编辑体验的合同。

1. 在编辑器中加载 WKND SPA Project 应用程序并切换到&#x200B;**预览**&#x200B;架构。

   `http://<host>:<port>/editor.html/content/wknd-spa-react/us/en/home.html`

1. 使用浏览器的内置开发人员工具检查页面内容。使用选择工具，在页面上选择一个可编辑的组件并查看元素详细信息。

   请注意，该组件具有一个新的数据属性 `data-cq-data-path`。

   ![检查 WKND SPA Project 元素](assets/wknd-inspector.png)

   例如

   `data-cq-data-path="/content/wknd-spa-react/us/en/home/jcr:content/root/responsivegrid/text`

   此路径允许检索和关联每个组件的编辑上下文配置对象。

   这是编辑器将组件识别为 SPA 中的可编辑组件所需的唯一标记属性。根据此属性，SPA 编辑器将确定哪项可编辑的配置与组件关联，以便加载正确的框架、工具栏等。

   还为标记占位符和资产拖放功能添加了一些特定的类名。

   >[!NOTE]
   >
   >此行为不同于 AEM 中的服务器端呈现的页面，其中为每个可编辑组件插入了一个 `cq` 元素。
   >
   >SPA 编辑器中的此方法消除了注入自定义元素的需求，仅依靠额外的数据属性，并为前端开发人员简化了标记。

## AEM 中的 Headful 和 Headless {#headful-headless}

可以通过 AEM 中灵活的集成级别启用 SPA，包括在 AEM 外部开发和维护的 SPA。此外，SPA可以在AEM中使用，同时还可以使用AEM无头地向其他端点提供内容。

>[!TIP]
>
>有关更多信息，请参阅文档 [AEM 中的 Headful 和 Headless](/help/implementing/developing/headful-headless.md)。

## 后续步骤 {#next-steps}

现在，您已了解 AEM 中的 SPA 编辑体验以及 SPA 与 SPA 编辑器的关系，请更深入地了解 SPA 的构建方式。

* [使用 React 在 AEM 中开始使用 SPA](getting-started-react.md) 说明了如何使用 React 构建基本 SPA 以与 AEM 中的 SPA 编辑器结合使用
* [使用 Angular 在 AEM 中开始使用 SPA](getting-started-angular.md) 说明了如何使用 Angular 构建基本 SPA 以与 AEM 中的 SPA 编辑器结合使用
* [SPA 编辑器概述](editor-overview.md)更深入地介绍了 AEM 和 SPA 之间的通信模型。
* [为 AEM 开发 SPA](developing.md) 介绍了如何让前端开发人员为 AEM 开发 SPA，以及 SPA 如何与 AEM 的架构进行交互。
