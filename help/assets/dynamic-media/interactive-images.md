---
title: 交互式图像
description: 了解如何在Dynamic Media中使用交互式图像。
contentOwner: Rick Brough
feature: Interactive Images
role: User
exl-id: 89eef5e6-d508-4f33-b54e-24d4df49f8c3
source-git-commit: b37ff72dbcf85e5558eb3421b5168dc48e063b47
workflow-type: tm+mt
source-wordcount: '4176'
ht-degree: 2%

---

# 交互式图像{#interactive-images}

通过将“可购物”热点拖放到图像上，您可以轻松使静态图像丰富并吸引客户体验。 可购物热点将有关产品或服务的其他信息与直接的销售点“添加到购物车”或“购买”功能相结合。 客户可以点按这些直接链接到产品或服务的热点，将其添加到购物车，或链接到网页。 此类直接体验可提高客户参与度和网站上的转化率。

以下是带有“概观”弹出窗口的可购物横幅。 用户通过在模型上点按圆或“热点”来激活概览。

![chlimage_1-152](assets/chlimage_1-368.png)

参见 [交互式图像正在起作用](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion-QVzoom/index2-shoppable.html) 在上图所示的网页上。

## 观看如何创建交互式图像横幅 {#watch-how-interactive-image-banners-are-created}

观看演练 [如何创建交互式图像横幅](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveCarouselBanner) （10分33秒）。 您还将了解如何预览、编辑和交付交互式图像横幅。

## 快速入门：交互式图像 {#quick-start-interactive-images}

以下分步工作流描述旨在帮助您在Adobe Experience Manager Assets中快速启动和运行交互式图像。

查找 **示例** 标题。 它包含一个基于的简短教程 [尚未添加交互式图像的网页示例](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html).



本教程有助于说明在您的网站上集成交互式图像的步骤。

交互式图像步骤：

1. **（可选）标识热点变量**. 如果您使用Adobe Experience Manager Assets和Dynamic Media独立，请标识在现有Quickview实施中使用的动态变量。 这样做可确保您在创建交互式图像时输入热点数据。 参见 [（可选）标识热点变量](#optional-identifying-hotspot-variables).
但是，如果您使用Experience Manager Sites或Experience Manager电子商务，或者同时使用两者，则无需执行此步骤。

1. **（可选）创建交互式图像查看器预设**. 自定义用于表示热点的图形图像。 如果您打算使用名为的现成交互式图像查看器预设，则无需创建自己的交互式图像查看器预设 `Shoppable_Banner` 而是。
参见 [（可选）创建交互式图像查看器预设](/help/assets/dynamic-media/managing-viewer-presets.md#creating-a-new-viewer-preset).

1. **上传图像横幅**. 上传要使其成为交互式图像的横幅。
参见 [上传图像横幅](#uploading-an-image-banner).

1. **将热点添加到图像横幅**. 将一个或多个热点添加到图像横幅。 将每个项目与操作（如超链接、概览或体验片段）关联。 添加热点后，将通过发布交互式图像来完成此任务。
参见 [将热点添加到图像横幅](#adding-hotspots-to-an-image-banner).
参见 [预览交互式图像](#optional-previewing-interactive-images)  — 可选。 如果需要，您可以查看可购物横幅的表示形式并测试其交互性。
参见 [发布资产](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md) 以了解有关如何发布交互式图像资源的详细信息。

1. **以Experience Manager将交互式图像添加到您的网站或您的网站**. 如果您使用“站点”或“电子商务”，或者同时使用两者，则可以直接将交互式图像添加到Experience Manager的网页。 将交互式媒体组件拖动到页面上。 参见 [将Dynamic Media资源添加到页面](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).
如果您单独使用Experience Manager Assets和Dynamic Media，请复制您网站上的嵌入代码。 然后，将其与您现有的概览集成。 参见 [将交互式图像与您的网站集成](#integrating-an-interactive-image-with-your-website).
如果您使用第三方WCM （Web内容管理器），请将新的交互式视频与网站上使用的现有快速视图集成。 参见 [将交互式图像与现有的概览集成](#integrating-an-interactive-image-with-an-existing-quickview).

## （可选）标识热点变量 {#optional-identifying-hotspot-variables}

>[!NOTE]
>
>仅当满足以下条件时，才需要此任务：
>
>* 要通过触发到快速视图来向图像添加交互性。
>* 您实施的Experience Manager可以 *非* 使用电子商务集成框架将产品数据从任何电子商务解决方案拉入Experience Manager。 此类解决方案包括IBM® WebSphere® Commerce、Elastic Path、SAP Hybris或Intershop。
>
如果您的Experience Manager实施使用的是电子商务，则可以跳过此任务并继续执行下一个任务。

首先，标识由您现有的概览实施使用的动态变量，以便您可以输入热点数据来创建交互式图像。

在Experience Manager Assets中将热点添加到横幅图像时，请分配SKU（库存单位）。 SKU是您提供的每个不同产品或服务的唯一标识符。 此外，还可以向每个热点添加任何额外的可选变量。 此类热点变量稍后用于匹配热点与概览内容。

正确标识要与热点数据关联的变量的数量和类型非常重要。 添加到横幅图像的每个热点都必须携带足够的信息，以便明确标识现有后端系统中的产品。

有不同的方法可标识一组用于热点数据的变量。

有时，咨询负责现有Quickview实施的IT专家就足够了。 此类人员可能知道在系统中标识概览所需的最小数据集。 但是，也可以简单地分析前端代码的现有行为。

大多数概览实施都使用以下范例：

* 用户在网站上激活用户界面元素。例如，选择“概览”按钮。
* 如果需要，网站会向后端发送Ajax请求以加载概览数据或内容。
* 概览数据将转换为内容，以便在网页上呈现。
* 最后，前端代码在屏幕上以可视方式呈现此类内容。

然后，方法是访问实施概览功能的现有网站的不同区域。 然后触发概览并获取网页发送的Ajax URL，以加载概览数据或内容。

通常，您无需使用任何专门的调试工具。 现代Web浏览器的功能是Web检查器，这些检查器能够完成适当的工作。 以下是一些包含Web检查器的Web浏览器示例：

* 要在Google Chrome中查看所有传出的HTTP请求，请按F12打开“开发人员工具”面板，然后选择“网络”选项卡。
在Mac上，按Command + Option + I以打开“开发人员工具”面板，然后选择“网络”选项卡。

* 在Firefox中，您可以通过按F12并使用其Net选项卡来激活Firebug插件。 或者，也可以使用内置的检查器工具及其“网络”选项卡。
在Mac上，按Command + Option + I以打开“开发人员工具”面板，然后选择“检查器”选项卡。

在浏览器中打开网络监视功能时，会在页面上触发概览。

现在，请在网络日志中找到Quickview Ajax URL，并复制记录的URL以供将来分析。 通常，在触发概览时，会向服务器发送大量请求。 通常，快速视图Ajax URL是列表中的前几个之一。 它具有复杂的查询字符串部分或路径，并且其响应MIME类型为 `text/html`， `text/xml`，或 `text/javascript`.

在此过程中，请务必访问网站的不同区域，以及不同的产品类别和类型。 原因是概观URL可以包含给定网站类别通用的部分。 但是，只有在访问网站的其他区域时，这些变量才会更改。

最简单的情况是，概览URL中的唯一变量部分是产品SKU。 在这种情况下，SKU值是向横幅图像添加热点所需的唯一数据段。

但是，在复杂情况下，除了SKU之外，快速视图URL还有不同的变化元素。 例如，变化的元素可能包括类别ID、颜色代码和大小代码。 在这种情况下，在Experience Manager Assets的可购物交互式图像功能中，每个元素在热点数据定义中都是一个单独的变量。

请考虑以下概观URL示例及其生成的热点变量：

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
    </ul> <p>URL中的唯一变量部分是productId=查询字符串参数的值，它显然是一个SKU值。 因此，热点只需要使用如下值填充的SKU字段 <strong><code>866558</code></strong>， <strong><code>1196184</code></strong>， <strong><code>1081492</code></strong>， <strong><code>1898294</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>单个SKU，可在URL路径中找到。</p> </td>
    <td><p>记录的概览URL包括：</p>
    <ul>
      <li><p><code>https://server/product/6422350843</code></p> </li>
      <li><p><code>https://server/product/1607745002</code></p> </li>
      <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>变量部分位于路径的最后一部分，它成为热点的SKU值： <strong><code>6422350843</code></strong>， <strong><code>1607745002</code></strong>， <strong><code>0086724882</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>查询字符串中的SKU和类别ID。</p> </td>
    <td><p>记录的概览URL包括：</p>
    <ul>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>在这种情况下，URL包含两个不同的部分。 SKU存储在 <code>prodId</code> 参数和类别ID<code></code> 存储在 <code>category=</code> 参数。</p> <p>因此，热点定义是对的。 即，一个SKU值和一个名为的额外变量 <code>categoryId</code>. 生成的对如下所示：</p>
    <ul>
      <li><p>SKU是 <strong><code>305466</code></strong> 和 <code>categoryId</code> 是 <code>1100004</code>.</p> </li>
      <li><p>SKU是 <strong><code>310181</code></strong> 和 <code>categoryId</code> 是 <strong><code>1100004</code></strong>.</p> </li>
      <li><p>SKU是 <strong><code>308706</code></strong> 和 <code>categoryId</code> 是 <strong><code>1740148</code></strong>.</p> </li>
    </ul> <p> </p> </td>
  </tr>
  </tbody>
</table>

**示例**

您可以将上述三个示例中使用的相同方法应用于 [演示网页](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html).

演示网页具有多个产品缩略图，每个产品缩略图都有一个标记为“查看更多”的“快速查看”按钮。 在Web浏览器的调试工具仍处于激活状态的情况下，选择每个按钮并记下记录的概览URL。 在激活页面上可用的所有四个产品快速视图后，您会获得向后端发出的以下快速视图请求列表：

* `/datafeed/Male-Windbreaker.json`
* `/datafeed/Male-SimpleHenley.json`
* `/datafeed/Male-CamoPullover.json`
* `/datafeed/Female-QuiltedDownJacket.json`

查看服务器调用时，您可以看到特定于产品的信息仅显示在请求路径中。 您还会注意到根本未使用查询字符串，并且涉及两种不同类型的数据段：

* 第一种类型是“男性”或“女性”。 您可以将此区段命名为“产品类别”。
* 第二种类型是产品名称，例如CamoPullover，它可能是产品SKU。

根据此信息，整个概览URL具有以下模式：

`/datafeed/$categoryId$-$SKU$.json`

基于此类分析，您应使用 `categoryId` 和 `SKU` 用于热点。

您现在可以使用Experience Manager Assets中的可购物交互式图像功能，上传图像横幅并向其中添加热点。

## （可选）创建交互式图像查看器预设 {#optional-creating-an-interactive-image-viewer-preset}

您可以选择使用默认的现成交互式图像查看器预设，其名称为 `Shoppable_Banner` Experience Manager Assets随附的。 或者，您也可以创建自己的自定义查看器预设以用于交互式图像。

创建自定义交互式图像查看器预设时，可以确定图像横幅上的热点外观。 在创建查看器预设时，您可以选择使用来自预定义图像库的热点图形。

保存查看器预设后，查看器预设将在Experience Manager Assets中的“查看器预设”列表页面上自动激活（打开）。 这项功能意味着在交互式媒体组件中以及查看资产时，都可看到该资产。 但是，到 *deliver* 具有此查看器预设的交互式横幅， *发布* 您的查看器预设也一样。 此规则适用于自定义或现成的查看器预设。

**要创建交互式图像查看器预设，请执行以下操作：**

1. 在左边栏中，转到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 查看器预设]**.
1. 在页面的右上角附近，点按 **[!UICONTROL 创建]**.
1. 在“新建查看器预设”对话框中，键入用于描述交互式横幅查看器预设的名称。

   保存后，此标题将显示在“查看器预设”列表页面中。

1. 在“富媒体类型”下拉菜单中，选择&#x200B;**[!UICONTROL 交互式图像]**。
1. 选择&#x200B;**[!UICONTROL 创建]**。
1. 在“编辑查看器预设”页面上，点按 **[!UICONTROL 外观]** 选项卡。
1. 执行下列操作之一：

   * 要上传您自己的要在图像中使用的热点图像，请点按资产选取器图标。 在“选择内容”页面中，导航到要使用的热点图像并将其选定。 选择右上角的复选标记图标。
   * 要选择预定义的热点图像，请点按热点库图标。 在热点库调色板上，点按要使用的热点图像。

1. 在页面的右上角附近，点按 **[!UICONTROL 保存]**.

   确保发布新的查看器预设。

   参见 [发布查看器预设](/help/assets/dynamic-media/managing-viewer-presets.md#publishing-viewer-presets).

   您现在可以上传图像横幅了。

## 上传图像横幅 {#uploading-an-image-banner}

如果您已上传要使用的图像，请前进到下一步， [将热点添加到图像横幅](#adding-hotspots-to-an-image-banner).

**上传图像横幅：**

1. 上传要使其成为交互式图像的横幅。

   参见 [正在上传资产](/help/assets/manage-digital-assets.md#uploading-assets).

   您现在可以将热点添加到图像横幅中；请参阅下面的下一个任务。

## 将热点添加到图像横幅 {#adding-hotspots-to-an-image-banner}

您可以使用“热点管理”页面上的编辑器将热点添加到图像横幅中。

添加热点时，可以将它们定义为概览弹出显示、超链接或体验片段。

参见 [体验片段](/help/sites-cloud/authoring/fundamentals/experience-fragments.md).

>[!NOTE]
将查看器嵌入体验片段时，不支持交互式图像中的社交媒体共享工具。 请改用或创建没有社交媒体共享工具的查看器预设。 通过此类查看器预设，您可以成功地将其嵌入体验片段中。

在当前创建/编辑会话期间，支持页面右上角附近的“撤消”和“重做”选项。

创建完交互式图像后，可以使用“预览”来查看向客户展示交互式图像的方式。

参见 [（可选）预览交互式图像](#optional-previewing-interactive-images).

>[!NOTE]
将热点添加到交互式图像或轮播横幅中的图像时，热点信息存储在相同的元数据位置。 此位置相对于图像的位置，无论图像是交互式图像还是轮播横幅。 这项功能意味着您可以轻松地在任一查看器中重用相同的图像及其定义的热点数据。
但是，请注意，轮播横幅支持图像映射，这些图像上也可能包含热点；而交互式图像则不支持。 如果您打算创建使用同一图像的交互式图像或轮播横幅，请记住这一点。 您可以改为使用同一图像的单独副本来创建交互式图像和轮播横幅。
另请参阅 [轮播横幅](/help/assets/dynamic-media/carousel-banners.md).

>[!NOTE]
如果您正在编辑具有热点的交互式图像并裁切图像，则您的热点会被删除。

**要将热点添加到图像横幅，请执行以下操作：**

1. 在“资产”视图中，导航到要使其成为交互式内容的图像横幅。
1. 执行下列操作之一：

   * 将鼠标悬停在图像上，然后点按 **[!UICONTROL 选择]** （复选标记图标）。 在工具栏上，点按 **[!UICONTROL 编辑]**.

   * 将鼠标悬停在图像上，然后点按 **[!UICONTROL 更多操作]** （三个圆点图标） **[!UICONTROL >编辑]**.

   * 要在“详细信息视图”页面中将其打开，请点按图像。 在工具栏中，点按 **[!UICONTROL 编辑]**.

1. 在页面的左上角附近，点按&#x200B;**[!UICONTROL 添加热点]**（手指点按图标）以打开热点管理页面。
1. 在页面的左上角附近，点按 **[!UICONTROL 热点]**.

   1. 在“热点管理”页面的左上角附近，点按 **[!UICONTROL 热点]**.
   1. 在图像上，点按您希望显示热点的位置。如有必要，可拖动热点以调整其位置。或者，使用键盘箭头键控制选定热点的位置。
   1. 重复步骤a和b，根据需要添加更多热点。
   1. （可选）要删除热点，请在图像上选择该热点，然后点按 **[!UICONTROL 删除]** （垃圾桶图标） **[!UICONTROL 热点]** 标题。

1. 在“名称”文本字段中，键入热点的名称。 此名称也会显示在选定热点下拉列表中。
1. 执行下列操作之一：

   * 选择 **[!UICONTROL 概览]**.

      * 如果您是Experience Manager Sites或电子商务客户，请选择产品选取器图标（放大镜）以打开“选择产品”页面。 选择要使用的产品，然后点按 **选择** 页面右上角的。 您将返回到“热点”管理页面。
      * 如果您是 *非* Experience Manager Sites或电子商务客户

         * 参见 [标识热点变量](#optional-identifying-hotspot-variables)；您必须定义这些变量。
         * 然后，手动输入SKU值。 在“SKU值”文本字段中，键入产品的SKU。 输入的SKU值会自动填充概览模板的变量部分。 它确保系统知道将点击的热点与特定SKU的Quickview相关联。
         * （可选）如果概览中有其他变量用于进一步标识产品，请点按 **[!UICONTROL 添加通用变量]**. 在文本字段中，指定一个额外的变量。 例如， `category=Mens` 是添加的变量。
   * 选择 **[!UICONTROL 超链接]**.

      * 如果您是Experience Manager Sites客户，请点按站点选择器图标（文件夹）。 导航到URL。 如果您的交互式内容具有带相对URL的链接，尤其是指向Experience Manager Sites页面的链接，则无法基于URL的链接方法。
      * 如果您是独立客户，请在HREF文本字段中指定链接网页的完整URL路径。

   请确保指定是在新的浏览器选项卡（推荐的默认值）中还是同一选项卡中打开链接。

   参见 [使用选择器](/help/assets/dynamic-media/working-with-selectors.md) 了解更多信息。

   * 选择 **[!UICONTROL 体验片段]**.

      * 如果您是Experience Manager Sites客户，请选择“搜索”图标（放大镜）以打开“体验片段”页面。 选择要使用的体验片段。 然后点按 **[!UICONTROL 选择]** 页面右上角的。 您将返回到“热点”管理页面。
参见 [体验片段](/help/sites-cloud/authoring/fundamentals/experience-fragments.md).

      * 指定您希望体验片段在横幅上显示的宽度和高度。

         >[!NOTE]
         将查看器嵌入体验片段时，不支持交互式图像中的社交媒体共享工具。 请改用或创建没有社交媒体共享工具的查看器预设。 通过此类查看器预设，您可以成功地将其嵌入体验片段中。



1. 选择 **[!UICONTROL 保存]** 以保存您的工作并返回到“浏览”页面。
1. 发布交互式图像。 发布功能通过云交付横幅，并生成嵌入代码，让您能够与第三方网站集成。

   参见 [发布资产](/help/assets/manage-digital-assets.md#publish-assets).

   添加热点并发布交互式图像后，您现在可以将其添加到现有网站。

   参见 [将交互式图像与您的网站集成](#integrating-an-interactive-image-with-your-website).

   >[!NOTE]
   如果您正在编辑具有热点的交互式图像并裁切图像，则您的热点会被删除。

### （可选）预览交互式图像 {#optional-previewing-interactive-images}

您可以使用“预览”来查看向客户展示交互式图像的方式。 通过预览，您还可以测试图像的热点，以确保它们按预期运行。

如果对交互式图像满意，则可以发布该图像。
参见 [在网页上嵌入视频查看器或图像查看器](/help/assets/dynamic-media/embed-code.md).
参见 [将URL链接到您的Web应用程序](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md). 如果您的交互式内容具有带相对URL的链接，尤其是指向Experience Manager Sites页面的链接，则无法基于URL的链接方法。
参见 [将Dynamic Media资源添加到页面](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

**要预览交互式图像，请执行以下操作：**

1. 在“资产”视图中，导航到已创建的现有交互式图像，然后点按以在“预览”中打开该图像。
1. 在“预览”页面的左上角附近的“内容”下拉列表中，点按 **[!UICONTROL 查看器]**.
1. 在“查看器”列表中，点按 **[!UICONTROL Shoppable_Banner]** 或您已创建的交互式图像查看器预设的名称。
1. 要测试热点的相关操作，请点按图像上的热点。

## 发布交互式图像资产 {#publishing-interactive-image-assets}

参见 [发布资产](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md) 以了解有关如何发布交互式图像资源的详细信息。

## 将交互式图像与您的网站集成 {#integrating-an-interactive-image-with-your-website}

上传横幅图像、向其添加热点并发布交互式图像后，便可以将其添加到网站页面。

如果您是Experience Manager Sites客户，则可以通过将交互式媒体组件拖动到页面上来添加交互式图像。 参见 [将Dynamic Media资源添加到页面](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

如果您是独立Experience Manager Assets客户，则可以手动将交互式图像添加到您的网站，如本节所述。

1. 复制发布的交互式图像的嵌入代码。
参见 [在网页上嵌入视频查看器或图像查看器](/help/assets/dynamic-media/embed-code.md).

1. 将复制的嵌入代码添加到网页中的所需位置。
复制的嵌入代码是为响应式环境设置的，因此会自动适应分配的区域。

**示例**

使用 [演示网站示例](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html)，请注意三个个人的图片是静态的 `IMG` 标记：

```xml {.line-numbers}
<img class="img-responsive" width="100%" title="Hero Image 2" alt="Hero Image 2" src="images/shoppable-banner.jpg">
```

集成就像删除 `IMG` 标记并将其替换为Experience Manager Assets中复制的嵌入代码。 您可以看到结果 [在带有三个圆热点的页面上显示购物交互式图像](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-1.html).

>[!NOTE]
在这一点上，演示网站的可购物交互式图像上的热点仅用于显示。 它们尚未与现有快速视图集成。

要在响应式环境中将“裁切”应用于购物交互式图像，请包含交互式图像配置属性 `ZoomView.iscommand` 到那条路。 在本例中， `ZoomView` 组件名为和 `iscommand` 是您应用的“裁切”图像服务命令。

参见 [ZoomView.iscommand](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/command-reference-configuration-attributes-interactive-images/r-html5-aem-interactive-image-config-attrib-zoomview-iscommand.html) 配置属性。

参见 [裁切](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-crop.html) 图像服务命令。

现在，您已经准备好将交互式图像与网站上的现有概览集成。

## 将交互式图像与现有的概览集成 {#integrating-an-interactive-image-with-an-existing-quickview}

>[!NOTE]
此任务仅适用于独立Experience Manager Assets客户。

此过程的最后一步是将交互式图像与网站上现有的概览实施集成。 集成没有适用于所有情况的解决方案。 每个概览实施都是独一无二的，需要特定的方法。 因此，获得前端IT人员的帮助会很有帮助。

现有的概览实施通常表示在网页上发生的一系列相互关联的操作，顺序如下：

1. 用户在网站的用户界面中触发元素。
1. 前端代码基于在步骤1中触发的用户界面元素获取概览URL。
1. 前端代码使用在步骤2中获取的URL发送Ajax请求。
1. 后端逻辑将相应的概览数据或内容返回到前端代码。
1. 前端代码加载概览数据或内容。
1. 前端代码可以选择将加载的概览数据转换为HTML表示形式。
1. 前端代码显示一个模式对话框或面板，并在屏幕上为最终用户渲染HTML内容。

这些调用不一定表示网页逻辑从任意步骤调用的独立公共API调用。 相反，它是一个链接调用，其中每个下一步都隐藏在上一步的最后阶段（回调）中。

当可购物交互式图像替换步骤1和部分步骤2时，用户点击可购物图像内的热点。 此类用户交互由查看者处理。 查看器会向网页返回一个事件，其中包含之前添加到Experience Manager Assets的所有热点数据。

在此类事件处理程序中，前端代码执行以下操作：

* 侦听由可购物交互式图像发出的事件。
* 根据热点数据构建概览URL。
* 触发从后端加载概览并在屏幕上呈现以进行显示的过程。

Experience Manager Assets返回的嵌入代码具有一个已注释掉的现成可用事件处理程序，如下面高亮显示的代码片段所示：

```xml {.line-numbers}
        var s7interactiveimageviewer = new s7viewers.InteractiveImage({
            "containerId" : "s7interactiveimage_div",
            "params" : {
                "serverurl" : "https://aodmarketingna.assetsadobe.com/is/image",
                "contenturl" : "https://aodmarketingna.assetsadobe.com/",
                "config" : "/etc/dam/presets/viewer/Shoppable_Media",
                "asset" : "/content/dam/mac/aodmarketingna/shoppable-banner/shoppable-banner.jpg" }
        })
        /* // Example of interactive image event for Quickview.
             s7interactiveimageviewer.setHandlers({
                "quickViewActivate": function(inData) {
                    var sku=inData.sku; //SKU for product ID
                    //To pass other parameter from the hotspot, you will need to add custom parameter during the hotspot setup as parameterName=value
                    loadQuickView(sku); //Replace this call with your Quickview plugin
                    //Please refer to your Quickviewer plugin for the Quickview call
                 },
             });
        */
        s7interactiveimageviewer.init();
```

因此，只需取消注释代码，并用特定网页特定的代码替换虚拟处理程序主体即可。

构建概观URL的过程与用于标识之前涵盖的热点变量的过程相反。

参见 [识别热点变量](#optional-identifying-hotspot-variables).

通过前面的“概览URL”示例，您可以看到以下示例中概览在各种情况下是如何构建的：

<table>
 <tbody>
  <tr>
   <td><p>单个SKU，在查询字符串中找到</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/json?productId=" + inData.sku + "&amp;amp;source=100";
      },
      });</code></td>
  </tr>
  <tr>
   <td><p>单个SKU，可在URL路径中找到</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/product/" + inData.sku;
      },
      });</code></td>
  </tr>
  <tr>
   <td><p>查询字符串中的SKU和类别标识</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/quickView/product/?category=" + inData.categoryId + "&amp;amp;prodId=" + inData.sku;
      },
      });</code></td>
  </tr>
 </tbody>
</table>

触发概观URL和激活概览面板的最后一步需要您工作的前端IT人员的协助。 他们最清楚如何从适当的步骤准确触发概览实施，拥有一个现成的概观URL。

您可以看到如何将这些步骤应用于演示网站，以将可购物交互式图像与概览代码完全集成。 之前，概观URL的结构标识如下：

```xml {.line-numbers}
/datafeed/$categoryId$-$SKU$.json
```

要在中重构此URL，请执行以下操作 `quickViewActivate` 处理程序，您可以使用 `categoryId` 和 `SKU` 字段。 这些字段位于 `inData` 通过查看器的代码传递给处理程序的对象：

```xml {.line-numbers}
var sku=inData.sku;
var categoryId=inData.categoryId;
var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
```

演示网站正在使用简单的 `loadQuickView()` 函数调用。 此函数仅接受一个参数，即概览数据URL。 因此，集成可购物交互式图像的最后一步是将以下代码行添加到 `quickViewActivate` 处理程序：

```xml {.line-numbers}
loadQuickView(quickViewUrl);
```

以下是完整的源代码：

```xml {.line-numbers}
 var s7interactiveimageviewer = new s7viewers.InteractiveImage({
  "containerId" : "s7interactiveimage_div",
  "params" : {
   "serverurl" : "https://aodmarketingna.assetsadobe.com/is/image",
   "contenturl" : "https://aodmarketingna.assetsadobe.com/",
   "config" : "/etc/dam/presets/viewer/Shoppable_Media",
   "asset" : "/content/dam/mac/aodmarketingna/shoppable-banner/shoppable-banner.jpg" }
 })
   s7interactiveimageviewer.setHandlers({
   "quickViewActivate": function(inData) {
     var sku=inData.sku;
     var categoryId=inData.categoryId;
    var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
    loadQuickView(quickViewUrl);
    },
   });
 s7interactiveimageviewer.init();
```

此 [带有完全集成的交互式图像的最终演示网站](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-3.html).

## 使用 Quickview 创建自定义弹出窗口 {#using-quickviews-to-create-custom-pop-ups}

参见 [使用Quickview创建自定义弹出窗口®](/help/assets/dynamic-media/custom-pop-ups.md).
