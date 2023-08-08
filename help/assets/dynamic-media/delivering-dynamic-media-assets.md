---
title: 交付Dynamic Media资源
description: 了解如何通过嵌入的视频和图像或者将URL关联到Web应用程序，将Dynamic Media资源交付到您的网页。
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 4557b561-b3c4-4d6f-8044-2069bda41613
source-git-commit: 0e452bd94d75609ecc3c20ab6b56ded968ed0a70
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 9%

---

# 交付Dynamic Media资源{#delivering-dynamic-media-assets}

如何投放Dynamic Media资源（视频和图像）取决于网站的实施方式。

使用Dynamic Media，您有多个选项：

* 如果您的网站托管在Adobe Experience Manager上，那么您希望直接将Dynamic Media资源添加到您的页面。
* 如果您的网站不在Experience Manager中，您可以选择以下任一选项：

   * 将视频或图像嵌入到网站中。
   * 将 URL 关联到您的 Web 应用程序. 当您希望将视频播放器作为弹出窗口或模式窗口交付时，请使用链接。
   * 如果您的网站是响应式的，您可以 [传送优化的图像](/help/assets/dynamic-media/responsive-site.md).

>[!NOTE]
>
>智能成像可与您现有的图像预设配合使用。 它利用在交付的最后毫秒的智能功能，根据浏览器或网络连接速度进一步减小图像文件大小。 请参阅 [智能成像](/help/assets/dynamic-media/imaging-faq.md) 以了解更多信息。

有关更多信息，请参阅以下主题：

* [将Dynamic Media资产添加到网页](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)
* [在网页上嵌入视频查看器或图像查看器](/help/assets/dynamic-media/embed-code.md)
* [在 Dynamic Media 中激活热链接保护](/help/assets/dynamic-media/hotlink-protection.md)
* [将URL链接到您的Web应用程序](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)
* [为响应式网站传送优化的图像](/help/assets/dynamic-media/responsive-site.md)
* [HTTP2内容交付](/help/assets/dynamic-media/http2faq.md)
* [通过 Dynamic Media 使 CDN 缓存失效](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)
* [通过 Dynamic Media Classic 使 CDN 缓存失效](/help/assets/dynamic-media/invalidate-cdn-cache-dm-classic.md)
* [使用规则集转换URL](/help/assets/dynamic-media/using-rulesets-to-transform-urls.md)

## Dynamic Media资源的HTTP/2交付 {#http-delivery-of-dynamic-media-assets}

Experience Manager现在支持通过HTTP/2交付所有Dynamic Media内容（图像和视频）。 即，图像或视频的已发布URL或嵌入代码可用于与接受托管资产的任何应用程序集成。 随后，该已发布的资产将通过HTTP/2协议进行交付。 这种交付方法改进了浏览器和服务器的通信方式，使得所有Dynamic Media资源都有更好的响应和加载时间。

要了解更多信息，请参阅 [HTTP/2内容交付常见问题解答](/help/assets/dynamic-media/http2faq.md).
