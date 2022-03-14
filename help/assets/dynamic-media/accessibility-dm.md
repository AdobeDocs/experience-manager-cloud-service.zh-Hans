---
title: Dynamic Media 中的辅助功能
description: 了解如何在Dynamic Media中处理视频，例如，对视频进行编码、将视频发布到YouTube以及查看视频报表的最佳实践。 还了解如何向视频添加隐藏式字幕、字幕或章节标记。
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
feature: Accessibility
role: Admin,User
exl-id: f8d2dcbf-f61a-4b27-a3fc-406e3662adcb
source-git-commit: 0d3262a3182063e69f764339e7937e2f83ad7bbb
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 1%

---

# Dynamic Media 中的辅助功能 {#accessibility-in-dm}

Dynamic Media在整个创作用户界面中支持键盘控制和辅助技术，如JAWS和NVDA屏幕阅读器。

## Dynamic Media中的键盘辅助功能支持 {#keyboard-support-in-dm}

因为Dynamic Media是 [!DNL Experience Manager Assets]，则大多数键盘控制行为与中的相同 [!DNL Experience Manager Assets]. 例如， `Cancel` 按钮的焦点突出显示与 [!DNL Experience Manager Assets]. 它还对 `Spacebar` 键 [!DNL Experience Manager Assets]. 请参阅 [资产中的键盘快捷键](/help/assets/accessibility.md#keyboard-shortcuts).

在Dynamic Media中，单个用户界面元素支持的击键在大多数情况下是显而易见的，并且易于查找。 Dynamic Media中的键盘控件与以下事项相关：

* 使用功能 `Tab` 和 `Shift+Tab` 键击，以在页面上的交互式元素之间导航。
使用 `Tab` 按Tab键顺序将输入焦点提前到下一个用户界面元素；使用 `Shift+Tab` 将输入焦点重新引回到上一个用户界面元素。
焦点遍历遵循屏幕上自然的用户界面元素位置，并按从左到右、从上到下的顺序移动。 此外，如果有任何字段出错，您可以按 `Tab` 把焦点移到它上。
* 能够使用 `Spacebar` 和 `Enter` 用于激活标准用户界面元素（如按钮和下拉列表）的键。
* 能够查看活动元素上的键盘焦点突出显示。 具有输入焦点的用户界面元素接收作为呈现在用户界面元素周围的边框的可视焦点指示。
* 在热点编辑器中，您可以使用一些自定义键击（如箭头键）与复杂的用户界面元素进行交互，以调整热点位置。
* 在交互式视频编辑器中，您可以使用 `Spacebar` 来选择图像并将其添加到区段。 此外，您还可以使用 `Backspace` 用于从 **[!UICONTROL 内容]** 选项卡。 还有，紧 `Tab` 功能。
* 在图像裁剪/智能裁剪编辑器中，您可以执行以下操作：
   * 使用箭头键裁剪帧大小，或调整图像位置，或者同时调整两者。
   * 第一个 `Tab` 停止会高亮显示整个图像帧。 然后，可使用键盘上的箭头键调整框架的位置。
   * 接下来的四个 `Tab` 停止是框架的四个角。 当焦点位于框架角上时，该角会突出显示。 再次重申，您可以使用键盘上的箭头键来移动聚焦的角。
请参阅 [编辑单个图像的智能裁剪或智能色板](/help/assets/dynamic-media/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (Experience Manager 6.5) or Coral Spectrum (in Skyline)) as entire Experience Manager Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md##adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## Dynamic Media中的辅助技术支持 {#assistive-technology=support-for-dm}

Dynamic Media用户界面元素可与屏幕阅读器等辅助技术配合使用。 例如，当您使用键盘快捷键导航地标时，它会识别页面上的地标 `D` 或使用键盘快捷键的区域 `R`. 使用标题键盘快捷键导航时，还会讲述标题 `H`.

## Dynamic Media查看器中支持键盘辅助功能 {#keyboard-accessibility-for-dm-viewers}

所有开箱即用的Dynamic Media查看器组件都支持为客户提供键盘辅助功能。

请参阅 [键盘辅助功能和导航](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility.html) (在《Dynamic Media查看器参考指南》中)。

## Dynamic Media查看器中的辅助技术支持 {#assistive-technology=support-for-dm-viewers}

所有Dynamic Media查看器组件都支持ARIA（无障碍的富互联网应用程序）角色和属性，以改进与屏幕阅读器等辅助技术的集成。
请参阅 **辅助技术支持** 《Dynamic Media查看器参考指南》中任何自定义查看器主题中的帮助主题。 例如，请参阅 [辅助技术支持](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html) ，或 [辅助技术支持](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html#viewers-for-aem-assets-only) （对于交互式图像查看器）。

## 中的隐藏式字幕支持 [!DNL Dynamic Media] {#closed-caption-support}

Dynamic Media支持交付带有隐藏式字幕的视频和自适应视频集。 字幕必须显示在视频内容的顶部。

请参阅 [Dynamic Media中的视频 — 在视频中添加隐藏式字幕或字幕](/help/assets/dynamic-media/video.md#adding-captions-to-video).


>[!MORELIKETHIS]
>
>* [Adobe解决方案的辅助功能](https://www.adobe.com/accessibility.html)
>* [Experience Manager Assets中的辅助功能](/help/assets/dynamic-media/accessibility-dm.md)

