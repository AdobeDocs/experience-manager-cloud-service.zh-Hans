---
title: 组件定义
description: 详细了解组件定义与通用编辑器之间的 JSON 契约。
feature: Developing
role: Admin, Architect, Developer
exl-id: e1bb1a54-50c0-412a-a8fd-8167c6f47d2b
source-git-commit: b4e61ec6abcaf73119f8963d72317759b2bd7c76
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 96%

---

# 组件定义 {#component-definition}

详细了解组件定义与通用编辑器之间的 JSON 契约。

## 概述 {#overview}

`component-definition.json` 文件定义了项目的内容作者可用的组件。本文档详细介绍了此文件的用途以及通用编辑器如何使用它向作者展示页面创作组件。

>[!TIP]
>
>有关内容建模过程的概述，请参阅文档[使用 Edge Delivery Services 项目进行所见即所得创作的内容建模。](https://www.aem.live/developer/component-model-definitions)

>[!TIP]
>
>您不需要从头开始创建自己的 `component-definition.json` 文件。您用于[引导项目](https://www.aem.live/developer/ue-tutorial)的项目样板中包含一个[完全正常工作的 `component-definition.json` 文件](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/component-definition.json)，您可以根据需要对其进行调整。

## 组件定义示例 {#example}

下面是一个完整而简单的 `component-definition.json` 示例。

```json
{
  "groups":[
    {
      "title":"General Components",
      "id":"general",
      "components":[
        {
          "title":"Text",
          "id":"text",
          "model": "text",
          "filter": "texts",
          "plugins":{
            "aem":{
              "page":{
                "resourceType":"wknd/components/text",
                "template":{
                  "text":"Default Text",
                  "name":"Text"
                }
              }
            },
            "aem65":{
              "page":{
                "resourceType":"wknd/components/text",
                "template":{
                  "text":"Default Text",
                  "name":"Text"
                }
              }
            }
          }
        }
      ]
    }
  ]
}
```

## `groups` {#groups}

`groups` 定义了当作者点击编辑器属性面板中的&#x200B;**添加**&#x200B;图标以[在页面中添加新组件](/help/sites-cloud/authoring/universal-editor/authoring.md#adding-components)时，在通用编辑器中看到的组件组。组有助于组织组件。常用的组包括&#x200B;**一般组件**&#x200B;和&#x200B;**高级组件**。

* `title` 定义了编辑器 UI 中显示的组的文字描述。
* `id` 是组的唯一标识。

## `components` {#components}

`components` 定义了哪些组件属于某个组。

* `title` 定义了 UI 中显示的组件的文字描述。
* `id` 是组件的唯一标识。
   * 相同 `id` 的[组件模型](/help/implementing/universal-editor/field-types.md#model-structure)定义了组件的字段。  
   * 因为它是唯一的，所以可用在例如[过滤器定义](/help/implementing/universal-editor/filtering.md)中，以确定哪些组件可以添加到容器中。
* `model` 定义了哪个[模型](/help/implementing/universal-editor/field-types.md#model-structure)与组件一起使用。
   * 此模型在组件定义中集中维护，无需被[指定适配。](/help/implementing/universal-editor/field-types.md#instrumentation)
   * 这样您就能跨容器移动组件。
* `filter` 定义了哪个[过滤器](/help/implementing/universal-editor/filtering.md)应与组件一起使用。

## `plugins` {#plugins}

`plugins` 定义了哪个插件负责保留组件。常用的插件有：

* `aem`AEM as a Cloud Service的[。](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service)
* `aem65`AEM 6.5.[和](https://experienceleague.adobe.com/en/docs/experience-manager-65)AEM 6.5 LTS[的](https://experienceleague.adobe.com/en/docs/experience-manager-65-lts)
* 使用AEM Sites为Edge Delivery Services创作`xwalk`的[。](https://www.aem.live/developer/ue-tutorial)

## `page` 或 `cf` {#page-cf}

定义了 `plugin` 之后，您需要指明它是与页面相关还是与片段相关。

* `page` 表示该组件是当前页面上的内容。
* `cf` 表示该组件与一个[内容片段](/help/assets/content-fragments/content-fragments.md)中的内容相关。

### `page` {#page}

如果组件是页面上的内容，您可以提供以下信息。

* `resourceType` 定义了用于渲染组件的 [Sling](/help/implementing/developing/introduction/sling-cheatsheet.md) `resourceType`。
* `template` 定义了要自动写入新创建的组件的可选键/值，还定义了应将哪个过滤器和/或模型应用于该组件。
   * 适用于解释性文本、示例文本或占位符文本。

#### `template` {#template}

通过提供可选的键/值对，`template` 可以将这些自动写入新组件。此外，还可以指定以下可选值。

### `cf` {#cf}

如果组件与一个内容片段中的内容相关，您可以提供以下信息。

* `name` 为新创建的组件定义了一个保存到 JCR 的可选名称。
   * 仅供参考，通常不会在 UI 中按 `title` 原样显示。
* `cfModel` 为新创建的组件定义[内容片段](/help/assets/content-fragments/content-fragments-models.md)模型。
* `cfFolder` 定义了应在哪个文件夹中创建内容片段。
* `title` 定义了新内容片段的标题。
* `description` 定义了新内容片段的描述。
* `template` 定义了被自动写入新创建的内容片段的可选键/值。
   * 适用于解释性文本、示例文本或占位符文本。

### `cf` 可以被隐含 {#cf-implied}

如果页面被[适配](/help/implementing/universal-editor/getting-started.md#instrument-page)指向一个引用字段，就会认为是 `cf`。

```html
<div data-aue-resource="urn:aem:/content" data-aue-type="container" data-aue-prop="field"></div>
```

在这种情况下认为是 `cf`，因为 `data-aue-prop` 指向一个引用字段。如果没有 `data-aue-prop`，通用编辑器就会认为是 `page`，因为在这种情况下组件不是通过引用字段关联。

```html
<div data-aue-resource="urn:aem:/content" data-aue-type="container"></div>
```

组件只是资源下方的子节点。
