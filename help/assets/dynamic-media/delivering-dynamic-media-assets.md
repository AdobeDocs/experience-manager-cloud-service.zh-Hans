---
title: 交付Dynamic Media资产
description: 了解如何交付Dynamic Media资产。
feature: Asset Management
role: User
exl-id: 4557b561-b3c4-4d6f-8044-2069bda41613
source-git-commit: 6933f053e11320d8201922723879983084c52209
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 10%

---

# 交付Dynamic Media资产{#delivering-dynamic-media-assets}

如何交付Dynamic Media资产（包括视频和图像）取决于网站的实施方式。

使用Dynamic Media，您有以下几个选项：

* 如果您的网站托管在Adobe Experience Manager上，则您希望将Dynamic Media资产直接添加到您的页面。
* 如果您的网站未Experience Manager，则可以选择以下任一选项：

   * 在您的网站上嵌入视频或图像。
   * 将URL关联到您的Web应用程序。当您希望将视频播放器作为弹出窗口或模式窗口进行传送时，请使用链接。
   * 如果您的网站是响应式的，您可以 [提供优化的图像](/help/assets/dynamic-media/responsive-site.md).

>[!NOTE]
>
>智能成像可与您现有的图像预设配合使用。 它在交付的最后一毫秒内使用智能功能，根据浏览器或网络连接速度进一步减小图像文件大小。 请参阅 [智能成像](/help/assets/dynamic-media/imaging-faq.md) 以了解更多信息。

有关更多信息，请参阅下列主题：

* [将Dynamic Media Assets添加到网页](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)
* [在网页上嵌入视频查看器或图像查看器](/help/assets/dynamic-media/embed-code.md)
* [在 Dynamic Media 中激活热链接保护](/help/assets/dynamic-media/hotlink-protection.md)
* [将URL关联到您的Web应用程序](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)
* [为响应式网站提供优化的图像](/help/assets/dynamic-media/responsive-site.md)
* [HTTP2内容交付](/help/assets/dynamic-media/http2faq.md)
* [通过 Dynamic Media 使 CDN 缓存失效](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)
* [通过 Dynamic Media Classic 使 CDN 缓存失效](/help/assets/dynamic-media/invalidate-cdn-cache-dm-classic.md)
* [使用规则集转换URL](/help/assets/dynamic-media/using-rulesets-to-transform-urls.md)

## HTTP/2交付Dynamic Media资产 {#http-delivery-of-dynamic-media-assets}

Experience Manager现在支持通过HTTP/2交付所有Dynamic Media内容（图像和视频）。 即，图像或视频的已发布URL或嵌入代码可与接受托管资产的任何应用程序集成。 然后，将通过HTTP/2协议来交付已发布的资产。 这种交付方法改进了浏览器和服务器通信的方式，从而可以缩短所有Dynamic Media资产的响应和加载时间。

要了解更多信息，请参阅 [HTTP/2内容交付常见问题解答](/help/assets/dynamic-media/http2faq.md).
