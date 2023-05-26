---
title: 交互式视频
description: 了解如何在Dynamic Media中使用交互式视频和可购物视频。
contentOwner: Rick Brough
feature: Interactive Videos
role: User
exl-id: e4859223-91de-47a1-a789-c2a9447e5f71
source-git-commit: b37ff72dbcf85e5558eb3421b5168dc48e063b47
workflow-type: tm+mt
source-wordcount: '5966'
ht-degree: 3%

---

# 交互式视频{#interactive-videos}

您可以轻松地创建交互式视频（也称为可购物视频），以直接从视频推动转化。 客户与视频的互动发生在视频播放器旁的面板中，相关服务、信息或产品缩略图会根据视频中的功能滚动到视图中。 客户可以选择缩略图并直接链接到服务，或者将商品添加到购物车以便立即购买，或者链接到网页以获取更多信息。

视频结束时，会显示所有产品的视觉摘要，以推动行动号召。 客户还有另一个机会选择所需的项目。 可操作且具体的体验，如这些体验可增加客户参与度和转化率。

另请参阅 [交互式图像](/help/assets/dynamic-media/interactive-images.md).

## 交互式视频的实际操作 {#interactive-video-in-action}

要查看交互式购物视频的实际操作情况，请选择 [实时演示](https://landing.adobe.com/zh-Hans/na/dynamic-media/ctir-2755/live-demos.html)，滚动到 **[!UICONTROL 可购物媒体]** 标题，然后选择购物视频开始播放。

* 在播放期间，当视频中使用产品时，相同的产品会在右侧显示为缩略图。

* 要暂停视频并打开产品的概览，请选择缩略图。 例如，在视频中选择KitchenAid缩略图图像以体验混合器的360°旋转视图，或放大以查看混合器的详细信息。

另请参阅 [在Dynamic Media中使用交互式视频](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-interactive-video-feature-video-use.html#dynamic-media)

<!-- 

There was a link here that showed the video frame of an interactive video and when the reader selected the frame the video would play https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/AXIS/index.html. This now needs to call a new interactive video

-->

<!-- 

[A frame from an interactive, shoppable video](assets/chlimage_1-126.png) *A video frame capture from an interactive, shoppable video.*

-->

>[!NOTE]
>
>如果在用户选择缩略图图像时创建交互式视频以启动网页，则某些设备会阻止打开弹出网页。 在这种情况下，请更改设备上的弹出窗口阻止程序设置。 例如，在Apple iPhone 6上，转到 **[!UICONTROL 设置]** > **[!UICONTROL Safari]** > **[!UICONTROL 阻止弹出窗口]**，然后将控件滑动到 **[!UICONTROL 关闭]**. 现在，当您播放交互式视频并选择缩略图时，系统会提示您是否要打开弹出窗口。 如果接受，将打开网页。

### 观看如何创建交互式视频 {#watch-how-interactive-videos-are-created}

观看演练 [如何创建交互式视频](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveVideo)（7分30秒）。
(尽管视频演练使用Assets on Demand进行标记，但原则和步骤仍然适用于Adobe Experience Manager Assets中的交互式视频。)

### Adobe客户成功网络研讨会 {#adobe-customer-success-webinar}

此 [在Experience Manager Assets中使用交互式视频、链接共享和YouTube共享](https://adobecustomersuccess.adobeconnect.com/p1yxzdo4aec/) 网络研讨会教您如何使用交互式视频和其他功能将转化驱动型事件与视频营销内容联系起来。

## 快速入门：交互式视频 {#quick-start-interactive-videos}

以下分步工作流描述旨在帮助您在Dynamic Media中快速启动和运行交互式视频。

查找 **示例** 标题。 它包含一个基于此内容的简短教程 [启动演示网页 *不会* 尚未添加交互功能](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html).

**示例**&#x200B;有助于说明在您的网站上集成交互式视频的步骤。

完成最后一个示例部分中的教程后， [您的最终演示网页中会以这种方式显示完全集成的交互式视频](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-3.html).

交互式视频步骤：

1. **（可选）标识概览变量**  — 首先确定现有Quickview实施使用的动态变量。 在创建交互式视频时，可使用变量将产品缩略图映射到相应的产品概览。 参见 [（可选）标识概览变量](#optional-identifying-quickview-variables).
   **仅当满足以下所有条件时，才需要执行此步骤：**
   * 要通过触发到快速视图来向视频添加交互性。
   * 您实施的Experience Manager可以 *非* 使用电子商务集成框架，将产品数据从任何电子商务解决方案(如IBM®WebSphere®Commerce、Elastic Path、SAP Hybris或Intershop)提取到Experience Manager中。

1. **（可选）创建交互式视频查看器预设**  — 自定义组成播放器的各种组件的外观和行为，例如视频洗刷和交互式缩略图。
如果您打算使用现成的交互式视频查看器预设，则无需创建自己的交互式视频查看器预设 `Shoppable_Video_Light` 或 `Shoppable_Video_Dark` 而是。
参见 [创建查看器预设](/help/assets/dynamic-media/managing-viewer-presets.md#creating-a-new-viewer-preset) （可选）和 [创建交互式查看器预设的特殊注意事项](/help/assets/dynamic-media/managing-viewer-presets.md#special-considerations-for-creating-an-interactive-viewer-preset).

1. **上传视频及其相关图像资产**  — 上传要使其成为交互式内容的视频和相关图像。
参见 [上传视频及其关联的缩略图资产](#uploading-a-video-and-its-associated-thumbnail-assets).

   >[!NOTE]
   >
   >尚不支持MXF视频格式用于Dynamic Media中的交互式视频。

1. **向视频添加交互性**  — 向视频添加一个或多个时间段。 然后，关联这些时间段中的图像缩略图。 将每个图像缩略图分配给操作，例如超链接、概览或体验片段。
(如果您的交互式内容包含具有相对URL的链接，尤其是指向Experience Manager Sites页面的链接，则无法使用基于URL的链接方法。)
通过发布交互式视频资产来完成。 发布操作将创建您最终复制并应用于网站登陆页面的嵌入代码或URL。 参见 [向视频添加交互性](#adding-interactivity-to-your-video).
参见 [发布资产](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

1. **以Experience Manager将交互式视频添加到您的网站或您的网站**  — 如果您使用Experience Manager Sites或eCommerce，或者同时使用两者，请将交互式视频添加到Experience Manager的网页中。 将交互式媒体组件拖动到页面上。 参见 [将Dynamic Media资源添加到页面](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).
使用嵌入代码或URL将交互式视频与网站体验集成。 参见 [将交互式视频与您的网站集成](#integrating-an-interactive-video-with-your-website).
如果您使用的是第三方WCM（Web内容管理器），则必须将新的交互式视频与网站上使用的现有Quickview实施集成。 参见 [将交互式视频与现有Quickview集成](#integrating-an-interactive-video-with-an-existing-quickview).
   [将Dynamic Media资源添加到页面](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)

## （可选）标识概览变量 {#optional-identifying-quickview-variables}

>[!NOTE]
>
>仅当满足以下条件时，才需要此任务：
>
>* 要通过触发到快速视图来向视频添加交互性。
>* 您实施的Experience Manager可以 *非* 使用电子商务集成框架，将产品数据从任何电子商务解决方案(如IBM®WebSphere®Commerce、Elastic Path、SAP Hybris或Intershop)提取到Experience Manager中。 <!-- See [eCommerce concepts in Experience Manager Assets](/help/sites-administering/concepts.md).-->
>
如果您的Experience Manager实施使用的是电子商务，则可以跳过此任务并继续执行下一个任务。

首先，标识现有概览实施使用的动态变量，以便您可以在交互式视频创建过程中将产品缩略图映射到相应的产品概观。

向视频添加时间区段时，需要为添加到区段的每个缩略图分配一个SKU（库存单位）和任何其他变量。 此类变量稍后用于显示正确的概览产品。

正确标识哪些变量是唯一触发产品概览所必需的，这一点很重要。

有时，咨询负责现有Quickview实施的IT专家就足够了。 他们可能会知道系统中标识概览的最小数据集。 但是，可以简单地分析前端代码的现有行为。

大多数概览实施都使用以下范例：

* 用户在网站上激活用户界面元素。例如，选择“概览”按钮。
* 如果需要，网站会向后端发送Ajax请求以加载概览数据或内容。
* 概览数据将转换为内容，以便在网页上呈现。
* 最后，前端代码在屏幕上以可视方式呈现此类内容。

因此，方法是访问实施Quickview的现有网站的不同区域。 然后触发Quickview，并获取网页发送的Ajax URL，以加载Quickview数据或内容。

通常，您无需使用任何专门的调试工具。 现代Web浏览器的功能是Web检查器，这些检查器能够完成适当的工作。 以下是一些包含Web检查器的Web浏览器示例：

* 要在Google Chrome中查看所有传出的HTTP请求，请按 **F12** (Windows®)或 **Command+Options+I** (Mac)以打开“开发人员工具”面板，然后选择 **网络** 选项卡。

* 在Firefox中，您可以通过按 **F12** (Windows®)或 **Command+Option+I** (Mac)并使用其 **[!UICONTROL Net]** 选项卡，或者可以使用内置的检查器工具及其“网络”选项卡。

* 在Internet Explorer中，通过按 **F12**.

在浏览器中打开网络监视功能时，会在页面上触发概览。

现在，请在网络日志中找到Quickview Ajax URL，并复制记录的URL以供将来分析。 通常，在触发概览时，会向服务器发送大量请求。 通常，快速视图Ajax URL是列表中的前几个之一。 它具有复杂的查询字符串部分或路径，并且其响应MIME类型为 `text/html`， `text/xml`，或 `text/javascript`.

在此过程中，请务必访问网站的不同区域，以及不同的产品类别和类型。 原因是概观URL具有给定网站类别共有的部分，但只有在访问网站的其他区域时才更改。

最简单的情况是，概览URL中的唯一变量部分是产品SKU。 在这种情况下，产品SKU值是向Experience Manager交互式视频中的时间段添加缩略图所需的唯一数据段。

但是，在复杂的情况下，除了产品SKU之外，快速视图URL还具有不同的变化元素，例如类别ID和颜色代码。 在这种情况下，每个此类元素在Experience Manager的缩略图数据定义中都将成为单独的变量。

请考虑以下概观URL示例及其生成的缩略图变量：

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
    </ul> <p>URL中的唯一变量部分是 <code>productId=</code> 查询字符串参数，它显然是一个SKU值。 因此，缩略图只需要使用如下值填充的SKU字段 <strong><code>866558</code></strong>， <strong><code>1196184</code></strong>， <strong><code>1081492</code></strong>， <strong><code>1898294</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>单个SKU，可在URL路径中找到。</p> </td>
    <td><p>记录的概览URL包括：</p>
    <ul>
      <li><p><code>https://server/product/6422350843</code></p> </li>
      <li><p><code>https://server/product/1607745002</code></p> </li>
      <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>变量部分位于路径的最后部分，它将成为Experience Manager缩略图的SKU值： <strong><code>6422350843</code></strong>， <strong><code>1607745002</code></strong>， <strong><code>0086724882</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>查询字符串中的SKU和类别ID。</p> </td>
    <td><p>记录的概览URL包括：</p>
    <ul>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>在这种情况下，URL包含两个不同的部分。 SKU存储在 <code>prodId</code> 参数和类别ID存储在 <code>category=</code> 参数。</p> <p>因此，缩略图定义是对。 即，一个SKU值和一个名为的额外变量 <code>categoryId</code>. 生成的对如下所示：</p>
    <ul>
      <li>SKU是 <code>305466</code> 和 <code>categoryId</code> 是 <code>1100004</code></li>
      <li>SKU是 <code>310181</code> 和 <code>categoryId</code> 是 <code>1100004</code></li>
      <li>SKU是 <code>308706</code> 和 <code>categoryId</code> 是 <code>1740148</code></li>
    </ul> <p> </p> </td>
  </tr>
  </tbody>
</table>

**示例**

将以上方法应用于示例网站后，您的网页具有多个产品缩略图，每个产品缩略图都有一个“查看更多”按钮：

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

查看服务器调用时，特定于产品的信息仅显示在请求路径中。 您还会注意到根本未使用查询字符串，并且涉及两种不同类型的数据段：

* 第一种是蜡烛、靠垫、家具和玻璃器具。 您可以将此区段命名为“产品类别”。
* 第二种是产品代码，如233916597。 您可以假设它是“产品SKU”。

根据此信息，整个概览URL具有以下模式：

`/datafeed/$categoryId$-$SKU$.json`

基于此类分析，可以得出以下结论：对于缩略图，可以使用以下两个变量： `categoryId` 和 `SKU`.

您现在可以上传视频及其关联的缩略图资产。

## （可选）创建交互式视频查看器预设 {#optional-creating-an-interactive-video-viewer-preset}

如果要使用默认的、现成的交互式视频查看器预设类型，可以跳过此任务并继续执行下一个任务 `Shoppable_Video_dark` 或 `Shoppable_Video_light`.

在创作环境中选择缩略图时，将显示“概观”对话框的预览。

![chlimage_1-21](assets/chlimage_1-127.png)

您可以选择创建自己的自定义交互式视频查看器预设。 您可以确定视频播放器的样式、交互式缩略图以及视频末尾显示的缩略图网格视图等。

交互式视频查看器预设可正确呈现视频以及您添加的所有时间轴区段。 在“预览”模式下选择产品缩略图时，它还会使用默认概览示例，以便您可以在发布之前测试其交互性。

保存查看器预设后，“查看器预设”页面中的查看器预设状态将自动设置为 **开**。此状态表明查看器预设在 Dynamic Media 组件中可见，预览视频时也可见。另请确保手动发布新查看器预设。

参见 [创建查看器预设](/help/assets/dynamic-media/managing-viewer-presets.md#creating-a-new-viewer-preset) 创建自己的交互式视频查看器预设。

## 上传视频及其关联的缩略图资产 {#uploading-a-video-and-its-associated-thumbnail-assets}

如果您已上传视频和缩略图资产，请转到 [向视频添加交互性](#adding-interactivity-to-your-video).

>[!NOTE]
尚不支持MXF视频格式用于Dynamic Media中的交互式视频。

如果您上传了错误的视频或图像，或者您想要删除不再需要的已上传视频或图像，请参阅 [删除资源](/help/assets/manage-digital-assets.md#delete-assets).

要上传视频及其关联的缩略图资产，请执行以下操作：

1. 将视频和相关联的缩略图资产上传到所需的一个或多个文件夹。

   参见 [上传资产](/help/assets/manage-digital-assets.md).
参见 [使用FTP作业计划上载资产](/help/assets/manage-digital-assets.md).

   现在，将交互性添加到您的视频。

## 向视频添加交互性 {#adding-interactivity-to-your-video}

您可以使用“创建交互式视频”页面上的就地可视编辑器将时间轴区段添加到视频中。

添加时间轴区段后，可在每个区段中添加缩略图图像。 对于您添加的每个缩略图，您都会对其应用操作。 例如，您可以将概览应用于缩略图，也可以为其分配超链接或体验片段。

参见 [体验片段](/help/sites-cloud/authoring/fundamentals/experience-fragments.md).

>[!NOTE]
将查看器嵌入体验片段时，不支持交互式视频中的社交媒体共享工具。 相反，您可以使用或创建没有社交媒体共享工具的查看器预设。 通过此类查看器预设，您可以成功地将其嵌入体验片段中。

>[!NOTE]
如果您的交互式内容具有带相对URL的链接，尤其是指向Experience Manager Sites页面的链接，则无法基于URL的链接方法。

在当前创建/编辑会话期间，支持页面右上角附近的“撤消”和“重做”选项。

保存交互式视频后，该视频会立即打开并预览。 从该位置，您可以选择交互式视频查看器预设并播放视频，以查看向客户显示的相应内容的大致呈现形式。

**要在视频中添加交互性，请执行以下操作：**

1. 在Assets视图中，导航到您上传并想要使其成为交互式视频的视频。
1. 执行下列操作之一：

   * 将鼠标悬停在图像上，然后选择 **[!UICONTROL 选择]** （复选标记图标）。 在工具栏上，选择 **[!UICONTROL 编辑]**.

   * 将鼠标悬停在图像上，然后选择 **[!UICONTROL 更多操作]** （三个圆点图标） **[!UICONTROL >编辑]**.

   * 要在“详细信息视图”页面中将其打开，请选择图像。 在工具栏上，选择 **[!UICONTROL 编辑]**.

1. 在“创建交互式视频”页面上，执行以下任一操作：

   * 要开始播放视频，请选择 **[!UICONTROL 播放]** 按钮。 查看要突出显示的特定产品、服务或详细信息时，选择 **[!UICONTROL 添加区段]** 工具栏上。 重复此步骤，直到视频结束。

      对于您添加的每个时间段，您可以为其分配一个或多个缩略图图像。 然后，您可以将这些缩略图链接到可供客户购买的快速查看产品页面，或链接到网页，以了解更多信息。

   * 要开始播放视频，请选择 **[!UICONTROL 播放]** 按钮。 查看要突出显示的特定产品、服务或详细信息时，选择 **[!UICONTROL 暂停]**. 选择 **[!UICONTROL 添加区段]**.

      在时间轴上您要添加区段的各个点继续播放和暂停视频，直到视频结束。

1. （可选）将栏拖到 **[!UICONTROL 时间轴范围滑块]** 左键放大或右键缩小。 通过此类操作，可控制您看到的已添加区段的详细信息量。

   ![chlimage_1-22](assets/chlimage_1-128.png)

   根据视频的长度，“区段持续时间”默认为以下值：

   <table>
      <tbody>
        <tr>
        <td><strong>如果视频长度为……</strong></td>
        <td><strong>“区段持续时间”设置默认为……</strong></td>
        </tr>
        <tr>
        <td>3分钟或更长</td>
        <td>60 秒</td>
        </tr>
        <tr>
        <td>2-3分钟</td>
        <td>30 秒</td>
        </tr>
        <tr>
        <td>1-2 分钟</td>
        <td>20秒<br /> </td>
        </tr>
        <tr>
        <td>30-60秒</td>
        <td>10 秒</td>
        </tr>
        <tr>
        <td>30秒或更短</td>
        <td>5 秒</td>
        </tr>
      </tbody>
    </table>

   视频时间轴使用的屏幕面积与它可用的屏幕面积相同。 因此，在调整浏览器大小时，您添加的区段将保持其正确的宽度。

   举例来说，以下三个屏幕截图使用的是同一视频。 请注意，每个区段的宽度会根据“时间轴缩放”设置而变化。

   ![chlimage_1-23](assets/chlimage_1-129.png)

   屏幕快照A

   上面的屏幕快照A显示了29秒的产品视频的默认视图。 时间轴刻度默认设置为5秒。

   ![chlimage_1-130](assets/chlimage_1-130.png)

   屏幕快照B

   在上面的屏幕快照B中，“时间轴缩放”滑块从5秒的默认值拖动到3秒。 请注意，各个时间轴比例时间戳现在均以3秒为间隔进行设置。

   ![chlimage_1-25](assets/chlimage_1-131.png)

   屏幕快照C

   在上面的屏幕快照C中，“时间轴缩放”设置已移动到8秒。 请注意包含产品缩略图的区段如何缩减。 如果您有一个长视频，并且希望能够查看更多通常适合页面宽度的区段的概述，则通过此方式缩小将会很有用。

1. （可选）执行以下任一操作：

   * 调整区段的开始时间和结束时间。

      选择一个区段，然后拖动前导蓝色椭圆或尾随蓝色椭圆以分别调整开始时间或结束时间。 显示的视频帧会根据您的调整移动到视频中的适当时间。 时间线区段的移动根据时间线中的任何相邻区段而受到限制。 允许的最短段时间为一秒。

      使用以下导航快捷方式快速检查和微调视频区段：

      * 要直接搜索到该区段开头的视频，请选择开头的蓝色椭圆。
      * 要直接搜索到视频区段末尾的视频，请选择末尾的蓝色椭圆。
      * 要将视频播放返回到该区段的开头，请选择整个区段。

   ![chlimage_1-26](assets/chlimage_1-132.png)

   重新定位时间线区段的结尾

   * 删除区段

      选择时间轴上的最后一个区段，然后在工具栏上，选择 **[!UICONTROL 删除区段]**. 如果选择了两个或多个区段，则“删除区段”功能将被禁用。

      您只能删除最后一个区段。 例如，如果要删除时间轴上的所有区段，则必须始终选择最后一个区段，然后选择 **[!UICONTROL 删除区段]**.


1. 选择要与一个或多个缩略图图像关联的时间段。
1. 在视频的右侧，选择 **[!UICONTROL 内容]** 选项卡。
1. 在内容选项卡下，选择 **[!UICONTROL 选择资源]**，然后浏览并选择要用于视频的所有图像资产。 选定的资源会添加到“内容”选项卡的资源选择器面板中。

1. 在“内容”选项卡下方的资源选择器中，执行以下任一操作：

   <table>
      <tbody>
        <tr>
        <td>要将缩略图与选定的时间线段相关联，请执行以下操作</td>
        <td><p>在右侧的资源选择器面板中选择图像。</p> <p>您可以向时间线区段添加任意数量的缩略图。 对于您选择的每个图像，资产选择器中的图像上方都会显示一个复选标记。</p> </td>
        </tr>
        <tr>
        <td>要从所选时间线段删除缩略图，请执行以下操作</td>
        <td><p>执行以下任一操作：</p>
          <ul>
          <li>在资产选择器面板中，选择带有复选标记的图像以取消选择它。 图像资产将从时间轴区段中删除。<br /> </li>
          <li>在选定的时间轴区段中，选择一个图像，然后在工具栏上，选择 <strong>删除产品</strong>.</li>
          </ul> </td>
        </tr>
      </tbody>
    </table>

   ![资产选取器](assets/chlimage_1-133.png)

   在资产选择器面板中选择图像，可将其添加到选定的时间线区段。

1. 选择一个时间轴区段中的单个缩略图图像，然后选择 **[!UICONTROL 操作]** 选项卡。
1. 执行以下任一操作：
   <table> 
    <tbody> 
      <tr> 
      <td>要将选定的缩略图图像与概览相关联，请执行以下操作</td> 
      <td><p>在Action Type下，选择 <strong>概览</strong>.</p> <p>如果您是Experience Manager Sites和电子商务客户：</p> 
       <ul> 
       <li>请注意，“SKU值”文本字段已预先填充了所选产品的SKU（库存单位）。 SKU是您提供的每个不同产品或服务的唯一标识符。 当图像与Experience Manager商业中的产品关联时，将自动填充此字段。</li> 
       <li>如果预填充的SKU不正确，请选择“产品选取器”图标（放大镜）以打开“选择产品”页面。 选择要使用的产品，然后选择页面右上角的复选标记。 您将返回到交互式视频编辑器。</li> 
       </ul> <p> 如果您是 <em>非</em> Experience Manager Sites或电子商务客户</p> 
       <ul> 
       <li>参见 <a href="/help/assets/dynamic-media/carousel-banners.md#identifying-hotspot-and-image-map-variables">标识热点变量</a>. 必须定义这些变量。</li> 
       <li>默认情况下，此SKU字段使用图像资源的文件名（不带扩展名）。 如果您对基于SKU的文件遵循标准命名约定，则此字段通常不需要任何额外的编辑。 </li> 
       <li>否则，请编辑默认值并输入正确的SKU值。 在“SKU值”文本字段中，键入产品的SKU（库存单位），它是您提供的每个不同产品或服务的唯一标识符。 输入的SKU值会自动填充概览模板的变量部分，以便系统知道将选定的图像与特定SKU的概览相关联。</li> 
       </ul> <p>（可选）如果概览中还有其他必须用来进一步标识产品的变量，请选择 <strong>添加通用变量</strong>. 在文本字段中，指定一个额外的变量。 例如， <code>category=Womens</code> 是添加的变量。</p> <p> </p> </td> 
      </tr> 
      <tr> 
      <td>将选定的缩略图图像与超链接相关联</td> 
      <td><p>在Action Type下，选择 <strong>超链接</strong>，然后执行以下操作之一：</p> 
       <ul> 
       <li>如果您是Experience Manager Sites客户，请选择“站点选择器”图标（文件夹）以导航到网页。 如果您的交互式内容具有带相对URL的链接，尤其是指向Experience Manager Sites页面的链接，则无法基于URL的链接方法。</li> 
       <li>如果您是独立Dynamic Media客户，请在HREF文本字段中指定链接网页的完整URL路径。</li> 
       </ul> <p>请确保指定是在新的浏览器选项卡中还是在当前选项卡中打开链接。</p> </td> 
      </tr> 
      <tr> 
      <td>将选定的缩略图图像与体验片段关联</td> 
      <td><p>在Action Type下，选择 <strong>体验片段</strong>，然后执行以下操作：<p> 
       <ul> 
       <li>如果您是Experience Manager Sites客户，请选择“搜索”图标（放大镜）以打开“体验片段”页面。 选择要使用的体验片段，然后选择 <strong>要返回到上一页的“操作”面板，请选择 </strong>页面右上角的。<br /> 参见 <a href="/help/sites-cloud/authoring/fundamentals/experience-fragments.md">体验片段</a>.</li> 
      </ul> 
       <ul> 
       <li>指定视频中显示的体验片段的宽度和高度。</li>
       </ul><strong>注释</strong>：将查看器嵌入体验片段时，不支持交互式视频中的社交媒体共享工具。 相反，您可以使用或创建没有社交媒体共享工具的查看器预设。 通过此类查看器预设，您可以成功地将其嵌入体验片段中。</p></tr>&lt; 
      <tr> 
      <td>要编辑已分配给缩略图图像的操作</td> 
      <td>在时间轴区段内，选择一个文本标签右侧具有链链接的缩略图图像。 链链接表示为其分配了操作。 要进行更改，请选择 <strong>操作</strong> 选项卡。</td> 
      </tr> 
      <tr> 
      <td>更改缩略图图像的文本标签</td> 
      <td><p>默认情况下，文本标签使用缩略图图像的 <code>Title</code> 元数据字段。 如果 <code>Title</code> 不存在，则改用缩略图图像的文件名，但不使用扩展名。</p> <p>要更改缩略图图像的文本标签，请在 <strong>操作 </strong>选项卡，在显示的图像资源正下方，输入所需的文本。 请参阅下图。</p> <p>新文本标签仅由视频播放器本身以及在时间轴区段中显示的缩略图文本使用。 标签更改不会影响缩略图图像的标题元数据字段及其文件名。</p> </td> 
      </tr> 
      <tr> 
      <td>还原更改</td> 
      <td>在页面的右上角附近，选择 <strong>撤消</strong> 或 <strong>重做</strong>.</td> 
      </tr> 
    </tbody> 
   </table>

   ![experiencefragment_interactivevideos](assets/experiencefragment_interactivevideos.png)

   新的文本标签将添加到缩略图图像。

1. 执行下列操作之一：

   * 重复步骤6-11以在视频中向时间轴区段添加更多缩略图图像。
   * 继续执行可选步骤13。

1. （可选）执行以下任一操作：

   * **[!UICONTROL 合并区段]**  — 您可以将两个相邻的区段（无论是否为其分配了产品缩略图）合并到一个区段中。

      在时间轴上，选择要合并为一个的一个或多个连续区段。 下图中的两个选定区段上没有蓝色椭圆拖动手柄。

      选择 **[!UICONTROL 合并区段]** 工具栏上。
   ![chlimage_1-134](assets/chlimage_1-134.png)

   将两个选定的5秒区段合并为1个10秒区段。

   * **[!UICONTROL 拆分区段]**  — 您可以将单个区段划分为两个等时区段。 如果已有产品缩略图分配给区段，则这些缩略图将合并到左侧区段中。

      在时间轴上，选择要分成两半的区段，然后选择 **[!UICONTROL 拆分区段]** 工具栏上。

      选择两个或多个区段会禁用 **[!UICONTROL 拆分区段]** 功能。
   ![chlimage_1-135](assets/chlimage_1-135.png)

   将所选的10秒区段拆分为两个区段，每个区段长5秒。

1. 在右上角附近 **[!UICONTROL 创建交互式视频]** 页面，显示当前所选与视频一起使用的查看器预设的名称。 要选择其他查看器预设，请选择名称。

   例如， `Shoppable_Video_light` 查看器预设允许您使用视频旁边的白色显示区域播放视频。 显示区域是播放期间显示可选缩略图图像的位置。 此 `Shoppable_Video_dark` 查看器预设允许您使用视频旁边的黑色显示区域播放视频。

   如果您创建了自己的交互式视频查看器预设，则可以在从中进行选择的预设列表中看到该预设。

   完成后，选择 **[!UICONTROL 保存]**.

   >[!NOTE]
   在保存交互式视频时，会自动保存 `.vtt` 一个关联的文件。 此 `.vtt` 文件将保存到 `_VTT` 根目录下的文件夹 **[!UICONTROL 资产]**. 要在网站上正确播放交互式视频，必须填写文件和文件夹。 因此，请勿移动、编辑或删除文件夹 `_VTT` 或其内容。

1. 发布交互式视频。 发布操作将创建您最终复制并粘贴到网站体验中的嵌入代码或URL。

   如果添加了与快速视图的交互，则仅使用嵌入代码；如果添加了与超链接网页的交互，则还可以使用已发布的URL。 但是，请注意，如果您的交互式内容包含具有相对URL的链接，尤其是指向Experience Manager Sites页面的链接，则无法基于URL进行链接。

   参见 [发布资产](publishing-dynamicmedia-assets.md).

   >[!NOTE]
   要发布带有快速查看功能的可购物视频，请确保您还分别从商务区发布视频的每个相关图像资产。

   在添加时间轴区段并发布交互式视频后，便可以将其添加到现有网站登陆页面。 参见 [将交互式视频与您的网站集成](#integrating-an-interactive-video-with-your-website).

## 发布交互式视频资产 {#publishing-interactive-video-assets}

参见 [发布资产](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md) 以了解有关如何发布交互式视频资产的详细信息。

## 将交互式视频与您的网站集成 {#integrating-an-interactive-video-with-your-website}

在上传视频、向其添加时间轴区段并发布交互式视频后，现在即可将其添加到现有网站。

如果您是Experience Manager Sites客户，则可以通过将交互式媒体组件拖动到页面来添加交互式视频。 参见 [将Dynamic Media资源添加到页面](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

如果您是独立Experience Manager Assets客户，则可以手动将交互式视频添加到您的网站，如本节所述。

1. 复制发布的交互式视频的嵌入代码或URL。
参见 [在网页上嵌入视频查看器或图像查看器](/help/assets/dynamic-media/embed-code.md).
如果添加了与快速视图的交互，则仅使用嵌入代码；如果添加了与超链接网页的交互，则还可以使用已发布的URL。 但是，请注意，如果您的交互式内容包含具有相对URL的链接，尤其是指向Experience Manager Sites页面的链接，则无法基于URL进行链接。

1. 在目标网站的网页代码中，标识静态视频的位置。
1. 删除静态视频，并将代码替换为您从Experience Manager Assets中复制的嵌入代码或URL（按原样）。
复制的嵌入代码是为响应式环境设置的，因此会自动适合之前由静态视频占用的区域。

>[!NOTE]
此时，如果您只添加与超链接网页的交互，则操作已完成。
但是，如果添加了任何交互来触发快速视图，则交互式视频旁边的缩略图仅用于显示；它们尚未与现有的快速视图集成。 在这种情况下，您必须将交互式视频与网站上现有的快速视图集成。

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

集成就像删除视频嵌入代码并将其替换为Experience Manager中的交互式视频嵌入代码一样简单。 您可以在以下URL中看到结果。 虽然它显示页面上存在的交互式视频，但它尚未与现有的快速视图集成：

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-1.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-1.html)

## 将交互式视频与现有Quickview集成 {#integrating-an-interactive-video-with-an-existing-quickview}

>[!NOTE]
此任务仅适用于独立Experience Manager Assets客户。

此过程的最后一步是将交互式视频与网站上使用的现有Quickview实施集成。 集成没有适用于所有情况的解决方案。 每个概览实施都是唯一的。 因此，需要涉及前端IT人员帮助的具体方法。

现有的概览实施通常表示在网页上发生的一系列相互关联的操作，顺序如下：

1. 用户在网站的用户界面中触发元素。
1. 前端代码基于在步骤1中触发的用户界面元素获取概览URL。
1. 前端代码使用在步骤2中获取的URL发送AJAX请求。
1. 后端逻辑将相应的概览数据或内容返回到前端代码。
1. 前端代码加载概览数据或内容。
1. 前端代码可以选择将加载的概览数据转换为HTML表示形式。
1. 前端代码显示一个模式对话框或面板，并在屏幕上为最终用户渲染HTML内容。

这些调用不表示独立的公共API调用，网页逻辑可以从任意步骤调用这些API调用。 相反，它是一个链接调用，其中每个下一步都隐藏在上一步的最后阶段（回调）中。

在交互式视频替换步骤1和部分步骤2的同时，当用户选择交互式视频内的缩略图时，这种用户交互由查看器处理。 查看器会向网页返回一个事件，其中包含之前添加到Experience Manager中的所有缩略图数据。

在此类事件处理程序中，前端代码执行以下操作：

* 侦听交互式视频发出的事件。
* 根据缩略图数据构建概览URL。
* 触发从后端加载概览并在屏幕上呈现以进行显示的过程。

此外，交互式视频查看器支持全屏操作模式。 最终用户通过选择缩略图而不离开全屏来触发快速查看。 要实现此功能，您需要更改前端代码，以便将“概览模式”对话框连接到查看器的容器。 请勿添加当查看器处于全屏模式时不可用的文档BODY或其他某个网页元素。 执行此作业的代码侦听在查看器在页面上加载后发送的一个或多个查看者回调。

Experience Manager返回的嵌入代码已具有现成的事件处理程序。 如以下高亮显示的代码片段中所示，它被注释掉：

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
    //Please refer to your quickviewer plugin for the quickview call
    },
"initComplete":function() {
    //--- Attach quickview popup to viewer container so popup will work in fullscreen mode ---
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

因此，只需取消对上面高亮显示的代码片段的注释，并用特定于特定网页的代码替换虚拟处理程序主体即可。

标准嵌入代码中存在两个默认回调处理程序： `quickViewActivate` 和 `initComplete`. 此 `quickViewActivate` 在查看器中选择缩略图时会触发处理程序。 使用它可将查看器与概览激活逻辑集成。 此 `initComplete` 当查看器加载到页面中时，处理程序仅触发一次。 此处理程序用于调整概览对话框在网页DOM中的位置。

构建概观URL的过程与标识本主题前面介绍的缩略图变量的过程相反。 使用之前标识的概览URL示例，您可以查看在各种情况下概览URL的构建方式：

<table>
  <tbody>
  <tr>
    <td><p>单个SKU，在查询字符串中找到</p> </td>
    <td><code class="code">s7interactivevideoviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/json?productId=" + inData.sku + "&amp;source=100";
      },
      });</code></td>
  </tr>
  <tr>
    <td>单个SKU，可在URL路径中找到</td>
    <td><code class="code">s7interactivevideoviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/product/" + inData.sku;
      },
      });</code></td>
  </tr>
  <tr>
    <td><p>查询字符串中的SKU和类别标识</p> </td>
    <td><code class="code">s7interactivevideoviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/quickView/product/?category=" + inData.categoryId + "&amp;prodId=" + inData.sku;
      },
      });</code></td>
  </tr>
  </tbody>
</table>

触发概观URL和激活概览面板的最后一步很可能需要您IT部门的前端IT人员的协助。 他们最清楚如何从适当的步骤准确触发概览实施，拥有一个现成的概观URL。

您可以看到如何将这些步骤应用于演示网站，以将交互式视频与概览代码完全集成。 在本主题的前面部分，概观URL的结构标识如下：

```xml {.line-numbers}
/datafeed/$CategoryId$-$SKU$.json
```

可以在中轻松重构此URL `quickViewActivate` 处理程序使用 `categoryId` 和 `sku` 中的可用字段 `inData` 对象通过查看器的代码传递给处理程序，如下所示：

```js {.line-numbers}
var sku=inData.sku;
var categoryId=inData.categoryId;
var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
```

演示网站正在使用简单的 `loadQuickView()` 函数调用。 此函数仅接受一个参数，即概览数据URL。 因此，集成交互式视频的最后一步是将下面一行代码添加到 `quickViewActivate` 处理程序：

```xml {.line-numbers}
loadQuickView(quickViewUrl);
```

最后，确保概览对话框已附加到查看器的容器元素。 嵌入代码默认值提供了实现此功能的示例步骤。 要获取对查看器容器元素的引用，您可以使用以下代码行：

```js {.line-numbers}
var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
var inner_container = document.getElementById(sdkContainerId);
```

位置 `inner_container` 是对 `DIV` 由查看器管理的元素。 您希望该对话框成为其子项 `DIV`.

实际定位模态对话框元素并将其附加到上述容器的步骤因具体情况而异。 同样，您可以向熟悉您的概览实施所需的前端开发人员寻求帮助。

对于示例网站，概览模式对话框实施为 `DIV` 直接附加到文档的概览模式ID `BODY`. 因此，将该对话框移动到查看器容器的代码如下所示：

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
    //--- Attach quickview popup to viewer container so popup will work in fullscreen mode ---
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

参见 [使用Quickview创建自定义弹出窗口®](/help/assets/dynamic-media/custom-pop-ups.md).
