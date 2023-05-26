---
title: 利用 Angular 在 AEM 中开始使用 SPA
description: 本文介绍了一个SPA应用程序示例，说明它是如何组合在一起的，并允许您使用Angular框架快速启动和运行自己的SPA。
exl-id: 8013ac2c-d1a7-4940-bb65-15e3ed7652d6
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 12%

---

# 利用 Angular 在 AEM 中开始使用 SPA {#getting-started-with-spas-in-aem-using-angular}

单页应用程序 (SPA) 可以为网站用户提供引人入胜的良好体验。开发人员希望能够使用SPA框架构建站点，而作者希望能够在AEM中无缝编辑使用SPA框架构建的站点的内容。

SPA创作功能提供了一个全面的解决方案，用于在AEM中支持SPA。 本文介绍了在Angular框架上实现的简化SPA应用程序，并说明它是如何进行组合，使您能够快速启动和运行自己的SPA。

>[!NOTE]
>
>本文基于Angular框架。 有关React框架的相应文档，请参阅 [AEM中的SPA快速入门 — React](getting-started-react.md).

## 简介 {#introduction}

本文总结了简单的SPA的基本功能以及运行它所需了解的最少信息。

有关SPA如何在AEM中工作的更多详细信息，请参阅以下文档：

* [SPA 简介和演练](introduction.md)
* [SPA 编辑器概述](editor-overview.md)
* [SPA Blueprint](blueprint.md)

>[!NOTE]
>
>为了能够在SPA中创作内容，内容必须存储在AEM中，并由内容模型公开。
>
>在AEM之外开发的SPA如果不遵守内容模型合同，则无法创作。

本文档将逐步说明简化SPA的结构，并阐述其工作方式，以便您将此理解应用于自己的SPA。

## 依赖关系、配置和构建 {#dependencies-configuration-and-building}

除了预期的Angular依赖项之外，示例SPA还可以利用其他库来提高SPA的创建效率。

### 依赖项 {#dependencies}

此 `package.json` file定义整个SPA包的要求。 此处列出了所需的最低AEM依赖项。

```
"dependencies": {
  "@adobe/aem-angular-editable-components": "~1.0.3",
  "@adobe/aem-spa-component-mapping": "~1.0.5",
  "@adobe/aem-spa-page-model-manager": "~1.0.3"
}
```

此 `aem-clientlib-generator` 用于在构建过程中自动创建客户端库。

`"aem-clientlib-generator": "^1.4.1",`

可以找到有关它的更多详细信息 [在此处GitHub上](https://github.com/wcm-io-frontend/aem-clientlib-generator).

此 `aem-clientlib-generator` 在中配置 `clientlib.config.js` 文件如下所示。

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

实际构建应用程序时所利用的资源 [网络包](https://webpack.js.org/) 用于翻译，以及用于自动创建客户端库的aem-clientlib-generator。 因此， build命令将类似于：

`"build": "ng build --build-optimizer=false && clientlib",`

构建后，可以将包上传到AEM实例。

### AEM 项目原型 {#aem-project-archetype}

任何 AEM 项目都应使用 [AEM 项目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)，它支持使用 React 或 Angular 的 SPA 项目并利用 SPA SDK。

## 应用程序结构 {#application-structure}

如前所述，包括依赖项和构建应用程序将为您留下一个有效的SPA包，您可以将该包上传到您的AEM实例。

本文档的下一部分将引导您了解AEM中SPA的结构方式、驱动应用程序的重要文件以及它们如何协同工作。

使用简化的图像组件作为示例，但应用程序的所有组件都基于相同的概念。

### app.module.ts {#app-module-ts}

进入SPA的入口点是 `app.module.ts` 此处显示的文件进行了简化，以重点关注重要内容。

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

此 `app.module.ts` file是应用程序的起点，包含初始项目配置和使用 `AppComponent` 以引导应用程序。

#### 静态实例化 {#static-instantiation}

使用组件模板静态实例化组件时，必须将值从模型传递到组件的属性。 模型中的值作为属性传递，以便以后作为组件属性使用。

### app.component.ts {#app-component-ts}

一次 `app.module.ts` bootstraps `AppComponent`之后，它可以初始化应用程序，此处以简化版的形式显示，以重点关注重要内容。

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

通过处理页面， `app.component.ts` 调用 `main-content.component.ts` 此处以简化版列出。

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

此 `MainComponent` 摄取页面模型的JSON表示形式，并处理内容以环绕/装饰页面的每个元素。 有关详情，请参阅 `Page` 可以在文档中找到 [SPA Blueprint](blueprint.md).

### image.component.ts {#image-component-ts}

此 `Page` 由组件组成。 引入JSON后， `Page` 可以处理这些组件，例如 `image.component.ts` 如下所示。

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

AEM中SPA的核心思想是：将SPA组件映射到AEM组件，并在修改内容时更新组件（反之亦然）。 查看文档 [SPA编辑器概述](editor-overview.md) 以获取该通信模型的摘要。

`MapTo('my-angular-app/components/image')(Image, ImageEditConfig);`

此 `MapTo` 方法将SPA组件映射到AEM组件。 它支持使用单个字符串或字符串数组。

`ImageEditConfig` 是一个配置对象，它通过为编辑器提供生成占位符所需的元数据来帮助启用组件的创作功能

如果没有内容，则会提供标签作为占位符来表示空内容。

#### 动态传递的属性 {#dynamically-passed-properties}

来自模型的数据将作为组件的属性动态传递。

### image.component.html {#image-component-html}

最后，可以在中渲染图像 `image.component.html`.

```
// image.component.html
<img [src]="src" [alt]="alt" [title]="title"/>
```

## 在SPA组件之间共享信息 {#sharing-information-between-spa-components}

单页应用程序中的组件经常需要共享信息。 有几种推荐的方法可以实现这一点，按复杂性递增的顺序列示如下。

* **选项1：** 例如，通过使用util类作为纯面向对象的解决方案，将逻辑集中并广播到必要的组件。
* **选项2：** 使用状态库（如NgRx）共享组件状态。
* **选项3：** 通过自定义和扩展容器组件来利用对象层次结构。

## 后续步骤 {#next-steps}

* [使用 React 在 AEM 中开始使用 SPA](getting-started-react.md) 说明了如何使用 React 构建基本 SPA 以与 AEM 中的 SPA 编辑器结合使用.
* [SPA 编辑器概述](editor-overview.md)更深入地介绍了 AEM 和 SPA 之间的通信模型。
* [WKND SPA项目](wknd-tutorial.md) 是一个分步教程，用于在AEM中实施简单的SPA项目。
* [SPA的动态模型到组件映射](model-to-component-mapping.md) 说明动态模型到组件的映射以及它在AEM中的SPA中的工作方式。
* [SPA Blueprint](blueprint.md) 深入了解SPA SDK for AEM的工作原理，以防您希望在AEM中为React或Angular以外的框架实施SPA，或者只是希望更深入地了解。
