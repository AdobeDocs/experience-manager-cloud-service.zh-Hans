---
title: Dynamic Media 中的辅助功能
description: 了解如何在Dynamic Media中使用视频，例如编码视频、将视频发布到YouTube以及查看视频报表的最佳实践。 还了解如何向视频添加隐藏式字幕、字幕或章节标记。
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
feature: Accessibility
role: Admin,User
exl-id: f8d2dcbf-f61a-4b27-a3fc-406e3662adcb
source-git-commit: 6ad46350906c3b8a36a8e361714fa5fffdbf8e82
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 1%

---

# Dynamic Media 中的辅助功能 {#accessibility-in-dm}

{{work-with-dynamic-media}}

Dynamic Media在整个创作用户界面中支持键盘控制和辅助技术，例如JAWS和NVDA屏幕阅读器。

## Dynamic Media中的键盘辅助功能支持 {#keyboard-support-in-dm}

由于Dynamic Media是[!DNL Experience Manager Assets]的一个插件，因此大部分键盘控件行为与[!DNL Experience Manager Assets]中的行为相同。 例如，Dynamic Media中的`Cancel`按钮与[!DNL Experience Manager Assets]中的焦点高亮相同。 它还会响应`Spacebar`键，如[!DNL Experience Manager Assets]中所示。 查看Assets](/help/assets/accessibility.md#keyboard-shortcuts)中的[键盘快捷键。

Dynamic Media中的“个人”用户界面元素支持的击键在大多数情况下显而易见，很容易找到。 Dynamic Media中的键盘控件与以下内容有关：

* 能够使用`Tab`和`Shift+Tab`按键在页面上的交互元素之间导航。
使用`Tab`将输入焦点推进到Tab键顺序中的下一个用户界面元素；使用`Shift+Tab`将输入焦点移回上一个用户界面元素。
焦点遍历将遵循屏幕上的自然用户界面元素位置，并以从左到右、从上到下的顺序移动。 此外，如果任何字段有错误，您可以按`Tab`将焦点移动到该字段。
* 能够使用`Spacebar`和`Enter`键激活标准用户界面元素，如按钮和下拉列表。
* 能够看到活动元素上的键盘焦点突出显示。 具有输入焦点的用户界面元素接收视觉焦点指示作为围绕用户界面元素呈现的边界。
* 在热点编辑器中，您可以使用某些自定义按键（如箭头键）与复杂的用户界面元素交互，以重新定位热点。
* 在交互式视频编辑器中，您可以使用`Spacebar`选择图像并将其添加到区段中。 此外，您可以使用`Backspace`键从&#x200B;**[!UICONTROL Content]**&#x200B;选项卡中删除所选项目。 此外，根据需要按`Tab`功能可在页面上的交互元素之间导航。
* 在图像裁切/智能裁切编辑器中，您可以执行以下操作：
   * 使用箭头键裁切框架大小或重新定位图像，或同时使用两者。
   * 第一个`Tab`停止点突出显示整个图像帧。 然后，可以使用键盘上的箭头键重新定位框架。
   * 接下来的四个`Tab`句点是该帧的四个角。 将焦点置于框架角上时，该角将突出显示。 同样，您可以使用键盘上的箭头键移动焦点角。
请参阅[编辑单个图像的智能裁剪或智能色板](/help/assets/dynamic-media/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (Experience Manager 6.5) or Coral Spectrum (in Skyline)) as entire Experience Manager Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md#adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## Dynamic Media {#assistive-technology=support-for-dm}中的辅助技术支持

Dynamic Media用户界面元素可与屏幕阅读器等辅助技术配合使用。 例如，当您使用键盘快捷键`D`导航地标或使用键盘快捷键`R`导航区域时，它可以识别页面上的地标。 它还会在使用标题键盘快捷键`H`导航时讲述标题。

## Dynamic Media查看器中的键盘辅助功能支持 {#keyboard-accessibility-for-dm-viewers}

所有开箱即用的Dynamic Media查看器组件都支持客户的键盘辅助功能。

请参阅《Dynamic Media查看器参考指南》中的[键盘辅助功能和导航](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility.html)。

## Dynamic Media查看器{#assistive-technology=support-for-dm-viewers}中的辅助技术支持

所有Dynamic Media查看器组件都支持ARIA（可访问的富互联网应用程序）角色和属性，以改进与屏幕阅读器等辅助技术的集成。
请参阅Dynamic Media查看器参考指南中的任何自定义查看器主题中的**辅助技术支持**&#x200B;帮助主题。 例如，对于视频查看器，请参阅[辅助技术支持](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html)；对于交互式图像查看器，请参阅[辅助技术支持](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html#viewers-for-aem-assets-only)。

## [!DNL Dynamic Media]支持隐藏式字幕 {#closed-caption-support}

Dynamic Media支持传送带隐藏式字幕的视频和自适应视频集。 字幕必须显示在视频内容的顶部。

查看Dynamic Media中的[视频 — 向视频](/help/assets/dynamic-media/video.md#adding-captions-to-video)添加隐藏式字幕。


>[!MORELIKETHIS]
>
>* Adobe解决方案的[辅助功能](https://www.adobe.com/accessibility.html)
>* Experience Manager Assets中的[辅助功能](/help/assets/dynamic-media/accessibility-dm.md)
