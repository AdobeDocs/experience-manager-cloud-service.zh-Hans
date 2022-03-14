---
title: 为响应式站点传送优化的图像
description: 了解如何使用响应式代码功能从Dynamic Media交付优化的图像。
feature: Asset Management
role: User
exl-id: 62af6f3f-9c86-44ad-870d-140f572f99c5
source-git-commit: a11529886d4b158c19a97ccbcb7d004cf814178d
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 27%

---

# 为响应式站点传送优化的图像 {#delivering-optimized-images-for-a-responsive-site}

如果您希望与 Web 开发人员共享代码以实现响应式服务，可使用响应式代码功能。复制响应式(**[!UICONTROL RESS]**)代码，以便您可以将其与web开发人员共享。

如果您的网站位于第三方WCM上，则使用此功能很有意义。 但是，如果您的网站位于Adobe Experience Manager上，则站外图像服务器会呈现该图像并将其提供到网页。

另请参阅 [在网页上嵌入视频查看器](embed-code.md).

另请参阅 [将URL关联到您的Web应用程序](linking-urls-to-yourwebapplication.md).

**要为响应式网站传送优化的图像，请执行以下操作：**

1. 导航到您要为提供响应代码的图像，然后在下拉菜单中，选择 **[!UICONTROL 演绎版]**.

   ![chlimage_1-408](assets/chlimage_1-408.png)

1. 选择响应式图像预设。 将显 **[!UICONTROL 示]** URL **[!UICONTROL 和]** RESS按钮。

   ![chlimage_1-409](assets/chlimage_1-409.png)

   >[!NOTE]
   >
   >必须发布选定的资产&#x200B;*和*&#x200B;选定的图像预设或查看器预设，才能使 **[!UICONTROL URL]** 或 **[!UICONTROL RESS]** 按钮可用。
   >
   >图像预设会自动发布。

1. 选择 **[!UICONTROL RESS]**.

   ![chlimage_1-410](assets/chlimage_1-410.png)

1. 在 **[!UICONTROL 嵌入响应式图像]** 对话框中，选择并复制响应代码文本，然后将其粘贴到您的网站中，以访问响应式资产。
1. 编辑嵌入代码中的默认断点，以便直接在代码中与响应式网站上的内容匹配。 此外，还应测试不同页面断点处使用的不同图像分辨率。

## 使用HTTP/2交付Dynamic Media资产 {#using-http-to-delivery-your-dynamic-media-assets}

HTTP/2是经过更新的新Web协议，可改进浏览器和服务器的通信方式。 它提供了更快的信息传输，并降低了所需的处理能力。 HTTP/2支持交付Dynamic Media资产，从而提供更好的响应和加载时间。

请参阅 [HTTP2内容交付](http2faq.md) 有关开始使用HTTP/2与您的Dynamic Media帐户的完整详细信息。
