---
title: 为 AEM 开发 SPA
description: 本文介绍了当让前端开发人员为AEM开发SPA时应考虑的重要问题，并概述了AEM与SPA相关的体系结构，以在在AEM上部署开发的SPA时牢记这一点。
exl-id: f6c6f31a-69ad-48f6-b995-e6d0930074df
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '2072'
ht-degree: 12%

---

# 为 AEM 开发 SPA {#developing-spas-for-aem}

单页应用程序 (SPA) 可以为网站用户提供引人入胜的良好体验。开发人员希望能够使用 SPA 框架构建站点，而作者则希望能够在 AEM 中顺畅地为使用此类框架构建的站点编辑内容。

本文介绍了在让前端开发人员开发SPA for AEM时需要考虑的重要问题，并概述了AEM的架构中有关在AEM上部署SPA的部分。

## AEM的SPA开发原则 {#spa-development-principles-for-aem}

在 AEM 上开发单页应用程序时，假定前端开发人员在创建 SPA 时遵循标准最佳实践。作为前端开发人员，如果您遵循这些常规最佳实践以及一些AEM特定原则，则您的SPA可以 [AEM及其内容创作功能](introduction.md#content-editing-experience-with-spa).

* **[可移植性](#portability)** – 与任何组件一样，应构建尽可能可移植的 组件。应使用可移植且可重用的组件构建 SPA。
* **[AEM 推动站点结构](#aem-drives-site-structure)** – 前端开发人员创建组件并拥有其内部结构，但依赖 AEM 来定义站点的内容结构。
* **[动态呈现](#dynamic-rendering)** – 所有呈现都应是动态的。
* **[动态路由](#dynamic-routing)** – SPA 负责路由，AEM 负责侦听它并根据它进行提取。任何路由也应是动态的。

如果您在开发SPA时牢记这些原则，那么在启用所有受支持的AEM创作功能时，将尽可能地灵活且经得起未来考验。

如果您不需要支持AEM创作功能，则可能需要考虑其他 [SPA设计模型](#spa-design-models).

### 可移植性 {#portability}

与开发任何组件时一样，组件的设计应最大限度地提高可移植性。 应避免任何影响组件可移植性或可重用性的模式，以确保将来的兼容性、灵活性和可维护性。

生成的SPA应使用高度可移植和可重用的组件构建。

### AEM驱动器站点结构 {#aem-drives-site-structure}

前端开发人员必须自行负责创建用于构建应用程序的SPA组件库。 前端开发人员对组件的内部结构具有完全控制权。 [但是，AEM始终拥有站点的结构。](editor-overview.md)

这意味着前端开发人员可以在组件的入口点之前或之后添加客户内容，并且还可以在组件内进行第三方调用。 但是，前端开发人员无法完全控制组件的嵌套方式。

### 动态渲染 {#dynamic-rendering}

SPA应仅依赖于内容的动态渲染。 这是AEM获取并渲染内容结构的所有子项的默认预期。

任何指向特定内容的显式渲染都被视为静态渲染，尽管受支持，但与AEM内容创作功能不兼容。 这也违反了 [可移植性](#portability).

### 动态路由 {#dynamic-routing}

与渲染一样，所有路由也应是动态的。 在AEM中， [SPA应始终拥有路由](routing.md) 并且AEM会侦听该视频并根据它获取内容。

任何静态路由都对 [可移植性原理](#portability) 和通过与AEM的内容创作功能不兼容来限制作者。 例如，对于静态路由，如果内容作者想要更改路由或更改页面，则必须请求前端开发人员执行此操作。

## AEM 项目原型 {#aem-project-archetype}

任何AEM项目都应使用 [AEM项目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=zh-Hans)，支持使用React或Angular的SPA项目，并使用SPA SDK。

## SPA设计模型 {#spa-design-models}

如果 [在AEM中开发SPA的原则](#spa-development-principles-for-aem) 之后，您的SPA即可使用所有受支持的AEM内容创作功能。

但是，在某些情况下，这可能并非完全必要。 下表概述了各种设计模型、其优点和缺点。

<table>
 <tbody>
  <tr>
   <th><strong>设计模型<br /> </strong></th>
   <th><strong>优点</strong></th>
   <th><strong>缺点</strong></th>
  </tr>
  <tr>
   <td>AEM用作Headless CMS，而不使用 <a href="/help/implementing/developing/hybrid/reference-materials.md">SPA编辑器SDK框架。</a></td>
   <td>前端开发人员对应用程序拥有完全控制权。</td>
   <td><p>内容作者无法使用AEM内容创作体验。</p> <p>如果代码包含静态引用或路由，则该代码既不可移植，也无法重用。</p> <p>不允许使用模板编辑器，因此前端开发人员必须通过JCR维护可编辑模板。</p> </td>
  </tr>
  <tr>
   <td>前端开发人员使用SPA Editor SDK框架，但只向内容作者打开某些区域。</td>
   <td>开发人员通过仅启用在应用程序的受限制区域中创作，保持对应用程序的控制。</td>
   <td><p>内容作者仅限于一组有限的AEM内容创作体验。</p> <p>如果代码包含静态引用或路由，则代码可能不可移植或重用。</p> <p>不允许使用模板编辑器，因此前端开发人员必须通过JCR维护可编辑模板。</p> </td>
  </tr>
  <tr>
   <td>项目完全使用SPA编辑器SDK，前端组件开发为一个库，并且应用程序的内容结构委派给AEM。</td>
   <td><p>该应用程序可重用和移植。</p> <p>内容作者可以使用AEM内容创作体验编辑应用程序。<br /> </p> <p>SPA与模板编辑器兼容。</p> </td>
   <td><p>开发人员无法控制应用程序的结构和委派给AEM的内容部分。</p> <p>开发人员仍然可以为不应使用AEM创作的内容保留应用程序的区域。</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>虽然AEM支持所有模型，但仅通过实施第三个（从而遵循建议的） [AEM中的SPA开发原则](#spa-development-principles-for-aem))内容作者能否在AEM中与用户交互并编辑SPA的内容。

## 将现有SPA迁移到AEM {#migrating-existing-spas-to-aem}

一般情况下，如果您的SPA遵循 [AEM的SPA开发原则](#spa-development-principles-for-aem)，则您的SPA将在AEM中运行并可使用AEM SPA编辑器编辑。

按照以下步骤操作，使现有SPA准备好使用AEM。

1. **使JS组件模块化。**  — 使它们能够按任何顺序、位置和大小渲染。
1. **使用我们的SDK提供的容器将组件放在屏幕上。** - AEM提供了一个页面和段落系统组件供您使用。
1. **为每个JS组件创建一个AEM组件。** - AEM组件定义对话框和JSON输出。

## 面向前端开发人员的说明 {#instructions-for-front-end-developers}

让前端开发人员为AEM创建SPA的主要任务是就组件及其JSON模型达成一致。

以下概述了前端开发人员在开发SPA for AEM时需要执行的步骤。

1. **就组件及其JSON模型达成一致**

   前端开发人员和后端AEM开发人员需要就所需的组件和模型达成一致，以便从SPA组件到后端组件进行一对一的匹配。

   AEM组件仍然主要用于提供“编辑”对话框和导出组件模型。

1. **在React组件中，通过以下方式访问模型`this.props.cqModel`**

   在同意组件且JSON模型到位后，前端开发人员可以自由开发SPA，并且只需通过访问JSON模型即可 `this.props.cqModel`.

1. **实施组件的 `render()` 方法**

   前端开发人员实施 `render()` 方法，因为它们认为适合，并且可以使用 `cqModel` 属性。 这会输出插入到页面中的DOM和HTML片段。 这是在React中构建应用程序的标准方法。

1. **通过以下方式将组件映射到AEM资源类型`MapTo()`**

   映射存储组件类，并由提供的内部使用 `Container` 组件，用于根据给定的资源类型检索并动态实例化组件。

   它用作前端和后端之间的“粘合剂”，因此编辑器知道react组件对应于哪些组件。

   此 `Page` 和 `ResponsiveGrid` 是扩展基类的良好示例 `Container`.

1. **定义组件的 `EditConfig` 作为参数`MapTo()`**

   此参数是告诉编辑器如何在尚未渲染或没有要渲染的内容时命名组件所必需的。

1. **扩展提供的 `Container` 页面和容器的类**

   页面和段落系统应该扩展此类，以便委派到内部组件的操作可以按预期进行。

1. **实施使用HTML的路由解决方案5 `History` API。**

   当 `ModelRouter` 已启用，调用 `pushState` 和 `replaceState` 函数将触发对 `PageModelManager` 以获取模型的缺失片段。

   当前版本的 `ModelRouter` 仅支持使用指向Sling模型入口点的实际资源路径的URL。 它不支持使用虚URL或别名。

   此 `ModelRouter` 可以禁用或配置为忽略正则表达式的列表。

## 与AEM无关 {#aem-agnostic}

这些代码块说明了您的React和Angular组件如何不需要特定于Adobe或AEM的内容。

* JavaScript组件中的所有内容都与AEM无关。
* 但是，特定于AEM的是，必须使用MapTo帮助程序将JS组件映射到AEM组件。

![与AEM无关的方法](assets/aem-agnostic.png)

此 `MapTo` helper是使后端和前端组件匹配在一起的“粘合剂”：

* 它告知JS容器（或JS段落系统）哪些JS组件负责渲染JSON中存在的每个组件。
* 它向JS组件渲染的HTML添加一个HTML数据属性，以便SPA编辑器知道在编辑组件时向作者显示哪个对话框。

有关使用的更多信息 `MapTo` 以及构建SPA for AEM的一般信息，请参阅所选框架的《快速入门》指南。

* [利用 React 在 AEM 中开始使用 SPA](getting-started-react.md)
* [利用 Angular 在 AEM 中开始使用 SPA](getting-started-angular.md)

## AEM架构和SPA {#aem-architecture-and-spas}

AEM的常规架构（包括开发、创作和发布环境）在使用SPA时不会发生更改。 但是，了解SPA开发如何适应此架构很有帮助。

![AEM架构和SPA](assets/aem-architecture.png)

* **构建环境**

  这是签出SPA应用程序源和组件源的位置。

   * NPM clientlib生成器从SPA项目创建一个客户端库。
   * 该库由Maven获取，并由Maven Build插件与组件部署到AEM创作。

* **AEM Author**

  在AEM创作实例上创建内容，包括创作SPA。

  在创作环境中使用SPA编辑器编辑SPA时：

   1. SPA请求外部HTML。
   1. CSS已加载。
   1. 加载SPA应用程序的Javascript。
   1. 执行SPA应用程序时，将请求JSON，以允许应用程序构建页面的DOM，包括 `cq-data` 属性。
   1. 此 `cq-data` 属性允许编辑器加载其他页面信息，以便它知道哪些编辑配置可用于组件。

* **AEM 发布**

  在此处发布创作内容和编译的库(包括SPA应用程序工件、clientlibs和组件)以供公众使用。

* **Dispatcher / CDN**

  Dispatcher用作网站访客的AEM缓存层。
   * 请求的处理方式与它们在AEM作者中的处理方式类似，但不会请求页面信息，因为只有编辑器需要它。
   * 缓存了Javascript、CSS、JSON和HTML，优化了页面以实现快速交付。

>[!NOTE]
>
>在AEM内部，无需执行Javascript构建机制或执行Javascript本身。 AEM仅托管来自SPA应用程序的编译工件。

## 后续步骤 {#next-steps}

* [使用 React 在 AEM 中开始使用 SPA](getting-started-react.md) 说明了如何使用 React 构建基本 SPA 以与 AEM 中的 SPA 编辑器结合使用.
* [使用 Angular 在 AEM 中开始使用 SPA](getting-started-angular.md) 说明了如何使用 Angular 构建基本 SPA 以与 AEM 中的 SPA 编辑器结合使用.
* [SPA 编辑器概述](editor-overview.md)更深入地介绍了 AEM 和 SPA 之间的通信模型。
* [WKND SPA项目](wknd-tutorial.md) 是一个分步教程，用于在AEM中实施简单的SPA项目。
* [SPA的动态模型到组件映射](model-to-component-mapping.md) 说明动态模型到组件的映射以及它在AEM中的SPA中的工作方式。
* [SPA Blueprint](blueprint.md) 深入了解SPA SDK for AEM的工作原理，以防您希望在AEM中为React或Angular以外的框架实施SPA，或者只是希望更深入地了解。
