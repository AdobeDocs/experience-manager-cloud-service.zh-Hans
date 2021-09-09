---
title: 自定义和扩展内容片段
description: 内容片段对标准资产进行了扩展。
exl-id: 58152d6e-21b6-4f45-a45c-0f46ee58825e
source-git-commit: c43b55243a73285b78447e32beb16b25608f6d3c
workflow-type: tm+mt
source-wordcount: '1808'
ht-degree: 1%

---

# 自定义和扩展内容片段{#customizing-and-extending-content-fragments}

在Adobe Experience Manager中作为Cloud Service，内容片段扩展标准资产；请参阅：

* [创建和管理内容片段](/help/assets/content-fragments/content-fragments.md) 和使用 [内容片段进行页面创](/help/sites-cloud/authoring/fundamentals/content-fragments.md) 作，以进一步了解内容片段。

* [管理资](/help/assets/manage-digital-assets.md) 产，以了解有关标准资产的更多信息。

## 架构 {#architecture}

内容片段的基本[组成部分](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment)包括：

* *内容片段*,
* 由一个或多个&#x200B;*内容元素*&#x200B;组成，
* 和，其中可以有一个或多个&#x200B;*内容变体*。

单个内容片段基于内容片段模型：

* 内容片段模型在创建内容片段时定义其结构。
* 片段引用模型；因此，对模型所做的更改可能会/将会影响任何依赖的片段。
* 模型是数据类型的构建。
* 用于添加新变量等的函数必须相应地更新片段。

   >[!NOTE]
   >
   >要显示/渲染内容片段，您的帐户必须具有`read`模型权限。

   >[!CAUTION]
   >
   >对现有内容片段模型所做的任何更改都可能影响依赖的片段；这可能会导致这些片段中的孤立属性。

### 将站点与资产集成 {#integration-of-sites-with-assets}

内容片段管理(CFM)是AEM Assets的一部分，其格式为：

* 内容片段是资产。
* 它们使用现有的资产功能。
* 它们与资产（管理控制台等）完全集成。

内容片段被视为站点功能，如下所示：

* 在创作页面时，会使用这些量度。

#### 将内容片段映射到资产 {#mapping-content-fragments-to-assets}

![内容片段到资产](assets/content-fragment-to-assets.png)

内容片段基于内容片段模型，会映射到单个资产：

* 所有内容都存储在资产的`jcr:content/data`节点下：

   * 元素数据存储在主控子节点下：
      `jcr:content/data/master`

   * 变体存储在带有变体名称的子节点下：
例如`jcr:content/data/myvariation`

   * 每个元素的数据作为具有元素名称的属性存储在相应的子节点中：
例如，元素`text`的内容将作为属性`text`存储在`jcr:content/data/master`上

* 元数据和关联内容存储在`jcr:content/metadata`下
除标题和描述之外，这些标题和描述不被视为传统元数据并存储在 
`jcr:content`

#### 资产位置 {#asset-location}

与标准资产一样，内容片段位于以下位置：

`/content/dam`

#### 资产权限 {#asset-permissions}

有关更多详细信息，请参阅[内容片段 — 删除注意事项](/help/assets/content-fragments/content-fragments-delete.md)。

#### 功能集成 {#feature-integration}

要与Assets核心集成，请执行以下操作：

* 内容片段管理(CFM)功能以资产核心为基础。

* CFM为卡片/列/列表视图中的项目提供了自己的实施；这些插件可插入现有资产内容渲染实施。

* 已扩展多个资产组件，以满足内容片段的需求。

### 在页面中使用内容片段 {#using-content-fragments-in-pages}

>[!CAUTION]
>
>[内容片段组件是核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html)的一部分。 有关更多详细信息，请参阅[开发核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/developing.html)。

可以像任何其他资产类型一样，从AEM页面引用内容片段。 AEM提供了&#x200B;**[内容片段核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html)** - a [组件，该组件允许您在页面](/help/sites-cloud/authoring/fundamentals/content-fragments.md#adding-a-content-fragment-to-your-page)上包含内容片段。 您还可以扩展此&#x200B;**[内容片段](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/developing.html)**&#x200B;核心组件。

* 组件使用`fragmentPath`属性引用实际的内容片段。 `fragmentPath`属性的处理方式与其他资产类型的类似属性相同；例如，当内容片段被移动到其他位置时。

* 组件允许您选择要显示的变量。

* 此外，还可以选择一系列段落以限制输出；例如，它可用于多列输出。

* 组件允许使用中间内容：

   * 在此，组件允许您放置其他资产（图像等） 在引用片段的段落之间。

   * 对于中间内容，您需要：

      * 注意可能出现不稳定的引用；中间内容（在创作页面时添加）与它位于旁边的段落没有固定的关系，在中间内容的位置可能丢失相对位置之前插入新段落（在内容片段编辑器中）

      * 考虑其他参数（如变体和段落过滤器）以配置页面上呈现的内容

>[!NOTE]
>
>**内容片段模型:**
>
>当页面上使用内容片段时，将引用该页面所基于的内容片段模型。
>
>这意味着，如果发布页面时尚未发布模型，则会标记该模型，并将模型添加到要随页面一起发布的资源中。

### 与其他框架集成 {#integration-with-other-frameworks}

内容片段可以与以下内容集成：

* **翻译**

   内容片段与[AEM翻译工作流](/help/sites-cloud/administering/translation/overview.md)完全集成。 在建筑层面，这意味着：

   * 内容片段的个别翻译实际上是单独的片段；例如：

      * 它们位于不同的语言根下；但在相关语言根目录下完全共享相同的相对路径：

         `/content/dam/<path>/en/<to>/<fragment>`

         与

         `/content/dam/<path>/de/<to>/<fragment>`
   * 除了基于规则的路径之外，内容片段的不同语言版本之间没有进一步的连接；虽然UI提供了在语言变体之间导航的方法，但它们将作为两个单独的片段进行处理。
   >[!NOTE]
   >
   >AEM翻译工作流可与`/content`配合使用：
   >
   >* 由于内容片段模型位于`/conf`中，因此此类转换中不包含这些模型。 您可以将UI字符串国际化。


* **元数据架构**

   * 内容片段（重新）使用[元数据架构](/help/assets/metadata-schemas.md)，该架构可以使用标准资产进行定义。

   * CFM提供了自己的特定架构：

      `/libs/dam/content/schemaeditors/forms/contentfragment`

      如果需要，可以扩展此功能。

   * 相应的架构表单与片段编辑器集成。

## 内容片段管理API — 服务器端 {#the-content-fragment-management-api-server-side}

您可以使用服务器端API访问您的内容片段；请参阅：

[com.adobe.cq.dam.cfm](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/adobe/cq/dam/cfm/package-summary.html#package.description)

>[!CAUTION]
>
>强烈建议使用服务器端API，而不是直接访问内容结构。

### 关键界面 {#key-interfaces}

以下三个界面可用作入口点：

* **内容片段** ([ContentFragment](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/adobe/cq/dam/cfm/ContentFragment.html))

   此界面允许您以抽象方式处理内容片段。

   该界面为您提供了以下方法：

   * 管理基本数据(例如，获取名称；get/set title/description)
   * 访问元数据
   * 访问元素：

      * 列表元素
      * 按名称获取元素
      * 创建新元素（请参阅[注意事项](#caveats)）

      * 访问元素数据（请参阅`ContentElement`）
   * 为片段定义的列表变量
   * 全局创建新变量
   * 管理关联内容：

      * 列出集合
      * 添加收藏集
      * 删除收藏集
   * 访问片段的模型

   表示片段主要元素的界面包括：

   * **内容元素** ([ContentElement](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/adobe/cq/dam/cfm/ContentElement.html))

      * 获取基本数据（名称、标题、描述）
      * 获取/设置内容
      * 访问元素的变体：

         * 列表变体
         * 按名称获取变体
         * 创建新变体（请参阅[注意事项](#caveats)）
         * 删除变体（请参阅[注意事项](#caveats)）
         * 访问变量数据（请参阅`ContentVariation`）
      * 解析变量的快捷方式（如果指定的变量不适用于元素，则应用一些其他特定于实施的回退逻辑）
   * **内容变体** ([ContentVariation](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/adobe/cq/dam/cfm/ContentVariation.html))

      * 获取基本数据（名称、标题、描述）
      * 获取/设置内容
      * 简单同步，基于上次修改的信息

   所有三个接口(`ContentFragment`、`ContentElement`、`ContentVariation`)都扩展了`Versionable`接口，该接口可添加内容片段所需的版本控制功能：

   * 创建元素的新版本
   * 元素的列表版本
   * 获取版本控制元素的特定版本的内容







### 适应 — 使用adaptTo() {#adapting-using-adaptto}

可以修改以下内容：

* `ContentFragment` 可适用于：

   * `Resource`  — 基础Sling资源；直接更新基础 `Resource` 对象需要重建 `ContentFragment` 对象。

   * `Asset`  — 表示内 `Asset` 容片段的DAM抽象；直接更 `Asset` 新需要重建对 `ContentFragment` 象。

* `ContentElement` 可适用于：

   * [`ElementTemplate`](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/adobe/cq/dam/cfm/ElementTemplate.html)  — 访问元素的结构信息。

* [`FragmentTemplate`](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/adobe/cq/dam/cfm/FragmentTemplate.html)

* `Resource` 可适用于：

   * `ContentFragment`

### 注意事项 {#caveats}

应当指出：

* 整个API设计为&#x200B;**不**&#x200B;自动保留更改（除非API JavaDoc中另有说明）。 因此，您将始终必须提交相应请求的资源解析程序（或您实际使用的解析程序）。

* 可能需要额外努力的任务：

   * 强烈建议从`ContentFragment`创建新变量。 这可确保所有元素都共享此变体，并且会根据需要更新相应的全局数据结构，以反映内容结构中新创建的变体。

   * 使用`ContentElement.removeVariation()`通过元素删除现有变量将不会更新分配给该变量的全局数据结构。 要确保这些数据结构保持同步，请改用`ContentFragment.removeVariation()`，这会全局删除变量。

## 内容片段管理API — 客户端 {#the-content-fragment-management-api-client-side}

>[!CAUTION]
>
>客户端API是内部API。

### 附加信息 {#additional-information}

请参阅以下内容：

* `filter.xml`

   内容片段管理的`filter.xml`已进行配置，以便它不会与资产核心内容包重叠。

## 编辑会话 {#edit-sessions}

>[!CAUTION]
>
>请考虑此背景信息。 您不应在此处更改任何内容（因为在存储库中标记为&#x200B;*专用区域*），但在某些情况下，它可能有助于您了解引擎盖下的工作方式。

编辑内容片段(可以跨多个视图（= HTML页面）)是一个原子过程。 因此，原子多视图编辑功能不是典型的AEM概念，因此内容片段使用的是所谓的&#x200B;*编辑会话*。

当用户在编辑器中打开内容片段时，将启动编辑会话。 当用户通过选择&#x200B;**Save**&#x200B;或&#x200B;**Cancel**&#x200B;离开编辑器时，编辑会话即告结束。

从技术上讲，所有编辑操作都是在&#x200B;*live*&#x200B;内容上完成的，就像所有其他AEM编辑操作一样。 启动编辑会话时，将创建当前未编辑状态的版本。 如果用户取消编辑，则会恢复该版本。 如果用户单击&#x200B;**Save**，则不会执行任何特定操作，因为所有编辑操作都在&#x200B;*live*&#x200B;内容上执行，因此所有更改都将保留。 此外，单击&#x200B;**Save**&#x200B;将触发一些后台处理（例如创建全文搜索信息和/或处理混合媒体资产）。

边缘案件有一些安全措施；例如，如果用户尝试离开编辑器而未保存或取消编辑会话。 此外，还提供定期自动保存，以防止数据丢失。
请注意，两个用户可以同时编辑同一内容片段，因此可能会覆盖彼此的更改。 要防止出现这种情况，需要通过在片段上应用DAM管理的*Checkout*&#x200B;操作来锁定内容片段。

## 示例 {#examples}

### 示例：访问现有内容片段 {#example-accessing-an-existing-content-fragment}

要实现此目的，您可以调整表示API的资源以：

`com.adobe.cq.dam.cfm.ContentFragment`

例如：

```java
// first, get the resource
Resource fragmentResource = resourceResolver.getResource("/content/dam/fragments/my-fragment");
// then adapt it
if (fragmentResource != null) {
    ContentFragment fragment = fragmentResource.adaptTo(ContentFragment.class);
    // the resource is now accessible through the API
}
```

### 示例：创建新内容片段 {#example-creating-a-new-content-fragment}

要以编程方式创建新内容片段，您需要使用
`FragmentTemplate`根据模型资源进行调整。

例如：

```java
Resource modelRsc = resourceResolver.getResource("...");
FragmentTemplate tpl = modelRsc.adaptTo(FragmentTemplate.class);
ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
```

### 示例：指定自动保存间隔 {#example-specifying-the-auto-save-interval}

[自动保存间隔](/help/assets/content-fragments/content-fragments-managing.md#save-close-and-versions)（以秒为单位）可以使用配置管理器(ConfMgr)定义：

* 节点：`<conf-root>/settings/dam/cfm/jcr:content`
* 属性名称: `autoSaveInterval`
* 类型: `Long`

* 默认：`600`（10分钟）；这在`/libs/settings/dam/cfm/jcr:content`上定义

如果要设置5分钟的自动保存间隔，则需要在节点上定义属性；例如：

* 节点：`/conf/global/settings/dam/cfm/jcr:content`
* 属性名称: `autoSaveInterval`

* 类型: `Long`

* 值：`300`（5分钟等于300秒）

## 用于创作页面的组件 {#components-for-page-authoring}

有关详细信息，请参阅

* [核心组件 — 内容片段组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html) （推荐）
