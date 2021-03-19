---
title: 在网页上嵌入Dynamic Media视频或图像查看器
description: 了解如何将Dynamic Media视频或图像资源嵌入网页。
feature: 资产管理
topic: 业务从业者
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 30%

---


# 在网页{#embedding-the-video-or-image-viewer-on-a-web-page}上嵌入Dynamic Media Video、Image Viewer或Dimensional查看器

当您想 **[!UICONTROL 要播放视频或查看嵌入到网页中的资产时]** ，请使用嵌入代码功能。 将嵌入代码复制到剪贴板，以便将其粘贴到网页中。 不允许在“嵌入代码”对 **[!UICONTROL 话框中编辑代码]** 。

仅当&#x200B;_不_&#x200B;使用AEM作为WCM时，才嵌入URL。 如果您使用AEM作为WCM，[将资产直接添加到页面。](adding-dynamic-media-assets-to-pages.md)

请参阅[将URL关联到您的Web 应用程序。](linking-urls-to-yourwebapplication.md)

请参阅[为响应式网站传送优化的图像。](responsive-site.md)

>[!NOTE]
>
>只有在发布选定的资产后，才可复制其嵌入代码。此外，您还必须发布查看器预设或图像预设。
>
>请参阅[发布资产](publishing-dynamicmedia-assets.md)。
>
>请参阅[发布查看器预设](managing-viewer-presets.md#publishing-viewer-presets)。
>
>请参阅[发布图像预设](managing-image-presets.md#publishing-image-presets)。

**将Dynamic Media视频查看器或图像查看器嵌入网页**

1. 导航到要复制其嵌入代码的&#x200B;*已发布的*&#x200B;视频或图像资产。

   请注意，只有在首次&#x200B;*发布*&#x200B;资产&#x200B;*后*，才可复制嵌入代码。此外，还必须发布查看器预设或图像预设。

   请参阅[发布资产](publishing-dynamicmedia-assets.md)。

   请参阅[发布查看器预设](managing-viewer-presets.md#publishing-viewer-presets)。

   请参阅[发布图像预设](managing-image-presets.md#publishing-image-presets)。

1. 在左边栏中，选择下拉列表，然后点按&#x200B;**[!UICONTROL 查看器]**。
1. 在左边栏中，点按查看器预设名称。查看器预设会应用于资产。
1. 点按&#x200B;**[!UICONTROL 嵌入]**。
1. 在&#x200B;**[!UICONTROL 嵌入代码]**&#x200B;对话框中，将整个代码复制到剪贴板，然后点按&#x200B;**[!UICONTROL 关闭]**。
1. 将嵌入代码粘贴到网页中。

## 使用HTTP/2传送Dynamic Media资源{#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2是新的、经过更新的Web协议，它改进了浏览器和服务器通信的方式。 它提供了更快的信息传输，并减少了所需的处理能力。 Dynamic Media资源的投放现在可以通过HTTP/2实现，从而提供更好的响应和加载时间。

有关使用Dynamic Media帐户HTTP/2快速入门的完整详细信息，请参阅[Content](http2faq.md)的HTTP2投放。
