---
title: 使用 Quickview 创建自定义弹出窗口
description: “了解在电子商务体验中如何使用默认的概览，在该体验中会显示一个弹出窗口，其中包含产品信息以促进购买。 您可以触发要在弹出窗口Windows®中显示的自定义内容。”
feature: Interactive Images,Interactive Videos,Carousel Banners
role: Admin,User
exl-id: c2bc6ec8-d46e-4681-ac3e-3337b9e6ae5c
source-git-commit: 77f1b744dabd72fc26d3b0607db9561e6cb7fa66
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 2%

---

# 使用概览创建自定义弹出窗口Windows® {#using-quickviews-to-create-custom-pop-ups}

默认的概览用于电子商务体验，其中会显示一个弹出窗口，其中包含产品信息以促进购买。 但是，您可以触发要在弹出窗口中显示的自定义内容。 根据您使用的查看器，客户可以选择热点、缩略图或图像映射，以查看信息或相关内容。

Dynamic Media中的以下查看器支持快速查看：

* 交互式图像（可选热点）
* 交互式视频（视频播放期间可选择的缩略图图像）
* 轮播横幅（可选热点或图像映射）

虽然每个查看器的功能不同，但在所有三个受支持的查看器中，创建概览的过程都是相同的。

**要使用概览创建自定义弹出窗口Windows®，请执行以下操作：**

1. 为上传的资产创建概览。

   通常，在编辑资产以用于所使用的查看器的同时，会创建一个概览。

   <table>
    <tbody>
    <tr>
    <td><strong>您使用的查看器</strong></td>
    <td><strong>要创建概览，请完成以下步骤</strong></td>
    </tr>
    <tr>
    <td>交互式图像</td>
    <td><a href="/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner" target="_blank">将热点添加到图像横幅</a>.</td>
    </tr>
    <tr>
    <td>交互式视频</td>
    <td><a href="/help/assets/dynamic-media/interactive-videos.md#adding-interactivity-to-your-video" target="_blank">为视频添加交互性</a>.</td>
    </tr>
    <tr>
    <td>传送横幅</td>
    <td><a href="/help/assets/dynamic-media/carousel-banners.md#adding-hotspots-or-image-maps-to-an-image-banner" target="_blank">将热点或图像映射添加到横幅</a>.<br /> </td>
    </tr>
    </tbody>
   </table>

1. 获取查看器嵌入代码以在您的网站中集成查看器。

   <table>
    <tbody>
    <tr>
    <td><strong>您使用的查看器</strong><br /> </td>
    <td><strong>要将查看器与您的网站集成，请完成以下步骤</strong></td>
    </tr>
    <tr>
    <td>交互式图像</td>
    <td><a href="/help/assets/dynamic-media/interactive-images.md#integrating-an-interactive-image-with-your-website" target="_blank">将交互式图像与您的网站集成</a>.<br /> </td>
    </tr>
    <tr>
    <td>交互式视频<br /> </td>
    <td><a href="/help/assets/dynamic-media/interactive-videos.md#integrating-an-interactive-video-with-your-website" target="_blank">将交互式视频与您的网站集成</a>.<br /> </td>
    </tr>
    <tr>
    <td>轮播横幅</td>
    <td><a href="/help/assets/dynamic-media/carousel-banners.md#adding-a-carousel-banner-to-your-website-page" target="_blank">将轮播横幅添加到您的网站页面</a>.<br /> </td>
    </tr>
    </tbody>
   </table>

1. 您使用的查看器必须知道如何使用概览。

   查看器使用名为的处理程序 `QuickViewActive`.

   **示例**
假定您在网页上对交互式图像使用了以下示例嵌入代码：

   ![chlimage_1-291](assets/chlimage_1-291.png)

   处理程序将使用加载到查看器中 `setHandlers`:

   `*viewerInstance*.setHandlers({ *handler 1*, *handler 2*}, ...`

   **使用上面的示例嵌入代码示例，您可以使用以下代码：**

   ```xml {.line-numbers}
   s7interactiveimageviewer.setHandlers({
       quickViewActivate": function(inData) {
           var sku=inData.sku;
           var genericVariable1=inData.genericVariable1;
           var genericVariable2=inData.genericVariable2;
          loadQuickView(sku,genericVariable1,genericVariable2);
       }
   })
   ```

   详细了解 `setHandlers()` 方法：

   * 交互式图像查看器 —  [塞特兰](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-sethandlers.html)
   * 交互式视频查看器 —  [塞特兰](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-sethandlers.html)

1. 现在，配置 `quickViewActivate` 处理程序。

   的 `quickViewActivate` 处理程序控制查看器中的概览。 处理程序包含变量列表和函数调用以与概览一起使用。 嵌入代码会为概览中设置的SKU变量提供映射。 还做了一个样本 `loadQuickView` 函数调用。

   **变量映射**
将网页中使用的变量映射到概览中包含的SKU值和通用变量：

   `var *variable1*= inData.*quickviewVariable*`

   提供的嵌入代码具有SKU变量的示例映射：

   `var sku=inData.sku`

   也从概览中映射其他变量，如下所示：

   ```xml {.line-numbers}
   var <i>variable2</i>= inData.<i>quickviewVariable2</i>
    var <i>variable3</i>= inData.<i>quickviewVariable3</i>
   ```

   **函数调用**
处理程序还需要函数调用，以便概览正常工作。 假定您的主机页面可以访问该函数。 嵌入代码提供了一个示例函数调用：

   `loadQuickView(sku)`

   示例函数调用假定函数 `loadQuickView()` 存在且可访问。

   详细了解 `quickViewActivate` 方法：

   * 交互式图像查看器 —  [事件回调](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-event-callbacks.html)
   * 交互式视频查看器 —  [事件回调](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-event-callbacks.html)
   * 交互式视频查看器中的交互式数据支持 —  [交互式数据支持](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-int-data-support.html)

1. 执行以下操作：

   * 取消对嵌入代码的setHandlers部分的注释。
   * 映射概览中包含的任何其他变量。

      * 更新 `loadQuickView(sku,*var1*,*var2*)` 调用。
   * 创建简单 `loadQuickView` ()函数。

      例如，以下内容会将SKU的值写入浏览器控制台：

   ```xml {.line-numbers}
   function loadQuickView(sku){
       console.log ("quickview sku value is " + sku);
   }
   ```

   * 将测试HTML页面上传到Web服务器并打开。

      快速视图中的变量已映射。 函数调用就绪。 浏览器控制台会将变量值写入浏览器控制台。 它使用提供的示例函数执行此操作。



1. 您现在可以使用函数在概览中调用一个简单的弹出窗口。 以下示例使用 `DIV` 来访问Advertising Cloud。
1. 设置弹出窗口的样式 `DIV` 以下方式。 根据需要添加其他样式。

   ```xml {.line-numbers}
   <style type="text/css">
       #quickview_div{
           position: absolute;
           z-index: 99999999;
           display: none;
       }
   </style>
   ```

1. 放置弹出窗口 `DIV` 在HTML页面的正文中。

   其中一个元素会使用ID进行设置，当用户调用概览时，该ID将随SKU值进行更新。 该示例还包含一个简单按钮，用于在弹出窗口可见后再次隐藏该弹出窗口。

   ```xml {.line-numbers}
   <div id="quickview_div" >
       <table>
           <tr><td><input id="btnClosePopup" type="button" value="Close"        onclick='document.getElementById("quickview_div").style.display="none"' /><br /></td></tr>
           <tr><td>SKU</td><td><input type="text" id="txtSku" name="txtSku"></td></tr>
       </table>
   </div>
   ```

1. 要在弹出窗口中更新SKU值，请添加函数。 将步骤5中创建的简单函数替换为以下内容，以使弹出窗口可见：

   ```xml {.line-numbers}
   <script type="text/javascript">
       function loadQuickView(sku){
           document.getElementById("txtSku").setAttribute("value",sku); // write sku value
           document.getElementById("quickview_div").style.display="block"; // show popup
       }
   </script>
   ```

1. 将测试HTML页面上传到Web服务器并打开。 查看器会显示弹出窗口 `DIV` 用户调用概览时。
1. **如何以全屏模式显示自定义弹出窗口**

   某些查看器（例如交互式视频查看器）支持以全屏模式显示。 但是，如果按照前面步骤中所述使用弹出窗口，则在全屏模式下，该弹出窗口会显示在查看器后面。

   要使弹出窗口以标准和全屏模式显示，请将弹出窗口附加到查看器容器。 在这种情况下，使用第二个处理程序方法， `initComplete`.

   的 `initComplete` 在查看器初始化后调用处理程序。

   ```xml {.line-numbers}
   "initComplete":function() { code block }
   ```

   详细了解 `init()` 方法：

   * 交互式图像查看器 —  [init](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-init.html)
   * 交互式视频查看器 —  [init](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-init.html)

1. 要将上述步骤中描述的弹出窗口附加到查看器，请使用以下代码：

   ```xml {.line-numbers}
   "initComplete":function() {
       var popup = document.getElementById('quickview_div');
       popup.parentNode.removeChild(popup);
       var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId();
       var inner_container = document.getElementById(sdkContainerId);
       inner_container.appendChild(popup);
   }
   ```

   在上述代码中，您已完成以下操作：

   * 已识别您的自定义弹出窗口。
   * 已从DOM中将其删除。
   * 已识别查看器容器。
   * 已将弹出窗口附加到查看器容器。

1. 您的整个setHandlers代码类似于以下代码（使用了交互式视频查看器）：

   ```xml {.line-numbers}
   s7interactivevideoviewer.setHandlers({
       "quickViewActivate": function(inData) {
           var sku=inData.sku;
           loadQuickView(sku);
   
       },
       "initComplete":function() {
           var popup = document.getElementById('quickview_div'); // get custom quick view container
           popup.parentNode.removeChild(popup); // remove it from current DOM
           var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId();
           var inner_container = document.getElementById(sdkContainerId);
           inner_container.appendChild(popup);
       }
   });
   ```

1. 加载处理程序后，可以初始化查看器：

   `*viewerInstance.*init()`

   **示例**
此示例使用交互式图像查看器。

   `s7interactiveimageviewer.init()`

   将查看器嵌入主机页面后，请确保已创建查看器实例。 此外，请确保在使用调用查看器之前加载了处理程序 `init()`.
