---
title: 管理查看器预设
description: 了解如何在Dynamic Media中创建和管理查看器预设。
feature: 查看器预设，查看器
role: Business Practitioner
exl-id: da2e1a10-f54b-440e-b70c-f04ad4caeac1
source-git-commit: d3ee23917eba4a2e4ae1f2bd44f5476d2ff7dce1
workflow-type: tm+mt
source-wordcount: '4236'
ht-degree: 23%

---

# 管理查看器预设{#managing-viewer-presets}

查看器预设是一组设置，这些设置决定用户如何在其计算机屏幕和移动设备上视图富媒体资产。如果您是管理员，则可以创建查看器预设。可用于查看器配置选项的数组设置。例如，可更改查看器的显示大小或缩放行为。

<!-- OBSOLETE SDK withdrawn from public view. Available internally only at `http://staging.scene7.com/s7sdk/3.8/docs/jsdoc/symbols/_s7sdk.html` 

For instructions on creating and customizing your own HTML5 viewer presets, see the *Adobe Scene7 HTML5 Viewer SDK*. The SDK is available on the IS publish server embedded in the SDK itself. Each library version has its own SDK documentation included.

Path: `<scene7_domain>/s7sdk/<library_version>/docs/jsdocs/index.html`.
For example, 3.5 SDK: [https://s7d1.scene7.com/s7sdk/3.5/docs/jsdoc/index.html](https://s7d1.scene7.com/s7sdk/3.5/docs/jsdoc/index.html)

-->

另请参阅[《Dynamic Media查看器参考指南》](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html)。

本节介绍如何创建、编辑和管理查看器预设。 无论您何时对资产进行预览，您都可以将查看器预设应用到资产。 请参阅[应用查看器预设](#applying-a-viewer-preset-to-an-asset)。

>[!NOTE]
>
>不支持编辑任何预定义的现成查看器预设&#x200B;*。*&#x200B;如果您尝试编辑现成的查看器预设，系统会提示您使用新名称保存查看器预设。

## 查看器{#keyboard-accessibility-for-viewers}的键盘可访问性

所有现成查看器都支持键盘辅助功能。

另请参阅[键盘辅助功能和导航](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility.html)。

## 管理查看器预设 {#managing-viewer-presets-1}

您可以通过点按&#x200B;**[!UICONTROL 工具]**（锤子图标）>**[!UICONTROL 资产]>[!UICONTROL 查看器预设]**，在Adobe Experience Manager中添加、编辑、删除、发布、取消发布和预览查看器预设。

![6_5_tools-assets-viewerpresets](assets/6_5_tools-assets-viewerpresets.png)

>[!NOTE]
>
>默认情况下，当您在资产的详细信息视图中选择查看器时，系统会显示15个查看器预设。 您可以提高此限制。请参阅[增加显示的查看器预设数量](#increasing-the-number-of-viewer-presets-that-display)。

### 查看器支持响应式设计网页{#viewer-support-for-responsive-designed-web-pages}

不同的网页有不同的需求。 例如，有时您希望网页提供链接，在单独的浏览器窗口中打开HTML5查看器。 在其他情况下，必须将HTML5查看器直接嵌入到托管页面。 在后一种情况下，网页具有静态布局。 或者，它是“响应式”的，在不同设备上显示时或针对不同浏览器窗口大小显示时不同。 为满足这些需求，Dynamic Media附带的所有预定义、现成的HTML5查看器都支持静态网页和响应式设计网页。

有关如何将响应式查看器嵌入网页的详细信息，请参阅&#x200B;*Dynamic Media图像服务和渲染API帮助*&#x200B;中的[响应式静态图像库](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/responsive-static-image-library/c-about-responsive-static-image-library.html#about-responsive-image-library)。

>[!NOTE]
>
>在首次使用开箱即用的查看器之前，先发布这些查看器。
>请参阅[发布查看器预设](#publishing-viewer-presets)。

### 查看器预设系统兼容性{#viewer-preset-system-compatibility}

Dynamic Media附带的所有现成查看器预设都与以下系统完全兼容：

* 桌面
* Apple iPhone
* Apple iPad
* Android™智能手机
* Android™平板电脑
* 对于视频，为[BlackBerry®](https://developer.blackberry.com/devzone/develop/supported_media/bb_media_support_at_a_glance.html#kba1328730952678)和[Windows® Phone](https://msdn.microsoft.com/library/windows/apps/ff462087%28v=vs.105%29.aspx)提供了对MP4播放的额外支持。

### 查看器预设的富媒体类型{#rich-media-types-for-viewer-presets}

管理员可以在创建查看器预设时添加和自定义以下富媒体类型。

<table>
 <tbody>
  <tr>
   <td><strong>轮播集</strong><br /> </td>
   <td><p>热点或图像映射，或两者都添加到一系列两个或多个图像中。 客户可以向左或向右平移图像，然后单击图像上的热点以了解详细信息，或直接从网站的登录、类别或主页购买。</p> </td>
  </tr>
    <tr>
   <td><strong>尺寸</strong><br /> </td>
   <td><p>显示3D场景，您可以通过这些场景来旋转、平移、缩放或重新进入相机。</p> </td>
  </tr>
  <tr>
   <td><strong>弹出缩放</strong></td>
   <td><p>在原始图像旁边显示缩放区域的副本图像。没有可用的控件 - 用户在要查看的区域上方移动选择。</p> <p>在决定此查看器的整体带宽使用率时，请考虑到主图像和弹出图像都在查看器中呈现。主图像的大小（暂存宽度和暂存高度）和缩放因子决定弹出图像的大小。为避免弹出图像过大，请平衡这两个值：如果主图像较大，请减小缩放因子的值。（弹出宽度和弹出高度决定弹出窗口的大小，但它们不决定在查看器中呈现的弹出图像的大小。）</p> <p>例如，如果主图像的大小是 350 X 350 像素，缩放因子为 3，则生成的弹出图像的大小就是 1050 X 1050 像素。如果主图像的大小是 300 X 300 像素，缩放因子为 4，则弹出图像的大小就是 1200 X 1200 像素。根据 JPEG 质量设置（建议的设置在 80 到 90 之间），您可以显著减小文件的大小。建议的缩放因子为 2.5 到 4，具体视主图像的大小而定。</p> </td>
  </tr>
  <tr>
   <td><strong>内联缩放</strong></td>
   <td>在原始查看器中显示缩放区域的图像。 没有可使用的控件。 即，用户在要视图的区域上移动选区。</td>
  </tr>
  <tr>
   <td><strong>图像集</strong></td>
   <td>在“图像集”查看器中，用户可以通过单击缩略图，查看项目的不同视图或颜色变量。此查看器还提供了用于仔细检查图像的缩放工具。</td>
  </tr>
  <tr>
   <td><strong>交互式图像</strong></td>
   <td>热点会添加到图像的某些部分，然后客户可以单击这些部分以了解详细信息，或直接从网站的登录、类别或主页购买。</td>
  </tr>
  <tr>
   <td><strong>交互式视频</strong></td>
   <td>缩略图会添加到视频中的时间轴区段，然后客户可以单击该区段以了解详细信息，或直接从网站的登录、类别或主页购买。</td>
  </tr>
  <tr>
   <td><strong>混合媒体</strong></td>
   <td>在一个查看器中显示不同类型的媒体。您可以包含旋转集、图像集、图像和视频。</td>
  </tr>
  <tr>
   <td><strong>全景图像</strong></td>
   <td><p>全景图像和全景VR查看器渲染球面全景图像，让用户在360°的房间、财产、位置或风景的观看体验中沉浸于其中。</p> <p>要使上传的图像符合球面全景，它必须具有以下任一项或两项：</p>
    <ul>
     <li>宽高比为2:1。</li>
     <li>使用关键字<code>equirectangular</code>、<code>spherical</code>和<code>panorama</code>或<code>spherical </code>和<code>panoramic</code>标记。 请参阅<a href="/help/sites-cloud/authoring/features/tags.md">使用标记</a>。</li>
    </ul> <p>长宽比和关键字条件都适用于资产详细信息页面和“全景媒体”WCM组件的全景资产。</p></td>
  </tr>
    <tr>
   <td><strong>智能裁剪视频</strong><br /> </td>
   <td><p>使用此查看器可自动检测任何视频中的焦点并裁剪到焦点。</p> </td>
  </tr>
  <tr>
   <td><strong>旋转集</strong></td>
   <td>提供图像的不同视图，以便用户可以旋转对象来从不同的侧边和角度进行检查。</td>
  </tr>
  <tr>
   <td><strong>360视频</strong></td>
   <td><p>使用360/VR视频查看器渲染等长方形视频，实现房间、财产、位置、风景或医疗程序的沉浸式查看体验。</p> <p>在平面显示器上播放时，用户可控制视角。 在移动设备上播放时使用内置的陀螺仪控件。</p> <p>查看器包含对360个视频资源的投放的本机支持。 默认情况下，查看或回放不需要任何其他配置。 您可以使用标准视频扩展(如.mp4、.mkv和.mov)交付360视频。 最常见的编解码器是H.264。</p> </td>
  </tr>
  <tr>
   <td><strong>视频</strong></td>
   <td><p>使用渐进式或自适应比特率流播放视频。 自适应比特率流会自动执行设备和带宽检测，以正确的格式提供正确质量的视频。</p> </td>
  </tr>
  <tr>
   <td><strong>垂直缩放</strong></td>
   <td><p>利用垂直缩放查看器，您可以最大化产品图像的查看体验，为用户提供最佳的产品展示效果。 色板的垂直位置如下所示：</p>
    <ul>
     <li>确保色板“位于折页上方”。<br/> 使用水平色板时，色板在用户向下滚动页面之前不可见，具体取决于用户的桌面屏幕大小。通过将色板垂直放置在查看器中，可确保无论用户的屏幕大小如何，色板都可见。</li>
     <li>最大化主图像大小。<br /> 使用水平色板时，必须在页面上保留空间，以确保它们可见。此定位缩小了主图像的大小。 但是，对于垂直色板布局，您无需分配此空间。 因此，您可以最大化主图像大小。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>缩放</strong></td>
   <td>用户可以通过单击该选项来缩放区域。用户可以单击相应控件来放大图像、缩小图像以及将图像重置为默认大小。</td>
  </tr>
 </tbody>
</table>

### 列表开箱即用的查看器预设{#list-of-out-of-the-box-viewer-presets}

下表列出了Dynamic Media附带的所有预定义现成查看器预设。

另请参阅[实时演示](https://landing.adobe.com/zh-Hans/na/dynamic-media/ctir-2755/live-demos.html)。

有关查看器支持的Web浏览器和操作系统版本的信息，您可以查看查看器发行说明。

请参阅[《查看器参考指南》](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html)的目录中的“查看器发行说明”。

>[!NOTE]
>
>Dynamic Media中的所有现成查看器预设都已激活（开始），但您必须发布它们。
>请参阅[发布查看器预设](#publishing-viewer-presets)。
>
>您创建和添加的任何新查看器预设都必须同时激活*和*已发布。
>请参阅[激活或取消激活查看器预设](#activating-or-deactivating-viewer-presets)和[发布查看器预设](#publishing-viewer-presets)。

<table>
 <tbody>
  <tr>
   <td><strong>查看器预设标题</strong></td>
   <td><strong>类型</strong></td>
   <td><strong>CSS 文件名称</strong><br /> </td>
  </tr>
  <tr>
   <td>传送_点线_暗</td>
   <td>传送(_S)</td>
   <td><code>html5_carouselviewer_dotted_dark.css</code></td>
  </tr>
  <tr>
   <td>传送_点线_光</td>
   <td>传送(_S)</td>
   <td><code>html5_carouselviewer_dotted_light.css</code></td>
  </tr>
  <tr>
   <td>传送_数值_深</td>
   <td>传送(_S)</td>
   <td><code>html5_carouselviewer_numeric_dark.css</code></td>
  </tr>
  <tr>
   <td>传送_数值_光</td>
   <td>传送(_S)</td>
   <td><code>html5_carouselviewer_numeric_light.css</code></td>
  </tr>
  <tr>
   <td>弹出</td>
   <td>弹出缩放</td>
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
   <td>弹出缩放</td>
   <td><code>html5_inlinezoomviewer.css</code></td>
  </tr>
  <tr>
   <td>MixedMedia_dark</td>
   <td>混合媒体</td>
   <td><code>html5_mixedmediaviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>混合媒体_light</td>
   <td>混合媒体</td>
   <td><code>html5_mixedmediaviewer_light.css</code></td>
  </tr>
  <tr>
   <td>PanoramicImage</td>
   <td>全景图(_I)</td>
   <td><code>html5_panoramicimage.css</code></td>
  </tr>
  <tr>
   <td>PanoramicImageVR</td>
   <td>全景图(_I)</td>
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
   <td><p>Video360_social</p> <p>(包括基本的视频播放控件、在立体模式下进行视频渲染、关闭手动视图点控件但打开陀螺仪控件，且没有社交媒体功能)</p> </td>
   <td>Video_360</td>
   <td><code>html5_video360viewersocial.css</code></td>
  </tr>
  <tr>
   <td><p>Video360VR</p> <p>(专为使用虚拟现实眼镜的最终用户设计。 包括基本的视频播放控件和社交媒体功能)</p> </td>
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

### 支持的移动查看器手势矩阵{#supported-mobile-viewers-gestures-matrix}

下表标识了iOS、Android™ 2.x和Android™ 3.x设备支持的移动查看器手势。

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
   <td><p><strong>多次点击</strong></p> </td>
   <td><p>不适用</p> </td>
   <td><p>放大或重置</p> </td>
   <td><p>放大或重置</p> </td>
  </tr>
  <tr>
   <td><p><strong>开合</strong></p> </td>
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

## 增加显示{#increasing-the-number-of-viewer-presets-that-display}的查看器预设数

Experience Manager在从&#x200B;**[!UICONTROL 详细信息视图>查看器]**&#x200B;查看资产时显示各种查看器预设。 您可以增加或减少显示的查看器数量。

**要增加显示的查看器预设数，请执行以下操作：**

1. 导航到CRXDE Lite([https://localhost:4502/crx/de](https://localhost:4502/crx/de))。
1. 导航到位于`/libs/dam/gui/coral/content/commons/sidepanels/viewerpresets/viewerpresetslist`的查看器预设列表节点

   ![chlimage_1-221](/help/assets/dynamic-media/assets/chlimage_1-221.png)

1. 在 **[!UICONTROL limit]** 属性中，将默认设 **[!UICONTROL 置为15的Value]**（值）更改为所需的数字。
1. 导航到位于`/libs/dam/gui/coral/content/commons/sidepanels/viewerpresets/viewerpresetslist/datasource`的查看器预设数据源

   ![chlimage_1-222](/help/assets/dynamic-media/assets/chlimage_1-222.png)

1. 在limit属性中，将数字更改为所需的数字，例如`{empty requestPathInfo.selectors[1] ? "20" : requestPathInfo.selectors[1]}`
1. 点按&#x200B;**[!UICONTROL 保存全部]**。

## 创建查看器预设{#creating-a-new-viewer-preset}

通过创建查看器预设，您可以将各种设置应用于视图并与资产交互。 但是，您不需要创建查看器预设。 您可以根据需要使用Experience Manager资产附带的现成默认查看器预设。

如果选择创建查看器预设，则在保存查看器预设后，查看器的状态将在“查看器预设”页面中自动激活（设置为&#x200B;**[!UICONTROL On]**）。 此状态意味着无论您何时预览图像或视频，都可以在Dynamic Media组件和交互式媒体组件中看到该状态。

某些查看器预设具有可影响查看器的使用和整体行为的专用设置。 根据您创建的查看器预设，您需要了解这些特殊注意事项。

请参阅[创建交互式查看器预设的特殊注意事项](#special-considerations-for-creating-an-interactive-viewer-preset)。

请参阅[创建传送横幅查看器预设的特殊注意事项](#special-considerations-for-creating-a-carousel-banner-viewer-preset)。

**要创建查看器预设，请执行以下操作：**

1. 在Experience Manager的左上角，点按Experience Manager徽标，然后在左边栏中，点按&#x200B;**[!UICONTROL 工具]**（锤子图标）> **[!UICONTROL 资产] > [!UICONTROL 查看器预设]**。

   ![6_5_viewerpresets](assets/6_5_viewerpresets.png)

1. 在“查看器预设”页面的工具栏中，点按&#x200B;**[!UICONTROL 创建]**。
1. 在&#x200B;**[!UICONTROL 新查看器预设]**&#x200B;对话框的&#x200B;**[!UICONTROL 预设名称]**&#x200B;字段中，输入新预设的名称。请仔细选择名称 - 在您点按&#x200B;**[!UICONTROL 创建]**&#x200B;后，这些名称将不可编辑。

   当您稍后在这些步骤中保存预设时，该名称会显示在“查看器预设”页面的“预设标题”列标题下。

1. 在“富媒体类型”下拉菜单中，选择要创建的查看器预设类型，然后在页面的右上角，点按&#x200B;**[!UICONTROL 创建]**。

   请参阅[查看器预设的富媒体类型](#rich-media-types-for-viewer-presets)。

1. 在“查看器预设编辑器”页面上，点按&#x200B;**[!UICONTROL 外观]**&#x200B;选项卡。
1. 执行下列操作之一：

   * 在&#x200B;**[!UICONTROL 选定类型]**&#x200B;下拉菜单中，选择要自定义其可视设计的组件。 或者，您也可以点按或单击查看器中的任何可视元素，以选择进行配置。

      通过可视编辑器，您可以查看特定属性对样式的影响。 设置或调整任何属性，以使用编辑器左侧的范例即时查看它对查看器产生的影响。

      [查看器参考指南](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html)中的“自定义&#x200B;*`<viewer name>`*&#x200B;查看器”帮助主题中介绍了每种类型的查看器预设的CSS样式属性。 例如，如果要创建类型为`Mixed_Media`的查看器预设，请参阅[自定义混合媒体查看器](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/mixed-media/customing-mixed-media/c-html5-mixedmedia-viewer-customizingviewer.html)以获取每个属性的列表和说明。

   * 如果您在单独的CSS文件中定义了样式设置，则可以将CSS文件上传到Experience Manager资产。 要查找已上传的CSS文件并将其与查看器预设关联，请点按&#x200B;**[!UICONTROL 选定类型]**&#x200B;下拉菜单下的&#x200B;**[!UICONTROL 导入CSS]**（如有必要，请向上滚动可视编辑器以查看它）。

      导入CSS文件时，可视编辑器会检查CSS是否使用了正确的查看器标记。 例如，如果要创建缩放查看器，则必须使用父查看器元素上定义的查看器类名`.s7mixedmediaviewer`定义导入的所有CSS规则。

      只要为给定查看器正确定义CSS标记，就可以导入任意手工CSS。 (在[查看器参考指南](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html)中的任何“自定义&#x200B;*&lt;查看器名称>*&#x200B;查看器”帮助主题中介绍了CSS标记。 例如，如果要阅读有关缩放查看器的CSS标记的信息，请参阅[自定义缩放查看器](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/zoom/customizing-zoom/c-html5-20-zoom-viewer-customizingviewer.html)。) 但是，可视编辑器可能不理解某些CSS值。 在这种情况下，可视编辑器会尝试覆盖错误，以便CSS仍然可以工作。
   >[!NOTE]
   >
   >如果您希望直接以CSS的原始形式编辑CSS，请点按“选定类型”下拉菜单下的&#x200B;**[!UICONTROL 显示/隐藏CSS]**（如有必要，向上滚动可视编辑器以查看它）。
   >与可视编辑器一样，当您直接在CSS中更改属性时，您可以立即看到它对查看器范例产生了什么影响。 而且，同一属性会在可视编辑器中同时自动更新。 因此，您可以使用原始CSS编辑器或可视编辑器，或同时使用两者。

   >[!NOTE]
   >
   >对于按钮图稿，选择2x图像并上传高分辨率图稿。 处理交互式图像和购物横幅时，您还可以从各种现成的热点按钮中进行选择。

1. （可选）在“编辑查看器预设”页面顶部附近，点按 **[!UICONTROL Desktop]**、 **[!UICONTROL Tablet]**&#x200B;或 **[!UICONTROL Phone]** ，为不同设备和屏幕类型唯一定义可视样式。
1. 在“查看器预设编辑器”页面上，点按&#x200B;**[!UICONTROL 行为]**&#x200B;选项卡。 或者，您也可以点按或单击查看器中的任何可视元素，以选择进行配置。
1. 从&#x200B;**[!UICONTROL 选定类型]**&#x200B;下拉菜单中，选择要更改其行为的组件。

   可视编辑器中的许多组件都有与其关联的详细说明。 当您展开组件以显示其关联参数时，这些说明会显示在蓝色框中。

   有些“查看器类型”具有的组件允许您在 **[!UICONTROL IS 命令]**&#x200B;文本字段中指定“图像提供”命令。有关可使用的命令列表，请参阅[图像提供 API 参考](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/c-is-home.html)。

   >[!NOTE]
   >
   >**如果您使用触控设备，如手机或平板电脑……**
   >
   >
   >在文本字段中键入值后，点按用户界面中的其他位置，以提交所做的更改并关闭虚拟键盘。如果您点按 Enter，则不会执行任何操作。

1. 在页面的右上角附近，点按&#x200B;**[!UICONTROL 保存]**。
1. 发布新查看器预设。 您必须先发布预设，然后才能在您的网站上使用预设。

   请参阅[发布查看器预设](#publishing-viewer-presets)。

### 创建交互式查看器预设{#special-considerations-for-creating-an-interactive-viewer-preset}的特殊注意事项

**关于面板中图像缩览图的显示模式：**

在创建或编辑交互式视频查看器预设时，您可以选择使用哪种显示模式设置。 当您从&#x200B;**[!UICONTROL 行为]**&#x200B;选项卡下的&#x200B;**[!UICONTROL 选定组件]**&#x200B;下拉菜单中选择`InteractiveSwatches`时，会出现此选择。 您选择的“显示”模式会影响视频播放时缩略图的显示方式和显示时间。您可以选择 `segment` 显示模式（默认）或 `continuous` 显示模式。

<table>
 <tbody>
  <tr>
   <td><strong>显示模式</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>区段</td>
   <td><p><code>Segment </code>是开箱即用的交互式视频查看器预设<code>Shoppable_Video_light</code>和<code>Shoppable_Video_dark</code>以及您自己创建的任何交互式视频查看器预设的默认显示模式。</p> <p>在此模式下，假定分配给视频区段的缩略图数少于显示面板中可见点数。 在这种情况下，下一个或上一个子段的缩览图不是</i>拖入，以填充面板中的任何空白点。 <i>也就是说，它会保留分配给特定视频区段的色板的显示。</i></p> </td>
  </tr>
  <tr>
   <td>连续</td>
   <td><p>在<code>continuous </code>显示模式中，假定区段中缩略图的数量小于面板中可见缩略图的数量。 在这种情况下，查看器会自动显示下一个区段或上一个区段的缩略图，而上一个区段会显示最后一个缩略图。</p> <p>本主题</a>中的<a href="/help/assets/dynamic-media/interactive-videos.md">视频是<code>continuous </code>显示模式的示例。</a></p> </td>
  </tr>
 </tbody>
</table>

**关于交互式视频查看器中的自动滚动行为：**

交互式视频查看器中缩略图的自动滚动行为与您选择的显示模式无关。

创建或编辑交互式视频查看器预设时，您可以从“行为”选项卡访问“自动滚动”。在“行为”选项卡的&#x200B;**[!UICONTROL 选定的组件]**&#x200B;下拉菜单中，点按 **[!UICONTROL InteractiveSwatches]**。“自动滚动”复选框列在“IS 命令”文本字段的下方。

如果在查看器预设中禁用&#x200B;**[!UICONTROL 自动滚动]**（清除复选框），则在用户播放视频时，该面板仅显示整个视频长度的第一个缩略图。但是，如果需要，用户可以使用向上和向下箭头图标手动滚动缩略图。

在查看器预设中启用（选择）**[!UICONTROL 自动滚动]**&#x200B;后，在视频播放过程中，分配给视频区段的缩略图图像会在区段开始时滚动到视图中。但是，在某些情况下，区段内某些缩略图的显示时间是其之前或之后缩略图显示时间的两倍。发生此行为的原因是区段中缩略图的数量大于面板中可见缩略图的数量，且不可平均分割。

为说明这一点，假定您有一个30秒的视频区段。 在30秒内总共有9个缩略图可显示。 您的浏览器的大小调整到显示面板中有四个可见的缩略图位置。 30秒的视频时间段被分成三个子段。 下表显示了对给定时间子区段显示哪些缩略图的划分：

| **视频子段** | **子区段时间（以秒为单位）** | **面板中可见的缩略图** |
|---|---|---|
| 1 | 0-10 | 1，2，3，4 |
| 2 | 10-20 | 4，5，6，7 |
| 3 | 20-30 | 6，7，8，9 |

视频子区段3不会超出分配给它的缩略图。 另请注意，缩略图 4、6 和 7 在面板中出现的时间是其他缩略图的两倍。

查看器根据可用位置的数量，根据面板中显示的缩略图数量，遵循以下逻辑：

* 子段数=舍入到下一个子段（缩略图数量/缩略图面板中可见插槽数，视浏览器窗口大小而定）。
使用上表中的示例，9个缩略图/ 4个插槽= 2.25;查看器逻辑将其舍入为三个子段。

* 缩略图数量=舍入到下一个缩略图（缩略图数量/视频子区段数量）。
使用上表中的示例，9个缩略图/ 3个视频子段= 3个缩略图。

* 子区段的持续时间=视频总持续时间/视频子区段的数量。
使用上表中的示例，30秒/ 3个视频子段=每个视频子段的10秒显示。

#### 创建传送横幅查看器预设的特殊注意事项{#special-considerations-for-creating-a-carousel-banner-viewer-preset}

创建传送横幅查看器预设时，可通过以下方式更改热点的样式：

|  | **描述** | **操作** |
|---|---|---|
| **[!UICONTROL 热点图标]** | 更改用于热点的图标 | 要更改热点图标图像，请在&#x200B;**[!UICONTROL 外观]**&#x200B;选项卡的&#x200B;**[!UICONTROL 选定组件]**&#x200B;中，点按&#x200B;**[!UICONTROL ImageMapEffect]**。 在&#x200B;**[!UICONTROL 图标]**&#x200B;下，选择&#x200B;**[!UICONTROL 背景]**，并在&#x200B;**[!UICONTROL 图像]**&#x200B;字段中导航到所需的背景图像。 |

## 激活或取消激活查看器预设{#activating-or-deactivating-viewer-presets}

用户界面中可用的查看器预设取决于哪些查看器预设在创作模式下处于活动状态。 默认情况下，在您创建查看器预设后，该查看器预设处于“开启”状态。 如果您关闭预设，则在“创作”模式下不会看到该预设。 如果预设已发布，则无论其是打开还是关闭，都始终会发布该预设。 如果列表变得过于笨拙或您不希望某个查看器预设可供使用，则取消激活查看器预设。

**要激活或取消激活查看器预设，请执行以下操作：**

1. 在Experience Manager的左上角，点按Experience Manager徽标，然后在左边栏中，点按&#x200B;**[!UICONTROL 工具]**（锤子图标）> **[!UICONTROL 资产] > [!UICONTROL 查看器预设]**。
1. 在“查看器预设”页面的&#x200B;**[!UICONTROL State]**&#x200B;列标题下，点按切换以激活或取消激活查看器预设。

   激活的查看器预设可在右侧蓝色框内进行切换；停用的查看器预设可让切换显示在灰色浅框内的左侧。

## 发布查看器预设{#publishing-viewer-presets}

激活（或打开“打开”）查看器预设的状态意味着查看器预设可在Dynamic Media组件、交互式媒体组件中以及每次视图资产时都可见。

但是，要&#x200B;*传送*&#x200B;包含查看器预设的资产，还必须发布查看器预设。 必须激活&#x200B;*和*&#x200B;所有查看器预设，才能获取资产的URL或嵌入代码。 激活和发布Dynamic Media附带的所有现成查看器预设。 您创建和添加的自定义查看器预设将自动激活，但也必须发布。

请参阅[激活或取消激活查看器预设](#activating-or-deactivating-viewer-presets)。

另请参阅[预览资产](/help/assets/dynamic-media/previewing-assets.md)。

**要发布查看器预设，请执行以下操作：**

1. 在Experience Manager的左上角，点按Experience Manager徽标，然后在左边栏中，点按&#x200B;**[!UICONTROL 工具]**（锤子图标）> **[!UICONTROL 资产] > [!UICONTROL 查看器预设]**。
1. 选择要发布的一个或多个查看器预设。
1. 在工具栏中，点按&#x200B;**[!UICONTROL 发布]**&#x200B;图标。

## 为查看器预设排序 {#sorting-viewer-presets}

1. 在Experience Manager的左上角，点按Experience Manager徽标，然后在左边栏中，点按&#x200B;**[!UICONTROL 工具]**（锤子图标）> **[!UICONTROL 资产] > [!UICONTROL 查看器预设]**。
1. 单击&#x200B;**[!UICONTROL 预设标题]**、**[!UICONTROL 类型]**、**[!UICONTROL 已发布]**&#x200B;或&#x200B;**[!UICONTROL 状态]**&#x200B;来按列标题进行排序。例如，单击&#x200B;**[!UICONTROL 类型]**&#x200B;按字母顺序或反向字母顺序对查看器预设类型进行排序。

## 编辑查看器预设 {#editing-viewer-presets}

不支持编辑任何预定义的现成查看器预设&#x200B;*。*&#x200B;如果您编辑现成的查看器预设，系统会提示您用新名称保存该查看器预设。

**要编辑查看器预设，请执行以下操作：**

1. 在Experience Manager的左上角，点按Experience Manager徽标，然后在左边栏中，点按&#x200B;**[!UICONTROL 工具]**（锤子图标）> **[!UICONTROL 资产] > [!UICONTROL 查看器预设]**。
1. 选中查看器预设标题左侧的框，以选择预设。
1. 在工具栏中，点按&#x200B;**[!UICONTROL 编辑]**。
1. 在&#x200B;**[!UICONTROL 查看器预设编辑器]**&#x200B;页面上，使用&#x200B;**[!UICONTROL 外观]**&#x200B;和&#x200B;**[!UICONTROL 行为]**&#x200B;选项卡上的选项，对查看器预设进行更改。

   在“查看器预设编辑器”页面左上角附近的&#x200B;**[!UICONTROL 外观]**&#x200B;选项卡中，点按&#x200B;**[!UICONTROL 桌面]**、**[!UICONTROL 平板电脑]**&#x200B;或&#x200B;**[!UICONTROL 手机]**，以更改资产的显示模式。

1. 在页面的右上角附近，执行下列操作之一：

   * 点按&#x200B;**[!UICONTROL 保存]**&#x200B;以保存更改并返回“查看器预设”页面。
   * 点按&#x200B;**[!UICONTROL 取消]**，撤消您所做的任何更改并返回“查看器预设”页面。

## 删除自定义查看器预设{#deleting-custom-viewer-presets}

您可以删除已创建并添加到Dynamic Media的查看器预设。

**要删除自定义查看器预设，请执行以下操作：**

1. 在Experience Manager的左上角，点按Experience Manager徽标，然后在左边栏中，点按&#x200B;**[!UICONTROL 工具]**（锤子图标）> **[!UICONTROL 资产] > [!UICONTROL 查看器预设]**。
1. 在“查看器预设”页面上，选中预设标题，然后点按&#x200B;**[!UICONTROL 垃圾桶]**&#x200B;图标。
1. 点按&#x200B;**[!UICONTROL 删除]**。

## 将查看器预设应用到资产{#applying-a-viewer-preset-to-an-asset}

如果已发布资产和选定的查看器，则在选择查看器预设后 **[!UICONTROL 将显示]** “ **[!UICONTROL URL]** ”和“嵌入”按钮。

**要将查看器预设应用到资产，请执行以下操作：**

1. 打开资产，然后在页面左上角附近，点按下拉菜单，然后选择&#x200B;**[!UICONTROL 查看器]**。

   >[!NOTE]
   >
   >如果已发布资产和选定的查看器，则在选择查看器预设后 **[!UICONTROL 将显示]** “ **[!UICONTROL URL]** ”和“嵌入”按钮。

1. 要将其应用到资产，请从左侧窗格中选择查看器预设。

   您可以[复制URL以与其他用户共享](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)。

## 使用查看器预设{#delivering-assets-with-viewer-presets}传送资产

要获取查看器预设的 URL，请参阅[将 URL 关联到您的 Web 应用程序](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)。另请参阅[将视频查看器嵌入网页](/help/assets/dynamic-media/embed-code.md)。

如果您使用Experience Manager作为WCM，则可以直接在页面上使用查看器预设添加资产。 请参阅[将Dynamic Media资产添加到页面](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)。
