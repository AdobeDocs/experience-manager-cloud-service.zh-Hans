---
title: 中的辅助功能 [!DNL Dynamic Media]
description: 了解如何在Dynamic Media中使用3D资产
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
translation-type: tm+mt
source-git-commit: d992b68d4a015f8f947167b5b1d5f0a1ac5c09ec
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---


# Dynamic Media中的辅助功能 {#working-with-three-d-assets-dm}

Dynamic Media支持跨创作用户界面的键盘控制和辅助技术，如JAWS和NVDA屏幕阅读器。

## Dynamic Media中的键盘辅助功能支持

在大多数情况下，单个用户界面元素支持的按键显而易见，易于发现。 Dynamic Media中的键盘控制与以下内容相关：

* 能够使用 `Tab` 和按 `Shift+Tab` 键在页面上的交互式元素之间导航。
使用 `Tab` Tab键顺序将输入焦点提前到下一个用户界面元素；使用 `Shift+Tab` 可将输入焦点重新放回以前的用户界面元素。
焦点遍历遵循屏幕上的自然用户界面元素位置，并按从左到右、从上到下的顺序移动。
* 能够使用 `Spacebar` 和 `Enter` 键激活标准用户界面元素，如按钮、下拉列表等。
* 能够使用一些自定义按键与复杂的UI元素进行交互，如热点编辑器中的箭头键。
* 能够在活动元素上查看键盘焦点突出显示。 具有输入焦点的用户界面元素可以接收可视焦点指示作为呈现在用户界面元素周围的边框。

由于Dynamic Media是AEM Assets的插件，因此大多数键盘控制行为与AEM Assets完全相同。 例如，Dynamic Media `Cancel` 中的按钮与AEM Assets中的焦点突出显示相同，并对键的反 `Spacebar` 应与AEM Assets中相同。 请参阅 [资产中的键盘快捷键](/help/assets/accessibility.md#keyboard-shortcuts)。 热点编辑器和图像裁剪／智能裁剪编辑器是例外。

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (AEM 6.5) or Coral Spectrum (in Skyline)) as entire AEM Assets.  -->

在热点编辑器中，Dynamic Media允许您使用箭头键控制热点的位置。 请参阅 [传送横幅](/help/assets/dynamic-media/carousel-banners.md##adding-hotspots-or-image-maps-to-an-image-banner) 或交 [互式图像](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)

在图像裁剪／智能裁剪编辑器中，使用箭头键可以裁剪帧大小，或者重新定位图像，或者同时使用箭头键。 请参 [阅编辑单个图像的智能裁剪或智能色板](/help/assets/dynamic-media/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## 对Dynamic Media查看器的键盘辅助功能支持 {#keyboard-accessibility-for-dm-viewers}

现成的所有Dynamic Media查看器组件都支持客户使用键盘进行辅助。

请参 [阅《Dynamic Media Viewers](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/c-keyboard-accessibility.html) Reference Guide》中的“Keyboard accessibility and navigation”。

## Dynamic Media查看器的辅助技术支持 {#assistive-technology=support-for-dm-viewers}

Dynamic Media中的所有查看器组件都支持ARIA（可访问的富Internet应用程序）角色和属性，以改进与屏幕阅读器等辅助技术的集成。

请参阅 **《Dynamic Media Viewers Reference Guide** 》中任何自定义查看器主题中的辅助技术支持帮助主题。 例如，请参 [阅视频查看器的](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html) “辅助型技术支持”或“ [交互式图像查看器](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html?lang=en#viewers-for-aem-assets-only) ”的“辅助型技术支持”。

>[!MORELIKETHIS]
>
>* [Adobe解决方案的辅助功能](https://www.adobe.com/accessibility.html)
>* [Experience Manager资源中的辅助功能](/help/assets/dynamic-media/accessibility-dm.md)

