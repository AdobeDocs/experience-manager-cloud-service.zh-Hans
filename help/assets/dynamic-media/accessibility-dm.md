---
title: Dynamic Media 中的辅助功能
description: 了解Dynamic Media和Dynamic Media观众的辅助功能。
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
translation-type: tm+mt
source-git-commit: 75caf21c399271b23e71c7c0045e3a41cda8a851
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 1%

---


# Dynamic Media 中的辅助功能 {#accessibility-in-dm}

Dynamic Media支持跨创作用户界面的键盘控制和辅助技术，如JAWS和NVDA屏幕阅读器。

## Dynamic Media{#keyboard-support-in-dm}中支持键盘辅助功能

由于Dynamic Media是Experience Manager资产的插件，因此大多数键盘控制行为与Experience Manager资产中的操作相同。 例如，Dynamic Media的`Cancel`按钮与Experience Manager资产中的焦点突出显示相同。 它还会像在Experience Manager资产中一样对`Spacebar`键做出响应。 请参阅Assets](/help/assets/accessibility.md#keyboard-shortcuts)中的[键盘快捷键。

在Dynamic Media，单个用户界面元素支持的按键在大多数情况下都显而易见，并且易于查找。 Dynamic Media的键盘控件与以下内容相关：

* 能够使用`Tab`和`Shift+Tab`按键在页面上的交互式元素之间导航。
使用`Tab`将输入焦点按Tab键顺序前进到下一个用户界面元素；使用`Shift+Tab`将输入焦点重新调回到以前的用户界面元素。
焦点遍历遵循屏幕上的自然用户界面元素位置，并按从左到右、从上到下的顺序移动。 此外，如果任何字段有错误，可按`Tab`将焦点移到该字段。
* 能够使用`Spacebar`和`Enter`键激活标准用户界面元素，如按钮、下拉列表等。
* 能够在活动元素上查看键盘焦点突出显示。 具有输入焦点的用户界面元素接收可视焦点指示作为呈现在用户界面元素周围的边框。
* 在热点编辑器中，您可以使用一些自定义按键（如箭头键）与复杂的用户界面元素进行交互，从而重新确定热点的位置。
* 在交互式视频编辑器中，可以使用`Spacebar`选择图像并将其添加到区段。 此外，还可以使用`Backspace`键从&#x200B;**[!UICONTROL 内容]**&#x200B;选项卡中删除选定项。 此外，按`Tab`可根据需要在页面上的交互式元素之间导航。
* 在图像裁剪／智能裁剪编辑器中，您可以执行以下操作：
   * 使用箭头键可裁剪帧大小，或调整图像的位置，或同时调整两者。
   * 第一个`Tab`停止将高亮显示整个图像帧。 然后，可使用键盘上的箭头键重新确定框架的位置。
   * 接下来的四个`Tab`停止是框架的四个角。 当焦点放在框架角上时，该角将高亮显示。 同样，您可以使用键盘上的箭头键移动聚焦的角。
请参阅[编辑单个图像的智能裁剪或智能色板](/help/assets/dynamic-media/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (AEM 6.5) or Coral Spectrum (in Skyline)) as entire AEM Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md##adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## Dynamic Media的辅助技术支持{#assistive-technology=support-for-dm}

Dynamic Media用户界面元素可与屏幕阅读器等辅助技术配合使用。 例如，当您使用键盘快捷键`D`导航地标时，它会识别页面上的地标；或者，当您使用键盘快捷键`R`导航地标时，它会识别页面上的地标。 在使用标题键盘快捷键`H`导航时，还会解说标题。

## Dynamic Media查看器中支持键盘辅助功能{#keyboard-accessibility-for-dm-viewers}

所有现成的Dynamic Media查看器组件都支持为客户提供键盘辅助功能。

请参阅《Dynamic Media查看器参考指南》中的[键盘辅助功能和导航](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility.html)。

## Dynamic Media查看器中的辅助技术支持{#assistive-technology=support-for-dm-viewers}

所有Dynamic Media查看器组件都支持ARIA（可访问的富Internet应用程序）角色和属性，以改进与屏幕阅读器等辅助技术的集成。
请参阅《Dynamic Media查看器参考指南》中任何自定义查看器主题中的**辅助型技术支持**&#x200B;帮助主题。 例如，请参阅视频查看器的[辅助技术支持](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html)或交互式图像查看器的[辅助技术支持](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html?lang=en#viewers-for-aem-assets-only)。

>[!MORELIKETHIS]
>
>* [Adobe解决方案的辅助功能](https://www.adobe.com/accessibility.html)
>* [Experience Manager资源中的辅助功能](/help/assets/dynamic-media/accessibility-dm.md)

