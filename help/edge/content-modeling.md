---
title: 使用 Edge Delivery Services 项目进行 AEM 创作的内容建模
description: 了解如何对使用 Edge Delivery Services 项目进行的 AEM 创作进行内容建模以及如何为您自己的内容进行建模。
exl-id: e68b09c5-4778-4932-8c40-84693db892fd
source-git-commit: becba7698afe4aa0629bf54fa0d0d26156784b5f
workflow-type: tm+mt
source-wordcount: '2072'
ht-degree: 99%

---

# 使用 Edge Delivery Services 项目进行 AEM 创作的内容建模 {#content-modeling}

了解如何对使用 Edge Delivery Services 项目进行的 AEM 创作进行内容建模以及如何为您自己的内容进行建模。

{{aem-authoring-edge-early-access}}

## 先决条件 {#prerequisites}

使用 Edge Delivery Services 进行 AEM 创作的项目继承了任何其他 Edge Delivery Services 项目的大部分机制，独立于内容源或[创作方法](/help/edge/authoring.md)。

在开始为项目内容建模之前，请确保先阅读以下文档。

* [快速入门 - 开发人员教程](/help/edge/developer/tutorial.md)
* [标记、分区、块和自动阻止](/help/edge/developer/markup-sections-blocks.md)
  <!--* [Block Collection](/help/edge/developer/block-collection.md)-->

必须理解这些概念，才能设计出通过与内容源无关方式工作的引人注目的内容模型。此文档提供了有关专门为 AEM 创作实施的机制的详细信息。

## 默认内容 {#default-content}

**默认内容**&#x200B;是作者在不添加任何额外语义的情况下直观地放置在页面上的内容。其中包括文本、标题、链接和图像。此类内容的功能和用途不言自明。

在 AEM 中，此内容作为具有非常简单的预定义模型的组件来实施，其中包括可在 Markdown 和 HTML 中序列化的所有内容。

* **文本**：富文本（包括列表元素和粗体或斜体文本）
* **标题**：文本、类型 (h1-h6)
* **图像**：来源、描述
* **按钮**：文本、标题、URL、类型（默认、主要、辅助）

这些组件的模型是[使用 Edge Delivery Services 进行 AEM 创作的样板](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/component-models.json#L2-L112)的一部分。

## 区块 {#blocks}

区块用于创建具有特定样式和功能的更丰富的内容。与默认内容相比，区块确实需要额外语义。可将区块比作 [AEM 页面编辑器中的组件](/help/implementing/developing/components/overview.md)。

区块实际上是由 JavaScript 装饰并使用样式表设置样式的内容片段。

### 区块模型定义 {#model-definition}

在使用 Edge Delivery Services 进行 AEM 创作时，必须对区块的内容进行显式建模，以便为作者提供用于创建内容的界面。从本质上讲，您需要创建一个模型，以便创作 UI 知道根据区块向作者提供哪些选项。

[`component-models.json`](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/component-models.json) 文件定义了区块的模型。组件模型中定义的字段将作为属性保留在 AEM 中，并在构成区块的表中呈现为单元格。

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

请注意，并非每个区块都必须具有模型。一些区块只是子级列表的[容器](#container)，其中每个子级都具有自己的模型。

还需要定义哪些区块存在并可使用 Universal Editor 将其添加到页面中。[`component-definitions.json`](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/component-definition.json) 文件列出了由 Universal Editor 提供的组件。

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

可以对多个区块使用一个模型。例如，一些区块可以共享一个定义文本和图像的模型。

对于每个区块，开发人员：

* 必须使用 `core/franklin/components/block/v1/block` 资源类型（AEM 中区块逻辑的一般实施）。
* 必须定义区块名称，该名称将呈现在区块的表标题中。
   * 区块名称用于获取正确的样式和脚本，以装饰区块。
* 可以定义[模型 ID](/help/implementing/universal-editor/field-types.md#model-structure)。
   * 模型 ID 是对组件模型的引用，它定义了作者在属性栏中可用的字段。
* 可以定义[过滤器 ID](/help/implementing/universal-editor/customizing.md#filtering-components)。
   * 过滤器 ID 是对组件过滤器的引用，它允许更改创作行为，例如通过限制可以将哪些子项添加到区块或部分，或者启用哪些 RTE 功能。

在将区块添加到页面时，所有这些信息都存储在 AEM 中。如果缺少资源类型或区块名称，则该区块将不会在页面上呈现。

>[!WARNING]
>
>在可能的情况下，没有必要或不建议实施自定义 AEM 组件。AEM 提供的 Edge Delivery Services 组件是足够的，并提供了某些护栏，以便于开发。
>
>AEM 提供的组件提供了一个标记，当发布到 Edge Delivery Services 时，[helix-html2md](https://github.com/adobe/helix-html2md) 可以使用该标记，当在通用编辑器中加载页面时，[aem.js](https://github.com/adobe/aem-boilerplate/blob/main/scripts/aem.js) 可以使用此标记。该标记是 AEM 与系统其他部分之间的稳定契约，不允许进行自定义。因此，项目不得更改组件，也不得使用自定义组件。

### 区块结构 {#block-structure}

区块的属性[在组件模型中定义](#model-definition)并保留在 AEM 中。属性呈现为区块的表状结构中的单元格。

#### 简单区块 {#simple}

在最简单的形式中，区块按照在模型中定义属性的顺序以单行/列形式呈现每个属性。

在以下示例中，在模型中依次定义图像和文本。因此，依次呈现图像和文本。

>[!BEGINTABS]

>[!TAB 数据]

```json
{
  "name": "Hero",
  "model": "hero",
  "image": "/content/dam/image.png",
  "imageAlt": "Helix - a shape like a corkscrew",
  "text": "<h1>Welcome to AEM</h1>"
}
```

>[!TAB 标记]

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

>[!TAB 表格]

```text
+---------------------------------------------+
| Hero                                        |
+=============================================+
| ![Helix - a shape like a corkscrew][image0] |
+---------------------------------------------+
| # Welcome to AEM                            |
+---------------------------------------------+
```

>[!ENDTABS]

您可能会发现，一些类型的值允许推断标记中的语义，并且属性将并入单个单元格中。[类型推断](#type-inference)部分中描述了此行为。

#### 键值区块 {#key-value}

在许多情况下，建议装饰呈现的语义标记、添加 CSS 类名称、添加新节点或在 DOM 中移动它们，以及应用样式。

但在其他情况下，区块将被读取为类似键值对的配置。

一个示例是[部分元数据。](/help/edge/developer/markup-sections-blocks.md#sections)在此用例中，可以将区块配置为呈现为键值对表。请参阅[部分和部分元数据](#sections-metadata)部分以了解更多信息。

>[!BEGINTABS]

>[!TAB 数据]

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

>[!TAB 标记]

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

>[!TAB 表格]

```text
+-----------------------------------------------------------------------+
| Featured Articles                                                     |
+=======================================================================+
| source   | [/content/site/articles.json](/content/site/articles.json) |
+-----------------------------------------------------------------------+
| keywords | Developer,Courses                                          |
+-----------------------------------------------------------------------+
| limit    | 4                                                          |
+-----------------------------------------------------------------------+
```

>[!ENDTABS]

#### 容器区块 {#container}

前面的两个结构都具有一个维度：属性列表。容器区块允许添加子级（通常属于相同类型或模型），因此是二维的。这些区块仍支持首先将其属性呈现为具有单列的行。但它们还允许添加子级，其中每个项目呈现为行，每个属性呈现为该行中的列。

在以下示例中，区块接受链接图标列表作为子级，其中每个链接的图标均有一个图像和一个链接。请注意区块数据中设置的[过滤器 ID](/help/implementing/universal-editor/customizing.md#filtering-components)，以便引用过滤器配置。

>[!BEGINTABS]

>[!TAB 数据]

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

>[!TAB 标记]

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

>[!TAB 表格]

```text
+------------------------------------------------------------ +
| Our Partners                                                |
+=============================================================+
| Our community of partners is ...                            |
+-------------------------------------------------------------+
| ![Icon of Foo][image0] | [https://foo.com](https://foo.com) |
+-------------------------------------------------------------+
| ![Icon of Bar][image1] | [https://bar.com](https://bar.com) |
+-------------------------------------------------------------+
```

>[!ENDTABS]

### 为区块创建语义内容模型 {#creating-content-models}

利用[解释的区块结构的机制](#block-structure)，可以创建一个内容模型，将 AEM 中保留的内容一对一映射到投放层。

在每个项目的早期阶段，必须仔细考虑每个区块的内容模型。它必须与内容源和创作体验无关，以允许作者在重用区块实施和样式时切换或组合它们。欲知更多详情和一般指南，请参阅 [David&#39;s Model （举例2）。](https://www.aem.live/docs/davidsmodel) <!--More specifically, the [block collection](/help/edge/developer/block-collection.md) contains a extensive set of content models for specific use cases of common user interface patterns.-->

对于使用 Edge Delivery Services 进行 AEM 创作，引出了一个问题：在使用由多个字段构成的表单创作信息，而不是在上下文（如富文本）中编辑语义标记时，如何提供引人注目的语义内容模型。

要解决此问题，可以使用三种方法来创建引人注目的内容模型：

* [类型推断](#type-inference)
* [字段折叠](#field-collapse)
* [元素分组](#element-grouping)

>[!NOTE]
>
>区块实施可以解构内容并将区块替换为客户端呈现的 DOM。虽然这对开发人员来说是可行且直观的，但这并不是 Edge Delivery Services 的最佳实践。

#### 类型推断 {#type-inference}

对于某些值，我们可以从值本身推断语义含义。此类值包括：

* **图像** - 如果对 AEM 中资源的引用是 MIME 类型的以 `image/` 开头的资源，则该引用将呈现为 `<picture><img src="${reference}"></picture>`。
* **链接** - 如果引用在 AEM 中存在且不是图像，或者值以 `https?://` 或 `#` 开头，则引用将呈现为 `<a href="${reference}">${reference}</a>`。
* **富文本** - 如果修剪后的值以段落（`p`、`ul`、`ol`、`h1`-`h6` 等）开头，该值将呈现为富文本。
* **类名** - `classes` 属性被视为区块选项，并呈现为表标题中的[简单区块](#simple)，或呈现为[容器区块](#container)中项目的值列表。
* **值列表** - 如果一个值是多值属性，并且第一个值不是前一个值，则所有值都以逗号分隔的列表形式连接起来。

所有其他内容都将呈现为纯文本。

#### 字段折叠 {#field-collapse}

字段折叠是根据使用后缀 `Title`、`Type`、`MimeType`、`Alt` 和 `Text`（均区分大小写）的命名约定，将多个字段值合并为一个语义元素的机制。任何以这些后缀结尾的属性将不被视为值，而被视为另一个属性的特性。

##### 图像 {#image-collapse}

>[!BEGINTABS]

>[!TAB 数据]

```json
{
  "image": "/content/dam/red-car.png",
  "imageAlt: "A red card on a road"
}
```

>[!TAB 标记]

```html
<picture>
  <img src="/content/dam/red-car.png" alt="A red car on a road">
</picture>
```

>[!TAB 表格]

```text
![A red car on a road][image0]
```

>[!ENDTABS]

##### 链接和按钮 {#links-buttons-collapse}

>[!BEGINTABS]

>[!TAB 数据]

```json
{
  "link": "https://www.adobe.com",
  "linkTitle": "Navigate to adobe.com",
  "linkText": "adobe.com",
  "linkType": "primary"
}
```

>[!TAB 标记]

无 `linkType` 或 `linkType=default`

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

>[!TAB 表格]

```text
[adobe.com](https://www.adobe.com "Navigate to adobe.com")
**[adobe.com](https://www.adobe.com "Navigate to adobe.com")**
_[adobe.com](https://www.adobe.com "Navigate to adobe.com")_
```

>[!ENDTABS]

##### 标题 {#headings-collapse}

>[!BEGINTABS]

>[!TAB 数据]

```json
{
  "heading": "Getting started",
  "headingType": "h2"
}
```

>[!TAB 标记]

```html
<h2>Getting started</h2>
```

>[!TAB 表格]

```text
## Getting started
```

>[!ENDTABS]

#### 元素分组 {#element-grouping}

[字段折叠](#field-collapse)是指将多个属性合并为单个语义元素，元素分组是指将多个语义元素连接成单个单元格。在应限制作者可创建的元素的类型和数量的用例中，这特别有用。

例如，Teaser 组件可能只会允许作者创建一个子标题、标题和单个段落描述，并与最多两个动作按钮相结合。将这些元素分组在一起会产生一个语义标记，无需进一步操作即可设置其样式。

元素分组会使用命名约定，其中组名称与组中的每个属性之间用下划线分隔。组中属性的字段折叠的工作原理如前所述。

>[!BEGINTABS]

>[!TAB 数据]

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

>[!TAB 标记]

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

>[!TAB 表格]

```text
+-------------------------------------------------+
| Teaser                                          |
+=================================================+
| ![A group of people sitting on a stage][image0] |
+-------------------------------------------------+
| Adobe Experience Cloud                          |
| ## Welcome to AEM                               |
| Join us in this ask me everything session ...   |
| [More Details](https://link.to/more-details)    |
| [RSVP](https://link.to/sign-up)                 |
+-------------------------------------------------+
```

>[!ENDTABS]

## 部分和部分元数据 {#sections-metadata}

利用开发人员用来对多个[区块](#blocks)进行定义和建模的方式，可以定义不同的部分。

Edge Delivery Services 的内容模型有意只允许单级嵌套，即部分包含的任何默认内容或区块。这意味着，要拥有可包含其他组件的更复杂的视觉组件，必须使用自动屏蔽客户端将它们作为部分进行建模和组合。典型示例是选项卡和可折叠部分，例如可折叠项。

可按照定义区块的方式定义部分，但资源类型为 `core/franklin/components/section/v1/section`。部分可具有一个名称、一个[过滤器 ID](/help/implementing/universal-editor/customizing.md#filtering-components)（仅由 [Universal Editor](/help/implementing/universal-editor/introduction.md) 使用）和一个[模型 ID](/help/implementing/universal-editor/field-types.md#model-structure)（用于呈现部分元数据）。这样一来，模型便为部分元数据区块的模型，如果它不为空，则会自动作为键值区块附加到部分中。

默认部分的[模型 ID](/help/implementing/universal-editor/field-types.md#model-structure) 和[过滤器 ID](/help/implementing/universal-editor/customizing.md#filtering-components) 是 `section`。它可用于更改默认部分的行为。以下示例将一些样式和背景图像添加到部分元数据模型。

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

以下示例定义一个选项卡部分，可用于通过在自动遮蔽期间将连续部分与选项卡标题数据属性组合成选项卡区块来创建选项卡区块。

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

文档可以具有页面[元数据区块](/help/edge/authoring.md#metadata--seo)，它用于定义哪些 `<meta>` 元素呈现在页面的 `<head>` 中。AEM as a Cloud Service 中页面的页面属性映射到 Edge Delivery Services 的现成页面属性，例如 `title`、`description`、`keywords` 等。

在进一步探索如何定义自己的元数据之前，请先查看以下文档以了解页面元数据的概念。

* [元数据](https://www.aem.live/developer/block-collection/metadata)
* [批量元数据](/help/edge/docs/bulk-metadata.md)

还可以通过两种方式定义其他页面元数据。

### 元数据电子表格 {#metadata-spreadsheets}

可以在 AEM as a Cloud Service 中以类似表格的方式定义每个路径或每个路径模式的元数据。有一个可用于类似 Excel 或 Google Sheets 的表格数据的创作 UI。

要创建此类表，请创建一个页面并使用 Sites 控制台中的元数据模板。

在电子表格的页面属性中，定义所需的元数据字段以及 URL。然后添加每个页面路径或页面路径模式的元数据。

在发布之前，请确保也已将电子表格添加到您的路径映射中。

```json
{
  "mappings": [
    "/content/site/:/",
    "/content/site/metadata:/metadata.json"
  ]
}
```

### 页面属性 {#page-properties}

AEM 中提供的许多默认页面属性都映射到文档中相应的页面元数据。例如，包括 `title`、`description`、`robots`、`canonical url` 或者 `keywords`。还提供一些特定于 AEM 的属性：

* `cq:lastModified`（ISO8601 格式）显示的 `modified-time` 
* 文档最后发布的时间为 `published-time`（ISO8601 格式）
* `cq:tags` 作为逗号分隔标记 ID 列表的 `cq-tags`。

还可以为自定义页面元数据定义组件模型，作者可以将其作为 AEM Sites 页面属性对话框的选项卡使用。

为此，请使用 ID `page-metadata` 创建组件模型。

```json
{
  "id": "page-metadata",
  "fields": [
    {
      "component": "text",
      "name": "theme",
      "label": "Theme"
    }
  ]
}
```
