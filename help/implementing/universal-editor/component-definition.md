---
title: 组件定义
description: 详细了解组件定义与通用编辑器之间的JSON约定。
feature: Developing
role: Admin, Architect, Developer
exl-id: e1bb1a54-50c0-412a-a8fd-8167c6f47d2b
source-git-commit: 384f8a1301ea488e0b2aa493389d090896fe3b33
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 1%

---

# 组件定义 {#component-definition}

详细了解组件定义与通用编辑器之间的JSON约定。

## 概述 {#overview}

`component-definition.json`文件定义了项目内容作者可用的组件。 本文档详细介绍此文件的用途以及通用编辑器如何使用它向作者展示页面创作组件。

>[!TIP]
>
>有关内容建模过程的概述，请参阅文档[使用Edge Delivery Services项目进行WYSIWYG创作的内容建模。](/help/edge/wysiwyg-authoring/content-modeling.md)

>[!TIP]
>
>您不需要从头开始创建自己的`component-definition.json`文件。 您用于[引导项目](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)的项目样板包含一个[功能齐全的`component-definition.json`文件](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/component-definition.json)，您可以根据自己的需求对其进行调整。

## 示例组件定义 {#example}

以下是一个完整但简单的`component-definition.json`示例。

```json
{
  "groups": [
    {
      "title": "General Components",
      "id": "general",
      "components": [
        {
          "title": "Text",
          "id": "text",
          "plugins": {
            "aem": {
              "page": {
                "resourceType": "wknd/components/text",
                "template": {
                  "text": "Default Text"
                }
              }
            },
            "aem65": {
              "page": {
                "resourceType": "wknd/components/text",
                "template": {
                  "text": "Default Text"
                }
              }
            }
          }
        },
      }
   ]
}
```

## `groups` {#groups}

`groups`定义作者在通用编辑器中看到的组件组，在编辑器的属性面板中单击&#x200B;**添加**&#x200B;图标可将新组件[添加到页面时，该组件组位于编辑器中。](/help/sites-cloud/authoring/universal-editor/authoring.md#adding-components)组帮助组织组件。 公共组可能是&#x200B;**常规组件**&#x200B;和&#x200B;**高级组件**。

* `title`定义编辑器UI中显示的组的文本说明。
* `id`唯一标识该组。

## `components` {#components}

`components`定义哪些组件属于组。

* `title`定义UI中显示的组件的文本说明。
* `id`唯一标识该组件。
   * 同一`id`的[组件模型](/help/implementing/universal-editor/field-types.md#model-structure)定义了组件的字段。
   * 由于它是唯一的，因此例如可在[筛选器定义](/help/implementing/universal-editor/filtering.md)中使用它来确定可将哪些组件添加到容器中。

## `plugins` {#plugins}

`plugins`定义哪个插件负责持久化该组件。 常用插件包括：

* AEM as a Cloud Service的`aem`。
* 适用于AEM 6.5的`aem5`。
* 用于AEM as a Cloud Service WYSIWYG创作的`xwalk`。

## `page` 或 `cf` {#page-cf}

定义`plugin`后，您需要指示它是与页面相关还是与片段相关。

* `page`指示组件在当前页面上为内容。
* `cf`指示组件与[内容片段中的内容相关。](/help/assets/content-fragments/content-fragments.md)

### `page` {#page}

如果组件是页面上的内容，您可以提供以下信息。

* `name`为新创建的组件定义保存到JCR的可选名称。
   * 仅供参考，通常不会在UI中显示为`title`。
* `resourceType`定义用于呈现组件的[Sling](/help/implementing/developing/introduction/sling-cheatsheet.md) `resourceType`。
* `template`定义要自动写入新创建组件的可选键/值。
   * 用于说明性文本、示例文本或占位符文本。

### `cf` {#cf}

如果组件与内容片段中的内容相关，您可以提供以下信息。

* `name`为新创建的组件定义保存到JCR的可选名称。
   * 仅供参考，通常不会在UI中显示为`title`。
* `cfModel`为新创建的组件定义[内容片段](/help/assets/content-fragments/content-fragments-models.md)模型。
* `cfFolder`定义将在哪个文件夹中创建内容片段。
* `title`定义新内容片段的标题。
* `description`定义新内容片段的描述。
* `template`定义了要自动写入新创建的内容片段的可选键/值。
   * 用于说明性文本、示例文本或占位符文本。

### `cf`可以默示 {#cf-implied}

如果页面[检测为](/help/implementing/universal-editor/getting-started.md#instrument-page)以指向引用字段，则将假定为`cf`。

```html
<div data-aue-resource="urn:aem:/content" data-aue-type="container" data-aue-prop="field"></div>
```

在这种情况下，假定为`cf`，因为`data-aue-prop`指向参考字段。 如果没有`data-aue-prop`，通用编辑器将采用`page`，因为在这种情况下，组件不通过引用字段链接。

```html
<div data-aue-resource="urn:aem:/content" data-aue-type="container"></div>
```

组件只是资源下的子节点。
