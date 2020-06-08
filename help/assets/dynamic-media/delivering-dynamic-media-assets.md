---
title: 传送 Dynamic Media 资产
description: 了解如何交付动态媒体资产
translation-type: tm+mt
source-git-commit: 218afb360ec3a13f2f4562a703ca3184083fa7f6
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 25%

---


# 传送 Dynamic Media 资产{#delivering-dynamic-media-assets}

您如何投放动态媒体资产（视频和图像）取决于网站的实施方式。

通过 Dynamic Media，您可以选择以下方式：

* 如果您的网站托管在 AEM 上，您会希望将 Dynamic Media 资产直接添加到您的页面。
* 如果您的网站不在AEM上，您可以选择：

   * 将视频或图像嵌入您的网站。
   * 将URL关联到您的Web应用程序。 当您希望以弹出窗口或模态窗口的形式传送视频播放器时，可使用链接。
   * 如果您的网站是响应式的，您可以投 [递优化的图像。](/help/assets/dynamic-media/responsive-site.md)

>[!NOTE]
>
>智能成像可以与现有图像预设配合使用，并在投放的最后一毫秒使用智能功能根据浏览器或网络连接速度进一步减小图像文件大小。 有关更 [多信息](/help/assets/dynamic-media/imaging-faq.md) ，请参阅智能成像。

有关更多信息，请参阅下列主题：

* [将Dynamic Media资产添加到网页](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)
* [在网页上嵌入视频查看器或图像查看器](/help/assets/dynamic-media/embed-code.md)
* [在 Dynamic Media 中激活热链接保护](/help/assets/dynamic-media/hotlink-protection.md)
* [将 URL 关联到您的 Web 应用程序](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)
* [为响应式网站传送优化的图像](/help/assets/dynamic-media/responsive-site.md)
* [内容的HTTP2投放](/help/assets/dynamic-media/http2faq.md)
* [使 CDN 缓存内容无效](/help/assets/dynamic-media/invalidate-cdn-cached-content.md)
* [使用规则集转换URL](/help/assets/dynamic-media/using-rulesets-to-transform-urls.md)

## HTTP/2投放Dynamic Media资产 {#http-delivery-of-dynamic-media-assets}

AEM现在支持通过HTTP/2投放所有Dynamic Media内容（图像和视频）。 即，图像或视频的已发布URL或嵌入代码可与接受托管资产的任何应用程序集成。 随后，将通过HTTP/2协议传送已发布的资产。 此投放方法改进了浏览器和服务器通信的方式，使所有Dynamic Media资源的响应和加载时间都更好。

请参 [阅HTTP/2投放内容常见问题](/help/assets/dynamic-media/http2faq.md) ，了解更多信息。
