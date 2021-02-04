---
title: 在AEM中编辑外部SPA
description: 本文档介绍了将独立SPA上传到AEM实例、添加内容的可编辑部分以及启用创作的建议步骤。
translation-type: tm+mt
source-git-commit: bb8ab907dbeb422db410328f9c559c6794c16a8f
workflow-type: tm+mt
source-wordcount: '2127'
ht-degree: 0%

---

# 在AEM {#editing-external-spa-within-aem}中编辑外部SPA

在决定[外部SPA和AEM之间希望具有的集成级别](/help/implementing/developing/headful-headless.md)时，您通常需要能够编辑并视图AEM。

## 概述 {#overview}

本文档介绍了将独立SPA上传到AEM实例、添加内容的可编辑部分以及启用创作的建议步骤。

## 前提条件 {#prerequisites}

先决条件很简单。

* 确保AEM的实例在本地运行。
* 使用[AEM项目原型创建基AEM SPA项目。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?#available-properties)
   * 这将构成AEM项目的基础，该项目将进行更新以包括外部SPA。
   * 对于此文档中的示例，我们使用的起点为[ WKND SPA项目。](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html#spa-editor)
* 让外部React SPA工作，让您随手集成。

## 将SPA上传到AEM项目{#upload-spa-to-aem-project}

首先，您需要将外部SPA上传到AEM项目。

1. 将`/ui.frontend`项目文件夹中的`src`替换为React应用程序的`src`文件夹。
1. 在应用程序`package.json`的`/ui.frontend/package.json`文件中包含任何其他依赖项。
   * 确保SPA SDK依赖项为[推荐版本。](/help/implementing/developing/hybrid/getting-started-react.md#dependencies)
1. 在`/public`文件夹中包含所有自定义项。
1. 包括在`/public/index.html`文件中添加的任何内联脚本或样式。

## 配置远程SPA {#configure-remote-spa}

由于外部SPA是AEM项目的一部分，因此需要在AEM中配置它。

### 包括AdobeSPA SDK包{#include-spa-sdk-packages}

要利用AEM SPA功能，需要依赖以下三个包。

* [`@adobe/aem-react-editable-components`](https://github.com/adobe/aem-react-editable-components)
* [`@adobe/aem-spa-component-mapping`](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)
* [`@adobe/aem-spa-page-model-manager`](https://www.npmjs.com/package/@adobe/aem-spa-model-manager)

`@adobe/aem-spa-page-model-manager` 提供用于初始化模型管理器并从AEM实例检索模型的API。然后，此模型可用于使用`@adobe/aem-react-editable-components`和`@adobe/aem-spa-component-mapping`的API渲染AEM组件。

#### 安装{#installation}

运行以下npm命令以安装所需的包。

```shell
npm install --save @adobe/aem-spa-component-mapping @adobe/aem-spa-page-model-manager @adobe/aem-react-editable-components
```

### ModelManager初始化{#model-manager-initialization}

在应用程序呈现之前，[`ModelManager`](/help/implementing/developing/hybrid/blueprint.md#pagemodelmanager)需要进行初始化以处理AEM `ModelStore`的创建。

这需要在应用程序的`src/index.js`文件中或在呈现应用程序根目录的任何地方完成。

对于此，我们可以使用`ModelManager`提供的`initializationAsync` API。

以下屏幕截图显示了如何在简单的React应用程序中启用初始化`ModelManager`。 唯一的约束是`initializationAsync`需要在`ReactDOM.render()`之前调用。

![初始化ModelManager](assets/external-spa-initialize-modelmanager.png)

在此示例中，初始化`ModelManager`并创建空的`ModelStore`。

`initializationAsync` 可以选择接 `options` 受对象作为参数：

* `path` -初始化时，将读取定义路径上的模型并将其存储在 `ModelStore`。如果需要，可以在初始化时使用它获取`rootModel`。
* `modelClient` -允许提供负责获取模型的自定义客户端。
* `model` -使用 `model` SSR时通常填充为参数 [的对象。](/help/implementing/developing/hybrid/ssr.md)

### AEM可创作的Leaf组件{#authorable-leaf-components}

1. 创建／标识将为其创建可授权React组件的AEM组件。 在此示例中，我们使用WKND项目的文本组件。

   ![WKND文本组件](assets/external-spa-text-component.png)

1. 在SPA中创建一个简单的React文本组件。 在此示例中，已使用以下内容创建了新文件`Text.js`。

   ![Text.js](assets/external-spa-textjs.png)

1. 创建配置对象以指定启用AEM编辑所需的属性。

   ![创建配置对象](assets/external-spa-config-object.png)

   * `resourceType` 必须将React组件映射到AEM组件，并在AEM编辑器中打开时启用编辑。

1. 使用包装函数`withMappable`。

   ![与Mappable一起使用](assets/external-spa-withmappable.png)

   此包装器函数将React组件映射到配置中指定的AEM `resourceType`，并在AEM编辑器中打开时启用编辑功能。 对于独立组件，它还将获取特定节点的模型内容。

   >[!NOTE]
   >
   >在此示例中，组件有不同版本：AEM封装和未封装的React组件。 显式使用组件时，需要使用打包版本。 当组件是页面的一部分时，您可以继续使用默认组件，就像当前在SPA编辑器中一样。

1. 渲染组件中的内容。

   文本组件的JCR属性在AEM中显示如下。

   ![文本组件属性](assets/external-spa-text-properties.png)

   这些值将作为属性传递给新创建的`AEMText` React组件，并可用于呈现内容。

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

   这是AEM配置完成后组件的显示方式。

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
   >在此示例中，我们对渲染的组件进行了进一步自定义以匹配现有文本组件。 但这与在AEM中进行创作无关。

#### 将可创作组件添加到页面{#add-authorable-component-to-page}

创建可创作的React组件后，我们可以在整个应用程序中使用它们。

让我们举一个示例页，其中需要从WKND SPA项目添加文本。 在此示例中，我们要显示文本“Hello World!” on `/content/wknd-spa-react/us/en/home.html`.

1. 确定要显示的节点的路径。

   * `pagePath`:包含节点的页面，在我们的示例中  `/content/wknd-spa-react/us/en/home`
   * `itemPath`:页面中节点的路径，在我们的示例中  `root/responsivegrid/text`
      * 这由页面上包含项目的名称组成。

   ![节点的路径](assets/external-spa-path.png)

1. 在页面中的所需位置添加组件。

   ![将组件添加到页面](assets/external-spa-add-component.png)

   `AEMText`组件可以添加到页面中的所需位置，其中`pagePath`和`itemPath`值设置为属性。 `pagePath` 是强制属性。

#### 验证编辑AEM {#verify-text-edit}上的文本内容

我们现在可以在运行的AEM实例上测试该组件。

1. 从`aem-guides-wknd-spa`目录运行以下Maven命令以构建项目并将其部署到AEM。

```shell
mvn clean install -PautoInstallSinglePackage
```

1. 在AEM实例上，导航到`http://<host>:<port>/editor.html/content/wknd-spa-react/us/en/home.html`。

![在AEM中编辑SPA](assets/external-spa-edit-aem.png)

`AEMText`组件现在可在AEM上授权。

### AEM可创作页面{#aem-authorable-pages}

1. 确定要在SPA中添加以进行创作的页面。 此示例使用`/content/wknd-spa-react/us/en/home.html`。
1. 创建新文件(例如，`Page.js`)。 在此，我们可以重用`@adobe/cq-react-editable-components`中提供的页面组件。
1. 在[AEM可创作叶组件部分中重复步骤4。](#authorable-leaf-components) 对组件使 `withMappable` 用包装器函数。
1. 如之前所述，将`MapTo`应用于页面中所有子组件的AEM资源类型。

   ```javascript
   import { Page, MapTo, withMappable } from '@adobe/aem-react-editable-components';
   import Text, { TextEditConfig } from './Text';
   
   export default withMappable(Page);
   
   MapTo('wknd-spa-react/components/text')(Text, TextEditConfig);
   ```

   >[!NOTE]
   >
   >在此示例中，我们使用未封装的React文本组件，而不是先前创建的封装的`AEMText`。 这是因为当组件是页面/容器的一部分，而不是独立的时候，容器将负责定期映射组件并启用创作功能，而且每个子级不需要额外的包装器。

1. 要在SPA中添加可创作页面，请按照[将可创作组件添加到页面中的相同步骤操作。](#add-authorable-component-to-page) 但是，我们可以跳过 `itemPath` 该属性。

#### 验证AEM {#verify-page-content}上的页面内容

要验证页面是否可以编辑，请按照AEM上[验证文本内容编辑部分中的相同步骤操作。](#verify-text-edit)

![在AEM中编辑页面](assets/external-spa-edit-page.png)

现在可在AEM上使用布局容器和子文本组件编辑页面。

### 虚拟叶组件{#virtual-leaf-components}

在前面的示例中，我们将组件添加到SPA中并包含现有AEM内容。 但是，有些情况下，内容尚未在AEM中创建，但需要由内容作者稍后添加。 为了适应这种情况，前端开发人员可以在SPA的适当位置添加组件。 这些组件在AEM的编辑器中打开时将显示占位符。 内容作者在这些占位符中添加内容后，将以JCR结构创建节点并保留内容。 创建的组件将允许与独立的叶组件相同的操作集。

在此示例中，我们将重复使用先前创建的`AEMText`组件。 我们希望在WKND主页的现有文本组件下添加新文本。 添加的组件与添加常规叶组件相同。 但是，`itemPath`可以更新到需要添加新组件的路径。

由于新组件需要添加到`root/responsivegrid/text`的现有文本下，因此新路径应为`root/responsivegrid/{itemName}`。

```html
<AEMText
 pagePath='/content/wknd-spa-react/us/en/home'
 itemPath='root/responsivegrid/text_20' />
```

添加虚拟组件后，`TestPage`组件如下所示。

![测试虚拟组件](assets/external-spa-virtual-component.png)

>[!NOTE]
>
>确保`AEMText`组件在配置中设置了`resourceType`以启用此功能。

现在，您可以按照AEM上[验证文本内容编辑部分中的步骤将更改部署到AEM。](#verify-text-edit) 将显示当前非现有节点的占位符 `text_20` 。

![aem中的text_20节点](assets/external-spa-text20-aem.png)

当内容作者更新此组件时，将在`/content/wknd-spa-react/us/en/home`的`root/responsivegrid/text_20`上创建新的`text_20`节点。

![text20节点](assets/external-spa-text20-node.png)

#### 要求和限制{#limitations}

添加虚拟叶组件有许多要求，并存在一些限制。

* 创建虚拟组件时，`pagePath`属性是必填项。
* 在`pagePath`路径中提供的页面节点必须存在于AEM项目中。
* 要创建的节点的名称必须在`itemPath`中提供。
* 可在任何级别创建组件。
   * 如果我们在上一个示例中提供`itemPath='text_20'`，则新节点将直接在页面下创建，即`/content/wknd-spa-react/us/en/home/jcr:content/text_20`
* 当通过`itemPath`提供时，创建新节点的节点的路径必须有效。
   * 在此示例中，`root/responsivegrid`必须存在，这样新节点`text_20`就可以在此处创建。
* 仅支持创建叶组件。 将来版本将支持虚拟容器和页面。

## 其他自定义{#additional-customizations}

如果您按照以前的示例操作，您的外部SPA现在可在AEM中编辑。 但是，外部SPA还有其他方面可供您进一步自定义。

### 根节点ID {#root-node-id}

默认情况下，我们假定React应用程序呈现在元素ID `spa-root`的`div`中。 如果需要，可以自定义此项。

例如，假定我们有一个SPA，其中应用程序呈现在元素ID `root`的`div`中。 这需要反映在三个文件中。

1. 在React应用程序的`index.js`中（或调用`ReactDOM.render()`的位置）

   ![index.js文件中的ReactDOM.render()](assets/external-spa-root-index.png)

1. 在React应用程序的`index.html`中

   ![应用程序的index.html](assets/external-spa-index.png)

1. 在AEM应用程序的页面组件主体中，通过两个步骤：

   1. 为页面组件新建`body.html`。

   ![创建新body.html文件](assets/external-spa-update-body.gif)

   1. 在新的`body.html`文件中添加新的根元素。

   ![将根元素添加到body.html](assets/external-spa-add-root.png)

### 使用路由{#editing-react-spa-with-routing}编辑React SPA

如果外部React SPA应用程序有多个页面，[它可以使用路由确定要呈现的页面／组件。](/help/implementing/developing/hybrid/routing.md) 基本用例是将当前活动的URL与为路由提供的路径匹配。要在启用路由的应用程序上启用编辑，需要转换要与之匹配的路径以适应AEM特定信息。

在以下示例中，我们有一个简单的React应用程序，它包含两页。 要呈现的页面是通过将提供给路由器的路径与活动URL进行匹配来确定的。 例如，如果我们位于`mydomain.com/test`上，则将呈现`TestPage`。

![路由外部SPA](assets/external-spa-routing.png)

要在AEM中为此示例启用编辑，需要执行以下步骤。

1. 确定作为AEM根的级别。

   * 对于我们的样本，我们考虑将wknd-spa-react/us/en作为SPA的根。 这意味着该路径之前的所有内容都仅为AEM页面／内容。

1. 在所需级别创建新页面。

   * 在此示例中，要编辑的页面为`mydomain.com/test`。 `test` 位于应用程序的根路径中。在AEM中创建页面时也需要保留该属性。 因此，我们可以在上一步中定义的根级别创建新页面。
   * 创建的新页面必须与要编辑的页面具有相同的名称。 在此示例中，对于`mydomain.com/test`，创建的新页面必须为`/path/to/aem/root/test`。

1. 在SPA路由中添加帮手。

   * 新创建的页面尚不会在AEM中呈现预期内容。 这是因为路由器希望路径为`/test` ，而AEM活动路径为`/wknd-spa-react/us/en/test`。 要适应AEM特定URL的部分，我们需要在SPA端添加一些帮手。

   ![路由帮助器](assets/external-spa-router-helper.png)

   * `@adobe/cq-spa-page-model-manager`提供的`toAEMPath`帮助程序可用于此。 当应用程序在AEM实例上打开时，它会将为路由提供的路径转换为包含AEM特定部分。 它接受三个参数：
      * 路由所需的路径
      * 编辑SPA的AEM实例的来源URL
      * AEM上的项目根（在第一步中确定）
   * 这些值可设置为环境变量，以提高灵活性。



1. 验证在AEM中编辑页面。

   * 将项目部署到AEM并导航到新创建的`test`页面。 页面内容现在呈现，AEM组件可编辑。

## 其他资源 {#additional-resources}

以下参考资料有助于在AEM的上下文中了解SPA。

* [AEM中的头和头](/help/implementing/developing/headful-headless.md)
* [AEM项目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)
* [WKND SPA项目](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html)
* [AEM中SPA使用React入门](/help/implementing/developing/hybrid/getting-started-react.md)
* [SPA参考材料（API参考）](/help/implementing/developing/hybrid/reference-materials.md)
* [SPA Blueprint和PageModelManager](/help/implementing/developing/hybrid/blueprint.md#pagemodelmanager)
* [SPA模型路由](/help/implementing/developing/hybrid/routing.md)
* [SPA和服务器端渲染](/help/implementing/developing/hybrid/ssr.md)
