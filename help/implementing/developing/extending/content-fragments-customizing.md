---
title: 自定义和扩展内容片段
description: 内容片段扩展标准资产。
translation-type: tm+mt
source-git-commit: a5d6a072dfd8df887309f56ad4a61b6b38b32fa7
workflow-type: tm+mt
source-wordcount: '2119'
ht-degree: 3%

---


# 自定义和扩展内容片段{#customizing-and-extending-content-fragments}

在Adobe Experience Manager中，内容片段作为Cloud Service扩展标准资产； 请参阅：

* [有关内容片段的更多信息](/help/assets/content-fragments/content-fragments.md) ，请 [使用内容片段创建和管理内容片段](/help/sites-cloud/authoring/fundamentals/content-fragments.md) ，以及使用页面创作。

* [管理资产](/help/assets/manage-digital-assets.md) 、 [自定义和扩展资产编辑器](/help/assets/extend-asset-editor.md) ，以了解有关标准资产的更多信息。

## 架构 {#architecture}

内容片 [段的基](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) 本组成部分包括：

* 内 *容片段*,
* 包含一个或多个 *内容元素*,
* 和可以具有一个或多个内 *容变量*。

根据片段类型，还使用模型 **或简单片段** 模板：

>[!CAUTION]
>
>[现在建议使用](/help/assets/content-fragments/content-fragments-models.md) “内容片段模型”来创建您的所有片段。
>
>内容片段模型用于WKND中的所有示例。

* 内容片段模型:

   * 用于定义包含结构化内容的内容片段。
   * 内容片段模型定义内容片段在创建时的结构。
   * 片段引用模型； 因此，对模型所做的更改可能会／会影响任何从属片段。
   * 模型是数据类型的构建。
   * 添加新变量等的函数必须相应更新片段。

   >[!NOTE]
   >
   >要显示／呈现内容片段，您的帐户必须具有该 `read` 模型的权限。

   >[!CAUTION]
   >
   >对现有内容片段模型的任何更改都可能影响相关片段； 这会导致这些片段中的孤立属性。

* 内容片段模板- **简单片段**:

   * 用于定义简单内容片段。

   * 此模板定义内容片段在创建时的（基本、仅文本）结构。

   * 创建模板时，模板将复制到片段。

   * 添加新变量等的函数必须相应更新片段。

   * 内容片段模板(**简单片段**)的操作方式与AEM生态系统中其他模板机制（如页面模板等）的操作方式不同。 因此，应单独考虑。

   * 当基于简单 **片段模板** ，内容的MIME类型将根据实际内容进行管理； 这意味着每个元素和变量都可以具有不同的MIME类型。

### 将站点与资产集成 {#integration-of-sites-with-assets}

内容片段管理(CFM)是以下AEM Assets的一部分：

* 内容片段是资产。
* 他们使用现有资产功能。
* 它们与资产（管理控制台等）完全集成。

内容片段被视为站点功能，因为：

* 在创作页面时，会使用它们。

#### 将结构化内容片段映射到资产 {#mapping-structured-content-fragments-to-assets}

![内容片段至结构化资产](assets/content-fragment-to-assets-structured.png)

具有结构化内容（即基于内容片段模型）的内容片段将映射到单个资产：

* 所有内容都存储在资 `jcr:content/data` 产的节点下：

   * 元素数据存储在主子节点下：
      `jcr:content/data/master`

   * 变体存储在子节点下，子节点带有变体的名称：
例如， `jcr:content/data/myvariation`

   * 每个元素的数据作为具有元素名称的属性存储在相应的子节点中：
例如，元素的内容 `text` 作为属性存储在 `text` `jcr:content/data/master`

* 元数据和关联内容存储在 `jcr:content/metadata`下面，但标题和说明除外，它们不被视为传统元数据，并存储在 
`jcr:content`

#### 将简单内容片段映射到资产 {#mapping-simple-content-fragments-to-assets}

![内容片段到资产的简单操作](assets/content-fragment-to-assets-simple.png)

简单内容片段(基于 **简单片段** 模板)映射到由主资产和（可选）子资产组成的组合：

* 片段的所有非内容信息（如标题、描述、元数据、结构）均专门在主资产上进行管理。
* 片段的第一个元素的内容将映射到主资产的原始演绎版。

   * 第一个元素的变量（如果有）会映射到主资产的其他演绎版。

* 其他元素（如果现有）会映射到主资产的子资产。

   * 这些附加元素的主要内容会映射到相应子资产的原始演绎版。
   * 任何其他元素的其他变体（如果适用）会映射到相应子资产的其他演绎版。

#### 资产位置 {#asset-location}

与标准资产一样，内容片段位于以下位置：

`/content/dam`

#### 资产权限 {#asset-permissions}

有关更多详细信息， [请参阅内容片段——删除注意事项](/help/assets/content-fragments/content-fragments-delete.md)。

#### 功能集成 {#feature-integration}

要与Assets核心集成，请执行以下操作：

* 内容片段管理(CFM)功能构建于资产核心之上。

* CFM为卡／列/列表视图中的项目提供其自己的实现； 这些插件可插入现有资产内容呈现实施。

* 已扩展多个资产组件，以满足内容片段的需要。

### 在页面中使用内容片段 {#using-content-fragments-in-pages}

>[!CAUTION]
>
>内 [容片段组件是核心组件的一部分](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/content-fragment-component.html)。 有关更 [多详细信息](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/developing.html) ，请参阅开发核心组件。

内容片段可以从AEM页面中引用，就像任何其他资产类型一样。 AEM提供内 **[容片段核心组件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/content-fragment-component.html)**-一[个允许您在页面上包含内容片段的组件](/help/sites-cloud/authoring/fundamentals/content-fragments.md#adding-a-content-fragment-to-your-page)。 您还可以扩展此内**[容片段](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/developing.html)** 核心组件。

* 组件使用属 `fragmentPath` 性引用实际内容片段。 该 `fragmentPath` 财产的处理方式与其他资产类型的类似财产相同； 例如，当内容片段被移动到其他位置时。

* 组件允许您选择要显示的变量。

* 此外，还可以选择一系列段落来限制输出； 例如，这可用于多列输出。

* 组件允许中间内容：

   * 在此组件中，您可以放置其他资产（图像等） 在引用片段的段落之间。

   * 对于中间内容，您需要：

      * 注意不稳定的参考资料的可能性； 中间内容（在创作页面时添加）与它位于旁边的段落没有固定关系，在中间内容的位置之前插入新段落（在内容片段编辑器中）可能会丢失相对位置

      * 考虑其他参数(如变体和段落过滤器)，以配置页面上呈现的内容

>[!NOTE]
>
>**内容片段模型:**
>
>当使用基于页面上的内容片段模型的内容片段时，将引用该模型。 这意味着，如果发布页面时尚未发布模型，则会标记该模型并将该模型添加到要随页面一起发布的资源。
>
>**内容片段模板——简单片段：**
>
>在使用基于页面上的内容片段模板简 **单片段** 的内容片段时，没有引用，因为创建片段时复制了模板。

### 与其他框架集成 {#integration-with-other-frameworks}

内容片段可与以下内容集成：

* **翻译**

   内容片段与AEM翻译工作流程完全集成。 在建筑层面，这意味着：

   * 内容片段的个别翻译实际上是单独的片段； 例如：

      * 它们位于不同的语言根系下； 但在相关语言根目录下共享完全相同的相对路径：

         `/content/dam/<path>/en/<to>/<fragment>`

         与

         `/content/dam/<path>/de/<to>/<fragment>`
   * 除了基于规则的路径之外，内容片段的不同语言版本之间没有进一步的联系； 它们作为两个单独的片段处理，但UI提供了在语言变体之间导航的方法。
   >[!NOTE]
   >
   >AEM翻译工作流程可用于 `/content`:
   >
   >* 由于内容片段模型位于 `/conf`其中，因此此类转换中不包含这些模型。 可以将UI字符串国际化。


* **元数据架构**

   * 内容片段（重新）使用元 [数据模式](/help/assets/metadata-schemas.md)，这些可以使用标准资产进行定义。

   * CFM提供其自己的特定模式:

      `/libs/dam/content/schemaeditors/forms/contentfragment`

      如果需要，可以扩展此功能。

   * 相应的模式表单与片段编辑器集成。

## 内容片段管理API —— 服务器端 {#the-content-fragment-management-api-server-side}

您可以使用服务器端API访问您的内容片段； 请参阅：

[com.adobe.cq.dam.cfm](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/ref/javadoc/com/adobe/cq/dam/cfm/package-frame.html)

>[!CAUTION]
>
>强烈建议使用服务器端API，而不是直接访问内容结构。

### 关键接口 {#key-interfaces}

以下三个接口可用作入口点：

* **内容片段** ([ContentFragment](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/ref/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html))

   此界面允许您以抽象方式处理内容片段。

   该界面为您提供了以下方法：

   * 管理基本数据(例如，获取名称； get/set title/description)
   * 访问元数据
   * 访问元素：

      * 列表元素
      * 按名称获取元素
      * 创建新元素(请参阅 [警告](#caveats))

      * 访问元素数据(请参 `ContentElement`阅)
   * 为片段定义的列表变量
   * 全局创建新变量
   * 管理关联内容：

      * 列表集合
      * 添加集合
      * 删除集合
   * 访问片段的模型或模板

   表示片段主元素的接口包括：

   * **内容元素** ([ContentElement](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/ref/javadoc/com/adobe/cq/dam/cfm/ContentElement.html))

      * 获取基本数据（名称、标题、说明）
      * 获取／设置内容
      * 访问元素的变体：

         * 列表变化
         * 按名称获取变体
         * 创建新变体(请参阅 [警告](#caveats))
         * 删除变体(请参 [阅警告](#caveats))
         * 访问变量数据(请参 `ContentVariation`阅)
      * 用于解析变量的快捷方式（如果指定的变量对元素不可用，则应用一些附加的特定于实施的回退逻辑）
   * **内容变化** ([ContentVariation](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/ref/javadoc/com/adobe/cq/dam/cfm/ContentVariation.html))

      * 获取基本数据（名称、标题、说明）
      * 获取／设置内容
      * 简单同步，基于上次修改的信息

   所有三个界面( `ContentFragment`、 `ContentElement`、 `ContentVariation`)都扩展了界面，它添加了内容片段 `Versionable` 所需的版本控制功能：

   * 创建元素的新版本
   * 列表元素的版本
   * 获取版本化元素的特定版本的内容







### 改编——使用adaptTo() {#adapting-using-adaptto}

可以调整以下内容：

* `ContentFragment` 可适用于：

   * `Resource` -基础Sling资源； 直接更新基础 `Resource` 需要重建对 `ContentFragment` 象。

   * `Asset` -表示内 `Asset` 容片段的DAM抽象； 直接更 `Asset` 新需要重建对 `ContentFragment` 象。

* `ContentElement` 可适用于：

   * `ElementTemplate` -用于访问元素的结构信息。

* `Resource` 可适用于：

   * `ContentFragment`

### 警告 {#caveats}

应当指出：

* 整个API设计为不自 **动保留** 更改（除非在API JavaDoc中另有说明）。 因此，您始终必须提交相应请求的资源解析程序（或您实际使用的解析程序）。

* 可能需要付出额外努力的任务:

   * 从中创建新变 `ContentFragment` 量以更新数据结构。

   * 使用元素删除现有变量 `ContentElement.removeVariation()`不会更新分配给该变量的全局数据结构。 要确保这些数据结构保持同步，请改 `ContentFragment.removeVariation()` 用它，从全局上删除变量。

## 内容片段管理API —— 客户端 {#the-content-fragment-management-api-client-side}

>[!CAUTION]
>
>客户端API是内部的。

### 附加信息 {#additional-information}

请参阅以下内容：

* `filter.xml`

   内 `filter.xml` 容片段管理的配置使其不与资产核心内容包重叠。

## 编辑会话 {#edit-sessions}

>[!CAUTION]
>
>请考虑此背景信息。 您不应在此处更改任何内容(因为在存储库中 *标记为* “专用区域”)，但在某些情况下，它可能有助于您了解内部的工作方式。

编辑内容片段(可以跨多个视图（= HTML页面）)是原子的。 由于这种原子多视图编辑功能不是典型的AEM概念，内容片段使用所谓的编辑 *会话*。

当用户在编辑器中打开内容片段时，将启动编辑会话。 当用户通过选择“保存”或“取消”离开编辑器时，编 **辑会** 话即 **结束**。

从技术上讲，所有编辑操 *作都是* 对实时内容进行的，就像所有其他AEM编辑一样。 启动编辑会话时，将创建当前未编辑状态的某个版本。 如果用户取消编辑，则恢复该版本。 如果用户单击“保 **存**”，则不会执行任何特定操作，因为所有编辑都对实 *时内容执* 行，因此所有更改都已保留。 此外，单击保 **存** 将触发一些后台处理（例如创建全文搜索信息和／或处理混合媒体资产）。

边缘案件有安全措施； 例如，如果用户尝试离开编辑器而不保存或取消编辑会话。 此外，还可定期自动保存以防止数据丢失。
请注意，两个用户可以同时编辑同一内容片段，因此可能会覆盖彼此的更改。 要防止出现这种情况，需要通过对片段应用DAM管理的“结帐” *操作* ，来锁定内容片段。

## 示例 {#examples}

### 示例： 访问现有内容片段 {#example-accessing-an-existing-content-fragment}

要实现此目标，您可以调整表示API的资源以：

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

### 示例： 创建新内容片段 {#example-creating-a-new-content-fragment}

要以编程方式创建新内容片段，您需要使用根据模型`FragmentTemplate` 或模板资源调整的内容片段。

例如：

```java
Resource templateOrModelRsc = resourceResolver.getResource("...");
FragmentTemplate tpl = templateOrModelRsc.adaptTo(FragmentTemplate.class);
ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
```

### 示例： 指定自动保存间隔 {#example-specifying-the-auto-save-interval}

自动 [保存间隔](/help/assets/content-fragments/content-fragments-managing.md#save-cancel-and-versions) （以秒为单位）可以使用配置管理器(ConfMgr)进行定义：

* 节点： `<conf-root>/settings/dam/cfm/jcr:content`
* 属性名称: `autoSaveInterval`
* 类型: `Long`

* 默认： `600` （10分钟）; 定义于 `/libs/settings/dam/cfm/jcr:content`

如果要设置5分钟的自动保存间隔，您需要定义节点上的属性； 例如：

* 节点： `/conf/global/settings/dam/cfm/jcr:content`
* 属性名称: `autoSaveInterval`

* 类型: `Long`

* 值： `300` （5分钟等于300秒）

## 用于创作页面的组件 {#components-for-page-authoring}

有关更多信息，请参阅

* [核心组件——内容片段组件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/content-fragment-component.html) （推荐）
