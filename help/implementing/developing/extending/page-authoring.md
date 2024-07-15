---
title: 自定义页面创作
description: 了解 AEM as a Cloud Service 提供的用于自定义页面创作功能的机制。
exl-id: 98d3c7ab-46d2-4e8d-b0da-5c8a7b398135
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 94%

---

# 自定义页面创作 {#customizing-page-authoring}

Adobe Experience Manager as a Cloud Service 提供了一些机制，让您可以自定义您的创作实例的页面创作功能（以及[控制台](/help/implementing/developing/extending/consoles.md)) 。

## Clientlibs {#clientlibs}

Clientlib 允许您扩展默认实现，以启用新功能，同时重新使用标准函数、对象和方法。

定制时，您可以在 `/apps.` 下创建自己的 clientlib。新的 clientlib 必须：

* 取决于创作 clientlib `cq.authoring.editor.sites.page`。
* 成为相应 `cq.authoring.editor.sites.page.hook` 类别的一部分。

请参阅[在AEM as a Cloud Service](/help/implementing/developing/introduction/clientlibs.md)上使用客户端库。

## 叠加 {#overlays}

叠加基于节点定义，允许您将 `/libs` 中的标准功能与 `/apps` 中的自定义功能叠加。

创建叠加时，不需要原件的 1:1 副本，因为[ Sling 资源合并器](/help/implementing/developing/introduction/sling-resource-merger.md)允许继承。

有关详细信息，请参阅[JS文档集](https://developer.adobe.com/experience-manager/reference-materials/6-5/jsdoc/ui-touch/editor-core/index.html)。

有关叠加的详细信息，请参阅Adobe Experience Manager as a Cloud Service的[叠加](/help/implementing/developing/introduction/overlays.md)。

## 添加新层（模式） {#add-new-layer-mode}

当您编辑页面的时候，有各种各样的[模式](/help/sites-cloud/authoring/page-editor/introduction.md#page-modes)可用。这些模式是使用[层次](/help/implementing/developing/introduction/ui-structure.md#layer)来实施的。其允许访问同一页面内容的不同类型的功能。标准 AEM 模式包括编辑、布局、开发人员、时间扭曲、Live Copy 状态和定位。

### 层次示例：Live Copy 状态 {#layer-example-live-copy-status}

标准 AEM 实例提供 MSM 层。这会访问与[多站点管理](/help/sites-cloud/administering/msm/overview.md)相关的数据，并在层次中突出显示它。

要查看其实际效果，您可以在 [WKND 样本内容](/help/implementing/developing/introduction/develop-wknd-tutorial.md)中编辑任何语言副本，并选择&#x200B;**Live Copy 状态**&#x200B;模式。

您可以在以下位置找到 MSM 层的定义（仅供参考）：

`/libs/wcm/msm/content/touch-ui/authoring/editor/js/msm.Layer.js`

### 代码示例 {#code-sample}

这是一个示例包，其中展示了如何为 MSM 视图创建层次（模式）。

您可以在[ GitHub ](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode)上找到此页面的代码。

## 将新的选择类别添加到资源浏览器 {#add-new-selection-category-to-asset-browser}

资源浏览器会显示各种类型/类别的资源（例如图像和文档）。还可以按这些资源类别过滤资源。

### 代码示例 {#code-sample-1}

`aem-authoring-extension-assetfinder-flickr` 是一个示例包，其中显示了如何将群组添加到资源查找器。此示例会连接到 [Flickr ](https://www.flickr.com)的公共流，并在侧面板中显示它们。

您可以在[ GitHub ](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr)上找到此页面的代码。

## 筛选资源 {#filtering-resources}

在创作页面时，用户必须经常从列表中的资源中进行选择。

为了使列表保持合理的大小并且与用例相关，可以通过自定义谓词的形式实施筛选条件。例如，如果 `pathbrowser`Granite 组件用于允许用户选择特定资源的路径，则可以通过以下方式筛选所显示的路径：

* 通过实施 [`com.day.cq.commons.predicate.AbstractNodePredicate`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/predicate/package-summary.html) 界面来实施自定义谓词。
* 指定谓词的名称，并在使用 `pathbrowser` 时引用该名称。

有关创建自定义谓词的更多详细信息，请参阅[本文](/help/implementing/developing/introduction/query-builder-custom-predicate.md)。

## 将新的操作添加到组件工具栏 {#add-new-action-to-a-component-toolbar}

每个组件通常都有一个工具栏，其中可提供对该组件可以执行的一系列操作的访问。

### 代码示例 {#code-sample-2}

`aem-authoring-extension-toolbar-screenshot` 是一个示例包，其中展示了如何创建自定义工具栏操作，以呈现组件。

您可以在[ GitHub ](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot)上找到此页面的代码。

## 添加新的就地编辑器 {#add-new-in-place-editor}

### 标准就地编辑器 {#standard-in-place-editor}

在标准 AEM 安装中：

1. `/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js` 会保存各种可用编辑器的定义。

1. 编辑器和可以使用它的每种资源类型（如在组件中）之间存在连接：

   * `cq:inplaceEditing`

     例如：

      * `/libs/foundation/components/text/cq:editConfig`
      * `/libs/foundation/components/image/cq:editConfig`

         * 属性：`editorType`

           定义触发对该组件进行就地编辑时使用的内联编辑器的类型；例如，`text`, `textimage`, `image`, `title`。

1. 编辑器的其他配置详细信息可以使用`config`包含配置的节点和包含必要插件配置详细信息的`plugin`节点进行配置。


以下是为图像组件的图像裁剪插件定义纵横比的示例。

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
>由 `ratio` 属性设置的 AEM 裁剪比例定义为&#x200B;**高度/宽度**。这与常见的宽高比的定义不同，这样做是出于对旧版兼容性的考虑。只要您清楚地定义 `name` 属性，页面创作用户便不会察觉到任何差异，因为您定义的名称才是 UI 中显示的内容。

#### 创建新的就地编辑器 {#creating-a-new-in-place-editor}

要实施新的就地编辑器（在您的 clientlib 中）：

1. 实施：

   * `setUp`
   * `tearDown`

1. 注册编辑器（包括构造函数）：

   * `editor.register`

1. 提供编辑器和可以使用它的每种资源类型（如在组件中）之间存在连接。

#### 用于创建新的就地编辑器的代码示例 {#code-sample-for-creating-a-new-in-place-editor}

`aem-authoring-extension-inplace-editor` 是一个示例包，其中展示如何在 AEM 中创建就地编辑器。

您可以在[ GitHub ](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor)上找到此页面的代码。

## 添加新的页面操作。 {#add-a-new-page-action}

向页面工具栏中添加新的页面操作，例如&#x200B;**返回站点** （控制台）操作。

### 代码示例 {#code-sample-3}

`aem-authoring-extension-header-backtosites` 是一个示例包，其中显示如何创建自定义标题栏操作，以跳回 Sites 控制台。

您可以在[ GitHub ](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites)上找到此页面的代码。

## 自定义激活请求工作流程程 {#customizing-the-request-for-activation-workflow}

开箱即用的工作流程程，**请求激活：**

* 当内容作者&#x200B;**没有**&#x200B;适当的复制权限，但&#x200B;**有** DAM 用户和作者的会员资格时，将会自动出现在适当的菜单上。

* 否则，不会显示任何内容，因为复制权限已被删除。

要在此类激活上自定义行为，您可以叠加&#x200B;**请求激活**&#x200B;工作流程程：

1. 在`/apps`叠加 **Sites** 向导`/libs/wcm/core/content/common/managepublicationwizard`

   * 这本身就覆盖了 `/libs/cq/gui/content/common/managepublicationwizard` 的常见的实例。

1. 根据需要更新工作流程程模型和相关的配置/脚本。
1. 删除所有相关页面的所有相应用户的`replicate`操作权限。当任何用户尝试发布（或复制）页面时，将此工作流程作为默认操作触发。
