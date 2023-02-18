---
title: 管理查看器预设
description: 了解如何在Dynamic Media中创建和管理查看器预设。
contentOwner: Rick Brough
feature: Viewer Presets,Viewers
role: User
exl-id: da2e1a10-f54b-440e-b70c-f04ad4caeac1
source-git-commit: b35455652bd16b6c56c0bd75ee87acfb50473f1c
workflow-type: tm+mt
source-wordcount: '4369'
ht-degree: 15%

---

# 管理查看器预设{#managing-viewer-presets}

查看器预设是一组设置，用于确定用户在其计算机屏幕和移动设备上查看富媒体资产的方式。如果您是管理员，则可以创建查看器预设。设置适用于查看器配置选项数组。例如，您可以更改查看器的显示大小或缩放行为。

<!-- OBSOLETE SDK withdrawn from public view. Available internally only at `http://staging.scene7.com/s7sdk/3.8/docs/jsdoc/symbols/_s7sdk.html` 

For instructions on creating and customizing your own HTML5 viewer presets, see the *Adobe Scene7 HTML5 Viewer SDK*. The SDK is available on the IS publish server embedded in the SDK itself. Each library version has its own SDK documentation included.

Path: `<scene7_domain>/s7sdk/<library_version>/docs/jsdocs/index.html`.
For example, 3.5 SDK: [https://s7d1.scene7.com/s7sdk/3.5/docs/jsdoc/index.html](https://s7d1.scene7.com/s7sdk/3.5/docs/jsdoc/index.html)

-->

另请参阅 [Dynamic Media查看器参考指南](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html).

本节介绍如何创建、编辑和管理查看器预设。 无论您何时预览资产，都可以将查看器预设应用到资产。 请参阅 [应用查看器预设](#applying-a-viewer-preset-to-an-asset).

>[!NOTE]
>
>编辑任意 *预定义的现成查看器预设* 不支持此方案。 如果您尝试编辑现成的查看器预设，系统会提示您使用新名称保存查看器预设。

## 查看器的键盘辅助功能 {#keyboard-accessibility-for-viewers}

所有现成的查看器都支持键盘辅助功能。

另请参阅 [键盘辅助功能和导航](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility.html).

## 管理查看器预设 {#managing-viewer-presets-1}

您可以通过导航到以下位置，在Adobe Experience Manager中添加、编辑、删除、发布、取消发布和预览查看器预设 **[!UICONTROL 工具]** （锤子图标）> **[!UICONTROL 资产] > [!UICONTROL 查看器预设]**.

![6_5_tools-assets-viewerpresets](assets/6_5_tools-assets-viewerpresets.png)

>[!NOTE]
>
>默认情况下，当您在资产的详细信息视图中选择查看器时，系统会显示15个查看器预设。 您可以提高此限制。请参阅 [增加显示的查看器预设数](#increasing-the-number-of-viewer-presets-that-display).

### 查看器支持响应式设计的网页 {#viewer-support-for-responsive-designed-web-pages}

不同的网页有不同的需求。 例如，有时您希望网页提供一个链接，以在单独的浏览器窗口中打开HTML5查看器。 在其他情况下，需要直接将HTML5查看器嵌入到托管页面。 在后一种情况下，网页具有静态布局。 或者，它是“响应式”的，并在不同设备上或针对不同浏览器窗口大小显示不同。 为了满足这些需求，Dynamic Media附带的所有预定义开箱即用的HTML5查看器都支持静态网页和响应式设计的网页。

请参阅 [响应式静态图像库](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/responsive-static-image-library/c-about-responsive-static-image-library.html#about-responsive-image-library) 在 *Dynamic Media图像提供和渲染API帮助* 有关如何将响应式查看器嵌入网页的更多信息。

>[!NOTE]
>
>在首次使用开箱即用的查看器之前，先发布所有开箱即用的查看器。
>请参阅 [发布查看器预设](#publishing-viewer-presets).

### 查看器预设系统兼容性  {#viewer-preset-system-compatibility}

Dynamic Media附带的所有现成查看器预设都与以下系统完全兼容：

* 台式机
* AppleiPhone
* AppleiPad
* Android™智能手机
* Android™平板电脑

<!-- OUTDATED 2/25/22 * For video, extra support for MP4 playback is provided for [BlackBerry&reg;](https://developer.blackberry.com/devzone/develop/supported_media/bb_media_support_at_a_glance.html#kba1328730952678) and [Windows&reg; Phone](https://docs.microsoft.com/en-us/windows/uwp/audio-video-camera/supported-codecs). -->

### 查看器预设的富媒体类型 {#rich-media-types-for-viewer-presets}

管理员在创建查看器预设时，可以添加和自定义以下富媒体类型。

<table>
 <tbody>
  <tr>
   <td><strong>轮播集</strong><br /> </td>
   <td><p>热点或图像映射，或两者都添加到两个或更多图像的系列中。 客户可以向左或向右平移图像，然后在图像上选择热点以获取更多详细信息，或直接从网站的登陆、类别或主页进行购买。</p> </td>
  </tr>
    <tr>
   <td><strong>尺寸</strong><br /> </td>
   <td><p>显示可让您转动、平移、缩放或重新进入相机的3D场景。</p> </td>
  </tr>
  <tr>
   <td><strong>弹出缩放</strong></td>
   <td><p>在原始图像旁边显示缩放区域的副本图像。没有可用的控件 - 用户在要查看的区域上方移动选择。</p> <p>在决定此查看器的整体带宽使用率时，请考虑到主图像和弹出图像都在查看器中呈现。主图像的大小（暂存宽度和暂存高度）和缩放因子决定弹出图像的大小。为避免弹出图像过大，请平衡这两个值：如果主图像较大，请减小缩放因子的值。（弹出宽度和弹出高度决定弹出窗口的大小，但它们不决定在查看器中呈现的弹出图像的大小。）</p> <p>例如，如果主图像的大小是 350 X 350 像素，缩放因子为 3，则生成的弹出图像的大小就是 1050 X 1050 像素。如果主图像的大小是 300 X 300 像素，缩放因子为 4，则弹出图像的大小就是 1200 X 1200 像素。根据 JPEG 质量设置（建议的设置在 80 到 90 之间），您可以显著减小文件的大小。建议的缩放因子为 2.5 到 4，具体视主图像的大小而定。</p> </td>
  </tr>
  <tr>
   <td><strong>内联缩放</strong></td>
   <td>在原始查看器中显示缩放区域的图像。 没有可使用的控件。 也就是说，用户会在要查看的区域上移动所做的选择。</td>
  </tr>
  <tr>
   <td><strong>图像集</strong></td>
   <td>在图像集查看器中，用户可以通过选择缩略图来查看项目的不同视图或颜色变化。 此查看器还提供了用于仔细检查图像的缩放工具。</td>
  </tr>
  <tr>
   <td><strong>交互式图像</strong></td>
   <td>热点会添加到图像的某些部分，客户随后可以选择这些部分以获取更多详细信息，或直接从网站的登陆、类别或主页购买。</td>
  </tr>
  <tr>
   <td><strong>交互式视频</strong></td>
   <td>缩略图会添加到视频中的时间轴区段，客户随后可以选择该区段以获取更多详细信息，或直接从网站的登陆、类别或主页购买。</td>
  </tr>
  <tr>
   <td><strong>混合媒体</strong></td>
   <td>在一个查看器中显示不同类型的媒体。您可以包含旋转集、图像集、图像和视频。</td>
  </tr>
  <tr>
   <td><strong>全景图像</strong></td>
   <td><p>全景图像和全景VR查看器可渲染球面全景图像，以让用户沉浸在房间、属性、位置或景观的360°观看体验中。</p> <p>要使上传的图像符合球面全景图的条件，该图像必须具有以下任一项或两项：</p>
    <ul>
     <li>宽高比为2:1。</li>
     <li>使用关键词标记 <code>equirectangular</code>或 <code>spherical</code> 和 <code>panorama</code>或 <code>spherical </code>和 <code>panoramic</code>. 请参阅 <a href="/help/sites-cloud/authoring/features/tags.md">使用标记</a>.</li>
    </ul> <p>纵横比和关键字条件都适用于资产详细信息页面和“全景媒体”WCM组件的全景资产。</p></td>
  </tr>
    <tr>
   <td><strong>智能裁剪视频</strong><br /> </td>
   <td><p>使用此查看器可自动检测任何视频中的焦点并将其裁剪到该焦点。</p> </td>
  </tr>
  <tr>
   <td><strong>旋转集</strong></td>
   <td>提供图像的不同视图，以便用户可以旋转对象来从不同的侧边和角度进行检查。</td>
  </tr>
  <tr>
   <td><strong>360视频</strong></td>
   <td><p>使用360/VR视频查看器可渲染等长形视频，以体验房间、属性、位置、景观或医疗程序的沉浸式观看体验。</p> <p>在平面显示器上播放期间，用户可以控制观看角度。 移动设备上的播放使用其内置的陀螺仪控件。</p> <p>查看器包含对交付360个视频资产的本机支持。 默认情况下，查看或播放不需要任何其他配置。 您使用标准视频扩展名(如.mp4、.mkv和.mov)来交付360视频。 最常见的编解码器是H.264。</p> </td>
  </tr>
  <tr>
   <td><strong>视频</strong></td>
   <td><p>使用渐进式比特率流或自适应比特率流播放视频。 自适应比特率流自动执行设备和带宽检测，以正确的格式提供正确质量的视频。</p> </td>
  </tr>
  <tr>
   <td><strong>垂直缩放</strong></td>
   <td><p>通过垂直缩放查看器，您可以最大化产品图像查看体验，从而让用户更好地呈现产品。 色板的垂直位置可执行以下操作：</p>
    <ul>
     <li>确保色板“位于折页上方”。<br/> 使用水平色板，根据用户的桌面屏幕大小，在用户向下滚动页面之前，不会显示色板。 通过将色板垂直放置在查看器中，可确保无论用户的屏幕大小如何，都可以看到这些色板。</li>
     <li>最大化主图像大小。<br /> 使用水平色板时，必须保留页面上的空间，以确保它们可见。 此定位缩小了主图像的大小。 但是，使用垂直色板布局时，您无需分配此空间。 因此，您可以最大化主图像大小。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>缩放</strong></td>
   <td>允许用户通过选择区域来放大该区域。 用户可以选择用于放大、缩小图像以及将图像重置为默认大小的控件。</td>
  </tr>
 </tbody>
</table>

### 现成查看器预设列表 {#list-of-out-of-the-box-viewer-presets}

下表标识了Dynamic Media附带的所有预定义现成查看器预设。

另请参阅 [实时演示](https://landing.adobe.com/zh-Hans/na/dynamic-media/ctir-2755/live-demos.html).

有关查看器支持的Web浏览器和操作系统版本的信息，您可以查看查看器发行说明。

请参阅 [查看器参考指南](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html).

>[!NOTE]
>
>Dynamic Media中所有现成的查看器预设都已激活（开启），但您必须发布它们。
>请参阅 [发布查看器预设](#publishing-viewer-presets).
>
>您创建和添加的任何新查看器预设都必须同时激活*和*已发布。
>请参阅 [激活或取消激活查看器预设](#activating-or-deactivating-viewer-presets) 和 [发布查看器预设](#publishing-viewer-presets).

<table>
 <tbody>
  <tr>
   <td><strong>查看器预设标题</strong></td>
   <td><strong>类型</strong></td>
   <td><strong>CSS 文件名称</strong><br /> </td>
  </tr>
  <tr>
   <td>轮播_点线_深色</td>
   <td>轮播(_S)</td>
   <td><code>html5_carouselviewer_dotted_dark.css</code></td>
  </tr>
  <tr>
   <td>轮播_虚线_光</td>
   <td>轮播(_S)</td>
   <td><code>html5_carouselviewer_dotted_light.css</code></td>
  </tr>
  <tr>
   <td>轮播_数值_深色</td>
   <td>轮播(_S)</td>
   <td><code>html5_carouselviewer_numeric_dark.css</code></td>
  </tr>
  <tr>
   <td>轮播_数值_光</td>
   <td>轮播(_S)</td>
   <td><code>html5_carouselviewer_numeric_light.css</code></td>
  </tr>
  <tr>
   <td>弹出</td>
   <td>Flyout_Zoom</td>
   <td><code>html5_flyoutviewer.css</code></td>
  </tr>
  <tr>
   <td>ImageSet_dark</td>
   <td>图像集</td>
   <td><code>html5_zoomviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>ImageSet_light</td>
   <td>图像集</td>
   <td><code>html5_zoomviewer_light.css</code></td>
  </tr>
  <tr>
   <td>InlineMixedMedia_dark</td>
   <td>混合媒体</td>
   <td><code>html5_inlinemixedmediaviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>InlineMixedMedia_light</td>
   <td>混合媒体</td>
   <td><code>html5_inlinemixedmediaviewer_light.css</code></td>
  </tr>
  <tr>
   <td>InlineZoom</td>
   <td>Flyout_Zoom</td>
   <td><code>html5_inlinezoomviewer.css</code></td>
  </tr>
  <tr>
   <td>MixedMedia_dark</td>
   <td>混合媒体</td>
   <td><code>html5_mixedmediaviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>MixedMedia_light</td>
   <td>混合媒体</td>
   <td><code>html5_mixedmediaviewer_light.css</code></td>
  </tr>
  <tr>
   <td>全景图像</td>
   <td>全景图像(_I)</td>
   <td><code>html5_panoramicimage.css</code></td>
  </tr>
  <tr>
   <td>全景图像VR</td>
   <td>全景图像(_I)</td>
   <td><code>html5_panoramicimage.css</code></td>
  </tr>
  <tr>
   <td>Shoppable_Banner</td>
   <td>Interactive_Image</td>
   <td><code>html5_interactiveimage.css</code></td>
  </tr>
  <tr>
   <td>Shoppable_Video_dark</td>
   <td>Interactive_Video</td>
   <td><code>html5_interactivevideoviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>Shoppable_Video_light</td>
   <td>Interactive_Video</td>
   <td><code>html5_interactivevideovewer_light.css</code></td>
  </tr>
  <tr>
   <td>SpinSet_dark</td>
   <td>旋转集</td>
   <td><code>html5_spinviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>SpinSet_light</td>
   <td>旋转集</td>
   <td><code>html5_spinviewer_light.css</code></td>
  </tr>
  <tr>
   <td><p>视频</p> <p>（包括对隐藏式字幕的支持）</p> </td>
   <td>视频</td>
   <td><code>html5_videoviewer.css</code></td>
  </tr>
  <tr>
   <td><p>Video360_social</p> <p>（包括基本视频播放控件，视频渲染在立体模式下完成，手动视点控件关闭，但陀螺仪控件打开，且没有社交媒体功能）</p> </td>
   <td>Video_360</td>
   <td><code>html5_video360viewersocial.css</code></td>
  </tr>
  <tr>
   <td><p>Video360VR</p> <p>(专为使用虚拟现实眼镜的最终用户而设计。 包括基本视频播放控件和社交媒体功能)</p> </td>
   <td>Video_360</td>
   <td><code>html5_video360viewer.css</code></td>
  </tr>
  <tr>
   <td><p>Video_social</p> <p>（包括对隐藏式字幕和社交媒体的支持）</p> </td>
   <td>视频</td>
   <td><code>html5_videoviewersocial.css</code></td>
  </tr>
  <tr>
   <td>Zoom_dark<br /> </td>
   <td>缩放<br /> </td>
   <td><code>html5_basiczoomviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>Zoom_light<br /> </td>
   <td>缩放</td>
   <td><code>html5_basiczoomviewer_light.css</code></td>
  </tr>
  <tr>
   <td>ZoomVertical_dark<br /> </td>
   <td>垂直缩放</td>
   <td><code>html5_zoomverticalviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>ZoomVertical_light</td>
   <td>垂直缩放</td>
   <td><code>html5_zoomverticalviewer_light.css</code></td>
  </tr>
 </tbody>
</table>

### 支持的移动查看器手势矩阵 {#supported-mobile-viewers-gestures-matrix}

下表标识了iOS、Android™ 2.x和Android™ 3.x设备上支持的移动查看器手势。

<table>
 <tbody>
  <tr>
   <td><strong>手势</strong></td>
   <td><strong>弹出缩放</strong></td>
   <td><strong>缩放</strong></td>
   <td><strong>旋转</strong></td>
  </tr>
  <tr>
   <td><p><strong>拖动</strong></p> </td>
   <td><p>平移</p> </td>
   <td><p>平移</p> </td>
   <td><p>平移</p> </td>
  </tr>
  <tr>
   <td><p><strong>点按</strong></p> </td>
   <td><p>显示弹出窗口</p> </td>
   <td><p>显示或隐藏用户界面</p> </td>
   <td><p>显示或隐藏用户界面</p> </td>
  </tr>
  <tr>
   <td><p><strong>双击</strong></p> </td>
   <td><p>不适用</p> </td>
   <td><p>放大或重置</p> </td>
   <td><p>放大或重置</p> </td>
  </tr>
  <tr>
   <td><p><strong>捏开</strong></p> </td>
   <td><p>不适用</p> </td>
   <td><p>放大(仅限iOS和Android™ 3x)</p> </td>
   <td><p>放大(仅限iOS和Android™ 3x)</p> </td>
  </tr>
  <tr>
   <td><p><strong>捏合关闭</strong></p> </td>
   <td><p>不适用</p> </td>
   <td><p>缩小(仅限iOS和Android™ 3x)</p> </td>
   <td><p>缩小(仅限iOS和Android™ 3x)</p> </td>
  </tr>
  <tr>
   <td><p><strong>轻扫</strong></p> </td>
   <td><p>滚动色板条</p> </td>
   <td><p>滚动图像</p> </td>
   <td><p>旋转</p> </td>
  </tr>
  <tr>
   <td><p><strong>弗里克</strong></p> </td>
   <td><p>滚动色板条</p> </td>
   <td><p>滚动图像</p> </td>
   <td><p>旋转</p> </td>
  </tr>
 </tbody>
</table>

## 增加显示的查看器预设数 {#increasing-the-number-of-viewer-presets-that-display}

Experience Manager在从以下位置查看资产时，会显示各种查看器预设 **[!UICONTROL 详细信息视图]** > **[!UICONTROL 查看器]**. 您可以增加或减少显示的查看器数量。

**要增加显示的查看器预设数，请执行以下操作：**

1. 导航到CRXDE Lite([https://localhost:4502/crx/de](https://localhost:4502/crx/de))。
1. 导航到位于的查看器预设列表节点 `/libs/dam/gui/coral/content/commons/sidepanels/viewerpresets/viewerpresetslist`

   ![chlimage_1-221](/help/assets/dynamic-media/assets/chlimage_1-221.png)

1. 在 **[!UICONTROL limit]** 属性中，将默认设 **[!UICONTROL 置为15的Value]**（值）更改为所需的数字。
1. 导航到位于的查看器预设数据源 `/libs/dam/gui/coral/content/commons/sidepanels/viewerpresets/viewerpresetslist/datasource`

   ![chlimage_1-222](/help/assets/dynamic-media/assets/chlimage_1-222.png)

1. 在limit属性中，将数字更改为所需的数字，例如 `{empty requestPathInfo.selectors[1] ? "20" : requestPathInfo.selectors[1]}`
1. 选择 **[!UICONTROL 全部保存]**.

## 创建查看器预设 {#creating-a-new-viewer-preset}

通过创建查看器预设，您可以应用各种设置来查看资产并与之交互。 但是，您不需要创建查看器预设。 如果您愿意，可以使用Experience Manager Assets附带的默认现成查看器预设。

如果选择创建查看器预设，则在保存该查看器预设后，查看器的状态将自动激活(设置为 **[!UICONTROL 开]**)。 此状态表示无论您何时预览图像或视频，都可以在Dynamic Media组件和交互式媒体组件中看到该图像或视频。

某些查看器预设具有可影响查看器的使用和整体行为的排他设置。 根据您创建的查看器预设，您需要注意这些特殊注意事项。

请参阅 [创建交互式查看器预设的特殊注意事项](#special-considerations-for-creating-an-interactive-viewer-preset).

请参阅 [创建轮播横幅查看器预设的特殊注意事项](#special-considerations-for-creating-a-carousel-banner-viewer-preset).

**要创建查看器预设，请执行以下操作：**

1. 在Experience Manager的左上角，选择Experience Manager徽标，然后在左边栏中，转到 **[!UICONTROL 工具]** （锤子图标）> **[!UICONTROL 资产]** > **[!UICONTROL 查看器预设]**.

   ![6_5_viewerpresets](assets/6_5_viewerpresets.png)

1. 在“查看器预设”页面的工具栏中，选择 **[!UICONTROL 创建]**.
1. 在&#x200B;**[!UICONTROL 新查看器预设]**&#x200B;对话框的&#x200B;**[!UICONTROL 预设名称]**&#x200B;字段中，输入新预设的名称。请仔细选择名称 — 在您选择 **[!UICONTROL 创建]**.

   在稍后的这些步骤中保存预设时，“查看器预设”页面的“预设标题”列标题下会显示该名称。

1. 在富媒体类型下拉菜单中，选择要创建的查看器预设类型，然后在页面的右上角，选择 **[!UICONTROL 创建]**.

   请参阅[查看器预设的富媒体类型](#rich-media-types-for-viewer-presets)。

1. 在“查看器预设编辑器”页面上，选择 **[!UICONTROL 外观]** 选项卡。
1. 执行下列操作之一：

   * 在 **[!UICONTROL 选定类型]** 下拉菜单中，选择要自定义其可视设计的组件。 或者，您也可以选择查看器中的任何可视化元素，以选择进行配置。

      通过可视编辑器，您可以查看特定属性对样式有何影响。 设置或调整任何属性，以便使用编辑器左侧的示例即时查看该属性对查看器有何影响。

      每种类型的查看器预设的CSS样式属性在“自定义”中有介绍 *`<viewer name>`* 查看者”帮助主题 [查看器参考指南](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html). 例如，如果您创建的是类型的查看器预设 `Mixed_Media`，请参阅 [自定义混合媒体查看器](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/mixed-media/customing-mixed-media/c-html5-mixedmedia-viewer-customizingviewer.html) ，以获取每个属性的列表和描述。

   * 如果您在单独的CSS文件中定义了样式设置，则可以将CSS文件上传到Experience Manager Assets。 要查找上传的CSS文件并将其与查看器预设关联，请选择 **[!UICONTROL 导入CSS]** 下面 **[!UICONTROL 选定类型]** 下拉菜单（如有必要，向上滚动可视编辑器以查看）。

      导入CSS文件时，可视编辑器会检查CSS是否使用正确的查看器标记。 例如，如果要创建缩放查看器，则必须使用其查看器类名称定义导入的所有CSS规则 `.s7mixedmediaviewer` 在父查看器元素上定义。

      只要为给定查看器正确定义CSS标记，就可以导入任意手工CSS。 (CSS标记在任何“自定义” *&lt;viewer name=&quot;&quot;>* 查看者”帮助主题 [查看器参考指南](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html). 例如，如果要阅读有关缩放查看器的CSS标记，请参阅 [自定义缩放查看器](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/zoom/customizing-zoom/c-html5-20-zoom-viewer-customizingviewer.html).) 但是，可视编辑器可能不了解某些CSS值。 在这种情况下，可视编辑器会尝试覆盖错误，以便CSS仍然可以工作。
   >[!NOTE]
   >
   >如果您希望直接在其原始表单中编辑CSS，请选择 **[!UICONTROL 显示/隐藏CSS]** 在“选定类型”下拉菜单下（如有必要，向上滚动可视编辑器以查看）。
   >与可视编辑器一样，当您直接在CSS中更改属性时，您可以立即查看该属性对查看器示例有何影响。 而且，该同一属性会在可视化编辑器中同时自动更新。 因此，您可以使用原始CSS编辑器或可视编辑器，或者两者交替使用。

   >[!NOTE]
   >
   >对于按钮图稿，选择2x图像并上传高分辨率艺术品。 使用交互式图像和购物横幅时，您还可以从各种现成的热点按钮中进行选择。

1. （可选）在“编辑查看器预设”页面顶部附近，选择 **[!UICONTROL 桌面]**, **[!UICONTROL 平板电脑]**&#x200B;或 **[!UICONTROL 电话]** 用于为不同设备和屏幕类型唯一定义可视样式。
1. 在“查看器预设编辑器”页面上，选择 **[!UICONTROL 行为]** 选项卡。 或者，您也可以选择查看器中的任何可视化元素，以选择进行配置。
例如，对于 *VideoPlayer* 类型，下 **[!UICONTROL 修饰符]** > **[!UICONTROL 播放]**，您可以从以下三个自适应流选项之一进行选择：

   * **[!UICONTROL 短划线]**  — 视频以短划线形式流。
   * **[!UICONTROL hls]**  — 视频流仅作为hls。
   * **[!UICONTROL 自动]**  — 最佳实践。 DASH和HLS流的创建是存储优化的。 因此，Adobe建议您始终选择 **[!UICONTROL 自动]** 类型。 视频以短划线、hls或渐进方式流，如下所示：
      * 如果浏览器支持短划线，则首先使用短划线流。
      * 如果浏览器不支持短划线，则使用HLS流，其次是。
      * 如果浏览器不支持短划线或HLS，则最后使用渐进式播放。

   >[!NOTE]
   >
   >要查看和使用 **[!UICONTROL 短划线]** 选项，则必须首先由您帐户上的Adobe技术支持人员启用。 请参阅 [在您的帐户上启用短划线](/help/assets/dynamic-media/video.md#enable-dash).

1. 从&#x200B;**[!UICONTROL 选定类型]**&#x200B;下拉菜单中，选择要更改其行为的组件。

   可视化编辑器中的许多组件都有与其关联的详细说明。 当您展开组件以显示其关联参数时，这些描述会显示在蓝色框中。

   有些“查看器类型”具有的组件允许您在 **[!UICONTROL IS 命令]**&#x200B;文本字段中指定“图像提供”命令。有关可使用的命令列表，请参阅[图像提供 API 参考](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/c-is-home.html)。

   >[!NOTE]
   >
   >**如果您使用的是触控设备，如手机或平板电脑……**
   >
   >
   >在文本字段中键入值后，请在用户界面的其他位置选择以提交更改并关闭虚拟键盘。 如果您选择 **[!UICONTROL 输入]**，则不会执行任何操作。

1. 在页面的右上角附近，选择 **[!UICONTROL 保存]**.
1. 发布新查看器预设。 有必要发布预设，以便您能够在网站上使用其生成的URL。

   请参阅 [发布查看器预设](#publishing-viewer-presets).

   >[!IMPORTANT]
   >
   >对于使用自适应流播放用户档案的旧视频，URL会继续照常播放（与HLS流播放），直到您 [重新处理视频资产](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). 重新处理后，同一URL将继续工作，但现在与 *both* 已启用DASH和HLS流。

### 创建交互式查看器预设的特殊注意事项 {#special-considerations-for-creating-an-interactive-viewer-preset}

**关于面板中图像缩略图的显示模式：**

创建或编辑交互式视频查看器预设时，您可以选择要使用的显示模式设置。 当您选择 `InteractiveSwatches` 从 **[!UICONTROL 选定的组件]** 下方的下拉菜单 **[!UICONTROL 行为]** 选项卡。 您选择的显示模式会影响视频播放时缩略图的显示方式和显示时间。 您可以选择 `segment` 显示模式（默认）或 `continuous` 显示模式。

<table>
 <tbody>
  <tr>
   <td><strong>显示模式</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>市场细分</td>
   <td><p><code>Segment </code>是现成交互式视频查看器预设的默认显示模式 <code>Shoppable_Video_light</code> 和 <code>Shoppable_Video_dark</code> 以及您自己创建的任何交互式视频查看器预设。</p> <p>在此模式下，假定分配给视频区段的缩略图数量少于显示面板中的可见点数。 在这种情况下，下一个或上一个子区段的缩略图是 <i>not </i>拉进来填充面板中的任何空白位置。 即，它保留分配给特定视频区段的色板的显示。</p> </td>
  </tr>
  <tr>
   <td>连续</td>
   <td><p>在 <code>continuous </code>显示模式，假设区段中缩略图的数量小于面板中可见缩略图的数量。 在这种情况下，查看器会自动包含显示下一个区段或显示最后一个缩略图的上一个区段的缩略图。</p> <p>的 <a href="/help/assets/dynamic-media/interactive-videos.md">本主题中的视频</a> 是 <code>continuous </code>显示模式。</p> </td>
  </tr>
 </tbody>
</table>

**关于交互式视频查看器中的自动滚动行为：**

交互式视频查看器中缩略图的自动滚动行为与您选择的显示模式无关。

创建或编辑交互式视频查看器预设时，您可以从“行为”选项卡访问“自动滚动”。在“行为”选项卡中，从 **[!UICONTROL 选定的组件]** 下拉菜单，选择 **[!UICONTROL InteractiveSwatches]**. “自动滚动”复选框列在“IS 命令”文本字段的下方。

如果在查看器预设中禁用&#x200B;**[!UICONTROL 自动滚动]**（清除复选框），则在用户播放视频时，该面板仅显示整个视频长度的第一个缩略图。但是，如果需要，用户可以使用向上和向下箭头图标手动滚动缩略图。

在查看器预设中启用（选择）**[!UICONTROL 自动滚动]**&#x200B;后，在视频播放过程中，分配给视频区段的缩略图图像会在区段开始时滚动到视图中。但是，在某些情况下，区段内某些缩略图的显示时间是其之前或之后缩略图显示时间的两倍。发生此行为的原因是区段中缩略图的数量大于面板中可见缩略图的数量，且不可平均分割。

为了说明这一点，假设您有一个30秒的视频区段。 此外，30秒内共显示9个缩略图。 您的浏览器的大小调整为显示面板中有四个可见的缩略图位置。 30秒视频时间段分为三个子段。 下表显示了在给定时间子区段中显示哪些缩略图的划分：

| **视频子区段** | **子区段时间（以秒为单位）** | **面板中可见的缩略图** |
|---|---|---|
| 1 | 0-10 | 1，2，3，4 |
| 2 | 10-20 | 4，5，6，7 |
| 3 | 20-30 | 6，7，8，9 |

视频子区段3的扩展范围不超出分配给它的缩略图。 另请注意，缩略图 4、6 和 7 在面板中出现的时间是其他缩略图的两倍。

查看器根据可用位置数量在面板中显示缩略图数量的逻辑如下：

* 子区段数量=舍入到下一个子区段（缩略图数量/缩略图面板中的可见版块数量，具体取决于浏览器窗口大小）。
使用上表中的示例，9个缩略图/ 4个版块= 2.25;查看器逻辑会将其舍入为三个子区段。

* 缩略图数量=舍入到下一个缩略图（缩略图数量/视频子区段数量）。
使用上表中的示例，9个缩略图/ 3个视频子区段= 3个缩略图。

* 子区段的持续时间=视频总持续时间/视频子区段的数量。
使用上表中的示例， 30秒/ 3个视频子区段=每个视频子区段的10秒显示。

#### 创建轮播横幅查看器预设的特殊注意事项 {#special-considerations-for-creating-a-carousel-banner-viewer-preset}

创建轮播横幅查看器预设时，可以按如下方式访问更改热点样式：

|  | **描述** | **操作** |
|---|---|---|
| **[!UICONTROL 热点图标]** | 更改用于热点的图标 | 要更改热点图标图像，请在 **[!UICONTROL 外观]** 选项卡，在 **[!UICONTROL 选定的组件]**，选择 **[!UICONTROL ImageMapEffect]**. 在 **[!UICONTROL 图标]**，选择 **[!UICONTROL 背景]** 和 **[!UICONTROL 图像]** 字段，导航到所需的背景图像。 |

## 激活或停用查看器预设 {#activating-or-deactivating-viewer-presets}

用户界面中可用的查看器预设取决于哪些查看器预设在创作模式下处于活动状态。 默认情况下，查看器预设在创建后为“开启”。 如果关闭预设，则在“创作”模式下看不到该预设。 如果发布了预设，则无论是打开还是关闭预设，都会始终发布预设。 如果列表变得过于庞大或您不希望某个查看器预设可供使用，请停用查看器预设。

**要激活或停用查看器预设，请执行以下操作：**

1. 在Experience Manager的左上角，选择Experience Manager徽标，然后在左边栏中，选择 **[!UICONTROL 工具]** （锤子图标）> **[!UICONTROL 资产]** > **[!UICONTROL 查看器预设]**.
1. 在“查看器预设”页面的 **[!UICONTROL 州]** 列标题中，选择用于激活或停用查看器预设的切换开关。

   已激活的查看器预设在右侧蓝色框中显示切换开关；已停用的查看器预设的切换开关会显示在灰色浅框中的左侧。

## 发布查看器预设 {#publishing-viewer-presets}

激活（或打开“打开”）查看器预设的状态意味着该查看器预设在Dynamic Media组件、交互式媒体组件以及您查看资产时均可见。

但是， *交付* 对于具有查看器预设的资产，还必须发布查看器预设。 必须激活所有查看器预设 *和* 发布以获取资产的URL或嵌入代码。 激活并发布Dynamic Media附带的所有现成查看器预设。 您创建和添加的自定义查看器预设将自动激活，但也必须发布。

请参阅 [激活或取消激活查看器预设](#activating-or-deactivating-viewer-presets).

另请参阅[预览资产](/help/assets/dynamic-media/previewing-assets.md)。

**要发布查看器预设，请执行以下操作：**

1. 在Experience Manager的左上角，选择Experience Manager徽标，然后在左边栏中，选择 **[!UICONTROL 工具]** （锤子图标）> **[!UICONTROL 资产] > [!UICONTROL 查看器预设]**.
1. 选择要发布的一个或多个查看器预设。
1. 在工具栏中，选择 **[!UICONTROL 发布]** 图标。

## 对查看器预设进行排序 {#sorting-viewer-presets}

1. 在Experience Manager的左上角，选择Experience Manager徽标，然后在左边栏中，选择 **[!UICONTROL 工具]** （锤子图标）> **[!UICONTROL 资产] > [!UICONTROL 查看器预设]**.
1. 选择 **[!UICONTROL 预设标题]**, **[!UICONTROL 类型]**, **[!UICONTROL 已发布]**&#x200B;或 **[!UICONTROL 州]** 按列标题排序。 例如，选择 **[!UICONTROL 类型]**  按字母顺序或反向字母顺序对查看器预设类型进行排序。

## 编辑查看器预设 {#editing-viewer-presets}

编辑任意 *预定义的现成查看器预设* 不支持此方案。 如果您编辑现成的查看器预设，系统会提示您使用新名称保存该查看器预设。

**要编辑查看器预设，请执行以下操作：**

1. 在Experience Manager的左上角，选择Experience Manager徽标，然后在左边栏中，选择 **[!UICONTROL 工具]** （锤子图标）> **[!UICONTROL 资产]** > **[!UICONTROL 查看器预设]**.
1. 选中查看器预设标题左侧的框以选择预设。
1. 在工具栏中，选择 **[!UICONTROL 编辑]**.
1. 在 **[!UICONTROL 查看器预设编辑器]** ，可使用 **[!UICONTROL 外观]** 和 **[!UICONTROL 行为]** 选项卡。

   从 **[!UICONTROL 外观]** ，在“查看器预设编辑器”页面的左上角附近，选择 **[!UICONTROL 桌面]**, **[!UICONTROL 平板电脑]**&#x200B;或 **[!UICONTROL 电话]** 更改资产的显示模式。

1. 在页面的右上角附近，执行下列操作之一：

   * 选择 **[!UICONTROL 保存]** ，以保存所做的更改并返回到“查看器预设”页面。
   * 选择 **[!UICONTROL 取消]** 撤消您所做的任何更改并返回到“查看器预设”页面。

## 删除自定义查看器预设 {#deleting-custom-viewer-presets}

您可以删除已创建并添加到Dynamic Media的查看器预设。

**要删除自定义查看器预设，请执行以下操作：**

1. 在Experience Manager的左上角，选择Experience Manager徽标，然后在左边栏中，选择 **[!UICONTROL 工具]** （锤子图标）> **[!UICONTROL 资产] > [!UICONTROL 查看器预设]**.
1. 在“查看器预设”页面上，选中预设标题，然后选择 **[!UICONTROL 垃圾]** 图标。
1. 选择&#x200B;**[!UICONTROL 删除]**。

## 将查看器预设应用于资产 {#applying-a-viewer-preset-to-an-asset}

如果已发布资产和选定的查看器，则在选择查看器预设后 **[!UICONTROL 将显示]** “ **[!UICONTROL URL]** ”和“嵌入”按钮。

**要将查看器预设应用到资产，请执行以下操作：**

1. 打开资产，在页面的左上角附近，选择下拉菜单，然后选择 **[!UICONTROL 查看器]**.

   >[!NOTE]
   >
   >如果已发布资产和选定的查看器，则在选择查看器预设后 **[!UICONTROL 将显示]** “ **[!UICONTROL URL]** ”和“嵌入”按钮。

1. 要将其应用于资产，请从左窗格中选择查看器预设。

   您可以 [复制要共享的URL](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) 其他用户。

## 使用查看器预设传送资产 {#delivering-assets-with-viewer-presets}

要获取查看器预设的URL，请参阅 [将URL关联到您的Web应用程序](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md). 另请参阅 [在网页上嵌入视频查看器](/help/assets/dynamic-media/embed-code.md).

如果您使用Experience Manager作为WCM，则可以直接在页面上使用查看器预设添加资产。 请参阅 [将Dynamic Media Assets添加到页面](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).
