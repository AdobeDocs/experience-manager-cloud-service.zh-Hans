---
title: 历程Dynamic Media，第二部分
description: Dynamic Media历程介绍了Dynamic Media的基础知识、其工作方式、可为您提供的功能以及它给您的工作和客户带来的价值。
contentOwner: Rick Brough
products: Experience Manager as a Cloud Service
topic-tags: introduction,administering
content-type: reference
feature: Image Profiles,Best Practices
role: User, Admin
mini-toc-levels: 4
hide: false
hidefromtoc: false
exl-id: cdca41ad-a2cd-4f68-aaa4-5eec33c30f0b
source-git-commit: 879af9e3168a1ab993eff930355c4bd200879c71
workflow-type: tm+mt
source-wordcount: '2621'
ht-degree: 0%

---

# Dynamic Media历程：基础知识，第二部分  {#dm-journey-part2}

{{work-with-dynamic-media}}

欢迎使用Dynamic Media历程：基础知识，第II部分，您可以从中学习以下内容：

* Dynamic Media URL剖析，以及Dynamic Media如何交付内容
* 创建图像预设以渲染资产的基础知识
* 图像集、旋转集和混合媒体集

另请参阅[Dynamic Media历程；基础知识，第一部分](/help/assets/dynamic-media/dm-journey-part1.md)。

>[!TIP]
>
>为获得最佳结果，Adobe建议您在台式计算机上阅读并查看此Dynamic Media历程。

## Dynamic Media URL剖析，以及Dynamic Media如何交付内容 {#dm-journey-d}

上传和发布Dynamic Media资源后，您可以复制资源生成的URL并将其粘贴到浏览器中，以查看向客户呈现资源的方式。 以下复制的监视图像URL按颜色进行划分，以便于阅读和理解。

![Dynamic Media URL的剖析](/help/assets/dynamic-media/assets/dm-colored-url.png)
_Dynamic Media URL的剖析。_

URL的第一个红色部分引用了服务器域本身。 在这种情况下，Dynamic Media正在通用服务器域`https://s7d1.scene7.com/is/image/`上运行。 通过查看服务器域，可以轻松查看一组图像并了解这些图像是否由Dynamic Media提供服务。 URL将保持相当一致。 但是，有一些Dynamic Media客户已切换到专用服务器域，该域可能为`name-of-your-company.scene7.com`。 智能成像需要一个专用服务器域。

帐户名称是紫色部分。 在这种情况下，该帐户名为`jpearldemo`。

资源ID或名称`AdobeStock_28563982`为绿色。 请注意，该资产具有&#x200B;_no_&#x200B;文件扩展名，如`.png`或`.jpg`。 将资源摄取到Dynamic Media中时，会剥离文件扩展名并创建另一种文件：金字塔TIFF文件。 金字塔TIFF允许Dynamic Media动态快速创建演绎版。

最后，还有图像处理参数`?wid=1000&fmt=jpeg&qlt=85`，这些参数在结尾以黄色显示。

整个URL路径是实时的。 [尝试它](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_28563982?wid=1000&amp;fmt=jpeg&amp;qlt=85){target="_blank"}。

在浏览器窗口仍打开以显示Dynamic Media URL和监视图像的情况下，让我们仔细了解如何通过更改URL来创建图像的演绎版。

### 通过URL呈现监视图像

首先，仅手动删除URL路径中的图像处理规则；保留服务器名称、帐户名称以及资产ID或图像名称。 [尝试它](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_28563982){target="_blank"}。

现在，将图像处理参数添加到URL的末尾。 在URL字段中，在图像名称的右侧，键入`?wid=500`，然后按&#x200B;**[!UICONTROL Enter]**。 [尝试它](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=500){target="_blank"}。

请注意，将生成监视的新演绎版。 要理解这个更改图像宽度这一简单操作的一个关键点是，看到的图像是100%动态生成的。

现在将`500`像素的宽度值更改为`1000`像素，然后按&#x200B;**[!UICONTROL Enter]**。 [尝试它](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000){target="_blank}。
当您按**[!UICONTROL Enter]**&#x200B;时，浏览器将返回到Dynamic Media图像服务器。 它会根据您刚刚输入的新宽度值生成手表的全新演绎版，然后将新图像发送回浏览器，然后进行缓存。

Dynamic Media具有大量图像处理参数，可用于微调网页上的图像资源。 您可以[在此](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html?lang=en)查看他们的列表。

现在，尝试向监视图像添加旋转参数。 URL路径的结尾，紧跟`wid=1000`，键入`&rotate=90`，然后按&#x200B;**[!UICONTROL Enter]**。 [尝试它](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000&amp;rotate=90){target="_blank"}。

这块表还是稍微向左偏了。 将`90`的旋转值更改为`92`，然后按&#x200B;**[!UICONTROL Enter]**。 [尝试它](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000&amp;rotate=9){target="_blank"}。

同样，当您按&#x200B;**[!UICONTROL Enter]**&#x200B;时，将立即生成手表的新演绎版。 您可以看到您获得的性能类型，这解释了为什么Dynamic Media在繁忙的周末或大假期可以每秒发送&#x200B;_个_&#x200B;超过800,000个图像请求。

虽然可以逐个图像更改URL中的图像处理参数，但这不是一种有效方法，尤其是在您的网站上包含成千上万张图像的情况下。 一种更好的方法是使用图像预设。

## 创建图像预设以渲染资产的基础知识 {#dm-journey-e}

有多种方法和位置可供您创建图像或让图像可用。 传统上，Creative进入Adobe Photoshop，并将每个演绎版另存为静态图像。

![静态图像](/help/assets/dynamic-media/assets/dm-static-images.png)
_良好：静态图像，每个图像都是手动创建的。_

想象一下Creative Director看到图片说，

_“我真的很想拍这张照片，好让大手指向四个，小手指向1，好让表盘旋钮更容易看到。”_

创意人员必须重新拍摄所有新的静态图像。

但是，通过Dynamic Media，如果您具有不同的图像预设，则可以在需要时随时使用这些图像。 图像预设可强制实施标准。

![主文件方法](/help/assets/dynamic-media/assets/dm-onefile.png)
_最佳：一个使用图像预设即时创建多个演绎版的文件，如`Search_Grid`和`Thumbnail`。_

| **为什么使用图像预设？** | |
|---|---|
| 标准 | 图像预设对请求的任何图像强制执行标准图像处理处理。 |
| 变更管理 | 如果必须更改图像处理，则只需编辑现有图像预设的参数即可。 更新的定义会自动传播到所有请求。 |

每个地方都需要一种特定的图像，例如，

* 产品详细信息页面，
* 搜索网格，
* 缩略图，
* 购物卡，或
* 主页图像

您希望在任何地方使用该图像时都使用相同的参数进行投放。

让我们看一下如何在Dynamic Media中创建图像预设。

![从“基本”选项卡开始创建图像预设](/help/assets/dynamic-media/assets/dm-image-preset-basictab.png)
_从“基本”选项卡开始创建图像预设。_

在上面的示例中，您可以看到已创建名为&#x200B;_Medium_&#x200B;的新图像预设。 Dynamic Media使用现成可用的图像（背包）作为示例，帮助您查看在创建图像预设时图像预设的特性。

_Medium_&#x200B;图像预设的宽度为500像素，高度为800像素。 在本历程的第一部分中，您已阅读有关以不同格式交付资产的信息。 从&#x200B;**[!UICONTROL 格式]**&#x200B;下拉菜单中，您可以选择以JPEG、PNG、TIFF或多种其他格式交付资源。 您可以灵活处理。

选择&#x200B;**[!UICONTROL 高级]**&#x200B;选项卡可为您提供资源色彩空间的选项。 根据您在&#x200B;**[!UICONTROL 基本]**&#x200B;选项卡中选择的格式(在上例中选择了JPEG)，您可以投放RGB、灰度或CMYK格式的资源。 从&#x200B;**[!UICONTROL 颜色配置文件]**&#x200B;下拉菜单中，您可以选择如何交付要用于打印的CMYK图像资产。 另外请注意，还可以应用其他参数来锐化图像。 在这种情况下，应用了&#x200B;**[!UICONTROL 钝化蒙版]**。

![通过选择“高级”选项卡中的选项来创建图像预设](/help/assets/dynamic-media/assets/dm-image-preset-advancedtab.png)
_通过选择“高级”选项卡中的选项来创建图像预设。_

您记得在之前的[Dynamic Media URL剖析](#dm-journey-d)中，您阅读了有关Dynamic Media URL及其构建方式的信息。 在&#x200B;**[!UICONTROL 图像修饰符]**&#x200B;文本框中，您可以键入所需的任何其他图像处理参数。 使用预设交付图像时，这些参数会包含在URL的预设名称中。 在上面的屏幕快照中，添加了参数`bgc=451B15`。 也就是说，添加了深棕色背景颜色。

您可以将图像预设视为图像的指导方针。 它将提供所有使用预设的图像，每次都一致；将是一样的。 还添加了参数`&op_brightness=+10`以略微增加亮度。

完成后，保存预设，该预设现在可用于您拥有的所有图像。 在这种情况下，您需要将&#x200B;_Medium_&#x200B;图像预设应用于一碗液态巧克力的图像。

![应用图像预设&#x200B;*Medium*&#x200B;以生成图像的演绎版](/help/assets/dynamic-media/assets/dm-medium-image-preset.png)
_应用图像预设Medium以生成图像的演绎版。_

复制URL，然后将其粘贴到浏览器中以检查图像的外观。 [尝试它](http://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_74043302?$Medium$){target="_blank"}。

在您的浏览器中，注意完整URL路径中的图像预设&#x200B;_Medium_&#x200B;的名称。

您可以看到图像所显示的清晰度。 这种品质部分是由于这碗巧克力的投球方式。 此外，部分原因在于，与Dynamic Media相比，您可以存储更大的图像。

如果你的巧克力碗看起来一切正常，你可以在网页上粘贴你希望图像出现在网站上的位置URL。

如果再次查看下面的手表图像，您可以看到有一个`Cart`图像预设、`Grid`预设、`Large`预设、`PDP-page` （产品详细信息页面）预设以及若干其他预设。

![静态和动态图像预设](/help/assets/dynamic-media/assets/dm-image-presets.png)
_静态和动态图像预设。 已使用`PDP-page`图像预设呈现监视图像。_

但是，如果您必须更改网站上的图像，该怎么办？ 例如，假设您已经进行了一些测试，发现未收到您认为的120 x 120的图像（`Cart`图像预设）。 您必须通过将宽度增加到175像素并将高度增加到175像素来增大图像。 传统上，您必须进入Adobe Photoshop并重新创建所有这些购物车图像。 但使用Dynamic Media，您只需编辑图像预设，只需将宽度和高度值更新为175并保存预设即可，如以下示例所示。

![编辑图像预设](/help/assets/dynamic-media/assets/dm-edit-image-preset.png)
_正在编辑`Cart`图像预设的宽度和高度。_

在更改图像预设并刷新缓存后，所有图像都会更新，并且与该预设一起使用的所有URL都不&#x200B;_会在任何地方更改_。 这意味着不需要断开链接，也不需要网页重定向。

## 图像集、旋转集和混合媒体集 {#dm-journey-f}

Dynamic Media的一些更常用的用途是，使您能够创建图像集、旋转集和混合媒体集。

图像集通常由一系列图像资产组成，这些资产以单个实体的形式呈现。 这些类型的集为用户提供了集成的查看体验，用户可以通过单击缩略图图像查看项目的不同视图。 通过图像集，您可以呈现某种内容的替代视图，并且查看器提供了缩放工具来仔细检查图像。 [查看名为“正在运行”且使用弹出查看器](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running)的图像集。

在Dynamic Media内部，您可以看到几张跑鞋的图片。 它是销售和营销部门希望客户作为单个演示文稿查看的产品线系列；图像集。

![创建图像集](/help/assets/dynamic-media/assets/dm-create-image-set.png)
_开始创建图像集。_

要创建图像集，请从&#x200B;**[!UICONTROL 创建]**&#x200B;下拉菜单中选择&#x200B;**[!UICONTROL 图像集]**。 请注意，菜单上还有创建&#x200B;**[!UICONTROL 混合媒体集]**、**[!UICONTROL 旋转集]**&#x200B;和&#x200B;**[!UICONTROL 轮播集]**&#x200B;的选项。 创建这些集的方式与创建图像集的方式大致相同。

混合媒体集可以包含图像、样本集、旋转集、视频和自适应视频集。 [尝试它](https://s7d9.scene7.com/s7viewers/html5/MixedMediaViewer.html?asset=Scene7SharedAssets/Mixed_Media_Set_Sample)。 旋转集模拟旋转对象以对其进行检查的真实行为。 利用旋转集，可以从任何角度查看关键的可视详细信息。 [尝试它](https://s7d9.scene7.com/s7viewers/html5/SpinViewer.html?asset=Scene7SharedAssets/SpinSet_Sample&amp;stagesize=500,400){target="_blank"}。

创建图像集非常简单。 您只需添加要包含在集中的图像资源即可。

![创建图像集](/help/assets/dynamic-media/assets/dm-create-image-set-add-assets.png)
_图像集编辑器允许您添加图像资源并对它们在集中的外观重新排序。_

您需要为集提供一个名称。 请仔细选择名称，因为您以后无法编辑它！ 在上述示例中，该集名为`Running`。 完成后，您将保存该集。

这是Experience Manager Assets中的`Running`图像集。

![Experience Manager Assets中正在运行的图像集，卡片视图](/help/assets/dynamic-media/assets/dm-image-set.png)
_Experience Manager Assets卡片视图中的`Running`图像集。_

无论您是否已创建图像集、混合媒体集、旋转集还是任何其他交互式媒体，在创建图像集后，您都可以查看该图像集的显示方式以及客户的行为。 Dynamic Media具有许多内置查看器，可让您做到这一点。

首先，选择构建图像集以在预览中将其打开，如下例所示。

![已选择“查看器”选项的“预览中正在运行的图像集”](/help/assets/dynamic-media/assets/dm-image-set-viewer.png)
_选择了查看器选项预览中的`Running`图像集。_

请注意，在预览中，您可以选择跑步鞋样本并放大和缩小鞋子。 要将查看器应用到集，请从下拉菜单中选择&#x200B;**[!UICONTROL 查看器]**。

![应用了弹出查看器的正在运行的图像集](/help/assets/dynamic-media/assets/dm-image-set-flyout-viewer.png)
_应用了弹出查看器的`Running`图像集。_

在这种情况下，已选择`Flyout`查看器。 此时，您可以预览查看器中设置的图像。 但是，最好是在浏览器中查看它，即客户如何查看它。 选择左下方的&#x200B;**[!UICONTROL URL]**，然后复制该URL并将其粘贴到浏览器中。 [尝试它](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running&amp;config=jpearldemo/Flyout){target="_blank"}。

单个URL允许您在网站上需要使用的位置使用图像集和查看器。 您可能在上一个示例中注意到&#x200B;**[!UICONTROL Embed]**&#x200B;位于URL按钮的右侧。 通过选择&#x200B;**[!UICONTROL 嵌入]**，您可以复制此图像集/查看器的代码，并将其添加到网页或Experience Manager Sites组件中。

弹出查看器是默认的现成查看器，可以编辑其属性。 或者，就像创建图像预设一样，您可以创建自己的自定义查看器。

现在，假设您的销售和营销团队不喜欢弹出查看器。 他们喜欢缩放功能，但他们希望客户能够直接在鞋子上看到缩放效果。 在这种情况下，您只需将InlineZoom查看器应用于图像集，并在浏览器中复制并粘贴其URL以查看其行为。 [尝试它](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running&amp;config=jpearldemo/InlineZoom){target="_blank"}。

当您将鼠标指针移到鞋上时，可以放大该图像，并且可以在移动指针时看到更多细节。 原因很简单，就是最初上传到Dynamic Media的图像的大小。

当你考虑作为消费者生活时，或者当你从事日常工作时，当你访问不同的网站时，你会看到类似这样的事情。 考虑一下如何做到这一点，以及如何在您自己的工作和您公司的网站上使用Dynamic Media的强大功能。

您刚刚阅读了图像集和查看器。 让我们看一下其他几个查看器，并在单个资产上尝试它们。 要重置查看器，请单击左下角的&#x200B;**[!UICONTROL 刷新]**&#x200B;按钮。

<!-- LEAVE THIS HIDDEN PATH IN THE DOCUMENTATION FOR DEMO PURPOSES [Flyout viewer with image set](http://www.partycity.com/girls-little-old-lady-costume-P750948.html) -->

* `ZoomVertical_dark`查看器已应用于图像资源。 [尝试它](https://s7d1.scene7.com/s7viewers/html5/ZoomVerticalViewer.html?asset=jpearldemo/AdobeStock_96311480&amp;config=jpearldemo/ZoomVertical_dark){target="_blank"}。
* `Zoom_light`查看器已应用于图像。 [尝试它](https://s7d1.scene7.com/s7viewers/html5/BasicZoomViewer.html?asset=jpearldemo/AdobeStock_38827423&amp;config=jpearldemo/Zoom_light){target="_blank"}。

## 可选 — 了解详情

如果要详细了解您刚刚阅读的内容，请使用以下材料更详细地探索概念。 否则，您的Dynamic Media历程已完成！

{{see-also-dm}}

<!--
_Dynamic Media Help topics_

* [How to create image presets](/help/assets/dynamic-media/image-presets.md)
* A list of [image processing parameters](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html) that you can use in the Image Modifier field when you create an image preset
* [How to preview assets](/help/assets/dynamic-media/previewing-assets.md)
* [How to preview 3D assets](/help/assets/dynamic-media/previewing-3d-assets.md)
* [How to create Image sets](/help/assets/dynamic-media/image-sets.md)
* [How to create Spin sets](/help/assets/dynamic-media/spin-sets.md)
* [How to create Mixed Media sets](/help/assets/dynamic-media/mixed-media-sets.md) -->

_Dynamic Media教程_

* [将Dynamic Media与Experience Manager Assets结合使用](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-overview-feature-video-use.html)
* [Adobe Experience Manager内容库](https://experienceleague.adobe.com/?lang=en#recommended/solutions/experience-manager) (在&#x200B;_Dynamic Media_&#x200B;上搜索)

_Dynamic Media查看器_

* 每个查看者的[实时演示](https://landing.adobe.com/zh-Hans/na/dynamic-media/ctir-2755/live-demos.html)

<!-- Live as of April 28 2022. LEAVE IN HERE https://landing.adobe.com/en/na/dynamic-media/ctir-2755/index.html -->