---
title: 将 Dynamic Media 资产添加到页面
description: 如何将Dynamic Media组件作为Cloud Service添加到Adobe Experience Manager的页面。
translation-type: tm+mt
source-git-commit: 3431f7f82b086c5c9aa0c2900332eae70728b147
workflow-type: tm+mt
source-wordcount: '3128'
ht-degree: 30%

---


# 将 Dynamic Media 资产添加到页面{#adding-dynamic-media-assets-to-pages}

要将Dynamic Media功能添加到您在网站上使用的资产中，您可以直接在页面上添加 **Dynamic Media**、 **Interactive Media**、 **Media**&#x200B;或 **** Video 360 Media全景组件。 为此，可进入布局模式并启用Dynamic Media组件。 然后，您可以将这些组件添加到页面，并将资产添加到该组件。 Dynamic media组件是智能的——它们知道您添加的是图像还是视频，可用的配置选项会相应地发生更改。

如果您使用Dynamic Media作为WCM，则可以直接将Experience Manager资源添加到页面。 如果您为 WCM 使用第三方，请[链接](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)或[嵌入](/help/assets/dynamic-media/embed-code.md)资产。有关响应式第三方网站，请参阅[将优化的图像交付到响应式网站](/help/assets/dynamic-media/responsive-site.md)。

>[!NOTE]
>
>您必须先发布资产，然后才能以Experience Manager将其添加到页面。 请参阅[发布Dynamic Media资产](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)。

## 将Dynamic Media组件添加到页面{#adding-a-dynamic-media-component-to-a-page}

向页面添加3D媒体、Dynamic Media、交互式媒体、全景媒体、智能裁剪视频或视频360媒体组件与向任何页面添加组件相同。 以下各节介绍了Dynamic Media各组成部分。

**向页面添加Dynamic Media组件**

1. 在Experience Manager中，打开要添加Dynamic Media组件的页面。
1. 在左窗格中，点按&#x200B;**[!UICONTROL 组件]**&#x200B;图标，然后过滤Dynamic Media。

   如果没有可用的列表Dynamic Media组件，您可能需要启用要使用的Dynamic Media组件。 请参阅[启用Dynamic Media组件](#enabling-dynamic-media-components)。

   ![6_5_360video_wcmcomponent](assets/6_5_360video_wcmcomponent.png)

1. 拖动&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;组件，将其放到页面上的所需位置。

1. 将鼠标指针直接悬停在组件上。 当组件被蓝色框包围时，点按一次以显示组件的工具栏。 点按&#x200B;**[!UICONTROL 配置（扳手）]**&#x200B;图标。

   ![6_5_360video_wcmcomponentconfigure](assets/6_5_360video_wcmcomponentconfigure.png)

1. 根据您放到页面上的Dynamic Media组件，将打开一个配置对话框。 [根据需要设置组](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#dynamic-media-components) 件选项。

   以下示例显示了“Dynamic Media视频360媒体&#x200B;]**”组件对话框以及“查看器预设”下拉列表中提供的选项。**[!UICONTROL 

   ![视频360媒体组件](assets/6_5_360video_wcmcomponentviewerpreset.png)

   Dynamic Media视频360媒体组件。

1. 完成后，在对话框的右上角，点按复选标记以保存更改。

### 启用Dynamic Media组件{#enabling-dynamic-media-components}

如果没有可添加到页面的Dynamic Media组件，则可能意味着您需要首先启用要使用的组件。

1. 在Experience Manager中，打开要添加Dynamic Media组件的页面。
1. 在工具栏左侧，点按页面顶部附近的页面信息图标，然后点按下拉列表中的&#x200B;**[!UICONTROL 编辑模板]**。

   ![edit-template](/help/assets/assets-dm/edit-template.png)

1. 在工具栏右侧页面顶部附近的下拉列表中，点按&#x200B;**[!UICONTROL 结构]**。

   ![策略](/help/assets/assets-dm/structure-mode.png)

1. 在页面底部附近，点按&#x200B;**[!UICONTROL 布局容器]**&#x200B;以打开其工具栏，然后点按策略图标。
1. 在&#x200B;**[!UICONTROL 布局容器]**&#x200B;页面的&#x200B;**[!UICONTROL 属性]**&#x200B;标题下，确保选中了&#x200B;**[!UICONTROL 允许的组件]**&#x200B;选项卡。

   ![允许的组件](/help/assets/assets-dm/allowed-components.png)

1. 滚动直到您看到&#x200B;**[!UICONTROL Dynamic Media]**。
1. 点按&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;左侧的>图标以展开列表，选择要启用的Dynamic Media组件。

   ![Dynamic Media部件列表](/help/assets/assets-dm/dm-components-select.png)

1. 在&#x200B;**[!UICONTROL 布局容器]**&#x200B;页面的右上角附近，点按完成（复选标记）图标。

1. 在工具栏右侧页面顶部附近的下拉列表中，点按&#x200B;**[!UICONTROL 初始内容]**，然后按[将Dynamic Media组件按常规方式添加到页面](#adding-a-dynamic-media-component-to-a-page)。

## 将Dynamic Media组件定位{#localizing-dynamic-media-components}

您可以通过以下两种方式之一本地化Dynamic Media组件：

* 在“站点”的网页中，打开“属 **[!UICONTROL 性]** ”，然后选择“ **[!UICONTROL 高级]** ”选项卡。 选择所需的本地化语言。

   ![chlimage_1-172](assets/chlimage_1-538.png)

* 从站点选择器中，选择所需的页面或页面组。 点按&#x200B;**[!UICONTROL 属性]**&#x200B;并选择&#x200B;**[!UICONTROL 高级]**&#x200B;选项卡。 选择所需的本地化语言。

   >[!NOTE]
   >
   >请注意，**[!UICONTROL 语言]**&#x200B;菜单中并非所有可用语言当前都分配了令牌。

## 可用的Dynamic Media组件{#dynamic-media-components}

当您点按&#x200B;**[!UICONTROL 组件]**&#x200B;图标，然后在&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;上进行筛选时，可使用Dynamic Media组件。

可用的Dynamic Media组件包括：

* **[!UICONTROL Dynamic Media]** - 用于图像、视频、电子目录和旋转集等资产。
* **[!UICONTROL 交互式媒体]** -用于任何交互式资产，如交互式视频、交互式图像或传送集。
* **[!UICONTROL 全景媒体]** -用于全景图像或全景VR图像资源。
* **[!UICONTROL 视频360媒体]** -用于360视频和360 VR视频资源。

>[!NOTE]
>
>这些组件默认不可用，在使用之前需要通过模板编辑器使用。 在模板编辑器中使用这些组件后，您可以像添加任何其他Experience Manager组件一样将这些组件添加到页面。

![6_5_dynamicmediawcmcomponents](assets/6_5_dynamicmediawcmcomponents.png)

### 组件：Dynamic Media{#dynamic-media-component}

Dynamic Media是聪明的。根据您添加的是图像还是视频，您有各种选项。 该组件支持图像预设、基于图像的查看器（例如图像集、旋转集、混合媒体集）和视频。此外，查看器是响应式的——屏幕大小会根据屏幕大小自动更改。 所有查看器都是 HTML5 查看器。

>[!NOTE]
>
>如果您的网页具有以下内容：
>
>* 在同一页面上使用的Dynamic Media组件的多个实例。
>* 每个实例都使用相同的资产类型。

>
>
请注意，不支持为该页面上的每个Dynamic Media组件分配不同的查看器预设。
>
>但是，您可以对页面中使用相同类型资产的所有Dynamic Media组件使用相同的查看器预设。

添加 Dynamic Media 组件时，如果 **[!UICONTROL Dynamic Media 设置]**&#x200B;为空或无法正常添加资产，请检查以下各项：

* 图像具有金字塔 TIFF 文件。在启用 Dynamic Media 之前导入的图像没有金字塔 TIFF 文件。

#### 处理图像时  {#when-working-with-images}

Dynamic Media 组件允许您添加动态图像，包括图像集、旋转集和混合媒体集。您可以缩放图像，并在适当的情况下在旋转集内旋转图像，或从其他类型的集合中选择图像。

您还可以直接在组件中配置查看器预设、图像预设或图像格式。要使图像成为响应式图像，您可以设置断点，或应用响应式图像预设。

通过点按组件中的&#x200B;**[!UICONTROL 编辑]**&#x200B;图标，然后&#x200B;**[!UICONTROL Dynamic Media设置]**，可以编辑以下Dynamic Media设置。

![dm-settings-image-preset](assets/dm-settings-image-preset.png)

>[!NOTE]
>
>默认情况下，Dynamic media图像组件是自适应的。 如果要使其变为固定大小，请在“高级”选项卡的组件中设置 **[!UICONTROL 它]** ，并使用“宽度”和“高 **** 度” ****。

* **[!UICONTROL 查看器预设]**-从下拉菜单中选择现有的查看器预设。如果未显示您要查找的查看器预设，则可能需要将其显示出来。请参阅管理查看器预设。如果您正在使用图像预设，则无法选择查看器预设，反之亦然。

   如果您查看的是图像集、旋转集或混合媒体集，这是唯一可用的选项。显示的查看器预设也是智能的 - 仅显示相关的查看器预设。

* **[!UICONTROL 查看器修饰符]**-查看器修饰符采用名称=值对和分隔符的形式，允许您根据《查看器参考指南》中的概述更改查看器。查看器修饰符的示例是`posterimage=img.jpg&caption=text.vtt,1`，它为视频缩略图设置不同的图像并将隐藏字幕／子标题文件与视频相关联。

* **[!UICONTROL 图像预设]**-从下拉菜单中选择现有的图像预设。如果未显示您要查找的图像预设，则可能需要将其显示出来。请参阅管理图像预设。如果您正在使用图像预设，则无法选择查看器预设，反之亦然。

   如果您查看的是图像集、旋转集或混合媒体集，则此选项不可用。

* **[!UICONTROL 图像修饰符]**-可以通过提供其他图像命令来应用图像效果。这些内容在图像预设和图像服务命令参考中进行了介绍。

   如果您查看的是图像集、旋转集或混合媒体集，则此选项不可用。

* **[!UICONTROL 断点]**-如果您在响应式站点上使用此资产，则需要添加图像断点。图像断点之间需要使用逗号 (,) 进行分隔。当图像预设中未定义高度或宽度时，可以使用此选项。

   如果您查看的是图像集、旋转集或混合媒体集，则此选项不可用。

   通过点按组件中的&#x200B;**[!UICONTROL 编辑]**，可以编辑以下高级设置。

* **[!UICONTROL 标题]**-更改图像的标题。

* **[!UICONTROL 替换文本]**-为关闭图形的用户添加图像标题。

   如果您查看的是图像集、旋转集或混合媒体集，则此选项不可用。

* **[!UICONTROL URL，打开位置]**-您可以设置资产以打开链接。设置 URL，并在打开方式中指示是要在同一窗口中还是在新窗口中打开该 URL。

   如果您查看的是图像集、旋转集或混合媒体集，则此选项不可用。

* **[!UICONTROL 宽度]**-如果希望图像具有固定大小，请输入以像素为单位的值。将此值留空可使资产具有自适应性。

* **[!UICONTROL 高度]**-如果希望图像具有固定大小，请以像素为单位输入值。将此值留空可使资产具有自适应性。


#### 处理视频时 {#when-working-with-video}

使用Dynamic Media组件将动态视频添加到网页。 编辑该组件时，您可以选择使用预定义的视频查看器预设，以在页面上播放视频。

![chlimage_1-173](assets/chlimage_1-540.png)

单击组件中的&#x200B;**[!UICONTROL 编辑]**&#x200B;可编辑以下Dynamic Media设置。

>[!NOTE]
>
>默认情况下，Dynamic Media 视频组件为自适应组件。如果要使其具有固定大小，请在组件中使用&#x200B;**[!UICONTROL 高级]**&#x200B;选项卡中的&#x200B;**[!UICONTROL 宽度]**&#x200B;和&#x200B;**[!UICONTROL 高度]**&#x200B;进行设置。

* **[!UICONTROL 查看器预设]**-从下拉菜单中选择现有的视频查看器预设。如果未显示您要查找的查看器预设，则可能需要将其显示出来。请参阅管理查看器预设。

* **[!UICONTROL 查看器修饰符]**-查看器修饰符采用名称=值对和分隔符的形式，允许您根据《Adobe查看器参考指南》中的概述更改查看器。查看器修饰符的示例为`posterimage=img.jpg&caption=text.vtt,1`

   例如，通过查看器修饰符，可以执行以下操作：

   * 将题注文件与视频关联：[题注](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-caption.html)
   * 将导航文件与视频关联：[navigation](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-navigation.html)

   单击组件中的&#x200B;**[!UICONTROL 编辑]**&#x200B;可编辑以下高级设置。

* **[!UICONTROL 标题]**-更改视频的标题。

* **[!UICONTROL 宽度]**-如果希望图像具有固定大小，请输入以像素为单位的值。将此值留空可使资产具有自适应性。

* **[!UICONTROL 高度]**-如果希望图像具有固定大小，请以像素为单位输入值。将此值留空可使资产具有自适应性。

#### 使用智能裁剪{#when-working-with-smart-crop}时

使用Dynamic Media组件将智能裁剪图像资产添加到您的网页。 编辑该组件时，您可以选择使用预定义的视频查看器预设，以在页面上播放视频。

请参阅[将智能裁剪与Experience Manager资产结合使用Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/smart-crop-feature-video-use.html#dynamic-media)

另请参阅[图像用户档案](/help/assets/dynamic-media/image-profiles.md)。

![dm-settings-smart-crop](assets/dm-settings-smart-crop.png)

单击组件中的&#x200B;**[!UICONTROL 编辑]**&#x200B;可编辑以下Dynamic Media设置。

>[!NOTE]
>
>默认情况下，Dynamic media图像组件是自适应的。 如果要使其变为固定大小，请在“高级”选项卡的组件中设置 **[!UICONTROL 它]** ，并使用“宽度”和“高 **** 度” ****。

* **[!UICONTROL 图像修饰符]**-可以通过提供其他图像命令来应用图像效果。这些内容在图像预设和图像服务命令参考中进行了介绍。

   如果您查看的是图像集、旋转集或混合媒体集，则此选项不可用。

   单击组件中的&#x200B;**[!UICONTROL 编辑]**&#x200B;可编辑以下高级设置。

* **[!UICONTROL 启用长宽比匹配]**-选择此选项可让Dynamic Media选择宽高比最匹配原始图像长宽比的智能裁剪再现。

* **[!UICONTROL 标题]**-更改智能裁剪图像的标题。

* **[!UICONTROL 替换文本]**-为关闭图形的用户添加智能裁剪图像的标题。

   如果您查看的是图像集、旋转集或混合媒体集，则此选项不可用。

* **[!UICONTROL URL，打开位置]**-您可以设置资产以打开链接。设置 URL，并在打开方式中指示是要在同一窗口中还是在新窗口中打开该 URL。

   如果您查看的是图像集、旋转集或混合媒体集，则此选项不可用。

* **[!UICONTROL 宽度]**-如果希望图像具有固定大小，请输入以像素为单位的值。将此值留空可使资产具有自适应性。

* **[!UICONTROL 高度]**-如果希望图像具有固定大小，请以像素为单位输入值。将此值留空可使资产具有自适应性。

### 组件：交互式媒体{#interactive-media-component}

交互式媒体组件适用于具有交互功能的资产，例如热点或图像映射。如果您具有交互式图像、交互式视频或传送横幅，请使用&#x200B;**[!UICONTROL 交互式媒体]**&#x200B;组件。

交互式媒体组件是智能的。根据您添加的是图像还是视频，您有各种选项。 此外，查看器是响应式的——屏幕大小会根据屏幕大小自动更改。 所有查看器都是 HTML5 查看器。

>[!NOTE]
>
>如果您的网页具有以下内容：
>
>* 在同一页面上使用的交互式媒体组件的多个实例。
>* 每个实例都使用相同的资产类型。

>
>
请注意，不支持为该页面上的每个交互式媒体组件分配不同的查看器预设。
>
>但是，您可以对页面中使用相同类型资产的所有交互式媒体组件使用相同的查看器预设。

![chlimage_1-174](assets/chlimage_1-541.png)

通过点按组件中的&#x200B;**[!UICONTROL 编辑]**，可以编辑以下&#x200B;**[!UICONTROL 常规]**&#x200B;设置。

* **[!UICONTROL 查看器预设]**-从下拉菜单中选择现有的查看器预设。如果未显示您要查找的查看器预设，则可能需要将其显示出来。查看器预设必须先发布，然后才能使用。请参阅管理查看器预设。

* **[!UICONTROL 标题]**-更改视频的标题。

* **[!UICONTROL 宽度]**-如果希望图像具有固定大小，请输入以像素为单位的值。将此值留空可使资产具有自适应性。

* **[!UICONTROL 高度]**-如果希望图像具有固定大小，请以像素为单位输入值。将此值留空可使资产具有自适应性。

   您可以通过在组件中单击&#x200B;**[!UICONTROL 编辑]**，来编辑以下&#x200B;**[!UICONTROL 添加到购物车]**&#x200B;设置。

* **[!UICONTROL 显示产品资产]**-默认情况下，此值处于选中状态。产品资产会按“商务”模块中的定义显示产品的图像。清除复选标记不会显示产品资产。

* **[!UICONTROL 显示产品价格]**-默认情况下，此值处于选中状态。产品价格会按“商务”模块中的定义显示项目的价格。清除复选标记不会显示产品价格。

* **[!UICONTROL 显示产品表单]**-默认情况下，此值未选中。产品表单包含所有产品变量，例如大小和颜色。清除复选标记不会显示产品变量。

### 组件：全景媒体{#panoramic-media-component}

全景媒体组件适用于那些球面全景图像的资源。 这些图像提供房间、房产、位置或风景的360°查看体验。 要使图像成为球面全景图，它必须具有以下任一或两项：

* 宽高比为2:1。
* 使用关键字`equirectangular`或(`spherical` + `panorama`)或(`spherical` + `panoramic`)进行标记。 请参阅[使用标记](/help/sites-cloud/authoring/features/tags.md)。

纵横比和关键字条件都适用于资产详细信息页面和&#x200B;**[!UICONTROL 全景媒体]** WCM 组件的全景资产。

>[!NOTE]
>
>如果您的网页具有以下内容：
>
>* 在同一页面上使用的&#x200B;**[!UICONTROL 全景媒体]**&#x200B;组件的多个实例。
>* 每个实例都使用相同的资产类型。

>
>
请注意，不支持为该页面上的每个&#x200B;**[!UICONTROL 全景媒体]**&#x200B;组件分配不同的查看器预设。
>
>但是，对于在页面中使用相同类型资产的所有全景媒体组件，您可以使用相同的查看器预设。

![panoramic-media-viewer-preset](assets/panoramic-media-viewer-preset.png)

通过点按组件中的&#x200B;**[!UICONTROL 配置]**，可以编辑以下设置。

* **[!UICONTROL 查看器预设]**-从查看器预设下拉菜单中选择现有的查看器。

如果未显示您要查找的查看器预设，请检查以确保其已发布。 您必须先发布查看器预设，然后才能使用它们。 请参阅[管理查看器预设](/help/assets/dynamic-media/managing-viewer-presets.md)。

### 组件：视频360介质{#video-media-component}

使用&#x200B;**[!UICONTROL 视频360媒体]**&#x200B;组件在您的网页上呈现等长形视频，让您沉浸在房间、财产、位置、风景或医疗过程的欣赏中。

在平面显示器上播放时，用户可以控制观看角度；在移动设备上播放通常利用其内置的陀螺仪控件。

查看器包含对360个视频资源投放的本机支持。 默认情况下，查看或回放不需要任何其他配置。 您可以使用标准视频扩展（如。mp4、.mkv和。mov）交付360视频。 最常见的编解码器是H.264。

![6_5_360video_wcmcomponent-1](assets/6_5_360video_wcmcomponent-1.png)

通过点按组件中的&#x200B;**[!UICONTROL 配置]**，可以编辑以下设置。

* **[!UICONTROL 查看器预设]**-从查看器预设下拉菜单中选择现有的查看器。将Video360VR用于使用虚拟现实眼镜的最终用户。 包括基本的视频播放控件和社交媒体功能。 使用Video360_social，它包含基本的视频播放控件。 视频渲染以立体模式完成。 手动视图点控制关闭，但陀螺仪控制打开。 没有社交媒体功能。

如果未显示您要查找的查看器预设，请检查以确保其已发布。 您必须先发布查看器预设，然后才能使用它们。 请参阅[管理查看器预设](/help/assets/dynamic-media/managing-viewer-presets.md)。

### 使用HTTP/2投放Dynamic Media资源{#using-http-to-delivery-dynamic-media-assets}

HTTP/2是新的、经过更新的Web协议，它改进了浏览器和服务器的通信方式。 它提供更快的信息传输，并减少所需的处理能力。 Dynamic Media资源的投放现在可以通过HTTP/2，从而提供更好的响应和加载时间。

有关使用Dynamic Media帐户HTTP/2入门的完整详细信息，请参阅[内容](/help/assets/dynamic-media/http2faq.md)的HTTP2投放。

>[!MORELIKETHIS]
>
>* [在Experience ManagerDynamic Media中使用视频播放器](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-video-player-feature-video-use.html#dynamic-media)
>* [与Experience ManagerDynamic Media一起使用交互式视频](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-interactive-video-feature-video-use.html#dynamic-media)
>* [通过Experience ManagerDynamic Media了解资产查看器](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-viewer-feature-video-understand.html#dynamic-media)
>* [将自定义视频缩略图与Experience ManagerDynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-video-thumbnails-feature-video-use.html#dynamic-media)
>* [使用Experience ManagerDynamic Media了解色彩管理](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-color-management-technical-video-setup.html#dynamic-media)
>* [使用图像锐化和Experience ManagerDynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-image-sharpening-feature-video-use.html#dynamic-media)

