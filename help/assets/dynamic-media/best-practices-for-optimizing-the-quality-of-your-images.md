---
title: 优化图像质量的最佳实践
description: 了解帮助您使用Dynamic Media优化图像资源质量的最佳实践。
contentOwner: Rick Brough
feature: Asset Management, Best Practices
role: User
exl-id: 2efc4a27-01d7-427f-9701-393497314402
source-git-commit: 62af768370ee0affa4003a7ae0c520ad1a065e8c
workflow-type: tm+mt
source-wordcount: '1648'
ht-degree: 1%

---

# 优化图像质量的最佳实践 {#best-practices-for-optimizing-the-quality-of-your-images}

优化图像质量可能是一个耗时的过程，因为许多因素有助于呈现可接受的结果。 结果部分具有主观性，因为个人对图像质量的看法不同。 结构化试验是关键。

Adobe Experience Manager包括100多条Dynamic Media图像投放命令，用于调整和优化图像和渲染结果。 以下准则可帮助您使用一些基本命令和最佳实践来简化流程并快速获得良好结果。

<!-- ADDED THE FOLLOWING TOPIC AS PER CQDOC-21594 -->

## 在Dynamic Media中启用智能成像 {#bp-enable-smart-imaging}

**智能成像：**

* 在Dynamic Media中启用“智能成像”可基于客户端浏览器功能自动优化图像格式、大小和质量。
想要了解更多信息？ 转到 [智能成像](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/imaging-faq).
* 它通过动态调整这些参数来增强图像投放性能。
* 可以使用自我评估工具评估智能成像 [快照](https://snapshot.scene7.com/).

**图像格式：**

* 避免使用显式 `fmt=webp` 或 `fmt=avif` 命令，除非用例特别需要。
* 智能成像会自动选择最佳格式，从而产生最佳的带宽增益。

**默认行为：**

* 如果未在URL中指定格式命令并且未启用智能成像，则Dynamic Media图像投放默认为使用JPEG格式。

通过针对图像格式做出明智的选择并启用智能成像，您可以显着影响性能和用户体验。


<!-- ADDED THE FOLLOWING TOPIC AS PER CQDOC-21594 -->

## 选择源图像的最佳实践 {#bp-select-source-image}

使用源图像的基本注意事项：

* **源图像格式：**
   * 使用PNG、TIFF或PSD等无损格式可确保图像质量保持高且无任何压缩伪像。
   * 这些格式会保留所有原始数据，因此非常适合进行编辑和进一步处理。
* **源图像大小：**
   * 从高分辨率图像开始，可提供更多细节和灵活性。
   * 当需要以不同大小（例如，跨设备或屏幕分辨率）显示图像时，具有较大的源图像可以更好地缩放。
   * 对于支持缩放（如产品照片）的图像，最大尺寸应在2,000像素左右，或者更大。
   * 不需要缩放的标识或横幅可以按照其预期用途所需的最大尺寸上传。

通过在源级别做出这些仔细的选择，您可以对视觉内容的整体质量做出重大贡献。

<!-- REMOVED TOPIC AS PER CQDOC-21594
## Best practices for image format (`&fmt=`) {#best-practices-for-image-format-fmt}

* JPG or PNG are the best choices to deliver images in good quality and with manageable size and weight.
* If no format command is supplied in the URL, Dynamic Media Image Delivery defaults to JPG for delivery.
* JPG compresses at a ratio of 10:1 and usually produces smaller image file sizes. PNG compresses at a ratio of about 2:1, except when images contain a white background. Typically though, PNG file sizes are larger than JPG files.
* JPG uses lossy compression, meaning that picture elements (pixels) are dropped during compression. PNG on the other hand uses lossless compression.
* JPG often compresses photographic images with better fidelity than synthetic images with sharp edges and contrast.
* If your images contain transparency, use PNG because JPG does not support transparency.

As a best practice for image format, start with the most common setting `&fmt=JPG`. -->

## 图像大小的最佳实践 {#best-practices-for-image-size}

动态减小图像大小是最常见的任务之一。 它涉及指定大小，以及（可选）使用哪种缩减取样模式来缩减图像。

* 对于图像大小调整，最好且最直接的方法是使用 `&wid=<value>` 和 `&hei=<value>,`或只是 `&hei=<value>`. 这些参数会根据长宽比自动设置图像宽度。
* `&resMode=<value>`控制用于缩减像素采样的算法。 开始于 `&resMode=sharp2`. 此值可提供最佳图像质量。 使用缩减像素取样时 `value =bilin` 速度越快，往往会导致伪像的锯齿。

作为调整图像大小的最佳实践，请使用 `&wid=<value>&hei=<value>&resMode=sharp2` 或 `&hei=<value>&resMode=sharp2`

## 图像锐化的最佳实践 {#best-practices-for-image-sharpening}

图像锐化是控制网站上图像的最复杂方面，并且会产生许多错误。 请查阅以下有用资源，以详细了解锐化和USM锐化在Experience Manager中的工作方式：

* 最佳实践白皮书 [Adobe Dynamic Media Classic图像质量和锐化最佳实践](/help/assets/dynamic-media/assets/sharpening_images.pdf) 也适用于Experience Manager。

* 观看 [在Experience Manager中使用图像锐化 — Dynamic Media](https://experienceleague.adobe.com/en/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-image-sharpening-feature-video-use#dynamic-media).

通过Experience Manager，您可以在摄取和/或交付时锐化图像。 但是，通常最好只使用一种方法或另一种方法来锐化图像，但不要同时使用这两种方法。 通常，在交付、URL上锐化图像可产生最佳效果。

可以使用两种图像锐化方法：

* 简单锐化( `&op_sharpen`) — 与Photoshop中使用的锐化滤镜类似，简单锐化会在动态调整大小后对图像的最终视图应用基本锐化。 但是，此方法不可由用户配置。 最佳实践是避免使用 `&op_sharpen` 除非有必要。
* USM锐化( `&op_USM`) — 钝化蒙版是一种行业标准锐化滤镜。 最佳实践是遵循以下准则，使用钝化蒙版来锐化图像。 USM锐化允许您控制以下三个参数：

   * `&op_sharpen=`数量，半径，阈值

      * **[!UICONTROL 数量]** （0-5，效果强度。）
      * **[!UICONTROL 半径]** （0-250，围绕锐化对象绘制的“锐化线”的宽度，以像素为单位。）

     请记住，参数半径和数量彼此对应。 减小半径可以通过增加量来补偿。 半径允许更细的控制，因为较低的值仅锐化边缘像素，而较高的值锐化较宽范围的像素。

      * **[!UICONTROL 阈值]** （0-255，影响的敏感性。）

     此参数确定锐化的像素与周围区域必须有多大的不同，才会被视为边缘像素，而滤镜会锐化这些像素。 此 **[!UICONTROL 阈值]** 参数有助于避免过度锐化颜色相似的区域，如肤色。 例如，阈值为12会忽略肤色亮度的细微变化，以避免添加“杂色”，同时仍会为高对比度区域添加边缘对比度，如睫毛与皮肤相遇的地方。

     有关如何设置这三个参数的更多信息（包括要与过滤器一起使用的最佳实践），请参阅以下资源：

      * 最佳实践白皮书 [Adobe Dynamic Media Classic图像质量和锐化最佳实践](/help/assets/dynamic-media/assets/sharpening_images.pdf) 也适用于Experience Manager。

      * 观看 [在Experience Manager中使用图像锐化 — Dynamic Media](https://experienceleague.adobe.com/en/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-image-sharpening-feature-video-use#dynamic-media).

      * Experience Manager还允许您控制第四个参数：单色(0,1)。 此参数确定是使用值0分别将钝化蒙版应用于每个颜色组件，还是使用值1将钝化蒙版应用于图像亮度/强度。

作为最佳实践，请从钝化蒙版半径参数开始。 可以开始使用的Radius设置如下：

* **[!UICONTROL 网站]**：0.2-0.3像素
* **[!UICONTROL 照片打印(250-300 ppi)]**：0.3-0.5像素
* **[!UICONTROL 胶印打印(266-300 ppi)]**：0.7-1.0像素
* **[!UICONTROL 画布打印(150 ppi)]**：1.5-2.0像素

逐渐将数量从1.75增加到4。 如果锐化仍不是您想要的方式，请将半径增加一个小数点，然后再次运行从1.75到4的锐化量。 根据需要重复执行上述步骤。

将单色参数设置保留为0。

### JPEF压缩的最佳实践(`&qlt=`) {#best-practices-for-jpef-compression-qlt}

* 此参数可控制JPG编码质量。 较高的值意味着较高质量的图像但文件大小较大；或者，较低的值意味着较低质量的图像但文件大小较小。 此参数的范围为0至100。
* 要优化质量，请勿将参数值设置为100。 将90或95设置为100几乎可以察觉到差异。 而100则毫无必要地增加了图像文件的大小。 因此，要优化质量但避免图像文件变得过大，请设置 `qlt= value` 到90或95。
* 要优化较小的图像文件大小，但使图像质量保持在可接受的级别，请设置 `qlt= value` 到80。 值低于70到75会导致图像质量显着下降。
* 作为最佳实践，要保持中立，请将 `qlt= value` 到85岁时保持中立。
* 在中使用色度标志 `qlt=`

   * 此 `qlt=` 参数具有第二个设置，允许您使用值打开RGB色度缩减像素采样 `,1` 或使用值关闭 `,0`.
   * 为了保持简单，请从RGB色度缩减像素取样关闭开始(`,0`)。 此设置通常可以获得更好的图像质量，尤其是对于具有大量锐边和对比度的合成图像。

作为使用JPG压缩的最佳实践 `&qlt=85,0`.

## JPEG大小调整的最佳实践(`&jpegSize=`) {#best-practices-for-jpeg-sizing-jpegsize}

参数 `jpegSize` 如果要确保图像不超过特定大小，以便交付给内存有限的设备，则非常有用。

* 此参数设置为KB (`jpegSize=&lt;size_in_kilobytes&gt;`)。 它定义图像投放允许的最大大小。
* `&jpegSize=` 与JPG压缩参数交互 `&qlt=`. 如果JPG响应具有指定的JPG压缩参数(`&qlt=`)不超过jpegSize值，则图像返回时为 `&qlt=` （按定义）。 否则， `&qlt=` 将逐渐减小，直到图像符合最大允许大小。 或者，直到系统确定它不合适并返回错误为止。

作为最佳实践，请设置 `&jpegSize=` 并添加参数 `&qlt=` 如果您要将JPG映像传送到内存有限的设备。

## 最佳实践摘要 {#best-practices-summary}

为了达到较高的图像质量和较小的文件大小，最好从以下参数组合开始：

`fmt=jpg&qlt=85,0&resMode=sharp2&op_usm=1.75,0.3,2,0`

在大多数情况下，这种设置组合会产生卓越的结果。

如果图像需要进一步优化，请从设置为0.2或0.3的半径开始逐步微调锐化（钝化蒙版）参数。然后，逐渐将数量从1.75增加到最大值4(相当于Photoshop中的400%)。 检查是否达到了预期效果。

如果锐化结果仍然不令人满意，请以小数增量增加半径。 对于每增加一个小数，将数量重新调整为1.75，然后逐渐增加到4。 重复此过程，直到获得所需的结果。 虽然上述价值观是创意工作室已经验证的方法，但请记住，您可以从其他价值观开始，并遵循其他策略。 因此，结构化试验是关键，其结果是否满意是主观问题。

在实验过程中，以下一般建议有助于优化您的工作流：

* 尝试直接在URL上实时测试不同的参数。
* 作为最佳实践，请记住，您可以将Dynamic Media图像服务命令分组到图像预设中。 图像预设基本上是带有自定义预设名称的URL命令宏，例如 `$thumb_low$` 和 `&product_high$`. URL路径中的自定义预设名称将调用这些预设。 此功能可帮助您管理网站上图像不同使用模式的命令和质量设置，并缩短URL的总长度。
* Experience Manager还提供了更高级的方法来调整图像质量，例如在摄取时应用锐化图像。 要优化渲染结果， [Adobe咨询服务](https://business.adobe.com/customers/consulting-services/main.html) 可以帮助您提供自定义的洞察信息和最佳实践。
