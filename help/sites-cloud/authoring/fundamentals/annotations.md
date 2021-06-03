---
title: 添加页面注释
description: 使用注释模式在页面上保留注释和草图，就像使用附注来协助内容审阅过程一样
exl-id: a9cb9745-8140-4795-a5f9-fb3a1a299bd8
source-git-commit: 5d533354a29237aeafc00e5570ede3ab00b721fd
workflow-type: tm+mt
source-wordcount: '700'
ht-degree: 35%

---

# 添加页面注释 {#adding-page-annotations}

创建数字体验的内容通常需要在发布之前进行讨论和提供反馈。 为了帮助完成此反馈过程，AEM允许您向内容添加注释。

页面上的注释会放置简单的草图或便笺（想想现实世界的便签）。 注释允许您为其他作者和审阅人留下意见或问题。

>[!TIP]
>
>请不要忘记，[评论](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)也可用于在页面中提供反馈。

这是一种特殊的[模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)，可用于创建和查看注释。

>[!TIP]
>
>根据您的要求，您还可以开发[工作流](/help/sites-cloud/authoring/workflows/overview.md)，以在添加、更新或删除注释时发送通知。

## 注释指示器 {#annotation-indicator}

在“编辑”模式下不会显示注释，但工具栏右上方的徽章会显示当前页面存在的注释数。该徽章取代了默认的“注释”图标，但还可用作打开/关闭“注释”模式的快速链接：

![注释指示器](/help/sites-cloud/authoring/assets/annotation-indicator.png)

## 注释模式{#annotate-mode}

注释仅在“注释”模式下可见。

1. 编辑页面时，使用工具栏（右上方）中的图标进入注释模式：

   ![“注释”按钮](/help/sites-cloud/authoring/assets/annotations.png)

   此时，您可以查看任何现有的注释。

   ![注释示例](/help/sites-cloud/authoring/assets/annotation-sketches.png)

1. 单击或点按注释以打开注释对话框并查看其详细信息。

   ![注释详细信息](/help/sites-cloud/authoring/assets/annotation-sketches.png)

1. 要退出“注释”模式并返回到之前使用的模式，请点按/单击顶部工具栏右侧的x按钮。

## 添加和编辑注释{#annotating-a-component}

除了查看注释之外，在注释模式下，您还可以创建、编辑、移动或删除内容的注释

1. [在页面上](#annotate-mode) 开始注释模式。

1. 单击或点按“添加注释”图标（工具栏左侧的加号）以开始添加注释。

1. 单击或点按所需的组件（可添加注释的组件将以蓝色边框突出显示）以添加注释并打开对话框：

   ![添加注释](/help/sites-cloud/authoring/assets/annotation-adding.png)

   在此，可使用相应的字段和/或图标执行以下操作：

   * 输入注释文本。
   * 创建草图（线和形状）以突出显示组件的某个区域。


      ![“注释草图”按钮](/help/sites-cloud/authoring/assets/annotation-sketch.png)

      创建草图时，光标将变成十字线。您可以绘制多条不同的线。草图线反映注释颜色，可为箭头、圆环或椭圆环。

   * 选择或更改颜色：

      ![注释色板按钮](/help/sites-cloud/authoring/assets/annotation-color-swatch.png)

1. 单击或点按对话框外部可关闭注释对话框。 将显示注释的截断视图以及任何草图：

   ![注释草图](/help/sites-cloud/authoring/assets/annotation-sketches.png)

1. 完成特定注释编辑之后，您可以：

   * 单击或点按文本标记以打开注释。 打开后，您可以查看全文，进行更改，或[删除注释。](#deleting-annotations)
   * 调整文本标记位置。
   * 单击或点按草图线以选择该草图，然后将其拖动到所需位置。
   * 移动或复制组件
      * 也会移动或复制任何相关注释及其草图，但它们相对于段落的位置将保持不变。


>[!NOTE]
>
>无法将注释添加到其他用户已锁定的页面。

>[!NOTE]
>
>单个组件类型的定义决定是否可在该组件的实例中添加注释。

## 删除注释和草图{#deleting-annotations}

可以删除注释及其关联的草图。

1. [在页面上](#annotate-mode) 开始注释模式。

1. 单击/点按文本标记以打开注释。

1. 单击或点按删除图标。

   ![删除注释](/help/sites-cloud/authoring/assets/annotation-delete.png)

1. 注释和所有关联的草图都将被删除。

>[!NOTE]
>
>删除组件会删除附加到该资源的所有注释和草图，无论这些注释和草图处于整个页面的什么位置，均将如此。

## 仅删除草图{#deleting-sketches}

只能删除特定草图，而不能删除包含所有关联草图的整个注释。

1. [在页面上](#annotate-mode) 开始注释模式。

1. 单击或点按草图。 AEM用较深的蓝色框突出显示它。

   ![选择要删除的草图](/help/sites-cloud/authoring/assets/annotation-sketch-delete.png)

1. 按键盘上的Delete键。

1. 草图已删除，但注释仍保留。

## 对其他资源添加注释 {#annotating-other-resources}

除了组件之外，您还可以对各种资源添加注释：

* 对资产添加注释[对资产添加注释](/help/assets/manage-digital-assets.md#annotating)
* 对视频资产添加注释[对视频资产添加注释](/help/assets/manage-video-assets.md#annotate-video-assets)
