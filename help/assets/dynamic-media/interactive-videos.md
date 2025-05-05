---
title: 交互式视频
description: 了解如何在Dynamic Media中使用交互式视频和可购物视频。
contentOwner: Rick Brough
feature: Interactive Videos
role: User
exl-id: e4859223-91de-47a1-a789-c2a9447e5f71
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '5863'
ht-degree: 2%

---

# 交互式视频{#interactive-videos}

您可以轻松地创建交互式视频（也称为购物视频），以直接从视频推动转化。 客户与视频的互动发生在视频播放器旁边的面板中，在该面板中，相关服务、信息或产品缩略图会根据视频中的功能滚动到视图中。 客户可以选择缩略图并直接链接到服务，或者将项目添加到购物车以供立即购买，或者链接到网页以了解更多信息。

视频结束时，会显示所有产品的可视化摘要，以激发行动号召。 客户还有另一个机会选择所需的项目。 诸如此类的可操作且具体的体验可提高客户参与度和转化率。

另请参阅[交互式图像](/help/assets/dynamic-media/interactive-images.md)。

## 交互式视频的实际操作情况 {#interactive-video-in-action}

要查看交互式购物视频的实际操作情况，请选择[实时演示](https://landing.adobe.com/zh-Hans/na/dynamic-media/ctir-2755/live-demos.html)，滚动到页面上的&#x200B;**[!UICONTROL 购物媒体]**&#x200B;标题，然后选择购物视频开始播放。

* 在播放期间，当在视频中使用产品时，相同的产品会在右侧显示为缩略图。

* 要暂停视频并打开产品的概览，请选择缩略图。 例如，在视频中选择KitchenAid缩略图图像以体验混合器的360°旋转视图，或放大以查看混合器的详细信息。

另请参阅[在Dynamic Media中使用交互式视频](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-interactive-video-feature-video-use.html#dynamic-media)

<!-- 

There was a link here that showed the video frame of an interactive video and when the reader selected the frame the video would play https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/AXIS/index.html. This must now call a new interactive video

-->

<!-- 

[A frame from an interactive, shoppable video](assets/chlimage_1-126.png) *A video frame capture from an interactive, shoppable video.*

-->

>[!NOTE]
>
>如果在用户选择缩略图图像时创建交互式视频以启动网页，则某些设备会阻止打开弹出网页。 在这种情况下，请更改设备上的弹出窗口阻止程序设置。 例如，在Apple iPhone 6上，转到&#x200B;**[!UICONTROL 设置]** > **[!UICONTROL Safari]** > **[!UICONTROL 阻止弹出窗口]**，然后将控件滑动到&#x200B;**[!UICONTROL 关闭]**。 现在，当您播放交互式视频并选择缩略图时，如果想要打开弹出窗口，系统会提示您进行选择。 如果接受，将打开网页。

### 观看如何创建交互式视频 {#watch-how-interactive-videos-are-created}

观看有关[如何创建交互式视频的演练](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveVideo)（7分30秒）。
(尽管视频演练使用Assets（按需）进行标记，但Adobe Experience Manager Assets中的交互式视频仍适用这些原则和步骤。)

### Adobe客户成功网络研讨会 {#adobe-customer-success-webinar}

Experience Manager Assets中的[使用交互式视频、链接共享和YouTube共享](https://adobecustomersuccess.adobeconnect.com/p1yxzdo4aec/)网络研讨会教您如何使用交互式视频和其他功能将转化驱动型事件与视频营销内容关联起来。

## 快速入门：交互式视频 {#quick-start-interactive-videos}

以下分步工作流描述旨在帮助您在Dynamic Media中快速启动和运行交互式视频。

在某些快速入门任务中查找&#x200B;**Example**&#x200B;标题。 它包含一个简短的教程，该教程基于此[启动演示网页，*尚未*&#x200B;添加交互功能](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html)。

**示例**&#x200B;有助于说明在您的网站上集成交互式视频的步骤。

当您完成最后一个示例部分中的教程时，[您的最终演示网页和完全集成的交互式视频将以这种方式显示](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-3.html)。

交互式视频步骤：

1. **（可选）识别概览变量** — 首先识别由您现有的概览实施使用的动态变量。 在创建交互式视频时，可使用变量将产品缩略图映射到对应的产品概览。 请参阅[（可选）标识概览变量](#optional-identifying-quickview-variables)。
   **仅当以下所有条件都为true时，才需要执行此步骤：**
   * 要通过触发快速视图向视频添加交互性。
   * Experience Manager实施&#x200B;*不*&#x200B;使用电子商务集成框架，将产品数据从任何电子商务解决方案(如IBM®WebSphere®Commerce、Elastic Path、SAP Hybris或Intershop)提取到Experience Manager。

1. **（可选）创建交互式视频查看器预设** — 自定义组成播放器的各种组件的外观和行为，如视频洗刷和交互式缩略图。
如果您打算使用现成的交互式视频查看器预设`Shoppable_Video_Light`或`Shoppable_Video_Dark`，则无需创建自己的交互式视频查看器预设。
请参阅[创建查看器预设](/help/assets/dynamic-media/managing-viewer-presets.md#creating-a-new-viewer-preset)（可选）以及创建交互式查看器预设的[特殊注意事项](/help/assets/dynamic-media/managing-viewer-presets.md#special-considerations-for-creating-an-interactive-viewer-preset)。

1. **上传视频及其相关图像资源** — 上传要交互的视频和相关图像。
查看[上传视频及其关联的缩略图资产](#uploading-a-video-and-its-associated-thumbnail-assets)。

   >[!NOTE]
   >
   >尚不支持MXF视频格式用于Dynamic Media中的交互式视频。

1. **向视频添加交互性** — 向视频添加一个或多个时间段。 然后，关联这些时间段内的图像缩略图。 将每个图像缩略图分配给某个操作，例如超链接、概览或体验片段。
(如果您的交互式内容包含具有相对URL的链接，尤其是指向Experience Manager Sites页面的链接，则无法基于URL的链接方法。)
完成方法是发布交互式视频资产。 发布操作将创建您最终复制并应用于网站登陆页面的嵌入代码或URL。 请参阅[向视频添加交互性](#adding-interactivity-to-your-video)。
请参阅[发布Assets](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)。

1. **在Experience Manager中将交互式视频添加到您的网站或您的网站** — 如果您使用Experience Manager Sites或eCommerce，或同时使用两者，请将该交互式视频添加到Experience Manager中的网页。 将Interactive Media组件拖动到页面上。 请参阅[将Dynamic Media Assets添加到页面](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)。
使用嵌入代码或URL将交互式视频与网站体验集成。 请参阅[将交互式视频与您的网站集成](#integrating-an-interactive-video-with-your-website)。
如果您使用的是第三方WCM（Web内容管理器），则必须将新的交互式视频与网站上使用的现有Quickview实施集成。 请参阅[将交互式视频与现有概览集成](#integrating-an-interactive-video-with-an-existing-quickview)。
   [将Dynamic Media Assets添加到页面](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)

## （可选）标识概览变量 {#optional-identifying-quickview-variables}

>[!NOTE]
>
>仅当满足以下条件时，才需要此任务：
>
>* 要通过触发快速视图向视频添加交互性。
>* Experience Manager实施&#x200B;*不*&#x200B;使用电子商务集成框架，将产品数据从任何电子商务解决方案(如IBM®WebSphere®Commerce、Elastic Path、SAP Hybris或Intershop)提取到Experience Manager。<!-- See [eCommerce concepts in Experience Manager Assets](/help/sites-administering/concepts.md).-->
>
>如果您的Experience Manager实施使用的是电子商务，则可以跳过此任务并继续执行下一个任务。

首先，标识现有Quickview实施使用的动态变量，以便您可以在交互式视频创建过程中将产品缩略图映射到其相应的产品Quickview。

向视频添加时间区段时，您需要为添加到区段的每个缩略图分配一个SKU（库存单位）和任何其他变量。 此类变量稍后用于显示正确的概览产品。

正确识别唯一触发产品概览所需的变量很重要。

有时，咨询负责现有Quickview实施的IT专家就足够了。 他们可能会知道系统中用于标识概览的最小数据集。 但是，可以简单地分析前端代码的现有行为。

大多数概览实施都使用以下范例：

* 用户在网站上激活用户界面元素。例如，选择“概览”按钮。
* 如果需要，网站会向后端发送Ajax请求以加载概览数据或内容。
* 概览数据将转换为内容，为在网页上呈现做准备。
* 最后，前端代码在屏幕上以可视方式呈现此类内容。

因此，方法是访问实施Quickview的现有网站的不同区域。 然后触发概观，并获取网页发送的Ajax URL，用于加载概观数据或内容。

通常，您无需使用任何专门的调试工具。 现代Web浏览器的功能是Web检查器，这些检查器可以完成适当的工作。 以下是一些包含Web检查器的Web浏览器示例：

* 要在Google Chrome中查看所有传出的HTTP请求，请按&#x200B;**F12** (Windows®)或&#x200B;**Command+Options+I** (Mac)以打开“开发人员工具”面板，然后选择&#x200B;**网络**&#x200B;选项卡。

* 在Firefox中，您可以通过按&#x200B;**F12** (Windows®)或&#x200B;**Command+Option+I** (Mac)并使用其&#x200B;**[!UICONTROL Net]**&#x200B;选项卡来激活Firebug插件，也可以使用内置的检查器工具及其“网络”选项卡。

* 在Internet Explorer中，按&#x200B;**F12**&#x200B;激活调试器工具。

在浏览器中打开网络监视时，将触发页面上的快速视图。

现在，在网络日志中找到Quickview Ajax URL，并复制记录的URL以供将来分析。 通常，在触发概览时，会向服务器发送大量请求。 通常，快速视图Ajax URL是列表中的第一个页面之一。 它具有复杂的查询字符串部分或路径，并且其响应MIME类型为`text/html`、`text/xml`或`text/javascript`。

在此过程中，请务必访问网站的不同区域，以及不同的产品类别和类型。 原因是概览的URL具有给定网站类别共有的部分，但只有在访问网站的其他区域时才发生更改。

最简单的例子是，概观URL中的唯一变量部分是产品SKU。 在这种情况下，产品SKU值是向Experience Manager中交互式视频的时间段添加缩略图所需的唯一数据块。

但是，在复杂的情况下，除了产品SKU之外，快速视图URL还有不同的元素，例如类别ID和颜色代码。 在这种情况下，在Experience Manager的缩略图数据定义中，每个此类元素都会成为单独的变量。

请仔细研究一下以下概览实例URL及其生成的缩略图变量：

<table>
  <tbody>
  <tr>
    <td><p>单个SKU，在查询字符串中找到。</p> </td>
    <td><p>记录的概览URL包括：</p>
    <ul>
      <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>URL中的唯一变量部分是<code>productId=</code>查询字符串参数的值，它显然是SKU值。 因此，缩略图只需要使用诸如<strong><code>866558</code></strong>、<strong><code>1196184</code></strong>、<strong><code>1081492</code></strong>、<strong><code>1898294</code></strong>之类的值填充的SKU字段。</p> </td>
  </tr>
  <tr>
    <td><p>单个SKU，可在URL路径中找到。</p> </td>
    <td><p>记录的概览URL包括：</p>
    <ul>
      <li><p><code>https://server/product/6422350843</code></p> </li>
      <li><p><code>https://server/product/1607745002</code></p> </li>
      <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>变量部分位于路径的最后一部分，它将变为Experience Manager缩略图的SKU值： <strong><code>6422350843</code></strong>、<strong><code>1607745002</code></strong>、<strong><code>0086724882</code></strong>。</p> </td>
  </tr>
  <tr>
    <td><p>查询字符串中的SKU和类别ID。</p> </td>
    <td><p>记录的概览URL包括：</p>
    <ul>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>在这种情况下，URL包含两个不同的部分。 SKU存储在<code>prodId</code>参数中，类别ID存储在<code>category=</code>参数中。</p> <p>因此，缩略图定义是对。 即SKU值和名为<code>categoryId</code>的额外变量。 生成的对如下所示：</p>
    <ul>
      <li>SKU是<code>305466</code>，<code>categoryId</code>是 <code>1100004</code></li>
      <li>SKU是<code>310181</code>，<code>categoryId</code>是 <code>1100004</code></li>
      <li>SKU是<code>308706</code>，<code>categoryId</code>是 <code>1740148</code></li>
    </ul> <p> </p> </td>
  </tr>
  </tbody>
</table>

**示例**

将以上方法应用于示例网站后，您的网页具有多个产品缩略图，每个产品缩略图都有一个“了解更多”按钮：

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html)

激活页面上所有可用的产品快速视图后，您将获得向后端发出的概览请求列表：

* datafeed/candles-233396346.json
* datafeed/candles-233978050.json
* datafeed/candles-234024346.json
* datafeed/candles-234024356.json
* datafeed/candles-234024359.json
* datafeed/cushions-233939848.json
* datafeed/cushions-234019477.json
* datafeed/cushions-234019483.json
* datafeed/furniture-231747479.json
* datafeed/furniture-232625621.json
* datafeed/furniture-232625626.json
* datafeed/furniture-233939810.json
* datafeed/furniture-233939825.json
* datafeed/furniture-233939828.json
* datafeed/furniture-233939853.json
* datafeed/furniture-233940334.json
* datafeed/glassware-000064007.json
* datafeed/glassware-230722193.json
* datafeed/glassware-233916550.json
* datafeed/glassware-233916597.json

查看服务器调用时，特定于产品的信息仅显示在请求路径中。 您还会注意到根本未使用查询字符串，并且其中涉及两种不同类型的数据段：

* 第一种是蜡烛、垫子、家具和玻璃器具。 您可以将此区段命名为“产品类别”。
* 第二种是产品代码，如233916597。 您可以假设它是“产品SKU”。

根据此信息，整个概览URL具有以下模式：

`/datafeed/$categoryId$-$SKU$.json`

基于此类分析，您可以得出这样的结论：对于缩略图，可以使用以下两个变量： `categoryId`和`SKU`。

您现在可以上传视频及其关联的缩略图资产。

## （可选）创建交互式视频查看器预设 {#optional-creating-an-interactive-video-viewer-preset}

如果您打算使用默认的、现成的交互式视频查看器预设类型`Shoppable_Video_dark`或`Shoppable_Video_light`，则可以跳过此任务并继续执行下一个任务。

在创作环境中选择缩略图时，会显示“概览”对话框的预览。

![chlimage_1-21](assets/chlimage_1-127.png)

您可以选择创建自己的自定义交互式视频查看器预设。 您可以确定视频播放器的样式、交互式缩略图以及视频末尾显示的缩略图网格视图等。

交互式视频查看器预设可正确呈现视频以及您添加的所有时间轴区段。 在“预览”模式下选择产品缩略图时，它还使用默认概览示例，以便您可以在发布之前测试其交互性。

保存查看器预设后，“查看器预设”页面中的查看器预设状态将自动设置为 **开**。此状态表明查看器预设在 Dynamic Media 组件中可见，预览视频时也可见。另请确保手动发布新查看器预设。

请参阅[创建查看器预设](/help/assets/dynamic-media/managing-viewer-presets.md#creating-a-new-viewer-preset)以创建您自己的交互式视频查看器预设。

## 上传视频及其关联的缩略图资产 {#uploading-a-video-and-its-associated-thumbnail-assets}

如果您已经上传了视频和缩略图资产，请继续[向视频添加交互性](#adding-interactivity-to-your-video)。

>[!NOTE]
>
>尚不支持MXF视频格式用于Dynamic Media中的交互式视频。

如果上传了错误的视频或图像，或者要删除不再需要的上传视频或图像，请参阅[删除Assets](/help/assets/manage-digital-assets.md#delete-assets)。

要上传视频及其关联的缩略图资产，请执行以下操作：

1. 将视频和相关缩略图资源上传到所需的一个或多个文件夹。

   查看[上传资源](/help/assets/manage-digital-assets.md)。
请参阅[使用FTP作业计划](/help/assets/manage-digital-assets.md)上载资源。

   现在，将交互性添加到您的视频。

## 向视频添加交互性 {#adding-interactivity-to-your-video}

使用“创建交互式视频”页面上的就地可视化编辑器，可以向视频添加时间轴区段。

添加时间轴区段后，可在每个区段中添加缩略图图像。 对于您添加的每个缩略图，您都会对其应用操作。 例如，您可以将概览应用于缩略图，也可以为其分配超链接或体验片段。

查看[体验片段](/help/sites-cloud/authoring/fragments/content-fragments.md)。

>[!NOTE]
>
>将查看器嵌入体验片段时，不支持交互式视频中的社交媒体共享工具。 相反，您可以使用或创建没有社交媒体共享工具的查看器预设。 通过此类查看器预设，可成功地将其嵌入体验片段中。

>[!NOTE]
>
>如果您的交互式内容包含具有相对URL的链接，尤其是指向Experience Manager Sites页面的链接，则基于URL的链接方法不可用。

在当前创建/编辑会话期间，支持页面右上角附近的“撤消”和“重做”选项。

保存交互式视频后，该视频会立即在“预览”中打开。 从该位置，您可以选择交互式视频查看器预设并播放视频，以查看向客户显示的相应内容的大致呈现形式。

**向视频添加交互性：**

1. 在Assets视图中，导航到您上传并想要变为交互式内容的视频。
1. 执行下列操作之一：

   * 将鼠标悬停在图像上，然后选择&#x200B;**[!UICONTROL 选择]**（复选标记图标）。 在工具栏上，选择&#x200B;**[!UICONTROL 编辑]**。

   * 将鼠标悬停在图像上，然后选择&#x200B;**[!UICONTROL 更多操作]**（三个圆点图标）**[!UICONTROL >编辑]**。

   * 要在“详细信息视图”页面中将其打开，请选择图像。 在工具栏上，选择&#x200B;**[!UICONTROL 编辑]**。

1. 在“创建交互式视频”页面上，执行以下任一操作：

   * 要开始播放视频，请选择&#x200B;**[!UICONTROL 播放]**&#x200B;按钮。 查看要突出显示的特定产品、服务或详细信息时，在工具栏上选择&#x200B;**[!UICONTROL 添加区段]**。 重复此步骤，直到视频结束。

     对于您添加的每个时间段，您可以为其分配一个或多个缩略图。 然后，您可以将这些缩略图链接到可供客户购买的快速视图产品页面或网页，以了解更多信息。

   * 要开始播放视频，请选择&#x200B;**[!UICONTROL 播放]**&#x200B;按钮。 查看要突出显示的特定产品、服务或详细信息时，请选择&#x200B;**[!UICONTROL 暂停]**。 选择&#x200B;**[!UICONTROL 添加区段]**。

     在时间轴上您要添加区段的各个点继续播放和暂停视频，直到视频结束。

1. （可选）向左拖动&#x200B;**[!UICONTROL 时间轴缩放滑块]**&#x200B;上的栏可放大（向右拖动则缩小）。 通过此类操作，您可以控制所添加区段的详细信息量。

   ![chlimage_1-22](assets/chlimage_1-128.png)

   根据视频的长度，区段持续时间默认为以下值：

   <table>
      <tbody>
        <tr>
        <td><strong>如果视频长度为……</strong></td>
        <td><strong>“区段持续时间”设置默认为……</strong></td>
        </tr>
        <tr>
        <td>3分钟或更多</td>
        <td>60秒</td>
        </tr>
        <tr>
        <td>2-3 分钟</td>
        <td>30秒</td>
        </tr>
        <tr>
        <td>1-2 分钟</td>
        <td>20秒<br /> </td>
        </tr>
        <tr>
        <td>30-60秒</td>
        <td>10秒</td>
        </tr>
        <tr>
        <td>30秒或更短</td>
        <td>5秒</td>
        </tr>
      </tbody>
    </table>

   视频时间轴使用它可用的屏幕区域。 因此，在调整浏览器大小时，您添加的区段将保持其正确的宽度。

   举例说明，以下三个屏幕截图使用的是同一视频。 请注意，每个区段的宽度会根据“时间轴比例”设置而变化。

   ![chlimage_1-23](assets/chlimage_1-129.png)

   屏幕快照A

   上面的屏幕快照A显示了29秒的产品视频的默认视图。 时间轴范围默认设置为5秒。

   ![chlimage_1-130](assets/chlimage_1-130.png)

   屏幕快照B

   在上面的屏幕快照B中，时间轴缩放滑块从默认的5秒拖动到3秒。 请注意，各个时间轴比例时间戳现在均以3秒为间隔进行设置。

   ![chlimage_1-25](assets/chlimage_1-131.png)

   屏幕快照C

   在上面的屏幕快照C中，“时间轴缩放”设置已移动到8秒。 请注意包含产品缩略图的区段如何收缩。 如果您有长视频，并且希望能够大致了解通常适合页面宽度的更多区段，则通过此方式缩小会很有用。

1. （可选）执行下列任一操作：

   * 要调整区段的开始时间和结束时间，请执行以下操作：

     选择一个区段，然后拖动前导或尾随的蓝色椭圆以分别调整开始时间或结束时间。 显示的视频帧会根据您的调整移动到视频中的适当时间。 时间线区段的移动根据时间线中的任何相邻区段而受到限制。 允许的最短段时间为1秒。

     使用以下导航快捷方式快速检查和微调您的视频区段：

      * 要直接搜索到该区段开头的视频，请选择开头的蓝色椭圆。
      * 要直接搜索该区段结尾的视频，请选择结尾的蓝色椭圆形。
      * 要将视频播放返回到该区段的开头，请选择整个区段。

   ![chlimage_1-26](assets/chlimage_1-132.png)

   重新定位时间线区段的结尾

   * 删除区段

     选择时间轴上的最后一个区段，然后在工具栏上，选择&#x200B;**[!UICONTROL 删除区段]**。 如果选择了两个或多个区段，则将禁用“删除区段”功能。

     您只能删除最后一个区段。 例如，如果要删除时间轴上的所有区段，则必须始终选择最后一个区段，然后选择&#x200B;**[!UICONTROL 删除区段]**。

1. 选择要与一个或多个缩略图图像关联的时间段。
1. 在视频的右侧，选择&#x200B;**[!UICONTROL 内容]**&#x200B;选项卡。
1. 在“内容”选项卡下，选择&#x200B;**[!UICONTROL 选择Assets]**，然后浏览并选择要用于视频的所有图像资源。 选定的资产会添加到内容选项卡的资产选择器面板。

1. 在内容选项卡下方的资源选择器中，执行以下任一操作：

   <table>
      <tbody>
        <tr>
        <td>要将缩略图与选定的时间线段相关联，请执行以下操作</td>
        <td><p>在右侧的资产选择器面板中选择图像。</p> <p>您可以向时间线区段添加任意数量的缩略图。 对于您选择的每个图像，资产选择器中的图像上方都会显示一个复选标记。</p> </td>
        </tr>
        <tr>
        <td>要从所选时间线段中删除缩略图，请执行以下操作</td>
        <td><p>执行以下任一操作：</p>
          <ul>
          <li>在资产选择器面板中，选择带有复选标记的图像以取消选择该图像。 图像资产已从时间线段删除。<br /> </li>
          <li>在选定的时间线区段中，选择一个图像，然后在工具栏上，选择<strong>删除产品</strong>。</li>
          </ul> </td>
        </tr>
      </tbody>
    </table>

   ![资产选取器](assets/chlimage_1-133.png)

   在资产选择器面板中选择图像，可将其添加到选定的时间线区段。

1. 选择一个时间轴区段中的单个缩略图图像，然后选择&#x200B;**[!UICONTROL 操作]**&#x200B;选项卡。
1. 执行以下任一操作：
   <table> 
    <tbody> 
      <tr> 
      <td>将选定的缩略图图像与概览关联</td> 
      <td><p>在操作类型下，选择<strong>概览</strong>。</p> <p>如果您是Experience Manager Sites和电子商务客户：</p> 
       <ul> 
       <li>请注意，已使用所选产品的SKU（库存单位）预填充了“SKU值”文本字段。 SKU是您提供的每个不同产品或服务的唯一标识符。 当图像与Experience Manager Commerce中的产品关联时，将自动填充此字段。</li> 
       <li>如果预填充的SKU不正确，请选择“产品选取器”图标（放大镜）以打开“选择产品”页面。 选择要使用的产品，然后选择页面右上角的复选标记。 您将返回到交互式视频编辑器。</li> 
       </ul> <p> 如果您<em>不是</em> Experience Manager Sites或电子商务客户</p> 
       <ul> 
       <li>请参阅<a href="/help/assets/dynamic-media/carousel-banners.md#identifying-hotspot-and-image-map-variables">识别热点变量</a>。 必须定义这些变量。</li> 
       <li>默认情况下，此SKU字段使用图像资源的文件名（不带扩展名）。 如果对基于SKU的文件遵循标准命名约定，则此字段通常不需要任何额外的编辑。 </li> 
       <li>否则，请编辑默认值并输入正确的SKU值。 在“SKU值”文本字段中，键入产品的SKU（库存单位），它是您提供的每个不同产品或服务的唯一标识符。 输入的SKU值会自动填充概览模板的变量部分，以便系统知道将选定的图像与特定SKU的概览相关联。</li> 
       </ul> <p>（可选）如果概览中还有其他变量必须用来进一步标识产品，请选择<strong>添加通用变量</strong>。 在文本字段中，指定一个额外的变量。 例如，<code>category=Womens</code>是添加的变量。</p> <p> </p> </td> 
      </tr> 
      <tr> 
      <td>将选定的缩略图图像与超链接相关联</td> 
      <td><p>在“操作类型”下，选择<strong>超链接</strong>，然后执行以下操作之一：</p> 
       <ul> 
       <li>如果您是Experience Manager Sites客户，请选择站点选择器图标（文件夹）以导航到网页。 如果您的交互式内容包含具有相对URL的链接，尤其是指向Experience Manager Sites页面的链接，则基于URL的链接方法不可用。</li> 
       <li>如果您是独立Dynamic Media客户，请在HREF文本字段中指定链接网页的完整URL路径。</li> 
       </ul> <p>请确保指定是在新的浏览器选项卡中还是在当前选项卡中打开链接。</p> </td> 
      </tr> 
      <tr> 
      <td>将选定的缩略图图像与体验片段关联</td> 
      <td><p>在“操作类型”下，选择<strong>体验片段</strong>，然后执行以下操作：<p> 
       <ul> 
       <li>如果您是Experience Manager Sites客户，请选择“搜索”图标（放大镜）以打开“体验片段”页面。 选择要使用的体验片段，然后选择<strong>要返回上一页的“操作”面板，请选择页面右上角的</strong>。<br />查看<a href="/help/sites-cloud/authoring/fragments/content-fragments.md">体验片段</a>。</li> 
      </ul> 
       <ul> 
       <li>指定视频中显示的体验片段的宽度和高度。</li>
       </ul><strong>注意</strong>：将查看器嵌入体验片段时，不支持交互式视频中的社交媒体共享工具。 相反，您可以使用或创建没有社交媒体共享工具的查看器预设。 通过此类查看器预设，可成功地将其嵌入体验片段中。</p></tr>&lt; 
      <tr> 
      <td>编辑已分配给缩略图图像的操作</td> 
      <td>在时间轴区段中，选择文本标签右侧具有链链接的缩略图图像。 链链接表示为其分配了操作。 要进行更改，请选择<strong>操作</strong>选项卡。</td> 
      </tr> 
      <tr> 
      <td>更改缩略图图像的文本标签</td> 
      <td><p>默认情况下，文本标签使用缩略图图像的<code>Title</code>元数据字段。 如果<code>Title</code>不存在，则改用缩略图图像的文件名，但不使用扩展名。</p> <p>要更改缩略图图像的文本标签，请在所显示图像资源正下方的<strong>操作</strong>选项卡下，输入所需的文本。 请参阅下图。</p> <p>新文本标签仅由视频播放器本身以及在时间轴区段中显示的缩略图文本使用。 标签更改不会影响缩略图图像的标题元数据字段及其文件名。</p> </td> 
      </tr> 
      <tr> 
      <td>还原更改</td> 
      <td>在页面的右上角附近，选择<strong>撤消</strong>或<strong>重做</strong>。</td> 
      </tr> 
    </tbody> 
   </table>

   ![experiencefragment_interactivevideos](assets/experiencefragment_interactivevideos.png)

   新的文本标签将添加到缩略图图像。

1. 执行下列操作之一：

   * 重复步骤6至11以将更多缩略图图像添加到视频中的时间轴区段。
   * 继续执行可选步骤13。

1. （可选）执行以下任一操作：

   * **[!UICONTROL 合并区段]** — 您可以将两个相邻的区段（无论是否为其分配了产品缩略图）合并到一个区段中。

     在时间轴上，选择要合并为一个的两个或多个连续区段。 下图中的两个选定区段上没有蓝色椭圆形拖动手柄。

     在工具栏上选择&#x200B;**[!UICONTROL 合并区段]**。

   ![chlimage_1-134](assets/chlimage_1-134.png)

   将两个选定的5秒区段合并为1个10秒区段。

   * **[!UICONTROL 拆分区段]** — 您可以将单个区段划分为两个等时区段。 如果已有产品缩略图分配给区段，则这些缩略图将合并到左侧区段中。

     在时间轴上，选择要拆分为一半的区段，然后在工具栏上选择&#x200B;**[!UICONTROL 拆分区段]**。

     选择两个或更多区段将禁用&#x200B;**[!UICONTROL 拆分区段]**&#x200B;功能。

   ![chlimage_1-135](assets/chlimage_1-135.png)

   将所选的十秒区段拆分为两个区段，每个区段五秒。

1. 在&#x200B;**[!UICONTROL 创建交互式视频]**&#x200B;页面的右上角附近，将显示当前选定的、用于该视频的查看器预设的名称。 要选择其他查看器预设，请选择名称。

   例如，`Shoppable_Video_light`查看器预设允许您使用视频旁边的白色显示区域播放视频。 在播放过程中，显示区域是显示可选缩略图图像的位置。 `Shoppable_Video_dark`查看器预设允许您使用视频旁边的黑色显示区域播放视频。

   如果您创建了自己的交互式视频查看器预设，则可以在可供选择的预设列表中看到该预设。

   完成后，选择&#x200B;**[!UICONTROL 保存]**。

   >[!NOTE]
   >
   >在保存交互式视频时，会自动保存 `.vtt` 一个关联的文件。 已将`.vtt`文件保存到&#x200B;**[!UICONTROL Assets]**&#x200B;根目录下的`_VTT`文件夹中。 要在网站上正确播放交互式视频，必须填写文件和文件夹。 因此，请勿移动、编辑或删除文件夹 `_VTT` 或其内容。

1. 发布交互式视频。 发布会创建您最终复制并粘贴到网站体验中的嵌入代码或URL。

   如果添加了与快速视图的交互，则仅使用嵌入代码；如果添加了与超链接网页的交互，则还可以使用已发布的URL。 但是，请注意，如果您的交互式内容具有带相对URL的链接，尤其是指向Experience Manager Sites页面的链接，则基于URL的链接方法是不可能的。

   请参阅[发布资源](publishing-dynamicmedia-assets.md)。

   >[!NOTE]
   >
   >要发布带有快速查看功能的可购物视频，请务必单独从商务区域发布视频的每个相关图像资产。

   添加时间轴区段并发布交互式视频后，即可将其添加到现有网站登陆页面。 请参阅[将交互式视频与您的网站集成](#integrating-an-interactive-video-with-your-website)。

## 发布交互式视频资产 {#publishing-interactive-video-assets}

有关如何发布交互式视频资源的详细信息，请参阅[发布Assets](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)。

## 将交互式视频与您的网站集成 {#integrating-an-interactive-video-with-your-website}

在上传视频、向其添加时间轴区段并发布交互式视频后，现在即可将其添加到现有网站。

如果您是Experience Manager Sites客户，则可以通过将交互式媒体组件拖动到页面来添加交互式视频。 请参阅[将Dynamic Media Assets添加到页面](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)。

如果您是独立Experience Manager Assets客户，则可以手动将交互式视频添加到您的网站，如本节所述。

1. 复制发布的交互式视频的嵌入代码或URL。
请参阅[在网页上嵌入视频查看器或图像查看器](/help/assets/dynamic-media/embed-code.md)。
如果添加了与快速视图的交互，则仅使用嵌入代码；如果添加了与超链接网页的交互，则还可以使用已发布的URL。 但是，请注意，如果您的交互式内容具有带相对URL的链接，尤其是指向Experience Manager Sites页面的链接，则基于URL的链接方法是不可能的。

1. 在目标网站的网页代码中，标识静态视频的位置。
1. 移除静态视频，并将代码替换为您从Experience Manager Assets中复制的嵌入代码或URL，如下所示。
复制的嵌入代码是针对响应式环境设置的，因此会自动适合之前由静态视频占用的区域。

>[!NOTE]
>
>此时，如果您只添加与超链接网页的交互，则操作已完成。
>
>但是，如果添加了任何交互性来触发快速视图，则交互式视频旁边的缩略图仅用于显示目的；它们尚未与现有的快速视图集成。 在这种情况下，您必须将交互式视频与网站上现有的快速视图相集成。

**示例**

以演示网站为例：

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html)

请注意，视频嵌入代码是标准代码：

```js {.line-numbers}
<style type="text/css">
 #s7video_div.s7videoviewer{
   width:100%;
   height:auto;
 }
</style>

<script type="text/javascript" src="https://demos-pub.assetsadobe.com/etc/dam/viewers/s7viewers/html5/js/VideoViewer.js"></script>
<div id="s7video_div"></div>
<script type="text/javascript">
 var s7videoviewer = new s7viewers.VideoViewer({
  "containerId" : "s7video_div",
  "params" : {
   "serverurl" : "https://adobedemo62-h.assetsadobe.com/is/image",
   "contenturl" : "https://demos-pub.assetsadobe.com/",
   "config" : "/etc/dam/presets/viewer/Video",
   "config2": "/etc/dam/presets/analytics",
   "videoserverurl": "https://gateway-na.assetsadobe.com/DMGateway/public/demoCo",
   "posterimage": "/content/dam/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4",
   "asset" : "/content/dam/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4" }
 }).init();
</script>
```

集成只需从Experience Manager中删除视频嵌入代码并将其替换为交互式视频嵌入代码即可。 您可以在以下URL中看到结果。 虽然它显示页面上存在的交互式视频，但它尚未与现有的快速视图集成：

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-1.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-1.html)

## 将交互式视频与现有Quickview集成 {#integrating-an-interactive-video-with-an-existing-quickview}

>[!NOTE]
>
>此任务仅适用于独立Experience Manager Assets客户。

此过程的最后一步是将交互式视频与网站上使用的现有Quickview实施集成。 集成没有适用于所有情况的解决方案。 每个概览实施都是独特的。 因此，需要一种包含前端IT人员帮助的具体方法。

现有的概览实施通常表示在网页上发生的一系列相互关联的操作，顺序如下：

1. 用户在网站的用户界面中触发元素。
1. 前端代码根据步骤1中触发的用户界面元素获取概览URL。
1. 前端代码使用在步骤2中获取的URL发送AJAX请求。
1. 后端逻辑将相应的概览数据或内容返回给前端代码。
1. 前端代码加载概览数据或内容。
1. 前端代码可以选择将加载的概览数据转换为HTML呈现形式。
1. 前端代码显示一个模式对话框或面板，并在屏幕上为用户渲染HTML内容。

这些调用不代表网页逻辑可以从任意步骤中调用的独立公共API调用。 相反，它是一个链接调用，其中每个下一步都隐藏在上一步的最后阶段（回调）中。

在交互式视频替换步骤1或部分步骤2的同时，当用户选择交互式视频内的缩略图时，这种用户交互由观看者处理。 查看器会向网页返回一个事件，其中包含之前添加到Experience Manager的所有缩略图数据。

在此类事件处理程序中，前端代码执行以下操作：

* 收听交互式视频发出的事件。
* 根据缩略图数据构建概览URL。
* 触发从后端加载概览并在屏幕上呈现以供显示的过程。

此外，交互式视频查看器支持全屏操作模式。 用户通过选择缩略图而不离开全屏来触发快速视图。 要实现此功能，您需要更改前端代码，以便将“概览模式”对话框附加到查看器的容器中。 不要添加当查看器处于全屏模式时不可用的文档BODY或其他网页元素。 执行此作业的代码侦听一个或多个查看器回调，该回调在查看器加载到页面上后发送。

Experience Manager返回的嵌入代码已具有现成的事件处理程序。 如以下高亮显示的代码片段中所示，该代码会被注释掉：

```js {.line-numbers}
<style type="text/css">
 #s7interactivevideo_div.s7interactivevideoviewer{
   width:100%;
   height:auto;
 }
</style>
<script type="text/javascript" src="https://demos-pub.assetsadobe.com/etc/dam/viewers/s7viewers/html5/js/InteractiveVideoViewer.js"></script>

<div id="s7interactivevideo_div"></div>
<script type="text/javascript">
 var s7interactivevideoviewer = new s7viewers.InteractiveVideoViewer({
  "containerId" : "s7interactivevideo_div",
  "params" : {
   "serverurl" : "https://adobedemo62-h.assetsadobe.com/is/image",
   "contenturl" : "https://demos-pub.assetsadobe.com/",
   "config" : "/etc/dam/presets/viewer/Shoppable_Video_light",
   "config2": "/etc/dam/presets/analytics",
   "videoserverurl": "https://gateway-na.assetsadobe.com/DMGateway/public/demoCo",
   "interactivedata": "content/dam/_VTT/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4.svideo.vtt",
   "VideoPlayer.contenturl": "https://adobedemo62-h.assetsadobe.com/is/content",
   "asset" : "/content/dam/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4" }
 })
 /* // Example of interactive video event for quickview.
   s7interactivevideoviewer.setHandlers({
   "quickViewActivate": function(inData) {
     var sku=inData.sku; //SKU for product ID
    //To pass other parameter from the hotspot, you need to add custom parameter during the hotspot setup as parameterName=value
    loadQuickView(sku); //Replace this call with your quickview plugin
    //See your quickviewer plugin for the quickview call
    },
"initComplete":function() {
    //--- Attach quickview pop-up to viewer container so pop-up works in fullscreen mode ---
    var popup = document.getElementById('quickview_div'); // get custom quickview container
    popup.parentNode.removeChild(popup); // remove it from current DOM
    var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
    var inner_container = document.getElementById(sdkContainerId);
    inner_container.appendChild(popup); //Attach custom quickview container to viewer
    }
   });
 */
 s7interactivevideoviewer.init();
</script>
```

因此，只需取消上面高亮显示的代码片段的注释，并用特定网页特定的代码替换虚拟处理程序主体即可。

标准嵌入代码中存在两个默认回调处理程序： `quickViewActivate`和`initComplete`。 在查看器中选择缩略图时，`quickViewActivate`处理程序将触发。 使用它可将查看器与概览激活逻辑集成。 当查看器加载到页面时，`initComplete`处理程序只触发一次。 此处理程序用于调整概览对话框在网页DOM中的位置。

构建概观URL的过程与标识本主题前面介绍的缩略图变量的过程相反。 使用之前标识的概览URL示例，您可以了解在各种情况下概览URL的构建方式：

<table>
  <tbody>
  <tr>
    <td><p>单个SKU，在查询字符串中找到</p> </td>
    <td><code class="code">s7interactivevideoviewer.setHandlers(&lbrace;
      "quickViewActivate": function(inData) &lbrace;
      var quickViewUrl = "https://server/json?productId=" + inData.sku + "&amp;source=100";
      &rbrace;,
      &rbrace;);</code></td>
  </tr>
  <tr>
    <td>单个SKU，可在URL路径中找到</td>
    <td><code class="code">s7interactivevideoviewer.setHandlers(&lbrace;
      "quickViewActivate": function(inData) &lbrace;
      var quickViewUrl = "https://server/product/" + inData.sku;
      &rbrace;,
      &rbrace;);</code></td>
  </tr>
  <tr>
    <td><p>查询字符串中的SKU和类别ID</p> </td>
    <td><code class="code">s7interactivevideoviewer.setHandlers(&lbrace;
      "quickViewActivate": function(inData) &lbrace;
      var quickViewUrl = "https://server/quickView/product/?category=" + inData.categoryId + "&amp;prodId=" + inData.sku;
      &rbrace;,
      &rbrace;);</code></td>
  </tr>
  </tbody>
</table>

触发概观URL和激活概览面板的最后一步很可能需要IT部门的前端IT人员的协助。 他们最了解如何从适当的步骤准确触发概览实施，并拥有现成的概观URL。

您可以看到如何将这些步骤应用于演示网站，以将交互式视频与概览代码完全集成。 在本主题的前面部分，概观URL的结构标识如下：

```xml {.line-numbers}
/datafeed/$CategoryId$-$SKU$.json
```

通过使用通过查看器的代码传递给处理程序的`inData`对象中可用的`categoryId`和`sku`字段，可以轻松地在`quickViewActivate`处理程序中重构此URL，如下所示：

```js {.line-numbers}
var sku=inData.sku;
var categoryId=inData.categoryId;
var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
```

演示网站正在使用简单的`loadQuickView()`函数调用触发概览对话框。 此函数仅接受一个参数，即概览数据URL。 因此，集成交互式视频的最后一步是将以下代码行添加到`quickViewActivate`处理程序中：

```xml {.line-numbers}
loadQuickView(quickViewUrl);
```

最后，确保概览对话框已附加到查看器的容器元素。 嵌入代码默认值提供了实现此功能的示例步骤。 要获取对查看器容器元素的引用，您可以使用以下代码行：

```js {.line-numbers}
var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
var inner_container = document.getElementById(sdkContainerId);
```

其中`inner_container`是对由查看器管理的`DIV`元素的引用。 您希望该对话框成为该`DIV`的子级。

实际定位模态对话框元素并将其附加到上述容器的步骤因具体情况而异。 同样，您可以向熟悉您的概览实施所需的前端开发人员寻求帮助。

对于示例网站，概览模式对话框实施为`DIV`，其概览模式ID直接附加到文档`BODY`。 因此，将该对话框移动到查看器容器的代码简单如下：

```js {.line-numbers}
var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
var inner_container = document.getElementById(sdkContainerId);
inner_container.appendChild(document.getElementById("quickview-modal"));
```

完整的源代码如下所示：

```javascript {.line-numbers}
<style type="text/css">
 #s7interactivevideo_div.s7interactivevideoviewer{
   width:100%;
   height:auto;
 }
</style>
<script type="text/javascript" src="https://demos-pub.assetsadobe.com/etc/dam/viewers/s7viewers/html5/js/InteractiveVideoViewer.js"></script>

<div id="s7interactivevideo_div"></div>
<script type="text/javascript">
 var s7interactivevideoviewer = new s7viewers.InteractiveVideoViewer({
  "containerId" : "s7interactivevideo_div",
  "params" : {
   "serverurl" : "https://adobedemo62-h.assetsadobe.com/is/image",
   "contenturl" : "https://demos-pub.assetsadobe.com/",
   "config" : "/etc/dam/presets/viewer/Shoppable_Video_light",
   "videoserverurl": "https://gateway-na.assetsadobe.com/DMGateway/public/demoCo",
   "interactivedata": "content/dam/_VTT/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4.svideo.vtt",
   "VideoPlayer.contenturl": "https://adobedemo62-h.assetsadobe.com/is/content",
   "asset" : "/content/dam/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4" }
 })
 // Example of interactive video event for quickview.
   s7interactivevideoviewer.setHandlers({
   "quickViewActivate": function(inData) {
     var sku=inData.sku; //SKU for product ID
     var categoryId=inData.categoryId; //categoryId
    var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
    loadQuickView(quickViewUrl);
    },
   "initComplete":function() {
    //--- Attach quickview pop-up to viewer container so pop-up works in fullscreen mode ---
    var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
    var inner_container = document.getElementById(sdkContainerId);
    inner_container.appendChild(document.getElementById("quickview-modal"));
    }
   });
 s7interactivevideoviewer.init();
</script>
```

带有完全集成交互式视频的最终演示网站如下所示：

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-3.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-3.html)

## 使用Quickview创建自定义弹出窗口® {#using-quickviews-to-create-custom-pop-ups}

请参阅[使用概览创建自定义弹出窗口®](/help/assets/dynamic-media/custom-pop-ups.md)。
