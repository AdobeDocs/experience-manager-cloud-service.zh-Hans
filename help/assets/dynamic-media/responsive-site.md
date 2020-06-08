---
title: 为响应式网站传送优化的图像
description: 如何使用响应式代码功能传送优化的图像
translation-type: tm+mt
source-git-commit: d6e92a433e61c2a959c62080fcd52fe0ebe67c4f
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 27%

---


# 为响应式网站传送优化的图像 {#delivering-optimized-images-for-a-responsive-site}

如果您希望与 Web 开发人员共享代码以实现响应式服务，可使用响应式代码功能。You copy the responsive (**[!UICONTROL RESS]**) code to the clipboard so you can share it with the web developer.

如果您的网站位于第三方WCM上，则使用此功能很合理。 但是，如果您的网站在AEM上，则非现场图像服务器会渲染该图像并将其提供到网页。

另请参阅[在网页上嵌入视频查看器。](embed-code.md)

另请参阅[将 URL 关联到您的 Web 应用程序。](linking-urls-to-yourwebapplication.md)

**为响应式网站提供优化的图像**:

1. 导航到您要为其提供响应式代码的图像，然后在下拉菜单中，点按演 **[!UICONTROL 绎版]**。

   ![chlimage_1-408](assets/chlimage_1-408.png)

1. 选择响应式图像预设。 将显 **[!UICONTROL 示]** URL **[!UICONTROL 和]** RESS按钮。

   ![chlimage_1-409](assets/chlimage_1-409.png)

   >[!NOTE]
   >
   >必须发布选定的资产&#x200B;*和*&#x200B;选定的图像预设或查看器预设，才能使 **[!UICONTROL URL]** 或 **[!UICONTROL RESS]** 按钮可用。
   >
   >图像预设会自动发布。

1. 点 **[!UICONTROL 击RESS]**。

   ![chlimage_1-410](assets/chlimage_1-410.png)

1. 在“嵌 **[!UICONTROL 入响应式图像]** ”对话框中，选择并复制响应式代码文本，然后将其粘贴到您的网站中以访问响应式资产。
1. 编辑嵌入代码中的默认断点，使其直接与响应式网站的代码断点相匹配。 此外，测试不同页面断点处使用的不同图像分辨率。

## 使用HTTP/2投放Dynamic Media资产 {#using-http-to-delivery-your-dynamic-media-assets}

HTTP/2是新的、经过更新的Web协议，它改进了浏览器和服务器的通信方式。 它提供更快的信息传输，并减少所需的处理能力。 HTTP/2支持Dynamic Media资产的投放，可提供更好的响应和加载时间。

有 [关使用Dynamic Media帐户](http2faq.md) HTTP/2入门的完整详细信息，请参阅内容的HTTP2投放。
