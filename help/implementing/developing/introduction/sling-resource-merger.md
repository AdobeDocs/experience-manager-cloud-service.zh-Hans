---
title: 以Adobe Experience Manager中的Sling资源合并为Cloud Service
description: Sling Resource Merager提供访问和合并资源的服务
translation-type: tm+mt
source-git-commit: 1a8a9781da7390d25ec687d46af8d8a976c069bc
workflow-type: tm+mt
source-wordcount: '1241'
ht-degree: 1%

---


# 在AEM中将Sling资源合并作为Cloud Service {#using-the-sling-resource-merger-in-aem}

## 用途 {#purpose}

Sling Resource Merager提供访问和合并资源的服务。 它为以下两者提供差异（差异）机制：

* **[使用](/help/implementing/developing/introduction/overlays.md)**已配置的搜索路[径覆盖资源](/help/implementing/developing/introduction/overlays.md#configuring-the-search-paths)。

* **使用** 资源类型层次结构(通过属性`cq:dialog`)覆盖触屏优化UI()的组件对话框 `sling:resourceSuperType`。

在Sling Resource Merabire中，叠加／覆盖资源和／或属性与原始资源／属性合并：

* 自定义定义的内容的优先级高于原始定义的内容(即，它 *叠加**或覆盖* 它)。

* 在必要时 [](#properties) ，在自定义中定义属性，指示如何使用合并自原始内容的内容。

<!-- Still links to reference material in 6.5 -->

>[!CAUTION]
>
>Sling Resource Merage及相关方法只能与Granite一 [起使用](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)。 这也意味着它仅适用于标准的触屏优化UI; 尤其是，以这种方式定义的重写仅适用于组件的触屏启用对话框。
>
>其他区域（包括触屏支持组件的其他方面）的叠加／覆盖涉及将相应的节点和结构从原始节点复制到定义自定义的位置。

### AEM目标 {#goals-for-aem}

在AEM中使用Sling Resource合并的目标是：

* 确保未在中进行自定义更 `/libs`改。
* 减少从中复制的结构 `/libs`。

   使用Sling Resource Merage时，不建议从中复制整个结构， `/libs` 因为这会导致在自定义中保留过多信息(通常 `/apps`)。 在以任何方式升级系统时，重复信息会不必要地增加出现问题的可能性。

>[!NOTE]
>
>覆盖不取决于搜索路径，它们使用属性 `sling:resourceSuperType` 建立连接。
>
>但是，重写通常在下 `/apps`定义，因为AEM的最佳实践是在下定义自定义 `/apps`; 这是因为你不能改变下面的任何 `/libs`。

>[!CAUTION]
>
>您 ***不得*** 更改路径中的任 `/libs` 何内容。
>
>这是因为下次升级实 `/libs` 例时，内容会被覆盖（而应用修补程序或功能包时，内容很可能会被覆盖）。
>
>建议的配置和其他更改方法是：
>
>1. 在下面重新创建所需的项(即，当它存在 `/libs`时) `/apps`
   >
   >
1. 在 `/apps`
>



### 属性 {#properties}

资源合并提供以下属性：

* `sling:hideProperties` ( `String` 或 `String[]`)

   指定要隐藏的属性或属性列表。

   通配符将 `*` 隐藏全部。

* `sling:hideResource` ( `Boolean`)

   指示资源是否应完全隐藏，包括其子项。

* `sling:hideChildren` ( `String` 或 `String[]`)

   包含要隐藏的子节点或子节点的列表。 将保留节点的属性。

   通配符将 `*` 隐藏全部。

* `sling:orderBefore` ( `String`)

   包含当前节点应位于的前面的同级节点的名称。

这些属性影响叠加／覆盖(通常 `/libs`在中)使用相应／原始资源／属 `/apps`性。

### 创建结构 {#creating-the-structure}

要创建叠加或覆盖，您需要在目标（通常）下重新创建具有等效结构的原始节 `/apps`点。 例如：

* 叠加

   * 如边栏中所示，“站点”控制台的导航条目定义在以下位置：

      `/libs/cq/core/content/nav/sites/jcr:title`

   * 要覆盖此节点，请创建以下节点：

      `/apps/cq/core/content/nav/sites`

      然后根据需要更 `jcr:title` 新属性。

* 覆盖

   * 文本控制台的触屏启用对话框的定义在以下位置进行定义：

      `/libs/foundation/components/text/cq:dialog`

   * 要覆盖此节点，请创建以下节点——例如：

      `/apps/the-project/components/text/cq:dialog`

要创建其中任何一个，您只需重新创建骨架结构。 为了简化结构的重建，所有中间节点都可以是 `nt:unstructured` 类型(它们不需要反映原始节点类型； 例如，在 `/libs`中。

因此，在上面的叠加示例中，需要以下节点：

```shell
/apps
  /cq
    /core
      /content
        /nav
          /sites
```

>[!NOTE]
>
>使用Sling资源合并（即处理标准的触屏优化UI时）时，不建议从中复制整个结构，因为 `/libs` 这会导致信息保留过多 `/apps`。 这可能在系统以任何方式升级时导致问题。

### Use Cases {#use-cases}

这些功能与标准功能相结合，使您能够：

* **添加属性**

   该属性在定义中不存 `/libs` 在，但在叠加／覆盖中 `/apps` 是必需的。

   1. 在中创建相应的节点 `/apps`
   1. 在此节点“”上创建新属性

* **重定义属性（非自动创建的属性）**

   属性在中定 `/libs`义，但叠加／覆盖中需要 `/apps` 一个新值。

   1. 在中创建相应的节点 `/apps`
   1. 在此节点上创建匹配属性(在/ `apps`下)

      * 该属性将基于Sling资源解析程序配置具有优先级。
      * 支持更改属性类型。

         如果您使用的属性类型与中使用的属 `/libs`性类型不同，则将使用您定义的属性类型。
   >[!NOTE]
   >
   >支持更改属性类型。

* **重新定义自动创建的属性**

   默认情况下，自动创建的属性( `jcr:primaryType`如)不受叠加／覆盖的约束，以确保尊重当前位于下的节 `/libs` 点类型。 要实施叠加／覆盖，您必须在中重新创建该节 `/apps`点，请显式隐藏该属性并重新定义它：

   1. 在下面创建相 `/apps` 应的节点 `jcr:primaryType`
   1. 在该节 `sling:hideProperties` 点上创建属性，并将值设置为自动创建属性的属性； 例如， `jcr:primaryType`

      此属性(定义 `/apps`于)现在将优先于 `/libs`

* **重新定义节点及其子节点**

   节点及其子项在中定 `/libs`义，但叠加／覆盖中需要 `/apps` 新配置。

   1. 组合下列操作：

      1. 隐藏节点的子项（保留节点的属性）
      1. 重定义属性／属性

* **隐藏属性**

   属性在中定义， `/libs`但在叠加／覆盖中 `/apps` 不是必需的。

   1. 在中创建相应的节点 `/apps`
   1. 创建或类 `sling:hideProperties` 型的 `String` 属性 `String[]`。 使用它指定要隐藏／忽略的属性。 也可以使用通配符。 例如：

      * `*`
      * `["*"]`
      * `jcr:title`
      * `["jcr:title", "jcr:description"]`

* **隐藏节点及其子节点**

   节点及其子项在中定义， `/libs`但在叠加／覆盖中 `/apps` 不是必需的。

   1. 在/apps下创建相应节点
   1. 创建属性 `sling:hideResource`

      * 类型: `Boolean`
      * value: `true`

* **隐藏节点的子项（同时保留节点的属性）**

   节点、其属性及其子项在中定义 `/libs`。 叠加／覆盖中需要节点及其 `/apps` 属性，但叠加／覆盖中不需要部分或全部子 `/apps` 节点。

   1. 在 `/apps`
   1. 创建属性 `sling:hideChildren`:

      * 类型: `String[]`
      * value: 要隐藏／忽略的子节点的列表( `/libs`如中定义)
      通配符&amp;ast; 可用于隐藏／忽略所有子节点。


* **对节点重新排序**

   节点及其同级在中定义 `/libs`。 需要新位置，因此在叠加／覆盖中重新创建 `/apps` 该节点，其中新位置是在引用中相应的同级节点时定义的 `/libs`。

   * 使用属 `sling:orderBefore` 性：

      1. 在 `/apps`
      1. 创建属性 `sling:orderBefore`:

         这指定了当前节点应 `/libs`在以下位置之前放置的节点（如中所示）:

         * 类型: `String`
         * value: `<before-SiblingName>`

### 从您的代码调用Sling Resource合并 {#invoking-the-sling-resource-merger-from-your-code}

Sling Resource Merager包括两个自定义资源提供商——一个用于叠加，另一个用于覆盖。 可以通过使用装载点在代码中调用其中的每一个：

>[!NOTE]
>
>访问资源时，建议使用相应的装载点。
>
>这可确保调用Sling Resource Mergare并购并并返回完全合并的资源(减少需要从中复制的结构 `/libs`)。

* 叠加:

   * 目的： 根据资源的搜索路径合并资源
   * 装载点： `/mnt/overlay`
   * usage: `mount point + relative path`
   * 示例：

      * `getResource('/mnt/overlay' + '<relative-path-to-resource>');`

* 覆盖：

   * 目的： 根据超类型合并资源
   * 装载点： `/mnt/overide`
   * usage: `mount point + absolute path`
   * 示例：

      * `getResource('/mnt/override' + '<absolute-path-to-resource>');`

<!--
### Example of Usage {#example-of-usage}

Some examples are covered:

* Overlay:

    * [Customizing the Consoles](/help/sites-developing/customizing-consoles-touch.md)
    * [Customizing Page Authoring](/help/sites-developing/customizing-page-authoring-touch.md)

* Override:

    * [Configuring your Page Properties](/help/sites-developing/page-properties-views.md#configuring-your-page-properties)
-->
