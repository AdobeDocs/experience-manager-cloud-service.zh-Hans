---
title: 为响应式站点传送优化的图像
description: 了解如何使用响应式代码功能从Dynamic Media交付优化的图像。
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 62af6f3f-9c86-44ad-870d-140f572f99c5
source-git-commit: b37ff72dbcf85e5558eb3421b5168dc48e063b47
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 14%

---

# 为响应式站点传送优化的图像 {#delivering-optimized-images-for-a-responsive-site}

当您想要与Web开发人员共享用于响应式服务的代码时，请使用响应式代码功能。 将响应式(**[!UICONTROL RESS]**)代码复制到剪贴板，以便与Web开发人员共享。

如果您的网站位于第三方WCM上，则此功能很有用。 但是，如果您的网站位于Adobe Experience Manager上，则异地图像服务器会渲染图像并将其提供给网页。

另请参阅[在网页上嵌入视频查看器](embed-code.md)。

另请参阅[将URL链接到您的Web应用程序](linking-urls-to-yourwebapplication.md)。

**要为响应式网站传送优化的图像：**

1. 导航到要为其提供响应式代码的图像，然后在下拉菜单中选择&#x200B;**[!UICONTROL 呈现版本]**。

   ![chlimage_1-408](assets/chlimage_1-408.png)

1. 选择响应式图像预设。 将显 **[!UICONTROL 示]** URL **[!UICONTROL 和]** RESS按钮。

   ![chlimage_1-409](assets/chlimage_1-409.png)

   >[!NOTE]
   >
   >必须发布选定的资产&#x200B;*和*&#x200B;选定的图像预设或查看器预设，才能使 **[!UICONTROL URL]** 或 **[!UICONTROL RESS]** 按钮可用。
   >
   >图像预设会自动发布。

1. 选择&#x200B;**[!UICONTROL RESS]**。

   ![chlimage_1-410](assets/chlimage_1-410.png)

1. 在&#x200B;**[!UICONTROL 嵌入响应图像]**&#x200B;对话框中，选择并复制响应代码文本，然后将其粘贴到您的网站中以访问响应资产。
1. 编辑嵌入代码中的默认断点，以直接在代码中匹配在响应式网站中找到的断点。 此外，还测试在不同页面断点提供的不同图像分辨率。

## 使用HTTP/2交付Dynamic Media资源 {#using-http-to-delivery-your-dynamic-media-assets}

HTTP/2是新的、更新的Web协议，它改进了浏览器和服务器的通信方式。 它提供了更快的信息传输速度并减少所需的处理能力。 HTTP/2支持交付Dynamic Media资源，可提供更好的响应和加载时间。

有关将HTTP/2与Dynamic Media帐户结合使用的完整详细信息，请参阅[HTTP2内容交付](http2faq.md)。
