---
title: 在 AEM 中编辑外部 SPA
description: 本文档介绍了将独立SPA上传到AEM实例、添加可编辑的内容部分和启用创作的建议步骤。
exl-id: 7978208d-4a6e-4b3a-9f51-56d159ead385
source-git-commit: 7260649eaab303ba5bab55ccbe02395dc8159949
workflow-type: tm+mt
source-wordcount: '2420'
ht-degree: 2%

---

# 在 AEM 中编辑外部 SPA {#editing-external-spa-within-aem}

在做出决定时 [什么级别的集成](/help/implementing/developing/headful-headless.md) 您希望在外部SPA和AEM之间切换，请考虑您必须经常能够在AEM中编辑和查看SPA。

## 概述 {#overview}

本文档介绍了将独立SPA上传到AEM实例、添加可编辑的内容部分和启用创作的建议步骤。

## 前提条件 {#prerequisites}

先决条件很简单。

* 确保AEM的实例正在本地运行。
* 使用以下方式创建基本AEM SPA项目 [AEM项目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?#available-properties).
   * Forms是AEM项目的基础，该项目已更新以包括外部SPA。
   * 对于本文档中的示例，Adobe是使用 [WKND SPA项目](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html#spa-editor).
* 准备好您想要集成的工作中的外部React SPA。

## 将SPA上传到AEM项目 {#upload-spa-to-aem-project}

首先，必须将外部SPA上传到AEM项目。

1. Replace `src` 在 `/ui.frontend` 使用React应用程序的 `src` 文件夹。
1. 在应用程序的 `package.json` 在 `/ui.frontend/package.json` 文件。
   * 确保SPA SDK依赖项为 [推荐版本](/help/implementing/developing/hybrid/getting-started-react.md#dependencies).
1. 将任何自定义项包含在 `/public` 文件夹。
1. 包括任何添加到的内联脚本或样式 `/public/index.html` 文件。

## 配置远程SPA {#configure-remote-spa}

现在，外部SPA已成为AEM项目的一部分，因此必须在AEM中对其进行配置。

### 包含AdobeSPA SDK包 {#include-spa-sdk-packages}

要利用AEM SPA功能，需要依赖以下三个软件包。

* [`@adobe/aem-react-editable-components`](https://github.com/adobe/aem-react-editable-components)
* [`@adobe/aem-spa-component-mapping`](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)
* [`@adobe/aem-spa-page-model-manager`](https://www.npmjs.com/login?next=/package/@adobe/aem-spa-model-manager)

此 `@adobe/aem-spa-page-model-manager` 包提供了用于初始化模型管理器和从AEM实例检索模型的API。 然后，此模型可用于使用来自的API渲染AEM组件 `@adobe/aem-react-editable-components` 和 `@adobe/aem-spa-component-mapping`.

#### 安装 {#installation}

运行以下命令 `npm` 命令，以便您可以安装所需的软件包。

```shell
npm install --save @adobe/aem-spa-component-mapping @adobe/aem-spa-page-model-manager @adobe/aem-react-editable-components
```

### ModelManager初始化 {#model-manager-initialization}

在应用程序渲染之前， [`ModelManager`](/help/implementing/developing/hybrid/blueprint.md#pagemodelmanager) 必须初始化才能处理AEM的创建 `ModelStore`.

此初始化必须在 `src/index.js` 应用程序的文件，或在呈现应用程序根目录的位置。

要执行此初始化，您可以使用 `initializationAsync` API由提供 `ModelManager`.

以下屏幕截图显示了如何启用 `ModelManager` 在简单的React应用程序中。 唯一的限制是 `initializationAsync` 必须在之前调用 `ReactDOM.render()`.

![初始化ModelManager](assets/external-spa-initialize-modelmanager.png)

在此示例中， `ModelManager` 已初始化并且为空 `ModelStore` 创建。

此 `initializationAsync` 可以选择接受 `options` 对象作为参数：

* `path`  — 初始化时，将获取定义路径处的模型并将其存储在 `ModelStore`. 此路径可用于获取 `rootModel` 初始化时（如果需要）。
* `modelClient`  — 允许提供负责提取模型的自定义客户端。
* `model` - A `model` 作为参数传递的对象通常填充于 [使用SSR](/help/implementing/developing/hybrid/ssr.md).

### AEM可创作叶组件 {#authorable-leaf-components}

1. 创建/标识为其创建了可授权的React组件的AEM组件。 在此示例中，它使用WKND项目的文本组件。

   ![WKND文本组件](assets/external-spa-text-component.png)

1. 在SPA中创建简单的React文本组件。 在本例中，是一个新文件 `Text.js` 已创建，内容如下。

   ![Text.js](assets/external-spa-textjs.png)

1. 创建一个配置对象，以便您可以指定启用AEM编辑所需的属性。

   ![创建配置对象](assets/external-spa-config-object.png)

   * `resourceType` 是将React组件映射到AEM组件并在AEM编辑器中打开时启用编辑功能的必需组件。

1. 使用包装函数 `withMappable`.

   ![使用withMappable](assets/external-spa-withmappable.png)

   此包装函数将React组件映射到AEM `resourceType` 在配置中指定，并在AEM编辑器中打开时启用编辑功能。 对于独立组件，它还会获取特定节点的模型内容。

   >[!NOTE]
   >
   >在此示例中，该组件有单独的版本：AEM封装和未封装的React组件。 显式使用组件时，必须使用包装的版本。 当组件是页面的一部分时，您可以继续使用默认组件，就像当前在SPA编辑器中完成的那样。

1. 呈现组件中的内容。

   文本组件的JCR属性在AEM中如下所示。

   ![文本组件属性](assets/external-spa-text-properties.png)

   这些值作为属性传递到新创建的 `AEMText` React组件，并可用于呈现内容。

   ```javascript
   import React from 'react';
   import { withMappable } from '@adobe/aem-react-editable-components';
   
   export const TextEditConfig = {
       // Empty component placeholder label
       emptyLabel:'Text', 
       isEmpty:function(props) {
          return !props || !props.text || props.text.trim().length < 1;
       },
       // resourcetype of the AEM counterpart component
       resourceType:'wknd-spa-react/components/text'
   };
   
   const Text = ({ text }) => (<div>{text}</div>);
   
   export default Text;
   
   export const AEMText = withMappable(Text, TextEditConfig);
   ```

   以下是完成AEM配置后组件的显示方式。

   ```javascript
   const Text = ({ cqPath, richText, text }) => {
      const richTextContent = () => (
         <div className="aem_text" id={cqPath.substr(cqPath.lastIndexOf('/') + 1)} data-rte-editelement dangerouslySetInnerHTML={{__html: text}}/>
      );
      return richText ? richTextContent() : (<div className="aem_text">{text}</div>);
   };
   ```

   >[!NOTE]
   >
   >在此示例中，对渲染的组件进行了进一步的自定义以匹配现有的文本组件。 它与AEM中的创作无关。

#### 将可创作组件添加到页面 {#add-authorable-component-to-page}

创建可创作的React组件后，您可以在整个应用程序中使用它们。

让我们举一个示例页面，您必须在其中添加来自WKND SPA项目的文本。 对于此示例，您希望显示文本“Hello World！” 开启 `/content/wknd-spa-react/us/en/home.html`.

1. 确定要显示的节点的路径。

   * `pagePath`：此示例中包含节点的页面 `/content/wknd-spa-react/us/en/home`
   * `itemPath`：此示例中页面内节点的路径 `root/responsivegrid/text`
      * 由页面上包含项目的名称组成。

   ![节点的路径](assets/external-spa-path.png)

1. 在页面中的所需位置添加组件。

   ![将组件添加到页面](assets/external-spa-add-component.png)

   此 `AEMText` 组件可以通过添加到页面的所需位置 `pagePath` 和 `itemPath` 值设置为属性。 `pagePath` 是必需属性。

#### 验证在AEM上编辑文本内容 {#verify-text-edit}

现在，请在正在运行的AEM实例上测试该组件。

1. 从运行以下Maven命令 `aem-guides-wknd-spa` 目录，以便您可以生成项目并将其部署到AEM。

```shell
mvn clean install -PautoInstallSinglePackage
```

1. 在您的AEM实例上，导航到 `http://<host>:<port>/editor.html/content/wknd-spa-react/us/en/home.html`.

![在AEM中编辑SPA](assets/external-spa-edit-aem.png)

此 `AEMText` 组件现在可在AEM上创作。

### AEM可创作页面 {#aem-authorable-pages}

1. 标识要在SPA中添加以进行创作的页面。 此示例使用 `/content/wknd-spa-react/us/en/home.html`.
1. 创建文件(例如， `Page.js`)。 使用中提供的页面组件 `@adobe/cq-react-editable-components`.
1. 在部分中重复步骤4 [AEM可授权的叶组件](#authorable-leaf-components). 使用包装函数 `withMappable` 在组件上。
1. 与之前一样，应用 `MapTo` 页中所有子组件的AEM资源类型。

   ```javascript
   import { Page, MapTo, withMappable } from '@adobe/aem-react-editable-components';
   import Text, { TextEditConfig } from './Text';
   
   export default withMappable(Page);
   
   MapTo('wknd-spa-react/components/text')(Text, TextEditConfig);
   ```

   >[!NOTE]
   >
   >在此示例中，使用未包装的React文本组件，而不是包装的 `AEMText` 之前创建。 原因在于，当组件是页面/容器的一部分而不是单独存在时，容器会负责递归映射组件。 而且，每个子项不需要启用创作功能和其他包装器。

1. 要在SPA中添加可创作页面，请执行部分中的相同步骤 [将可创作组件添加到页面](#add-authorable-component-to-page). 在此，您可以跳过 `itemPath` 属性。

#### 验证AEM上的页面内容 {#verify-page-content}

要验证是否可以编辑页面，请执行部分中的相同步骤 [验证在AEM上编辑文本内容](#verify-text-edit).

![在AEM中编辑页面](assets/external-spa-edit-page.png)

现在，该页面可以在带有布局容器和子文本组件的AEM上编辑。

### 虚拟叶组件 {#virtual-leaf-components}

在前面的示例中，您使用现有AEM内容将组件添加到SPA。 但是，在某些情况下，内容尚未在AEM中创建，但必须由内容作者稍后添加。 为了适应此方案，前端开发人员可以在SPA内的相应位置添加组件。 在AEM的编辑器中打开这些组件时，会显示占位符。 内容作者将内容添加到这些占位符中后，将在JCR结构中创建节点并保留内容。 创建的元件允许一组与独立叶元件相同的操作。

在此示例中，您将重用 `AEMText` 之前创建的组件。 您希望将新文本添加到WKND主页上的现有文本组件下方。 各组分的添加与普通叶组分相同。 但是， `itemPath` 可以更新到必须添加新组件的路径。

因为新组件必须添加到位于的现有文本下方 `root/responsivegrid/text`，新路径为 `root/responsivegrid/{itemName}`.

```html
<AEMText
 pagePath='/content/wknd-spa-react/us/en/home'
 itemPath='root/responsivegrid/text_20' />
```

此 `TestPage` 添加虚拟组件后，组件如下所示。

![测试虚拟组件](assets/external-spa-virtual-component.png)

>[!NOTE]
>
>确保 `AEMText` 组件具有其 `resourceType` 在配置中设置，以便您可以启用此功能。

现在，您可以按照一节中的步骤将更改部署到AEM [验证在AEM上编辑文本内容](#verify-text-edit). 将显示当前不存在的占位符 `text_20` 节点。

![aem中的text_20节点](assets/external-spa-text20-aem.png)

当内容作者更新此组件时，将使用 `text_20` 节点创建于 `root/responsivegrid/text_20` 在 `/content/wknd-spa-react/us/en/home`.

![text20节点](assets/external-spa-text20-node.png)

#### 要求和限制 {#limitations}

添加虚拟叶组件有几项要求和一些限制。

* 此 `pagePath` 属性是创建虚拟组件的必需属性。
* 中的路径中提供的页面节点 `pagePath` 必须存在于AEM项目中。
* 要创建的节点的名称必须提供在 `itemPath`.
* 可以在任何级别创建组件。
   * 如果您提供 `itemPath='text_20'` 在上一个示例中，新节点直接在页面下创建，即 `/content/wknd-spa-react/us/en/home/jcr:content/text_20`
* 通过提供的指向在其中创建新节点的节点的路径必须有效 `itemPath`.
   * 在此示例中， `root/responsivegrid` 必须存在，以便新节点 `text_20` 可以在那里创建。
* 仅支持创建叶组件。 未来版本将支持虚拟容器和页面。

### 虚拟容器 {#virtual-containers}

支持添加容器的功能，即使尚未在AEM中创建相应的容器。 其概念和方法类似于 [虚拟叶组件](#virtual-leaf-components).

前端开发人员可以将容器组件添加到SPA内的相应位置，这些组件在AEM的编辑器中打开时会显示占位符。 然后，作者可以将组件及其内容添加到容器中，容器会在JCR结构中创建所需的节点。

例如，如果容器存在于 `/root/responsivegrid`，并且开发人员想要添加一个子容器：

![容器位置](assets/container-location.png)

此 `newContainer` 在AEM中尚不存在。

在AEM中编辑包含此组件的页面时，会显示一个空的容器占位符，作者可以在其中添加内容。

![容器占位符](assets/container-placeholder.png)

![JCR中的容器位置](assets/container-jcr-structure.png)

作者向容器中添加子组件后，将创建一个新的容器节点，该节点的JCR结构中具有对应的名称。

![包含内容的容器](assets/container-with-content.png)

![包含JCR中内容的容器](assets/container-with-content-jcr.png)

现在，可以根据作者的需要向容器中添加更多组件和内容，并且所做的更改会一直保留。

#### 要求和限制 {#container-limitations}

添加虚拟容器有几项要求和一些限制。

* 用于确定可以添加哪些组件的策略继承自父容器。
* 要创建的容器的直接父级必须存在于AEM中。
   * 如果容器 `root/responsivegrid` 存在于AEM容器中，则可以通过提供路径来创建新容器 `root/responsivegrid/newContainer`.
   * 但是 `root/responsivegrid/newContainer/secondNewContainer` 是不可能的。
* 一次只能创建一个新级别的组件。

## 其他自定义项 {#additional-customizations}

如果您按照上面的示例进行操作，则现在可以在AEM中编辑外部SPA。 但是，您可以进一步自定义外部SPA的其他方面。

### 根节点编号 {#root-node-id}

默认情况下，您可以假定React应用程序呈现在内部， `div` 元素ID的 `spa-root`. 如有必要，可以自定义此语法。

例如，假设您有一个SPA，其中应用程序呈现在 `div` 元素ID的 `root`. 此语法必须反映在三个文件中。

1. 在 `index.js` React应用程序的(或 `ReactDOM.render()` 称为)

   ![index.js文件中的ReactDOM.render()](assets/external-spa-root-index.png)

1. 在 `index.html` React应用程序的

   ![应用程序的index.html](assets/external-spa-index.png)

1. 在AEM应用程序的页面组件正文中，执行以下两个步骤：

   1. 创建 `body.html` 页面组件的。

   ![创建body.html文件](assets/external-spa-update-body.gif)

   1. 在新的中添加根元素 `body.html` 文件。

   ![将根元素添加到body.html](assets/external-spa-add-root.png)

### 编辑React SPA和路由 {#editing-react-spa-with-routing}

如果外部React SPA应用程序有多个页面， [它可以使用路由来确定要渲染的页面/组件](/help/implementing/developing/hybrid/routing.md). 基本用例是将当前活动的URL与为路由提供的路径进行匹配。 要在此类启用了路由的应用程序上启用编辑，必须转换要匹配的路径以容纳特定于AEM的信息。

在以下示例中，您有一个包含两个页面的简单React应用程序。 要渲染的页面是通过将提供给路由器的路径与活动URL进行匹配来确定的。 例如，如果您在 `mydomain.com/test`， `TestPage` 已呈现。

![外部SPA中的路由](assets/external-spa-routing.png)

要在AEM中为此示例SPA启用编辑，需要执行以下步骤。

1. 确定将用作AEM根目录的级别。

   * 对于示例，请将wknd-spa-react/us/en视为SPA的根。 此根意味着该路径之前的所有内容仅包含AEM页面/内容。

1. 在所需级别创建页面。

   * 在此示例中，要编辑的页面是 `mydomain.com/test`. `test` 在应用程序的根路径中。 在AEM中创建页面时，也必须保留此根路径。 因此，您可以在上一步中定义的根级别创建页面。
   * 创建的新页面必须与要编辑的页面具有相同的名称。 在此示例中，对于 `mydomain.com/test`，则创建的新页面必须 `/path/to/aem/root/test`.

1. 在SPA路由中添加帮助程序。

   * 新创建的页面尚无法在AEM中呈现预期内容。 原因是路由器需要一条路径 `/test` 而AEM活动路径为 `/wknd-spa-react/us/en/test`. 要容纳特定于AEM的URL部分，您必须在SPA端添加一些帮助程序。

   ![路由帮助程序](assets/external-spa-router-helper.png)

   * 此 `toAEMPath` 帮助程序提供者 `@adobe/cq-spa-page-model-manager` 可以使用。 当应用程序在AEM实例上打开时，它会转换为路由提供的路径，以包含AEM特定的部分。 它接受三个参数：
      * 路由所需的路径
      * 编辑SPA的AEM实例的源URL
      * 第一步中确定的AEM上的项目根目录

   * 可以将这些值设置为环境变量，以获得更大的灵活性。

1. 验证是否在AEM中编辑页面。

   * 将项目部署到AEM并导航到新创建的 `test` 页面。 页面内容现已呈现，并且AEM组件可编辑。

## 框架限制 {#framework-limitations}

RemotePage组件要求实施提供与资产清单类似的资产清单 [在此处找到](https://github.com/shellscape/webpack-manifest-plugin). 但是，RemotePage组件仅经过测试，可以与React框架（和通过remote-page-next组件的Next.js）配合使用，因此不支持从其他框架(如Angular)远程加载应用程序。

## 其他资源 {#additional-resources}

以下参考资料可能有助于了解AEM上下文中的SPA。

* [AEM 中的 Headful 和 Headless](/help/implementing/developing/headful-headless.md)
* [AEM项目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=zh-Hans)
* [WKND SPA项目](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html?lang=zh-Hans)
* [利用 React 在 AEM 中开始使用 SPA](/help/implementing/developing/hybrid/getting-started-react.md)
* [SPA参考资料（API参考）](/help/implementing/developing/hybrid/reference-materials.md)
* [SPA蓝图和PageModelManager](/help/implementing/developing/hybrid/blueprint.md#pagemodelmanager)
* [SPA模型路由](/help/implementing/developing/hybrid/routing.md)
* [SPA和服务器端渲染](/help/implementing/developing/hybrid/ssr.md)
