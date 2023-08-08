---
title: 发布 Dynamic Media 资源
description: 了解如何发布Dynamic Media视频和图像资源，以便可以通过URL或在网页上嵌入代码的方式将其包含在网页中。
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 8ee759dc-cb8f-4e80-8175-2c3ba06da862
source-git-commit: 0e452bd94d75609ecc3c20ab6b56ded968ed0a70
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 4%

---

# 发布 Dynamic Media 资源 {#publishing-dynamic-media-assets}

您可以通过选择已上传的资源并选择，来发布Dynamic Media资源 **[!UICONTROL Publish]** 或 **[!UICONTROL 快速发布]**. 发布Dynamic Media资源后，您便可以通过URL或通过在页面上嵌入代码的方式将其包含在网页中。

您还可以即时发布您上传的资产，无需任何用户干预。 或者，您可以选择发布这些资产。 请参阅 [配置Dynamic Media](config-dm.md). 或者，您可以选择将资源发布到Dynamic Media或Adobe Experience Manager，二者相互排斥，使用 **[!UICONTROL 选择性发布]** 在文件夹级别。 请参阅 [使用Dynamic Media中的“选择性发布”功能](/help/assets/dynamic-media/selective-publishing.md).

在 **[!UICONTROL 卡片视图]**，资产名称的正下方以及日期和时间左侧会显示一个小地球图标，指示资产已发布。 在&#x200B;**[!UICONTROL 列表视图]**&#x200B;中，**[!UICONTROL 已发布]**&#x200B;列显示已发布的资产和未发布的资产。

>[!NOTE]
>
>如果资产已经发布，那么您将资产移动到另一个文件夹，并从其新位置重新发布，则原始发布的资产位置以及新重新发布的资产仍然可用。 但是，原始发布的资产会被Experience Manager“丢失”，无法取消发布。 因此，作为最佳实践，请先取消发布资产，然后再将资产移动到其他文件夹。

如果您打算在编码视频资产后立即发布这些资产，请确保编码已完成。 在对视频进行编码时，系统会告知您视频处理工作流正在进行中。 完成视频编码后，您可以预览视频演绎版。 在这种情况下，您可以安全地发布视频，而不会发生任何发布错误。

另请参阅 [将URL链接到您的Web应用程序](linking-urls-to-yourwebapplication.md).

另请参阅 [将Dynamic Media视频查看器或图像查看器嵌入网页](embed-code.md).

>[!NOTE]
>
>* 必须发布资源才能使用该URL。 如果资产未发布，则无法将URL复制并粘贴到Web浏览器。
>* 必须激活并发布图像预设和查看器预设才能实时交付。
>

有关发布集或资源的详细信息，请参阅 [发布资产](/help/assets/manage-digital-assets.md).

## Dynamic Media资源的HTTP/2交付 {#http-delivery-of-dynamic-media-assets}

Experience Manager现在支持通过HTTP/2交付所有Dynamic Media内容（图像和视频）。 即，图像或视频的已发布URL或嵌入代码可用于与接受托管资产的任何应用程序集成。 随后，该已发布的资产将通过HTTP/2协议进行交付。 这种交付方法改进了浏览器和服务器的通信方式，使得所有Dynamic Media资源都有更好的响应和加载时间。

请参阅 [HTTP/2内容交付常见问题解答](/help/assets/dynamic-media/http2faq.md).

<!--this md file used to reside under sites-administering-->
