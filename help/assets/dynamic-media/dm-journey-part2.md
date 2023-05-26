---
title: 历程Dynamic Media，第二部分
description: Dynamic Media历程介绍了Dynamic Media的基础知识、工作原理、可为您执行的操作，以及它给您的工作和客户带来的价值。
contentOwner: Rick Brough
products: Experience Manager as a Cloud Service
topic-tags: introduction,administering
content-type: reference
feature: Image Profiles
role: User, Admin
mini-toc-levels: 4
hide: false
hidefromtoc: false
exl-id: cdca41ad-a2cd-4f68-aaa4-5eec33c30f0b
source-git-commit: 9202cf44595070c98ca3d21887dff257bcd88b87
workflow-type: tm+mt
source-wordcount: '2878'
ht-degree: 0%

---

# Dynamic Media历程：基础知识，第二部分  {#dm-journey-part2}

欢迎访问Dynamic Media历程：基础知识，第II部分，您可以从中了解以下内容：

* Dynamic Media URL的剖析，以及Dynamic Media如何交付内容
* 创建图像预设以渲染资产的基础知识
* 图像集、旋转集和混合媒体集

另请参阅 [Dynamic Media历程；基础知识，第一部分](/help/assets/dynamic-media/dm-journey-part1.md).

>[!TIP]
>
>为获得最佳结果，Adobe建议您在台式计算机上阅读并查看此Dynamic Media历程。

## Dynamic Media URL的剖析，以及Dynamic Media如何交付内容 {#dm-journey-d}

上传和发布Dynamic Media资源后，您可以复制资源生成的URL并将其粘贴到浏览器中，以查看向客户显示的资源的外观。 手表图像的以下复制URL按颜色进行划分，使其更易于阅读和理解。

![Dynamic Media URL的剖析](/help/assets/dynamic-media/assets/dm-colored-url.png)
_Dynamic Media URL的剖析。_

URL的第一部分（红色）是引用服务器域本身。 在这种情况下，Dynamic Media运行在通用服务器域上，该域是 `https://s7d1.scene7.com/is/image/`. 通过查看服务器域，可以轻松查看一组图像并了解Dynamic Media是否为这些图像提供服务。 URL将非常一致。 但是，有一些Dynamic Media客户已切换到专用服务器域，该域可能位于该域中 `name-of-your-company.scene7.com`. 智能成像需要专用服务器域。

帐户名称是紫色部分。 在这种情况下，将调用该帐户 `jpearldemo`.

资产ID或名称， `AdobeStock_28563982` 是绿色的。 请注意，该资产具有 _否_ 文件扩展名，例如 `.png` 或 `.jpg`. 将资源摄取到Dynamic Media中时，会剥离文件扩展名，并创建另一种类型的文件：金字塔TIFF文件。 金字塔TIFF允许Dynamic Media动态快速创建演绎版。

最后给出一些图像处理参数， `?wid=1000&fmt=jpeg&qlt=85`，以黄色显示在末尾。

整个URL路径都是实时的。 [试试看](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_28563982?wid=1000&amp;fmt=jpeg&amp;qlt=85){target="_blank"}.

在浏览器窗口仍打开并显示Dynamic Media URL和监视图像的情况下，让我们仔细看看如何通过更改URL来创建图像的演绎版。

### 通过URL渲染监视图像

首先，仅手动删除URL路径中的图像处理规则；保留服务器名称、帐户名称以及资产ID或图像名称。 [试试看](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_28563982){target="_blank"}.

现在，将图像处理参数添加到URL的末尾。 在URL字段中，在图像名称的右侧，键入 `?wid=500`，然后按键 **[!UICONTROL 输入]**. [试试看](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=500){target="_blank"}.

请注意，将生成监视的新演绎版。 从这种更改图像宽度的简单练习中，有一个关键要点是完全动态地生成所看到的图像。

现在更改宽度值 `500` 像素至 `1000` 像素，然后按 **[!UICONTROL 输入]**. [试试看](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000){target="_blank}.
按下时 **[!UICONTROL 输入]**，则浏览器将返回到Dynamic Media Image Server。 它会根据您刚刚输入的新宽度值生成手表的全新演绎版，然后将新图像交付回浏览器，并缓存该图像。

Dynamic Media具有许多图像处理参数，您可以使用这些参数微调网页上的图像资源。 您可以 [在此处查看它们的列表](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html?lang=en).

现在，尝试向监视图像添加旋转参数。 URL路径的末尾，紧跟在 `wid=1000`，类型 `&rotate=90`，然后按下 **[!UICONTROL 输入]**. [试试看](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000&amp;rotate=90){target="_blank"}.

这块表还是稍微向左倾斜。 更改旋转值 `90` 到 `92`，然后按下 **[!UICONTROL 输入]**. [试试看](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000&amp;rotate=9){target="_blank"}.

再说一次，只要你按下 **[!UICONTROL 输入]**，会几乎立即生成手表的新演绎版。 您可以看到您获得的性能类型，这解释了为什么Dynamic Media可以提供超过800,000个图像请求， _每秒_、忙碌的周末或大假日。

虽然可以逐个图像更改URL中的图像处理参数，但这不是一种有效方法，尤其是在您的网站上包含成千上万张图像的情况下。 一种更好的方法是使用图像预设。

## 创建图像预设以渲染资产的基础知识 {#dm-journey-e}

有多种方法和位置可让您创建图像或让图像可用。 传统上，Creative进入Adobe Photoshop，并将每个演绎版保存为静态图像。

![静态图像](/help/assets/dynamic-media/assets/dm-static-images.png)
_良好：静态图像，每个图像都是手动创建的。_

想象一下Creative Director看着图片说，

_“我真的很想拍这张照片，好让大手指4个，小手指1个，好让表盘更容易看到。”_

创意人员必须重新拍摄所有这些新的静态图像。

但是，通过Dynamic Media，如果您有不同的图像预设，则可以在需要时随时使用这些图像。 图像预设强制执行标准。

![主要文件方法](/help/assets/dynamic-media/assets/dm-onefile.png)
_最佳：一个文件，其中包含使用图像预设即时创建的多个演绎版，例如 `Search_Grid` 和 `Thumbnail`._

| **为何使用图像预设？** |  |
|---|---|
| 标准 | 图像预设对由其请求的任何图像强制执行标准图像处理处理。 |
| 变更管理 | 如果必须更改图像处理，则只需编辑现有图像预设的参数即可。 更新的定义会自动传播到所有请求。 |

每个您需要拥有特定图像类型的位置，例如，

* 产品详细信息页面，
* 搜索网格，
* 缩略图，
* 购物卡，或
* 主页图像

您希望在任何位置使用该图像时，都使用相同的参数进行投放。

让我们看一下如何在Dynamic Media中创建图像预设。

![创建图像预设，从“基本”选项卡开始](/help/assets/dynamic-media/assets/dm-image-preset-basictab.png)
_从“基本”选项卡开始创建图像预设。_

在上面的示例中，您可以看到使用名称创建了新图像预设 _中_. Dynamic Media使用现成可用的图像（背包）作为示例，帮助您查看在创建图像预设时图像预设的特性。

此 _中_ 图像预设的宽度为500像素，高度为800像素。 在本历程的第一部分中，您已阅读有关以不同格式交付资源的说明。 从 **[!UICONTROL 格式]** 下拉菜单中，您可以选择以JPEG、PNG、TIFF或多种其他格式交付资产。 您在此具有灵活性。

选择 **[!UICONTROL 高级]** 选项卡为您提供资源的颜色空间选项。 根据您在 **[!UICONTROL 基本]** 选项卡 — 在上例中选择了JPEG — 您可以以RGB、灰度或CMYK格式交付资源。 从 **[!UICONTROL 颜色配置文件]** 在下拉菜单中，您可以选择如何交付要用于打印的CMYK图像资产。 另外请注意，还可以应用其他参数来锐化图像。 在这个案例中， **[!UICONTROL 钝化蒙版]** 已应用。

![通过从“高级”选项卡中选择选项来创建图像预设](/help/assets/dynamic-media/assets/dm-image-preset-advancedtab.png)
_通过从“高级”选项卡中选择选项来创建图像预设。_

您回想一下 [Dynamic Media URL的剖析](#dm-journey-d) 之前，您将了解有关Dynamic Media URL及其构建方式的信息。 此 **[!UICONTROL 图像修饰符]** 可在文本框中键入所需的任何其他图像处理参数。 使用预设交付图像时，这些参数包含在URL的预设名称中。 在上面的屏幕快照中，参数 `bgc=451B15` 添加了。 即，添加了深棕色背景颜色。

您可以将图像预设视为图像的指导方针。 它会传送任何使用预设的图像，每次都一致；都会一样。 参数 `&op_brightness=+10` 还增加了稍微增加亮度的功能。

完成后，保存预设，该预设现在可用于您拥有的所有图像。 在本例中，我们要应用 _中_ 图像预设为一碗液态巧克力的图像。

![应用图像预设 *中* 生成图像的演绎版](/help/assets/dynamic-media/assets/dm-medium-image-preset.png)
_应用图像预设媒体以生成图像的演绎版。_

复制URL，然后将其粘贴到浏览器中以检查图像的外观。 [试试看](http://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_74043302?$Medium$){target="_blank"}.

在浏览器中，注意图像预设的名称 _中_ 在完整URL路径中。

您可以看到图像中所显示的清晰度。 这种品质部分归功于这碗巧克力的投球方式。 此外，部分原因在于，与Dynamic Media相比，您可以存储更大的图像。

如果你的一碗巧克力看起来一切正常，你可以在网页上粘贴自己想要图像出现在网站上的位置。

如果您再次查看下面的观看图像，您可以看到有一个 `Cart` 图像预设，a `Grid` 预设， a `Large` 预设， a `PDP-page` （产品详细信息页面）预设以及其他多个预设。

![静态和动态图像预设](/help/assets/dynamic-media/assets/dm-image-presets.png)
_静态和动态图像预设。 观看图像是使用 `PDP-page` 图像预设。_

但是，如果您必须更改网站上的图像，该怎么办？ 例如，假设您已经进行了一些测试，发现图像为120 x 120 (即 `Cart` 图像预设)未按您预期的那样被接收。 您必须通过将宽度增加到175像素并将高度增加到175像素来增大图像。 传统上，您必须进入Adobe Photoshop并重新创建所有这些购物车图像。 但使用Dynamic Media，您只需通过将宽度和高度值更新为175并保存预设来编辑图像预设即可，如下例所示。

![编辑图像预设](/help/assets/dynamic-media/assets/dm-edit-image-preset.png)
_编辑的宽度和高度 `Cart` 图像预设。_

在更改图像预设并清除缓存后，所有图像都会更新，并且与该预设一起使用的所有URL都会 _非_ 随处改变。 这意味着无需断开链接和网页重定向。

## 图像集、旋转集和混合媒体集 {#dm-journey-f}

Dynamic Media的一些更常用的用途是允许您创建图像集、旋转集和混合媒体集。

图像集通常由一系列图像资产组成，这些资产以单个实体的形式呈现。 这些类型的集为用户提供了集成的查看体验，用户可通过单击缩略图图像查看项目的不同视图。 通过图像集，您可以呈现一些内容的替代视图，并且查看器提供了缩放工具来仔细检查图像。 [查看名为“正在运行”且使用弹出查看器的图像集](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running).

在Dynamic Media内部，您可以看到几张跑鞋的图片。 它是销售和营销部门希望客户作为单个演示文稿查看的产品线系列，即图像集。

![创建图像集](/help/assets/dynamic-media/assets/dm-create-image-set.png)
_创建图像集的开始。_

要创建图像集，请选择 **[!UICONTROL 图像集]** 从 **[!UICONTROL 创建]** 下拉菜单。 请注意，菜单上也有用于创建 **[!UICONTROL 混合媒体集]**， a **[!UICONTROL 旋转集]**，和 **[!UICONTROL 轮播集]**. 创建这些集的方式与创建图像集的方式大致相同。

混合媒体集可以包含图像、样本集、旋转集、视频和自适应视频集。 [试试看](https://s7d9.scene7.com/s7viewers/html5/MixedMediaViewer.html?asset=Scene7SharedAssets/Mixed_Media_Set_Sample). 旋转集模拟实际操作来旋转对象以对其进行检查。 利用旋转集，可以从任何角度查看关键的可视详细信息。 [试试看](https://s7d9.scene7.com/s7viewers/html5/SpinViewer.html?asset=Scene7SharedAssets/SpinSet_Sample&amp;stagesize=500,400){target="_blank"}.

创建图像集很简单。 您只需添加要包含在集中的图像资源即可。

![创建图像集](/help/assets/dynamic-media/assets/dm-create-image-set-add-assets.png)
_使用图像集编辑器，可添加图像资源并对它们在集中的外观重新排序。_

您需要为集提供一个名称。 请仔细选择名称，因为以后无法编辑它！ 在上面的示例中，将调用该集 `Running`. 完成后，保存集。

这里是 `Running` Experience Manager Assets中的图像集。

![Experience Manager Assets中的运行图像集，卡片视图](/help/assets/dynamic-media/assets/dm-image-set.png)
_此 `Running` Experience Manager Assets中的图像集，卡片视图。_

无论您是否已创建图像集、混合媒体集、旋转集还是任何其他交互式媒体，在创建图像集后，您都可以查看该图像集对于客户的显示和行为方式。 Dynamic Media具有许多内置查看器，可让您做到这一点。

首先，选择构建的图像集在预览中将其打开，如下例所示。

![选中了查看器选项后，在预览中运行图像集](/help/assets/dynamic-media/assets/dm-image-set-viewer.png)
_此 `Running` 选中查看器选项时，在预览中设置图像。_

请注意，在预览中，您可以选择跑步鞋样本并放大和缩小鞋子。 要将查看器应用到集，请选择 **[!UICONTROL 查看器]** 下拉菜单中。

![应用了弹出查看器的运行图像集](/help/assets/dynamic-media/assets/dm-image-set-flyout-viewer.png)
_此 `Running` 应用了弹出查看器的图像集。_

在本例中， `Flyout` 已选择查看器。 此时，您可以预览查看器中设置的图像。 但是，最好是在浏览器中看到它，即客户如何看到它。 您选择 **[!UICONTROL URL]** 然后复制URL并将其粘贴到浏览器中。 [试试看](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running&amp;config=jpearldemo/Flyout){target="_blank"}.

单个URL允许您在网站上所需的位置使用图像集和查看器。 您在前面的示例中可能已经注意到 **[!UICONTROL 嵌入]** 位于URL按钮的右侧。 通过选择 **[!UICONTROL 嵌入]**，您可以复制此图像集/查看器的代码，并将其添加到网页或Experience Manager Sites组件中。

弹出查看器是默认的现成查看器，可以编辑其属性。 或者，就像创建图像预设一样，您可以创建自己的自定义查看器。

现在，假设您的销售和营销团队不喜欢弹出查看器。 他们喜欢缩放功能，但他们希望客户能够直接在鞋子上看到缩放效果。 在这种情况下，您只需将InlineZoom查看器应用于图像集，并在浏览器中复制和粘贴其URL以查看其行为。 [试试看](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running&amp;config=jpearldemo/InlineZoom){target="_blank"}.

当您将鼠标指针移到鞋子上时，可以放大该图像，并且可以在移动指针时看到更多细节。 原因很简单，就是最初上传到Dynamic Media的图像的大小。

当你考虑作为消费者生活时，或者当你从事日常工作时，当你访问不同的网站时，你会看到类似这样的事情。 思考如何做到这一点，以及如何在您自己的工作和您公司的网站上使用Dynamic Media的强大功能。

你只需要读一点关于影像集和观众的知识。 让我们看一下其他几个查看者，并在单个资产上尝试它们。 要重置查看器，请单击 **[!UICONTROL 刷新]** 按钮。

<!-- LEAVE THIS HIDDEN PATH IN THE DOCUMENTATION FOR DEMO PURPOSES [Flyout viewer with image set](http://www.partycity.com/girls-little-old-lady-costume-P750948.html) -->

* `ZoomVertical_dark` 已将查看器应用于图像资源。 [试试看](https://s7d1.scene7.com/s7viewers/html5/ZoomVerticalViewer.html?asset=jpearldemo/AdobeStock_96311480&amp;config=jpearldemo/ZoomVertical_dark){target="_blank"}.
* `Zoom_light` 应用于图像的查看器。 [试试看](https://s7d1.scene7.com/s7viewers/html5/BasicZoomViewer.html?asset=jpearldemo/AdobeStock_38827423&amp;config=jpearldemo/Zoom_light){target="_blank"}.

## 可选 — 了解详情

如果您想详细了解刚刚阅读的内容，请使用以下材料更详细地探索概念。 否则，您的Dynamic Media历程已完成！

_Dynamic Media帮助主题_

* [如何创建图像预设](/help/assets/dynamic-media/image-presets.md)
* 列表 [图像处理参数](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html) 创建图像预设时，可在“图像修饰符”字段中使用的修饰符
* [如何预览资源](/help/assets/dynamic-media/previewing-assets.md)
* [如何预览三维资源](/help/assets/dynamic-media/previewing-3d-assets.md)
* [如何创建图像集](/help/assets/dynamic-media/image-sets.md)
* [如何创建旋转集](/help/assets/dynamic-media/spin-sets.md)
* [如何创建混合媒体集](/help/assets/dynamic-media/mixed-media-sets.md)

_Dynamic Media教程_

* [将Dynamic Media与Experience Manager Assets结合使用](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-overview-feature-video-use.html)
* [Adobe Experience Manager内容库](https://experienceleague.adobe.com/?lang=en#recommended/solutions/experience-manager) (搜索 _Dynamic Media_)

_Dynamic Media查看器_

* [实时演示](https://landing.adobe.com/zh-Hans/na/dynamic-media/ctir-2755/live-demos.html) 每个查看者的

<!-- Live as of April 28 2022. LEAVE IN HERE https://landing.adobe.com/en/na/dynamic-media/ctir-2755/index.html -->