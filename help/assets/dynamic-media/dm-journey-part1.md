---
title: Dynamic Media历程，第一部分
description: Dynamic Media历程介绍了Dynamic Media的基础知识、其工作方式、可为您提供的功能以及它给您的工作和客户带来的价值。
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
source-git-commit: 8ed477ec0c54bb0913562b9581e699c0bdc973ec
workflow-type: tm+mt
source-wordcount: '3706'
ht-degree: 1%

---

# Dynamic Media历程：基础知识，第I部分 {#dm-journey-part1}

欢迎使用Dynamic Media历程。

此历程涵盖Dynamic Media的基础知识、其工作方式、可为您提供的功能以及它给您的工作和客户带来的价值。

**_前提条件_**

* 对图像和视频格式的基本了解
* 对HTML和CSS的基本了解
* 基本了解Adobe Illustrator、Adobe Photoshop、Adobe XD等设计工具
* 在Experience Manager时访问Dynamic Media会很有帮助，但不是必需的

**_期待您了解的内容_**

_第一部分_

* Dynamic Media是什么以及它如何帮助您？
* Dynamic Media的用例
* 资产如何在Dynamic Media系统中流动

_第二部分_

* Dynamic Media URL剖析，以及Dynamic Media如何交付内容
* 创建图像预设以渲染资产的基础知识
* 图像集、旋转集和混合媒体集

**_受众_**
以下受众最适合此历程的读者，他们是Dynamic Media的Experience Manager新手：

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
>为获得最佳结果，Adobe建议您在台式计算机上阅读并查看此Dynamic Media历程。

## Dynamic Media是什么以及它如何帮助您？ {#dm-journey-a}

Dynamic Media可帮助您按需提供丰富的可视化推销和营销资源。 它还帮助您创建并提供交互式查看体验，包括缩放、360度旋转和视频。 您的资产会动态缩放以用于Web、移动和社交网站。 使用一组主要源资产（如图像、视频和3D ），Dynamic Media通过其可伸缩且性能优化的全局CDN（内容交付网络）实时生成并交付此丰富内容的多种变体。

Dynamic Media整合了Adobe Experience Manager Assets数字资产管理解决方案的工作流，以简化和简化数字营销活动管理流程。

### 一个具有无限可能性的文件

关于Dynamic Media，要了解的要点之一是的概念 _一个具有无限可能性的主要资源文件_.

要更好地理解此概念，请思考您传统上处理单个资产（如图像或视频）的方式。 通常创建一个主资源。 然后，为每个体验、所需的每个设备、每个网页以及使用资产的每个资产手动创建该资产的版本。 随着时间的推移，该单个资产可能会增长到20个、30个或更多版本，并且不会附加任何版本历史记录。 现在，想象一下，对每一个您拥有的图像或视频都这样做。 资产版本的数量将很快变得难以维护和更新，更不用说存储成本的增加了。

但是，Dynamic Media与其他系统存在根本性差异，因为您使用它来交付媒体 _动态_ 来自单个主资产和URL调用。 您请求的Dynamic Media URL路径中包含一些说明，告知Adobe发布服务器在将资源交付到客户屏幕时如何显示资源。 例如，使用相同的单个主资产，您可以让资产以无限演绎版的形式即时交付，并可以更改大小、格式、分辨率、粗细、颜色、裁切和缩放视图等效果。

这种独特的投放方法可确保向任何屏幕发送一致的质量体验，而不管屏幕的大小或带宽如何。 全尺寸视频也针对所有屏幕类型进行了优化，并自适应流式传输，以确保获得一致、高质量的用户体验。

<!-- As part of building and publishing assets with Dynamic Media, you visually configure the effects that you want to apply to assets. In so doing, you are literally building the URL that correctly tells the publish server how to deliver your primary asset to the screen.  -->

![AdobeDynamic Media可将相同的主图像提供给大小和格式不同的介质](/help/assets/dynamic-media/assets/dm-oneasset-multioutput.png)
_AdobeDynamic Media可确保向任何屏幕提供一致、优质的体验，而不管其大小或带宽如何。_

随着您继续阅读，您将了解更多有关“一个主要资源文件，无限可能性”的概念为什么重要的原因。

### 内容交付网络

当您准备好使用图像资源或视频资源时，Dynamic Media的骨干网络将支持该资源，该骨干网络由功能强大的顶级交付网络组成。 该网络每天为全世界数百个客户提供服务。 资产在由Akamai托管的内容交付网络（或CDN）上分发。 CDN是一种计算机服务系统，它们以透明方式连接在一起，共同向最终用户交付内容，特别是大型富媒体内容。

在CDN系统中，Web内容通过Internet存储在Web缓存中。 然后，它从Web Cache交付给最终用户，以实现更快的交付。 因此，首次下载网页时，用户会将其看到的资产传送到CDN缓存。 它们存储在服务器上，以便下次同一区域中的某人访问网页时，可以更快地交付相同的缓存内容。 因为离用户更近，所以内容交付速度更快。 CDN使得网页显示速度更快，但它降低了对中央服务器的带宽需求，因为内容是从缓存网络交付的，而不是从每个实例中的中央服务器交付的。 这一优化的流程意味着更好的用户体验，从而带来更高的销售额。

<!-- USE AN IMAGE HERE? ![Content delivery network](/help/assets/assets-dm/cdn.png) -->

过去，CDN每月会向客户提供3.5 PB的流量。 该系统一天可以提供520亿项资产。 这一数字相当于成功向客户发送了864,000个图像和视频， _每秒_.

### 智能成像

Dynamic Media在优化资源以及通过CDN确保每个资源在移动和桌面系统上快速加载方面已经功不可没。 要实现这一点，Dynamic Media中使用图像预设来定义图像的质量。 它们还定义了您要发送的图像类型、其锐化程度以及您的体验或页面各个部分的其他部分。

但是，为了进一步让Dynamic Media在图像预设之外增加价值，我们提供了 _智能成像_.

智能图像可根据客户的浏览器功能自动优化图像的格式和文件大小，从而提供更好的图像资产交付性能。 它可与您现有的图像预设（此历程的第二部分中将讨论图像预设）配合使用，并在投放时使用智能。

这种智能根据浏览器和网络连接速度进一步减小图像文件大小。 由于图像资产构成了页面加载时间的大部分，因此性能改进可能会对关键业务指标产生彻底的影响，例如：

* 较高的转化率
* 网站逗留时间
* 较低的网站跳出率

总体而言，对于智能成像，根据现有图像预设设置和特定最终用户特性，性能可望提高22%到47%。 同时保持图像质量，就像它从未被触摸过一样。

![智能成像](/help/assets/dynamic-media/assets/dm-smart-imaging.png)
_智能成像可根据客户的浏览器功能和网络速度自动优化图像的格式和文件大小。_

默认情况下，不会打开智能成像，因为您需要与AdobeDynamic Media技术支持协调工作。 此外，启用智能成像需要完全清除CDN缓存，然后使用时间重新填充。 如果您有兴趣使用智能成像，可以与Adobe合作，通过提交技术支持票证来启用它。 然后，技术支持会为您提供一个URL参数，以便您预先尝试智能成像。 您可以在您的任何网页或图像上尝试它，以便查看您获得的性能以及节省的成本。 然后，您可以为整个网站打开智能成像。

### 自适应视频集

当页面上存在视频或主页时，客户往往会更长时间地关注该内容并在页面上停留较长时间，这通常是好事。 Adobe所做的分析已经展示了这种行为。 但是，视频可能很复杂。 首先，您通常有一个大型主文件。 确定视频的大小和交付方式非常复杂，而所有这些都是为了确保体验能够顺利运行，而不管观看的是什么设备，也不管带宽如何。

要解决此问题，Dynamic Media让您能够创建 _自适应视频集_.

![自适应视频集](/help/assets/dynamic-media/assets/dm-smart-imaging.png)
_自适应视频集对以不同比特率和格式编码的相同视频的版本进行分组。_

首先从您上传到系统中的原始主视频开始。 Dynamic Media会自动调整大小，或者 _转码_，将该视频转换为多个视频。 然后，在交付时，它会智能地确定要使用哪种视频屏幕、哪种质量和哪种格式，并将其交付到手机、平板电脑或台式计算机。

例如，在iOS移动设备上，它会检测4G、5G或Wi-Fi等带宽。 然后，它自动从自适应视频集内的各种视频比特率中选择正确的编码视频。 视频将流式传输到移动设备、平板电脑或台式计算机。

此外，如果网络状况改变，视频质量会自动进行动态切换。 此外，如果客户在桌面上进入全屏模式，则自适应视频集将使用更好的分辨率进行响应，从而改善客户的观看体验。

使用自适应视频集，客户可以在多个屏幕和设备上播放Dynamic Media视频，从而流畅、高质量地回放视频。 它真正地消除了视频的复杂性。

## Dynamic Media的用例 {#dm-journey-b}

以下是Dynamic Media可以帮助您提高客户参与度、忠诚度、转化率和ROI的常见用例问题和解决方案。

### 用例：主要文件方法

Dynamic Media最重要的用例之一也是最明显的用例之一。 也就是说，要降低所交付的页面和体验的重量以及内容的大小（无论是图像还是视频）。

下面显示了典型的体验或网页。 一个页面中约有90%由富媒体（如图像和视频）组成，这些通常是比这重得多的文件。

![内容页面权重](/help/assets/dynamic-media/assets/dm-content-page-weight.png)
_典型网页的内容页面权重。_

其余10%是HTML、CSS代码和特定标记。 您希望优化该页面的90%权重，Dynamic Media会帮助完成该工作。 之前，您阅读了关于 _一个具有无限可能性的主要资源文件_. 此方法对于降低页面总体权重具有重要意义。 能够获取一项主要资产并将其用于产品详细信息页面、缩略图页面、购物车和搜索网格，是一种非常节省时间的方法。 它还可确保跨体验的一致性。

![主要文件方法](/help/assets/dynamic-media/assets/dm-onefile.png)
_监视文件是一个主要资源文件，但会动态创建其多个演绎版（而非副本）。_

让我们更仔细地看一下Dynamic Media通过单个文件解决的问题，以及这种方法的一些解决方案。

| **问题** | **Dynamic Media解决方案** |
|---|---|
| 创建并存储每个资产。 | 使用单个图像文件，仅在投放时自动创建所需的演绎版。 |
| 存储成本高。 | 无需创建和存储资产的多个副本。 |
| 难以维护监管链。 | 确保交付设备优化且一致的体验。 |
| 无版本历史记录。 | |
| 跨设备的品牌体验不一致。 | |
| 重复资产创建的不必要成本。 | |

当您想到某个文件时，您正在为各种体验创建资产。 您可能有一个起始映像，然后您必须创建该映像的20、30或40个变体，最终您需要存储这些变体并为其付费。

然后，您必须确保使用正确的映像，这可能会影响您保持品牌一致性的能力。 如果找不到图像，则必须返回并复制这些资源。

Dynamic Media允许您动态地从该起始图像创建图像的变体。 它使您能够使用该主要资产进行创意，而不必与图形设计艺术家或照片工作室反复沟通以创建其他内容。 这能节省金钱和时间。

使用单个文件方法时，使用单个主文件。 然后，仅在客户交付或看到这些版本或呈现时，创建您的网站、资产和体验中所需的版本或呈现版本。 这样的效率可以大大减少资产所需的存储量，并降低总体工作流的复杂性。 借助Dynamic Media的交付系统，它可以确保优化每个图像和视频，快速加载，并在所有屏幕和设备上呈现出卓越的外观。

### 用例：视频

Dynamic Media为解决的另一个用例是视频。 视频很复杂。 它很难管理。 视频文件由于其固有的文件大小而难以存储和移动。

| **问题** | **Dynamic Media解决方案** |
|---|---|
| 难以管理和投放针对各种设备优化的视频。 | 使用可自动调整所有设备大小的单个视频。 |
| 由于用户的可用带宽，视频会以低质量停止播放或回放。 | 通过可自动检测可用带宽并调整质量的HTML播放器交付视频，以确保高保真和平滑的播放。 |
| 手动创建视频的所有版本以确保跨设备良好显示和回放非常耗时而且不可行。 | 通过简化的工作流，消除繁琐的代码转换工作。 |
| | 腾出时间从事价值更高的工作。 |

来到Dynamic Media的客户会遇到以下他们希望解决的问题：

&quot;_我们有视频，我们花了很多钱来制作它。 但是我们避免把它放在网页上，或者传送它，因为从我们的测试来看，我们无法保证视频的质量，或者它是否真的要播放。 最终，这将影响我们的品牌，并影响我们实现甚至转化的潜在角色。_&quot;

Dynamic Media的解决方案是采用一个主视频文件，让Dynamic Media通过转码过程生成所有大小。 然后，再将其与Dynamic Media的智能视频播放器配对。 此工作流程可确保您在主登录页面、类别或产品详细信息页面上使用该视频，并且始终保持一致和高质量交付。

下面是需要考虑的更多用例。

### 用例：单一的真实来源

| **问题** | **Dynamic Media解决方案** |
|---|---|
| 数字资产分散在组织内，孤立在不同的团队或业务部门中。 | 在一个中心位置存储和管理所有数字资产。 |
| 团队成员下载并创建本地版本。 | 团队成员使用单个主文件来创建 _和_ 跨各种屏幕大小和设备提供所有必要的版本。 |
| 为每个体验和设备创建的一次性资产。 | 消除一次性资产，节省创建这些资产的时间和金钱。 |

### 用例：AI支持的用于富媒体的智能裁剪

| **问题** | **Dynamic Media解决方案** |
|---|---|
| 手动绘制、测量和剪切图像或视频以突出显示焦点并在所有屏幕大小和设备上正确显示非常耗时且耗费大量人力。 | 使用Adobe Sensei AI功能Dynamic Media中的智能裁剪自动检测任何图像或视频中的焦点，并裁剪以维护该焦点。 |
| 浪费的时间可以更好地用于创造高影响力的体验。 | 捕获预期目标点，而不管屏幕大小如何。 |
| 为每个体验和设备创建的一次性资产。 | 消除繁琐的手动任务，并提供在任何设备或屏幕上看起来都良好的高质量、快速加载的图像和视频。 |

### 用例：交互式媒体创作

| **问题** | **Dynamic Media解决方案** |
|---|---|
| 平面和静态的客户体验，不会引起客户兴趣、不会带来忠诚度或不会推动转化。 | 使非技术用户能够轻松无缝地添加交互元素，例如热点、轮播和旋转集，以获得更动态、更吸引人的体验。 |
| 数字资产的投资回报有限，客户体验乏善可陈。 | 推动转化并从富媒体体验中获得投资回报。 |

## 资产如何在Dynamic Media系统中流动 {#dm-journey-c}

下面显示了Dynamic Media的典型工作流程。

![Dynamic Media工作流程](/help/assets/dynamic-media/assets/dm-workflow.png)
_资产如何在Dynamic Media系统中流动。_

您从创建阶段开始，主要目标是最终创建主资产。 这些主要资产可能来自照片拍摄或视频供应商，也可能是由您创建的一些音频文件。 您可以使用Adobe的Creative Suite应用程序(如Adobe InDesign、Adobe Photoshop、Adobe Illustrator)帮助您制作内容。

创建部分完成后，您可以通过将资源上传到Dynamic Media，将资源放入创作解决方案。 在Dynamic Media中，您可以确保为网站上的各种网页设置正确的图像预设和查看器。

最终，您可以优化所有这些内容并将其发布到Dynamic Media服务器，以便将其用于Web、打印、电子邮件、桌面和移动设备。

### 将资源上传到Dynamic Media

创建完主资源后，可将其上传到Dynamic Media。 上传的文件类型以及文件的格式和大小是Dynamic Media的重要属性。 在上传时，您希望确保获得一个文件支持的最大值。

例如，下面的手表图像为4560 x 3020像素。 虽然您绝不能使用如此大小的图像，但您仍可以上传该图像。 图像越大，Dynamic Media提供的质量就越好，甚至可以向下扩展到缩略图演绎版。 记住：您可以轻松地 _减少_ 现有图像的分辨率。 但如果你试图 _增加_ 图像的分辨率，结果可能会令人不满意。

![上传到Dynamic Media的推荐格式](/help/assets/dynamic-media/assets/dm-upload-formats.png)
_资源上传的注意事项。_

Adobe建议您以无损格式上传资源。 通常，最好避免JPEG，因为当您交付JPEG或继续保存JPEG时，随着时间的推移，您会开始失去图像质量。 您希望以无损格式开始显示最高分辨率的图像，以便您随时使用。 该格式通常为TIFF或PNG文件。

关于色彩空间，当您考虑数字渠道或Web视图时，您通常会考虑RGB（红色、绿色、蓝色）。

大多数用户都不会考虑使用CMYK交付某些内容，甚至不会考虑您为何希望使用CMYK交付内容。 原因在于，该色彩空间最常用于交付打印项目。 但是，Dynamic Media可以在两个色彩空间中进行交付。

还有许多客户仍在从事印刷业务，如仓库批发俱乐部。 还有杂货店，它们经常每周打印传单。 此类客户要求他们的图像位于两个颜色空间中。 传统上，这需要两个不同的图像：一个是RGB图像，一个是CMYK图像。 但是，您可以将CMYK资源直接上传到Dynamic Media，并让Dynamic Media通过图像预设或色彩配置文件自动交付RGB资源。 无需创建文件的多个版本，因此保留了 _一个具有无限可能性的主要资源文件_.

<!-- **The Value of Renditioning??? or Demo portion** -->

### 发布和预览资源

将资源上传到Dynamic Media后，最佳做法是执行以下操作 _发布_ 选择资产，然后单击 **[!UICONTROL Publish]** 或 **[!UICONTROL 快速发布]** 在Dynamic Media中。 如果您打算在任何体验中使用资产，则必须发布资产。 发布资源后，您可以使用复制的由Dynamic Media生成的URL将资源包含在网页中，或者通过在页面上嵌入代码的方式将这些资源包含在网页中。

除了手动发布资产之外，您还可以配置Dynamic Media，以便在上传时即时发布资产，而无需任何用户干预。

上传后，可通过多种方式在Dynamic Media中预览资源的演绎版。 预览呈现版本可帮助您了解客户看到的内容。 一种常见的预览方法是选择资源，然后通过选择 _图像预设_ 如下所示。

![预览基于大型图像预设的资产演绎版](/help/assets/dynamic-media/assets/dm-image-preset-with-url.png)
_预览基于所选“大”图像预设的资产演绎版。 已单击URL按钮。 生成的URL路径包含“大”图像预设名称，可在网页中使用。_

上述URL是实时的！ [试试看](http://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_28563982?$Large$){target="_blank"}.

另一种预览资源的方法是选择图像资源，然后选择 _查看器_ 预设，如下所示。

![基于缩放垂直光源查看器预设预览资源](/help/assets/dynamic-media/assets/dm-viewer-preset.png)
_根据选定的“ZoomVertical_light”查看器预设预览资源。 鼠标指针(`+`)移到手表上以放大。 请注意URL和嵌入按钮。_

以上演绎版是实时的！ [试试看](https://s7d1.scene7.com/s7viewers/html5/ZoomVerticalViewer.html?asset=jpearldemo/AdobeStock_28563982&amp;config=jpearldemo/ZoomVertical_light){target="_blank"}.

## 可选 — 了解详情

此历程的第一部分介绍了各种Dynamic Media主题的基础知识。 如果您想详细了解刚刚阅读的内容，请使用以下材料更详细地探索概念。 否则，您可以继续历程的第二部分。 请参阅 [此Dynamic Media历程的后续内容](#whats-next).

_Dynamic Media帮助主题_

* [在Experience Manager中使用Dynamic Media](/help/assets/dynamic-media/dynamic-media.md)
* [关于智能成像](/help/assets/dynamic-media/imaging-faq.md)
* [如何创建自适应视频集](/help/assets/dynamic-media/video.md)
* [优化图像质量的最佳实践](/help/assets/dynamic-media/best-practices-for-optimizing-the-quality-of-your-images.md)
* [如何上传资源](/help/assets/add-assets.md#upload-assets)
* [如何预览资源](/help/assets/dynamic-media/previewing-assets.md)
* [如何预览三维资源](/help/assets/dynamic-media/previewing-3d-assets.md)
* [如何交付Dynamic Media资产](/help/assets/dynamic-media/delivering-dynamic-media-assets.md)
* [如何发布资源](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)
* [使用 Dynamic Media 中的“选择性发布”功能](/help/assets/dynamic-media/selective-publishing.md)

_Dynamic Media教程_

* [将Dynamic Media与Experience Manager Assets一起使用](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-overview-feature-video-use.html)
* [Adobe Experience Manager内容库](https://experienceleague.adobe.com/?lang=en#recommended/solutions/experience-manager) (搜索 _Dynamic Media_)

_Dynamic Media查看器_

* [实时演示](https://landing.adobe.com/zh-Hans/na/dynamic-media/ctir-2755/live-demos.html) 每个查看者

## 此Dynamic Media历程的后续内容 {#whats-next}

在此历程的第二部分中，您更近地检查了Dynamic Media URL，以更好地了解交付资产时发生了什么情况。 您还将了解有关创建图像预设以呈现资产的基础知识的更多信息，并了解图像集、旋转集和混合媒体集及其创建方式。

带我到 [Dynamic Media历程：基础知识，第二部分](/help/assets/dynamic-media/dm-journey-part2.md#dm-journey-d).

<!-- Live as of April 28 2022. LEAVE IN HERE https://landing.adobe.com/en/na/dynamic-media/ctir-2755/index.html -->