---
title: SPA Blueprint
description: 本文档介绍了任何SPA框架都应该履行的一般且独立于框架的合同，以便您可以在AEM中实施可编辑的SPA组件。
exl-id: 9d47c0e9-600c-4f45-9169-b3c9bbee9152
feature: Developing
role: Admin, Architect, Developer
index: false
source-git-commit: 7a9d947761b0473f5ddac3c4d19dfe5bed5b97fe
workflow-type: tm+mt
source-wordcount: '2022'
ht-degree: 1%

---


# SPA Blueprint {#spa-blueprint}

要使作者能够使用AEM SPA编辑器编辑SPA的内容，SPA必须满足一些要求。

{{ue-over-spa}}

## 简介 {#introduction}

本文档介绍了任何SPA框架都应该履行的一般合同(即AEM支持层的类型)，以便您可以在AEM中实施可编辑的SPA组件。

要使作者能够使用AEM页面编辑器编辑单页应用程序框架公开的数据，项目必须能够解释模型的结构，该结构表示AEM存储库中应用程序所存储数据的语义。 为实现此目标，提供了两个与框架无关的库： `PageModelManager`和`ComponentMapping`。

>[!NOTE]
>
>以下要求与框架无关。 如果满足这些要求，则可以提供由模块、组件和服务组成的框架特定层。
>
>**AEM中的React和Angular框架已满足这些要求。**&#x200B;此Blueprint中的要求仅在您想实施其他框架以用于AEM时才相关。

>[!CAUTION]
>
>尽管AEM的SPA功能与框架无关，但当前仅支持React和Angular框架。

## PageModelManager {#pagemodelmanager}

`PageModelManager`库是作为NPM包提供的，将由SPA项目使用。 它与SPA配合使用，用作数据模型管理器。

它代表SPA抽象出代表实际内容结构的JSON结构的检索和管理。 它还负责与SPA同步，以告知何时必须重新渲染其组件。

查看NPM包[@adobe/aem-spa-model-manager](https://www.npmjs.com/package/@adobe/aem-spa-model-manager)

初始化`PageModelManager`时，库首先加载提供的应用程序根模型（通过参数、元属性或当前URL）。 如果库标识当前页面的模型不是其获取的根模型的一部分，并包含它作为子页面的模型。

![页面模型合并](assets/page-model-consolidation.png)

### 组件映射 {#componentmapping}

`ComponentMapping`模块作为NPM包提供给前端项目。 它存储前端组件，并为SPA提供一种将前端组件映射到AEM资源类型的方法。 这可以在解析应用程序的JSON模型时启用组件的动态分辨率。

模型中存在的每个项目都包含一个`:type`字段，该字段公开了AEM资源类型。 安装后，前端组件可以使用从基础库收到的模型片段来呈现自身。

#### 对组件映射进行动态建模 {#dynamic-model-to-component-mapping}

有关AEM的JavaScript SPA SDK中如何进行动态模型到组件映射的详细信息，请参阅文章[SPA的动态模型到组件映射](model-to-component-mapping.md)。

### 特定于框架的层 {#framework-specific-layer}

必须为每个前端框架实施第三层。 此第三个库负责与底层库交互，并提供一系列集成良好且易于使用的入口点以便与数据模型交互。

本文档的其余部分描述了此中间框架特定层的要求以及独立于框架的愿望。 通过满足以下要求，可以为项目组件提供特定于框架的层，以便与负责管理数据模型的底层库交互。

## 一般概念 {#general-concepts}

### 页面模型 {#page-model}

页面的内容结构存储在AEM中。 页面模型用于映射和实例化SPA组件。 SPA开发人员创建映射到AEM组件的SPA组件。 为此，他们使用资源类型(或AEM组件的路径)作为唯一键值。

SPA组件必须与页面模型同步，并根据对内容所做的任何更改进行更新。 必须使用使用动态元件的阵列来按照提供的页面模型结构即时实例化元件。

### 元字段 {#meta-fields}

页面模型使用JSON模型导出器，它本身基于[Sling模型](https://sling.apache.org/documentation/bundles/models.html) API。 可导出的sling模型显示以下字段列表，以启用基础库解释数据模型：

* `:type`： AEM资源的类型（默认值=资源类型）
* `:children`：当前资源的分层子级。 子项不是当前资源的内部内容的一部分（可以在表示页面的项目上找到）
* `:hierarchyType`：资源的分层类型。 `PageModelManager`当前支持页面类型

* `:items`：当前资源的子内容资源（嵌套结构，仅存在于容器上）
* `:itemsOrder`：已排序的子项列表。 JSON映射对象不保证其字段的顺序。 通过同时具有映射和当前数组，API的使用者可以同时拥有这两种结构的好处
* `:path`：项目的内容路径（位于表示页面的项目上）

另请参阅[AEM Content Services快速入门](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html)。

### 特定于Framework的模块 {#framework-specific-module}

区分关注点有助于促进项目实施。 因此，应提供特定于npm的包。 此资源包负责聚合和公开基本模块、服务和组件。 这些组件必须封装数据模型管理逻辑，并提供对项目组件所预期数据的访问。 模块还负责过渡性地公开基础库的有用入口点。

为了促进这些库的互操作性，Adobe建议框架特定的模块捆绑以下库。 如有必要，该层可以先封装并调整底层API，然后再将其公开给项目。

* [@adobe/aem-spa-model-manager](https://www.npmjs.com/package/@adobe/aem-spa-model-manager)
* [@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

#### 实施 {#implementations}

#### React {#react}

npm模块： [@adobe/aem-react-editable-components](https://www.npmjs.com/package/@adobe/aem-react-editable-components)

#### Angular {#angular}

npm模块： [@adobe/aem-angular-editable-components](https://www.npmjs.com/package/@adobe/aem-angular-editable-components)

## 主要服务和组件 {#main-services-and-components}

应根据每个框架的具体准则实施以下实体。 基于框架体系结构，实现方式可能相差很大，但必须提供所描述的功能。

### 模型提供程序 {#the-model-provider}

项目组件必须将模型片段的访问权限委派给模型提供程序。 然后，模型提供程序负责侦听对模型的指定片段所做的更改，并将更新的模型返回到委托组件。

为此，模型提供程序必须向[`PageModelManager`](#pagemodelmanager)注册。 然后，当发生更改时，它会接收更新后的数据并将其传递给委托组件。 按照惯例，可用于将承载模型片段的委托组件的属性名为`cqModel`。 实施可以自由地为组件提供此属性，但应考虑与框架架构集成、可发现性和易用性等方面。

### 组件HTML Decorator {#the-component-html-decorator}

组件修饰器负责使用页面编辑器所需的一系列数据属性和类名称来修饰每个组件实例元素的外部HTML。

#### 组件声明 {#component-declaration}

必须将以下元数据添加到项目组件生成的外部HTML元素中。 它们允许页面编辑器检索相应的编辑配置。

* `data-cq-data-path`：相对于`jcr:content`的资源路径

#### 编辑功能声明和占位符 {#editing-capability-declaration-and-placeholder}

必须将以下元数据和类名称添加到项目组件生成的外部HTML元素中。 它们允许页面编辑器提供相关功能。

* `cq-placeholder`：标识空组件的占位符的类名称
* `data-emptytext`：组件实例为空时要由叠加显示的标签

空组件的&#x200B;**占位符**

每个组件都必须进行扩展，以便能够使用特定于占位符的数据属性和类名以及相关的叠加图（当组件标识为空时）来修饰外部HTML元素。

**关于组件的空白**

* 该组件在逻辑上是否为空？
* 组件为空时，叠加图应显示什么标签？

### 容器 {#container}

容器是指用于包含和呈现子组件的组件。 为此，容器迭代其模型的`:itemsOrder`、`:items`和`:children`属性。

容器从[`ComponentMapping`](#componentmapping)库的存储中动态获取子组件。 然后，容器使用模型提供程序功能扩展子组件，最后实例化它。

### 页面 {#page}

`Page`组件扩展`Container`组件。 容器是一个组件，旨在包含和渲染子组件，包括子页面。 为此，容器迭代了其模型的`:itemsOrder`、`:items`和`:children`属性。 `Page`组件从[`ComponentMapping`](#componentmapping)库的存储中动态获取子组件。 `Page`负责实例化子组件。

### 响应式网格 {#responsive-grid}

响应式网格组件是一个容器。 它包含模型提供程序的特定变体，该变体表示其列。 响应式网格及其列负责使用模型中包含的特定类名装饰项目组件的外部HTML元素。

响应式网格组件应该预先映射到其AEM对应组件，因为此组件比较复杂，很少进行自定义。

#### 特定模型字段 {#specific-model-fields}

* `gridClassNames:`为响应式网格提供了类名
* `columnClassNames:`为响应列提供了类名

另请参阅npm资源[@adobe/aem-react-editable-components](https://www.npmjs.com/package/@adobe/aem-react-editable-components)

#### 响应式网格的占位符 {#placeholder-of-the-responsive-grid}

SPA组件将映射到图形容器，例如响应式网格，并且在创作内容时必须添加虚拟子占位符。 当页面编辑器创作SPA的内容时，该内容会使用iframe嵌入到编辑器中，并且`data-cq-editor`属性会添加到该内容的文档节点中。 当存在`data-cq-editor`属性时，容器必须包含一个HTMLElement以表示在将新组件插入页面时作者与之交互的区域。

例如：

```html
<div data-cq-data-path={"path/to/the/responsivegrid/*"} className="new section aem-Grid-newComponent"/>
```

>[!NOTE]
>
>该示例中使用的类名当前是页面编辑器所必需的。
>
>* `"new section"`：指示当前元素是容器的占位符
>* `"aem-Grid-newComponent"`：为布局创作标准化组件
>

#### 组件映射 {#component-mapping}

基础的[`Component Mapping`](#componentmapping)库及其`MapTo`函数可以封装和扩展，以提供与当前组件类一起提供的编辑配置相关的功能。

```javascript
const EditConfig = {

    emptyLabel: 'My Component',

    isEmpty: function() {
        return !this.props || !this.props.cqModel || this.props.cqModel.isEmpty;
    }
};

class MyComponent extends Component {

    render() {
        return <div className={'my-component'}></div>;
    }
}

MapTo('component/resource/path')(MyComponent, EditConfig);
```

在上述实现中，在[组件映射](#componentmapping)存储中实际注册项目之前，使用空功能扩展了项目组件。 这是通过封装和扩展[`ComponentMapping`](#componentmapping)库来完成，以引入`EditConfig`配置对象的支持：

```javascript
/**
 * Configuration object in charge of providing the necessary data expected by the page editor to initiate the authoring. The provided data is decorating the associated component
 *
 * @typedef {{}} EditConfig
 * @property {String} [dragDropName]       If defined, adds a specific class name enabling the drag and drop functionality
 * @property {String} emptyLabel           Label to be displayed by the placeholder when the component is empty. Optionally returns an empty text value
 * @property {function} isEmpty            Should the component be considered empty. The function is called using the context of the wrapper component giving you access to the component model
 */

/**
 * Map a React component with the given resource types. If an {@link EditConfig} is provided the <i>clazz</i> is wrapped to provide edition capabilities on the AEM Page Editor
 *
 * @param {string[]} resourceTypes                      - List of resource types for which to use the given <i>clazz</i>
 * @param {class} clazz                                 - Class to be instantiated for the given resource types
 * @param {EditConfig} [editConfig]                     - Configuration object for enabling the edition capabilities
 * @returns {class}                                     - The resulting decorated Class
 */
ComponentMapping.map = function map (resourceTypes, clazz, editConfig) {};
```

## 与页面编辑器签订合同 {#contract-with-the-page-editor}

项目组件必须至少生成以下数据属性，才能让编辑器与它们交互。

* `data-cq-data-path`： `PageModel`提供的组件的相对路径（例如，`"root/responsivegrid/image"`）。 不应将此属性添加到页面。

总之，要由页面编辑器解释为可编辑，项目组件必须遵循以下合同：

* 提供将前端组件实例关联到AEM资源的预期属性。
* 提供允许创建空占位符的预期属性和类名系列。
* 提供用于启用拖放资源的预期类名。

### 典型HTML元素结构 {#typical-html-element-structure}

以下片段说明了页面内容结构的典型HTML表示形式。 以下是一些要点：

* 响应式网格元素带有以`aem-Grid--`为前缀的类名称
* 响应列元素具有以`aem-GridColumn--`为前缀的类名
* 响应式网格（也是父网格的列）被包住，例如前两个前缀未出现在同一元素上
* 与可编辑资源对应的元素带有`data-cq-data-path`属性。 请参阅本文档的[与页面编辑器的合同](#contract-with-the-page-editor)部分。

```javascript
<div data-cq-data-path="/content/page">
    <div class="aem-Grid aem-Grid--12 aem-Grid--default--12">
        <div class="aem-container aem-GridColumn aem-GridColumn--default--12" data-cq-data-path="/content/page/jcr:content/root/responsivegrid">
            <div class="aem-Grid aem-Grid--12 aem-Grid--default--12">
                <div class="cmp-image cq-dd-image aem-GridColumn aem-GridColumn--default--12" data-cq-data-path="/root/responsivegrid/image">
                    <img src="/content/we-retail-spa-sample/react/jcr%3acontent/root/responsivegrid/image.img.jpeg/1512113734019.jpeg">
                </div>
            </div>
        </div>
    </div>
</div>
```

## 导航和路由 {#navigation-and-routing}

应用程序拥有路由。 前端开发人员必须首先实施导航组件(映射到AEM导航组件)。 此组件将渲染要与一系列显示或隐藏内容片段的路由一起使用的URL链接。

基础[`PageModelManager`](#pagemodelmanager)库及其[`ModelRouter`](routing.md)模块（默认启用）负责预获取并提供对与给定资源路径关联的模型的访问权限。

这两个实体与路由的概念有关，但[`ModelRouter`](routing.md)只负责使用与当前应用程序状态同步的结构化数据模型加载[`PageModelManager`](#pagemodelmanager)。

有关详细信息，请参阅文章[SPA模型路由](routing.md)。

## SPA的实际操作 {#spa-in-action}

请继续参阅以下文档，了解简单的SPA如何工作并自行体验SPA：

* [在AEM中使用React快速入门SPA](getting-started-react.md)。
* [使用Angular在AEM中开始使用SPA](getting-started-angular.md)。

## 深入阅读 {#further-reading}

有关AEM中SPA的更多信息，请参阅以下文档：

* 有关AEM中的SPA和通信模型的[SPA编辑器概述](editor-overview.md)
