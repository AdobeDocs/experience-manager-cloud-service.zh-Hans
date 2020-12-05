---
title: ' [!DNL Dynamic Media]中的辅助功能'
description: 了解Dynamic Media和Dynamic Media查看器中的辅助功能
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
translation-type: tm+mt
source-git-commit: d87710badeeb0518a2e51b8abc3974fa77914515
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 0%

---


# Dynamic Media {#working-with-three-d-assets-dm}中的辅助功能

Dynamic Media支持跨创作用户界面的键盘控制和辅助技术，如JAWS和NVDA屏幕阅读器。

## Dynamic Media中的键盘辅助功能支持

由于Dynamic Media是Experience Manager资产的插件，因此大多数键盘控制行为与Experience Manager资产完全相同。 例如，Dynamic Media中的`Cancel`按钮与Experience Manager资产中的焦点突出显示相同，并且与Experience Manager资产中的`Spacebar`键作出响应。 请参阅Assets](/help/assets/accessibility.md#keyboard-shortcuts)中的[键盘快捷键。

Dynamic Media中各个用户界面元素支持的按键在大多数情况下都显而易见，易于发现。 Dynamic Media中的键盘控制与以下内容相关：

* 能够使用`Tab`和`Shift+Tab`按键在页面上的交互式元素之间导航。
使用`Tab`将输入焦点按Tab键顺序前进到下一个用户界面元素；使用`Shift+Tab`将输入焦点重新调回到以前的用户界面元素。
焦点遍历遵循屏幕上的自然用户界面元素位置，并按从左到右、从上到下的顺序移动。 此外，如果任何字段有错误，可按`Tab`将焦点移到该字段。
* 能够使用`Spacebar`和`Enter`键激活标准用户界面元素，如按钮、下拉列表等。
* 能够在活动元素上查看键盘焦点突出显示。 具有输入焦点的用户界面元素可以接收可视焦点指示作为呈现在用户界面元素周围的边框。
* 在热点编辑器中，您可以使用一些自定义按键（如箭头键）与复杂的用户界面元素进行交互，从而重新确定热点的位置。
* 在交互式视频编辑器中，可以使用`Spacebar`选择图像并将其添加到区段。 此外，您还可以使用`Backspace`键从&#x200B;**[!UICONTROL 内容]**&#x200B;选项卡中删除选定项。 此外，按`Tab`可根据需要在页面上的交互式元素之间导航。
* 在图像裁剪／智能裁剪编辑器中，您可以执行以下操作：
   * 使用箭头键可裁剪帧大小，或者重新定位图像，或者两者。
   * 第一个`Tab`停止将高亮显示整个图像帧。 然后，可以使用键盘上的箭头键重新定位框架。
   * 接下来的四个`Tab`停止是框架的四个角。 当焦点放在框架角上时，该角将高亮显示。 同样，您可以使用键盘上的箭头键移动聚焦的角。
请参阅[编辑单个图像的智能裁剪或智能色板](/help/assets/dynamic-media/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (AEM 6.5) or Coral Spectrum (in Skyline)) as entire AEM Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md##adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## Dynamic Media中的辅助技术支持{#assistive-technology=support-for-dm}

动态媒体用户界面元素可与屏幕阅读器等辅助技术结合使用。 例如，当您使用键盘快捷键`D`导航地标时，它会识别页面上的地标；或者，当您使用键盘快捷键`R`导航地标时，它会识别页面上的地标。 在使用标题键盘快捷键`H`导航时，还会解说标题。

## Dynamic Media查看器中的键盘辅助功能支持{#keyboard-accessibility-for-dm-viewers}

现成的所有Dynamic Media查看器组件都支持客户使用键盘进行辅助。

请参阅《Dynamic Media Viewers Reference Guide》中的[键盘辅助功能和导航](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/c-keyboard-accessibility.html)。

## Dynamic Media查看器中的辅助技术支持{#assistive-technology=support-for-dm-viewers}

所有Dynamic Media查看器组件都支持ARIA（可访问的富Internet应用程序）角色和属性，以改进与屏幕阅读器等辅助技术的集成。
请参阅《Dynamic Media查看器参考指南》中任何自定义查看器主题中的**辅助技术支持**&#x200B;帮助主题。 例如，请参阅视频查看器的[辅助技术支持](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html)或交互式图像查看器的[辅助技术支持](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html?lang=en#viewers-for-aem-assets-only)。

>[!MORELIKETHIS]
>
>* [Adobe解决方案的辅助功能](https://www.adobe.com/accessibility.html)
>* [Experience Manager资源中的辅助功能](/help/assets/dynamic-media/accessibility-dm.md)

