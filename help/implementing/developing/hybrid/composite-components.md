---
title: SPA 中的复合组件
description: 了解如何创建自己的复合组件，这些组件由使用AEM单页应用程序(SPA)编辑器的其他组件组成。
exl-id: fa1ab1dd-9e8e-4e2c-aa9a-5b46ed8a02cb
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 1%

---

# SPA 中的复合组件 {#composite-components-in-spas}

复合组件通过将多个基础组件组合到一个组件中，来使用AEM组件的模块化特性。 常见的复合组件用例是卡组件，由图像和文本组件组合而成。

在AEM单页应用程序(SPA)编辑器框架中正确实施复合组件后，内容作者可以像拖放任何其他组件一样拖放此类组件，但仍可以单独编辑构成复合组件的每个组件。

本文演示了如何将复合组件添加到单页应用程序，以便与AEM SPA编辑器无缝地配合使用。

{{ue-over-spa}}

## 用例 {#use-case}

本文将以典型卡组件作为示例用例。 信息卡是许多数字体验的公用UI元素，通常由图像和相关文本或标题组成。 作者希望能够拖放整个卡片，但能够单独编辑卡片的图像并自定义关联的文本。

## 先决条件 {#prerequisites}

以下支持复合组件用例的模型需要以下先决条件。

* 您的AEM开发实例正在带有示例项目的端口4502上本地运行。
* 您已启用工作正常的外部React应用程序[以便在AEM](editing-external-spa.md)中进行编辑。
* 使用RemotePage组件[&#128279;](remote-page.md)在AEM编辑器中加载React应用程序。

## 将复合组件添加到SPA {#adding-composite-components}

实施复合组件有三种不同的模型，具体取决于AEM中的SPA实施。

* [您的AEM项目中不存在该组件](#component-does-not-exist)。
* [组件存在于您的AEM项目中，但其必需的内容不是](#content-does-not-exist)。
* [组件及其所需内容都存在于您的AEM项目](#both-exist)中。

以下部分提供了使用卡组件作为示例来实施每个用例的示例。

### 您的AEM项目中不存在该组件。 {#component-does-not-exist}

首先，创建将构成复合组件的组件，即图像及其文本的组件。

1. 在AEM项目中创建文本组件。
1. 在组件的`editConfig`节点中，从项目中添加相应的`resourceType`。

   ```text
    resourceType: 'wknd-spa/components/text' 
   ```

1. 使用`withMappable`帮助程序启用组件的编辑。

   ```text
   export const AEMText = withMappable(Text, TextEditConfig); 
   ```

文本组件类似于以下内容。

```javascript
import React from 'react';
import { withMappable } from '@adobe/aem-react-editable-components';

export const TextEditConfig = {
  emptyLabel: 'Text',
  isEmpty: function(props) {
    return !props || !props.text || props.text.trim().length < 1;
  },
  resourceType: 'wknd-spa/components/text'
};

export const Text = ({ cqPath, richText, text }) => {
  const richTextContent = () => (
    <div className="aem_text"
      id={cqPath.substr(cqPath.lastIndexOf('/') + 1)}
      data-rte-editelement
      dangerouslySetInnerHTML={{__html: text}} />
  );
  return richText ? richTextContent() : (
     <div className="aem_text">{text}</div>
  );
};

export const AEMText = withMappable(Text, TextEditConfig);
```

如果以类似方式创建图像组件，则可以将其与`AEMText`组件组合到一个新的卡组件中，并将图像和文本组件用作子组件。

```javascript
import React from 'react';
import { AEMText } from './AEMText';
import { AEMImage } from './AEMImage';

export const AEMCard = ({ pagePath, itemPath}) => (
  <div>
    <AEMText
       pagePath={pagePath}
       itemPath={`text`} />
    <AEMImage
       pagePath={pagePath}
       itemPath={`image`} />
   </div>
);
```

生成的复合组件现在可以放置在应用程序中的任意位置，并且将在SPA编辑器中为文本和图像组件添加占位符。 在以下示例中，信息卡组件被添加到标题下的主页组件。

```javascript
function Home() {
  return (
    <div className="Home">
      <h2>Current Adventures</h2>
      <AEMCard
        pagePath='/content/wknd-spa/home' />
    </div>
  );
}
```

这将在编辑器中显示文本和图像的空占位符。 使用编辑器输入这些值的值时，它们存储在指定的页面路径上，即`/content/wknd-spa/home`，根级别为`itemPath`中指定的名称。

编辑器中的![复合卡组件](assets/composite-card.png)

### 您的AEM项目中存在该组件，但其必需的内容不存在。 {#content-does-not-exist}

在这种情况下，卡组件已在包含标题和图像节点的AEM项目中创建了。 子节点（文本和图像）具有相应的资源类型。

卡组件![&#128279;](assets/composite-node-structure.png)的节点结构

然后，您可以将其添加到SPA并检索其内容。

1. 在SPA中为此创建对应的组件。 确保子组件映射到SPA项目中的相应AEM资源类型。 在此示例中，我们使用与上一个案例[&#128279;](#component-does-not-exist)中详细的相同的`AEMText`和`AEMImage`组件。

   ```javascript
   import React from 'react';
   import { Container, withMappable, MapTo } from '@adobe/aem-react-editable-components';
   import { Text, TextEditConfig } from './AEMText';
   import Image, { ImageEditConfig } from './AEMImage';
   
   export const AEMCard = withMappable(Container, {
     resourceType: 'wknd-spa/components/imagecard'
   });
   
   MapTo('wknd-spa/components/text')(Text, TextEditConfig);
   MapTo('wknd-spa/components/image')(Image, ImageEditConfig);
   ```

1. 由于`imagecard`组件没有内容，请将该卡添加到页面。 在SPA中包含来自AEM的现有容器。
   * 如果AEM项目中已有容器，我们可以改为将此容器包含在SPA中，并改为从AEM将组件添加到容器中。
   * 确保卡组件映射到SPA中相应的资源类型。

   ```javascript
   <ResponsiveGrid
    pagePath='/content/wknd-spa/home'
    itemPath='root/responsivegrid' />
   ```

1. 将创建的`wknd-spa/components/imagecard`组件添加到页面模板[&#128279;](/help/sites-cloud/authoring/page-editor/templates.md)中的容器组件允许的组件中。

现在，可以在AEM编辑器中将`imagecard`组件直接添加到容器中。

编辑器中的![复合卡](assets/composite-card.gif)

### AEM项目中同时存在该组件及其必需内容。 {#both-exist}

如果内容存在于AEM中，则通过提供内容的路径可以直接将其包含在SPA中。

```javascript
<AEMCard
    pagePath='/content/wknd-spa/home'
    itemPath='root/responsivegrid/imagecard' />
```

![节点结构中的复合路径](assets/composite-path.png)

`AEMCard`组件与上一个用例[&#128279;](#content-does-not-exist)中定义的相同。 此处，在AEM项目的上述位置中定义的内容包含在SPA中。
