---
title: Dynamic Media历程，第二部分
description: Dynamic Media历程涵盖Dynamic Media的基础知识、工作方式、可为您做什么、以及它为您的工作和客户带来什么价值。
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
source-git-commit: 94d77e08e5df82f9bb432bb06c4f05301d119f9e
workflow-type: tm+mt
source-wordcount: '2817'
ht-degree: 0%

---

# Dynamic Media历程:基础知识，第二部分  {#dm-journey-part2}

欢迎使用Dynamic Media历程:基础知识，第二部分，您可以从中学习以下内容：

* Dynamic Media URL及Dynamic Media如何交付内容的剖析
* 创建图像预设以渲染资产的基础知识
* 图像集、旋转集和混合媒体集

另请参阅 [Dynamic Media历程;基础知识，第一部分](/help/assets/dynamic-media/dm-journey-part1.md).

>[!TIP]
>
>为获得最佳结果，Adobe建议您在台式计算机上阅读和查看Dynamic Media历程。

## Dynamic Media URL及Dynamic Media如何交付内容的剖析 {#dm-journey-d}

上传和发布Dynamic Media资产后，您可以复制资产生成的URL，并将其粘贴到浏览器中，以了解资产将如何显示给客户。 以下复制的手表图像URL按颜色划分，以便于阅读和理解。

![Dynamic Media URL剖析](/help/assets/dynamic-media/assets/dm-colored-url.png)
_Dynamic Media URL的解剖。_

URL的第一部分以红色表示，引用服务器域本身。 在这种情况下，Dynamic Media在通用服务器域(即 `https://s7d1.scene7.com/is/image/`. 只需查看服务器域，便能轻松查看一组图像并了解Dynamic Media是否提供了这些图像。 URL将保持相当一致。 但是，有些Dynamic Media客户已切换到可能位于的专用服务器域 `name-of-your-company.scene7.com`. 智能成像需要专用的服务器域。

帐户名称是紫色的部分。 在这种情况下，该帐户称为 `jpearldemo`.

资产ID或名称， `AdobeStock_28563982` 为绿色。 请注意，资产已 *否* 文件扩展名，如 `.png` 或 `.jpg`. 将资产摄取到Dynamic Media后，将删除文件扩展名，并创建不同类型的文件：金字塔TIFF文件。 通过TIFF图像，Dynamic Media可以即时快速创建演绎版。

最后，还有一些图像处理参数， `?wid=1000&fmt=jpeg&qlt=85`，在末尾以黄色显示。

整个URL路径处于实时状态。 [试试看](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_28563982?wid=1000&amp;fmt=jpeg&amp;qlt=85).

由于您的浏览器窗口仍然会打开Dynamic Media URL和Watch图像，因此我们将进一步了解您如何只通过更改URL来创建图像的演绎版。

### 通过URL呈现监视图像

首先，手动仅删除URL路径中的图像处理规则；保留服务器名称、帐户名称以及资产ID或图像名称。 [试试看](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_28563982).

现在，在URL的末尾添加一个图像处理参数。 在“URL”字段中，在图像名称右侧键入 `?wid=500`，然后按 **[!UICONTROL 输入]**. [试试看](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=500).

请注意，手表的新呈现版本已生成。 要了解更改图像宽度这一简单练习的一个关键内容是，所看到的图像是100%动态生成的。

现在，更改 `500` 像素到 `1000` 像素，然后按 **[!UICONTROL 输入]**. [试试看](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000).
你按下 **[!UICONTROL 输入]**，则浏览器将返回到Dynamic Media图像服务器。 它会根据您刚刚输入的新宽度值生成手表的全新呈现版本，然后将新图像交回浏览器并缓存。

Dynamic Media具有许多图像处理参数，可用于在网页上微调图像资产。 您可以 [请在此处查看这些列表](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html?lang=en).

现在，尝试向监视图像添加旋转参数。 URL路径的结尾，紧接 `wid=1000`，类型 `&rotate=90`，然后按 **[!UICONTROL 输入]**. [试试看](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000&amp;rotate=90).

手表还是略偏左。 更改 `90` to `92`，然后按 **[!UICONTROL 输入]**. [试试看](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000&amp;rotate=9)

再说一遍，你按下 **[!UICONTROL 输入]**，则表格的新呈现会近乎瞬间生成。 您可以看到您获得的性能，这解释了为什么Dynamic Media可以提供超过800,000个图像请求， *每秒*、在繁忙的周末或大节假日。

虽然可以逐个图像更改URL中的图像处理参数，但这种方法并不有效，尤其是当您的网站上有数万幅图像时。 使用图像预设是一种更好的方法。

## 创建图像预设以渲染资产的基础知识 {#dm-journey-e}

您希望通过多种方式和位置来创建图像或使图像可用。 传统上，创作元素会进入Adobe Photoshop，并将每个不同的演绎版另存为静态图像。

![静态图像](/help/assets/dynamic-media/assets/dm-static-images.png)
_好：静态图像，每个图像都是手动创建的。_

想象一下，创意Director看着这些图片说，

_“我真的想拍这张表，这样大手指向四，小手指向1，让表盘更容易看。”_

创意人员必须再次重新拍摄所有这些新的静态图像。

但是，使用Dynamic Media时，如果您有不同的图像预设，则可以在需要时随处使用这些图像。 图像预设强制标准。

![主文件方法](/help/assets/dynamic-media/assets/dm-onefile.png)
_最佳：一个文件，其中包含使用图像预设即时创建的多个演绎版，例如 `Search_Grid` 和 `Thumbnail`._

| **为何使用图像预设？** |  |
|---|---|
| 标准 | 图像预设可对随请求的图像强制执行标准图像处理处理。 |
| 变更管理 | 如果必须更改图像处理，则只需编辑现有图像预设的参数即可。 更新的定义会自动传播到所有请求中。 |

例如，您需要具有特定类型图像的每个位置，

* 产品详细信息页面，
* 搜索网格，
* 缩略图，
* 购物卡，或
* 主页图像

您希望无论在何处使用图像，都使用相同的参数来传送图像。

现在，我们来看一下图像预设是如何在Dynamic Media中创建的。

![从“基本”选项卡开始创建图像预设](/help/assets/dynamic-media/assets/dm-image-preset-basictab.png)
_从“基本”选项卡开始创建图像预设。_

在以上示例中，您可以看到已使用名称创建新的图像预设 _中_. Dynamic Media使用一个现成的图像（即背包）示例，帮助您在创建图像预设时查看图像预设的特性。

的 _中_ 图像预设的宽度为500像素，高度为800像素。 在本历程的第一部分中，您阅读了有关以不同格式传送资产的内容。 从 **[!UICONTROL 格式]** 下拉菜单中，您可以选择以JPEG、PNG、TIFF或多种其他格式来交付资产。 你在这里很灵活。

选择 **[!UICONTROL 高级]** 选项卡会为您提供资产的色彩空间选项。 根据您在 **[!UICONTROL 基本]** 选项卡 — 在上面的示例中，已选择JPEG — 您可以以RGB、灰度或CMYK来传送资产。 从 **[!UICONTROL 颜色配置文件]** 下拉菜单中，您可以选择如何传送用于打印的CMYK图像资产。 另请注意，您还可以应用其他参数来锐化图像。 在这种情况下， **[!UICONTROL 钝化蒙版]** 的次数。

![通过从高级选项卡中选择选项来创建图像预设](/help/assets/dynamic-media/assets/dm-image-preset-advancedtab.png)
_通过从高级选项卡中选择选项来创建图像预设。_

你记得 [Dynamic Media URL剖析](#dm-journey-d) 以前，您阅读了有关Dynamic Media URL及其构建方式的信息。 的 **[!UICONTROL 图像修饰符]** 在文本框中，您可以键入任何需要的其他图像处理参数。 使用预设传送图像后，这些参数将包含在URL的预设名称中。 在上面的屏幕截图中，参数 `bgc=451B15` 添加。 即，添加了一种深棕色背景颜色。

您可以将图像预设视为图像的方法。 它每次都会以一致的方式传送任何使用预设的图像；会一样的。 参数 `&op_brightness=+10` 以略微增加亮度。

完成后，您会保存预设，现在该预设可用于您拥有的所有图像。 在这种情况下，我们要应用 _中_ 图像预设为一碗液态巧克力的图像。

![应用图像预设 *中* 生成图像的呈现版本](/help/assets/dynamic-media/assets/dm-medium-image-preset.png)
_应用图像预设媒体以生成图像的呈现版本。_

复制URL，然后将其粘贴到浏览器中，以检查图像的外观。 [试试看](http://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_74043302?$Medium$). 在您的浏览器中，请注意图像预设的名称 _中_ 在完整URL路径中。

您可以看到图像中显示的清晰度。 这种品质部分要归功于这碗巧克力的拍摄方式。 此外，这在一定程度上是因为使用Dynamic Media，您可以存储比交付到数字渠道的图像大的图像。

如果一碗巧克力的一切看起来都令人满意，请将URL粘贴到您的网页中，以便将图像显示在您的网站上。

如果您再次查看下面的手表图像，您会看到 `Cart` 图像预设， `Grid` 预设， `Large` 预设， `PDP-page` （产品详细信息页面）预设，以及其他几个预设。

![静态和动态图像预设](/help/assets/dynamic-media/assets/dm-image-presets.png)
_静态和动态图像预设。 手表图像使用 `PDP-page` 图像预设。_

但是，如果您必须更改网站上的图像，该怎么办？ 例如，假设您已经完成了一些测试，并发现图像的长度为120 x 120( `Cart` 图像预设)。 必须将宽度增加到175像素，将高度增加到175像素，从而使图像变大。 传统上，您必须进入Adobe Photoshop并重新创建所有这些购物车图像。 但是，使用Dynamic Media，您只需通过将宽度和高度值更新为175并保存预设来编辑图像预设，如以下示例所示。

![编辑图像预设](/help/assets/dynamic-media/assets/dm-edit-image-preset.png)
_编辑 `Cart` 图像预设。_

在更改图像预设并刷新缓存后，所有图像都会更新，并且该预设中使用的所有URL都会更新 _not_ 随处更改。 这意味着无需断开链接和网页重定向。

## 图像集、旋转集和混合媒体集 {#dm-journey-f}

Dynamic Media的一些较受欢迎用途是允许您创建图像集、旋转集和混合媒体集。

图像集通常由一系列作为单个实体呈现的图像资产组成。 这些类型的集合为用户提供了集成的查看体验，用户可以通过单击缩略图来查看项目的不同视图。 图像集允许您显示某些内容的替代视图，并且查看器提供了用于仔细检查图像的缩放工具。 [查看名为“正在运行”的图像集，该图像集使用弹出查看器](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running).

在Dynamic Media内，您可以看到几张跑鞋的图像。 它是一个产品系列，销售和营销部门希望客户将其视为单一演示；图像集。

![创建图像集](/help/assets/dynamic-media/assets/dm-create-image-set.png)
_开始创建图像集。_

要创建图像集，请选择 **[!UICONTROL 图像集]** 从 **[!UICONTROL 创建]** 下拉菜单。 请注意，菜单中还有一些用于创建 **[!UICONTROL 混合媒体集]**, a **[!UICONTROL 旋转集]**&#x200B;和 **[!UICONTROL 轮播集]**. 创建这些集的方式与创建图像集的方式大致相同。

混合媒体集可以包含图像、色板集、旋转集、视频和自适应视频集。 [试试看](https://s7d9.scene7.com/s7viewers/html5/MixedMediaViewer.html?asset=Scene7SharedAssets/Mixed_Media_Set_Sample). 旋转集模拟旋转对象的真实动作，以对其进行检查。 旋转集允许从任何角度查看关键的可视细节。 [试试看](https://s7d9.scene7.com/s7viewers/html5/SpinViewer.html?asset=Scene7SharedAssets/SpinSet_Sample&amp;stagesize=500,400).

创建图像集非常简单。 您只需添加要包含在规则集中的图像资产即可。

![创建图像集](/help/assets/dynamic-media/assets/dm-create-image-set-add-assets.png)
_图像集编辑器允许您添加图像资产并重新排序其在图像集中的外观。_

您需要为集指定一个名称。 请仔细选择名称，因为以后无法编辑该名称！ 在以上示例中，该集称为 `Running`. 完成后，您保存该集。

这是 `Running` 在Experience Manager Assets中设置图像。

![在Experience Manager Assets卡片视图中运行的图像集](/help/assets/dynamic-media/assets/dm-image-set.png)
_的 `Running` 在卡片视图中的Experience Manager Assets中设置图像。_

无论您是创建了图像集、混合媒体集、旋转集还是任何其他交互式媒体，在创建图像集后，您都希望了解该集的显示和行为方式。 Dynamic Media有众多内置查看器，您可以通过它来实现这一点。

首先，选择构建的图像集以在预览中将其打开，如以下示例所示。

![在预览中运行图像集，并选择查看器选项](/help/assets/dynamic-media/assets/dm-image-set-viewer.png)
_的 `Running` 在预览中设置图像，并选择查看器选项。_

请注意，在预览中，您可以选择跑鞋色板并放大和缩小鞋。 要将查看器应用到该集，请选择 **[!UICONTROL 查看器]** 中。

![应用了弹出查看器的运行图像集](/help/assets/dynamic-media/assets/dm-image-set-flyout-viewer.png)
_的 `Running` 在应用弹出查看器时设置的图像。_

在本例中， `Flyout` 查看器。 此时，您可以预览查看器中的图像集。 但是，最好在浏览器中查看它，即客户如何查看它。 您选择 **[!UICONTROL URL]** 在左下方，复制URL并将其粘贴到浏览器中。 [试试看](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running&amp;config=jpearldemo/Flyout).

通过单个URL，您可以在网站上需要的图像集和查看器的位置使用它们。 您可能在上一个示例中注意到 **[!UICONTROL 嵌入]** 在URL按钮的右侧。 通过选择 **[!UICONTROL 嵌入]**，则可以复制此图像集/查看器的代码，并将其添加到网页或Experience Manager Sites组件中。

弹出查看器是一个默认的现成查看器，您可以编辑其属性。 或者，与创建图像预设一样，您也可以创建自己的自定义查看器。

假设您的销售和营销团队不喜欢弹出查看器。 他们喜欢缩放功能，但希望客户直接在鞋上查看缩放效果。 在这种情况下，您只需将InlineZoom查看器应用到图像集，并复制其URL并将其粘贴到浏览器中，即可查看其行为方式。 [试试看](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running&amp;config=jpearldemo/InlineZoom).

将鼠标指针移到鞋上时，放大到该图像，当鼠标指针移动时，可以看到更多细节。 原因只是最初上传到Dynamic Media的图像大小。

当你考虑以消费者的身份生活，或者当你在日常工作中工作时，当你访问不同的网站时，你会看到这样的东西。 想想这是怎么做到的，以及如何在您自己的工作和公司网站上使用Dynamic Media的力量。

您只需阅读一些关于图像集和查看器的内容。 让我们看看其他几个查看者，并在单个资产上试用它们。 要重置查看器，请单击 **[!UICONTROL 刷新]** 按钮。

<!-- LEAVE THIS HIDDEN PATH IN THE DOCUMENTATION FOR DEMO PURPOSES [Flyout viewer with image set](http://www.partycity.com/girls-little-old-lady-costume-P750948.html) -->

* `ZoomVertical_dark` 查看器。 [试试看](https://s7d1.scene7.com/s7viewers/html5/ZoomVerticalViewer.html?asset=jpearldemo/AdobeStock_96311480&amp;config=jpearldemo/ZoomVertical_dark).
* `Zoom_light` 查看器。 [试试看](https://s7d1.scene7.com/s7viewers/html5/BasicZoomViewer.html?asset=jpearldemo/AdobeStock_38827423&amp;config=jpearldemo/Zoom_light).

## 了解更多

_Dynamic Media主题_

* [创建图像预设](/help/assets/dynamic-media/image-presets.md)
* 列表 [图像处理参数](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html) 在创建图像预设时，您可以在“图像修饰符”字段中使用的预设值
* [预览资源](/help/assets/dynamic-media/previewing-assets.md)
* [预览 3D 资源](/help/assets/dynamic-media/previewing-3d-assets.md)
* [图像集](/help/assets/dynamic-media/image-sets.md)
* [旋转集](/help/assets/dynamic-media/spin-sets.md)
* [混合媒体集](/help/assets/dynamic-media/mixed-media-sets.md)

_Dynamic Media教程_

* [将Dynamic Media与Experience Manager Assets结合使用](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-overview-feature-video-use.html)
* [Adobe Experience Manager内容库](https://experienceleague.adobe.com/?lang=en#recommended/solutions/experience-manager) (搜索 _Dynamic Media_)