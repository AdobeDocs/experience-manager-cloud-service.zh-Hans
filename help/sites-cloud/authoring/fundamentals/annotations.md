---
title: 添加页面注释
description: 使用注释模式可像使用便笺一样在页面上留下注释和草图，协助您的内容审阅过程
exl-id: a9cb9745-8140-4795-a5f9-fb3a1a299bd8
source-git-commit: 64d801b108229866394e993811a67f983be5df6c
workflow-type: ht
source-wordcount: '699'
ht-degree: 100%

---

# 添加页面注释 {#adding-page-annotations}

为数字体验创作内容一般都需要进行反复讨论和反馈后再发布。为了帮助进行此反馈过程，AEM 允许您将注释添加到内容。

注释可在页面上放置简单的草图或便笺（想象一下现实世界的便笺）。通过注释，可为其他作者和审阅者留下评论或问题。

>[!TIP]
>
>请不要忘记，[评论](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)也可用于在页面中提供反馈。

这是一种特殊的[模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)，可用于创建和查看注释。

>[!TIP]
>
>根据要求，还可制定[工作流](/help/sites-cloud/authoring/workflows/overview.md)以在添加、更新或删除注释时发送通知。

## 注释指示器 {#annotation-indicator}

在“编辑”模式下不会显示注释，但工具栏右上方的徽章会显示当前页面存在的注释数。该徽章取代了默认的“注释”图标，但还可用作打开/关闭“注释”模式的快速链接：

![注释指示器](/help/sites-cloud/authoring/assets/annotation-indicator.png)

## 注释模式 {#annotate-mode}

仅在注释模式下可看到注释。

1. 在编辑页面时，请使用工具栏右上方的以下图标进入注释模式：

   ![“注释”按钮](/help/sites-cloud/authoring/assets/annotations.png)

   此时，您可以查看任何现有的注释。

   ![注释示例](/help/sites-cloud/authoring/assets/annotation-sketches.png)

1. 单击或点按注释以打开“注释”对话框并查看其详细信息。

   ![注释详细信息](/help/sites-cloud/authoring/assets/annotation-adding.png)

1. 要退出“注释”模式并返回之前使用的模式，请点按/单击顶部工具栏右侧的 x 按钮。

## 添加和编辑注释 {#annotating-a-component}

除了查看注释之外，通过注释模式还可在内容上创建、编辑、移动或删除注释

1. 在页面上[启动“注释”模式](#annotate-mode)。

1. 单击/点按“添加注释”图标（工具栏左侧的加号）以开始添加注释。

1. 单击/点按需要添加注释的组件（将以蓝色边框突出显示可添加注释的组件）并打开对话框：

   ![添加注释](/help/sites-cloud/authoring/assets/annotation-adding.png)

   在此，可使用相应的字段和/或图标执行以下操作：

   * 输入注释文本。
   * 创建草图（线和形状）以突出显示组件的某个区域。


      ![“注释草图”按钮](/help/sites-cloud/authoring/assets/annotation-sketch.png)

      创建草图时，光标将变成十字线。您可以绘制多条不同的线。草图线反映注释颜色，可为箭头、圆环或椭圆环。

   * 选择或更改颜色：

      ![注释色板按钮](/help/sites-cloud/authoring/assets/annotation-color-swatch.png)

1. 单击/点按注释对话框外部可关闭该对话框。随后将显示截断的注释视图及任何草图：

   ![注释草图](/help/sites-cloud/authoring/assets/annotation-sketches.png)

1. 完成特定注释编辑之后，您可以：

   * 单击或点按文本标记以打开该注释。打开后，即可查看全文、作出更改或[删除注释](#deleting-annotations)。
   * 调整文本标记位置。
   * 单击或点按草图线以选择该草图，并将它拖至所需的位置。
   * 移动或复制组件
      * 还将移动或复制任何相关的注释及其草图，但它们相对于段落的位置将保持不变。


>[!NOTE]
>
>无法将注释添加到其他用户已锁定的页面。

>[!NOTE]
>
>单个组件类型的定义决定是否可在该组件的实例中添加注释。

## 删除注释和草图 {#deleting-annotations}

可以删除注释及其关联的草图。

1. 在页面上[启动“注释”模式](#annotate-mode)。

1. 单击/点按文本标记以打开注释。

1. 单击或点按“删除”图标。

   ![删除注释](/help/sites-cloud/authoring/assets/annotation-delete.png)

1. 现已删除注释和所有关联的草图。

>[!NOTE]
>
>删除组件将删除所有附加到该资源的注释和草图，无论它们在整个页面上的什么位置。

## 仅删除草图 {#deleting-sketches}

可仅删除特定的草图，而非删除整个注释及所有关联的草图。

1. 在页面上[启动“注释”模式](#annotate-mode)。

1. 单击或点按草图。AEM 用深蓝色的框突出显示它。

   ![选择要删除的草图](/help/sites-cloud/authoring/assets/annotation-sketch-delete.png)

1. 按键盘上的 Delete 键。

1. 现已删除草图，但保留了注释。

## 为其他资源添加注释 {#annotating-other-resources}

除了组件之外，您还可以对各种资源添加注释：

* 对资产添加注释[对资产添加注释](/help/assets/manage-digital-assets.md#annotating)
* 对视频资产添加注释[对视频资产添加注释](/help/assets/manage-video-assets.md#annotate-video-assets)
