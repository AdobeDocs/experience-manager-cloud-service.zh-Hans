---
title: 交互式图像
description: 了解如何在Dynamic Media中使用交互式图像。
feature: 交互式图像
topic: 业务从业者
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '4249'
ht-degree: 17%

---


# 交互式图像{#interactive-images}

通过将“购物”热点拖放到图像上，您可以轻松地为客户打造出丰富、引人入胜的静态图像体验。购物热点将有关产品或服务的附加信息与直接的、销售点的“添加到购物车”或“购买”功能结合在一起。 客户可以点按直接链接到产品或服务、将其添加到购物车或链接到网页的这些热点。 这类直接体验能够提高客户在您网站上的参与度和转化率。

下面是一个带“快速视图”弹出窗口的购物横幅。 用户点按模型上的圆或“热点”，即可激活“快速视图”。

![chlimage_1-152](assets/chlimage_1-368.png)

请参阅上图所示网页上的[交互式图像的操作情况](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion-QVzoom/index2-shoppable.html)。

## 观看如何创建交互式图像横幅{#watch-how-interactive-image-banners-are-created}

观看[如何创建交互式图像横幅的10分钟33秒演练](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveCarouselBanner)。 您还可以学习如何预览、编辑和投放交互式图像横幅。

## 快速开始:交互式图像{#quick-start-interactive-images}

以下工作流分步说明旨在帮助您在AEM Assets中快速设置并运行交互式图像。

请查找某些“快速入门”任务中的&#x200B;**示例**&#x200B;标题。它包含一个简短的教程，该教程基于尚未向其](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html)添加交互式图像的[网页示例。



本教程有助于说明在您自己的网站上集成交互式图像的步骤。

交互式图像步骤：

1. **（可选）识别热点变量**。如果您使用Adobe Experience Manager Assets和Dynamic Media独立版本，请识别现有快速视图实施中使用的动态变量。 这样做可确保您在创建交互式图像时输入热点数据。 请参阅[（可选）识别热点变量](#optional-identifying-hotspot-variables)。
但是，如果您使用AEM Sites或AEM eCommerce，或同时使用两者，则不需要执行此步骤。

1. **（可选）创建交互式图像查看器预设**。自定义用于表示热点的图形图像。 如果您打算使用名为`Shoppable_Banner`的现成交互式图像查看器预设，则无需创建您自己的交互式图像查看器预设。
请参阅[（可选）创建交互式图像查看器预设](/help/assets/dynamic-media/managing-viewer-presets.md#creating-a-new-viewer-preset)。

1. **上传图像横幅**。上传要实现交互的图像横幅。请参 [阅上传图像横幅](#uploading-an-image-banner)。

1. **将热点添加到图像横幅**。向图像横幅添加一个或多个热点。将每个视图与一个操作关联，如超链接、快速体验片段。 添加热点后，您将通过发布交互式图像来完成此任务。
请参阅[将热点添加到图像横幅](#adding-hotspots-to-an-image-banner)。
请参阅[预览交互式图像](#optional-previewing-interactive-images) — 可选。 如果需要，您可以查看购物横幅的呈现形式并测试其交互性。
有关如何发布交互式图像资产的详细信息，请参阅[发布资产](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)。

1. **以Experience Manager方式将交互式图像添加到您的网站或您的网站**。如果您使用站点或电子商务，或者同时使用两者，则可以在Experience Manager中将交互式图像直接添加到网页。 将交互式媒体组件拖动到页面上。 请参阅[将Dynamic Media资产添加到页面。](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)
如果您使用Experience Manager资产和Dynamic Media独立版本，请将嵌入代码复制到您的网站。然后，将其与现有快速视图集成。 请参阅[将交互式图像与您的网站集成](#integrating-an-interactive-image-with-your-website)。
如果您使用第三方WCM（Web内容管理器），请将新的交互式视频与您网站上使用的现有快速视图集成。 请参阅[将交互式图像与现有快速视图集成](#integrating-an-interactive-image-with-an-existing-quickview)。

## （可选）识别热点变量{#optional-identifying-hotspot-variables}

>[!NOTE]
>
>只有在以下情况下才需要此任务:
>
>* 您希望通过触发快速视图来为图像添加交互性。
>* 您的Experience Manager实施&#x200B;*不*&#x200B;使用电子商务集成框架从任何电子商务解决方案将产品数据拉入Experience Manager。 此类解决方案包括IBM WebSphere® Commerce、Elastic Path、hybris或Intershop。

>
>
如果您的AEM实施使用电子商务，则可以跳过此任务并继续到下一个任务。

开始，您可以识别现有“快速视图”实施所使用的动态变量，以便输入热点数据以创建交互式图像。

在Experience Manager资产中向横幅图像添加热点时，请分配SKU（库存单位）。 SKU是您所优惠的每个不同产品或服务的唯一标识符。 此外，还可向每个热点添加任何其他可选变量。 以后会使用这些热点变量来将热点与“快速视图”内容相匹配。

必须准确地识别要与热点数据相关联的变量数量及类型，这一点很重要。而且，添加到横幅图像的每个热点都必须附带足够的信息，以便能够在现有的后端系统中明确地识别产品。

有多种不同的方法可以识别用于热点数据的变量集。

有时，只需咨询负责现有快速视图实施的IT专家即可。 此类人员可能了解在系统中识别快速视图所需的最少数据集。 但是，也可以简单地分析前端代码的现有行为。

大多数快速视图实施采用以下模式：

* 用户在网站上激活用户界面元素。例如，单击“快速视图”按钮。
* 如果需要，网站会向后端发送Ajax请求以加载快速视图数据或内容。
* “快速视图”数据将转换为准备在网页上呈现的内容。
* 最后，前端代码以可视形式将这些内容呈现在屏幕上。

接下来的方法是访问现有网站中实施“快速视图”功能的不同区域。 然后触发快速视图并捕获由网页发送的用于加载快速视图数据或内容的Ajax URL。

通常情况下，您不需要使用任何专业的调试工具。现代的 Web 浏览器具备 Web 检查器，可以实现相同的功能。下面列举了一些具备 Web 检查器的 Web 浏览器：

* 要在 Google Chrome 中查看发出的所有 HTTP 请求，请按 F12 键以打开“开发人员工具”面板，然后单击“网络”选项卡。在Mac上，按Command+Option+I打开“开发人员工具”面板，然后单击“网络”选项卡。

* 在Firefox中，您可以按F12并使用其“网络”选项卡来激活Firebug插件。 或者，您可以使用内置的检查器工具及其“网络”选项卡。
在Mac上，按Command+Option+I打开“开发人员工具”面板，然后单击“检查器”选项卡。

在浏览器中打开网络监视时，在页面上触发“快速视图”。

现在，在网络日志中找到“快速视图Ajax URL”，并复制记录的URL以供将来分析。 通常，当您触发“快速视图”时，会有许多请求被发送到服务器。 通常，快速视图Ajax URL是列表中最早的URL之一。 它具有复杂的查询字符串部分或路径，其响应MIME类型为`text/html`、`text/xml`或`text/javascript`。

在此过程中，请务必访问网站中具有不同产品类别和类型的不同区域。 其原因是，快速视图URL可能包含特定网站类别通用的部件。 但是，仅当您访问网站的其他区域时，它们才会更改。

在最简单的情况下，快速视图URL中唯一的变量部分是产品SKU。在这种情况下，SKU值是您向横幅图像添加热点时唯一需要的数据。

但是，在复杂情况下，快速视图URL除了SKU之外，还具有不同的可变元素。 例如，可变元素可能包括类别ID、颜色代码和大小代码。 在这种情况下，在“Experience Manager资产”的交互式购物图像功能中，每个元素都是热点数据定义中的一个单独变量。

请考虑以下快速视图URL示例及其生成的热点变量：

<table>
  <tbody>
  <tr>
    <td><p>单个 SKU，位于查询字符串中。</p> </td>
    <td><p>录制的快速视图URL包括：</p>
    <ul>
      <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>URL 中唯一的变量部分是 productId= 查询字符串参数的值，很明显它就是 SKU 值。因此，热点只需在SKU字段中填充<strong><code>866558</code></strong>、<strong><code>1196184</code></strong>、<strong><code>1081492</code></strong>、<strong><code>1898294</code></strong>等值即可。</p> </td>
  </tr>
  <tr>
    <td><p>单个 SKU，位于 URL 路径中。</p> </td>
    <td><p>录制的快速视图URL包括：</p>
    <ul>
      <li><p><code>https://server/product/6422350843</code></p> </li>
      <li><p><code>https://server/product/1607745002</code></p> </li>
      <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>路径的最后一部分是变量部分，它成为热点的SKU值：<strong><code>6422350843</code></strong>、<strong><code>1607745002</code></strong>、<strong><code>0086724882</code></strong>。</p> </td>
  </tr>
  <tr>
    <td><p>SKU 和类别 ID，位于查询字符串中。</p> </td>
    <td><p>录制的快速视图URL包括：</p>
    <ul>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>在这种情况下，URL 中有两个可变部分。SKU存储在<code>prodId</code>参数中，类别ID<code></code>存储在<code>category=</code>参数中。</p> <p>因此，热点定义是成对存在的，即，一个SKU值和一个额外的变量<code>categoryId</code>。 生成的各对如下所示：</p>
    <ul>
      <li><p>SKU为<strong><code>305466</code></strong>,<code>categoryId</code>为<code>1100004</code>。</p> </li>
      <li><p>SKU为<strong><code>310181</code></strong>,<code>categoryId</code>为<strong><code>1100004</code></strong>。</p> </li>
      <li><p>SKU为<strong><code>308706</code></strong>,<code>categoryId</code>为<strong><code>1740148</code></strong>。</p> </li>
    </ul> <p> </p> </td>
  </tr>
  </tbody>
</table>

**示例**

您可以将上述三个示例中使用的相同方法应用于[演示网页](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html)。

演示网页有多个产品缩略图，每个缩略图都有一个标有“查看更多”的“快速视图”按钮。在Web浏览器的调试工具仍处于激活状态时，单击每个按钮并记下录制的快速视图URL。在您激活页面上所有四个可用的产品快速视图后，您对向后端发出的快速视图请求有以下列表:

* `/datafeed/Men-Windbreaker.json`
* `/datafeed/Men-SimpleHenley.json`
* `/datafeed/Men-CamoPullover.json`
* `/datafeed/Women-QuiltedDownJacket.json`

查看服务器调用，您会发现产品特定信息仅存在于请求路径中。 您还会注意到，查询字符串根本不被使用，并且涉及两种不同类型的数据段：

* 第一类是“男人”或“妇女”。 您可以称此为“产品类别”。
* 第二种类型是产品名称，如CamoPullover，它可能是产品SKU。

根据此信息，整个快速视图URL具有以下模式：

`/datafeed/$categoryId$-$SKU$.json`

依据上述分析，您可以在热点中使用 `categoryId` 和 `SKU`。

现在，您便可以使用 AEM Assets 中的交互式购物图像功能，上传图像横幅并向其添加热点。

## （可选）创建交互式图像查看器预设{#optional-creating-an-interactive-image-viewer-preset}

您可以选择使用 AEM Assets 默认附带的名为 `Shoppable_Banner` 的现成交互式图像查看器预设。或者，您也可以创建自己的自定义查看器预设以用于交互式图像。

在创建自定义交互式图像查看器预设时，您可以确定图像横幅上热点的外观。 在创建查看器预设的过程中，您可以选择使用预定义图像库中提供的热点图形。

在保存查看器预设后，查看器预设会在AEM Assets的“查看器预设”列表页面上自动激活（打开）。 此功能意味着无论您何时视图资产，都可以在交互式媒体组件中看到此功能。 但是，要&#x200B;*传送*&#x200B;具有此查看器预设的交互式横幅，*也要发布*&#x200B;您的查看器预设。 对于自定或现成查看器预设，此规则为true。

**要创建交互式图像查看器预设，请执行以下操作**

1. 在左边栏中，点按&#x200B;**[!UICONTROL 工具>资产>查看器预设]**。
1. 在页面的右上角附近，点按&#x200B;**[!UICONTROL 创建]**。
1. 在“新查看器预设”对话框中，键入一个用于描述该交互式横幅查看器预设的名称。


   保存后，此标题将显示在“查看器预设”列表页中。

1. 在“富媒体类型”下拉菜单中，选择&#x200B;**[!UICONTROL 交互式图像]**。
1. 点按&#x200B;**[!UICONTROL 创建]**。
1. 在“编辑查看器预设”页面中，点按&#x200B;**[!UICONTROL 外观]**&#x200B;选项卡。
1. 执行下列操作之一：

   * 要上传您自己的热点图像以在图像上使用，请点按“资产选取器”图标。在“选择内容”页面中，导航到您要使用的热点图像并将其选中。 点按右上角的对勾标记图标。
   * 要选择预定义的热点图像，请点按“热点图库”图标。在热点图库调板上，点按您要使用的热点图像。

1. 在页面的右上角附近，点按&#x200B;**[!UICONTROL 保存]**。

   请确保您发布了新查看器预设。

   请参阅[发布查看器预设](/help/assets/dynamic-media/managing-viewer-presets.md#publishing-viewer-presets)。

   现在，您便可以上传图像横幅。

## 上传图像横幅 {#uploading-an-image-banner}

如果您已上传要使用的图像，请继续执行下一步[将热点添加到图像横幅](#adding-hotspots-to-an-image-banner)。

**上传图像横幅**

1. 上传您要实现交互的图像横幅。

   请参阅[上传资产](/help/assets/manage-digital-assets.md#uploading-assets)。


   现在，您可以向图像横幅添加热点；请参阅下面的下一个任务。

## 将热点添加到图像横幅 {#adding-hotspots-to-an-image-banner}

您可以使用“热点管理”页面上的编辑器将热点添加到图像横幅。

添加热点时，您可以将热点定义为“快速视图”弹出显示、超链接或体验片段。

请参阅[体验片段](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)。

>[!NOTE]
>
>将查看器嵌入体验片段时，不支持交互式图像中的社交媒体共享工具。 请改用或创建没有社交媒体共享工具的查看器预设。 此类查看器预设使您能够成功地将其嵌入到体验片段中。

在当前创建/编辑会话中，页面右上角附近支持撤消和重做选项。

创建完交互式图像后，您可以使用预览来查看交互式图像如何呈现给客户的演示。

请参阅[（可选）预览交互式图像](#optional-previewing-interactive-images)。

>[!NOTE]
>
>当您在交互式图像或传送横幅中向图像添加热点时，热点信息会存储在同一元数据位置。 此位置是相对于图像位置的，而不管它是交互式图像还是传送横幅。 此功能意味着您可以在任一查看器中轻松重复使用同一图像及其定义的热点数据。
但是，请注意，传送横幅支持图像上的图像映射，这些图像上可能还包含热点；交互式图像不会。 如果您要创建使用相同图像的交互式图像或传送横幅，请牢记这一点。 您可以改为使用同一图像的单独副本创建交互式图像和传送横幅。
另请参阅[传送横幅](/help/assets/dynamic-media/carousel-banners.md)。

>[!NOTE]
如果您正在编辑具有热点的交互式图像并裁剪图像，则您的热点将被删除。

**向图像横幅添加热点**

1. 在“资产”视图中，导航到您要实现交互的图像横幅。
1. 执行下列操作之一：

   * 将鼠标悬停在图像上，然后点按&#x200B;**[!UICONTROL 选择]**（复选标记图标）。 在工具栏中，点按&#x200B;**[!UICONTROL 编辑]**。

   * 将鼠标悬停在图像上，然后点按&#x200B;**[!UICONTROL 更多操作]**（三个点图标）**[!UICONTROL >编辑]**。

   * 要在“详细信息”视图页中打开它，请点按图像。 在工具栏中，点按&#x200B;**[!UICONTROL 编辑]**。

1. 在页面的左上角附近，点按&#x200B;**[!UICONTROL 添加热点]**（手指点按图标）以打开热点管理页面。
1. 在页面的左上角附近，点按&#x200B;**[!UICONTROL 热点]**。

   1. 在“热点管理”页面的左上角附近，点按&#x200B;**[!UICONTROL 热点]**。
   1. 在图像上，点按您希望显示热点的位置。如有必要，可拖动热点以调整其位置。或者，使用键盘箭头键控制选定热点的位置。
   1. 重复步骤a和b，根据需要添加更多热点。
   1. （可选）要删除热点，请在图像上选择它，然后点按&#x200B;**[!UICONTROL 热点]**&#x200B;标题下的&#x200B;**[!UICONTROL 删除]**（垃圾桶图标）。

1. 在“名称”文本字段中，键入热点的名称。此名称也会显示在“选定的热点”下拉列表中。
1. 执行下列操作之一：

   * 点按&#x200B;**[!UICONTROL 快速视图]**。

      * 如果您是AEM Sites或电子商务客户，请点按或单击产品选取器图标（放大镜）以打开选择产品页面。 点按要使用的产品，然后点按页面右上角的&#x200B;**选择**。 您将返回到“热点”管理页面。
      * 如果您是&#x200B;*不是* Experience Manager站点或电子商务客户

         * 请参阅[识别热点变量](#optional-identifying-hotspot-variables);您必须定义这些变量。
         * 然后，手动输入SKU值。 在“SKU值”文本字段中，键入产品的SKU。 输入的SKU值会自动填充“快速视图”模板的变量部分。 它可确保系统知道将点按的热点与特定SKU的快速视图关联。
         * （可选）如果“快速”视图中有其他用于进一步标识产品的变量，请点按&#x200B;**[!UICONTROL 添加常规变量]**。 在文本字段中，指定一个额外的变量。 例如，`category=Mens` 就是一个添加的变量。
   * 点按&#x200B;**[!UICONTROL 超链接]**。

      * 如果您是Experience Manager站点客户，请点按站点选择器图标（文件夹）。 导航到URL。 如果您的交互式内容包含与相对URL(尤其是指向Experience Manager站点页面的链接)的链接，则无法使用基于URL的链接方法。
      * 如果您是独立客户，请在“HREF”文本字段中指定链接网页的完整URL路径。

   请确保指定是在新的浏览器选项卡（建议的默认选项卡）还是在同一选项卡中打开链接。

   有关详细信息，请参阅[使用选择器](/help/assets/dynamic-media/working-with-selectors.md)。

   * 点按&#x200B;**[!UICONTROL 体验片段]**。

      * 如果您是AEM Sites客户，请点按或单击搜索图标（放大镜）以打开体验片段页面。 点按您要使用的体验片段。 然后点按页面右上角的&#x200B;**[!UICONTROL 选择]**。 您将返回到“热点”管理页面。
请参阅[体验片段](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)。

      * 指定体验片段在横幅上显示时的宽度和高度。

         >[!NOTE]
         将查看器嵌入体验片段时，不支持交互式图像中的社交媒体共享工具。 请改用或创建没有社交媒体共享工具的查看器预设。 此类查看器预设使您能够成功地将其嵌入到体验片段中。



1. 点按&#x200B;**[!UICONTROL 保存]**&#x200B;以保存您的工作并返回浏览页面。
1. 发布交互式图像。 发布功能通过云提供横幅，还生成可让您与第三方网站集成的嵌入代码。

   请参阅[发布资产](/help/assets/manage-digital-assets.md#publish-assets)。

   在添加热点并发布交互式图像后，您现在可以将其添加到现有网站。

   请参阅[将交互式图像与您的网站集成](#integrating-an-interactive-image-with-your-website)。

   >[!NOTE]
   如果您正在编辑具有热点的交互式图像并裁剪图像，则您的热点将被删除。

### （可选）预览交互式图像{#optional-previewing-interactive-images}

您可以使用预览来查看交互式图像对客户的呈现效果。 预览还允许您测试图像的热点，确保它们按预期的方式显示。

当您对交互式图像感到满意时，您可以发布该图像。
请参阅[在网页上嵌入视频查看器或图像查看器](/help/assets/dynamic-media/embed-code.md)。请参阅[将 URL 关联到您的 Web 应用程序](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)。如果您的交互式内容包含与相对URL(尤其是指向AEM Sites页面的链接)的链接，则无法使用基于URL的链接方法。
请参阅[将Dynamic Media资产添加到页面。](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)

**预览交互式图像**

1. 在“资产”视图中，导航到您创建的现有交互式图像，然后点按以在预览中打开它。
1. 在预览页面的左上角附近，在“内容”下拉列表中，点按&#x200B;**[!UICONTROL 查看器]**。
1. 在“查看器”列表中，点按&#x200B;**[!UICONTROL Shoppable_Banner]**&#x200B;或您创建的交互式图像查看器预设的名称。
1. 要测试热点的关联操作，请点按图像上的热点。

## 发布交互式图像资源{#publishing-interactive-image-assets}

有关如何发布交互式图像资产的详细信息，请参阅[发布资产](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)。

## 将交互式图像与您的网站{#integrating-an-interactive-image-with-your-website}集成

在上传横幅图像、向其添加热点以及发布交互式图像后，即可将其添加到网站页面。

如果您是AEM Sites客户，则可以通过将交互式媒体组件拖动到页面上来添加交互式图像。 请参阅[将Dynamic Media资产添加到页面。](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)

如果您是独立的AEM Assets客户，则可以按本节所述手动将交互式图像添加到您的网站。

1. 复制已发布的交互式图像的嵌入代码。
请参阅[在网页上嵌入视频查看器或图像查看器](/help/assets/dynamic-media/embed-code.md)。

1. 将复制的嵌入代码添加到网页中的所需位置。
复制的嵌入代码是为响应式环境设置的，因此会自动适应分配的区域。

**示例**

以[演示网站为例](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html)，请注意，这三个人的图片是静态`IMG`标签：

```xml
<img class="img-responsive" width="100%" title="Hero Image 2" alt="Hero Image 2" src="images/shoppable-banner.jpg">
```

集成过程很简单，只需删除 `IMG` 标记并将其替换为从 AEM Assets 中复制的嵌入代码即可。您可以看到，结果[显示页面上的交互式购物图像，其中有三个圆形热点](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-1.html)。

>[!NOTE]
至此，演示网站的交互式购物图像上的热点仅用于显示目的。它们尚未与现有的快速视图集成。

要对交互式购物图像应用“裁剪”以实现响应式环境，请将交互式图像配置属性`ZoomView.iscommand`包含到路径中。 在这种情况下，将调用`ZoomView`组件，`iscommand`是您应用的“裁剪”图像服务命令。

请参阅 [ZoomView.iscommand](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/command-reference-configuration-attributes-interactive-images/r-html5-aem-interactive-image-config-attrib-zoomview-iscommand.html) 配置属性。

请参阅[裁剪](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-crop.html)图像服务命令。

现在，您可以将交互式图像与网站上现有的快速视图集成。

## 将交互式图像与现有快速视图{#integrating-an-interactive-image-with-an-existing-quickview}集成

>[!NOTE]
此任务仅在您是独立AEM Assets客户时适用。

此过程的最后一步是将交互式图像与网站上现有的快速视图实施相集成。 但是，没有任何一种集成解决方案是在所有情况下都适用的。每个快速视图实施都是独一无二的，并且需要一种特定的方法。 因此，在前端IT人员的协助下工作非常有帮助。

现有的“快速视图”实施通常表示按以下顺序在网页上发生的一系列相互关联的操作：

1. 用户在网站的用户界面上触发一个元素。
1. 前端代码根据在步骤1中触发的用户界面元素获取快速视图URL。
1. 前端代码使用在第 2 步获取的 URL 发送一个 Ajax 请求。
1. 后端逻辑将相应的快速视图数据或内容返回给前端代码。
1. 前端代码加载快速视图数据或内容。
1. （可选）前端代码将加载的快速视图数据转换为HTML表示形式。
1. 前端代码显示一个模态对话框或面板，并将 HTML 内容呈现在屏幕上以供最终用户查看。

这些调用不一定代表由网页逻辑从任意步骤调用的独立公共API调用。 相反，这些调用属于链式调用，即，每个后续步骤都隐藏在前一步的最后阶段（回调）。

当交互式购物图像替换第1步（部分替换第2步）时，用户将在购物图像内点击热点。 此类用户交互由查看器处理。 查看器会向网页返回一个事件，其中包含之前添加到 AEM Assets 中的所有热点数据。

在此类事件处理程序中，前端代码会执行下列操作：

* 监听交互式购物图像发出的事件。
* 根据热点数据构建快速视图URL。
* 触发从后端加载快速视图并在屏幕上显示它的过程。

Experience Manager资产返回的嵌入代码具有一个已注释掉的可用事件处理程序，如下面突出显示的代码片断所示：

```xml
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

因此，只需取消对该代码的注释，并用针对特定网页的代码来替换虚拟处理程序主体即可。

构建快速视图URL的过程与之前介绍的用于识别热点变量的过程相反。

请参阅[识别热点变量](#optional-identifying-hotspot-variables)。

使用上面的快速视图URL示例，您可以在以下示例中了解每种情况下如何构建快速视图URL:

<table>
 <tbody>
  <tr>
   <td><p>单个 SKU，位于查询字符串中</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/json?productId=" + inData.sku + "&amp;amp;source=100";
      },
      });</code></td>
  </tr>
  <tr>
   <td><p>单个 SKU，位于 URL 路径中</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/product/" + inData.sku;
      },
      });</code></td>
  </tr>
  <tr>
   <td><p>SKU 和类别 ID，位于查询字符串中</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/quickView/product/?category=" + inData.categoryId + "&amp;amp;prodId=" + inData.sku;
      },
      });</code></td>
  </tr>
 </tbody>
</table>

触发“快速视图URL”并激活“快速视图”面板的最后一步，需要业务前端IT人员的协助。 他们最了解如何通过拥有现成的快速视图URL从正确的步骤准确触发快速视图实施。

您可以了解如何将这些步骤应用到演示网站，以将交互式购物图像与快速视图代码完全集成。以前，快速视图URL的结构如下所示：

```xml
/datafeed/$categoryId$-$SKU$.json
```

要在`quickViewActivate`处理函数中重建此URL，可使用`categoryId`和`SKU`字段。 这些字段在`inData`对象中可用，该对象由查看器的代码传递给处理函数：

```xml
var sku=inData.sku;
var categoryId=inData.categoryId;
var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
```

演示网站使用简单的`loadQuickView()`函数调用触发“快速视图”对话框。 此函数只采用一个参数，即快速视图数据URL。 因此，集成交互式购物图像的最后一步是将以下代码行添加到`quickViewActivate`处理函数中：

```xml
loadQuickView(quickViewUrl);
```

下面是完整的源代码：

```xml
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

具有完全集成的交互式图像的[最终演示网站](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-3.html)。

## 使用快速视图创建自定义弹出窗口{#using-quickviews-to-create-custom-pop-ups}

请参阅[使用快速视图创建自定义弹出窗口](/help/assets/dynamic-media/custom-pop-ups.md)。
