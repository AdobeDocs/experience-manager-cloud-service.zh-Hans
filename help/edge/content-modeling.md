---
title: 用于通过Edge Delivery Services项目进行AEM创作的内容建模
description: 了解内容建模如何用于AEM创作和Edge Delivery Services项目，以及如何对您自己的内容建模。
source-git-commit: 8f3c7524ae8ee642a9aee5989e03e6584a664eba
workflow-type: tm+mt
source-wordcount: '1940'
ht-degree: 1%

---


# 用于通过Edge Delivery Services项目进行AEM创作的内容建模 {#content-modeling}

了解内容建模如何用于AEM创作和Edge Delivery Services项目，以及如何对您自己的内容建模。

{{aem-authoring-edge-early-access}}

## 前提条件 {#prerequisites}

将AEM创作与Edge Delivery Services结合使用的项目继承了任何其他Edge Delivery Services项目的大部分机制，这与内容源或无关。 [创作方法。](/help/edge/authoring.md)

在开始为项目建模内容之前，请确保首先阅读以下文档。

* [快速入门 - 开发人员教程](/help/edge/developer/tutorial.md)
* [标记、部分、区块和自动屏蔽](/help/edge/developer/markup-sections-blocks.md)
* [区块集合](/help/edge/developer/block-collection.md)

为了提出一种不受内容源限制且引人注目的内容模型，必须了解这些概念。 本文档详细介绍专门为AEM创作实施的机制。

## 默认内容 {#default-content}

**默认内容** 是作者直观地放置在页面上的内容，而不添加任何其他语义。 这包括文本、标题、链接和图像。 这些内容在其功能和目的方面是自明的。

在AEM中，此内容作为组件实施，带有非常简单的预定义模型，其中包括可以在Markdown和HTML中序列化的所有内容。

* **文本**：富文本（包括列表元素以及强文本或斜体文本）
* **标题**：文本，类型(h1-h6)
* **图像**：源，描述
* **按钮**：文本、标题、URL、类型（默认、主要、次要）

这些元件的模型是 [使用Edge Delivery Services进行AEM创作的样板。](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/component-models.json#L2-L112)

## 区块 {#blocks}

块用于创建具有特定样式和功能的更丰富内容。 与默认内容相反，块确实需要额外的语义。 可以将块比作 [AEM页面编辑器中的组件。](/help/implementing/developing/components/overview.md)

块本质上是由JavaScript修饰的内容片段，使用样式表进行样式。

### 块模型定义 {#model-definition}

在将AEM创作与Edge Delivery Services结合使用时，必须显式建模块的内容，以便为作者提供创建内容的界面。 本质上，您需要创建一个模型，以便创作UI知道根据块向作者显示哪些选项。

此 [`component-models.json`](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/component-models.json) 文件定义块的模型。 在组件模型中定义的字段在AEM中作为属性保留，并在构成块的表中呈现为单元格。

```json
{
  "id": "hero",
  "fields": [
    {
      "component": "reference",
      "valueType": "string",
      "name": "image",
      "label": "Image",
      "multi": false
    },
    {
      "component": "text-input",
      "valueType": "string",
      "name": "imageAlt",
      "label": "Alt",
      "value": ""
    },
    {
      "component": "text-area",
      "name": "text",
      "value": "",
      "label": "Text",
      "valueType": "string"
    }
  ]
}
```

请注意，并非每个块都必须具有模型。 有些区块只是 [容器](#container) 用于子项列表，其中每个子项都有自己的模型。

还必须定义哪些块存在，并且可以使用通用编辑器将其添加到页面中。 此 [`component-definitions.json`](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/component-definition.json) 文件会列出由通用编辑器提供的组件。

```json
{
  "title": "Hero",
  "id": "hero",
  "plugins": {
    "xwalk": {
      "page": {
        "resourceType": "core/franklin/components/block/v1/block",
        "template": {
          "name": "Hero",
          "model": "hero"
        }
      }
    }
  }
}
```

可以为多个块使用一个模型。 例如，某些块可能共享定义文本和图像的模型。

对于每个块，开发人员会：

* 必须使用 `core/franklin/components/block/v1/block` 资源类型，AEM中块逻辑的常规实现。
* 必须定义块名称，该名称将在块的表头中呈现。
* 可以定义 [型号ID。](/help/implementing/universal-editor/field-types.md#model-structure)
* 可以定义 [过滤器ID。](/help/implementing/universal-editor/customizing.md#filtering-components)

将块添加到页面后，所有这些信息都会存储在AEM中。

>[!WARNING]
>
>如果可能，则无需实施自定义AEM组件。 AEM提供的Edge Delivery Services组件已足够，并且提供了某些护栏来简化开发。
>
>因此，Adobe不建议使用自定义AEM资源类型。

### 块结构 {#block-structure}

块的属性为 [在元件模型中定义](#model-definition) 并在AEM中持久保留。 属性在块的表状结构中呈现为单元格。

#### 简单块 {#simple}

在最简单的形式中，块按照属性在模型中定义的顺序，在单个行/列中呈现每个属性。

在以下示例中，首先在模型中定义图像，其次是文本。 因此，它们使用图像第一和文本第二渲染。

##### 数据 {#data-simple}

```json
{
  "name": "Hero",
  "model": "hero",
  "image": "/content/dam/image.png",
  "imageAlt": "Helix - a shape like a corkscrew",
  "text": "<h1>Welcome to AEM</h1>"
}
```

##### 标记 {#markup-simple}

```html
<div class="hero">
  <div>
    <div>
      <picture>
        <img src="/content/dam/image.png" alt="Helix - a shape like a corkscrew">
      </picture>
    </div>
  </div>
  <div>
    <div>
      <h1>Welcome to AEM</h1>
    </div>
  </div>
</div>
```

您可能会注意到某些类型的值允许在标记中推断语义，并且属性在单个单元格中组合在一起。 此行为在一节中进行描述 [类型推理。](#type-inference)

#### 键值块 {#key-value}

在许多情况下，建议修饰渲染的语义标记、添加CSS类名称、添加新节点或在DOM中移动它们以及应用样式。

但在其他情况下，块会作为类似键值对的配置读取。

这方面的一个例子是 [节元数据。](/help/edge/developer/markup-sections-blocks.md#sections) 在此使用案例中，可以将块配置为呈现为键值对表。 请参阅部分 [节和节元数据](#sections-metadata) 以了解更多信息。

##### 数据 {#data-key-value}

```json
{
  "name": "Featured Articles",
  "model": "spreadsheet-input",
  "key-value": true,
  "source": "/content/site/articles.json",
  "keywords": ['Developer','Courses'],
  "limit": 4
}
```

##### 标记 {#markup-key-value}

```html
<div class="featured-articles">
  <div>
    <div>source</div>
    <div><a href="/content/site/articles.json">/content/site/articles.json</a></div>
  </div>
  <div>
    <div>keywords</div>
    <div>Developer,Courses</div>
  <div>
  <div>
    <div>limit</div>
    <div>4</div>
  </div>
</div>
```

#### 容器块 {#container}

前两个结构都有一个维度：属性列表。 容器块允许添加子项（通常为相同类型或模型），因此是二维的。 这些块仍支持其自身的属性，这些属性呈现为先显示单个列的行。 但它们也允许添加子项，其中每个项都呈现为行，而每个属性都呈现为该行中的列。

在以下示例中，块接受链接图标列表作为子项，其中每个链接图标都有一个图像和链接。 请注意 [过滤器ID](/help/implementing/universal-editor/customizing.md#filtering-components) 在块的数据中设置，以引用过滤器配置。

##### 数据 {#data-container}

```json
{
  "name": "Our Partners",
  "model": "text-only",
  "filter": "our-partners",
  "text": "<p>Our community of partners is ...</p>",
  "item_0": {
    "model": "linked-icon",
    "image": "/content/dam/partners/foo.png",
    "imageAlt": "Icon of Foo",
    "link": "https://foo.com/"
  },
  "item_1": {
    "model": "linked-icon"
    "image": "/content/dam/partners/bar.png",
    "imageAlt": "Icon of Bar",
    "link": "https://bar.com"
  }
}
```

##### 标记 {#markup-container}

```html
<div class="our-partners">
  <div>
    <div>
        Our community of partners is ...
    </div>
  </div>
  <div>
    <div>
      <picture>
         <img src="/content/dam/partners/foo.png" alt="Icon of Foo">
      </picture>
    </div>
    <div>
      <a href="https://foo.com">https://foo.com</a>
    </div>
  </div>
  <div>
    <div>
      <picture>
         <img src="/content/dam/partners/bar.png" alt="Icon of Bar">
      </picture>
    </div>
    <div>
      <a href="https://bar.com">https://bar.com</a>
    </div>
  </div>
</div>
```

### 创建块的语义内容模型 {#creating-content-models}

使用 [块体结构的力学解释，](#block-structure) 可以创建将AEM中保留的内容一对一映射到交付层的内容模型。

在每个项目早期，必须为每个块仔细考虑内容模型。 它必须与内容源和创作体验无关，这样可让作者在重用块实施和样式时切换或组合它们。 欲知更多详情和一般指南，请参阅 [David&#39;s Model （举例2）。](https://www.aem.live/docs/davidsmodel) 更具体地说， [块集合](/help/edge/developer/block-collection.md) 包含一组广泛的内容模型，用于常见用户界面模式的特定用例。

对于使用Edge Delivery Services进行AEM创作，这就提出了一个问题：当使用由多个字段组成的表单来创作信息时，如何提供引人注目的语义内容模型，而不是像富文本那样编辑上下文中的语义标记。

要解决此问题，可通过三种方法轻松创建引人注目的内容模型：

* [类型推理](#type-inference)
* [字段折叠](#field-collapse)
* [元素分组](#element-grouping)

>[!NOTE]
>
>块实施可以解构内容并使用客户端渲染的DOM替换块。 虽然这对于开发人员来说是可能的、直观的，但对于Edge Delivery Services来说，这不是最佳实践。

#### 类型推理 {#type-inference}

对于某些值，我们可以从值本身推断出语义含义。 这些值包括：

* **图像**  — 如果对AEM中资源的引用是MIME类型以开头的资源 `image/`时，引用呈现为 `<picture><img src="${reference}"></picture>`.
* **链接**  — 如果引用存在于AEM中并且不是图像，或者如果值开头为 `https?://`  或 `#`时，引用呈现为 `<a href="${reference}">${reference}</a>` .
* **富文本**  — 如果修剪的值以段落(`p`， `ul`， `ol`， `h1`-`h6`，以富文本形式呈现值。
* **类名** - `classes` 属性被视为块选项，并在的表标题中呈现 [简单块，](#simple) 或作为中项目的值列表 [容器块。](#container)
* **值列表**  — 如果某个值是多值属性，且第一个值不为以前的任何值，则所有值都将连接为逗号分隔列表。

其他所有内容都将呈现为纯文本。

#### 字段折叠 {#field-collapse}

字段折叠是一种机制，它使用后缀根据命名惯例将多个字段值组合为一个语义元素 `Title`， `Type`， `Alt`、和 `Text` （全部区分大小写）。 任何以这些后缀结尾的属性都不会被视为值，而是另一个属性的属性。

##### 图像 {#image-collapse}

###### 数据 {#data-image}

```json
{
  "image": "/content/dam/red-car.png",
  "imageAlt: "A red card on a road"
}
```

###### 标记 {#markup-image}

```html
<picture>
  <img src="/content/dam/red-car.png" alt="A red car on a road">
</picture>
```

##### 链接和按钮 {#links-buttons-collapse}

###### 数据 {#data-links-buttons}

```json
{
  "link": "https://www.adobe.com",
  "linkTitle": "Navigate to adobe.com",
  "linkText": "adobe.com",
  "linkType": "primary"
}
```

###### 标记 {#markup-links-buttons}

否 `linkType`，或 `linkType=default`

```html
<a href="https://www.adobe.com" title="Navigate to adobe.com">adobe.com</a>
```

`linkType=primary`

```html
<strong>
  <a href="https://www.adobe.com" title="Navigate to adobe.com">adobe.com</a>
</strong>
```

`linkType=secondary`

```html
<em>
  <a href="https://www.adobe.com" title="Navigate to adobe.com">adobe.com</a>
</em>
```

##### 标题 {#headings-collapse}

###### 数据 {#data-headings}

```json
{
  "heading": "Getting started",
  "headingType": "h2"
}
```

###### 标记 {#markup-headings}

```html
<h2>Getting started</h2>
```

#### 元素分组 {#element-grouping}

同时 [字段折叠](#field-collapse) 是将多个属性组合为一个语义元素，元素组合是将多个语义元素组合为一个单元格。 对于应限制作者可创建的元素的类型和数量的用例，这尤其有帮助。

例如，作者应仅创建子标题、标题和单个段落描述，并最多创建两个行动号召按钮。 将这些元素组合在一起会生成无需进一步操作即可设置样式的语义标记。

##### 数据 {#data-grouping}

```json
{
  "name": "teaser",
  "model": "teaser",
  "image": "/content/dam/teaser-background.png",
  "imageAlt": "A group of people sitting on a stage",
  "teaserText_subtitle": "Adobe Experience Cloud"
  "teaserText_title": "Meet the Experts"
  "teaserText_titleType": "h2"
  "teaserText_description": "<p>Join us in this ask me everything session...</p>"
  "teaserText_cta1": "https://link.to/more-details",
  "teaserText_cta1Text": "More Details"
  "teaserText_cta2": "https://link.to/sign-up",
  "teaserText_cta2Text": "RSVP",
  "teaserText_cta2Type": "primary"
}
```

##### 标记 {#markup-grouping}

```html
<div class="teaser">
  <div>
    <div>
      <picture>
        <img src="/content/dam/teaser-background.png" alt="A group of people sitting on a stage">
      </picture>
    </div>
  </div>
  <div>
    <div>
      <p>Adobe Experience Cloud</p>
      <h2>Meet the Experts</h2>
      <p>Join us in this ask me everything session ...</p>
      <p><a href="https://link.to/more-details">More Details</a></p>
      <p><strong><a href="https://link.to/sign-up">RSVP</a></strong></p>
    </div>
  </div>
</div>
```

## 节和节元数据 {#sections-metadata}

与开发人员定义和建模多个文件的方式相同 [块，](#blocks) 它们可以定义不同的部分。

Edge Delivery Services的内容模型特意只允许单级别的嵌套，即部分包含的任何默认内容或块。 这意味着，为了拥有可包含其他组件的更复杂的可视化组件，必须将这些组件建模为部分，并使用自动阻止客户端组合在一起。 典型的示例是选项卡和可折叠部分，例如折叠。

可以使用与块相同的方式定义部分，但资源类型为 `core/franklin/components/section/v1/section`. 区域可以具有名称和 [筛选器ID、](/help/implementing/universal-editor/customizing.md#filtering-components) ，由 [通用编辑器](/help/implementing/universal-editor/introduction.md) 只是，以及 [型号ID，](/help/implementing/universal-editor/field-types.md#model-structure) 用于呈现节元数据。 这样，节元数据块的模型便会自动作为键值块附加到节（如果它不为空）。

此 [型号ID](/help/implementing/universal-editor/field-types.md#model-structure) 和 [过滤器ID](/help/implementing/universal-editor/customizing.md#filtering-components) 默认部分的 `section`. 它可用于更改默认节的行为。 以下示例将一些样式和背景图像添加到节元数据模型。

```json
{
  "id": "section",
  "fields": [
    {
      "component": "multiselect",
      "name": "style",
      "value": "",
      "label": "Style",
      "valueType": "string",
      "options": [
        {
          "name": "Fade in Background",
          "value": "fade-in"
        },
        {
          "name": "Highlight",
          "value": "highlight"
        }
      ]
    },
    {
      "component": "reference",
      "valueType": "string",
      "name": "background",
      "label": "Image",
      "multi": false
    }
  ]
}
```

以下示例定义了一个选项卡部分，在自动阻止期间，该部分可用于通过将连续部分与选项卡标题数据属性组合到选项卡块中来创建选项卡块。

```json
{
  "title": "Tab",
  "id": "tab",
  "plugins": {
    "xwalk": {
      "page": {
        "resourceType": "core/franklin/components/section/v1/section",
        "template": {
          "name": "Tab",
          "model": "tab",
          "filter": "section"
        }
      }
    }
  }
}
```

## 页面元数据 {#page-metadata}

文档可以有一个页面 [元数据块，](/help/edge/authoring.md#metadata--seo) 用于定义 `<meta>` 元素在中呈现 `<head>` 页面的。 AEMas a Cloud Service中页面的页面属性映射到那些可用于Edge Delivery Services的现成页面属性，例如 `title`， `description`， `keywords`，等等。

在进一步探索如何定义您自己的元数据之前，请查看以下文档以首先了解页面元数据的概念。

* [元数据](https://www.aem.live/developer/block-collection/metadata)
* [批量元数据](/help/edge/docs/bulk-metadata.md)

也可以通过两种方式定义其他页面元数据。

### 元数据电子表格 {#metadata-spreadsheets}

在AEMas a Cloud Service中，可以使用类似表的方式按路径或按路径模式定义元数据。 提供了一个用于类似于Excel或Google Sheets的类似表数据的创作UI。

要创建此类表，请创建一个页面，然后使用站点控制台中的元数据模板。

>[!NOTE]
>
>编辑元数据电子表格时，确保切换到 **预览** 模式，因为创作发生在页面本身，而不是编辑器中。

在电子表格的页面属性中，定义所需的元数据字段以及URL。 然后，为每个页面路径或页面路径模式添加元数据，其中URL字段与AEM中的映射公共路径而不是内容路径相关。

在发布之前，请确保电子表格已添加到路径映射中。

```text
mappings:
  - /content/site/:/
  - /content/site/metadata:/metadata.json
```

### 页面属性 {#page-properties}

还可以为页面元数据定义组件模型，该组件模型将作为AEM Sites页面属性对话框的选项卡提供给作者。

为此，需使用ID创建元件模型 `page-metadata`.

```json
{
  "id": "page-metadata",
  "fields": [
    {
      "component": "text-input",
      "name": "theme",
      "label": "Theme"
    }
  ]
}
```

有一些字段名称具有特殊含义，在提供创作对话框UI时将跳过这些名称：

* **`cq:tags`**  — 默认情况下， `cq:tags` 不会添加到元数据。 将它们添加到 `page-metadata` model会将标记ID作为以逗号分隔的列表添加为 `tags` meta标记到头。
* **`cq:lastModified`** - `cq:lastModified` 将其数据添加为 `last-modified` 头部。
