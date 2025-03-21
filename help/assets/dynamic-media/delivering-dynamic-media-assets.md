---
title: 投放Dynamic Media Assets
description: 了解如何通过嵌入的视频和图像或将URL关联到Web应用程序，将Dynamic Media资产交付到您的网页。
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 4557b561-b3c4-4d6f-8044-2069bda41613
source-git-commit: c82f84fe99d8a196adebe504fef78ed8f0b747a9
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 11%

---

# 投放Dynamic Media Assets{#delivering-dynamic-media-assets}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime和Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup><a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets与Edge Delivery Services的集成</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI可扩展性</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新建</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>启用Dynamic Media Prime和Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>搜索最佳实践</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>元数据最佳实践</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>具有 OpenAPI 功能的 Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 开发人员文档</b></a>
        </td>
    </tr>
</table>

如何投放Dynamic Media资产（视频和图像）取决于网站的实施方式。

使用Dynamic Media，您有多个选项：

* 如果您的网站托管在Adobe Experience Manager上，那么您需要将Dynamic Media资源直接添加到您的页面。
* 如果您的网站不在Experience Manager上，则可以选择以下任一选项：

   * 将视频或图像嵌入到网站中。
   * 将URL链接到您的Web应用程序。 当您希望将视频播放器作为弹出窗口或模式窗口交付时，请使用链接。
   * 如果您的网站是响应式的，您可以[交付优化的图像](/help/assets/dynamic-media/responsive-site.md)。

>[!NOTE]
>
>智能成像可与您现有的图像预设配合使用。 它利用在交付的最后毫秒的智能功能，根据浏览器或网络连接速度进一步减小图像文件大小。 有关详细信息，请参阅[智能成像](/help/assets/dynamic-media/imaging-faq.md)。

有关更多信息，请参阅以下主题：

* [将Dynamic Media Assets添加到网页](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)
* [在网页上嵌入视频查看器或图像查看器](/help/assets/dynamic-media/embed-code.md)
* [在 Dynamic Media 中激活热链接保护](/help/assets/dynamic-media/hotlink-protection.md)
* [将URL链接到您的Web应用程序](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)
* [为响应式网站传送优化的图像](/help/assets/dynamic-media/responsive-site.md)
* [HTTP2内容交付](/help/assets/dynamic-media/http2faq.md)
* [通过 Dynamic Media 使 CDN 缓存失效](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)
* [通过 Dynamic Media Classic 使 CDN 缓存失效](/help/assets/dynamic-media/invalidate-cdn-cache-dm-classic.md)
* [使用规则集转换URL](/help/assets/dynamic-media/using-rulesets-to-transform-urls.md)

## Dynamic Media资产的HTTP/2交付 {#http-delivery-of-dynamic-media-assets}

Experience Manager现在支持通过HTTP/2交付所有Dynamic Media内容（图像和视频）。 即，图像或视频的已发布URL或嵌入代码可用于与接受托管资产的任何应用程序集成。 随后，该已发布的资产将通过HTTP/2协议进行交付。 这种交付方法改进了浏览器和服务器的通信方式，使得所有Dynamic Media资产都有更好的响应和加载时间。

若要了解更多信息，请参阅[HTTP/2内容交付常见问题解答](/help/assets/dynamic-media/http2faq.md)。
