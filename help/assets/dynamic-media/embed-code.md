---
title: 在网页上嵌入Dynamic Media视频或图像查看器
description: 了解如何在网页上嵌入Dynamic Media视频或图像资源。
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 76335781-e39f-4aae-967f-5af8634d8f61
source-git-commit: b37ff72dbcf85e5558eb3421b5168dc48e063b47
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 21%

---

# 在网页上嵌入Dynamic Media视频、图像查看器或维度查看器 {#embedding-the-video-or-image-viewer-on-a-web-page}

当您想 **[!UICONTROL 要播放视频或查看嵌入到网页中的资产时]** ，请使用嵌入代码功能。 将嵌入代码复制到剪贴板，以便将其粘贴到网页中。 不允许在“嵌入代码”对 **[!UICONTROL 话框中编辑代码]** 。

仅当您使用Adobe Experience Manager作为WCM _而非_&#x200B;时，才嵌入URL。 如果您将Experience Manager用作WCM，请[直接在页面上添加资源](adding-dynamic-media-assets-to-pages.md)。

查看[将URL链接到您的Web应用程序](linking-urls-to-yourwebapplication.md)。

查看[为响应式网站传送优化的图像](responsive-site.md)。

>[!NOTE]
>
>在发布选定资产之前，无法复制嵌入代码。 此外，还必须发布查看器预设或图像预设。
>
>请参阅[Publish Assets](publishing-dynamicmedia-assets.md)。
>
>请参阅[Publish查看器预设](managing-viewer-presets.md#publishing-viewer-presets)。
>
>请参阅[Publish图像预设](managing-image-presets.md#publishing-image-presets)。

**要在网页上嵌入Dynamic Media视频或图像查看器，请执行以下操作：**

1. 导航到&#x200B;*已发布*&#x200B;要复制其嵌入代码的视频或图像资产。

   请注意，只有在首次&#x200B;*发布*&#x200B;资产&#x200B;*后*，才可复制嵌入代码。此外，还必须发布查看器预设或图像预设。

   请参阅[Publish Assets](publishing-dynamicmedia-assets.md)。

   请参阅[Publish查看器预设](managing-viewer-presets.md#publishing-viewer-presets)。

   请参阅[Publish图像预设](managing-image-presets.md#publishing-image-presets)。

1. 在左边栏中，选择下拉列表并选择&#x200B;**[!UICONTROL 查看器]**。
1. 在左边栏中，选择一个查看器预设名称。 查看器预设将应用于资产。
1. 选择&#x200B;**[!UICONTROL 嵌入]**。
1. 在&#x200B;**[!UICONTROL 嵌入代码]**&#x200B;对话框中，将整个代码复制到剪贴板，然后选择&#x200B;**[!UICONTROL 关闭]**。
1. 将嵌入代码粘贴到网页中。

## 使用HTTP/2交付您的Dynamic Media资源 {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2是新的、更新的Web协议，它改进了浏览器和服务器的通信方式。 它提供了更快的信息传输速度并减少所需的处理能力。 Dynamic Media资源的交付现在可以通过HTTP/2进行，从而缩短响应时间和加载时间。

有关将HTTP/2与Dynamic Media帐户结合使用的完整详细信息，请参阅[HTTP2内容交付](http2faq.md)。
