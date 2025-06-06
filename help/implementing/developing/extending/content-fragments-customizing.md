---
title: 自定义和扩展内容片段
description: 内容片段扩展了标准资产。 了解如何对其进行自定义。
exl-id: 58152d6e-21b6-4f45-a45c-0f46ee58825e
feature: Developing, Content Fragments
role: Admin, Architect, Developer
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '1689'
ht-degree: 1%

---

# 自定义和扩展内容片段{#customizing-and-extending-content-fragments}

在Adobe Experience Manager as a Cloud Service中，内容片段扩展了标准资源；请参阅：

* [创建和管理内容片段](/help/sites-cloud/administering/content-fragments/overview.md)和使用内容片段进行[页面创作](/help/sites-cloud/authoring/fragments/content-fragments.md)，以获取有关内容片段的更多信息。

* [管理Assets](/help/assets/manage-digital-assets.md)，以获取有关标准资源的详细信息。

## 架构 {#architecture}

内容片段的基本[组成部分](/help/sites-cloud/administering/content-fragments/overview.md#constituent-parts-of-a-content-fragment)如下：

* *内容片段*&#x200B;本身
* 它包含一个或多个&#x200B;*内容元素*
* 它可以有一个或多个&#x200B;*内容变体*

单个内容片段基于内容片段模型：

* 内容片段模型在创建内容片段时定义其结构。
* 片段引用模型；因此，对模型的更改可能会影响或确实影响任何依赖的片段。
* 模型由数据类型构建。
* 用于添加新变体的函数等，必须相应地更新片段。

  >[!NOTE]
  >
  >要显示/呈现内容片段，您的帐户必须具有模型的`read`权限。

  >[!CAUTION]
  >
  >对现有内容片段模型所做的任何更改都会影响从属片段；这可能会导致这些片段中的属性孤立。

### Sites与Assets集成 {#integration-of-sites-with-assets}

内容片段管理(CFM)是Adobe Experience Manager (AEM) Assets的一部分，如下所示：

* 内容片段是资产。
* 它们使用现有的Assets功能。
* 它们与Assets（Admin Console等）完全集成。

内容片段被视为一项AEM Sites功能，如下所示：

* 在创作页面时将使用它们。

#### 将内容片段映射到Assets {#mapping-content-fragments-to-assets}

![内容片段到资产](assets/content-fragment-to-assets.png)

基于内容片段模型的内容片段将映射到单个资源：

* 所有内容都存储在资源的`jcr:content/data`节点下：

   * 元素数据存储在主子节点下：

     `jcr:content/data/master`

   * 变体存储在子节点下，该子节点带有变体的名称：
例如，`jcr:content/data/myvariation`

   * 每个元素的数据作为具有元素名称的属性存储在相应的子节点中：
例如，元素`text`的内容作为属性`text`存储在`jcr:content/data/master`上

* 元数据和关联内容存储在`jcr:content/metadata`下
除了标题和描述，它们不被视为传统元数据并存储在`jcr:content`上

#### 资产位置 {#asset-location}

与标准资产一样，内容片段位于下：

`/content/dam`

#### 资源权限 {#asset-permissions}

请参阅[内容片段 — 删除注意事项](/help/sites-cloud/administering/content-fragments/delete-considerations.md)。

#### 功能集成 {#feature-integration}

要与Assets核心集成，请执行以下操作：

* 内容片段管理(CFM)功能以Assets核心为基础。

* CFM为卡片/列/列表视图中的项目提供自己的实施；这些实施可以插入现有的Assets内容呈现实施。

* 扩展了多个Assets组件以满足内容片段的需求。

### 在页面中使用内容片段 {#using-content-fragments-in-pages}

>[!CAUTION]
>
>[内容片段组件是核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=zh-Hans)的一部分。 有关详细信息，请参阅[开发核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html?lang=zh-Hans)。

可以从AEM页面引用内容片段，就像任何其他资源类型一样。 AEM提供了&#x200B;**[内容片段核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=zh-Hans)** — 一个[组件，它允许您在页面上包含内容片段](/help/sites-cloud/authoring/fragments/content-fragments.md#adding-a-content-fragment-to-your-page)。 您还可以扩展此&#x200B;**[内容片段](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html?lang=zh-Hans)**&#x200B;核心组件。

* 组件使用`fragmentPath`属性引用实际内容片段。 `fragmentPath`属性的处理方式与其他资产类型的类似属性相同；例如，当内容片段移动到其他位置时。

* 利用组件，可选择要显示的变体。

* 此外，可以选择一系列段落以限制输出；例如，这可用于多列输出。

* 该组件允许中间内容：

   * 在本例中，通过组件，您可以在引用片段的段落之间放置其他资产（图像等）。

   * 对于中间内容：

      * 请注意引用不稳定的可能性。 中间内容（在创作页面时添加）与位于其旁边的段落没有固定关系。 如果在中间内容的位置之前插入新段落（在内容片段编辑器中），可能会丢失相对位置。

      * 考虑使用其他参数（如变体和段落过滤器）来配置在页面上渲染的内容。

>[!NOTE]
>
>**内容片段模型：**
>
>在页面上使用内容片段时，将引用它所基于的内容片段模型。
>
>这意味着，如果在您发布页面时模型尚未发布，则会标记此状态并将模型添加到要与页面一起发布的资源。

### 与其他框架集成 {#integration-with-other-frameworks}

内容片段可以与集成：

* **翻译**

  内容片段已与[AEM翻译工作流](/help/sites-cloud/administering/translation/overview.md)完全集成。 在架构方面，这意味着：

   * 内容片段的各个翻译是单独的片段；例如：

      * 它们位于不同的语言根下，但共享相关语言根下的相对路径：

        `/content/dam/<path>/en/<to>/<fragment>`

        对比

        `/content/dam/<path>/de/<to>/<fragment>`

   * 除了基于规则的路径之外，内容片段的不同语言版本之间没有其他连接。 虽然UI提供了在语言变体之间导航的方法，但它们作为两个单独的片段处理。

  >[!NOTE]
  >
  >AEM翻译工作流适用于`/content`：
  >
  >* 由于内容片段模型驻留在`/conf`中，因此这些翻译中不包含这些模型。 您可以将UI字符串国际化。

* **元数据架构**

   * 内容片段使用并重用可用标准资源定义的[元数据架构](/help/assets/metadata-schemas.md)。

   * CFM提供了自己的特定架构：

     `/libs/dam/content/schemaeditors/forms/contentfragment`

     如有必要，可以扩展此功能。

   * 相应的架构表单与片段编辑器集成。

## 内容片段管理API — 服务器端 {#the-content-fragment-management-api-server-side}

您可以使用服务器端API访问内容片段；请参阅：

[com.adobe.cq.dam.cfm](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/package-summary.html#package.description)

>[!CAUTION]
>
>Adobe建议使用服务器端API，而不是直接访问内容结构。

### 关键界面 {#key-interfaces}

以下三个接口可用作入口点：

* **内容片段** ([ContentFragment](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html))

  利用此界面，您可以以抽象方式处理内容片段。

  该界面为您提供了以下方法：

   * 管理基本数据（例如，获取名称；获取/设置标题/描述）
   * 访问元数据
   * 访问元素：

      * 列出元素
      * 按名称获取元素
      * 创建元素（请参阅[注意事项](#caveats)）

      * 访问元素数据（请参阅`ContentElement`）

   * 为片段定义的列表变量
   * 全局创建变量
   * 管理关联内容：

      * 列出收藏集
      * 添加收藏集
      * 移除收藏集

   * 访问片段的模型

  表示片段的主元素的接口包括：

   * **Content元素** ([ContentElement](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ContentElement.html))

      * 获取基本数据（名称、标题、描述）
      * 获取/设置内容
      * 访问元素的变体：

         * 列表变量
         * 按名称获取变体
         * 创建变体（请参阅[注意事项](#caveats)）
         * 删除变体（请参阅[注意事项](#caveats)）
         * 访问变量数据（请参阅`ContentVariation`）

      * 解决变体的快捷方式（如果指定的变体不适用于元素，则应用一些其他特定于实施的回退逻辑）

   * **内容变量** ([ContentVariation](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ContentVariation.html))

      * 获取基本数据（名称、标题、描述）
      * 获取/设置内容
      * 简单同步，基于上次修改的信息

  所有三个接口(`ContentFragment`、`ContentElement`、`ContentVariation`)都扩展了`Versionable`接口，这添加了内容片段所需的版本控制功能：

   * 创建元素的版本
   * 列出元素的版本
   * 获取版本化元素的特定版本的内容

### 适应 — 使用adaptTo() {#adapting-using-adaptto}

可以调整以下内容：

* `ContentFragment`可以适应：

   * `Resource` — 基础Sling资源；直接更新基础`Resource`需要重建`ContentFragment`对象。

   * `Asset` — 表示内容片段的DAM `Asset`抽象；直接更新`Asset`需要重新生成`ContentFragment`对象。

* `ContentElement`可以适应：

   * [`ElementTemplate`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ElementTemplate.html) — 用于访问元素的结构信息。

* [`FragmentTemplate`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/FragmentTemplate.html)

* `Resource`可以适应：

   * `ContentFragment`

### 注意事项 {#caveats}

应当指出：

* 整个API设计为&#x200B;**而非**&#x200B;自动保留更改（除非在API JavaDoc中另有说明）。 因此，请始终提交相应请求的资源解析程序（或您实际使用的解析程序）。

* 可能需要额外工作的任务：

   * Adobe建议您从`ContentFragment`创建变体。 这可确保所有元素都共享此变化，并根据需要更新适当的全局数据结构以反映内容结构中的新变化。

   * 使用`ContentElement.removeVariation()`通过元素删除现有变体不会更新分配给变体的全局数据结构。 要确保这些数据结构保持同步，请改用`ContentFragment.removeVariation()`，这样会全局删除变体。

## 内容片段管理API — 客户端 {#the-content-fragment-management-api-client-side}

>[!CAUTION]
>
>客户端API是内部的。

### 附加信息 {#additional-information}

请参阅以下内容：

* `filter.xml`

  用于内容片段管理的`filter.xml`已配置为不与Assets核心内容包重叠。

## 编辑会话 {#edit-sessions}

>[!CAUTION]
>
>请参考此背景信息。 您不应在此更改任何内容（因为它在存储库中标记为&#x200B;*私有区域*），但有时它可能会有助于了解内容背后的工作原理。

编辑内容片段(可以跨越多个视图(=HTML页面))是原子级的。 因此，原子多视图编辑功能不是典型的AEM概念，内容片段使用称为&#x200B;*编辑会话*&#x200B;的内容。

当用户在编辑器中打开内容片段时，会启动编辑会话。 当用户通过选择&#x200B;**保存**&#x200B;或&#x200B;**取消**&#x200B;离开编辑器时，编辑会话已完成。

从技术上讲，所有编辑都在&#x200B;*实时*&#x200B;内容上完成，就像所有其他AEM编辑一样。 启动编辑会话时，将创建当前未编辑状态的版本。 如果用户取消编辑，则会恢复该版本。 如果用户单击“保存”**&#x200B;**，则不会执行任何特定操作，因为编辑是在&#x200B;*实时*&#x200B;内容上运行的，因此所有更改已保留。 此外，单击&#x200B;**保存**&#x200B;将触发一些后台处理，例如创建全文搜索信息或处理混合媒体资产，或同时触发两者。

对于边缘情况，有一些安全措施；例如，如果用户尝试离开编辑器而不保存或取消编辑会话。 此外，还可以定期自动保存以防止数据丢失。
两个用户可以同时编辑相同的内容片段，因此会覆盖彼此的更改。 要防止出现这种情况，必须通过对内容片段应用DAM管理的*签出*&#x200B;操作来锁定内容片段。

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

### 示例：创建内容片段 {#example-creating-a-new-content-fragment}

要以编程方式创建内容片段，请使用从模型资源中修改的`FragmentTemplate`。

例如：

```java
Resource modelRsc = resourceResolver.getResource("...");
FragmentTemplate tpl = modelRsc.adaptTo(FragmentTemplate.class);
ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
```

### 示例：指定自动保存时间间隔 {#example-specifying-the-auto-save-interval}

可以使用配置管理器(ConfMgr)定义[自动保存间隔](/help/sites-cloud/administering/content-fragments/managing.md#save-close-and-versions)（以秒为单位）：

* 节点： `<conf-root>/settings/dam/cfm/jcr:content`
* 属性名称： `autoSaveInterval`
* 类型：`Long`

* 默认值： `600` （10分钟）；此默认值在`/libs/settings/dam/cfm/jcr:content`上定义

如果要将自动保存间隔设置为5分钟，请在节点上定义属性。

例如：

* 节点： `/conf/global/settings/dam/cfm/jcr:content`
* 属性名称： `autoSaveInterval`

* 类型：`Long`

* 值： `300`（5分钟等于300秒）

## 用于页面创作的组件 {#components-for-page-authoring}

有关更多信息，请参阅

* [核心组件 — 内容片段组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=zh-Hans) （推荐）
