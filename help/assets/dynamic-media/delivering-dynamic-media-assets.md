---
title: 传送 Dynamic Media 资产
description: 了解如何交付Dynamic Media资产。
feature: 资产管理
topic: 商务从业人员
role: Business Practitioner
exl-id: 4557b561-b3c4-4d6f-8044-2069bda41613
translation-type: tm+mt
source-git-commit: 6b232ab512a6faaf075faa55c238dfb10c00b100
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 14%

---

# 传送 Dynamic Media 资产{#delivering-dynamic-media-assets}

您如何提供Dynamic Media资产（视频和图像）取决于网站的实施方式。

有了Dynamic Media，您有以下几种选择：

* 如果您的网站托管在AEM上，则您希望将Dynamic Media资产直接添加到您的页面。
* 如果您的网站不在AEM上，您可以选择：

   * 将视频或图像嵌入您的网站。
   * 将URL关联到您的Web应用程序。当您希望以弹出窗口或模态窗口的形式传送视频播放器时，可使用链接。
   * 如果您的站点是响应式的，则您可以[传送优化的图像](/help/assets/dynamic-media/responsive-site.md)。

>[!NOTE]
>
>智能图像处理功能可与现有图像预设配合使用。 它在投放的最后毫秒使用智能根据浏览器或网络连接速度进一步减小图像文件大小。 有关详细信息，请参阅[智能成像](/help/assets/dynamic-media/imaging-faq.md)。

有关更多信息，请参阅下列主题：

* [将Dynamic Media资产添加到网页](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)
* [在网页上嵌入视频查看器或图像查看器](/help/assets/dynamic-media/embed-code.md)
* [在 Dynamic Media 中激活热链接保护](/help/assets/dynamic-media/hotlink-protection.md)
* [将 URL 关联到您的 Web 应用程序](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)
* [为响应式网站传送优化的图像](/help/assets/dynamic-media/responsive-site.md)
* [内容的HTTP2投放](/help/assets/dynamic-media/http2faq.md)
* [通过Dynamic Media使CDN缓存失效](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)
* [通过Dynamic Media Classic使CDN缓存失效](/help/assets/dynamic-media/invalidate-cdn-cache-dm-classic.md)
* [使用规则集转换URL](/help/assets/dynamic-media/using-rulesets-to-transform-urls.md)

## HTTP/2投放Dynamic Media资源{#http-delivery-of-dynamic-media-assets}

AEM现在支持通过HTTP/2投放所有Dynamic Media内容（图像和视频）。 即，图像或视频的已发布URL或嵌入代码可与接受托管资产的任何应用程序集成。 然后，通过HTTP/2协议传送已发布的资产。 此投放方法改进了浏览器和服务器通信的方式，使您的所有Dynamic Media资源都能得到更好的响应和加载时间。

要了解更多信息，请参阅[HTTP/2投放内容常见问题](/help/assets/dynamic-media/http2faq.md)。
