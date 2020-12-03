---
title: SPA Blueprint
description: 本文档描述了任何SPA框架为在AEM内实施可编辑的SPA组件而应履行的与框架无关的一般合同。
translation-type: tm+mt
source-git-commit: d70f531087cccd45793f091b9fab7e8a25143c1e
workflow-type: tm+mt
source-wordcount: '2058'
ht-degree: 0%

---


# SPA Blueprint {#spa-blueprint}

要使作者能够使用AEM SPA编辑器编辑SPA的内容，SPA必须满足以下要求。

## 简介 {#introduction}

本文档描述了任何SPA框架(即AEM支持层)为在AEM中实施可编辑的SPA组件而应履行的一般合同。

要使作者能够使用AEM页面编辑器编辑单页应用程序框架公开的数据，项目必须能够解释表示为AEM存储库内的应用程序存储的数据的语义的模型结构。 为实现这一目标，提供了两个不受框架限制的库：`PageModelManager`和`ComponentMapping`。

>[!NOTE]
>
>以下要求与框架无关。 如果满足这些要求，则可以提供由模块、组件和服务组成的框架特定层。
>
>**AEM中的React和Angular框架已满足这些要求。** 仅当您希望实施另一个框架以与AEM一起使用时，此蓝图中的要求才相关。

>[!CAUTION]
>
>尽管AEM的SPA功能与框架无关，但目前仅支持React和Angular框架。

## PageModelManager {#pagemodelmanager}

`PageModelManager`库作为NPM包提供，供SPA项目使用。 它随SPA提供，并充当数据模型管理器。

它代表SPA抽象了表示实际内容结构的JSON结构的检索和管理。 它还负责与SPA同步，以告知它何时必须重新呈现其组件。

请参阅NPM包[@adobe/aem-spa-model-manager](https://www.npmjs.com/package/@adobe/aem-spa-model-manager)

初始化`PageModelManager`时，库首先加载提供的应用程序根模型（通过参数、元属性或当前URL）。 如果库标识当前页面的模型不是其获取的根模型的一部分，并将其作为子页面的模型包含在其中。

![页面模型整合](assets/page-model-consolidation.png)

### ComponentMapping {#componentmapping}

`ComponentMapping`模块作为NPM包提供到前端项目。 它存储前端组件，并为SPA将前端组件映射到AEM资源类型提供了一种方法。 这样，在解析应用程序的JSON模型时，可动态解析组件。

模型中存在的每个项都包含一个公开AEM资源类型的`:type`字段。 装载后，前端组件可以使用它从基础库接收的模型片段来呈现自己。

#### 动态模型到组件映射{#dynamic-model-to-component-mapping}

有关在AEM的Javascript SPA SDK中如何进行动态模型到组件映射的详细信息，请参阅文章[SPA的动态模型到组件映射](model-to-component-mapping.md)。

### 框架特定层{#framework-specific-layer}

每个前端框架必须实现第三层。 此第三个库负责与底层库交互，并提供一系列集成良好且易于使用的入口点以与数据模型交互。

本文档的其余部分描述了这一中间框架特定层的要求，并希望与框架无关。 通过遵守以下要求，可以为项目组件提供一个特定于框架的层，以与负责管理数据模型的底层库交互。

## 一般概念{#general-concepts}

### 页面型号{#page-model}

页面的内容结构存储在AEM中。 页面模型用于映射和实例化SPA组件。 SPA开发人员创建映射到AEM组件的SPA组件。 为此，他们使用资源类型(或AEM组件的路径)作为唯一键。

SPA组件必须与页面模型同步，并相应地更新其内容。 必须使用利用动态组件的模式来根据提供的页面模型结构动态实例化组件。

### 元字段{#meta-fields}

页面模型利用JSON Model Exporter，它本身基于[Sling Model](https://sling.apache.org/documentation/bundles/models.html) API。 可导出的吊索模型公开以下字段列表，以使底层库能解释数据模型：

* `:type`:AEM资源的类型（默认=资源类型）
* `:children`:当前资源的分层子项。子项不是当前资源的内部内容的一部分（可以在表示页面的项目上找到）
* `:hierarchyType`:资源的分层类型。`PageModelManager`当前支持页面类型

* `:items`:当前资源的子内容资源(嵌套结构，仅存在于容器上)
* `:itemsOrder`:命令列表孩子。JSON地图对象不保证其字段的顺序。 通过使映射和当前阵列同时使用，API的用户具有这两种结构的优点
* `:path`:项目的内容路径（在表示页面的项目上显示）

另请参阅[AEM Content Services快速入门。](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-with-aem-headless/overview.html)

### 框架特定模块{#framework-specific-module}

将关切事项分开有助于促进项目实施。 因此，应提供npm特定的包。 此包负责聚合和公开基本模块、服务和组件。 这些组件必须封装数据模型管理逻辑并提供对项目组件期望的数据的访问。 该模块还负责过渡地暴露底层库的有用入口点。

为了促进库的互操作性，Adobe建议特定框架的模块捆绑以下库。 如果需要，该层可以在将底层API公开到项目之前封装和调整它们。

* [@adobe/aem-spa-model-manager](https://www.npmjs.com/package/@adobe/aem-spa-model-manager)
* [@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

#### 实现{#implementations}

#### 反应{#react}

npm模块：[@adobe/aem-react-editable-components](https://www.npmjs.com/package/@adobe/aem-react-editable-components)

#### 角度{#angular}

npm模块：[@adobe/aem-angular-editable-components](https://www.npmjs.com/package/@adobe/aem-angular-editable-components)

## 主服务和组件{#main-services-and-components}

应按照每个框架的具体准则执行下列实体。 基于框架架构，实现方式可能差异很大，但必须提供描述的功能。

### 模型提供程序{#the-model-provider}

项目组件必须将模型片段的访问权限委派给模型提供者。 然后，模型提供程序负责侦听对模型的指定片段所做的更改并将更新的模型返回给委托组件。

为此，模型提供程序必须注册到[`PageModelManager`](#pagemodelmanager)。 然后，当发生更改时，它接收更新的数据并将其传递到委托组件。 根据惯例，将包含模型片段的委托组件的可用属性命名为`cqModel`。 实现可免费向组件提供此属性，但应考虑到与框架架构的集成、可发现性和易用性等方面。

### 组件HTML修饰符{#the-component-html-decorator}

组件修饰器负责装饰每个组件实例的元素的外部HTML，其中包含页面编辑器所期望的一系列数据属性和类名称。

#### 组件声明{#component-declaration}

以下元数据必须添加到项目组件生成的外部HTML元素。 它们使页面编辑器能够检索相应的编辑配置。

* `data-cq-data-path`:资源相对于  `jcr:content`

#### 编辑功能声明和占位符{#editing-capability-declaration-and-placeholder}

以下元数据和类名称必须添加到项目组件生成的外部HTML元素。 它们使页面编辑器能够优惠相关功能。

* `cq-placeholder`:用于标识空组件占位符的类名称
* `data-emptytext`:组件实例为空时叠加要显示的标签

**空组件占位符**

每个组件都必须扩展一个功能，当组件被标识为空时，该功能将使用特定于占位符和相关叠加的数据属性和类名称装饰外部HTML元素。

**论构件的空虚性**

* 组件在逻辑上是空的吗？
* 当组件为空时，叠加应显示什么标签？

### 容器 {#container}

容器是用于包含和呈现子组件的组件。 为此，容器迭代其模型的`:itemsOrder`、`:items`和`:children`属性。

容器从[`ComponentMapping`](#componentmapping)库的存储中动态获取子组件。 然后，该容器使用模型提供程序功能扩展子组件，并最终将其实例化。

### 页面 {#page}

`Page`组件扩展`Container`组件。 容器是用于包含和呈现子组件（包括子页面）的组件。 为此，容器迭代其模型的`:itemsOrder`、`:items`和`:children`属性。 `Page`组件动态从[`ComponentMapping`](#componentmapping)库的存储中获取子组件。 `Page`负责实例化子组件。

### 响应式网格 {#responsive-grid}

响应式网格组件是容器。 它包含表示其列的模型提供程序的特定变体。 响应式网格及其列负责用模型中包含的特定类名称装饰项目组件的外部HTML元素。

响应式网格组件应预先映射到AEM对应组件，因为此组件复杂且很少进行自定义。

#### 特定模型字段{#specific-model-fields}

* `gridClassNames:` 为响应式网格提供的类名
* `columnClassNames:` 为响应式列提供的类名

另请参阅npm资源[@adobe/aem-react-editable-components](https://www.npmjs.com/package/@adobe/aem-react-editable-components)

#### 响应式网格{#placeholder-of-the-responsive-grid}的占位符

SPA组件将映射到图形容器（如响应式网格），并且在创作内容时必须添加虚拟子占位符。 当页面编辑器创作SPA的内容时，该内容会使用iframe嵌入到编辑器中，并且`data-cq-editor`属性会添加到该内容的文档节点。 当存在`data-cq-editor`属性时，容器必须包含HTMLElement，以表示将新组件插入页面时作者与之交互的区域。

例如：

```html
<div data-cq-data-path={"path/to/the/responsivegrid/*"} className="new section aem-Grid-newComponent"/>
```

>[!NOTE]
>
>示例中使用的类名称当前为页面编辑器所必需的。
>
>* `"new section"`:指示当前元素是容器的占位符
>* `"aem-Grid-newComponent"`:为布局创作规范化组件

>



#### 组件映射{#component-mapping}

基础[`Component Mapping`](#componentmapping)库及其`MapTo`函数可进行封装和扩展，以提供与当前组件类旁边提供的编辑配置相关的功能。

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

在上述实施中，项目组件在实际注册到[组件映射](#componentmapping)存储之前以空虚功能进行扩展。 这是通过封装和扩展[`ComponentMapping`](#componentmapping)库来引入对`EditConfig`配置对象的支持来实现的：

```javascript
/**
 * Configuration object in charge of providing the necessary data expected by the page editor to initiate the authoring. The provided data will be decorating the associated component
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

## 与页面编辑器{#contract-with-the-page-editor}合同

项目组件必须至少生成以下数据属性，以便编辑者能够与它们交互。

* `data-cq-data-path`:组件的相对路径， `PageModel` 如( `"root/responsivegrid/image"`)。不应将此属性添加到页面。

总之，要让页面编辑器将其解释为可编辑，项目组件必须遵守以下合同：

* 提供将前端组件实例关联到AEM资源的预期属性。
* 提供允许创建空占位符的预期一系列属性和类名称。
* 提供支持拖放资产的预期类名称。

### 典型HTML元素结构{#typical-html-element-structure}

以下片段说明了页面内容结构的典型HTML表示形式。 以下是几个重要要点：

* 响应式网格元素具有前缀为`aem-Grid--`的类名
* 响应式列元素具有前缀为`aem-GridColumn--`的类名
* 响应式网格（也是父网格的列）被封装，例如两个以前的前缀不出现在同一元素上
* 与可编辑资源对应的元素具有`data-cq-data-path`属性。 请参阅本文档的[与页面编辑器](#contract-with-the-page-editor)联系。

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

## 导航和路由{#navigation-and-routing}

应用程序拥有路由。 前端开发人员首先需要实现导航组件(映射到AEM导航组件)。 此组件将呈现要与一系列路由结合使用的URL链接，这些路由将显示或隐藏内容片段。

基础[`PageModelManager`](#pagemodelmanager)库及其[`ModelRouter`](routing.md)模块（默认启用）负责预取和提供对与给定资源路径关联的模型的访问。

两个实体与路由概念相关，但[`ModelRouter`](routing.md)仅负责用与当前应用程序状态同步的数据模型加载[`PageModelManager`](#pagemodelmanager)。

有关详细信息，请参阅文章[SPA Model路由](routing.md)。

## SPA实际操作{#spa-in-action}

继续访问以下文档，了解简单的SPA如何工作并亲自与SPA进行试验：

* [AEM中使用React的SPA入门](getting-started-react.md)。
* [AEM中的SPA使用角度入门](getting-started-angular.md)。

## 进一步阅读{#further-reading}

有关AEM中SPA的详细信息，请参阅以下文档:

* [SPA ](editor-overview.md) Editor概述SPA AEM和通信模型概述
