---
title: AEM中的SPA使用React快速入门
description: 本文提供了一个SPA应用程序示例，介绍了它的组合方式，并允许您使用React框架快速启动并运行自己的SPA。
exl-id: 13998526-65e7-4d1b-bd47-452bad3780a2
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 1%

---

# AEM中的SPA使用React {#getting-started-with-spas-in-aem-using-react}快速入门

单页应用程序 (SPA) 可以为网站用户提供引人入胜的良好体验。开发人员希望能够使用SPA框架构建站点，而作者则希望在AEM中无缝编辑使用SPA框架构建的站点的内容。

SPA创作功能提供了一个全面的解决方案，可在AEM中支持SPA。 本文介绍了React框架上的一个简化SPA应用程序，并说明了它的组合方式，从而使您能够快速启动并运行自己的SPA。

>[!NOTE]
>
>本文基于React框架。 有关Angular框架的相应文档，请参阅[AEM SPA快速入门 — Angular](getting-started-angular.md)。

## 简介 {#introduction}

本文概述了简单SPA的基本功能以及运行运行所需了解的最低值。

有关SPA在AEM中工作方式的更多详细信息，请参阅以下文档：

* [SPA简介和演练](introduction.md)
* [SPA编辑器概述](editor-overview.md)
* [SPA Blueprint](blueprint.md)

>[!NOTE]
>
>为了能够在SPA中创作内容，内容必须存储在AEM中并由内容模型公开。
>
>如果在AEM之外开发的SPA不遵守内容模型合同，则该将不可授权。

本文档将介绍使用React框架创建的简化SPA的结构，并说明其工作方式，以便您能够将此理解应用于您自己的SPA。

## 依赖关系、配置和构建{#dependencies-configuration-and-building}

除了预期的React依赖关系之外，示例SPA还可以利用其他库来更高效地创建SPA。

### 依赖关系 {#dependencies}

`package.json`文件定义了整个SPA包的要求。 此处列出了工作SPA的最低AEM依赖项。

```
  "dependencies": {
    "@adobe/aem-react-editable-components": "~1.0.4",
    "@adobe/aem-spa-component-mapping": "~1.0.5",
    "@adobe/aem-spa-page-model-manager": "~1.0.3"
  }
```

由于此示例基于React框架，因此`package.json`文件中必须存在两个特定于React的依赖项：

```
 react
 react-dom
```

利用`aem-clientlib-generator`可在构建过程中自动创建客户端库。

`"aem-clientlib-generator": "^1.4.1",`

有关该报表包的更多详细信息，请在GitHub上找到[此处](https://github.com/wcm-io-frontend/aem-clientlib-generator)。

`aem-clientlib-generator`在`clientlib.config.js`文件中进行配置，如下所示。

```
module.exports = {
    // default working directory (can be changed per 'cwd' in every asset option)
    context: __dirname,

    // path to the clientlib root folder (output)
    clientLibRoot: "./../content/jcr_root/apps/my-react-app/clientlibs",

    libs: {
        name: "my-react-app",
        allowProxy: true,
        categories: ["my-react-app"],
        embed: ["my-react-app.responsivegrid"],
        jsProcessor: ["min:gcc"],
        serializationFormat: "xml",
        assets: {
            js: [
                "dist/**/*.js"
            ],
            css: [
                "dist/**/*.css"
            ]
        }
    }
};
```

### 正在生成 {#building}

实际构建应用程序时，除了使用aem-clientlib-generator自动创建客户端库外，还会利用[Webpack](https://webpack.js.org/)进行转换。 因此，build命令将类似于：

`"build": "webpack && clientlib --verbose"`

生成后，可将包上传到AEM实例。

### AEM 项目原型 {#aem-project-archetype}

任何AEM项目都应使用[AEM项目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)，它支持使用React或Angular的SPA项目并利用SPA SDK。

## 应用程序结构{#application-structure}

如前所述，包括依赖项和构建应用程序时，您将获得一个可上传到AEM实例的工作SPA包。

本文档的下一部分将介绍AEM中SPA的结构方式、驱动应用程序的重要文件以及它们如何协同工作。

以简化的图像组件为例，但应用程序的所有组件都基于相同的概念。

### index.js {#index-js}

进入SPA的入口点当然是此处显示的`index.js`文件，该文件经过简化，可集中显示重要内容。

```
import ReactDOM from 'react-dom';
import App from './App';
import { ModelManager, Constants } from "@adobe/aem-spa-page-model-manager";

...

ModelManager.initialize().then((pageModel) => {
ReactDOM.render(
    <App cqChildren={pageModel[Constants.CHILDREN_PROP]} cqItems={pageModel[Constants.ITEMS_PROP]} cqItemsOrder={pageModel[Constants.ITEMS_ORDER_PROP]} cqPath={ModelManager.rootPath} locationPathname={ window.location.pathname }/>
, document.getElementById('page'));

});
```

`index.js`的主要功能是利用`ReactDOM.render`函数确定DOM中要插入应用程序的位置。

这是此函数的标准用法，并非此示例应用程序所独有。

#### 静态实例化{#static-instantiation}

使用组件模板（例如JSX）静态实例化组件时，必须将值从模型传递到组件的属性。

### App.js {#app-js}

通过渲染应用程序，`index.js`会调用`App.js`，此处以简化版本显示，以重点关注重要内容。

```
import {Page, withModel } from '@adobe/aem-react-editable-components';

...

class App extends Page {
...
}

export default withModel(App);
```

`App.js` 主要用于封装构成应用程序的根组件。任何应用程序的入口点都是页面。

### Page.js {#page-js}

通过渲染页面，`App.js`会调用此处以简化版本列出的`Page.js`。

```
import {Page, MapTo, withComponentMappingContext } from "@adobe/aem-react-editable-components";

...

class AppPage extends Page {
...
}

MapTo('my-react-app/components/structure/page')(withComponentMappingContext(AppPage));
```

在此示例中，`AppPage`类扩展了`Page`，其中包含随后可以使用的内容方法。

`Page`将摄取页面模型的JSON表示形式，并处理内容以包装/装饰页面的每个元素。 有关`Page`的更多详细信息，请参阅文档[SPA Blueprint。](blueprint.md)

### Image.js {#image-js}

渲染页面后，可以渲染组件，如`Image.js`，如下所示。

```
import React, {Component} from 'react';
import {MapTo} from '@adobe/aem-react-editable-components';

require('./Image.css');

const ImageEditConfig = {

    emptyLabel: 'Image',

    isEmpty: function() {
        return !this.props || !this.props.src || this.props.src.trim().length < 1;
    }
};

class Image extends Component {

    render() {
        return (<img src={this.props.src}>);
    }
}

MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);
```

AEM中SPA的核心思想是将SPA组件映射到AEM组件，并在修改内容时更新组件（反之亦然）。 有关此通信模型的摘要，请参阅文档[SPA Editor概述](editor-overview.md)。

`MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);`

`MapTo`方法可将SPA组件映射到AEM组件。 它支持使用单个字符串或字符串数组。

`ImageEditConfig` 是一个配置对象，通过为编辑器提供生成占位符所需的元数据来有助于启用组件的创作功能

如果没有内容，则将提供标签作为占位符来表示空内容。

#### 动态传递的属性{#dynamically-passed-properties}

来自模型的数据将作为组件的属性动态传递。

## 导出可编辑内容{#exporting-editable-content}

您可以导出组件并使其保持可编辑状态。

```
import React, { Component } from 'react';
import { MapTo } from '@adobe/aem-react-editable-components';

...

const EditConfig = {...}

class PageClass extends Component {...};

...

export default MapTo('my-react-app/react/components/structure/page')(PageClass, EditConfig);
```

`MapTo`函数返回`Component`，该函数是使用类名称和属性扩展提供的`PageClass`以启用创作的组合的结果。 此组件可导出到，以供稍后在应用程序的标记中实例化。

使用`MapTo`或`withModel`函数导出时，`Page`组件会与`ModelProvider`组件封装在一起，该组件提供对页面模型最新版本或页面模型中精确位置的标准组件访问权限。

有关详细信息，请参阅[SPA Blueprint文档](blueprint.md)。

>[!NOTE]
>
>默认情况下，使用`withModel`函数时，会收到组件的整个模型。

## 在SPA组件{#sharing-information-between-spa-components}之间共享信息

单页应用程序中的组件需要定期共享信息。 有几种推荐的方法可以执行此操作，如下所示，它们的复杂性会越来越高。

* **选项1:** 将逻辑集中并广播到必要的组件，例如使用React Context。
* **选项2:** 使用状态库（如Redux）共享组件状态。
* **选项3:** 通过自定义和扩展容器组件来利用对象层次结构。

## 后续步骤{#next-steps}

* [AEM SPA使用入门指](getting-started-angular.md) 南显示了如何构建基本SPA以使用AEM中的SPA编辑器来使用Angular。
* [SPA编辑](editor-overview.md) 器概述对AEM与SPA之间的通信模型有更深入的了解。
* [WKND SPA](wknd-tutorial.md) 项目是在AEM中实施简单SPA项目的分步教程。
* [SPA的动态模型到组件映](model-to-component-mapping.md) 射将动态模型扩展到组件映射，以及它在AEM的SPA中的工作方式。
* [SPA ](blueprint.md) Blueprintotof深入了解SPA SDK for AEM的工作方式，以防您希望在AEM中为除React或Angular之外的其他框架实施SPA，或者只是希望加深对的了解。
