---
title: 自定义控制台
description: 了解AEM为自定义创作实例的控制台提供的各种选项。
source-git-commit: f159f0ef86c2b82da4e7308a0892b4947b6e43fb
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---


# 自定义控制台 {#customizing-consoles}

AEM提供了用于自定义控制台(以及 [页面创作功能](/help/implementing/developing/extending/page-authoring.md))。

## Clientlibs {#clientlibs}

Clientlibs允许您扩展默认实施以提供新功能，同时重用标准函数、对象和方法。 使用clientlibs进行自定义时，您可以在下面创建自己的clientlib `/apps.` 例如，它可以保存自定义组件所需的代码。

有关clientlibs的更多详细信息，请参阅文档 [在AEMas a Cloud Service上使用客户端库。](/help/implementing/developing/introduction/clientlibs.md)

## 叠加 {#overlays}

叠加基于节点定义，允许您叠加下的标准功能 `/libs` 下有您自己的自定义功能 `/apps`. 创建叠加时，不需要原始的1:1副本，如 [Sling资源合并器](/help/implementing/developing/introduction/sling-resource-merger.md) 允许继承。

叠加可以以多种方式用于扩展AEM控制台。 以下部分提供了几个示例。

有关叠加的详细信息，请参阅文档 [Adobe Experience Manager as a Cloud Service的叠加。](/help/implementing/developing/introduction/overlays.md)

>[!TIP]
>
>如果您对用于自定义创作体验的选项感兴趣，请参阅文档 [自定义页面创作。](/help/implementing/developing/extending/page-authoring.md)

## 自定义控制台的默认视图 {#customizing-the-default-view-for-a-console}

您可以自定义控制台的默认视图（列、卡片、列表）：

* 可通过覆盖下列项下的所需条目来重新排序视图：

   * `/libs/wcm/core/content/sites/jcr:content/views`

   * 第一个条目是默认条目。

   * 可用的节点与可用的视图选项相关联：

      * `column`
      * `card`
      * `list`

* 例如，在列表的覆盖中：

   * `/apps/wcm/core/content/sites/jcr:content/views/list`

   * 定义以下属性：

      * **名称**: `sling:orderBefore`
      * **类型**： `String`
      * **值**: `column`

### 向工具栏添加新操作 {#add-a-new-action-to-the-toolbar}

您可以构建自己的组件，并为自定义操作包含相应的客户端库。

* 例如，您可能要创建 **提升至社交媒体** 操作位置：

   * `/apps/wcm/core/clientlibs/sites/js/socialmedia.js`

   * 然后，可以将其连接到控制台上的工具栏项目：

   * `/apps/<yourProject>/admin/ext/launches`

   * 例如，在选择模式中：

   * `content/jcr:content/body/content/header/items/selection/items/socialmedia`

### 将工具栏操作限制为特定组 {#restrict-a-toolbar-action-to-a-specific-group}

您可以使用自定义渲染条件来叠加标准操作并施加在渲染之前必须满足的特定条件。

例如，您可能要创建组件以根据组控制渲染条件：

* `/apps/myapp/components/renderconditions/group`

要将这些应用于 **创建站点** 站点控制台上的操作：

* `/libs/wcm/core/content/sites`

1. 创建叠加：

   * `/apps/wcm/core/content/sites`

1. 然后，为操作添加渲染条件：

   * `jcr:content/body/content/header/items/default/items/create/items/createsite/rendercondition`

使用此节点上的属性，您可以定义 `groups` 允许执行特定操作；例如， `administrators`

### 在列表视图中自定义列 {#customizing-columns-in-list-view}

要自定义列表视图中的列，请执行以下操作：

1. 覆盖可用列的列表。

   * 在节点上：

     `/apps/wcm/core/content/common/availablecolumns`

1. 添加新列或删除现有列。

如果要插入附加数据，则需要编写 [PageInfoProvider](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/PageInfoProvider.html) 带有 `pageInfoProviderType` 属性。

>[!NOTE]
>
>此功能已针对文本字段列进行优化。 对于其他数据类型，可以叠加 `cq/gui/components/siteadmin/admin/listview/columns/analyticscolumnrenderer` 在 `/apps`.

### 筛选资源 {#filtering-resources}

使用控制台时，用户通常必须从页面、组件或资产等资源中进行选择。 这可以采用列表形式，作者必须从该列表中选择项目。

为了使列表保持合理的大小并且与用例相关，可以采用自定义谓词的形式实施过滤器。 请参阅文档[自定义页面创作](/help/implementing/developing/extending/page-authoring.md#filtering-resources) 以了解详细信息。
