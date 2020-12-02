---
title: AEM UI的结构
description: AEM UI具有几个基本原则，由几个关键元素组成
translation-type: tm+mt
source-git-commit: 0799a817095558edd49b53ddc915c9474181fef7
workflow-type: tm+mt
source-wordcount: '915'
ht-degree: 2%

---


# AEM UI的结构{#structure-of-the-aem-ui}

AEM UI具有几个基本原则，由几个关键元素组成：

## 控制台 {#consoles}

### 基本布局和大小调整{#basic-layout-and-resizing}

UI适合移动和桌面设备，但AEM使用一种适用于所有屏幕和设备的样式，而不是创建两种样式。

所有模块都使用相同的基本布局，在AEM中，这可以看作：

![AEM Sites控制台](assets/ui-sites-console.png)

布局采用响应式设计样式，并会根据您所使用的设备／窗口的大小调整自身。

例如，当分辨率低于1024px（如在移动设备上）时，将相应地调整显示屏：

![站点控制台移动视图](assets/ui-sites-mobile.png)

### 标题栏 {#header-bar}

![AEM标题栏](assets/ui-header-bar.png)

标题栏显示全局元素，包括：

* 您当前使用的徽标和特定产品／解决方案；对于AEM，它还构成指向全局导航的链接
* 搜索
* 访问帮助资源的图标
* 用于访问其他解决方案的图标
* 等待您的任何警报或收件箱项目的指示器（并可以访问）
* 用户图标，以及指向用户档案管理的链接

### 工具栏 {#toolbar}

工具栏与您的位置相关，并显示与控制下面页面中的视图或资产相关的工具。 工具栏特定于产品，但元素有一些通用性。

在任何位置，工具栏都会显示当前可用的操作：

![AEM Sites工具栏](assets/ui-sites-toolbar.png)

还取决于当前是否选择了某个资源：

![已选择AEM Sites工具栏](assets/ui-sites-toolbar-selected.png)

### 左边栏 {#left-rail}

可根据需要打开／隐藏左边栏以显示：

* **仅限内容**
* **内容树**
* **时间轴**
* **引用**
* **筛选器**

默认值为&#x200B;**仅限内容**（边栏隐藏）。

![左边栏](assets/ui-left-rail.png)

## 页面创作 {#page-authoring}

创作页面时，结构区域如下所示。

### 内容帧{#content-frame}

页面内容会呈现在内容框架中。 内容框架完全独立于编辑器——确保不会因CSS或javascript而发生冲突。

内容框架位于窗口的右侧部分工具栏下。

![内容框架](assets/ui-content-frame.png)

### 编辑器帧{#editor-frame}

编辑器框架支持编辑功能。

编辑器框架是所有页面创作元素的容器（摘要）。 它位于内容框架的顶部，包括：

* 顶部工具栏
* 侧面板
* 所有叠加
* 任何其他页面创作元素；例如，组件工具栏

![编辑器框架](assets/ui-editor-frame.png)

### 侧面板{#side-panel}

它包含三个默认选项卡。 **资产**&#x200B;和&#x200B;**组件**&#x200B;选项卡允许您选择这些元素，并将它们从面板拖放到页面上。 **内容树**&#x200B;选项卡允许您检查页面上的内容层次结构。

侧面板默认为隐藏。 选择后，窗口将显示在左侧，或者当窗口大小低于1024px的宽度时，它将滑过以覆盖整个窗口；例如，在移动设备上。

![侧面板](assets/ui-side-panel.png)

### 侧面板——资产{#side-panel-assets}

在“资产”选项卡中，您可以从资产范围中进行选择。 您还可以过滤特定术语或选择组。

![“资产”选项卡](assets/ui-side-panel-assets.png)

### 侧面板——资产组{#side-panel-asset-groups}

在资产选项卡中，您可以使用下拉列表选择特定的资产组。

![资产组](assets/ui-side-panel-asset-groups.png)

### 侧面板——组件{#side-panel-components}

在组件选项卡中，您可以从组件范围中进行选择。 您还可以过滤特定术语或选择组。

![组件选项卡](assets/ui-side-panel-components.png)

### 侧面板——内容树{#side-panel-content-tree}

在内容树选项卡中，您可以视图页面上的内容层次结构。 单击选项卡中的条目将跳转至编辑器中页面上的项目并进行选择。

![内容树](assets/ui-side-panel-content-tree.png)

### 叠加{#overlays}

这些组件覆盖内容框架，并由[层](#layer)使用，以了解如何与组件及其内容进行（完全透明）交互的机制。

叠加位于编辑器框架中（与所有其他页面创作元素一起），但实际上它们叠加了内容框架中的相应组件。

![叠加](assets/ui-overlays.png)

### 层{#layer}

图层是可以激活的独立功能束，用于：

* 提供页面的其他视图
* 允许您处理页面和／或与页面交互

图层为整个页面提供复杂的功能，而不是对单个组件执行特定操作。

AEM附带有已用于页面创作的多个层；例如，编辑、预览和注释图层。

>[!NOTE]
>
>图层是一个强大的概念，它影响用户对页面内容的视图以及与页面内容的交互。 在开发您自己的图层时，您需要确保该图层在退出时清理干净。

### 层切换器{#layer-switcher}

图层切换器允许您选择要使用的图层。 关闭时，它指示当前正在使用的层。

图层切换器可从工具栏（位于窗口顶部，在编辑器框架中）下拉出。

![图层切换器](assets/ui-layer-switcher.png)

### 组件工具栏 {#component-toolbar}

单击组件时，每个实例都将显示其工具栏(单击一次或慢速多次单击)。 工具栏包含特定操作（例如，复制、粘贴、打开编辑器），这些操作对页面上的组件实例可用。

组件工具栏位于相应组件的右上角或右下角，具体取决于可用空间。

![组件工具栏](assets/ui-component-toolbar.png)

## 更多信息 {#further-information}

<!--For more details about the concepts around the touch-enabled UI, continue to the article [Concepts of the AEM Touch-Enabled UI](/help/sites-developing/touch-ui-concepts.md).-->

有关更多技术信息，请参阅页面编辑器的[JS文档集](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/jsdoc/ui-touch/editor-core/index.html)。
