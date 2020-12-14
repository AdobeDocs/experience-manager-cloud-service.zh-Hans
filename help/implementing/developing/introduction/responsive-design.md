---
title: 响应式设计
description: 通过响应式设计，可以在多个设备上以多个方向有效地显示相同的体验
translation-type: tm+mt
source-git-commit: a3b2a66958fd8d3a68b450938c5c18053f00b998
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---


# 响应式设计{#responsive-design}

设计您的体验，使其能够适应显示体验的客户端视图。 通过响应式设计，可以在多种设备上以两种方向有效地显示相同的页面。 下图演示了页面对视图端口大小更改做出响应的一些方式：

* 布局：对较小的视区使用单列布局，对较大的视区使用多列布局。
* 文本大小：在较大的视区中使用较大的文本大小（如果适用，如标题）。
* 内容：在较小的设备上显示时，仅包含最重要的内容。
* 导航：提供了用于访问其他页面的设备特定工具。
* 图像：根据窗口尺寸提供适合客户端视图的图像演绎版。

![响应式设计示例](assets/responsive-example.png)

开发Adobe Experience Manager(AEM)应用程序，它们生成可适应多种窗口大小和方向的HTML5。 例如，以下视区宽度范围与各种设备类型和方向相对应

* 最大宽度为480像素（手机、纵向）
* 最大宽度767像素（手机、横向）
* 宽度介于768像素和979像素之间（平板电脑、纵向）
* 宽度介于980和1199像素之间（平板电脑、横向）
* 宽度为1200px或更高（桌面）

有关实施响应式设计行为的信息，请参阅以下主题：

* [媒体查询](#using-media-queries)
* [流体网格](#developing-a-fluid-grid)
* [自适应图像](#using-adaptive-images)

在进行设计时，请使用&#x200B;**模拟器**&#x200B;工具栏预览页面，使其适合各种屏幕大小。

## 开发{#before-you-develop}之前

在开发支持网页的AEM应用程序之前，应该做出一些设计决策。 例如，您需要具有以下信息：

* 您所针对的设备
* 目标视区大小
* 每个目标视区大小的页面布局

### 应用程序结构{#application-structure}

典型的AEM应用程序结构支持所有响应式设计实现：

* 页面组件位于`/apps/<application_name>/components`下
* 模板位于`/apps/<application_name>/templates`下

## 使用媒体查询{#using-media-queries}

媒体查询支持选择性地使用CSS样式进行页面渲染。 AEM开发工具和功能使您能在应用程序中有效、高效地实施媒体查询。

W3C组提供[媒体查询](https://www.w3.org/TR/css3-mediaqueries/)推荐，用于描述此CSS3功能和语法。

### 创建CSS文件{#creating-the-css-file}

在CSS文件中，根据目标设备的属性定义媒体查询。 以下实施策略对于管理每个媒体查询的样式非常有效：

* 使用[客户端库文件夹](clientlibs.md)定义呈现页面时组合的CSS。
* 在单独的CSS文件中定义每个媒体查询和相关的样式。 使用表示媒体查询设备功能的文件名很有用。
* 在单独的CSS文件中定义所有设备通用的样式。
* 在“客户端库”文件夹的css.txt文件中，按照组合的CSS文件中的要求对列表CSS文件进行排序。

[WKND教程](develop-wknd-tutorial.md)使用此策略定义站点设计中的样式。 WKND使用的CSS文件位于`/apps/wknd/clientlibs/clientlib-grid/less/grid.less`。
