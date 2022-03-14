---
title: SPA 中的复合组件
description: 了解如何创建您自己的复合组件（由其他组件组成的组件），这些组件可与AEM单页应用程序(SPA)编辑器配合使用。
exl-id: fa1ab1dd-9e8e-4e2c-aa9a-5b46ed8a02cb
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 1%

---

# SPA 中的复合组件 {#composite-components-in-spas}

复合组件通过将多个基本组件组合到单个组件中，来利用AEM组件的模块化性质。 常见的复合组件用例是卡组件，由图像和文本组件的组合构成。

在AEM单页应用程序(SPA)编辑器框架中正确实施复合组件后，内容作者可以像拖放任何其他组件一样拖放此类组件，但仍能够单独编辑构成复合组件的每个组件。

本文演示了如何将复合组件添加到单页应用程序，以便与AEM SPA Editor无缝协作。

## 用例 {#use-case}

本文将以典型的卡组件作为示例用例。 卡片是许多数字体验的常用UI元素，通常由图像以及关联的文本或题注组成。 作者希望能够拖放整个卡片，但能够单独编辑卡片的图像并自定义关联的文本。

## 前提条件 {#prerequisites}

以下用于支持复合组件用例的模型需要满足以下先决条件。

* 您的AEM开发实例正在端口4502本地运行，并带有一个示例项目。
* 您有一个正在运行的外部React应用程序 [在AEM中启用进行编辑。](editing-external-spa.md)
* React应用程序将加载到AEM编辑器中 [使用RemotePage组件。](remote-page.md)

## 将复合组件添加到SPA {#adding-composite-components}

实施复合组件的模型有三种，具体取决于AEM中的SPA实施。

* [组件在您的AEM项目中不存在。](#component-does-not-exist)
* [组件存在于您的AEM项目中，但其必需内容不存在。](#content-does-not-exist)
* [组件及其所需内容都存在于您的AEM项目中。](#both-exist)

以下各节提供了使用卡组件作为示例实施每个案例的示例。

### 组件在您的AEM项目中不存在。 {#component-does-not-exist}

首先，创建将构成复合组件的组件，即图像及其文本的组件。

1. 在AEM项目中创建文本组件。
1. 添加对应的 `resourceType` 从组件中的项目 `editConfig` 节点。

   ```text
    resourceType: 'wknd-spa/components/text' 
   ```

1. 使用 `withMappable` 帮助程序以启用组件的编辑。

   ```text
   export const AEMText = withMappable(Text, TextEditConfig); 
   ```

文本组件将类似于以下内容。

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

如果您以类似的方式创建图像组件，则可以将其与 `AEMText` 组件转换为新卡片组件时，会将图像和文本组件用作子组件。

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

现在，此生成的复合组件可以放置在应用程序中的任意位置，并将在SPA编辑器中为文本和图像组件添加占位符。 在以下示例中，卡片组件会添加到标题下方的主组件中。

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

这将在编辑器中显示文本和图像的空占位符。 使用编辑器输入这些值时，它们会存储在指定的页面路径(即 `/content/wknd-spa/home`  在根级别上，使用 `itemPath`.

![编辑器中的复合卡组件](assets/composite-card.png)

### 组件存在于您的AEM项目中，但其必需内容不存在。 {#content-does-not-exist}

在这种情况下，已在包含标题和图像节点的AEM项目中创建卡组件。 子节点（文本和图像）具有相应的资源类型。

![卡组件的节点结构](assets/composite-node-structure.png)

然后，您可以将其添加到SPA并检索其内容。

1. 在SPA中为此创建相应的组件。 确保将子组件映射到SPA项目中相应的AEM资源类型。 在本例中，我们使用相同的 `AEMText` 和 `AEMImage` 组件详情 [在上一个情况下。](#component-does-not-exist)

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

1. 由于 `imagecard` 组件，将卡添加到页面。 在SPA中包含AEM中的现有容器。
   * 如果AEM项目中已存在一个容器，我们可以将其包含在SPA中，改为从AEM将组件添加到容器中。
   * 确保将卡组件映射到SPA中的相应资源类型。

   ```javascript
   <ResponsiveGrid
    pagePath='/content/wknd-spa/home'
    itemPath='root/responsivegrid' />
   ```

1. 添加已创建的 `wknd-spa/components/imagecard` 组件添加到容器组件允许的组件 [中。](/help/sites-cloud/authoring/features/templates.md)

现在 `imagecard` 组件可直接添加到AEM编辑器中的容器。

![编辑器中的复合卡片](assets/composite-card.gif)

### 组件及其所需内容都存在于您的AEM项目中。 {#both-exist}

如果内容存在于AEM中，则可以通过提供内容路径直接将其包含在SPA中。

```javascript
<AEMCard
    pagePath='/content/wknd-spa/home'
    itemPath='root/responsivegrid/imagecard' />
```

![节点结构中的复合路径](assets/composite-path.png)

的 `AEMCard` 组件与定义的组件相同 [在上一个用例中。](#content-does-not-exist) 在此，AEM项目中上述位置定义的内容将包含在SPA中。
