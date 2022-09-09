---
title: AEM SPA使用Angular入门
description: 本文提供了一个SPA应用程序示例，介绍了它的组合方式，并允许您使用Angular框架快速启动并运行自己的SPA。
exl-id: 8013ac2c-d1a7-4940-bb65-15e3ed7652d6
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 4%

---

# AEM SPA使用Angular入门 {#getting-started-with-spas-in-aem-using-angular}

单页应用程序 (SPA) 可以为网站用户提供引人入胜的良好体验。开发人员希望能够使用SPA框架构建站点，而作者则希望在AEM中无缝编辑使用SPA框架构建的站点的内容。

SPA创作功能提供了一个全面的解决方案，可在AEM中支持SPA。 本文介绍了Angular框架上的一个简化的SPA应用程序，并说明了它的组合方式，使您能够快速启动并运行自己的SPA。

>[!NOTE]
>
>本文基于Angular框架。 有关React框架的相应文档，请参阅 [AEM - React中的SPA快速入门](getting-started-react.md).

## 简介 {#introduction}

本文概述了简单SPA的基本功能以及运行运行所需了解的最低值。

有关SPA在AEM中工作方式的更多详细信息，请参阅以下文档：

* [SPA 简介和演练](introduction.md)
* [SPA 编辑器概述](editor-overview.md)
* [SPA Blueprint](blueprint.md)

>[!NOTE]
>
>为了能够在SPA中创作内容，内容必须存储在AEM中并由内容模型公开。
>
>如果在AEM之外开发的SPA不遵守内容模型合同，则该将不可授权。

本文档将介绍简化的SPA的结构并说明其工作方式，以便您能够将此理解应用于您自己的SPA。

## 依赖关系、配置和构建 {#dependencies-configuration-and-building}

除了预期的Angular依赖关系之外，示例SPA还可以利用其他库来更高效地创建SPA。

### 依赖项 {#dependencies}

的 `package.json` 文件定义了整个SPA包的要求。 此处列出了所需的最低AEM依赖项。

```
"dependencies": {
  "@adobe/aem-angular-editable-components": "~1.0.3",
  "@adobe/aem-spa-component-mapping": "~1.0.5",
  "@adobe/aem-spa-page-model-manager": "~1.0.3"
}
```

的 `aem-clientlib-generator` 可让客户端库的创建在生成过程中自动进行。

`"aem-clientlib-generator": "^1.4.1",`

有关该报表的更多详细信息，请参阅 [在GitHub上，单击此处](https://github.com/wcm-io-frontend/aem-clientlib-generator).

的 `aem-clientlib-generator` 在 `clientlib.config.js` 文件，如下所示。

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

实际构建应用程序需要利用 [Webpack](https://webpack.js.org/) ，以便除用于自动创建客户端库的aem-clientlib-generator之外进行转换。 因此，build命令将类似于：

`"build": "ng build --build-optimizer=false && clientlib",`

生成后，可将包上传到AEM实例。

### AEM 项目原型 {#aem-project-archetype}

任何AEM项目都应利用 [AEM项目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)，它支持使用React或Angular的SPA项目并利用SPA SDK。

## 应用程序结构 {#application-structure}

如前所述，包括依赖项和构建应用程序时，您将获得一个可上传到AEM实例的工作SPA包。

本文档的下一部分将介绍AEM中SPA的结构方式、驱动应用程序的重要文件以及它们如何协同工作。

以简化的图像组件为例，但应用程序的所有组件都基于相同的概念。

### app.module.ts {#app-module-ts}

进入SPA的入口点是 `app.module.ts` 此处显示的文件经过简化，可重点关注重要内容。

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

的 `app.module.ts` 文件是应用程序的起点，包含初始项目配置和使用 `AppComponent` 引导应用程序。

#### 静态实例化 {#static-instantiation}

使用组件模板静态实例化组件时，必须将值从模型传递到组件的属性。 模型中的值将作为属性传递，以便稍后作为组件属性提供。

### app.component.ts {#app-component-ts}

一次 `app.module.ts` 引导 `AppComponent`，则可以初始化应用程序，该应用程序将以简化版本显示在此处，以重点关注重要内容。

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

通过处理页面， `app.component.ts` 调用 `main-content.component.ts` 以简化版本列于此处。

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

的 `MainComponent` 摄取页面模型的JSON表示形式并处理内容以包装/装饰页面的每个元素。 有关 `Page` 可以在文档中找到 [SPA Blueprint](blueprint.md).

### image.component.ts {#image-component-ts}

的 `Page` 由组件组成。 摄取JSON后， `Page` 可以处理这些组件，例如 `image.component.ts` 如此处所示。

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

AEM中SPA的核心思想是将SPA组件映射到AEM组件，并在修改内容时更新组件（反之亦然）。 查看文档 [SPA编辑器概述](editor-overview.md) 以了解此通信模型的摘要。

`MapTo('my-angular-app/components/image')(Image, ImageEditConfig);`

的 `MapTo` 方法将SPA组件映射到AEM组件。 它支持使用单个字符串或字符串数组。

`ImageEditConfig` 是一个配置对象，通过为编辑器提供生成占位符所需的元数据来有助于启用组件的创作功能

如果没有内容，则将提供标签作为占位符来表示空内容。

#### 动态传递的属性 {#dynamically-passed-properties}

来自模型的数据将作为组件的属性动态传递。

### image.component.html {#image-component-html}

最后，图像可在 `image.component.html`.

```
// image.component.html
<img [src]="src" [alt]="alt" [title]="title"/>
```

## 在SPA组件之间共享信息 {#sharing-information-between-spa-components}

单页应用程序中的组件需要定期共享信息。 有几种推荐的方法可以执行此操作，如下所示，它们的复杂性会越来越高。

* **选项1:** 将逻辑和广播集中到必要的组件，例如，将util类用作纯面向对象的解决方案。
* **选项2:** 使用状态库（如NgRx）共享组件状态。
* **选项3:** 通过自定义和扩展容器组件来利用对象层次结构。

## 后续步骤 {#next-steps}

* [AEM SPA使用React快速入门](getting-started-react.md) 显示如何构建基本的SPA，以便使用React在AEM中与SPA编辑器一起使用。
* [SPA编辑器概述](editor-overview.md) 更深入地介绍了AEM与SPA之间的通信模型。
* [WKND SPA项目](wknd-tutorial.md) 是在AEM中实施简单SPA项目的分步教程。
* [适用于SPA的动态模型到组件映射](model-to-component-mapping.md) 介绍动态模型到组件的映射，以及它如何在AEM的SPA中工作。
* [SPA Blueprint](blueprint.md) 深入了解SPA SDK for AEM的工作方式，以防您希望在AEM中为除React或Angular以外的框架实施SPA，或者只是希望加深了解。
