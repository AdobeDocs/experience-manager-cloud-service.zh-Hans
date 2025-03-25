---
title: 将 URL 关联到您的 Web 应用程序
description: 了解如何在Dynamic Media中将URL链接到Web应用程序。
contentOwner: Rick Brough
feature: Publishing,Upload,Viewer Presets,Image Presets,Video
role: User
exl-id: 3cd3f4d5-ebf0-4318-9a0d-1ea69453d57b
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '1281'
ht-degree: 4%

---

# 将 URL 关联到您的 Web 应用程序 {#linking-urls-to-your-web-application}

您的网站和应用程序通过URL调用访问Dynamic Media服务。 发布资产后，Dynamic Media会激活引用该资产的URL字符串。 您可以将这些URL粘贴到Web浏览器中进行测试。

仅当您&#x200B;*不是*&#x200B;使用Adobe Experience Manager作为您的WCM时，才会链接到URL。 当您要以弹出窗口或模式窗口形式交付视频播放器时，将使用链接（与嵌入）。 如果您将Experience Manager用作WCM，[请直接在页面上添加资源](adding-dynamic-media-assets-to-pages.md)。

要将这些URL字符串放置在网页和应用程序中，请从Dynamic Media复制它们。

>[!NOTE]
>
>URL字符串仅适用于资产的动态演绎版。 它们当前不适用于位于DAM中的静态资产，也不适用于Dynamic Media服务器。 对于静态的演绎版，不会显示URL按钮。

另请参阅[在网页上嵌入视频或图像查看器](embed-code.md)。

另请参阅[将YouTube URL链接到您的Web应用程序](video.md)。

另请参阅[为响应式网站传送优化的图像](responsive-site.md)。

另请参阅[上传Assets](/help/assets/manage-digital-assets.md#uploading-assets)。

## 获取资产的URL {#obtaining-a-url-for-an-asset}

您可以获取由图像预设或查看器预设生成的URL字符串。 复制URL后，该URL会登陆剪贴板，以便您可以根据需要将其粘贴到网站或应用程序中的页面。

>[!NOTE]
>
>在发布所选资产之前，无法复制URL。 此外，还必须发布查看器预设或图像预设。
>
>请参阅[发布Assets](publishing-dynamicmedia-assets.md)。
>
>请参阅[发布查看器预设](managing-viewer-presets.md#publishing-viewer-presets)。
>
>请参阅[发布图像预设](managing-image-presets.md#publishing-image-presets)。

您可以通过多种不同的方式获取URL字符串。 但是，下面的步骤只向您显示一种您可以使用的方法。

**要获取资产的URL：**

1. 导航到要复制其图像预设URL或查看器预设URL的&#x200B;*已发布*&#x200B;资产，然后选择资产以将其打开。

   请注意，只有在首次&#x200B;*发布*&#x200B;资产&#x200B;*后*，才可复制 URL。此外，还必须发布查看器预设或图像预设。

   请参阅[发布Assets](publishing-dynamicmedia-assets.md)。

   请参阅[发布查看器预设](managing-viewer-presets.md#publishing-viewer-presets)。

   请参阅[发布图像预设](managing-image-presets.md#publishing-image-presets)。

1. 根据您选择的资产，执行以下操作之一：

   * 如果您选择了图像，请在下拉菜单中选择&#x200B;**[!UICONTROL 格式副本]**。

     在&#x200B;**[!UICONTROL 动态]**&#x200B;标题下，选择一个预设名称，以在右框架中查看其演绎版。 如有必要，请滚动格式副本列表以查看动态标题。

     在左边栏底部，选择&#x200B;**[!UICONTROL URL]**。

     ![chlimage_1-270](assets/chlimage_1-270.png)

   * 如果您在下拉菜单中选择了旋转集、图像集、轮播集或视频，请选择&#x200B;**[!UICONTROL 查看器]**。

     在左边栏中，选择一个查看器预设名称。 将在单独的页面中打开集合或视频的预览。

     在左边栏的底部，选择&#x200B;**[!UICONTROL URL]**。

     ![chlimage_1-271](assets/chlimage_1-271.png)

1. 要预览资源或添加到Web内容页面，请选择文本并将其复制到Web浏览器。

   要退出URL窗口，请选择&#x200B;**[!UICONTROL X]**&#x200B;或选择&#x200B;**[!UICONTROL 关闭]**。

## 获取静态资源的URL {#obtaining-a-url-for-a-static-asset}

Dynamic Media支持静态资源的交付，而静态资源不仅仅是图像和视频的其他资源。 支持的静态资产交付格式包括：

* 三维文件
* GIF动画
* 音频文件
* CSS
* JavaScript（当您的公司配置有自己的域时）
* PDF
* SVG
* XML
* ZIP

**要获取静态资源的URL：**

1. 导航到要复制其URL的&#x200B;*已发布*&#x200B;静态资源，然后选择该资源以将其打开。

   请记住，在您首次&#x200B;*发布*&#x200B;静态资产后&#x200B;*后，只能复制*&#x200B;的URL。

   请参阅[发布Assets](publishing-dynamicmedia-assets.md)。

1. 使用以下任意方法获取已发布的静态资源的URL：

   * `The URL of the published static is the following:`

      * `https://*<server_name>*/is/content/*<company_name>*/*<static_asset_filename>*.*<extension>*`

        例如 `https://aem.com/is/content/adobe/image.gif`。

   * 选择&#x200B;**[!UICONTROL 资源]** > **[!UICONTROL 动态演绎版]**，然后选择静态资源的动态演绎版并复制URL。

     更改复制的URL以在路径中使用`is/content`而不是`is/image/`。

## 获取已发布视频演绎版的视频URL {#obtaining-a-video-url-for-a-published-video-rendition}

1. 在Experience Manager中，导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 云]** > **[!UICONTROL 云服务]**。
1. 在&#x200B;**[!UICONTROL 云服务]**&#x200B;页面上，向下滚动到&#x200B;**[!UICONTROL Dynamic Media云服务]**&#x200B;标题，然后选择&#x200B;**[!UICONTROL 显示配置]**。
1. 在&#x200B;**[!UICONTROL 可用配置]**&#x200B;下，选择所需配置的名称。

1. 在&#x200B;**[!UICONTROL Dynamic Media云设置]**&#x200B;页面的&#x200B;**[!UICONTROL 视频服务URL]**&#x200B;下，复制整个URL路径。 在稍后的步骤中，您需要复制的URL路径。

   例如，URL路径可能类似于以下内容：

   `https://s7athens.macromedia.com:9090/DMGateway/`

   （以上路径仅供解释；它不是您复制的实际路径。）

1. 在&#x200B;**[!UICONTROL 注册 ID]** 下，复制 ID 最后一部分中的客户名称。

   例如，如果注册ID为`87654321|MyCompany`，则客户名称将为`MyCompany`。

1. 在页面的左上角附近，选择&#x200B;**[!UICONTROL Cloud Services]**，然后选择Experience Manager图标并导航到&#x200B;**[!UICONTROL 常规]** > **[!UICONTROL CRXDE Lite]**。
1. 从JCR (Java™内容存储库)中向下复制整个视频演绎版路径。

   例如，视频的演绎版路径可能类似于以下内容：

   `/_renditions_/0bd/0bd28743-a616-4fe6-92aa-6eae7c2112f/avs/Momentum_1080-0x720-2600k.mp4`

   （以上路径仅供解释；它不是您复制的实际路径。）

1. 要形成完整的URL路径，请按照以下顺序排列复制的信息：

   `<Video_Service_URL>/public/<Customer_name_from_Registration_ID>/<Video_rendition_path>`

   例如，使用上述步骤中的示例路径和示例客户名称，完整路径如下所示：

   `https://s7athens.macromedia.com:9090/DMGateway/public/MyCompany/_renditions_/0bd/0bd28743-a616-4fe6-92aa-6eae7c2112ff/avs/Momentum_1080-0x720-2600k.mp4`

   此路径是已发布视频演绎版的完整视频URL。

## 获取用于自适应比特率流的视频URL (HLS) {#obtaining-a-video-url-for-adaptive-streaming-hls}

1. 在Experience Manager中，导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 云]** > **[!UICONTROL 云服务]**。
1. 在&#x200B;**[!UICONTROL 云服务]**&#x200B;页面上，向下滚动到&#x200B;**[!UICONTROL Dynamic Media云服务]**&#x200B;标题，然后选择&#x200B;**[!UICONTROL 显示配置]**。
1. 在&#x200B;**[!UICONTROL 可用配置]**&#x200B;下，选择所需配置的名称。
1. 在&#x200B;**[!UICONTROL Dynamic Media云服务设置]**&#x200B;页面上，执行以下操作：

   * 在&#x200B;**[!UICONTROL 视频服务URL]**&#x200B;下，复制整个URL路径。 在稍后这些步骤中，您需要复制的URL路径。 例如，URL路径可能类似于以下内容：

   `https://gateway-na.assetsadobe.com/DMGateway/`

   （以上路径仅供解释；它不是您复制的实际路径。）

   * 在&#x200B;**[!UICONTROL 注册ID]**&#x200B;下，复制ID最后一部分中的客户名称。 在稍后这些步骤中，您需要复制的客户名称。

     例如，如果注册ID为`87654321|demoCo`，则您复制的客户名称将是`demoCo`。

1. 根据您使用的视频交付协议，复制相应的协议选择器。 在稍后这些步骤中，您需要复制的协议选择器。

   <table>
    <tbody>
      <tr>
      <td><strong>您正在使用的视频投放协议</strong></td>
      <td><strong>要使用的协议选择器</strong></td>
      </tr>
      <tr>
      <td><p>HTTP</p> <p>如果您使用的是HTTP（非安全视频交付），请确保在之前复制的视频服务URL值中将<code>https</code>更改为<code>http</code>。</p> </td>
      <td><code>public/</code></td>
      </tr>
      <tr>
      <td>HTTPS</td>
      <td><code>public-ssl/</code></td>
      </tr>
    </tbody>
   </table>

1. 在Experience Manager中复制由Dynamic Media处理的完整视频资源路径。 在稍后这些步骤中，您需要此复制的视频资产路径。

   例如：

   `/content/dam/marketing/MyVideo.mp4`

1. 合并先前复制的所有片段，按以下顺序创建字符串：

   &lt; `video service URL`>&lt; `protocol selector`>&lt; `customer name`>&lt; `video asset path`>

   例如，使用这些步骤中示例复制的信息，字符串将如下所示：

   `https://gateway-na.assetsadobe.com/DMGateway/public-ssl/demoCo/content/dam/marketing/MyVideo.mp4`

1. 通过将`.m3u8`附加到字符串的末尾来完成URL。 例如，将`.m3u8`附加到上一步中的字符串后，完整的URL路径将显示如下：

   `https://gateway-na.assetsadobe.com/DMGateway/public-ssl/demoCo/content/dam/marketing/MyVideo.mp4.m3u8`

## 使用HTTP/2交付Dynamic Media资产 {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2是新的、更新的Web协议，它改进了浏览器和服务器的通信方式。 它提供了更快的信息传输速度并减少所需的处理能力。 Dynamic Media资产的投放现在可以通过HTTP/2进行，从而提供更好的响应和加载时间。

有关将HTTP/2与Dynamic Media帐户一起使用的完整详细信息，请参阅[HTTP2内容交付](http2faq.md)。
