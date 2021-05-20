---
title: 添加页面注释
description: 许多与内容直接相关的组件允许您添加注释
exl-id: a9cb9745-8140-4795-a5f9-fb3a1a299bd8
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 100%

---

# 添加页面注释 {#adding-page-annotations}

向网站的页面中添加内容时，通常需要先经过一系列讨论，然后才实际发布网站页面。为了对此有所帮助，与内容有直接关系（举例来说，并非与布局直接相关）的许多组件都允许添加注释。

页面上的注释以彩色草图/便签显示。您（或其他用户）可以通过注释给其他作者/审阅人留下意见和/或问题。

>[!NOTE]
>
>请不要忘记，[评论](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)也可用于在页面中提供反馈。

## 注释 {#annotations}

这是一种特殊的[模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)，可用于创建和查看注释。

>[!CAUTION]
>
>删除资源（例如，组件）会删除附加到该资源的所有注释和草图，无论这些注释和草图处于整个页面的什么位置，均将如此。

>[!NOTE]
>
>根据您的要求，您还可以开发一个工作流，用于在添加、更新或删除注释时发送通知。

### 对组件添加注释 {#annotating-a-component}

在“注释”模式中可以创建、编辑、移动或删除内容的注释：

1. 编辑页面时，可以使用工具栏（右上方）中的图标进入“注释”模式：

   ![“注释”按钮](/help/sites-cloud/authoring/assets/annotations.png)

   此时，您可以查看任何现有的注释。

   >[!NOTE]
   >
   >要退出“注释”模式，请点按/单击顶部工具栏右侧的“注释”图标（x 符号）。

1. 单击/点按“添加注释”图标（工具栏左侧的加号）以开始添加注释。

   >[!NOTE]
   >
   >要停止添加注释（并返回到查看模式），请点按/单击顶部工具栏左侧的“取消”图标（用白色圆圈圈住的 x 符号）。

1. 单击/点按需要添加注释的组件（可添加注释的组件将用蓝色边框突出显示），此时将打开如下对话框：

   ![添加注释](/help/sites-cloud/authoring/assets/annotation-adding.png)

   在此，可使用相应的字段和/或图标执行以下操作：

   * 输入注释文本。
   * 创建草图（线和形状）以突出显示组件的某个区域。


      ![“注释草图”按钮](/help/sites-cloud/authoring/assets/annotation-sketch.png)

      创建草图时，光标将变成十字线。您可以绘制多条不同的线。草图线反映注释颜色，可为箭头、圆环或椭圆环。

   * 选择/更改颜色：

      ![注释色板按钮](/help/sites-cloud/authoring/assets/annotation-color-swatch.png)

   * 删除注释。

      ![注释删除按钮](/help/sites-cloud/authoring/assets/annotation-delete.png)

1. 单击/点按对话框外部可关闭注释对话框。将显示注释截断视图（第一个单词）及任何草图：

   ![注释草图](/help/sites-cloud/authoring/assets/annotation-sketches.png)

1. 完成特定注释编辑之后，您可以：

   * 单击/点按文本标记以打开注释。打开注释后，您可以查看整个文本，进行更改或删除注释。

      * 无法不考虑注释而单独删除草图。
   * 调整文本标记位置。
   * 单击/点按草图线以选择该草图，然后将其拖动到所需位置。
   * 移动或复制组件

      * 任何相关注释及其草图也会被移动或复制，它们相对于段落的位置将保持不变。


1. 要退出“注释”模式并返回之前使用的模式，请点按/单击顶部工具栏右侧的“注释”图标（x 符号）。

>[!NOTE]
>
>无法将注释添加到其他用户已锁定的页面。

>[!NOTE]
>
>单个组件类型的定义决定是否可在该组件的实例中添加注释。

## 注释指示器 {#annotation-indicator}

在“编辑”模式下不会显示注释，但工具栏右上方的徽章会显示当前页面存在的注释数。该徽章取代了默认的“注释”图标，但还可用作打开/关闭“注释”模式的快速链接：

![注释指示器](/help/sites-cloud/authoring/assets/annotation-indicator.png)

## 对其他资源添加注释 {#annotating-other-resources}

除了组件之外，您还可以对各种资源添加注释：

* 对资产添加注释[对资产添加注释](/help/assets/manage-digital-assets.md#annotating)
* 对视频资产添加注释[对视频资产添加注释](/help/assets/manage-video-assets.md#annotate-video-assets)
