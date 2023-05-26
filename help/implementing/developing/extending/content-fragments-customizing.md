---
title: 自定义和扩展内容片段
description: 内容片段扩展了标准资产。
exl-id: 58152d6e-21b6-4f45-a45c-0f46ee58825e
source-git-commit: 47910a27118a11a8add6cbcba6a614c6314ffe2a
workflow-type: tm+mt
source-wordcount: '1811'
ht-degree: 2%

---

# 自定义和扩展内容片段{#customizing-and-extending-content-fragments}

在Adobe Experience Manager as a Cloud Service中，内容片段扩展了标准资源；请参阅：

* [创建和管理内容片段](/help/sites-cloud/administering/content-fragments/content-fragments.md) 和 [使用内容片段进行页面创作](/help/sites-cloud/authoring/fundamentals/content-fragments.md) 以了解有关内容片段的更多信息。

* [管理资源](/help/assets/manage-digital-assets.md) 以了解有关标准资产的更多信息。

## 架构 {#architecture}

基本 [组成部分](/help/sites-cloud/administering/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) 的内容片段包括：

* A *内容片段*，
* 由一个或多个组成 *内容元素*，
* 可以有一个或多个 *内容变体*.

各个内容片段基于内容片段模型：

* 内容片段模型在创建内容片段时定义其结构。
* 片段引用模型；因此，对模型的更改可能会影响任何依赖的片段。
* 模型由数据类型构建。
* 添加新变体的函数等必须相应地更新片段。

   >[!NOTE]
   >
   >要显示/渲染内容片段，您的帐户必须具有 `read` 模型的权限。

   >[!CAUTION]
   >
   >对现有内容片段模型所做的任何更改都会影响从属片段；这可能会导致这些片段中的属性孤立。

### Sites与资产的集成 {#integration-of-sites-with-assets}

内容片段管理(CFM)是AEM Assets的一部分，如下所示：

* 内容片段是资产。
* 它们使用现有的Assets功能。
* 它们与Assets（管理控制台等）完全集成。

内容片段被视为站点功能，如下所示：

* 在创作页面时，会使用它们。

#### 将内容片段映射到资产 {#mapping-content-fragments-to-assets}

![将内容片段复制到资产](assets/content-fragment-to-assets.png)

基于内容片段模型的内容片段将映射到单个资源：

* 所有内容都存储在 `jcr:content/data` 资源的节点：

   * 元素数据存储在主控子节点下：
      `jcr:content/data/master`

   * 变量存储在子节点下，该子节点带有变量的名称：例如， `jcr:content/data/myvariation`

   * 每个元素的数据作为具有元素名称的属性存储在相应的子节点中：例如，元素的内容 `text` 存储为属性 `text` 日期 `jcr:content/data/master`

* 元数据和关联内容存储在下方 `jcr:content/metadata`
除了标题和描述之外，它们不被视为传统元数据并存储于 
`jcr:content`

#### 资源位置 {#asset-location}

与标准资产一样，内容片段位于下方：

`/content/dam`

#### 资源权限 {#asset-permissions}

有关更多详细信息，请参阅 [内容片段 — 删除注意事项](/help/sites-cloud/administering/content-fragments/content-fragments-delete.md).

#### 功能集成 {#feature-integration}

要与Assets核心集成：

* 内容片段管理(CFM)功能以Assets核心为基础。

* CFM为卡片/列/列表视图中的项目提供自己的实施；这些实施可以插入现有的Assets内容渲染实施。

* 扩展了多个Assets组件以适应内容片段。

### 在页面中使用内容片段 {#using-content-fragments-in-pages}

>[!CAUTION]
>
>此 [内容片段组件是核心组件的一部分](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=zh-Hans). 参见 [开发核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/developing.html) 了解更多详细信息。

可以从AEM页面引用内容片段，就像任何其他资源类型一样。 AEM提供 **[内容片段核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=zh-Hans)** - a [允许您在页面上包含内容片段的组件](/help/sites-cloud/authoring/fundamentals/content-fragments.md#adding-a-content-fragment-to-your-page). 您还可以扩展此功能 **[内容片段](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/developing.html)** 核心组件。

* 组件使用 `fragmentPath` 属性以引用实际内容片段。 此 `fragmentPath` 资产的处理方式与其他资产类型的类似资产相同；例如，当内容片段移动到其他位置时。

* 利用组件，可选择要显示的变体。

* 此外，可以选择段落范围以限制输出；例如，这可用于多列输出。

* 该组件允许中间内容：

   * 在这里，组件允许您放置其他资产（图像等） 在所引用片段的段落之间。

   * 对于中间内容，您需要：

      * 请注意，可能存在不稳定的引用；中间内容（在创作页面时添加）与其旁边的段落没有固定的关系，在中间内容的位置可能丢失相对位置之前插入新段落（在内容片段编辑器中）

      * 请考虑使用其他参数（如变量和段落过滤器）来配置在页面上渲染的内容

>[!NOTE]
>
>**内容片段模型:**
>
>在页面上使用内容片段时，将引用它所基于的内容片段模型。
>
>这意味着，如果在您发布页面时模型尚未发布，则会标记该模型，并将模型添加到要与页面一起发布的资源中。

### 与其他框架集成 {#integration-with-other-frameworks}

内容片段可以与以下集成：

* **翻译**

   内容片段与完全集成 [AEM翻译工作流](/help/sites-cloud/administering/translation/overview.md). 在架构级别，这意味着：

   * 内容片段的各个翻译实际上是单独的片段；例如：

      * 它们位于不同的语言根下；但在相关语言根下共享完全相同的相对路径：

         `/content/dam/<path>/en/<to>/<fragment>`

         对比

         `/content/dam/<path>/de/<to>/<fragment>`
   * 除了基于规则的路径之外，内容片段的不同语言版本之间没有进一步的连接；它们作为两个单独的片段处理，尽管UI提供了在语言变体之间导航的方法。
   >[!NOTE]
   >
   >AEM翻译工作流程适用于 `/content`：
   >
   >* 由于内容片段模型驻留在 `/conf`，这些不会包含在此类翻译中。 您可以国际化UI字符串。


* **元数据架构**

   * 内容片段（重新）使用 [元数据架构](/help/assets/metadata-schemas.md)，这些资源可使用标准资源定义。

   * CFM提供了自己的特定架构：

      `/libs/dam/content/schemaeditors/forms/contentfragment`

      如果需要，可以扩展此功能。

   * 相应的架构表单与片段编辑器集成。

## 内容片段管理API — 服务器端 {#the-content-fragment-management-api-server-side}

您可以使用服务器端API访问内容片段；请参阅：

[com.adobe.cq.dam.cfm](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/package-summary.html#package.description)

>[!CAUTION]
>
>强烈建议使用服务器端API，而不是直接访问内容结构。

### 关键界面 {#key-interfaces}

以下三个接口可用作入口点：

* **内容片段** ([内容片段](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html))

   利用此界面，可采用抽象方式处理内容片段。

   该界面为您提供了以下方法：

   * 管理基本数据（例如，获取名称；获取/设置标题/描述）
   * 访问元数据
   * 访问元素：

      * 列表元素
      * 按名称获取元素
      * 创建新元素(请参阅 [注意事项](#caveats))

      * 访问元素数据(请参阅 `ContentElement`)
   * 为片段定义的列表变量
   * 全局创建新变体
   * 管理关联内容：

      * 列出收藏集
      * 添加收藏集
      * 删除收藏集
   * 访问片段的模型

   表示片段的主要元素的界面包括：

   * **内容元素** ([内容元素](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ContentElement.html))

      * 获取基本数据（名称、标题、描述）
      * 获取/设置内容
      * 访问元素的变体：

         * 列表变体
         * 按名称获取变体
         * 创建新变体(请参阅 [注意事项](#caveats))
         * 删除变体(请参阅 [注意事项](#caveats))
         * 访问变量数据(请参阅 `ContentVariation`)
      * 解析变体的快捷方式（如果指定的变体不适用于元素，则应用一些其他特定于实施的回退逻辑）
   * **内容变体** ([Contentvariation](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ContentVariation.html))

      * 获取基本数据（名称、标题、描述）
      * 获取/设置内容
      * 基于上次修改信息的简单同步

   所有三个接口( `ContentFragment`， `ContentElement`， `ContentVariation`)扩展 `Versionable` 界面，添加了内容片段所需的版本控制功能：

   * 创建新版本的元素
   * 列出元素的版本
   * 获取版本化元素的特定版本的内容







### 适应 — 使用adaptTo() {#adapting-using-adaptto}

可以调整以下内容：

* `ContentFragment` 可以适应：

   * `Resource`  — 底层Sling资源；更新底层 `Resource` 直接要求重建 `ContentFragment` 对象。

   * `Asset` - DAM `Asset` 表示内容片段的抽象；更新 `Asset` 直接要求重建 `ContentFragment` 对象。

* `ContentElement` 可以适应：

   * [`ElementTemplate`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ElementTemplate.html)  — 用于访问元素的结构信息。

* [`FragmentTemplate`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/FragmentTemplate.html)

* `Resource` 可以适应：

   * `ContentFragment`

### 注意事项 {#caveats}

应当指出：

* 整个API旨在 **非** 自动保留更改（除非在API JavaDoc中另有说明）。 因此，您必须始终提交相应请求的资源解析程序（或您实际使用的解析程序）。

* 可能需要额外工作的任务：

   * 强烈建议从以下位置创建新变体： `ContentFragment`. 这可确保所有元素都将共享此变体，并根据需要更新相应的全局数据结构，以反映内容结构中新创建的变体。

   * 通过元素删除现有变体，使用 `ContentElement.removeVariation()`，将不会更新分配给变体的全局数据结构。 要确保这些数据结构保持同步，请使用 `ContentFragment.removeVariation()` 而是全局删除变体。

## 内容片段管理API — 客户端 {#the-content-fragment-management-api-client-side}

>[!CAUTION]
>
>客户端API是内部的。

### 附加信息 {#additional-information}

请参阅以下内容：

* `filter.xml`

   此 `filter.xml` 用于内容片段管理的配置为不与Assets核心内容包重叠。

## 编辑会话 {#edit-sessions}

>[!CAUTION]
>
>请考虑此背景信息。 您不应在此更改任何内容(因为它被标记为 *专用区域* 但在某些情况下，了解事物背后的工作原理可能会有所帮助。

编辑内容片段(可以跨多个视图(=HTML页面))是原子级的。 因此，这种原子多视图编辑功能不是典型的AEM概念，内容片段使用所谓的 *编辑会话*.

当用户在编辑器中打开内容片段时，会启动编辑会话。 当用户通过选择任一选项离开编辑器时，编辑会话即完成 **保存** 或 **取消**.

从技术上讲，所有编辑都是在以下日期完成的： *实时* 内容，就像所有其他AEM编辑一样。 当编辑会话启动时，将创建当前未编辑状态的版本。 如果用户取消编辑，则该版本会恢复。 如果用户单击 **保存**，则不执行任何特定操作，因为执行所有编辑的日期为 *实时* 因此，所有更改已保留。 此外，单击 **保存** 将触发某些后台处理（例如，创建全文搜索信息和/或处理混合媒体资产）。

对于边缘情况，有一些安全措施；例如，如果用户尝试离开编辑器而不保存或取消编辑会话。 此外，还可以定期自动保存以防止数据丢失。
请注意，两个用户可以同时编辑相同的内容片段，因此可能会覆盖彼此所做的更改。 要防止出现这种情况，需要通过应用DAM管理的 *结账* 操作。

## 示例 {#examples}

### 示例：访问现有内容片段 {#example-accessing-an-existing-content-fragment}

要实现此目的，您可以使表示API的资源适应：

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

要以编程方式创建新的内容片段，您需要使用
`FragmentTemplate` 修改自模型资源。

例如：

```java
Resource modelRsc = resourceResolver.getResource("...");
FragmentTemplate tpl = modelRsc.adaptTo(FragmentTemplate.class);
ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
```

### 示例：指定自动保存间隔 {#example-specifying-the-auto-save-interval}

此 [自动保存间隔](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#save-close-and-versions) （以秒为单位）可以使用配置管理器(ConfMgr)定义：

* 节点： `<conf-root>/settings/dam/cfm/jcr:content`
* 属性名称: `autoSaveInterval`
* 类型: `Long`

* 默认： `600` （10分钟）；此时间定义于 `/libs/settings/dam/cfm/jcr:content`

如果要将自动保存间隔设置为5分钟，则需要在节点上定义属性；例如：

* 节点： `/conf/global/settings/dam/cfm/jcr:content`
* 属性名称: `autoSaveInterval`

* 类型: `Long`

* 值： `300` （5分钟等于300秒）

## 用于页面创作的组件 {#components-for-page-authoring}

有关详细信息，请参阅

* [核心组件 — 内容片段组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=zh-Hans) （推荐）
