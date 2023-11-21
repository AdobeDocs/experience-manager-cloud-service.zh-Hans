---
title: 传送横幅
description: 了解如何在Dynamic Media中使用轮播横幅。
contentOwner: Rick Brough
feature: Carousel Banners
role: User
exl-id: 34541302-6610-4f5e-af93-c95328dda910
source-git-commit: 8ed477ec0c54bb0913562b9581e699c0bdc973ec
workflow-type: tm+mt
source-wordcount: '4534'
ht-degree: 1%

---

# 传送横幅{#carousel-banners}

轮播横幅通过轻松创建交互式轮播促销内容并将其交付到任何屏幕，使营销人员能够推动转化。

创建和修改促销横幅中提供的内容可能非常耗时，从而限制您快速发布新内容或使其更具针对性的能力。 轮播横幅允许您快速创建或修改旋转横幅，并添加交互功能，例如链接到产品详细信息或相关资源的热点。 您可以将这些内容交付到任何屏幕，从而更快地向市场提供新的促销内容。

轮播横幅由带有单词的横幅指定 **[!UICONTROL CAROUSELSET]**：

![chlimage_1-438](assets/chlimage_1-438.png)

在您的网站上，轮播横幅可以如下所示：

![chlimage_1-439](assets/chlimage_1-439.png)

在此，您可以通过选择编号来浏览图像。 此外，幻灯片会根据您可以自定义的时间间隔自动旋转。 传送横幅中的图像同时支持热点和图像映射。 用户可以选择或转到超链接或访问概览窗口。

在此示例中，用户已选择了一个图像映射并访问手套的“概览”窗口：

![chlimage_1-440](assets/chlimage_1-440.png)

## 观看如何创建轮播横幅 {#watch-how-carousel-banners-are-created}

观看演练 [如何创建轮播横幅](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveCarouselBanner) （持续时间：10分33秒）。 您还将了解如何预览、编辑和交付轮播横幅。

>[!NOTE]
>
>必须将非管理用户添加到 **[!UICONTROL dam-users]** 组才能创建或编辑轮播横幅。 如果您在创建或编辑时遇到问题，请咨询您的系统管理员，管理员可以将您添加到 **d[!UICONTROL am-users]** 组。

## 快速入门：轮播横幅 {#quick-start-carousel-banners}

要让您快速启动并运行，请执行以下操作：

1. [识别热点和图像映射变量](#identifying-hotspot-and-image-map-variables) (仅适用于使用Adobe Experience Manager Assets + Dynamic Media的客户)

   首先，确定现有快速视图实施使用的动态变量。 这样做有助于在Experience Manager Assets中的轮播横幅创建过程中正确输入热点和图像映射数据。

<!-- LEAVE; COMMERCE BEING ADDED AGAIN IN THE FUTURE

   >[!NOTE]
   >
   >If you are an Experience Manager Sites or Ecommerce customer, you can use the built-in feature to navigate to product pages and lookup the existing skus in the product catalog. You do not need to manually enter hotspot or image map variables.
   >
   >
   >If you are an Experience ManagerAssets and Dynamic Media customer, you will manually enter data for hotspots and image maps, and then integrate the published URL or Embed code with your third-party content management system.

-->

1. 可选：根据需要[创建轮播集查看器预设](/help/assets/dynamic-media/managing-viewer-presets.md)。

   如果您是管理员，则可以通过创建自己的轮盘查看器预设来自定义轮盘的行为和外观。 主要好处是，您可以对多个轮播重复使用此自定义查看器预设。 但是，用户可以选择在创作轮播时直接自定义轮播的行为和外观。 当您希望为给定的轮播提供特定设计时，首选使用此方法。

1. [上传图像横幅](#uploading-image-banners).

   上传要使其成为交互式内容的图像横幅。

1. [创建传送集](#creating-carousel-sets).

   在轮播集中，用户浏览横幅图像并选择热点或图像映射以访问相关内容。

   要在Assets中创建轮播集，请选择 **[!UICONTROL 创建]**，然后选择 **[!UICONTROL 传送集]**. 将资源添加到幻灯片并选择 **[!UICONTROL 保存]**. 您还可以直接在编辑器中编辑轮播集的外观和行为。

1. [将热点或图像映射添加到图像横幅](#adding-hotspots-or-image-maps-to-an-image-banner).

   将一个或多个热点或图像映射添加到图像横幅。 然后，将每个项目与操作（如链接、快速视图或体验片段）关联。 添加热点或图像映射后，可通过发布轮播集来完成此任务。 发布操作将创建可用于复制并应用于您的网站登陆页面的嵌入代码。

   请参阅 [（可选）预览轮播横幅](#optional-previewing-carousel-banners)  — 可选。 如果需要，您可以查看轮播集的表示形式并测试其交互性。

1. [发布轮播横幅](#publishing-carousel-banners).

   您可以像发布任何资源一样发布传送集。 在Assets中，导航到轮播集并将其选定，然后选择 **[!UICONTROL Publish]**. 发布轮播集将激活URL和嵌入字符串。

1. 执行下列操作之一：

   * [向您的网站页面添加轮播横幅](#adding-a-carousel-banner-to-your-website-page)您可以将复制的轮播横幅URL或嵌入代码添加到网站页面。

      * [将轮播横幅与现有快速视图集成](#integrating-the-carousel-banner-with-an-existing-quickview). 如果您使用的是第三方Web内容管理系统，则必须将新的轮播横幅与网站上现有的快速视图实施集成。

   * [在Experience Manager中将轮播横幅添加到您的网站](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md). 如果您是Experience Manager Sites客户，则可以使用交互式媒体组件将轮播集直接添加到页面。

如果必须编辑传送集，请参阅 [编辑传送集](#editing-carousel-sets). 此外，您还可以查看和编辑 [轮播集属性](/help/assets/manage-digital-assets.md#editing-properties).

## 识别热点和图像映射变量 {#identifying-hotspot-and-image-map-variables}

首先，确定现有快速视图实施使用的动态变量。 此方法可帮助您在Experience Manager Assets中的轮播集创建过程中正确输入热点或图像映射数据。

将热点或图像映射添加到横幅图像时，需要分配SKU（库存单位）。 您还可以为每个热点或图像映射分配可选的额外变量。 此类变量稍后用于匹配热点或图像映射与快速视图内容。

<!-- LEAVE; COMMERCE BEING ADDED LATER

>[!NOTE]
>
>If you are an Experience Manager Sites and/or Experience Manager Ecommerce customer, skip this step. You do not need to manually identify hotspot or image map variables; you can use the integration with Ecommerce for product integration. See information on [setting up eCommerce](/help/sites-cloud/administering/generic.md). In addition, you can use the Interactive component and add it to your web page.
>
>If you are an Experience Manager Assets or Media customer, you publish the URL or Embed code and then integrate with your third-party content management system and identify hotspots and image maps manually.

-->

正确标识要与热点或图像映射数据关联的变量的数量和类型很重要。 添加到横幅图像的每个热点或图像映射都必须包含足够的信息，以便明确标识现有后端系统中的产品。 同时，请确保每个热点或图像映射所包含的数据不超过所需的数量。 这是因为这会使数据录入过程过于复杂和进行中的热点或者图像映射管理更加容易出错。

有多种不同的方法可以识别一组要用于热点或图像映射数据的变量。

有时，咨询负责现有Quickview实施的IT专家就足够了。 他们可能会知道系统中用于标识快速视图的最小数据集。 但是，可以简单地分析前端代码的现有行为。

大多数概览实施都使用以下范例：

* 用户在网站上激活用户界面元素。例如，选择 **[!UICONTROL 概览]** 按钮。
* 如果需要，网站会向后端发送Ajax请求以加载概览数据或内容。
* 概览数据将转换为内容，为在网页上呈现做准备。
* 最后，前端代码在屏幕上以可视方式呈现此类内容。

然后，方法是访问实施概览功能的现有网站的不同区域。 然后触发概览并获取网页发送的Ajax URL，以加载概览数据或内容。

通常，您无需使用任何专门的调试工具。 现代Web浏览器的功能是Web检查器，这些检查器可以完成适当的工作。 以下是一些包含Web检查器的Web浏览器示例：

* 要在Google Chrome中查看所有传出的HTTP请求，请按F12 (Windows®)或Command-Option-I (Mac)打开开发人员工具面板。 选择“网络”选项卡。
* 在Firefox中，您可以通过按F12 (Windows®)或Command-Option-I (Mac)来激活Firebug插件。 使用其“网络”选项卡，或使用内置的“检查器”工具及其“网络”选项卡。

在浏览器中打开网络监视时，将触发页面上的快速视图。

现在，在网络日志中找到快速视图Ajax URL，并复制记录的URL以供将来分析。 通常，在触发概览时，会向服务器发送大量请求。 通常，快速视图Ajax URL是列表中的第一个页面之一。 它具有复杂的查询字符串部分或路径，并且其响应MIME类型是 `text/html`， `text/xml`，或 `text/javascript`.

在此过程中，请务必访问网站的不同区域，以及不同的产品类别和类型。 原因是快速视图URL具有给定网站类别所共有的部分，但只有在访问网站的其他区域时才发生更改。

最简单的例子是，概观URL中的唯一变量部分是产品SKU。 在这种情况下，将hotspot或图像映射添加到横幅图像时，SKU值是唯一需要的数据块。

但是，在复杂的情况下，除了SKU之外，快速视图URL还具有不同的变化元素。 其中一些元素包括类别ID、颜色代码、大小代码等。 在此类情况下，每个元素都是热点中的单独变量，或者轮播横幅功能中的图像映射数据定义。

请考虑以下概览示例URL及其生成的热点或图像映射变量：

<table>
 <tbody>
  <tr>
   <td>单个SKU，在查询字符串中找到。</td>
   <td><p>记录的快速视图URL包括：</p>
    <ul>
     <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>URL中的唯一变量部分是 <code>productId=</code> 查询字符串参数，它显然是一个SKU值。 因此，热点或图像映射只需要使用如下值填充的SKU字段 <code>866558,</code> <code>1196184,</code> <code>1081492,</code> <code>1898294.</code></p> </td>
  </tr>
  <tr>
   <td>单个SKU，可在URL路径中找到。</td>
   <td><p>记录的概览URL包括：</p>
    <ul>
     <li><p><code>https://server/product/6422350843</code></p> </li>
     <li><p><code>https://server/product/1607745002</code></p> </li>
     <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>变量部分位于路径的最后一部分，它成为热点/图像映射的SKU值：<strong><code>6422350843</code>， <code>1607745002,</code> </strong><code>0086724882.</code></p> </td>
  </tr>
  <tr>
   <td>查询字符串中的SKU和类别ID。</td>
   <td><p>记录的快速视图URL包括：</p>
    <ul>
     <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
     <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
     <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>在这种情况下，URL包含两个不同的部分。 SKU存储在 <code>prodId</code> 参数和类别ID存储在 <code>category=</code>参数。</p> <p>因此，热点/图像映射定义是对。 即，一个SKU值和一个名为的额外变量 <code>categoryId</code>. 生成的对如下所示：</p>
    <ul>
     <li><p>SKU是 <strong><code>305466</code></strong> 和 <code>categoryId</code> 是 <code>1100004</code>.</p> </li>
     <li><p>SKU是 <strong><code>310181</code></strong> 和 <code>categoryId</code> 是 <strong><code>1100004</code></strong>.</p> </li>
     <li><p>SKU是 <strong><code>308706</code></strong> 和 <code>categoryId</code> 是 <strong><code>1740148</code></strong>.</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 上传图像横幅 {#uploading-image-banners}

如果您已经上传了要使用的图像，请前进到下一步， [创建传送集](#creating-carousel-sets). 启用Dynamic Media后，必须上传轮播中使用的图像。

要上传图像横幅，请参阅 [上传资源](/help/assets/manage-digital-assets.md).

## 创建传送集 {#creating-carousel-sets}

>[!NOTE]
>
>必须将非管理用户添加到 **[!UICONTROL dam-users]** 组才能创建或编辑轮播横幅。 如果您在创建或编辑时遇到问题，请咨询您的系统管理员，管理员可以将您添加到 **[!UICONTROL dam-users]** 组。

**要创建传送集，请执行以下操作：**

1. 在Assets中，导航到要创建轮播集的文件夹，然后转到 **[!UICONTROL 创建>轮播集]**.
1. 在“轮播横幅编辑器”页面上，选择 **[!UICONTROL 点按以打开资产选择器]** 以选择第一张幻灯片的图像。

   在“轮播横幅编辑器”页面上，执行以下任一操作：

   * 在页面的左上角附近，选择 **[!UICONTROL 添加幻灯片]** 图标。

   * 在页面中间附近，选择 **[!UICONTROL 点按以打开资产选择器]**.

   选择以选择要包含在轮播集中的资源。 选定资源上有一个复选标记图标。 完成后，在页面的右上角附近，选择 **[!UICONTROL 选择]**.

   借助资产选择器，您可以通过键入关键字并选择 **[!UICONTROL 返回]**. 您还可以应用过滤器来优化搜索结果。您可以按路径、收藏集、文件类型和标记进行过滤。选择过滤器，然后选择 **[!UICONTROL 筛选]** 图标。 通过选择视图图标并选择更改视图 **[!UICONTROL 列视图]**， **[!UICONTROL 卡片视图]**，或 **[!UICONTROL 列表视图]**.

   请参阅 [使用选择器](/help/assets/dynamic-media/working-with-selectors.md) 以了解更多信息。

1. 继续添加幻灯片，直到在轮播集中添加了所有要旋转的图像为止。
1. （可选）执行以下任一操作：

   * 如有必要，请拖动幻灯片以重新排序集合列表中的图像。
   * 要删除图像，请选择该图像，然后选择 **[!UICONTROL 删除幻灯片]** 工具栏中。

   * 要应用预设，请在页面右上角附近选择预设下拉列表，然后选择要应用于该设置的预设。

   要删除幻灯片，请选择幻灯片。 在工具栏上，选择 **[!UICONTROL 删除幻灯片]** 工具栏上。 要移动幻灯片，请选择重新排序图标并移动到所需位置。

1. 在幻灯片中添加图像后，您可以向图像添加热点、图像映射，或同时添加这两者。 请参阅 [将热点或图像映射添加到图像横幅](#adding-hotspots-or-image-maps-to-an-image-banner).
1. 您可以更改轮播集的视觉设计和行为。 选择 **[!UICONTROL 行为]** 和 **[!UICONTROL 外观]** 选项卡。 请参阅 [管理查看器预设](/help/assets/dynamic-media/viewer-presets.md) 有关如何使用查看器编辑器的更多信息。

   >[!NOTE]
   >
   >对于轮播横幅，您可以调整以下内容：
   >
   >* 图像显示的持续时间。 默认情况下，每个图像会显示9秒。
   >* 动画. 默认情况下，每个幻灯片过渡都是淡入淡出。 您可以将其更改为幻灯片过渡。
   >* 按钮的样式。 通过选择每个点或数字，用户可以旋转横幅。 您可以更改设置指示器按钮的显示位置（以及数字或点线样式）和大小。
   >* 更改图像映射的高亮样式或热点图标。
   >* 在编辑查看器预设之前，请选择预设所基于的样式。 如果未选择样式，则在开始编辑查看器预设时，如果更改为其他预设，则会丢失所有更改。

   您还可以预览轮播横幅的外观。 请参阅 [（可选）预览轮播横幅](#optional-previewing-carousel-banners).

1. 选择 **[!UICONTROL 保存]** 完成后。

## 将热点或图像映射添加到图像横幅 {#adding-hotspots-or-image-maps-to-an-image-banner}

您可以使用轮播集编辑器将热点或图像映射添加到横幅中。

添加热点或图像映射时，可以将它们定义为快速视图弹出显示、超链接或体验片段。

请参阅 [体验片段](/help/sites-cloud/authoring/fundamentals/experience-fragments.md).

>[!NOTE]
>
>将查看器嵌入体验片段时，不支持轮播横幅中的社交媒体共享工具。
>
>要解决此问题，您可以使用或创建没有社交媒体共享工具的查看器预设。 通过此类查看器预设，可成功地将其嵌入体验片段中。

将热点或图像映射添加到图像时，请记得保存所做的工作。 在当前创建/编辑会话期间，支持页面右上角附近的“撤消”和“重做”选项。

创建完轮播横幅后，您可以选择使用预览来查看向客户展示轮播横幅的方式。

请参阅 [（可选）预览轮播横幅](#optional-previewing-carousel-banners).

>[!NOTE]
>
>在向图像横幅添加热点时，热点信息将存储在相对于图像位置的同一元数据位置。 无论它是交互式图像还是轮播横幅，该观点都正确。 这项功能意味着您可以在任一查看器中轻松重用同一图像，及其定义的热点数据。
>
但是，请注意，轮播横幅支持在可能还包含热点的图像上进行图像映射；而交互式图像则不支持。 如果您打算创建使用相同图像的交互式图像或轮播横幅，请记住此提示。 请考虑改用同一图像的单独副本来创建交互式图像和轮播横幅。

>[!NOTE]
>
如果您正在编辑具有热点的交互式图像并裁切图像，则将删除您的热点。

<!-- See also [Adding Image Maps](/help/assets/image-maps.md). -->

**要将热点或图像映射添加到图像横幅，请执行以下操作：**

1. 在Assets中，导航到要使其成为交互式内容的轮播集。
1. 选择轮播集并选择 **[!UICONTROL 编辑]**. 此时将打开轮播查看器编辑器。
1. 选择要使其成为交互式幻灯片的幻灯片。
1. 在页面的左上角附近，选择 **[!UICONTROL 热点]** 或 **[!UICONTROL 图像映射]**.
1. 执行以下任一操作：

   * 对于热点：在图像上，选择要显示热点的位置。
   * 对于图像映射：在图像上，从左上角拖动到右下角以创建图像映射区域。 您可以通过拖动角来调整图像映射的大小。

   如有必要，请将热点或图像映射拖动到新位置。 或者，使用键盘箭头键控制选定热点的位置。 根据需要添加更多热点或图像映射。

   要删除热点或图像映射，请选择 **[!UICONTROL 操作]** 选项卡。 在 **[!UICONTROL 映射和热点]** 标题，从 **[!UICONTROL 选定类型]** 在下拉列表中，选择要删除的热点或图像映射的名称。 选择 **[!UICONTROL 垃圾桶]** 图标，然后选择 **[!UICONTROL 删除]**.

1. 在“名称”文本字段中，键入热点或图像映射的名称。 此名称还会显示在 **[!UICONTROL 映射和热点]** 下拉列表。 提供名称可让您在决定将来更改热点或图像映射时轻松识别它。
1. 在中执行以下操作之一 **[!UICONTROL 操作]** 选项卡：

   * 选择 **[!UICONTROL 概览]**.

      * 如果您是Experience Manager Sites <!-- and Ecommerce--> ，选择产品选取器图标（放大镜）以打开“选择产品”页面。 要返回到轮播横幅编辑器，请选择要使用的产品，然后选择页面右上角的复选标记。
      * 如果您不是Experience Manager Sites <!-- or Ecommerce --> 客户：

         * 定义变量。 请参阅 [识别热点变量](#identifying-hotspot-and-image-map-variables).
         * 然后，手动输入SKU值。 在“SKU值”文本字段中，键入产品的SKU（库存单位），它是您提供的每个不同产品或服务的唯一标识符。 输入的SKU值将自动填充快速视图模板的变量部分。 系统现在知道将选定的热点与特定SKU的快速视图相关联。
         * （可选）如果快速视图中存在必须用来进一步标识产品的其他变量，请选择 **[!UICONTROL 添加常规变量]**. 在文本字段中，指定一个额外的变量。 例如， category=Mens是一个添加的变量。

         * 请参阅 [使用选择器](/help/assets/dynamic-media/working-with-selectors.md) 以了解更多信息。

   * 选择 **[!UICONTROL 超链接]**.

      * 如果您是Experience Manager Sites客户，请选择站点选择器图标（文件夹）以导航到URL。

        >[!NOTE]
        >
        如果您的交互式内容包含具有相对URL的链接，尤其是指向Experience Manager Sites页面的链接，则基于URL的链接方法不可用。

      * 如果您是独立客户，请在href文本字段中指定链接网页的完整URL路径。

   请确保您指定是在新的浏览器选项卡（推荐的默认值）中还是同一选项卡中打开链接。

   请参阅 [使用选择器](/help/assets/dynamic-media/working-with-selectors.md) 以了解更多信息。

   * 选择 **[!UICONTROL 体验片段]**.

      * 如果您是Experience Manager Sites客户，请选择“搜索”图标（放大镜）以打开“体验片段”页面。 要返回热点管理页面，请选择要使用的体验片段，然后在该页面的右上角选择 **[!UICONTROL 选择]**.
请参阅 [体验片段](/help/sites-cloud/authoring/fundamentals/experience-fragments.md).

      * 指定体验片段在横幅上显示的宽度和高度。

        >[!NOTE]
        >
        将查看器嵌入体验片段时，不支持轮播横幅中的社交媒体共享工具。
        >
        要解决此问题，您可以使用或创建没有社交媒体共享工具的查看器预设。 通过此类查看器预设，可成功地将其嵌入体验片段中。

   ![experience_fragment-carouselbanner](assets/experience_fragment-carouselbanner.png)

   您还可以预览轮播横幅的外观。 请参阅 [（可选）预览轮播横幅](#optional-previewing-carousel-banners).

1. 选择&#x200B;**[!UICONTROL 保存]**。
1. 发布轮播集。 发布会创建可在网站页面上使用的嵌入代码或URL。 如果您是Experience Manager Sites客户，请直接将轮播集添加到您的网页。

   请参阅 [发布资源](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

   请参阅 [将轮播集添加到您的网站登陆页面](#adding-a-carousel-banner-to-your-website-page)

## 编辑传送集 {#editing-carousel-sets}

>[!NOTE]
>
必须将非管理用户添加到 **[!UICONTROL dam-users]** 组才能创建或编辑轮播横幅。 如果您在创建或编辑时遇到问题，请咨询您的系统管理员，管理员可以将您添加到 **[!UICONTROL dam-users]** 组。

您可以对轮播集执行各种编辑任务，如下所示：

* 将幻灯片添加到轮播集。 另请参阅 [使用选择器](/help/assets/dynamic-media/working-with-selectors.md).
* 重新排列轮播集中的幻灯片。
* 删除轮播集中的资源。
* 应用查看器预设。
* 删除轮播集。
* 添加或编辑热点和图像映射。 另请参阅 [使用选择器](/help/assets/dynamic-media/working-with-selectors.md).

**要编辑传送集，请执行以下操作：**

1. 执行以下任一操作：

   * 将鼠标悬停在轮播集资源上，然后选择 **[!UICONTROL 编辑]** （铅笔图标）。
   * 将鼠标悬停在轮播集资源上，选择 **[!UICONTROL 选择]** （复选标记图标），然后在工具栏中选择 **[!UICONTROL 编辑]**.

   * 选择一个轮播集资源，然后在页面的左上角选择 **[!UICONTROL 编辑]** （铅笔图标）。

1. 要编辑轮播集，请执行以下任一操作：

   * 要添加幻灯片，请选择 **[!UICONTROL 添加幻灯片]** 图标。 导航到要添加到该幻灯片的资产，然后选择复选标记。
   * 要重新排序幻灯片，请将幻灯片拖到新位置（选择重新排序图标以移动项目）。
   * 要添加热点或图像映射，请选择热点或图像映射图标并参阅 [将热点和图像映射添加到图像横幅](#adding-hotspots-or-image-maps-to-an-image-banner).
   * 要编辑轮播集的外观或行为，请选择 **[!UICONTROL 外观]** 制表符或 **[!UICONTROL 行为]** 选项卡，然后设置所需的选项。
   * 要编辑热点或图像映射，请在相应的幻灯片上选择一个热点或图像映射。 在 **[!UICONTROL 操作]** 选项卡，进行更改。
   * 要删除幻灯片，请选择它，然后选择 **[!UICONTROL 删除幻灯片]** 工具栏中。
   * 要应用预设，请选择页面右上角附近的 **[!UICONTROL 预设]** 下拉列表，然后选择查看器预设。
   * 要删除整个轮播集，请导航到该轮播集，选择它，然后选择 **[!UICONTROL 删除]**.

   >[!NOTE]
   >
   如果您正在编辑具有热点的交互式图像并裁切图像，则将删除您的热点。

## （可选）预览轮播横幅 {#optional-previewing-carousel-banners}

您可以使用“预览”来查看向客户显示的轮播横幅。 使用预览，您还可以测试轮播横幅的热点和图像映射，以确保它们按预期运行。

如果对轮播横幅满意，则可以发布该横幅。
请参阅 [在网页上嵌入视频查看器或图像查看器](/help/assets/dynamic-media/embed-code.md).
请参阅 [将URL链接到您的Web应用程序](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md). 如果您的交互式内容包含具有相对URL的链接，尤其是指向Experience Manager Sites页面的链接，则基于URL的链接方法不可用。
请参阅 [将Dynamic Media资源添加到页面](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

您可以从轮播编辑器（首选方法）预览轮播横幅，也可以从 **[!UICONTROL 查看器]** 列表。

**要选择性地预览轮播横幅，请执行以下操作：**

1. 在 **[!UICONTROL 资产]**，导航到您创建的现有轮播横幅，然后选择以将其打开。
1. 选择&#x200B;**[!UICONTROL 编辑]**。
1. 在工具栏右角的查看器预设列表中，选择一个查看器以预览轮播横幅。

   ![experience_fragment-carouselbanner-viewerdropdown](assets/experience_fragment-carouselbanner-viewerdropdown.png)

1. 选择&#x200B;**[!UICONTROL 预览]**。
1. 要测试其关联的操作，请选择图像上的热点或图像映射。

**要从查看器列表中预览轮播横幅，请执行以下操作：**

1. 在 **[!UICONTROL 资产]**，导航到您创建的现有轮播横幅，然后选择以将其打开。
1. 在“预览”页面的左上角附近，选择“内容”图标。
1. 在 **[!UICONTROL 查看器]** 在页面左侧的面板中，选择要使用的轮播横幅查看器预设的名称。
1. 要测试其关联的操作，请选择图像上的热点或图像映射。

## 发布轮播横幅 {#publishing-carousel-banners}

要使用轮播，您必须发布它。 发布轮播集将激活URL和嵌入代码。 此外，它还会将轮播发布到Dynamic Media云，该云与CDN集成以实现可扩展的高性能交付。

>[!NOTE]
>
如果为轮播横幅使用带热点的现有交互式图像，则必须在发布轮播横幅后单独发布交互式图像。
>
此外，如果修改在轮播横幅中使用的预先存在的已发布交互式图像，请发布该交互式图像，以便这些更改会反映在轮播横幅中。

请参阅 [发布Dynamic Media资源](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md) 有关如何发布轮播横幅的信息。

## 向您的网站页面添加轮播横幅 {#adding-a-carousel-banner-to-your-website-page}

上传横幅图像以创建轮播后，将热点或图像映射（或同时添加两者）添加到横幅。 已发布轮播集。 您现在可以将其添加到现有网站页面了。

>[!NOTE]
>
如果您是Experience Manager Sites客户，则可以通过将交互式媒体组件拖动到页面，将轮播横幅直接添加到页面。 请参阅 [将Dynamic Media资源添加到页面](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

但是，如果您是独立的Experience Manager Assets客户，则可以手动将轮播横幅添加到网站登陆页面。

1. 复制已发布的轮播集的嵌入代码。
请参阅 [在网页上嵌入视频查看器或图像查看器](/help/assets/dynamic-media/embed-code.md).

1. 将您从Experience Manager Assets复制的嵌入代码添加到您的网页。
复制的嵌入代码是响应式的，因此会自动适应页面的嵌入区域。

## 将轮播横幅与现有的概览集成 {#integrating-the-carousel-banner-with-an-existing-quickview}

注意：仅当您是独立的Experience Manager Assets客户时，此步骤才适用。

此过程的最后一步是将轮播横幅与网站上现有的概览实施集成。 每个快速视图实施都是独一无二的，需要一种通常需要前端IT人员帮助的特定方法。

现有的概览实施通常表示在网页上发生的一系列相互关联的操作，顺序如下：

1. 用户在网站的用户界面中触发元素。
1. 前端代码根据步骤1中触发的用户界面元素获取快速视图URL。
1. 前端代码使用在步骤2中获取的URL发送Ajax请求。
1. 后端逻辑将相应的快速视图数据或内容返回给前端代码。
1. 前端代码加载快速视图数据或内容。
1. 前端代码可以选择将加载的快速视图数据转换为HTML表示形式。
1. 前端代码显示一个模式对话框或面板，并在屏幕上为用户呈现HTML内容。

这些调用不代表网页逻辑可以从任意步骤中调用的独立公共API调用。 相反，它是一个链接调用，其中每个下一步都隐藏在上一步的最后阶段（回调）中。

在轮播横幅替换步骤1或部分步骤2的同时，当用户选择热点或图像映射时，这种交互由查看器处理。 查看器会向网页返回一个事件，其中包含之前添加的所有热点或图像映射数据。

在此类事件处理程序中，前端代码执行以下操作：

* 侦听轮播横幅发出的事件。
* 根据热点或图像映射数据构造快速视图URL。
* 触发从后端加载快速视图并在屏幕上呈现以供显示的过程。

Experience Manager Assets返回的嵌入代码已具有标记为注释掉的现成事件处理程序。

因此，只需取消注释代码，并用特定网页特定的代码替换虚拟处理程序主体即可。

构建快速视图URL的过程与之前用于识别热点和图像映射变量的过程相反。

请参阅 [识别热点和图像映射变量](#identifying-hotspot-and-image-map-variables).

触发快速视图URL和激活快速视图面板的最后一步很可能需要IT部门的前端IT人员的帮助。 他们最了解如何通过适当的步骤准确触发快速视图实施，拥有现成的快速视图URL。

## 使用Quickview创建自定义弹出窗口® {#using-quickviews-to-create-custom-pop-ups}

请参阅 [使用Quickview创建自定义弹出窗口®](/help/assets/dynamic-media/custom-pop-ups.md).
