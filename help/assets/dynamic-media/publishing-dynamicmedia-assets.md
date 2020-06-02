---
title: 发布 Dynamic Media 资产
description: 如何发布Dynamic Media资产
contentOwner: Rick Brough
translation-type: tm+mt
source-git-commit: d84a6692f2d0aae496bd2bd98ac99c2663f3fe52
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 13%

---


# 发布 Dynamic Media 资产 {#publishing-dynamic-media-assets}

通过选择已上传的资产并点按发布或快速发布，可 **[!UICONTROL 以发]** 布 **[!UICONTROL Dynamic Media资产]**。 在发布Dynamic Media资产后，您可以通过URL或通过在页面上嵌入代码的方式将资产包含在网页中。

您还可以立即发布上传的资产，无需任何用户干预。 或者，您也可以选择性发布这些资产。 See [Configuring Dynamic Media](config-dm.md).

在卡 **[!UICONTROL 片视图]**&#x200B;中，资产名称的正下方以及日期和时间的左侧会显示一个小地球图标，以指示资产已发布。 在&#x200B;**[!UICONTROL 列表视图]**&#x200B;中，**[!UICONTROL 已发布]**&#x200B;列显示已发布的资产和未发布的资产。

>[!NOTE]
>
>如果资产已发布，则您可以使用AEM将资产移动到其他文件夹，并从新位置重新发布，则原始发布的资产位置以及新重新发布的资产仍然可用。 但是，原始已发布的资产会“丢失”到AEM，无法取消发布。 因此，作为最佳实践，在将资产移至其他文件夹之前，请先取消发布资产。

如果您打算在对视频资产进行编码后立即发布这些资产，请确保编码已完成。 当视频仍在编码时，系统会告知您视频处理工作流正在进行中。 完成视频编码后，您应该能够预览视频演绎版。 此时，您可以安全地发布视频，而不会出现任何发布错误。

另请参阅[将 URL 关联到您的 Web 应用程序](linking-urls-to-yourwebapplication.md)。

另请参 [阅在网页上嵌入Dynamic Media视频查看器或图像查看器。](embed-code.md)

>[!NOTE]
>
>* 要使用 URL，必须先发布资产。如果资产未发布，您便无法将 URL 复制并粘贴到 Web 浏览器。
>* 必须为实时投放激活和发布图像预设和查看器预设。
>



有关发布集或资产的详细信息，请参阅发 [布资产。](/help/assets/manage-digital-assets.md)

## HTTP/2投放Dynamic Media资产 {#http-delivery-of-dynamic-media-assets}

AEM现在支持通过HTTP/2投放所有Dynamic Media内容（图像和视频）。 即，图像或视频的已发布URL或嵌入代码可与接受托管资产的任何应用程序集成。 随后，将通过HTTP/2协议传送已发布的资产。 此投放方法改进了浏览器和服务器通信的方式，使所有Dynamic Media资源的响应和加载时间都更好。

请参 [阅HTTP/2投放内容常见问题](/help/assets/dynamic-media/http2faq.md) ，了解更多信息。
<!--this md file used to reside under sites-administering-->
