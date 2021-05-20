---
title: SPA编辑器概述
description: 本文全面概述了SPA Editor及其工作方式，包括AEM中SPA Editor交互的详细工作流程。
exl-id: 9814d86e-8d87-4f7f-84ba-6943fe6da22f
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '1641'
ht-degree: 1%

---

# SPA编辑器概述{#spa-editor-overview}

单页应用程序 (SPA) 可以为网站用户提供引人入胜的良好体验。开发人员希望能够使用SPA框架构建站点，而作者则希望在AEM中为使用此类框架构建的站点无缝编辑内容。

SPA编辑器提供了一个全面的解决方案，可在AEM中支持SPA。 本页概述了AEM中SPA支持的结构、SPA编辑器的工作方式以及SPA框架和AEM如何保持同步。

## 简介 {#introduction}

使用常用SPA框架(如React和Angular)构建的站点通过动态JSON加载其内容，并且不提供AEM页面编辑器必须的HTML结构才能放置编辑控件。

要在AEM中启用SPA的编辑功能，需要SPA的JSON输出与AEM存储库中的内容模型之间的映射，才能保存对内容所做的更改。

AEM中的SPA支持引入了一个精简JS层，当该层在页面编辑器中加载时，会与SPA JS代码交互，通过该层可以发送事件，并且可以激活编辑控件的位置以允许进行上下文编辑。 此功能基于Content Services API端点概念，因为SPA中的内容需要通过Content Services加载。

有关AEM中SPA的更多详细信息，请参阅以下文档：

* [SPA ](blueprint.md) Blueprint，以满足SPA的技术要求
* [AEM SPA使用React快速入门，](getting-started-react.md) 以快速了解使用React的简单SPA
* [AEM SPA使用Angular快速入](getting-started-angular.md) 门，快速浏览使用Angular的简单SPA

## 设计 {#design}

SPA的页面组件不会通过JSP或HTL文件提供其子组件的HTML元素。 此操作将委派给SPA框架。 子组件或模型的表示形式将从JCR中作为JSON数据结构获取。 然后，会根据该结构将SPA组件添加到页面中。 此行为可将页面组件的初始主体构成与非SPA对应项区分开来。

### 页面模型管理{#page-model-management}

页面模型的解析和管理将委派给提供的`PageModel`库。 SPA必须使用页面模型库才能进行初始化，并由SPA编辑器进行创作。 页面模型库通过`aem-react-editable-components` npm间接提供给AEM页面组件。 页面模型是AEM和SPA之间的解释器，因此必须始终存在。 创作页面时，必须添加一个额外的库`cq.authoring.pagemodel.messaging`才能启用与页面编辑器的通信。

如果SPA页面组件从页面核心组件继承，则可使`cq.authoring.pagemodel.messaging`客户端库类别可用的选项有两个：

* 如果模板是可编辑的，请将其添加到页面策略中。
* 或使用`customfooterlibs.html`添加类别。

对于导出模型中的每个资源，SPA将映射一个将执行
呈现。 该模型以JSON形式表示，然后使用容器中的组件映射来呈现。

![SPA中的模型和组件映射](assets/model-component-mapping.png)

>[!CAUTION]
>
>`cq.authoring.pagemodel.messaging`类别的包含应限于SPA编辑器的上下文。

### 通信数据类型{#communication-data-type}

将`cq.authoring.pagemodel.messaging`类别添加到页面后，它会向页面编辑器发送消息以建立JSON通信数据类型。 当通信GET类型设置为JSON时，数据请求将与组件的Sling模型端点通信。 在页面编辑器中发生更新后，更新组件的JSON表示形式将发送到页面模型库。 然后，页面模型库会通知SPA进行更新。

![SPA通信](assets/communication.png)

## 工作流 {#workflow}

您可以将SPA编辑器视为SPA和AEM之间的调解者，从而了解与之间交互的流程。

* 页面编辑器与SPA之间的通信是使用JSON而不是HTML进行的。
* 页面编辑器通过iFrame和消息传送API向SPA提供页面模型的最新版本。
* 页面模型管理器会通知编辑器已准备好进行编辑，并将页面模型作为JSON结构传递。
* 编辑器不会更改或甚至访问所创作页面的DOM结构，而是会提供最新的页面模型。

![SPA工作流](assets/workflow.png)

### 基本SPA编辑器工作流{#basic-spa-editor-workflow}

请记住SPA编辑器的关键元素，创作人员可以看到在AEM中编辑SPA的高级工作流，如下所示。

![动画SPA工作流](assets/workflow.gif)

1. SPA编辑器加载。
1. SPA将加载到单独的框架中。
1. SPA在客户端请求JSON内容并渲染组件。
1. SPA编辑器会检测渲染的组件并生成叠加。
1. 作者单击叠加，以显示组件的编辑工具栏。
1. SPA编辑器在向服务器发出POST请求时保留所做的编辑。
1. SPA编辑器会向SPA编辑器请求更新的JSON，该编辑器将通过DOM事件发送到SPA。
1. SPA会重新渲染相关组件，并更新其DOM。

>[!NOTE]
>
>请记住：
>
>* SPA始终负责其显示。
>* SPA编辑器与SPA本身分离。
>* 在生产（发布）中，永远不会加载SPA编辑器。


### 客户端服务器页面编辑工作流{#client-server-page-editing-workflow}

这是编辑SPA时客户端与服务器交互的更详细概述。

![客户端服务器编辑工作流](assets/client-server-editing.png)

1. SPA会自行初始化，并从Sling模型导出器请求页面模型。
1. Sling模型导出程序从存储库请求构成页面的资源。
1. 存储库会返回资源。
1. Sling模型导出程序会返回页面的模型。
1. SPA会根据页面模型实例化其组件。
1. **6** 内容会通知编辑器已准备好进行创作。

   **6** b页面编辑器请求组件创作配置。

   **6** 页面编辑器接收组件配置。
1. 作者编辑组件时，页面编辑器会向默认POSTServlet发布修改请求。
1. 资源将在存储库中更新。
1. 更新的资源将提供给POSTServlet。
1. 默认POSTServlet会通知页面编辑器资源已更新。
1. 页面编辑器会请求新的页面模型。
1. 从存储库请求构成页面的资源。
1. 组成页面的资源由存储库提供给Sling模型导出器。
1. 更新的页面模型将返回到编辑器。
1. 页面编辑器会更新SPA的页面模型引用。
1. SPA会根据新的页面模型引用更新其组件。
1. 页面编辑器的组件配置已更新。

   **17**  SPA表示页面编辑器内容已准备就绪。

   **17** b页面编辑器为SPA提供组件配置。

   **17**  SPA提供了更新的组件配置。

### 创作工作流{#authoring-workflow}

以创作体验为重点，提供了更详细的概述。

![SPA创作工作流程](assets/authoring-workflow.png)

1. SPA会获取页面模型。
1. **2** 页面模型为编辑器提供了创作所需的数据。

   **2** b当收到通知时，组件orchestrator会更新页面的内容结构。
1. 组件orchestrator查询AEM资源类型与SPA组件之间的映射。
1. 组件orchestrator根据页面模型和组件映射动态实例化SPA组件。
1. 页面编辑器会更新页面模型。
1. **6** 页面模型向页面编辑器提供了更新的创作数据。

   **6** b页面模型将更改调度给component orchestrator。
1. 组件Orchestrator将获取组件映射。
1. 组件Orchestrator会更新页面内容。
1. 当SPA完成页面内容的更新时，页面编辑器会加载创作环境。

## 要求和限制{#requirements-limitations}

要使作者能够使用页面编辑器编辑SPA的内容，必须实施SPA应用程序才能与AEM SPA Editor SDK进行交互。 请至少查看您需要知道才能运行的AEM中使用React](getting-started-react.md)的[SPA快速入门文档。

### 支持的框架{#supported-frameworks}

SPA Editor SDK支持以下最低版本：

* React 16.x及更高版本
* Angular6.x及更高版本

这些框架的早期版本可以与AEM SPA Editor SDK一起使用，但不受支持。

### 其他框架{#additional-frameworks}

可以实施其他SPA框架以与AEM SPA Editor SDK一起使用。 请参阅[SPA Blueprint](blueprint.md)文档，了解框架要创建由模块、组件和服务组成的框架特定层以与AEM SPA Editor配合使用所必须满足的要求。

### 使用多个选择器{#multiple-selectors}

其他自定义选择器可以定义，并用作为为AEM SPA SDK开发的SPA的一部分。 但是，此支持要求`model`选择器是JSON导出程序所需的第一个选择器，扩展是`.json`。

### 文本编辑器要求{#text-editor-requirements}

如果要使用在SPA中创建的文本组件的就地编辑器，则需要其他配置。

1. 在包含文本HTML的容器包装器元素中设置属性（可以是任意属性）。 对于WKND SPA项目，它是`<div>`元素，使用的选择器是`data-rte-editelement`。
1. 在相应AEM文本组件的`cq:InplaceEditingConfig`中设置指向该选择器的配置`editElementQuery`，例如`data-rte-editelement`。 这可让编辑者知道HTML文本的包装是哪个HTML元素。

有关富文本编辑器`editElementQuery`属性和配置的其他信息，请参阅[配置富文本编辑器。](/help/implementing/developing/extending/rich-text-editor.md)

### 限制 {#limitations}

AEM SPA Editor SDK完全受Adobe支持，作为一项新功能，它将继续得到增强和扩展。 SPA编辑器尚不支持以下AEM功能：

* 目标模式
* ContextHub
* 内联图像编辑
* 编辑配置(例如 listeners)
* 样式系统
* 撤消/重做
* 页面差异和时间扭曲
* 执行HTML重写服务器端的功能，如链接检查程序、CDN重写服务、URL缩短等。
* 开发人员模式
* AEM启动项
