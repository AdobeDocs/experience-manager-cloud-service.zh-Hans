---
title: SPA AEM使用角度式入门
description: 本文展示了一个SPA应用程序示例，介绍了它是如何组合在一起的，并允许您使用角度框架快速与自己的SPA联动手运行。
translation-type: tm+mt
source-git-commit: 8bdb7bbe80a4e22bb2b750c0719c6db745133392
workflow-type: tm+mt
source-wordcount: '995'
ht-degree: 1%

---


# SPA AEM使用角度式入门 {#getting-started-with-spas-in-aem-using-angular}

单页应用程序(SPA)可以为网站用户优惠引人入胜的体验。 开发人员希望能够使用SPA框架构建站点，而作者希望无缝编辑AEM中的内容，使用SPA框架构建站点。

SPA创作功能优惠了在AEM内支持SPA的一个全面的解决方案。 本文介绍了Angular框架上简化的SPA应用程序，并解释了它是如何组合在一起的，使您能快速与自己的SPA一起运行。

>[!NOTE]
>
>本文基于角框架。 有关React框架的相应文档，请参 [阅AEM中的SPA入门](getting-started-react.md)。

## 简介 {#introduction}

本文概括了简单的SPA的基本功能以及运行所需的最低要求。

有关SPA在AEM中的工作方式的详细信息，请参阅以下文档:

* [SPA简介和演练](introduction.md)
* [SPA编辑器概述](editor-overview.md)
* [SPA Blueprint](blueprint.md)

>[!NOTE]
>
>要在SPA中创作内容，内容必须存储在AEM中并由内容模型公开。
>
>如果SPA不遵守内容模型合同，则在AEM之外开发的将不可授权。

本文档将介绍简化的SPA的结构并说明其工作方式，以便您能够将这一理解应用于您自己的SPA。

## 依赖关系、配置和构建 {#dependencies-configuration-and-building}

除了期望的角度依赖关系外，示例SPA还可以利用其他库来提高SPA创建的效率。

### 依赖关系 {#dependencies}

文 `package.json` 件定义整个SPA包的要求。 此处列出所需的最低AEM依赖项。

```
"dependencies": {
  "@adobe/aem-angular-editable-components": "~1.0.3",
  "@adobe/aem-spa-component-mapping": "~1.0.5",
  "@adobe/aem-spa-page-model-manager": "~1.0.3"
}
```

利用 `aem-clientlib-generator` 该工具，可以在构建过程中自动创建客户端库。

`"aem-clientlib-generator": "^1.4.1",`

有关该功能的更多详细信 [息，请访问](https://github.com/wcm-io-frontend/aem-clientlib-generator)。

在文 `aem-clientlib-generator` 件中进行 `clientlib.config.js` 如下配置。

```
module.exports = {
    // default working directory (can be changed per 'cwd' in every asset option)
    context: __dirname,

    // path to the clientlib root folder (output)
    clientLibRoot: "./../content/jcr_root/apps/my-angular-app/clientlibs",

    libs: {
        name: "my-angular-app",
        allowProxy: true,
        categories: ["my-angular-app"],
        embed: ["my-angular-app.responsivegrid"],
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

实际构建应用程序 [除了aem](https://webpack.js.org/) -clientlib-generator用于自动创建客户端库外，还利用Webpack进行转换。 因此，build命令将类似于：

`"build": "ng build --build-optimizer=false && clientlib",`

构建后，包可以上传到AEM实例。

### AEM 项目原型 {#aem-project-archetype}

任何AEM项目都应利用AEM [项目原型](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/developing/archetype/overview.html)，它支持SPA项目（使用React或Angular）并利用SPA SDK。

## 应用程序结构 {#application-structure}

如前所述，包括依赖项和构建应用程序将留给您一个可上传到AEM实例的SPA工作包。

本文档的下一节将介绍AEM的构建方式、驱动应用程序的重要文件以及它们如何协同工作。

以简化的图像组件为例，但应用程序的所有组件都基于相同的概念。

### app.module.ts {#app-module-ts}

进入SPA的入口点是此处显示的 `app.module.ts` 文件，它经过简化以集中处理重要内容。

```
// app.module.ts
import { BrowserModule, BrowserTransferStateModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { AppComponent } from './app.component';
import { SpaAngularEditableComponentsModule } from '@adobe/aem-angular-editable-components';
import { AppRoutingModule } from './app-routing.module';

@NgModule({
  imports: [ BrowserModule.withServerTransition({ appId: 'my-angular-app' }),
    SpaAngularEditableComponentsModule,
    AppRoutingModule,
    BrowserTransferStateModule ],
  providers: ...,
  declarations: [ ... ],
  entryComponents: [ ... ],
  bootstrap: [ AppComponent ]
})
export class AppModule {}
```

文 `app.module.ts` 件是应用程序的起点，包含初始项目配置，并用于引导 `AppComponent` 应用程序。

#### 静态实例化 {#static-instantiation}

当使用组件模板静态实例化组件时，必须将值从模型传递到组件的属性。 模型中的值作为属性传递，以后可作为组件属性使用。

### app.component.ts {#app-component-ts}

引导 `app.module.ts` 完 `AppComponent`成后，它便可以初始化应用程序，该应用程序以简化版本显示，以专注于重要内容。

```
// app.component.ts
import { Component } from '@angular/core';
import { ModelManager } from '@adobe/aem-spa-page-model-manager';
import { Constants } from "@adobe/aem-angular-editable-components";

@Component({
  selector: 'app-root',
  template: `
    <router-outlet></router-outlet>
  `
})

export class AppComponent {
  items;
  itemsOrder;
  path;

  constructor() {
    ModelManager.initialize().then(this.updateData.bind(this));
  }

  private updateData(model) {
    this.path = model[Constants.PATH_PROP];
    this.items = model[Constants.ITEMS_PROP];
    this.itemsOrder = model[Constants.ITEMS_ORDER_PROP];
  }
}
```

### main-content.component.ts {#main-content-component-ts}

通过处理页面， `app.component.ts` 以简 `main-content.component.ts` 化版本列出的调用。

```
import { Component } from '@angular/core';
import { ModelManagerService }     from '../model-manager.service';
import { ActivatedRoute } from '@angular/router';
import { Constants } from "@adobe/aem-angular-editable-components";

@Component({
  selector: 'app-main',
  template: `
    <aem-page class="structure-page" [attr.data-cq-page-path]="path" [cqPath]="path" [cqItems]="items" [cqItemsOrder]="itemsOrder" ></aem-page>
  `
})

export class MainContentComponent {
  items;
  itemsOrder;
  path;

  constructor( private route: ActivatedRoute,
    private modelManagerService: ModelManagerService) {
    this.modelManagerService.getData({ path: this.route.snapshot.data.path }).then((data) => {
      this.path = data[Constants.PATH_PROP];
      this.items = data[Constants.ITEMS_PROP];
      this.itemsOrder = data[Constants.ITEMS_ORDER_PROP];
    });
  }
}
```

收 `MainComponent` 集页面模型的JSON表示形式并处理内容以包装／装饰页面的每个元素。 有关该产品的更 `Page` 多详细信息，请参 [阅文档SPA Blueprint](blueprint.md)。

### image.component.ts {#image-component-ts}

它 `Page` 由组件组成。 摄取JSON后，可 `Page` 以处理这些组件， `image.component.ts` 如下所示。

```
/// image.component.ts
import { Component, Input } from '@angular/core';

const ImageEditConfig = {

    emptyLabel: 'Image',

    isEmpty: function(cqModel) {
        return !cqModel || !cqModel.src || cqModel.src.trim().length < 1;
    }
};

@Component({
  selector: 'app-image',
  templateUrl: './image.component.html',
})

export class ImageComponent {
  @Input() src: string;
  @Input() alt: string;
  @Input() title: string;
}

MapTo('my-angular-app/components/image')(ImageComponent, ImageEditConfig);
```

SPA AEM的核心思想是将SPA组件映射到AEM组件，并在内容被修改时更新组件（反之亦然）。 有关此通信 [模型的摘要](editor-overview.md) ，请参阅文档SPA编辑器概述。

`MapTo('my-angular-app/components/image')(Image, ImageEditConfig);`

该方 `MapTo` 法将SPA组件映射到AEM组件。 它支持使用单个字符串或字符串数组。

`ImageEditConfig` 是一个配置对象，它通过为编辑器提供生成占位符所需的元数据来帮助启用组件的创作功能

如果没有内容，则标签将作为占位符提供以表示空内容。

#### 动态传递的属性 {#dynamically-passed-properties}

来自模型的数据将作为组件的属性动态传递。

### image.component.html {#image-component-html}

最后，可在中渲染图像 `image.component.html`。

```
// image.component.html
<img [src]="src" [alt]="alt" [title]="title"/>
```

## 在SPA组件之间共享信息 {#sharing-information-between-spa-components}

单页应用程序中的组件需要定期共享信息。 有几种推荐的方法可以这样做，其复杂程度按顺序增加如下所示。

* **选项1:** 将逻辑集中化并广播到必要的组件，例如，将util类用作纯面向对象的解决方案。
* **选项2:** 使用状态库（如NgRx）共享组件状态。
* **选项3:** 通过自定义和扩展容器组件来利用对象层次结构。

## 后续步骤 {#next-steps}

* [SPA AEM使用React入门说明如何构建基本的SPA](getting-started-react.md) ，以便使用React在AEM中与SPA Editor一起使用。
* [SPA Editor概述](editor-overview.md) 深入介绍AEM与SPA之间的通信模型。
* [WKND SPA Project](wknd-tutorial.md) （WKND项目）是一个分步教程，它在AEM中实施一个简单的SPA项目。
* [SPA的动态模型到组件映射](model-to-component-mapping.md) (Dynamic Model to Component Mapping)解释了动态模型到组件映射，以及它在SPA中如何工作。
* [SPA](blueprint.md) Blueprint优惠深入了解SPA SDK for AEM如何工作，以防您希望在中实施除React或Angular之外的框架，或只是希望深入了解。
