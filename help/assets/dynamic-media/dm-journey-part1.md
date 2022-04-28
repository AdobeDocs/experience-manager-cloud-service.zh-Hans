---
title: Dynamic Media历程，第一部分
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
exl-id: f3472006-d5ae-4f70-af3e-44e73aee85cc
source-git-commit: 69d2121323d8a8ab54db3fb0a56195a1271e6112
workflow-type: tm+mt
source-wordcount: '3585'
ht-degree: 2%

---

# Dynamic Media历程:基础知识，第一部分 {#dm-journey-part1}

欢迎来到Dynamic Media历程。

此历程涵盖Dynamic Media的基础知识、工作方式、可为您做什么以及它对您的工作和客户有何价值。

**_前提条件_**

* 对图像和视频格式的基本了解
* HTML和CSS的基本了解
* 对设计工具(如Adobe Illustrator、Adobe Photoshop、Adobe XD)的基本了解
* 在Experience Manager中访问Dynamic Media非常有用，但并非必需

**_您希望了解的内容_**

_第一部分_

* 什么是Dynamic Media，它有什么帮助吗？
* Dynamic Media用例
* 资产如何通过Dynamic Media系统

_第二部分_

* Dynamic Media URL及Dynamic Media如何交付内容的剖析
* 创建图像预设以渲染资产的基础知识
* 图像集、旋转集和混合媒体集

**_受众_**
最适合此历程读者的受众包括以下刚接触Dynamic MediaExperience Manager的受众：

* 管理员
* 业务分析师
* 内容架构师
* 内容作者
* Designer
* 开发人员
* 营销
* 产品经理/所有者

>[!TIP]
>
>为获得最佳结果，Adobe建议您在台式计算机上阅读和查看Dynamic Media历程。

## 什么是Dynamic Media，它有什么帮助吗？ {#dm-journey-a}

Dynamic Media可帮助您按需提供丰富的可视化推销和营销资产。 它还可帮助您创建和提供交互式查看体验，包括缩放、360度旋转和视频。 您的资产会根据Web、移动设备和社交网站的使用情况进行动态缩放。 使用一组主源资产（如图像、视频和3D），Dynamic Media通过其全球、可扩展、性能优化的CDN（内容交付网络）实时生成并交付此丰富内容的多个变体。

Dynamic Media整合了Adobe Experience Manager Assets数字资产管理解决方案的工作流程，以简化和简化数字营销活动管理流程。

### 一个文件，有无限的可能性

要了解Dynamic Media的一个要点是 _一个主资产文件，可提供无限的可能性_.

要更好地了解此概念，请考虑您传统处理单个资产（如图像或视频）的方式。 您通常会创建一个主资产。 然后，您可以为每个体验、每个所需设备、每个网页以及使用该资产的每个属性手动创建同一资产的版本。 随着时间的推移，该单个资产可能会增长到20、30或更多版本，并且不会附加任何版本历史记录。 现在，想象一下，对于您拥有的每个图像或视频，都要这样做。 维护和更新的资产版本数量将很快变得非常庞大，更不用说存储成本的增加了。

但是，Dynamic Media与其他系统有根本不同，因为您使用它来传送媒体 _动态_ 来自单个、主资产和URL调用。 您请求的Dynamic Media URL路径包含相关说明，这些说明会告知Adobe发布服务器在将资产交付到客户屏幕时如何显示资产。 例如，使用同一个主资产，您可以立即以无限的呈现形式交付资产，从而更改大小、格式、分辨率、粗细、颜色、裁剪以及缩放视图等效果。

这种独特的交付方法可确保将一致的质量体验发送到任何屏幕，而不管其大小或带宽如何。 全尺寸视频还针对所有屏幕类型进行了优化，并自适应地流式传输，以确保用户体验的一致性和质量。

<!-- As part of building and publishing assets with Dynamic Media, you visually configure the effects that you want to apply to assets. In so doing, you are literally building the URL that correctly tells the publish server how to deliver your primary asset to the screen.  -->

![AdobeDynamic Media以不同的大小和格式将相同的主图像提供给不同的媒体。](/help/assets/dynamic-media/assets/dm-oneasset-multioutput.png)
_AdobeDynamic Media可确保向任何屏幕提供一致的高质量体验，而无论其大小或带宽如何。_

正如您所阅读的，您将进一步了解为什么“一个主资产文件，无限可能”的概念很重要。

### 内容交付网络

当您准备好使用图像资产或视频资产上线时，Dynamic Media的骨干网将支持该功能，该骨干网由功能强大的顶层交付网络组成。 该网络每天为世界各地的数百个客户提供服务。 资产由Akamai托管在内容交付网络（或CDN）上分发。 CDN是一个计算机服务系统，它们通过网络实现透明地协作，以向最终用户交付内容，尤其是大型富媒体内容。

在CDN系统中，Web内容通过Internet存储在Web缓存中。 然后，它会从Web缓存交付给最终用户，以便更快地交付。 因此，当用户首次下载网页时，他们看到的资产会交付到CDN缓存。 它们存储在服务器上，这样当同一区域中的某人下次访问网页时，就可以更快地交付相同的缓存内容。 内容的交付速度更快，因为它位于更靠近最终用户的位置。 CDN可加快网页显示速度，但却降低了中央服务器的带宽需求，因为内容是从缓存网络（而不是从每个实例的中央服务器）交付的。 此优化流程意味着更好的用户体验，从而增加销售。

<!-- USE AN IMAGE HERE? ![Content delivery network](/help/assets/assets-dm/cdn.png) -->

过去，CDN每月为客户提供3.5 PB的流量。 该系统一天可交付520亿个资产。 这一数量相当于向客户成功交付了864,000张图像和视频， _每秒_.

### 智能成像

Dynamic Media已经非常出色地优化了资产，并通过CDN确保每个资产在移动和桌面系统上快速加载。 为了实现此目的，图像预设会用在Dynamic Media中来定义图像质量。 它们还可定义您要发送的图像类型、图像的清晰度以及体验或页面不同部分的其他图像片段。

但是，要进一步为Dynamic Media增加图像预设以外的价值，还有 _智能成像_.

“智能成像”功能可根据客户的浏览器功能自动优化图像的格式和文件大小，从而提供更好的图像资产交付性能。 它可与您现有的图像预设配合使用（此历程的第II部分对图像预设进行了讨论），并且在交付时会使用智能。

这种智能根据浏览器和网络连接速度进一步减小图像文件大小。 由于图像资产占页面加载时间的大部分，因此性能改进可能会对关键业务指标产生全面影响，例如：

* 更高的转化率
* 网站逗留时间
* 较低的网站跳出率

总体而言，使用智能成像，您可以根据现有图像预设设置和特定最终用户特征，获得22%到47%的性能提升。 同时保持像从未接触过一样的图像质量。

![智能成像](/help/assets/dynamic-media/assets/dm-smart-imaging.png)
_智能成像可根据客户的浏览器功能和网络速度自动优化图像的格式和文件大小。_

默认情况下，智能成像未打开，因为它需要您与AdobeDynamic Media技术支持人员进行协作。 此外，启用智能成像需要完全清除CDN缓存，然后重新填充该缓存。 如果您有兴趣使用智能成像，则可以与Adobe合作，通过提交技术支持票证来启用它。 然后，技术支持会为您提供一个URL参数，以便您提前尝试进行智能成像。 您可以在任何网页或图像上尝试使用该功能，以便查看您获得的性能以及节省的成本。 然后，您可以为整个网站打开智能成像。

### 自适应视频集

当页面或主页上有视频时，客户倾向于延长与该内容的交互时间，并在页面上停留更长的时间，这通常是件好事。 此行为已通过Adobe完成的分析进行展示。 但是，视频可能非常复杂。 首先，您通常拥有一个较大的主文件。 确定视频大小和传送方式非常复杂，所有这些操作都可确保体验平稳运行，而无论其正在观看的设备，也无论带宽如何。

为了解决此问题，Dynamic Media允许您创建 _自适应视频集_.

![自适应视频集](/help/assets/dynamic-media/assets/dm-smart-imaging.png)
_自适应视频集按不同的比特率和格式对同一视频的版本进行编码。_

首先从您上传到系统的原始主视频开始。 Dynamic Media会自动调整大小，或 _转码_，将该视频放入多个视频中。 然后，在交付时，它会智能地确定要使用的视频屏幕、质量和格式，并将其交付到手机、平板电脑或台式计算机。

例如，在 iOS 移动设备上，设备检测到 4G、5G 或 Wi-Fi 等带宽。设备会随之自动从自适应视频集内的各种视频比特率中选择正确的编码视频。视频会流式传输到移动设备、平板电脑或台式计算机。

此外，如果网络条件发生变化，视频质量会自动进行动态切换。 此外，如果客户在桌面上进入全屏模式，自适应视频集将使用更好的分辨率做出响应，从而改善客户的观看体验。

使用自适应视频集可为在多个屏幕和设备上播放Dynamic Media视频的客户提供流畅、高质量的播放。 它真正消除了视频的复杂性。

## Dynamic Media用例 {#dm-journey-b}

以下是常见的用例问题和解决方案，Dynamic Media可以帮助您提高客户积极参与度、忠诚度、转化率和更高的ROI。

### 用例：主文件方法

Dynamic Media最重要的用例之一也是最明显的用例之一。 也就是说，可以减轻页面和体验的重量，以及正在交付的内容大小，无论是图像还是视频。

下面显示了典型的体验或网页。 一个页面大约90%由富媒体构成，例如图像和视频，这些媒体通常是较重的文件。

![内容页面权重](/help/assets/dynamic-media/assets/dm-content-page-weight.png)
_典型网页的内容页面权重。_

其余10%为HTML、CSS代码和特定标记。 您希望优化该页面的90%重量，而Dynamic Media可帮助您完成这项工作。 以前，您阅读了 _一个主资产文件，无尽可能_. 此方法对于减少页面总体权重非常重要。 能够获取一个主资产并将其用在产品详细信息页面、缩略图页面、购物车和搜索网格上，这是一个极好的时间节省器。 同时，它还确保了不同体验之间的一致性。

![主文件方法](/help/assets/dynamic-media/assets/dm-onefile.png)
_Watch是一个主资产文件，但会随手创建多个演绎版（而非副本）。_

让我们来更详细地了解Dynamic Media通过一个文件以及该方法的一些解决方案正在解决的问题。

| **带有 OS 剪贴板** | **Dynamic Media解决方案** |
|---|---|
| 创建并存储每个资产。 | 使用单个图像文件，仅在交付时自动创建所需的演绎版。 |
| 存储成本高。 | 无需创建和存储资产的多个副本。 |
| 难以维持监管链。 | 确保提供设备优化且一致的体验。 |
| 没有版本历史记录。 |  |
| 跨设备的品牌体验不一致。 |  |
| 创建重复资产的不必要成本。 |  |

考虑一个文件时，您会为各种体验创建一个资产。 您可能有一个起始映像，然后您必须创建该映像的20个、30个或40个变体，您最终必须存储这些变体并为该存储付费。

然后，您必须确保使用了正确的图像，这可能会影响您在各个品牌之间保持一致的能力。 此外，如果您找不到图像，则必须返回并复制这些资产。

Dynamic Media允许您从该起始图像动态创建各种图像。 它让您能够使用该主要资产发挥创意，并且无需与图形设计艺术家或照片工作室来回切换，即可创建其他内容。 这是省下的钱和时间。

使用单个文件方法时，可使用单个主文件。 然后，创建您的网站、属性和体验中所需的版本或演绎版，只是在客户交付或查看这些版本或体验时才创建。 这样的效率可以大大降低资产所需的存储量，并降低整个工作流的复杂性。 借助Dynamic Media的投放系统，它可确保优化每个图像和视频，并快速加载，并在所有屏幕和设备上都呈现出完美的外观。

### 用例：视频

Dynamic Media解决的另一个用例是视频。 视频很复杂。 这很难管理。 由于视频文件的固有文件大小，因此存储和移动视频文件非常困难。

| **带有 OS 剪贴板** | **Dynamic Media解决方案** |
|---|---|
| 难以管理和提供针对各种设备优化的视频。 | 使用一个可自动调整所有设备大小的视频。 |
| 由于最终用户的可用带宽，视频在低质量下停止播放或播放。 | 通过HTML播放器传送视频，该播放器可自动检测可用带宽并调整质量，以确保高保真度和流畅播放。 |
| 手动创建视频的所有版本是不可行且耗时的，这只是为了确保跨设备的良好显示和播放。 | 通过简化的工作流，消除了耗时的繁琐转码工作。 |
|  | 腾出时间做价值更高的工作。 |

客户来到Dynamic Media时，会遇到以下他们希望解决的问题：

&quot;_我们拿了视频，花了很多钱制作它。 但是我们避免将它放在页面上，或者传送它，因为通过我们的测试，我们无法保证视频的质量，或者它是否真的要播放。 最终，这会影响我们的品牌，甚至会影响我们在转化中的作用。_&quot;

Dynamic Media的解决方案是获取一个主视频文件，并让Dynamic Media通过其转码过程制作所有大小。 然后，将其与Dynamic Media的智能视频播放器配对。 此工作流可确保无论您是在主登录页面上，还是在类别或产品详细信息页面上使用该视频，都能在整个过程中保持一致，并以高质量交付该视频。

还有几个用例需要考虑。

### 用例：单一真相来源

| **带有 OS 剪贴板** | **Dynamic Media解决方案** |
|---|---|
| 分散在整个组织中的数字资产，分散在不同的团队或业务单位中。 | 在中心位置存储和管理所有数字资产。 |
| 团队成员下载并创建本地版本。 | 团队成员使用单个主文件创建 _和_ 跨各种屏幕大小和设备提供所有必需版本。 |
| 为每个体验和设备创建的一次性资产。 | 消除了单次使用的资产，从而节省了创建这些资产的时间和资金。 |

### 用例：AI支持的富媒体智能裁剪

| **带有 OS 剪贴板** | **Dynamic Media解决方案** |
|---|---|
| 手动绘制、测量和剪切图像或视频，以突出焦点并在所有屏幕大小和设备上正确显示，既费时又费力。 | 使用Adobe Sensei AI中的Dynamic Media智能裁切功能，自动检测任何图像或视频中的焦点，然后进行裁切以对其进行维护。 |
| 所浪费的时间可以更好地用于创建具有影响力的体验。 | 捕获预期的目标点，而不考虑屏幕大小。 |
| 为每个体验和设备创建的一次性资产。 | 消除了繁琐的手动任务，并提供了高质量、快速加载的图像和视频，在任何设备或屏幕上都非常美观。 |

### 用例：交互式媒体创作

| **带有 OS 剪贴板** | **Dynamic Media解决方案** |
|---|---|
| 不参与、不产生忠诚度或不推动转化的扁平化和静态客户体验。 | 使非技术用户能够轻松、无缝地添加交互式元素，如热点、轮播和旋转集，以获得更动态、更吸引人的体验。 |
| 数字资产的投资回报有限，客户体验平平。 | 推动富媒体体验的转化和投资回报。 |

## 资产如何通过Dynamic Media系统 {#dm-journey-c}

以下显示了Dynamic Media的典型工作流。

![Dynamic Media工作流](/help/assets/dynamic-media/assets/dm-workflow.png)
_资产如何通过Dynamic Media系统流动。_

您从创建阶段开始，主要目标是将主资产放在最后。 这些主要资产可能来自照片拍摄，来自视频供应商，也可能是您创建的一些音频文件。 您可以使用Adobe的Creative Suite应用程序(如Adobe InDesign、Adobe Photoshop、Adobe Illustrator)来帮助您编写内容。

创建部分完成后，您可以通过将资产上传到Dynamic Media，将资产放入创作解决方案。 在Dynamic Media中，您应确保拥有正确的图像预设，并且查看器已排列到您网站上各个网页的对齐位置。

最终，您会优化所有内容并将其发布到Dynamic Media服务器，以便该内容可用于Web、打印、电子邮件、桌面和移动设备。

### 将资产上传到Dynamic Media

创建完主资产后，您会将其上传到Dynamic Media。 您上传的文件类型以及文件的格式和大小是Dynamic Media的重要属性。 在上传时，您需要确保从一个文件支持中获取最大值。

例如，下面的监视图像为4560 x 3020像素。 虽然您可能永远不会使用这种大小的图像，但您仍可以上传它。 图像越大，Dynamic Media可交付的质量就越好，甚至可以交付到缩略图呈现版本。 请记住：您可以轻松 _减少_ 现有图像的分辨率。 但如果你试着 _增加_ 图像的分辨率，结果可能不令人满意。

![要上传到Dynamic Media的建议格式](/help/assets/dynamic-media/assets/dm-upload-formats.png)
_有关资产上传的注意事项。_

Adobe建议您以无损格式上传资产。 通常，最好避免JPEG，因为当您提供JPEG或继续保存JPEG时，随着时间的推移，图像质量会开始下降。 您希望以可以忍受的无损格式从高分辨率图像开始。 该格式通常为TIFF或PNG文件。

关于色彩空间，当您考虑数字渠道或Web视图时，通常会考虑RGB（红色、绿色、蓝色）。

大多数人永远不会考虑以CMYK传送某些内容，或者您甚至可能想以CMYK传送的原因。 原因是色彩空间最常用于传送打印项目。 但是，Dynamic Media可以在两个色彩空间中传递。

还有很多仍在印刷的顾客，如仓库批发俱乐部。 还有一些杂货店经常每周打印传单。 此类客户要求其图像同时位于两个色彩空间中。 传统上，这需要两种不同的图像：一个RGB，一个CMYK。 但是，您可以直接将CMYK资产上传到Dynamic Media，并让Dynamic Media通过图像预设或颜色配置文件自动传送RGB资产。 无需创建文件的多个版本，因此可以维护 _一个主资产文件，无尽可能_.

<!-- **The Value of Renditioning??? or Demo portion** -->

### 发布和预览资产

将资产上传到Dynamic Media后，最佳做法是 _发布_ 通过选择资产，然后单击 **[!UICONTROL 发布]** 或 **[!UICONTROL 快速发布]** 在Dynamic Media。 如果您打算在任何体验中使用资产，则必须发布资产。 发布资产后，您便可以使用这些资产，通过您复制的Dynamic Media生成的URL或在页面上嵌入代码的方式，将其包含在网页中。

除了手动发布资产之外，您还可以配置Dynamic Media，以便在上传时立即发布资产（无需任何用户干预）。

上传后，在Dynamic Media中预览资产演绎版的方法有所不同。 预览演绎版可帮助您了解客户会看到的内容。 一种常见的预览方法是选择资产，然后通过选择 *图像预设* 如下所示。

![基于大图像预设预览资产的演绎版](/help/assets/dynamic-media/assets/dm-image-preset-with-url.png)
_根据选定的“大”图像预设预览资产的演绎版。 单击了URL按钮。 生成的URL路径包含“大”图像预设名称，并可在网页中使用。_

上述URL是实时的！ [试试看](http://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_28563982?$Large$).

预览资产的另一种方法是，选择图像资产，然后选择 *查看器* 预设，如下所示。

![基于缩放垂直光查看器预设预览资产](/help/assets/dynamic-media/assets/dm-viewer-preset.png)
_根据所选的“ZoomVertical_light”查看器预设预览资产。 鼠标指针(`+`)被移到手表上以放大。 请注意URL和嵌入按钮。_

上面的演绎版是实时的！ [试试看](https://s7d1.scene7.com/s7viewers/html5/ZoomVerticalViewer.html?asset=jpearldemo/AdobeStock_28563982&amp;config=jpearldemo/ZoomVertical_light).

让我们更仔细地检查这些URL，以便您更好地了解当前的情况。 带我去 [Dynamic Media历程:基础知识，第二部分](/help/assets/dynamic-media/dm-journey-part2.md#dm-journey-d).

## 了解更多

_Dynamic Media主题_

* [使用 Dynamic Media](/help/assets/dynamic-media/dynamic-media.md)
* [智能成像](/help/assets/dynamic-media/imaging-faq.md)
* [自适应视频集](/help/assets/dynamic-media/video.md)
* [优化图像质量的最佳实践](/help/assets/dynamic-media/best-practices-for-optimizing-the-quality-of-your-images.md)
* [上传资源](/help/assets/add-assets.md#upload-assets)
* [预览资源](/help/assets/dynamic-media/previewing-assets.md)
* [预览 3D 资源](/help/assets/dynamic-media/previewing-3d-assets.md)
* [交付Dynamic Media资产](/help/assets/dynamic-media/delivering-dynamic-media-assets.md)
* [发布资产](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)
* [使用 Dynamic Media 中的“选择性发布”功能](/help/assets/dynamic-media/selective-publishing.md)

_Dynamic Media教程_

* [将Dynamic Media与Experience Manager Assets结合使用](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-overview-feature-video-use.html)
* [Adobe Experience Manager内容库](https://experienceleague.adobe.com/?lang=en#recommended/solutions/experience-manager) (搜索 *Dynamic Media*)

_Dynamic Media查看器_

* [实时演示](https://landing.adobe.com/zh-Hans/na/dynamic-media/ctir-2755/live-demos.html)