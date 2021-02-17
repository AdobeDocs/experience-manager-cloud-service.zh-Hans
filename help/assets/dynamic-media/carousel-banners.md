---
title: 传送横幅
description: 了解如何在Dynamic Media中使用传送横幅。
translation-type: tm+mt
source-git-commit: 3391045d867cdfc21ab9784e20c6893d38bc78f0
workflow-type: tm+mt
source-wordcount: '4561'
ht-degree: 9%

---


# 传送横幅{#carousel-banners}

传送横幅使营销人员能通过轻松创建交互式旋转促销内容并将其交付到任何屏幕来推动转化率。

创建和修改促销横幅中特有的内容可能非常耗时，从而限制您快速发布新内容或使其更具针对性的能力。 传送横幅允许您快速创建或修改旋转横幅并添加交互性，如链接到产品详细信息或相关资源的热点。 您可以将内容投放到任何屏幕，从而更快地将新的促销内容投放市场。

传送横幅由带有&#x200B;**[!UICONTROL CAROUSELSET]**&#x200B;字样的横幅来指定：

![chlimage_1-438](assets/chlimage_1-438.png)

在您的网站上，传送横幅可以如下所示：

![chlimage_1-439](assets/chlimage_1-439.png)

在此，您可以通过单击数字来浏览图像。 此外，幻灯片会根据您可以自定义的时间间隔自动旋转。 您在传送横幅中添加的图像支持热点和图像映射。 用户可以点按或转到超链接或访问“快速视图”窗口。

在此示例中，用户已点按或单击图像映射，并访问了手套的“快速视图”窗口：

![chlimage_1-440](assets/chlimage_1-440.png)

## 观看如何创建传送横幅{#watch-how-carousel-banners-are-created}

观看有关如何创建传送横幅的[的10分钟33秒演练](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveCarouselBanner)。 您还可以了解如何预览、编辑和传送传送传送横幅。

>[!NOTE]
>
>必须将非管理用户添加到&#x200B;**[!UICONTROL dam-users]**&#x200B;组，才能创建或编辑传送横幅。 如果您在创建或编辑时遇到问题，请咨询系统管理员，他可以将您添加到&#x200B;**d[!UICONTROL am-users]**&#x200B;组。

## 快速开始:传送横幅{#quick-start-carousel-banners}

要快速设置并运行图像集，请执行以下操作：

1. [识别热点和图像映射变量](#identifying-hotspot-and-image-map-variables) (仅适用于使用Adobe Experience Manager Assets + Dynamic Media的客户)

   开始，确定现有“快速视图”实施所使用的动态变量。 这样做可帮助您在Experience Manager资产中创建传送横幅的过程中正确输入热点和图像映射数据。

<!-- LEAVE; COMMERCE BEING ADDED AGAIN IN THE FUTURE

   >[!NOTE]
   >
   >If you are an AEM Sites or Ecommerce customer, you can use the built-in feature to navigate to product pages and lookup the existing skus in the product catalog. You do not need to manually enter hotspot or image map variables.
   >
   >
   >If you are an AEM Assets and Dynamic Media customer, you will manually enter data for hotspots and image maps, and then integrate the published URL or Embed code with your third-party content management system.

-->

1. 可选：根据需要[创建轮播集查看器预设](/help/assets/dynamic-media/managing-viewer-presets.md)。

   如果您是管理员，则可以通过创建自己的传送查看器预设来自定义传送的行为和外观。 主要优点是，您可以对多个轮播重复使用此自定义查看器预设。 但是，用户可以在创作传送时选择直接自定义传送的行为和外观。 当您需要给定传送的特定设计时，最好使用此方法。

1. [上传图像横幅](#uploading-image-banners)。

   上传您要实现交互的图像横幅。

1. [创建传送集](#creating-carousel-sets)。

   在轮盘集中，用户在横幅图像之间导航，并点按热点或图像映射以访问相关内容。

   要在 Assets 中创建轮播集，请点按&#x200B;**[!UICONTROL 创建]**，然后选择&#x200B;**[!UICONTROL 轮播集]**。将资产添加到幻灯片，然后点按&#x200B;**[!UICONTROL 保存]**。您还可以直接在编辑器中编辑轮播集的外观和行为。

1. [将热点或图像映射添加到图像横幅。](#adding-hotspots-or-image-maps-to-an-image-banner)

   向图像横幅添加一个或多个热点或图像映射。 然后，将每个视图与一个操作（如链接、快速体验片段）关联。 添加热点或图像映射后，可通过发布传送集来完成此任务。 发布后会创建可用于复制并应用于网站登陆页的嵌入代码。

   请参阅[（可选）预览传送横幅。](#optional-previewing-carousel-banners) - 可选. 如果需要，您可以视图轮盘集的表示形式并测试其交互性。

1. [发布传送横幅](#publishing-carousel-banners)。

   您可以像发布任何资产一样发布传送集。 在资产中，导航到传送集并将其选中，然后点按&#x200B;**[!UICONTROL 发布]**。 发布传送集时，将激活URL和嵌入字符串。

1. 执行下列操作之一：

   * [将传送横幅添加到您的网站](#adding-a-carousel-banner-to-your-website-page)页面您可以添加已复制到网站页面上的传送横幅URL或嵌入代码。

      * [将轮盘横幅与现有的快速视图集成](#integrating-the-carousel-banner-with-an-existing-quickview)。如果您使用的是第三方Web内容管理系统，则必须将新的传送横幅与网站上现有的快速视图实施相集成。
   * [以Experience Manager方式将传送横幅添加到您的网站](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)。如果您是Experience Manager站点客户，则可以使用交互式媒体组件将传送集直接添加到页面。


如果必须编辑传送集，请参阅[编辑传送集。](#editing-carousel-sets) 此外，您还可以视图和编辑传送 [集属性](/help/assets/manage-digital-assets.md#editing-properties)。

## 识别热点和图像映射变量{#identifying-hotspot-and-image-map-variables}

开始，确定现有“快速视图”实施所使用的动态变量。 此方法可帮助您在创建传送集的过程中在Experience Manager资产中输入热点或图像映射数据。

在向横幅图像添加热点或图像映射时，您需要分配一个SKU（库存单位）。 您还可以为每个热点或图像映射分配可选的额外变量。 以后会使用这些变量将热点或图像映射与快速视图内容相匹配。

<!-- LEAVE; COMMERCE BEING ADDED LATER

>[!NOTE]
>
>If you are an AEM Sites and/or AEM Ecommerce customer, skip this step. You do not need to manually identify hotspot or image map variables; you can use the integration with Ecommerce for product integration. See information on [setting up eCommerce](/help/sites-cloud/administering/generic.md). In addition, you can use the Interactive component and add it to your web page.
>
>If you are an AEM Assets or Media customer, you publish the URL or Embed code and then integrate with your third-party content management system and identify hotspots and image maps manually.

-->

必须正确识别要与热点或图像地图数据关联的变量的数量和类型。 添加到横幅图像的每个热点或图像映射都必须包含足够的信息，以便在现有后端系统中明确地识别产品。 同时，请确保每个热点或图像映射不包含的数据不比必需的更多。 原因在于，这会使数据输入过程变得过于复杂，并且持续的热点或图像映射管理更容易出错。

有不同的方法可识别用于热点或图像地图数据的一组变量。

有时，只需咨询负责现有快速视图实施的IT专家即可。 他们可能知道在系统中识别快速视图的最少数据集。 但是，可以简单地分析前端代码的现有行为。

大多数快速视图实施采用以下模式：

* 用户在网站上激活用户界面元素。例如，点按&#x200B;**[!UICONTROL 快速查看]**&#x200B;按钮。
* 如果需要，网站会向后端发送一个Ajax请求以加载快速视图数据或内容。
* “快速视图”数据将转换为准备在网页上呈现的内容。
* 最后，前端代码以可视形式将这些内容呈现在屏幕上。

接下来的方法是访问现有网站中实施“快速视图”功能的不同区域。 然后触发快速视图并捕获网页发送的用于加载快速视图数据或内容的Ajax URL。

通常情况下，您不需要使用任何专业的调试工具。现代的 Web 浏览器具备 Web 检查器，可以实现相同的功能。下面列举了一些具备 Web 检查器的 Web 浏览器：

* 要在Google Chrome中查看所有传出HTTP请求，请按F12(Windows)或Command-Option-I(Mac)打开“开发人员工具”面板。 点按网络选项卡。
* 在Firefox中，您可以按F12(Windows)或Command-Option-I(Mac)激活Firebug插件。 使用其“网络”选项卡，或使用内置的“检查器”工具及其“网络”选项卡。

在浏览器中打开网络监视时，在页面上触发“快速视图”。

现在，在网络日志中找到“快速视图Ajax URL”，并复制记录的URL以供将来分析。 通常，当您触发“快速视图”时，会有许多请求被发送到服务器。 通常，快速视图Ajax URL是列表中最早的URL之一。 它具有复杂的查询字符串部分或路径，其响应MIME类型为`text/html`、`text/xml`或`text/javascript`。

在此过程中，请务必访问网站中具有不同产品类别和类型的不同区域。 其原因是，快速视图URL的某些部分对于给定的网站类别是通用的，但仅在您访问网站的其他区域时才会更改。

在最简单的情况下，快速视图URL中唯一的变量部分是产品SKU。 在这种情况下，SKU值是您向横幅图像添加热点或图像映射时唯一需要的数据。

但是，在复杂情况下，快速视图URL除了SKU之外，还具有不同的可变元素。 其中一些元素包括类别ID、颜色代码、大小代码等。 在这种情况下，在旋转横幅功能中，每个元素都是热点或图像映射数据定义中的单独变量。

请考虑以下快速视图URL示例及其生成的热点或图像映射变量：

<table>
 <tbody>
  <tr>
   <td>单个 SKU，位于查询字符串中。</td>
   <td><p>录制的快速视图URL包括：</p>
    <ul>
     <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>URL中唯一的变量部分是<code>productId=</code>查询字符串参数的值，很明显它是SKU值。 因此，热点或图像映射只需在SKU字段中填充值，例如 <code>866558,</code> <code>1196184,</code> <code>1081492,</code> <code>1898294.</code></p> </td>
  </tr>
  <tr>
   <td>单个 SKU，位于 URL 路径中。</td>
   <td><p>录制的快速视图URL包括：</p>
    <ul>
     <li><p><code>https://server/product/6422350843</code></p> </li>
     <li><p><code>https://server/product/1607745002</code></p> </li>
     <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>变量部分位于路径的最后一部分，它将成为热点/图像映射的SKU值：<strong><code>6422350843</code>、<code>1607745002,</code> </strong><code>0086724882.</code></p> </td>
  </tr>
  <tr>
   <td>SKU 和类别 ID，位于查询字符串中。</td>
   <td><p>录制的快速视图URL包括：</p>
    <ul>
     <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
     <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
     <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>在这种情况下，URL 中有两个可变部分。SKU存储在<code>prodId</code>参数中，类别ID存储在<code>category=</code>参数中。</p> <p>因此，热点/图像映射定义是成对存在的。 即，一个SKU值和一个额外的变量<code>categoryId</code>。 生成的各对如下所示：</p>
    <ul>
     <li><p>SKU为<strong><code>305466</code></strong>,<code>categoryId</code>为<code>1100004</code>。</p> </li>
     <li><p>SKU为<strong><code>310181</code></strong>,<code>categoryId</code>为<strong><code>1100004</code></strong>。</p> </li>
     <li><p>SKU为<strong><code>308706</code></strong>,<code>categoryId</code>为<strong><code>1740148</code></strong>。</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 上传图像横幅{#uploading-image-banners}

如果您已上传要使用的图像，请前进到下一步[创建传送集](#creating-carousel-sets)。 在启用Dynamic Media后，必须上传传送中使用的图像。

要上传图像横幅，请参阅[上传资产](/help/assets/manage-digital-assets.md)。

## 创建传送集{#creating-carousel-sets}

>[!NOTE]
>
>必须将非管理用户添加到&#x200B;**[!UICONTROL dam-users]**&#x200B;组，才能创建或编辑传送横幅。 如果您在创建或编辑时遇到问题，请咨询系统管理员，他可以将您添加到&#x200B;**[!UICONTROL dam-users]**&#x200B;组。

**创建传送集**

1. 在资产中，导航到要创建传送集的文件夹，然后点按&#x200B;**[!UICONTROL 创建>传送集]**。
1. 在传送横幅编辑器页面上，点按&#x200B;**[!UICONTROL 以打开资产选择器]**&#x200B;以选择第一张幻灯片的图像。

   在“传送横幅编辑器”页面上，执行下列操作之一：

   * 在页面的左上角附近，点按&#x200B;**[!UICONTROL 添加幻灯片]**&#x200B;图标。

   * 在页面中间附近，点按&#x200B;**[!UICONTROL 点按以打开资产选择器]**。
   点按以选择要包含在轮播集中的资产。选定的资产上面有一个勾形图标。 完成后，在页面右上角附近，点按&#x200B;**[!UICONTROL 选择]**。

   借助资产选择器，您可以通过键入关键字并点按或单击&#x200B;**[!UICONTROL 返回]**&#x200B;来搜索资产。您还可以应用过滤器来优化搜索结果。您可以按路径、收藏集、文件类型和标记进行过滤。选择该过滤器，然后点按工具栏中的&#x200B;**[!UICONTROL 过滤器]**&#x200B;图标。 点按“视图”图标并选择&#x200B;**[!UICONTROL 列视图]**、**[!UICONTROL 卡片视图]**&#x200B;或&#x200B;**[!UICONTROL 列表视图]**&#x200B;可更改视图。

   有关详细信息，请参阅[使用选择器](/help/assets/dynamic-media/working-with-selectors.md)。

1. 继续添加幻灯片，直到添加了要在传送集中旋转的所有图像。
1. （可选）执行以下操作之一：

   * 如有必要，拖动幻灯片可以在列表中对图像重新排序。
   * 要删除图像，请选择该图像，然后点按工具栏中的&#x200B;**[!UICONTROL 删除幻灯片]**。

   * 要应用预设，请点按页面右上角附近的预设下拉列表，然后选择要一次应用到该集的预设。
   要删除幻灯片，请点按或单击幻灯片，然后点按或单击工具栏中的&#x200B;**[!UICONTROL 删除幻灯片]**。 要移动幻灯片，请点按重新排序图标，然后按住并移至所需位置。

1. 在幻灯片中添加图像后，可以向图像中添加热点和/或图像映射。 请参阅[添加热点或图像映射](#adding-hotspots-or-image-maps-to-an-image-banner)。
1. 您可以更改传送集的可视设计和行为。 点按或单击“行为”和“外观”选项卡，并调整旋转横幅的外观或特定组件的行为方式。 有关如何使用查看器编辑器的详细信息，请参阅[管理查看器预设](/help/assets/dynamic-media/viewer-presets.md)。

   >[!NOTE]
   >
   >对于传送横幅，您可以调整以下内容：
   >    * 图像显示的持续时间。 默认情况下，每幅图像显示9秒。
   >    * 动画. 默认情况下，每张幻灯片过渡都是淡入淡出。 您可以将其更改为幻灯片过渡。
   >    * 按钮的样式。 用户点击每个点或数字即可旋转横幅。 您可以更改设置指示符按钮的显示位置（以及它们是数字或虚线样式）以及它们的大小。
   >    * 更改图像映射的高亮样式或用于热点的图标。
   >    * 在编辑查看器预设之前，请选择要作为预设基础的样式。 如果您不选择样式，则在开始编辑查看器预设时，如果您更改为其他预设，则会丢失所有更改。


   您还可以预览传送横幅的外观。 请参阅[（可选）预览传送横幅](#optional-previewing-carousel-banners)。

1. 完成后，点按&#x200B;**[!UICONTROL 保存]**。

## 将热点或图像映射添加到图像横幅{#adding-hotspots-or-image-maps-to-an-image-banner}

您可以使用传送集编辑器将热点或图像映射添加到横幅。

在添加热点或图像映射时，您可以将热点定义为“快速视图”弹出显示、超链接或体验片段。

请参阅[体验片段](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)。

>[!NOTE]
>
>将查看器嵌入体验片段时，不支持传送横幅中的社交媒体共享工具。
>
>要解决此问题，您可以使用或创建没有社交媒体共享工具的查看器预设。 此类查看器预设使您能够成功地将其嵌入到体验片段中。

在将热点或图像映射添加到图像时，请切记保存您的工作。 在当前创建/编辑会话中，页面右上角附近支持撤消和重做选项。

创建完传送横幅后，您可以选择使用“预览”来查看传送横幅对客户的显示方式。

请参阅[（可选）预览传送横幅。](#optional-previewing-carousel-banners)

>[!NOTE]
>
>在将热点添加到图像横幅时，热点信息会存储在相同的元数据位置 — 相对于图像的位置。 无论是交互式图像还是传送横幅，此点均为真。 此功能意味着您可以在任一查看器中轻松重复使用同一图像及其定义的热点数据。
但是，请注意，传送横幅支持图像上的图像映射，这些图像上可能还包含热点；交互式图像不会。 如果您要创建使用相同图像的交互式图像或传送横幅，请记住此提示。 请考虑改为使用同一图像的单独副本创建交互式图像和传送横幅。

>[!NOTE]
如果您正在编辑具有热点的交互式图像并裁剪图像，则您的热点将被删除。

<!-- See also [Adding Image Maps](/help/assets/image-maps.md). -->

**向图像横幅添加热点或图像映射**

1. 从资产中，导航到您要实现交互的传送集。
1. 选择传送集，然后点按&#x200B;**[!UICONTROL 编辑]**。 此时将打开传送查看器编辑器。
1. 选择要进行交互的幻灯片。
1. 在页面的左上角附近，点按&#x200B;**[!UICONTROL 热点]**&#x200B;或&#x200B;**[!UICONTROL 图像映射]**。
1. 执行下列操作之一：

   * 对于热点：在图像上，点按您希望显示热点的位置。
   * 对于图像映射：在图像上，单击，然后从左上角拖动到右下角以创建图像映射区域。 您可以通过拖动角来调整图像映射的大小。

   如有必要，将热点或图像映射拖到新位置。 或者，使用键盘箭头键控制选定热点的位置。 根据需要添加更多热点或图像映射。

   要删除热点或图像映射，请点按&#x200B;**[!UICONTROL 操作]**&#x200B;选项卡。在&#x200B;**[!UICONTROL 映射和热点]**&#x200B;标题下，从&#x200B;**[!UICONTROL 选定类型]**&#x200B;下拉列表中，选择要删除的热点或图像映射的名称。 点按菜单旁边的&#x200B;**[!UICONTROL 废纸篓]**&#x200B;图标，然后点按&#x200B;**[!UICONTROL 删除]**。

1. 在“名称”文本字段中，键入热点或图像映射的名称。 此名称也显示在&#x200B;**[!UICONTROL 映射和热点]**&#x200B;下拉列表中。 如果您决定在将来更改热点或图像映射，通过提供名称可以轻松地识别它。
1. 在&#x200B;**[!UICONTROL Actions]**&#x200B;选项卡中执行下列操作之一：

   * 点按&#x200B;**[!UICONTROL 快速视图]**。

      * 如果您是Experience Manager站点<!-- and Ecommerce-->客户，请点按产品选取器图标（放大镜）以打开选择产品页面。 要返回到传送横幅编辑器，请点按要使用的产品，然后点按页面右上角的复选标记。
      * 如果您不是Experience Manager站点<!-- or Ecommerce -->客户：

         * 定义变量。 请参阅[识别热点变量](#identifying-hotspot-and-image-map-variables)。
         * 然后，手动输入SKU值。 在“SKU值”文本字段中，键入产品的SKU（库存单位），即您所优惠的每个不同产品或服务的唯一标识符。 输入的SKU值会自动填充“快速视图”模板的变量部分。 系统现在可以将点按的热点与特定SKU的快速视图关联。
         * （可选）如果您必须在“快速”视图中使用其他变量来进一步标识产品，请点按&#x200B;**[!UICONTROL 添加常规变量]**。 在文本字段中，指定一个额外的变量。 例如，类别=Mens是一个添加的变量。

         * 有关详细信息，请参阅[使用选择器](/help/assets/dynamic-media/working-with-selectors.md)。
   * 点按&#x200B;**[!UICONTROL 超链接]**。

      * 如果您是AEM Sites客户，请点按站点选择器图标（文件夹）以导航到URL。

         >[!NOTE]
         如果您的交互式内容包含与相对URL(尤其是指向AEM Sites页面的链接)的链接，则无法使用基于URL的链接方法。

      * 如果您是独立客户，请在“href”文本字段中指定链接网页的完整URL路径。

   请确保指定是在新的浏览器选项卡（建议的默认选项卡）还是在同一选项卡中打开链接。

   有关详细信息，请参阅[使用选择器](/help/assets/dynamic-media/working-with-selectors.md)。

   * 点按&#x200B;**[!UICONTROL 体验片段]**。

      * 如果您是AEM Sites客户，请点按搜索图标（放大镜）以打开体验片段页面。 要返回到“热点”管理页面，请点按您要使用的体验片段，然后点按页面右上角的选择。
请参阅[体验片段](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)。

      * 指定在横幅上显示的体验片段的宽度和高度。

         >[!NOTE]
         将查看器嵌入体验片段时，不支持传送横幅中的社交媒体共享工具。
         要解决此问题，您可以使用或创建没有社交媒体共享工具的查看器预设。 此类查看器预设使您能够成功地将其嵌入到体验片段中。
   ![experience_fragment-carouselbanner](assets/experience_fragment-carouselbanner.png)

   您还可以预览传送横幅的外观。 请参阅[（可选）预览传送横幅](#optional-previewing-carousel-banners)。

1. 点按&#x200B;**[!UICONTROL 保存]**。
1. 发布传送集。 发布后会创建可在网站页面上使用的嵌入代码或URL。 如果您是Experience Manager站点客户，请直接将传送集添加到网页。

   请参阅[发布资产](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)。

   请参阅[将传送集添加到网站登陆页](#adding-a-carousel-banner-to-your-website-page)

## 编辑传送集{#editing-carousel-sets}

>[!NOTE]
必须将非管理用户添加到&#x200B;**[!UICONTROL dam-users]**&#x200B;组，才能创建或编辑传送横幅。 如果您在创建或编辑时遇到问题，请咨询系统管理员，他可以将您添加到&#x200B;**[!UICONTROL dam-users]**&#x200B;组。

您可以对传送集执行各种编辑任务，如：

* 向传送集添加幻灯片。 另请参阅[使用选择器](/help/assets/dynamic-media/working-with-selectors.md)。
* 在传送集中对幻灯片重新排序。
* 删除传送集中的资源。
* 应用查看器预设。
* 删除传送集。
* 添加或编辑热点和图像映射。 另请参阅[使用选择器](/help/assets/dynamic-media/working-with-selectors.md)。

**编辑传送集**

1. 执行下列任一操作：

   * 将鼠标悬停在传送集资产上，然后点按&#x200B;**[!UICONTROL 编辑]**（铅笔图标）。
   * 将鼠标悬停在传送集资产上，点按&#x200B;**[!UICONTROL 选择]**（复选标记图标），然后点按工具栏中的&#x200B;**[!UICONTROL 编辑]**。

   * 点按传送集资产，然后在页面的左上角点按&#x200B;**[!UICONTROL 编辑]**（铅笔图标）。

1. 要编辑传送集，请执行下列任一操作：

   * 要添加幻灯片，请点按&#x200B;**[!UICONTROL 添加幻灯片]**&#x200B;图标。 导航到要添加到该幻灯片的资产，然后点按或单击复选标记。
   * 要对幻灯片重新排序，请将幻灯片拖到新位置（选择重新排序图标以移动项目）。
   * 要添加热点或图像映射，请单击热点或图像映射图标，并参阅[添加热点和图像映射](#adding-hotspots-or-image-maps-to-an-image-banner)。
   * 要编辑轮盘集的外观或行为，请点按&#x200B;**[!UICONTROL 外观]**&#x200B;选项卡或&#x200B;**[!UICONTROL 行为]**&#x200B;选项卡，然后设置所需的选项。
   * 要编辑热点或图像映射，请在相应的幻灯片上选择热点或图像映射。 在&#x200B;**[!UICONTROL 操作]**&#x200B;选项卡下，进行更改。
   * 要删除幻灯片，请选择它，然后点按工具栏中的&#x200B;**[!UICONTROL 删除幻灯片]**。
   * 要应用预设，请点按页面右上角附近的&#x200B;**[!UICONTROL 预设]**&#x200B;下拉列表，然后选择查看器预设。
   * 要删除整个传送集，请导航到传送集，将其选中，然后点按&#x200B;**[!UICONTROL 删除]**。

   >[!NOTE]
   如果您正在编辑具有热点的交互式图像并裁剪图像，则您的热点将被删除。

## （可选）预览传送横幅{#optional-previewing-carousel-banners}

您可以使用预览来查看传送横幅对客户的外观。 使用预览还可以测试传送横幅的热点和图像映射，以确保它们按预期的方式工作。

当您对传送横幅满意时，可以发布它。
请参阅[在网页上嵌入视频查看器或图像查看器](/help/assets/dynamic-media/embed-code.md)。请参阅[将 URL 关联到您的 Web 应用程序](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)。如果您的交互式内容包含与相对URL(尤其是指向AEM Sites页面的链接)的链接，则无法使用基于URL的链接方法。
请参阅[将Dynamic Media资产添加到页面。](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)

您可以从传送编辑器（首选方法）或&#x200B;**[!UICONTROL 查看器]**&#x200B;预览中列表传送横幅。

**预览传送横幅**

1. 在&#x200B;**[!UICONTROL 资产]**&#x200B;中，导航到您已创建的现有传送横幅，然后点按以将其打开。
1. 点按&#x200B;**[!UICONTROL 编辑]**。
1. 在工具栏右角的查看器预设列表中，选择一个查看器以预览传送横幅。

   ![experience_fragment-carouselbanner-viewerdropdown](assets/experience_fragment-carouselbanner-viewerdropdown.png)

1. 点按&#x200B;**[!UICONTROL 预览]**。
1. 要测试其关联的操作，请点按图像上的热点或图像映射。

**从“查看器”预览传送横幅列表**

1. 在&#x200B;**[!UICONTROL 资产]**&#x200B;中，导航到您已创建的现有传送横幅，然后点按以将其打开。
1. 在预览页面的左上角附近，单击内容图标。
1. 在页面左侧面板的&#x200B;**[!UICONTROL 查看器]**&#x200B;列表中，点按要使用的传送横幅查看器预设的名称。
1. 要测试其关联的操作，请点按图像上的热点或图像映射。

## 发布传送横幅{#publishing-carousel-banners}

要使用传送，您必须发布它。 发布传送集时，将激活URL和嵌入代码。 它还将传送发布到Dynamic Media云，该云与CDN集成，可实现可扩展且高性能的投放。

>[!NOTE]
如果您将具有热点的现有交互式图像用于传送横幅，则必须在发布传送横幅后单独发布该交互式图像。
此外，如果您修改在传送横幅中使用的已发布交互式图像，则发布交互式图像，以便这些更改反映在传送横幅中。

有关如何发布传送横幅的信息，请参阅[发布Dynamic Media资产](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)。

## 将传送横幅添加到您的网站页面{#adding-a-carousel-banner-to-your-website-page}

在上传横幅图像以创建轮播后，将热点或图像映射（或两者）添加到横幅。 已发布传送集。 现在，您可以将其添加到现有网站页面。

>[!NOTE]
如果您是AEM Sites客户，则可以通过将交互式媒体组件拖动到页面来直接将传送横幅添加到页面。 请参阅[将Dynamic Media资产添加到页面。](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)

但是，如果您是独立的Experience Manager资产客户，则可以手动将传送横幅添加到您的网站登陆页。

1. 复制已发布的传送集的嵌入代码。
请参阅[在网页上嵌入视频查看器或图像查看器](/help/assets/dynamic-media/embed-code.md)。

1. 将您从Experience Manager资产中复制的嵌入代码添加到您的网页。
复制的嵌入代码是响应式的，因此会自动适合页面的嵌入区域。

## 将传送横幅与现有快速视图{#integrating-the-carousel-banner-with-an-existing-quickview}集成

注意：此步骤仅适用于您是独立的AEM Assets客户。

此过程的最后一步是将传送横幅与网站上现有的快速视图实施相集成。 每个快速视图实施都是独一无二的，需要一种特定的方法，通常需要前端IT人员的协助。

现有的“快速视图”实施通常表示按以下顺序在网页上发生的一系列相互关联的操作：

1. 用户在网站的用户界面上触发一个元素。
1. 前端代码根据在步骤1中触发的用户界面元素获取快速视图URL。
1. 前端代码使用在第 2 步获取的 URL 发送一个 Ajax 请求。
1. 后端逻辑将相应的快速视图数据或内容返回给前端代码。
1. 前端代码加载快速视图数据或内容。
1. （可选）前端代码将加载的快速视图数据转换为HTML表示形式。
1. 前端代码显示一个模态对话框或面板，并将 HTML 内容呈现在屏幕上以供最终用户查看。

这些调用不代表独立的公共API调用，网页逻辑可以从任意步骤调用这些调用。 相反，这些调用属于链式调用，即，每个后续步骤都隐藏在前一步的最后阶段（回调）。

当用户单击热点或图像映射时，轮盘横幅将替换第1步，并部分替换第2步时，查看器将处理此类交互。 查看器将返回一个事件到网页，其中包含之前添加的所有热点或图像映射数据。

在此类事件处理程序中，前端代码会执行下列操作：

* 监听轮播横幅发出的事件。
* 根据热点或图像映射数据构建快速视图URL。
* 触发从后端加载快速视图并在屏幕上显示它的过程。

AEM Assets返回的嵌入代码已经有一个已注释掉的可用事件处理程序。

因此，只需取消对该代码的注释，并用针对特定网页的代码来替换虚拟处理程序主体即可。

构建快速视图URL的过程与用于识别前面介绍的热点和图像映射变量的过程相反。

请参阅[识别热点和图像映射变量](#identifying-hotspot-and-image-map-variables)。

触发“快速视图URL”并激活“快速视图”面板的最后一步操作，极有可能需要IT部门的前端IT人员的协助。他们最了解如何通过拥有现成的快速视图URL从正确的步骤准确触发快速视图实施。

## 使用快速视图创建自定义弹出窗口{#using-quickviews-to-create-custom-pop-ups}

请参阅[使用快速视图创建自定义弹出窗口](/help/assets/dynamic-media/custom-pop-ups.md)。