---
title: SPA简介和演练
description: 本文介绍SPA的概念，并逐步介绍如何使用基本的SPA应用程序进行创作，并说明它与底层AEM SPA编辑器的关系。
translation-type: tm+mt
source-git-commit: b8bc27b51eefcfcfa1c23407a4ac0e7ff068081e
workflow-type: tm+mt
source-wordcount: '1930'
ht-degree: 0%

---


# SPA简介和演练 {#spa-introduction}

单页应用程序(SPA)可以为网站用户优惠引人入胜的体验。 开发人员希望能够使用SPA框架构建站点，而作者希望在AEM内无缝编辑内容，使用此类框架构建站点。

SPA编辑器优惠了一个全面的解决方案，支持AEM中的SPA。 本文将逐步介绍如何使用基本的SPA应用程序进行创作，并说明它与基础的AEM SPA Editor的关系。

## 简介 {#introduction}

### 文章目标 {#article-objective}

本文介绍了SPA的基本概念，然后使用一个简单的SPA应用程序演示基本内容编辑，带领读者演练SPA编辑器。 然后深入到页面的构造以及SPA应用程序与AEM SPA Editor的关联和交互。

本简介和演练的目的是向AEM开发人员演示SPA的相关性、它们的一般工作方式、AEM SPA编辑器如何处理SPA以及它与标准AEM应用程序有何不同。

演练基于标准AEM功能和示例WKND SPA项目应用程序。 要继续操作，请 [在此处从GitHub下载并安装示例WKND SPA项目应用程序。](https://github.com/adobe/aem-guides-wknd-spa)

>[!CAUTION]
>
>此文档仅将 [WKND SPA项目应用程序用](https://github.com/adobe/aem-guides-wknd-spa) 于演示目的。 它不应用于任何项目工作。

>[!TIP]
>
>任何AEM项目都应利用 [AEM Project](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/developing/archetype/overview.html)Archetype，它支持使用React或Angular的SPA项目并利用SPA SDK。

### 什么是SPA? {#what-is-a-spa}

单页应用程序(SPA)与传统页面不同，它在客户端呈现，主要由Javascript驱动，它依赖Ajax调用加载数据和动态更新页面。 大多数或所有内容在单页加载中检索一次，并根据用户与页面的交互情况按需异步加载其他资源。

这减少了页面刷新的需求，并为用户提供了无缝、快速的体验，更像原生的App体验。

AEM SPA编辑器允许前端开发人员创建可集成到AEM站点中的SPA，使内容作者能够像编辑任何其他AEM内容一样轻松地编辑SPA内容。

### 为什么要做SPA? {#why-a-spa}

SPA更快、更流畅，更像本机应用程序，它不仅对网页的访客非常有吸引力，而且对营销人员和开发人员也极具吸引力，因为SPA的工作方式。

![SPA优势](assets/spa-benefits.png)

#### 访客数 {#visitors}

* 访客在与内容交互时需要类似于原生的体验。
* 有明确的数据表明，页面越快，转换的可能性就越大。

#### 营销人员 {#marketers}

* 营销人员希望优惠丰富的类似于原生的体验，以吸引访客充分参与内容。
* 个性化可以让这些体验更加引人注目。

#### 开发人员 {#developers}

* 开发人员希望将内容和演示之间的疑虑清晰地分开。
* 清洁分离使系统更具扩展性，并允许独立的前端开发。

### SPA如何工作？ {#how-does-a-spa-work}

SPA的主要思想是减少对服务器的调用和对服务器的依赖，以最大限度地减少由服务器延迟引起的延迟，使SPA接近本机应用程序的响应。

在传统的连续网页中，只加载立即页面所需的数据。 这意味着当访客移到其他页面时，将调用服务器获取其他资源。 当访客与页面上的元素交互时，可能需要进行其他调用。 由于页面必须跟上访客的请求，因此这些多次调用可能会产生延迟或延迟。

![顺序体验与流畅体验](assets/spa-sequential-vs-fluid.png)

为了获得更流畅的体验，SPA在第一次加载时为访客加载所有必要的访客数据，这接近从移动本机应用程序中的期望。 尽管这一过程一开始可能需要稍长一些，但随后它就不再需要额外的服务器调用。

通过在客户端进行渲染，页面元素可以更快地反应，并且访客可以立即与页面进行交互。 可能需要的任何其他数据都将异步调用，以最大化页面速度。

>[!TIP]
>
>有关AEM中SPA工作方式的技术详细信息，请参阅文章：
>* [AEM SPA快速入门（使用React）](getting-started-react.md)
>* [AEM SPA入门（使用角度）](getting-started-angular.md)

>
>
要详细了解SPA编辑器的设计、架构和技术工作流程，请参阅文章：
>* [SPA编辑器概述](editor-overview.md)。


## SPA内容编辑体验 {#content-editing-experience-with-spa}

当构建SPA以利用AEM SPA编辑器时，内容作者注意到在编辑和创建内容时没有区别。 通用的AEM功能可用，无需更改作者的工作流程。

1. 在AEM中编辑WKND SPA项目应用程序。

   `http://localhost:4502/editor.html/content/wknd-spa-react/us/en/home.html`

   ![WKND SPA项目主页](assets/wknd-home.png)

1. 选择一个文本组件，注意工具栏的显示方式与任何其他组件相同。 选择&#x200B;**编辑**。

   ![选择文本组件](assets/wknd-text.png)

1. 按照AEM中的正常方式编辑内容，并注意更改会保留。

   ![编辑文本](assets/wknd-edit-text.png)

1. 使用资产浏览器将新图像拖放到图像组件中。

   ![删除图像资产](assets/wkdn-drop-image.png)

1. 更改将被保留。

   ![图像已保留](assets/wknd-change-persisted.png)

与任何非SPA AEM应用程序一样，支持其他创作工具，如在页面上拖放其他组件、重新排列组件以及修改布局。

>[!NOTE]
>
>SPA编辑器不修改应用程序的DOM。 SPA本身负责DOM。
>
>要了解其工作方式，请继续阅读本文SPA应 [用程序和AEM SPA编辑器的下一节](#spa-apps-and-the-aem-spa-editor)。

## SPA应用程序和AEM SPA编辑器 {#spa-apps-and-the-aem-spa-editor}

了解SPA对最终用户的作用，然后检查SPA页面有助于更好地了解SAP应用程序如何与AEM中的SPA编辑器配合使用。

### 使用SPA应用程序 {#using-an-spa-application}

1. 在发布服务器上或使用页面编辑器的“页面信息”菜单中的“ **视图为已发布** ”选 **项，加载WKND** SPA项目应用程序。

   `http://<host>:<port>/content/wknd-spa-react/us/en/home.html`

   ![预览WKND SPA项目主页](assets/wknd-preview.png)

   请注意页面结构，包括到子页面、菜单和文章卡的导航。

1. 使用菜单导航到子页面，无需刷新即可立即加载页面。

   ![WKND SPA项目第1页](assets/wknd-page1.png)

1. 在导航子页面时，打开浏览器的内置开发人员工具并监视网络活动。

   ![网络活动](assets/wknd-network-activity.png)

   应用程序中的页面之间移动时，流量非常小。 不会重新加载页面，只请求新图像。

   SPA完全在客户端管理内容和路由。

因此，如果在子页面之间导航时页面未重新加载，页面如何加载？

下一节加 [载SPA应用程序](#loading-a-spa-application)，深入探讨加载SPA的机制以及如何同步和异步加载内容。

### 加载SPA应用程序 {#loading-a-spa-application}

1. 如果尚未加载，请在发布服务器上加载We.Retail日志应用程序，或从页面编辑器的“页面信息” **菜单中使用** “ **视图为已发布** ”选项。

   `http://<host>:<port>/content/wknd-spa-react/us/en/home.html`

   ![WKND SPA项目预览](assets/wknd-preview.png)

1. 使用浏览器的内置工具视图页面源。
1. 请注意，源的内容有限。

   ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8"/>
        <title>WKND SPA React Home Page</title>
   
        <meta name="template" content="spa-page-template"/>
        <meta name="viewport" content="width=device-width, initial-scale=1"/>
   
    <link rel="stylesheet" href="/etc.clientlibs/wknd-spa-react/clientlibs/clientlib-base.min.css" type="text/css">
   
    <meta name="theme-color" content="#000000"/>
    <link rel="icon" href="/etc.clientlibs/wknd-spa-react/clientlibs/clientlib-react/resources/favicon.ico"/>
    <link rel="apple-touch-icon" href="/etc.clientlibs/wknd-spa-react/clientlibs/clientlib-react/resources/logo192.png"/>
    <link rel="manifest" href="/etc.clientlibs/wknd-spa-react/clientlibs/clientlib-react/resources/manifest.json"/>
   
    <!-- AEM page model -->
    <meta property="cq:pagemodel_root_url" content="/content/wknd-spa-react/us/en.model.json"/>
    <link href="//fonts.googleapis.com/css?family=Source+Sans+Pro:400,600|Asar&display=swap" rel="stylesheet"/>
    <meta property="cq:datatype" content="JSON"/>
    <meta property="cq:wcmmode" content="edit"/>
   
    <link rel="stylesheet" href="/libs/cq/gui/components/authoring/editors/clientlibs/internal/page.min.css" type="text/css">
    <link rel="stylesheet" href="/etc.clientlibs/wcm/foundation/clientlibs/main.min.css" type="text/css">
    <script type="text/javascript" src="/libs/cq/gui/components/authoring/editors/clientlibs/internal/messaging.min.js"></script>
    <script type="text/javascript" src="/libs/cq/gui/components/authoring/editors/clientlibs/utils.min.js"></script>
    <script type="text/javascript" src="/libs/granite/author/deviceemulator/clientlibs.min.js"></script>
    <script type="text/javascript" src="/libs/cq/gui/components/authoring/editors/clientlibs/internal/page.min.js"></script>
    <script type="text/javascript" src="/etc.clientlibs/wcm/foundation/clientlibs/main.min.js"></script>
    <script type="text/javascript" src="/etc.clientlibs/clientlibs/granite/jquery.min.js"></script>
    <script type="text/javascript" src="/etc.clientlibs/clientlibs/granite/utils.min.js"></script>
    <script type="text/javascript" src="/etc.clientlibs/clientlibs/granite/jquery/granite.min.js"></script>
    <script type="text/javascript" src="/etc.clientlibs/foundation/clientlibs/jquery.min.js"></script>
    <script type="text/javascript" src="/etc.clientlibs/foundation/clientlibs/shared.min.js"></script>
   
    <!--cq{"decorated":false,"type":"cq/cloudconfig/components/scripttags/header","path":"/content/wknd-spa-react/us/en/home/jcr:content/cloudconfig-header","structurePath":"/content/wknd-spa-react/us/en/home/jcr:content/cloudconfig-header","selectors":null,"servlet":"Script /libs/cq/cloudconfig/components/scripttags/header/header.html","totalTime":2,"selfTime":2}-->
   
    <link rel="stylesheet" href="/etc.clientlibs/wknd-spa-react/clientlibs/clientlib-react.min.css" type="text/css">
   
    </head>
   
    <body class="page basicpage">
        <noscript>You need to enable JavaScript to run this app.</noscript>
    <div id="spa-root"></div>
   
    <script type="text/javascript" src="/etc.clientlibs/wknd-spa-react/clientlibs/clientlib-react.min.js"></script>
   
    <script type="text/javascript" src="/etc.clientlibs/core/wcm/components/commons/site/clientlibs/container.min.js"></script>
    <script type="text/javascript" src="/etc.clientlibs/wknd-spa-react/clientlibs/clientlib-base.min.js"></script>
   
    <script type="text/javascript" src="/libs/cq/gui/components/authoring/editors/clientlibs/internal/pagemodel/messaging.min.js"></script>
   
    <link rel="stylesheet" href="/etc.clientlibs/wknd-spa-react/clientlibs/clientlib-author.min.css" type="text/css">
   
    <!--cq{"decorated":true,"type":"cq/cloudserviceconfigs/components/servicecomponents","path":"/content/wknd-spa-react/us/en/home/jcr:content/cloudservices","selectors":null,"servlet":"Script /libs/cq/cloudserviceconfigs/components/servicecomponents/servicecomponents.jsp","totalTime":2,"selfTime":2}-->
   
    <!--cq{"decorated":false,"type":"cq/cloudconfig/components/scripttags/footer","path":"/content/wknd-spa-react/us/en/home/jcr:content/cloudconfig-footer","structurePath":"/content/wknd-spa-react/us/en/home/jcr:content/cloudconfig-footer","selectors":null,"servlet":"Script /libs/cq/cloudconfig/components/scripttags/footer/footer.html","totalTime":2,"selfTime":2}-->
   
    </body>
    </html>
    <!--cq{"decorated":false,"type":"wknd-spa-react/components/page","path":"/content/wknd-spa-react/us/en/home/jcr:content","selectors":null,"servlet":"Script /apps/spa-project-core/components/page/page.html","totalTime":39,"selfTime":33}-->
   ```

   页面的正文中没有任何内容。 它主要由样式表和对各种脚本的调用组成，如 `clientlib-react.min.js`。

   这些脚本是此应用程序的主要驱动程序，负责呈现所有内容。

1. 使用浏览器的内置工具检查页面。 查看完全加载的DOM的内容。

   ![DOM of WKND SPA项目](assets/wknd-dom.png)

1. 切换到检查器中的“网络”选项卡并重新加载该页。

   忽略图像请求，请注意为页面加载的主要资源包括页面本身、CSS、React Javascript、其依赖项以及页面的JSON数据。

   ![WKND SPA项目网络活动](assets/wknd-network.png)

1. 在新选 `home.model.json` 项卡中加载。

   `http://<host>:<port>/content/wknd-spa-react/us/en/home.model.json`

   ![WKND SPA项目主页的JSON](assets/wknd-json.png)

   AEM SPA Editor利用 [AEM Content](/help/assets/content-fragments/content-fragments.md) Services将页面的整个内容作为JSON模型提供。

   通过实现特定界面，Sling Models为SPA提供必要的信息。 JSON投放的会向下委派给每个组件（从页面、段落、组件等）。

   每个组件都选择它公开的内容以及呈现方式（在服务器端使用HTL，在客户端使用React或Angular）。 本文重点介绍使用React进行客户端渲染。

1. 该模型还可以将页面分组在一起，以便它们同步加载，从而减少需要重新加载的页面数。

   在We.Retail日志的示例中，将同 `home`步加 `page-1`载、 `page-2`和 `page-3` 页面，因为访客通常访问所有这些页面。

   此行为不是强制的，并且完全可以定义。

   ![WKND SPA项目项分组](assets/wknd-pages.png)

1. 要视图行为上的这种差异，请重 `home` 新加载页面并清除检查器的网络活动。 导航到 `page-1` 页面菜单中，您会发现唯一的网络活动是对的图像的请求 `page-1`。 `page-1` 本身无需加载。

   ![WKND SPA项目第1页网络活动](assets/wknd-page1-network.png)

### 与SPA编辑器交互 {#interaction-with-the-spa-editor}

使用示例WKND SPA项目应用程序，可以清楚地了解应用程序的行为和发布时的加载方式，利用内容服务进行JSON内容投放以及异步加载资源。

此外，对于内容作者而言，使用SPA编辑器在AEM中创建内容是无缝的。

在下一节中，我们将探索允许SPA编辑器将SPA中的组件与AEM组件关联并实现无缝编辑体验的合同。

1. 在编辑器中加载WKND SPA项目应用程序并切换到 **预览** 模式。

   `http://<host>:<port>/editor.html/content/wknd-spa-react/us/en/home.html`

1. 使用浏览器内置的开发人员工具检查页面内容。 使用选择工具，在页面上选择一个可编辑的组件，然后视图元素详细信息。

   请注意，该组件具有新的数据属性 `data-cq-data-path`。

   ![检查WKND SPA项目元素](assets/wknd-inspector.png)

   例如

   `data-cq-data-path="/content/wknd-spa-react/us/en/home/jcr:content/root/responsivegrid/text`

   此路径允许检索和关联每个组件的编辑上下文配置对象。

   这是编辑器将其识别为SPA中的可编辑组件所需的唯一标记属性。 根据此属性，SPA编辑器将确定与组件关联的可编辑配置，以便正确的框架、工具栏等。 已加载。

   还为标记占位符和资产拖放功能添加了一些特定类名称。

   >[!NOTE]
   >
   >此行为与AEM中服务器端呈现的页面不同，在中，每个可编辑组件 `cq` 都插入了一个元素。
   >
   >SPA编辑器中的此方法消除了注入自定义元素的需要，只依赖附加的数据属性，使前端开发者的标记更简单。

## 后续步骤 {#next-steps}

现在，您已了解AEM的SPA编辑体验以及SPA与SPA编辑器的关系，进一步了解SPA的构建方式。

* [AEM中SPA使用入门](getting-started-react.md) ，显示如何构建基本SPA以使用React与AEM中的SPA编辑器配合使用
* [AEM SPA使用角度式入门](getting-started-angular.md) ，显示如何构建基本SPA以使用角度式SPA与AEM的SPA编辑器配合使用
* [SPA编辑器概述](editor-overview.md) 深入介绍AEM与SPA之间的通信模型。
* [为AEM开发SPA](developing.md) ，介绍如何吸引前端开发人员来为AEM开发SPA，以及SPA如何与AEM体系结构交互。
