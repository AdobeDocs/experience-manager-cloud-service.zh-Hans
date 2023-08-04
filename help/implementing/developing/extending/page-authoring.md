---
title: 自定义页面创作
description: 了解AEMas a Cloud Service为自定义页面创作功能提供的机制。
source-git-commit: f159f0ef86c2b82da4e7308a0892b4947b6e43fb
workflow-type: tm+mt
source-wordcount: '981'
ht-degree: 2%

---


# 自定义页面创作 {#customizing-page-authoring}

Adobe Experience Manager as a Cloud Service提供了一些机制，可让您自定义页面创作功能(以及 [控制台](/help/implementing/developing/extending/consoles.md))。

## Clientlibs {#clientlibs}

Clientlibs允许您扩展默认实施以启用新功能，同时重用标准函数、对象和方法。

进行自定义时，您可以在下面创建自己的clientlib `/apps.` 新clientlib必须：

* 取决于创作clientlib `cq.authoring.editor.sites.page`.
* 属于适当的 `cq.authoring.editor.sites.page.hook` 类别。

有关clientlibs的更多详细信息，请参阅文档 [在AEMas a Cloud Service上使用客户端库。](/help/implementing/developing/introduction/clientlibs.md)

## 叠加 {#overlays}

叠加基于节点定义，允许您叠加中的标准功能 `/libs` 在中使用您自己的自定义功能 `/apps`.

创建叠加时，不需要原稿的1:1副本，因为 [sling资源合并器](/help/implementing/developing/introduction/sling-resource-merger.md) 允许继承。

欲知更多信息，请参见 [JS文档集](https://developer.adobe.com/experience-manager/reference-materials/6-5/jsdoc/ui-touch/editor-core/index.html).

有关叠加的详细信息，请参阅文档 [Adobe Experience Manager as a Cloud Service的叠加。](/help/implementing/developing/introduction/overlays.md)

## 添加新图层（模式） {#add-new-layer-mode}

在编辑页面时，有各种 [模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) 可用。 这些模式通过以下方式实现 [图层](/help/implementing/developing/introduction/ui-structure.md#layer). 这些功能允许对同一页面内容访问不同类型的功能。 标准AEM模式包括“编辑”、“布局”、“开发人员”、“时间扭曲”、“Live Copy状态”和“定位”。

### 层示例：Live Copy状态 {#layer-example-live-copy-status}

标准AEM实例提供MSM层。 这将访问与以下对象相关的数据： [多站点管理](/help/sites-cloud/administering/msm/overview.md) 并在图层中将它突出显示。

要查看其实际操作情况，您可以编辑 [WKND示例内容](/help/implementing/developing/introduction/develop-wknd-tutorial.md) 并选择 **Live Copy状态** 模式。

可以在以下位置找到MSM层定义（供参考）：

`/libs/wcm/msm/content/touch-ui/authoring/editor/js/msm.Layer.js`

### 代码示例 {#code-sample}

这是一个示例包，显示如何为MSM视图创建层（模式）。

您可以在此页面中找到代码： [GitHub。](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode)

## 将新的选择类别添加到资产浏览器 {#add-new-selection-category-to-asset-browser}

资产浏览器显示各种类型/类别的资产（例如图像和文档）。 资源也可以按这些资源类别进行筛选。

### 代码示例 {#code-sample-1}

`aem-authoring-extension-assetfinder-flickr` 是一个示例包，显示如何将组添加到资产查找器。 此示例连接到 [闪烁](https://www.flickr.com)的公开流，并在侧面板中显示它们。

您可以在此页面中找到代码： [GitHub。](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr)

## 筛选资源 {#filtering-resources}

创作页面时，用户通常必须从列表中的资源中进行选择。

要使列表保持合理的大小并与用例相关，可以采用自定义谓词的形式实施过滤器。 例如，如果 `pathbrowser` Granite组件用于允许用户选择特定资源的路径，提供的路径可通过以下方式进行过滤：

* 通过实施自定义谓词 [`com.day.cq.commons.predicate.AbstractNodePredicate`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/predicate/package-summary.html) 界面。
* 指定谓词的名称，并在使用 `pathbrowser`.

有关创建自定义谓词的更多详细信息，请参阅 [本文。](/help/implementing/developing/introduction/query-builder-custom-predicate.md)

## 将新操作添加到组件工具栏 {#add-new-action-to-a-component-toolbar}

每个组件通常都有一个工具栏，通过该工具栏可访问可对该组件执行的一系列操作。

### 代码示例 {#code-sample-2}

`aem-authoring-extension-toolbar-screenshot` 是一个示例包，显示如何创建自定义工具栏操作以呈现组件。

您可以在此页面中找到代码： [GitHub。](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot)

## 添加新的就地编辑器 {#add-new-in-place-editor}

### 标准就地编辑器 {#standard-in-place-editor}

在标准 AEM 安装中：

1. `/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js` 包含各种可用编辑器的定义。

1. 编辑器和每个可以使用它的资源类型（组件中为）之间存在一个连接：

   * `cq:inplaceEditing`

     例如：

      * `/libs/foundation/components/text/cq:editConfig`
      * `/libs/foundation/components/image/cq:editConfig`

         * 属性: `editorType`

           定义当为该组件触发就地编辑时使用的内联编辑器类型；例如， `text`， `textimage`， `image`， `title`.

1. 可以使用配置编辑器的其他配置详细信息 `config` 包含配置和 `plugin` 节点，以包含必要的插件配置详细信息。


以下是为图像组件的图像裁剪插件定义长宽比的示例。

```xml
   <cq:inplaceEditing
           jcr:primaryType="cq:InplaceEditingConfig"
           active="{Boolean}true"
           editorType="image">
           <config jcr:primaryType="nt:unstructured">
               <plugins jcr:primaryType="nt:unstructured">
                   <crop jcr:primaryType="nt:unstructured">
                       <aspectRatios jcr:primaryType="nt:unstructured">
                           <_x0031_6-10
                               jcr:primaryType="nt:unstructured"
                               name="16 : 10"
                               ratio="0.625"/>
                       </aspectRatios>
                   </crop>
               </plugins>
           </config>
   </cq:inplaceEditing>
```

>[!NOTE]
>
>AEM裁剪比率，由设置 `ratio` 属性，定义为 **高度/宽度**. 这与常见的宽高比的定义不同，这样做是出于对旧版兼容性的考虑。只要您定义 `name` 属性，因为这是UI中显示的内容。

#### 创建新的就地编辑器 {#creating-a-new-in-place-editor}

要实施新的就地编辑器（在clientlib中），请执行以下操作：

1. 实施：

   * `setUp`
   * `tearDown`

1. 注册编辑器（包括构造函数）：

   * `editor.register`

1. 提供编辑器与可以使用该编辑器的每种资源类型（如组件中所示）之间的连接。

#### 用于创建新的就地编辑器的代码示例 {#code-sample-for-creating-a-new-in-place-editor}

`aem-authoring-extension-inplace-editor` 是一个示例包，显示如何在AEM中创建就地编辑器。

您可以在此页面中找到代码： [GitHub。](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor)

## 添加新页面操作 {#add-a-new-page-action}

要向页面工具栏中添加新的页面操作，例如 **返回站点** （控制台）操作。

### 代码示例 {#code-sample-3}

`aem-authoring-extension-header-backtosites` 是一个示例包，显示如何创建自定义标题栏操作以跳回站点控制台。

您可以在此页面中找到代码： [GitHub。](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites)

## 自定义激活请求工作流 {#customizing-the-request-for-activation-workflow}

开箱即用的工作流程， **请求激活**：

* 当内容作者时，将自动显示在相应的菜单中 **没有** 适当的复制权限，但 **有** DAM用户和作者的成员资格。

* 否则，不会显示任何内容，因为复制权限已被删除。

要在此类激活中进行自定义行为，您可以叠加 **请求激活** 工作流：

1. 在 `/apps` 叠加 **站点** 向导 `/libs/wcm/core/content/common/managepublicationwizard`

   * 它本身会覆盖 `/libs/cq/gui/content/common/managepublicationwizard`.

1. 根据需要更新工作流模型和相关配置/脚本。
1. 删除对的权限 `replicate` 操作时，执行与所有相关页面相关的操作。 要在任何用户时将此工作流作为默认操作触发，请尝试发布（或复制）页面。
