---
title: 配置布局容器和布局模式
description: 了解如何配置布局容器和布局模式以便为内容作者启用响应式布局。
exl-id: 469e8151-8231-4ccc-b7f6-855545f87440
solution: Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1250'
ht-degree: 3%

---

# 配置布局容器和布局模式 {#configuring-layout-container-and-layout-mode}

[响应式布局](/help/sites-cloud/authoring/page-editor/responsive-layout.md)是一种用于实现[响应式网页设计的机制。](https://en.wikipedia.org/wiki/Responsive_web_design)这允许内容作者创建其布局和维度与其用户使用的设备相关的网页。

AEM 使用一组机制为页面实现响应式布局：

* **[布局容器](/help/sites-cloud/authoring/page-editor/responsive-layout.md#adding-a-layout-container-and-its-content-edit-mode)** — 此组件提供了一个网格段落系统，允许您在响应式网格内添加和放置组件。
   * 它可以用作页面的默认Parsys，和/或在组件浏览器中提供给作者。
   * 在`/libs/wcm/foundation/components/responsivegrid`下定义了默认&#x200B;**布局容器**&#x200B;组件。
   * 您可以定义布局容器：
      * 作为用户可以添加到页面中的组件。
      * 作为页面的默认parsys。
      * 作为组件和默认Parsys。
         * 您可以将布局容器作为页面的标准，同时允许用户在此中添加更多布局容器；例如，实现列控件。
* **[布局模式](/help/sites-cloud/authoring/page-editor/introduction.md#mode-selector)** — 将布局容器放置到页面上后，就可以使用&#x200B;**布局**&#x200B;模式在响应式网格内放置内容。
* **[模拟器](/help/sites-cloud/authoring/page-editor/responsive-layout.md#selecting-a-device-to-emulate)** — 允许您通过以交互方式调整组件大小来创建和编辑响应式网站，这些网站会根据设备/窗口大小重新排列布局。 随后，用户可以使用模拟器查看内容的呈现方式。

通过这些响应式网格机制，您可以：

* 使用断点（指示设备分组）根据设备布局定义不同的内容行为。
* 根据设备组隐藏组件（定义将隐藏组件的断点）。
* 使用水平对齐网格功能（将组件放入网格中，根据需要调整大小，定义它们何时应该折叠/重排成并排或上下对齐）。
* 实现列控件。

>[!NOTE]
>
>从[项目原型](#addlink)或从[标准站点模板](#addlink)创建站点时，通常会配置响应式布局。 否则，您必须为页面[激活布局容器组件](#enable-the-layout-container-component-for-page)。

## 启用模拟器 {#enabling-emulator}

已启用[项目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)和[标准站点模板](/help/sites-cloud/administering/site-creation/site-templates.md#standard-site-template)以使用模拟器。 如果您开发自己的内容不是基于核心组件或原型，请参阅文档[响应式设计](/help/implementing/developing/introduction/responsive-design.md)，了解如何在利用这些功能的同时开发组件的详细信息。

## 激活网站的布局模式 {#activate-layout-mode-for-your-site}

**布局**&#x200B;模式允许您使用模拟器为不同设备调整内容的布局。 已为&#x200B;**布局**&#x200B;模式启用WKND示例站点。 按照以下步骤启用您自己的站点。

### 配置断点 {#configure-breakpoints}

断点对于响应式设计至关重要，它定义了将内容调整到目标设备的方式和时间。 但是，请务必谨慎，因为您引入的每个断点都会为作者生成额外的工作，以适应内容。 很多情况下，两个断点就足够了，其中包括始终存在的默认断点。 Adobe建议不要创建超过三个断点，包括默认值，即在`cq:responsive/breakpoint`下创建不超过两个节点。

* 断点具有标题和宽度：
   * 标题描述了通用设备分组，并根据需要提供了方向。
      * 例如，`phone`，`tablet`
   * 宽度定义该通用设备分组的最大宽度（以像素为单位）。
      * 例如，如果断点电话的宽度为768，则表示它是用于电话设备的最大布局宽度。
* 可以定义断点：
   * 在页面模板上，设置会从中复制到使用该模板创建的任何页面。
   * 在页面节点上，任何子页面都会从中继承设置。
* 使用模拟器时，断点将作为标记显示在页面编辑器的顶部。
* 断点继承自父节点层次结构，可以随意覆盖。
* 有一个默认（开箱即用）断点，它涵盖了上次配置断点之上的所有内容。
* 可以使用CRXDE Lite或XML定义断点。

新项目和现有项目都应考虑断点。

* 如果您正在设置新项目，则应该向模板添加断点。
* 如果要迁移现有项目（包含现有内容），您必须：
   * 向模板添加断点。
   * 将相同的断点添加到现有页面。

由于继承关系，您只需对内容的根页面执行此操作。

#### 使用CRXDE Lite配置断点 {#configuring-breakpoints-using-crxde-lite}

1. 使用CRXDE Lite，导航到：

   * 您的模板定义。
   * 页面的`jcr:content`节点。

1. 在`jcr:content`下创建节点：

   * 名称：`cq:responsive`
   * 类型：`nt:unstructured`

1. 在此下创建节点：

   * 名称：`breakpoints`
   * 类型：`nt:unstructured`

1. 在断点节点下，可以创建任意数量的断点。 每个定义都是一个具有以下属性的节点：

   * 名称：`<descriptive name>`
   * 类型：`nt:unstructured`
   * 标题： `String <descriptive title seen in Emulator>`
   * 宽度： `Decimal <value of breakpoint>`

#### 使用XML配置断点 {#configuring-breakpoints-using-xml}

断点位于`.context.html`的`<jcr:content>`部分中，位于相应的模板（或内容）文件夹下。

示例定义：

```xml
<cq:responsive jcr:primaryType="nt:unstructured">
  <breakpoints jcr:primaryType="nt:unstructured">
    <phone jcr:primaryType="nt:unstructured" title="{String}Phone" width="{Decimal}768"/>
    <tablet jcr:primaryType="nt:unstructured" title="{String}Tablet" width="{Decimal}1200"/>
  </breakpoints>
</cq:responsive>
```

## 为页面启用组件调整大小 {#enable-component-resizing-for-the-page}

在&#x200B;**布局**&#x200B;模式下调整组件大小是响应式设计的重要组成部分，可在WKND示例站点中使用。 按照以下步骤启用您自己的站点。

### 将布局容器设置为主Parsys {#set-layout-container-as-main-parsys}

要将页面的main parsys设置为布局容器，请将parsys定义为：

`wcm/foundation/components/responsivegrid`

在：

* 页面组件
* 页面模板（供将来使用）

以下两个示例说明了定义：

* **HTL：**

  ```xml
  <sly data-sly-resource="${'par' @ resourceType='wcm/foundation/components/responsivegrid'}/>
  ```

* **JSP：**

  ```xml
  <cq:include path="par" resourceType="wcm/foundation/components/responsivegrid" />
  ```

### 包含响应式CSS {#include-the-responsive-css}

#### 使用LESS的断点的CSS {#css-for-breakpoints-using-less}

AEM使用LESS来生成必要的CSS部分，这些项目需要包含在您的项目中。

您必须创建一个[客户端库](/help/implementing/developing/introduction/clientlibs.md)以提供额外的配置和函数调用。 以下LESS提取是您必须添加到项目的最小值示例：

```java
@import (once) "/libs/wcm/foundation/clientlibs/grid/grid_base.less";

/* maximum amount of grid cells to be provided */
@max_col: 12;

/* default breakpoint */
.aem-Grid {
  .generate-grid(default, @max_col);
}

/* phone breakpoint */
@media (max-width: 768px) {
  .aem-Grid {
    .generate-grid(phone, @max_col);
  }
}

/* tablet breakpoint */
@media (min-width: 769px) and (max-width: 1200px) {
  .aem-Grid {
    .generate-grid(tablet, @max_col);
  }
}
```

可在以下位置找到基本网格定义：

`/libs/wcm/foundation/clientlibs/grid/grid_base.less`

#### 样式设置注意事项 {#styling-considerations}

保持在响应容器内的组件(连同它们各自的HTMLDOM元素)根据响应栅格大小而调整大小。 因此，在这些情况下，建议避免（或更新）固定宽度（包含）DOM元素的定义。

例如：

* 之前：

   * `width=100px`

* 之后：

   * `max-width=100px`

#### 调整大小和自适应图像合规性 {#resizing-and-adaptive-image-compliance}

网格中组件的任何大小调整都将相应地触发以下监听器：

* `beforeedit`
* `beforechildedit`
* `afteredit`
* `afterchildedit`

要正确调整响应式网格中包含的自适应图像的大小并更新其内容，您需要将设置为`REFRESH_PAGE`的`afterEdit`侦听器添加到每个包含组件的`EditConfig`文件中。

例如：

`<cq:listeners jcr:primaryType="cq:EditListenersConfig" afteredit="REFRESH_PAGE" />`

该自适应图像机制可通过控制为窗口的当前大小选择正确图像的脚本来提供。 它在DOM准备就绪或收到专用事件时激活。 当前必须刷新页面才能正确反映用户操作的结果。

>[!CAUTION]
>
>自定义样式表客户端库必须作为标头的一部分加载，它们才能在创作和发布中正常工作。

## 为页面启用布局容器组件 {#enable-the-layout-container-component-for-page}

要获得有效的响应式布局，内容作者必须能够将布局容器组件的实例拖动到页面上。 WKND示例站点已经启用了此功能。 按照以下步骤启用您自己的站点。

### 启用布局容器组件以进行页面编辑 {#enable-the-layout-container-component-for-page-editing}

要允许作者向内容页面添加更多响应式网格，您需要为页面启用布局容器组件。 您可以使用以下任一方式执行此操作：

* **通过创作环境** - [编辑页面模板](/help/sites-cloud/authoring/sites-console/templates.md)以启用页面的布局容器。
* **组件定义** — 在定义组件时使用`allowedComponent`或静态包含。

### 配置布局容器的网格 {#configure-the-grid-of-the-layout-container}

您可以通过编辑页面模板来配置布局容器[的每个特定实例的可用列数。](/help/sites-cloud/authoring/sites-console/templates.md)
