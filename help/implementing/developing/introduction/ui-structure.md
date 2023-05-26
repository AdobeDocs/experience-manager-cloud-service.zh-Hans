---
title: AEM UI 的结构
description: AEM UI具有几个基本原则，并且由几个关键元素组成
exl-id: ac211716-d699-4fdb-a286-a0a1122c86c5
source-git-commit: 47910a27118a11a8add6cbcba6a614c6314ffe2a
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 4%

---

# AEM UI 的结构 {#structure-of-the-aem-ui}

AEM UI具有几个基本原则，并且由几个关键元素组成：

## 控制台 {#consoles}

### 基本布局和调整大小 {#basic-layout-and-resizing}

UI同时适用于移动设备和桌面设备，不过，AEM不会创建两种样式，而是使用一种适用于所有屏幕和设备的样式。

所有模块都使用相同的基本布局，在AEM中，这可以看作是：

![AEM Sites控制台](assets/ui-sites-console.png)

布局遵循响应式设计样式，并根据您所使用的设备/窗口的大小进行调整。

例如，当分辨率低于1024px（在移动设备上一样）时，显示器将相应地调整：

![站点控制台移动视图](assets/ui-sites-mobile.png)

### 标题栏 {#header-bar}

![AEM标题栏](assets/ui-header-bar.png)

标题栏显示全局元素，包括：

* 徽标以及您当前使用的特定产品/解决方案；对于AEM，这也会构成指向全局导航的链接
* 搜索
* 用于访问帮助资源的图标
* 用于访问其他解决方案的图标
* 任何等待您的警报或收件箱项目的指示器（以及对该项目的访问权限）
* 用户图标以及指向配置文件管理的链接

### 工具栏 {#toolbar}

工具栏与您的位置相关，并且会显示与控制以下页面中的视图或资产相关的工具。 工具栏是特定于产品的，但是与元素有一些共同之处。

在任意位置，工具栏都会显示当前可用的操作：

![AEM Sites工具栏](assets/ui-sites-toolbar.png)

还取决于当前是否选择了资源：

![已选择AEM Sites工具栏](assets/ui-sites-toolbar-selected.png)

### 左边栏 {#left-rail}

可以根据需要打开/隐藏左边栏以显示：

* **仅限内容**
* **内容树**
* **时间线**
* **引用**
* **过滤器**

默认为 **仅内容** （边栏隐藏）。

![左边栏](assets/ui-left-rail.png)

## 页面创作 {#page-authoring}

创作页面时，结构区域如下所示。

### 内容框架 {#content-frame}

页面内容在内容框架中呈现。 内容框架完全独立于编辑器 — 以确保不会因CSS或javascript而发生冲突。

内容框架位于窗口的右侧部分工具栏下。

![内容框架](assets/ui-content-frame.png)

### 编辑器框架 {#editor-frame}

编辑器框架可启用编辑功能。

编辑器框架是所有页面创作元素的容器（抽象）。 它位于内容框架顶部，包括：

* 顶部工具栏
* 侧面板
* 所有叠加图
* 任何其他页面创作元素；例如，组件工具栏

![编辑器框架](assets/ui-editor-frame.png)

### 侧面板 {#side-panel}

这包含三个默认选项卡。 此 **资产** 和 **组件** 选项卡允许您选择此类元素，并将它们从面板中拖放到页面上。 此 **内容树** 选项卡允许您检查页面上内容的层次结构。

默认情况下，侧面板处于隐藏状态。 选中后，它将显示在左侧，或者当窗口大小低于1024像素的宽度时（例如，在移动设备上），它滑过以覆盖整个窗口。

![侧面板](assets/ui-side-panel.png)

### 侧面板 — 资产 {#side-panel-assets}

在“资源”选项卡中，您可以从资源范围中进行选择。 您还可以根据特定术语进行筛选，或选择组。

![“资源”选项卡](assets/ui-side-panel-assets.png)

### 侧面板 — 资产组 {#side-panel-asset-groups}

在资源选项卡中，有一个下拉列表，您可以使用它选择特定的资源组。

![资产组](assets/ui-side-panel-asset-groups.png)

### 侧面板 — 组件 {#side-panel-components}

在“组件”选项卡中，您可以从组件范围中进行选择。 您还可以根据特定术语进行筛选，或选择组。

![“组件”选项卡](assets/ui-side-panel-components.png)

### 侧面板 — 内容树 {#side-panel-content-tree}

在内容树选项卡中，您可以查看页面上内容的层次结构。 单击选项卡中的条目会跳转到编辑器中的页面并选择该项目。

![内容树](assets/ui-side-panel-content-tree.png)

### 叠加 {#overlays}

这些标记覆盖内容框架，并由 [图层](#layer) 实现与组件及其内容交互（完全透明）的机制。

叠加在编辑器框架中处于活动状态（包含所有其他页面创作元素），但它们实际上叠加了内容框架中的相应组件。

![叠加](assets/ui-overlays.png)

### 图层 {#layer}

层是一个独立的功能捆绑，可以激活它来：

* 提供页面的其他视图
* 允许您处理页面和/或与之交互

这些层为整个页面提供了完善的功能，而不是为单个组件执行特定操作。

AEM附带了多个已经为页面创作实施的图层；例如，包括编辑、预览和注释图层。

>[!NOTE]
>
>层是一个强大的概念，它影响用户对页面内容的查看以及与页面内容的交互。 在开发自己的层时，您需要确保层在退出时进行清理。

### 图层切换器 {#layer-switcher}

层切换器允许您选择要使用的层。 关闭时，它表示当前使用的图层。

图层切换器可以从工具栏的下拉菜单（在窗口顶部、编辑器框架中）中使用。

![图层切换器](assets/ui-layer-switcher.png)

### 组件工具栏 {#component-toolbar}

单击时（单击一次或缓慢双击），组件的每个实例都会显示其工具栏。 工具栏包含页面上组件实例可用的特定操作（例如，复制、粘贴、打开编辑器）。

根据可用的空间，组件工具栏位于相应组件的右上角或右下角。

![组件工具栏](assets/ui-component-toolbar.png)

## 更多信息 {#further-information}

<!--For more details about the concepts around the touch-enabled UI, continue to the article [Concepts of the AEM Touch-Enabled UI](/help/sites-developing/touch-ui-concepts.md).-->

欲知更多技术信息，请参见 [JS文档集](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/jsdoc/ui-touch/editor-core/index.html) （对于页面编辑器）。
