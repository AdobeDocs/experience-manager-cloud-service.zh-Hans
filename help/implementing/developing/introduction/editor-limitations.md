---
title: 编辑器限制
description: 触屏优化UI中的编辑器利用叠加与iframe中限制的内容交互。 此交互在编辑器的使用方面以及对于开发人员而言都有一些限制。
translation-type: tm+mt
source-git-commit: fee73b5f5ba69422494efe554ac5aa62c046ad86
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 0%

---


# 编辑器限制 {#editor-limitations}

触屏优化UI中的编辑器利用叠加与iframe中限制的内容交互。 此交互在编辑器的使用方面以及对于开发人员而言都有一些限制。 本页概括了这些限制，并尽可能提供解决方案或解决办法。

## 功能限制 {#functional-limitations}

使用编辑器创作页面时，作者可能会遇到以下功能限制。

### 链接不活动 {#links-not-active}

编辑 [页面时](/help/sites-cloud/authoring/fundamentals/editing-content.md)，链接不处于活动状态。

* [切换到 **预览** 模式](/help/sites-cloud/authoring/fundamentals/editing-content.md#preview-mode) ，以使用内容中的链接进行导航。

### 结构页面 {#structure-pages}

无法命名页面 `structure`。 命名的页面 `structure` 在页面编辑器中不可编辑。

## CSS限制 {#css-limitations}

开发人员在编辑器与CSS的交互时可能会遇到以下限制。

### 绝对定位元素 {#absolutely-positioned-elements}

绝对定位的元素可能导致其叠加位置出现问题。

* 如果发生这种情况，请确保绝对定位元素的尺寸正确，因为编辑器将创建尺寸完全相同的叠加。

### V Units {#vh-units}

`vh` 不支持iframe高度，因为AEM必须自动调整iframe高度。

### 固定背景图像 {#fixed-background-images}

由于固定背景图像嵌入在iframe中，因此在滚动时，固定背景图像可能不显示为固定。

* 在标 **题栏操作中** ，选择视图页面作为已发布页面时，将正确显示页面。

### 100% Height {#height}

页面的正文元素不支持100%高度。

* 为了实现全屏机身，可进行如下“拉伸”机身元素：

```xml
body {
    position: absolute;
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
}
```

### 边距折叠 {#margin-collapsing}

如果主体元素的第一个子元素具有边距，则可以看到边距折叠问题。

* 解决方案是在主体元素级别添加一个清除器，如：

```xml
body:before, body:after{
    content: ' ';
    display: table;
}
```
