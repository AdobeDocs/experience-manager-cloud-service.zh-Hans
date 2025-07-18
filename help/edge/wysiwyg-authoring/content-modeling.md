---
title: 使用 Edge Delivery Services 项目进行所见即所得创作的内容建模
description: 了解使用 Edge Delivery Services 项目进行所见即所得创作的内容建模工作原理，以及如何为自己的内容建模。
exl-id: e68b09c5-4778-4932-8c40-84693db892fd
feature: Edge Delivery Services
role: Admin, Architect, Developer
index: false
hide: true
hidefromtoc: true
source-git-commit: fecbebde808c545a84889da5610a79c088f2f459
workflow-type: ht
source-wordcount: '2160'
ht-degree: 100%

---


# 使用 Edge Delivery Services 项目进行所见即所得创作的内容建模 {#content-modeling}

了解使用 Edge Delivery Services 项目进行所见即所得创作的内容建模工作原理，以及如何为自己的内容建模。

## 前提条件 {#prerequisites}

使用 Edge Delivery Services 项目进行所见即所得创作继承了其他 Edge Delivery Services 项目的大部分机制，这与内容来源或[创作方法](/help/edge/wysiwyg-authoring/authoring.md)无关。

在开始为项目内容建模之前，请确保先阅读以下文档。

* [快速入门 - 开发人员教程](/help/edge/developer/tutorial.md)
* [标记、部分、块和自动屏蔽](/help/edge/developer/markup-sections-blocks.md)
* [块集合](/help/edge/developer/block-collection.md)

必须理解这些概念，才能设计出通过与内容源无关方式工作的引人注目的内容模型。本文档详细介绍了专为所见即所得创作而实施的机制。

## 默认内容 {#default-content}

**默认内容**&#x200B;是作者在不添加任何额外语义的情况下直观地放置在页面上的内容。其中包括文本、标题、链接和图像。此类内容的功能和用途不言自明。

在 AEM 中，此内容作为具有非常简单的预定义模型的组件来实施，其中包括可在 Markdown 和 HTML 中序列化的所有内容。

* **文本**：富文本（包括列表元素和粗体或斜体文本）
* **标题**：文本、类型 (h1-h6)
* **图像**：来源、描述
* **按钮**：文本、标题、URL、类型（默认、主要、辅助）

这些组件的模型是[使用 Edge Delivery Services 进行所见即所得创作的样板文件](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/component-models.json#L2-L112)的一部分。

## 块 {#blocks}

块用于创建具有特定样式和功能的更丰富的内容。与默认内容相比，块确实需要额外的语义。

块实际上是由 JavaScript 装饰并使用样式表设置样式的内容片段。

### 块模型定义 {#model-definition}

当使用 Edge Delivery Services 进行所见即所得创作时，必须明确地对块的内容进行建模，以便为作者提供创建内容的界面。从本质上讲，您需要创建一个模型，以便创作 UI 知道根据块向作者提供哪些选项。

[`component-models.json`](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/component-models.json) 文件定义了块的模型。组件模型中定义的字段将作为属性保留在 AEM 中，并在构成块的表中呈现为单元格。

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

请注意，并非每个块都必须具有模型。一些块只是子级列表的[容器](#container)，其中每个子级都具有自己的模型。

还需要定义哪些块存在并可使用 Universal Editor 将其添加到页面中。[`component-definitions.json`](/help/implementing/universal-editor/component-definition.md) 文件列出了由 Universal Editor 提供的组件。

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

可以对多个块使用一个模型。例如，一些块可以共享一个定义文本和图像的模型。

对于每个块，开发人员：

* 必须使用 `core/franklin/components/block/v1/block` 资产类型（AEM 中块逻辑的一般实施）。
* 必须定义块名称，该名称将呈现在块的表标题中。
   * 块名称用于获取正确的样式和脚本，以装饰块。
* 可以定义[模型 ID](/help/implementing/universal-editor/field-types.md#model-structure)。
   * 模型 ID 是对组件模型的引用，它定义了作者在属性面板中可用的字段。
* 可以定义[过滤器 ID](/help/implementing/universal-editor/filtering.md)。
   * 过滤器 ID 是对组件过滤器的引用，它允许更改创作行为，例如通过限制可以将哪些子项添加到块或部分，或者启用哪些 RTE 功能。

在将块添加到页面时，所有这些信息都存储在 AEM 中。如果缺少资产类型或块名称，则该块将不会在页面上呈现。

>[!WARNING]
>
>在可能的情况下，没有必要或不建议实施自定义 AEM 组件。AEM 提供的 Edge Delivery Services 组件是足够的，并提供了某些护栏，以便于开发。
>
>AEM 提供的组件提供了一个标记，当发布到 Edge Delivery Services 时，[helix-html2md](https://github.com/adobe/helix-html2md) 可以使用该标记，当在通用编辑器中加载页面时，[aem.js](https://github.com/adobe/aem-boilerplate/blob/main/scripts/aem.js) 可以使用此标记。该标记是 AEM 与系统其他部分之间的稳定契约，不允许进行自定义。因此，项目不得更改组件，也不得使用自定义组件。

### 块结构 {#block-structure}

块的属性[在组件模型中定义](#model-definition)并保留在 AEM 中。属性呈现为块的表状结构中的单元格。

#### 简单块 {#simple}

在最简单的形式中，块按照在模型中定义属性的顺序以单行/列形式呈现每个属性。

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

#### 键值块 {#key-value}

在许多情况下，建议装饰呈现的语义标记、添加 CSS 类名称、添加新节点或在 DOM 中移动它们，以及应用样式。

但在其他情况下，块将被读取为类似键值对的配置。

一个示例是[部分元数据](/help/edge/developer/markup-sections-blocks.md#sections)。在此用例中，可以将块配置为呈现为键值对表。请参阅[部分和部分元数据](#sections-metadata)部分以了解更多信息。

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

#### 容器块 {#container}

前面的两个结构都具有一个维度：属性列表。容器块允许添加子级（通常属于相同类型或模型），因此是二维的。这些块仍支持首先将其属性呈现为具有单列的行。但它们还允许添加子级，其中每个项目呈现为行，每个属性呈现为该行中的列。

在以下示例中，块接受链接图标列表作为子级，其中每个链接的图标均有一个图像和一个链接。请注意块数据中设置的[过滤器 ID](/help/implementing/universal-editor/filtering.md)，以便引用过滤器配置。

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

### 为块创建语义内容模型 {#creating-content-models}

利用[解释的块结构的机制](#block-structure)，可以创建一个内容模型，将 AEM 中保留的内容一对一映射到投放层。

在每个项目的早期阶段，必须仔细考虑每个块的内容模型。它必须与内容源和创作体验无关，以允许作者在重用块实施和样式时切换或组合它们。有关更多详细信息和一般指南，请参阅 [David&#39;s 模型（take 2）](https://www.aem.live/docs/davidsmodel)。 更具体地说，[块集合](/help/edge/developer/block-collection.md)包含一组广泛的内容模型，可用于常见用户界面模式的特定用例。

对于使用 Edge Delivery Services 进行所见即所得的创作的情况来说，这就提出了一个问题，即当信息是用由多个字段组成的表单创作的，而不是在类似上下文的富文本中编辑语义标记时，如何提供一个引人注目的语义内容模型。

要解决此问题，可以使用三种方法来创建引人注目的内容模型：

* [类型推断](#type-inference)
* [字段折叠](#field-collapse)
* [元素分组](#element-grouping)

>[!NOTE]
>
>块实施可以解构内容并将块替换为客户端呈现的 DOM。虽然这对开发人员来说是可行且直观的，但这并不是 Edge Delivery Services 的最佳实践。

#### 类型推断 {#type-inference}

对于某些值，我们可以从值本身推断语义含义。此类值包括：

* **图像** - 如果对 AEM 中资产的引用是 MIME 类型的以 `image/` 开头的资产，则该引用将呈现为 `<picture><img src="${reference}"></picture>`。
* **链接** - 如果引用在 AEM 中存在且不是图像，或者值以 `https?://` 或 `#` 开头，则引用将呈现为 `<a href="${reference}">${reference}</a>`。
* **富文本** - 如果修剪后的值以段落（`p`、`ul`、`ol`、`h1`-`h6` 等）开头，该值将呈现为富文本。
* **类名** - `classes` 属性被视为[块选项](/help/edge/developer/markup-sections-blocks.md#block-options)，并在[简单块](#simple)的表头中呈现，或作为[容器块](#container)中项目的值列表呈现。如果您想[以不同的方式设置一个块](/help/edge/wysiwyg-authoring/create-block.md#block-options)，但不需要创建一个全新的块，这很有用。
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
| ## Meet the Experts                             |
| Join us in this ask me everything session ...   |
| [More Details](https://link.to/more-details)    |
| [RSVP](https://link.to/sign-up)                 |
+-------------------------------------------------+
```

>[!ENDTABS]

## 部分和部分元数据 {#sections-metadata}

利用开发人员用来对多个[块](#blocks)进行定义和建模的方式，可以定义不同的部分。

Edge Delivery Services 的内容模型有意只允许单级嵌套，即部分包含的任何默认内容或块。这意味着，要拥有可包含其他组件的更复杂的视觉组件，必须使用自动屏蔽客户端将它们作为部分进行建模和组合。典型示例是选项卡和可折叠部分，例如可折叠项。

可按照定义块的方式定义部分，但资产类型为 `core/franklin/components/section/v1/section`。部分可具有一个名称、一个[过滤器 ID](/help/implementing/universal-editor/filtering.md)（仅由[通用编辑器](/help/implementing/universal-editor/introduction.md)使用）和一个[模型 ID](/help/implementing/universal-editor/field-types.md#model-structure)（用于呈现部分元数据）。这样一来，模型便为部分元数据块的模型，如果它不为空，则会自动作为键值块附加到部分中。

默认部分的[模型 ID](/help/implementing/universal-editor/field-types.md#model-structure) 和[过滤器 ID](/help/implementing/universal-editor/filtering.md) 是 `section`。它可用于更改默认部分的行为。以下示例将一些样式和背景图像添加到部分元数据模型。

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

以下示例定义一个选项卡部分，可用于通过在自动遮蔽期间将连续部分与选项卡标题数据属性组合成选项卡块来创建选项卡块。

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

文档可以具有页面[元数据块](https://www.aem.live/developer/block-collection/metadata)，它用于定义哪些 `<meta>` 元素呈现在页面的 `<head>` 中。AEM as a Cloud Service 中页面的页面属性映射到 Edge Delivery Services 的现成页面属性，例如 `title`、`description`、`keywords` 等。

在进一步探索如何定义自己的元数据之前，请先查看以下文档以了解页面元数据的概念。

* [元数据](https://www.aem.live/developer/block-collection/metadata)
* [批量元数据](/help/edge/docs/bulk-metadata.md)

还可以通过两种方式定义其他页面元数据。

### 元数据电子表格 {#metadata-spreadsheets}

可以在 AEM as a Cloud Service 中以类似表格的方式定义每个路径或每个路径模式的元数据。有一个可用于类似 Excel 或 Google Sheets 的表格数据的创作 UI。

有关更多详细信息，请参阅文档[使用电子表格管理表格数据](/help/edge/wysiwyg-authoring/tabular-data.md)以获取更多信息。

### 页面属性 {#page-properties}

AEM 中提供的许多默认页面属性都映射到文档中相应的页面元数据。例如，包括 `title`、`description`、`robots`、`canonical url` 或者 `keywords`。还提供一些特定于 AEM 的属性：

* `cq:lastModified`（ISO8601 格式）显示的 `modified-time` 
* 文档最后发布的时间为 `published-time`（ISO8601 格式）
* `cq:tags` as `cq-tags`作为逗号分隔标记 ID 列表。

还可以为自定义页面元数据定义一个组件模型，该模型将在通用编辑器中提供给作者。

为此，创建一个 ID 为 `page-metadata` 的组件模型。

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

## 后续步骤 {#next-steps}

现在您已经知道如何对内容进行建模，您可以使用所见即所得创作项目为自己的 Edge Delivery Services 创建块。

请参阅文档[创建与通用编辑器配合使用的块](/help/edge/wysiwyg-authoring/create-block.md)，了解如何在所见即所得的创作中使用 Edge Delivery Services 项目创建与通用编辑配合使用的块。

如果您已经熟悉如何创建块，请参阅文档[使用 Edge Delivery Services 进行所见即所得创作的开发者入门指南](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)，以使用 Edge Delivery Services 和通用编辑器进行内容创作，从而启动并运行新的 Adobe Experience Manager Site。
