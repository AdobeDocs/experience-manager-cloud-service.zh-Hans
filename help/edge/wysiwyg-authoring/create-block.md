---
title: 创建与通用编辑器配合使用的块
description: 了解如何在使用 Edge Delivery Services 项目进行的所见即所得创作中创建可与通用编辑器配合使用的块。
exl-id: 65a5600a-8d16-4943-b3cd-fe2eee1b4abf
feature: Edge Delivery Services
role: Admin, Architect, Developer
source-git-commit: 7f54d2ee61d2b92e7a0f02c66ce8ee5cdbedd73c
workflow-type: tm+mt
source-wordcount: '1415'
ht-degree: 96%

---


# 创建与通用编辑器配合使用的块 {#create-block}

了解如何在使用 Edge Delivery Services 项目进行的所见即所得创作中创建可与通用编辑器配合使用的块。

## 先决条件 {#prerequisites}

本指南提供了如何在使用 Edge Delivery Services 项目进行的所见即所得创作中创建可与通用编辑器配合使用的块的分步说明。它包括添加组件、在 Universal Editor 中加载组件定义、发布页面、实施块装饰和样式、将更改引入生产环境以及验证更改。完成本指南后，您可以为自己的项目创建和部署新块。

本指南要求读者必须具备使用 Edge Delivery Services 项目进行所见即所得创作以及通用编辑器方面的基础知识。在开始阅读本指南之前，您应有权访问 Edge Delivery Services 并熟悉其基础知识，其中包括：

* 您已学完 [Edge Delivery Services 教程](/help/edge/developer/tutorial.md)。
* 您有权访问 [AEM Cloud Service 沙盒](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md)。
* 您已[启用同一沙盒环境上的 Universal Editor](/help/implementing/universal-editor/getting-started.md)。
* 您已经完成了[使用 Edge Delivery Services 进行所见即所得创作的开发人员快速入门指南](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)。

本指南基于[使用 Edge Delivery Services 进行所见即所得创作的开发人员快速入门指南](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)中所完成的内容。

## 向项目添加新块 {#add-block}

在本指南中，您将构建一个块来在页面上呈现令人难忘的引用。

为了简化此示例，所有更改都针对项目存储库的 `main` 分支进行。当然，对于您的实际项目，[您应遵循开发最佳实践](https://www.aem.live/docs/dev-collab-and-good-practices)，在不同的分支上进行开发，并在合并到 `main` 之前通过拉取请求检查所有更改。

Adobe 建议您采用三阶段方法来开发块：

1. 为块创建定义和模型，对其进行审查，然后将其投入生产。
1. 使用新块创建内容。
1. 实施新块的装饰和样式。

以下引用块示例遵循此方法。

### 创建块定义和模型 {#create-block-model}

1\. 在本地克隆您在[使用 Edge Delivery Services 进行所见即所得创作的开发人员快速入门指南](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)中创建的 GitHub 项目，并使用您选择的编辑器打开它。

* 此处使用的 Microsoft Code 用于说明目的。

![克隆项目](assets/create-block/clone.png)

2\. 编辑项目根目录中的[`component-definition.json`文件](/help/implementing/universal-editor/component-definition.md)，并为新报价块添加以下定义并保存文件。

>[!BEGINTABS]

>[!TAB JSON 示例]

```json
{
  "title": "Quote",
  "id": "quote",
  "plugins": {
    "xwalk": {
      "page": {
        "resourceType": "core/franklin/components/block/v1/block",
        "template": {
          "name": "Quote",
          "model": "quote",
          "quote": "<p>Think, McFly! Think!</p>",
          "author": "Biff Tannen"
        }
      }
    }
  }
}
```

>[!TAB 屏幕快照]

![编辑 component-definitions.json 文件以定义引用块](assets/create-block/component-definitions.png)

>[!ENDTABS]

3\. 编辑项目的根目录下的 `component-models.json` 文件，为新的引用块添加以下[模型定义](/help/implementing/universal-editor/field-types.md#model-structure)并保存该文件。

* 请参阅文档[使用 Edge Delivery Services 项目进行所见即所得创作的内容建模](/help/edge/wysiwyg-authoring/content-modeling.md)，以获取更多关于创建内容模型时需要考虑的重要事项的信息。

>[!BEGINTABS]

>[!TAB JSON 示例]

```json
{
  "id": "quote",
  "fields": [
     {
       "component": "richtext",
       "name": "quote",
       "value": "",
       "label": "Quote",
       "valueType": "string"
     },
     {
       "component": "text",
       "valueType": "string",
       "name": "author",
       "label": "Author",
       "value": ""
     }
   ]
}
```

>[!TAB 屏幕快照]

![编辑 component-models.json 文件以定义引用块的模型](assets/create-block/component-models.png)

>[!ENDTABS]

4\. 编辑项目根目录中的[`component-filters.json`文件](/help/implementing/universal-editor/customizing.md#filtering-components)，并将引用块添加到[筛选器定义](/help/implementing/universal-editor/customizing.md#filtering-components)中，以允许将该块添加到任何部分并保存该文件。

>[!BEGINTABS]

>[!TAB JSON 示例]

```json
{
  "id": "section",
  "components": [
    "text",
    "image",
    "button",
    "title",
    "hero",
    "cards",
    "columns",
    "quote"
   ]
}
```

>[!TAB 屏幕快照]

![编辑 component-filters.json 文件以定义引用块的过滤器](assets/create-block/component-filters.png)

>[!ENDTABS]

5\. 使用 git 将这些更改提交到 `main` 分支。

* 提交到 `main` 仅用于说明目的。[遵循最佳实践](https://www.aem.live/docs/dev-collab-and-good-practices)，并对实际项目工作使用拉取请求。

### 使用块创建内容 {#create-content}

现在，已定义您的基本引用块并将其提交到示例项目，您可以将引用块添加到现有页面。

1. 在浏览器中，登录到 AEM as a Cloud Service。[使用 Sites 控制台，](/help/sites-cloud/authoring/basic-handling.md)导航到您在[使用 Edge Delivery Services 进行所见即所得创作的开发人员快速入门指南](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)中创建的网站，并选择一个页面。

   * 在此示例中，`index` 用于说明目的。

   ![在 Sites 控制台中选择索引页面](assets/create-block/sites-console.png)

1. 点击或单击控制台工具栏中的&#x200B;**编辑**，Universal Editor 随即打开。

   * 为了加载该页面，您可能需要点击或单击&#x200B;**使用 Adobe 登录**&#x200B;以在 Universal Editor 中向 AEM 进行身份验证。

1. 在 Universal Editor 中，选择一个部分。在属性面板中，点击或单击&#x200B;**添加**&#x200B;图标，然后从菜单中选择新的&#x200B;**引用**&#x200B;块。

   * **添加**&#x200B;图标是一个加号。
   * 如果所选对象的蓝色轮廓有一个标记为&#x200B;**部分**&#x200B;的选项卡，则表明您已选择一个部分。
   * 在此示例中，点击或单击 **Lorem Ipsum** 标题的略上位置可选择包含标题和 lorem ipsum 文本的部分。

   ![在 Universal Editor 中选择一个部分](assets/create-block/add-quote-block.png)

1. 页面将重新加载，引用块将与 `component-definitions.json` 文件中指定的默认内容一起添加到所选部分的底部。

   * 可以像任何其他块一样，就地或在属性面板中选择和编辑引用块。
   * 将在下一步中应用样式。

   ![所选部分中包含新引用块的页面](assets/create-block/quote-added.png)

1. 一旦您对引用内容感到满意，可以通过点击或单击 Universal Editor 工具栏中的&#x200B;**发布**&#x200B;按钮来发布页面。

1. 通过导航到已发布的页面来验证是否已发布内容。该链接将类似于 `https://<branch>--<repo>--<owner>.aem.page`

   ![已发布的引用](assets/create-block/quote-published.png)

### 设置块的样式 {#style-block}

现在，您已使用一个可对其应用样式的引用块。

1\. 返回到您项目的编辑器。

2\. 在 `blocks` 文件夹下创建一个 `quote` 文件夹。

![创建引用文件夹](assets/create-block/new-folder.png)

3\. 在新的 `quote` 文件夹中，添加一个 `quote.js` 文件以通过添加以下 JavaScript 来实施块装饰，然后保存该文件。

>[!BEGINTABS]

>[!TAB JavaScript 示例]

```javascript
export default function decorate(block) {
  const [quoteWrapper] = block.children;
 
  const blockquote = document.createElement('blockquote');
  blockquote.textContent = quoteWrapper.textContent.trim();
  quoteWrapper.replaceChildren(blockquote);
}
```

>[!TAB 屏幕快照]

![添加 JavaScript 以装饰块](assets/create-block/quote-js.png)

>[!ENDTABS]

4\. 在 `quote` 文件夹中，添加一个 `quote.css` 文件以通过添加以下 CSS 代码来定义块的样式，然后保存该文件。

>[!BEGINTABS]

>[!TAB CSS 示例]

```css
.block.quote {
    background-color: #ccc;
    padding: 0 0 24px;
    display: flex;
    flex-direction: column;
    margin: 1rem 0;
}
 
.block.quote blockquote {
    margin: 16px;
    text-indent: 0;
}
 
.block.quote > div:last-child > div {
    margin: 0 16px;
    font-size: small;
    font-style: italic;
    position: relative;
}
 
.block.quote > div:last-child > div::after {
    content: "";
    display: block;
    position: absolute;
    left: 0;
    bottom: -8px;
    height: 5px;
    width: 30px;
    background-color: darkgray;
}
```

>[!TAB 屏幕快照]

![添加 CSS 以定义块样式](assets/create-block/quote-css.png)

>[!ENDTABS]

5\. 使用 git 将这些更改提交到 `main` 分支。

* 提交到 `main` 仅用于说明目的。[遵循最佳实践](https://www.aem.live/docs/dev-collab-and-good-practices)，并对实际项目工作使用拉取请求。

6\. 返回到您正在编辑项目页面的通用编辑器浏览器选项卡，并重新加载页面以查看您已设置样式的块。

7\. 请参阅页面上的样式化引用块。

![Universal Editor 中的样式化引用块](assets/create-block/quote-styled.png)

8\. 通过导航到已发布的页面来验证更改是否已推送到生产环境。该链接将类似于 `https://<branch>--<repo>--<owner>.aem.page`

![已发布的样式化引用块](assets/create-block/quote-styled-published.png)

恭喜！您现在拥有一个完全工作的样式化引用块。您可以使用此示例作为设计您自己的项目特定块的基础。

### 阻止选项 {#block-options}

如果您需要一个块根据特定情况看起来或表现得略有不同，但这种不同不足以使其成为一个新的块，您可以让作者从[块选项](content-modeling.md#type-inference)中进行选择。

通过向块添加 `classes` 属性，该属性会在简单块的表头中呈现，或在容器块中的项目上作为值列表呈现。

```json
{
  "id": "simpleMarquee",
  "fields": [
    {
      "component": "text",
      "valueType": "string",
      "name": "marqueeText",
      "value": "",
      "label": "Marquee text",
      "description": "The text you want shown in your marquee"
    },
    {
      "component": "select",
      "name": "classes",
      "value": "",
      "label": "Background Color",
      "description": "The marquee background color",
      "valueType": "string",
      "options": [
        {
          "name": "Red",
          "value": "bg-red"
        },
        {
          "name": "Green",
          "value": "bg-green"
        },
        {
          "name": "Blue",
          "value": "bg-blue"
        }
      ]
    }
  ]
}
```

## 使用其他工作分支 {#other-branches}

为简单起见，本指南要求您直接提交到 `main`。对于示例存储库中的试验，这通常不是问题。对于实际项目工作，[您应遵循开发最佳实践](https://www.aem.live/docs/dev-collab-and-good-practices)，在不同的分支上进行开发，并在合并到 `main` 之前通过拉取请求检查所有更改。

当您未在 `main` 分支上进行开发时，可以在 Universal Editor 位置栏中追加 `?ref=<branch>` 以从分支加载页面。`<branch>` 是分支名称，因为它将用于项目的预览或实时 URL，例如 `https://<branch>--<repo>--<owner>.aem.page`。

## 重用块进行基于文档的创作 {#reusing-blocks}

如果您遵循相同的内容模型，您可以使用通用编辑器为所见即所得创作创建的块进行基于文档的创作。

请参阅文档[用于所见即所得和基于文档的创作的块](/help/edge/wysiwyg-authoring/wysiwyg-doc-blocks.md)，了解更多信息。

## 后续步骤 {#next-steps}

现在您知道了如何创建块，接下来，了解如何以语义的方式对内容进行建模以实现精益的开发人员体验至关重要。

请参阅文档[使用 Edge Delivery Services 项目进行所见即所得创作的内容建模](/help/edge/wysiwyg-authoring/content-modeling.md)，了解使用 Edge Delivery Services 项目进行所见即所得创作的内容建模的工作原理。

>[!TIP]
>
>有关创建新的 Edge Delivery Services 项目的端到端演练，该项目支持使用 AEM as a Cloud Service 作为内容源进行所见即所得创作，请查看[该 AEM GEM 网络研讨会。](https://experienceleague.adobe.com/zh-hans/docs/events/experience-manager-gems-recordings/gems2024/aem-authoring-and-edge-delivery)
