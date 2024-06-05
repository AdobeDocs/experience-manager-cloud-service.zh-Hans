---
title: 自定义控制台
description: 了解 AEM 提供的用于自定义创作实例控制台的不同选项。
exl-id: 832f9a86-07c4-4229-a0dc-8ad50a8195b0
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 87%

---

# 自定义控制台 {#customizing-consoles}

AEM 提供了自定义创作实例控制台（以及[页面创作功能](/help/implementing/developing/extending/page-authoring.md)）的选项。

## Clientlibs {#clientlibs}

Clientlib 允许您扩展默认实现，以提供新功能，同时重新使用标准函数、对象和方法。使用clientlibs进行自定义时，您可以在下面创建自己的clientlib `/apps.` 例如，它可以保存自定义组件所需的代码。

请参阅 [在AEMas a Cloud Service上使用客户端库](/help/implementing/developing/introduction/clientlibs.md).

## 叠加 {#overlays}

叠加基于节点定义，允许您将 `/libs` 下的标准功能与 `/apps` 下的自定义功能叠加。创建叠加时，不需要原件的 1:1 副本，因为[ Sling 资源合并器](/help/implementing/developing/introduction/sling-resource-merger.md)允许继承。

可以通过多种方式使用叠加来扩展您的 AEM 控制台。以下部分提供了几个示例。

另请参阅 [Adobe Experience Manager as a Cloud Service的叠加](/help/implementing/developing/introduction/overlays.md).

>[!TIP]
>
>如果您对用于自定义创作体验的选项感兴趣，请参阅 [自定义页面创作](/help/implementing/developing/extending/page-authoring.md).

## 自定义控制台的默认视图 {#customizing-the-default-view-for-a-console}

您可以自定义控制台的默认视图（列、信息卡、列表）：

* 您可以通过将所需条目叠加在以下位置来重新对视图排序：

   * `/libs/wcm/core/content/sites/jcr:content/views`

   * 第一个条目是默认条目。

   * 可用的节点与可用的视图选项相关：

      * `column`
      * `card`
      * `list`

* 例如，在列表的叠加层中：

   * `/apps/wcm/core/content/sites/jcr:content/views/list`

   * 定义下列属性：

      * **名称**：`sling:orderBefore`
      * **类型**：`String`
      * **值**：`column`

### 将新的操作添加到工具栏 {#add-a-new-action-to-the-toolbar}

您可以构建自己的组件并包含用于自定义操作的相应客户端库。

* 例如，您可能想要创建一个&#x200B;**推广到社交媒体**&#x200B;操作：

   * `/apps/wcm/core/clientlibs/sites/js/socialmedia.js`

   * 然后可以将其连接到控制台上的工具栏项：

   * `/apps/<yourProject>/admin/ext/launches`

   * 例如，在选择模式下：

   * `content/jcr:content/body/content/header/items/selection/items/socialmedia`

### 将工具栏操作限制为特定组 {#restrict-a-toolbar-action-to-a-specific-group}

您可以使用自定义呈现条件来叠加标准操作，并施加在呈现它之前必须满足的特定条件。

例如，您可能想要创建一个组件来根据组控制呈现条件：

* `/apps/myapp/components/renderconditions/group`

要将这些应用到站点控制台上的&#x200B;**创建站点**&#x200B;操作：

* `/libs/wcm/core/content/sites`

1. 创建叠加：

   * `/apps/wcm/core/content/sites`

1. 然后添加动作的呈现条件：

   * `jcr:content/body/content/header/items/default/items/create/items/createsite/rendercondition`

使用此节点上的属性，您可以定义`groups`允许执行特定操作；例如，`administrators`

### 列表视图中的自定义列 {#customizing-columns-in-list-view}

要自定义列表视图中的列：

1. 叠加可用列的列表。

   * 在节点上：

     `/apps/wcm/core/content/common/availablecolumns`

1. 添加新列或删除现有列。

如果你想插入额外的数据，您需要编写一个具有 `pageInfoProviderType` 属性的 [PageInfoProvider](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/PageInfoProvider.html)。

>[!NOTE]
>
>此功能针对文本字段列进行了优化。对于其他数据类型，可以在 `/apps` 中叠加 `cq/gui/components/siteadmin/admin/listview/columns/analyticscolumnrenderer`。

### 筛选资源 {#filtering-resources}

使用控制台时，用户通常必须从页面、组件或资源等资源中进行选择。这可以采用列表的形式，作者必须从中选择一个项目。

为了使列表保持合理的大小并且与用例相关，可以通过自定义谓词的形式实施筛选条件。请参阅 [自定义页面创作](/help/implementing/developing/extending/page-authoring.md#filtering-resources) 以了解详细信息。
