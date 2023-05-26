---
title: 编辑器限制
description: 触屏UI中的编辑器利用叠加与iframe中限定的内容进行交互。 这种交互方式会对编辑器的使用以及开发人员造成一些限制。
exl-id: 6a4f0e43-1076-4da9-95dc-9c5bf83e30d0
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 10%

---

# 编辑器限制 {#editor-limitations}

触屏UI中的编辑器利用叠加与iframe中限定的内容进行交互。 这种交互方式会对编辑器的使用以及开发人员造成一些限制。本页总结了这些限制，并在可能的情况下提供了解决方案或变通办法。

## 功能限制 {#functional-limitations}

使用编辑器创作页面时，作者可能会遇到以下功能限制。

### 链接未激活 {#links-not-active}

时间 [编辑页面](/help/sites-cloud/authoring/fundamentals/editing-content.md)中，链接处于非活动状态。

* [切换到 **预览** 模式](/help/sites-cloud/authoring/fundamentals/editing-content.md#preview-mode) 以使用内容中的链接进行导航。

### 结构页面 {#structure-pages}

页面不能命名 `structure`. 已命名的页面 `structure` 在页面编辑器中将不可编辑。

## CSS限制 {#css-limitations}

开发人员在编辑器与CSS的交互中可能会遇到以下限制。

### 绝对定位的元素 {#absolutely-positioned-elements}

绝对定位的元素可能会导致叠加位置出现问题。

* 如果发生这种情况，请确保绝对定位元素的维度正确，因为编辑器将创建具有相同维度的叠加。

### vh单位 {#vh-units}

`vh` 不支持单位，因为iframe高度必须由AEM自动调整。

### 固定背景图像 {#fixed-background-images}

由于固定背景图像嵌入到iframe中，因此滚动时固定背景图像可能无法显示为固定。

* 选择 **查看已发布的页面** 在标题栏中，操作可正确显示页面。

### 100%高度 {#height}

页面的正文元素不支持100%高度。

* 可以通过“拉伸”body元素来实施全屏主体，具体方法如下：

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

如果body元素的第一个子元素具有边距，则可以看到边距折叠问题。

* 解决方案是在body元素级别添加clearfix，如下所示：

```xml
body:before, body:after{
    content: ' ';
    display: table;
}
```
