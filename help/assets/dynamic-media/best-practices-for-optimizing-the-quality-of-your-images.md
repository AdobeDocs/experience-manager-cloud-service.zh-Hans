---
title: 优化图像质量的最佳实践
description: 了解使用Dynamic Media优化图像资产质量的最佳实践。
contentOwner: Rick Brough
feature: 资产管理
role: Business Practitioner
exl-id: 2efc4a27-01d7-427f-9701-393497314402
translation-type: tm+mt
source-git-commit: 1fe6ce1259972c1805d934327aa2f24cdcdc0bc8
workflow-type: tm+mt
source-wordcount: '1478'
ht-degree: 48%

---

# 优化图像质量的最佳实践 {#best-practices-for-optimizing-the-quality-of-your-images}

优化图像质量可能会是一个很耗时的过程，因为渲染可接受的效果涉及到很多因素。在某种程度上，效果带有主观性，因为每个人对图像质量都会有不同的看法。结构化试验是关键所在。

Adobe Experience Manager包含100多个Dynamic Media图像投放命令，用于调整和优化图像及渲染结果。 以下准则可以帮助您通过使用一些基本的命令和最佳实践，简化操作过程，并快速获得最佳效果。

## 图像格式的最佳实践 (`&fmt=`) {#best-practices-for-image-format-fmt}

* 如果要以良好的质量以及可管理的大小和权重来传送图像，JPG 或 PNG 是最佳选择。
* 如果 URL 中未提供任何格式命令，Dynamic Media 图像传送将默认采用 JPG 格式。
* JPG 的压缩比率为 10:1，通常生成的图像文件较小。PNG的压缩比约为2:1，但当图像包含白色背景时除外。 但是，通常 PNG 文件大于 JPG 文件。
* JPG 采用有损压缩，这意味着在压缩过程中图像元素（像素）会有所丢失。PNG 则采用无损压缩。
* 通常情况下，JPG 在压缩摄影图像时保真度会比合成图像更高，具有清晰的边缘和对比度。
* 如果您的图像包含透明度，请使用 PNG，因为 JPG 不支持透明度。

作为图像格式的最佳实践，使用最常见的设置`&fmt=JPG`进行开始。

## 图像大小的最佳实践 {#best-practices-for-image-size}

动态缩减图像大小是最常见的任务之一。这涉及到指定大小，以及（可选）指定用于缩小图像的缩减采样模式。

* 对于图像大小调整，最佳且最直接的方法是使用`&wid=<value>`和`&hei=<value>,`或仅使用`&hei=<value>`。 这些参数会根据宽高比自动设置图像宽度。
* `&resMode=<value>`控制用于缩减采样的算法。开始`&resMode=sharp2`。 使用此值可提供最佳图像质量。虽然使用缩减像素采样`value =bilin`速度更快，但通常会导致出现锯齿伪像。

作为调整图像大小的最佳实践，请使用`&wid=<value>&hei=<value>&resMode=sharp2`或`&hei=<value>&resMode=sharp2`

## 图像锐化的最佳实践 {#best-practices-for-image-sharpening}

在控制网站中的图像时，图像锐化是最复杂的方面，很容易出现多种错误。请参阅以下有用资源，花时间进一步了解锐化和USM锐化在Experience Manager中的工作原理：

* 最佳实践白皮书[“Adobe Dynamic Media经典图像质量和锐化最佳实践”](/help/assets/dynamic-media/assets/sharpening_images.pdf)同样适用于Experience Manager。

* 观看[使用Experience Manager锐化 — Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-image-sharpening-feature-video-use.html#dynamic-media)。

借助Experience Manager，您可以在摄取、投放或同时在两种情况下锐化图像。 但是，通常最好只使用一种方法锐化图像，而不同时使用两种方法。 通常，在传送过程中通过 URL 锐化图像可实现最佳效果。

有两种可用的图像锐化方法：

* 简单锐化(`&op_sharpen`) — 简单锐化与Photoshop中使用的锐化滤镜类似，它会在动态调整大小后对图像的最终视图应用基本锐化。 但是，用户不能对这种方法进行配置。最佳实践是，除非另有要求，否则不使用&amp;op_sharpen。
* USM锐化(`&op_USM`)- USM锐化是行业标准的锐化滤镜。 最佳实践是按照下面的准则，使用 USM 锐化来锐化图像。您可以通过 USM 锐化控制下面的三个参数：

   * `&op_sharpen=`amount，radius，threshold

      * **[!UICONTROL amount]** （0-5，效果的强度。）
      * **[!UICONTROL radius]** （0-250，在锐化对象周围绘制的“锐化线条”的宽度，以像素为单位。）

      请记住，radius和amount参数相辅相成。减少半径可以通过增加数量来补偿。“半径”允许进行更精细的控制，较低值仅锐化边缘像素，而较高值锐化较宽范围的像素。

      * **[!UICONTROL threshold]** （0-255，效果的敏感度。）
      此参数确定锐化的像素与周围区域必须有多大的不同，才会被视为边缘像素，而滤镜会锐化这些像素。 **[!UICONTROL threshold]**&#x200B;参数有助于避免使用类似颜色（如肤色）过度锐化区域。 例如，阈值为12时，会忽略肤色亮度的细微变化，以避免添加“杂色”，同时仍会为高对比度区域添加边缘对比度，如睫毛与皮肤相遇的地方。

      有关如何设置这三个参数的更多信息，包括使用滤镜方面的最佳实践，请参阅以下资源：

      * 最佳实践白皮书[“Adobe Dynamic Media经典图像质量和锐化最佳实践”](/help/assets/dynamic-media/assets/sharpening_images.pdf)同样适用于Experience Manager。

      * 观看[使用Experience Manager锐化 — Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-image-sharpening-feature-video-use.html#dynamic-media)。

      * Experience Manager还允许您控制第四个参数：monochrome(0,1)。 此参数确定是将USM锐化分别应用于每个颜色组件（使用值0），还是应用于图像亮度/强度（使用值1）。



作为最佳实践，应首先开始设置 USM 锐化 radius 参数。您可以先使用以下 radius 设置：

* **[!UICONTROL 网站]**:0.2-0.3像素
* **[!UICONTROL 照片打印(250-300 ppi)]**:0.3-0.5像素
* **[!UICONTROL 胶印(266-300 ppi)]**:0.7-1.0像素
* **[!UICONTROL 画布打印(150 ppi)]**:1.5-2.0像素

将 amount 从 1.75 逐渐增加至 4。如果锐化仍未达到您需要的效果，请将 radius 增加 0.1，然后再次将 amount 从 1.75 逐渐增加至 4。根据需要，重复上述步骤。

将 monochrome 参数设置保留为 0。

### JPEF 压缩的最佳实践 (`&qlt=`) {#best-practices-for-jpef-compression-qlt}

* 此参数控制 JPG 编码质量。值越大表示图像质量越高，但文件也越大；反之，值越小表示图像质量越低，但文件也越小。此参数的范围是 0-100。
* 要优化质量，切勿将该参数值设置为 100。设置为 90 或 95 与设置为 100 几乎没有什么区别，但是设置为 100 会不必要地增加图像文件的大小。因此，要优化质量，但避免图像文件过大，请将`qlt= value`设置为90或95。
* 要优化较小的图像文件大小，但将图像质量保持在可接受的水平，请将`qlt= value`设置为80。 低于70到75的值会导致图像质量显着下降。
* 作为最佳实践，要保持在中间，请将`qlt= value`设置为85以保持在中间。
* 使用`qlt=`中的色度标志

   * `qlt=`参数还有另一个设置，允许您使用值`,1`打开RGB色度缩减采样，或使用值`,0`关闭。
   * 要保持简单，请关闭RGB色度缩减采样的开始(`,0`)。 此设置通常会提高图像质量，尤其是对于具有大量清晰边缘和对比度的合成图像。

作为JPG压缩的最佳实践，请使用`&qlt=85,0`。

## JPEG 大小调整的最佳实践 (`&jpegSize=`) {#best-practices-for-jpeg-sizing-jpegsize}

如果要保证图像不会超过某个大小，以投放到内存有限的设备，则参数`jpegSize`很有用。

* 此参数以千字节(`jpegSize=&lt;size_in_kilobytes&gt;`)为单位设置。 它为图像投放定义允许的最大大小。
* `&jpegSize=` 与JPG压缩参数交互 `&qlt=`。如果具有指定JPG压缩参数(`&qlt=`)的JPG响应未超过jpegSize值，则将按照定义以`&qlt=`返回图像。 否则，`&qlt=`会逐渐减小，直到图像符合允许的最大大小，或直到系统确定它无法适应并返回错误。

作为最佳实践，如果要将JPG图像传送到内存有限的设备，请设置`&jpegSize=`并添加参数`&qlt=`。

## 最佳实践小结 {#best-practices-summary}

作为最佳实践，要获得较高的图像质量和较小的文件大小，请首先使用以下参数组合：

`fmt=jpg&qlt=85,0&resMode=sharp2&op_usm=1.75,0.3,2,0`

在大多数情况下，此设置组合可生成出色的效果。

如果图像需要进一步优化，请先将 radius 设置为 0.2 或 0.3，以便逐渐微调锐化（USM 锐化）参数。然后，将 amount 从 1.75 逐渐增加至最大值 4（相当于 Photoshop 中的 400%）。检查是否达到所需的效果。

如果锐化效果仍然不能让您满意，请按小数位递增的方式增大 radius。对于每次递增，重新将 amount 从 1.75 逐渐增加至 4。重复此过程，直至达到所需效果。尽管采用上述值是创意工作室已经验证过的方法，但请记住，您也可以从其他值开始设置，并遵循其他策略。关于效果是否能让您满意，这是个主观性问题，因此进行结构化的试验很关键。

在您进行试验时，以下一般建议对优化工作流很有帮助：

* 直接在URL上实时尝试和测试不同的参数。
* 作为最佳实践，请记住，您可以将Dynamic Media图像服务命令分组到图像预设中。 图像预设基本上就是具有自定义预设名称（如`$thumb_low$`和`&product_high$`）的URL命令宏。 URL路径中的自定义预设名称会调用这些预设。 这类功能可帮助您针对网站中图像的不同使用模式来管理命令和质量设置，并缩短 URL 的整体长度。
* Experience Manager还提供了更高级的图像质量调整方法，例如在摄取时应用锐化图像。 要调整和优化渲染结果，[Adobe的咨询服务](https://business.adobe.com/customers/consulting-services/main.html)可以帮助您进行自定义分析和最佳实践。
