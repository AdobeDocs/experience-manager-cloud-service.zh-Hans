---
title: 发布Dynamic Media资产
description: 了解如何发布Dynamic Media资产。
contentOwner: Rick Brough
feature: 资产管理
role: User
exl-id: 8ee759dc-cb8f-4e80-8175-2c3ba06da862
source-git-commit: a11529886d4b158c19a97ccbcb7d004cf814178d
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 7%

---

# 发布Dynamic Media资产 {#publishing-dynamic-media-assets}

要发布Dynamic Media资产，请选择已上传的资产，然后选择&#x200B;**[!UICONTROL 发布]**&#x200B;或&#x200B;**[!UICONTROL 快速发布]**。 发布Dynamic Media资产后，您便可以通过URL或在页面上嵌入代码的方式，将这些资产包含在网页中。

您还可以立即发布上传的资产，无需任何用户干预。 或者，您也可以选择性地发布这些资产。 请参阅[配置Dynamic Media](config-dm.md)。 或者，您也可以使用文件夹级别的&#x200B;**[!UICONTROL 选择性发布]** ，有选择地将资产发布到相互排斥的Dynamic Media或Adobe Experience Manager。 请参阅[使用Dynamic Media中的“选择性发布”功能](/help/assets/dynamic-media/selective-publishing.md)。

在&#x200B;**[!UICONTROL 卡片视图]**&#x200B;中，资产名称的正下方以及日期和时间的左侧会显示一个小地球图标，指示资产已发布。 在&#x200B;**[!UICONTROL 列表视图]**&#x200B;中，**[!UICONTROL 已发布]**&#x200B;列显示已发布的资产和未发布的资产。

>[!NOTE]
>
>如果资产已发布，则您会将资产移动到其他文件夹，并从新位置重新发布，则原始已发布的资产位置以及新重新发布的资产仍然可用。 但是，原始已发布的资产将“丢失”到Experience Manager，无法取消发布。 因此，作为最佳实践，请先取消发布资产，然后再将资产移动到其他文件夹。

如果您打算在对视频资产进行编码后立即发布这些资产，请确保编码已完成。 对视频进行编码时，系统会告知您正在进行视频处理工作流。 视频编码完成后，您可以预览视频演绎版。 此时，您便可以安全地发布视频，而不会出现任何发布错误。

另请参阅[将URL链接到Web应用程序](linking-urls-to-yourwebapplication.md)。

另请参阅[在网页上嵌入Dynamic Media视频查看器或图像查看器](embed-code.md)。

>[!NOTE]
>
>* 必须发布资产才能使用URL。 如果资产未发布，则复制URL并将其粘贴到Web浏览器中不起作用。
>* 必须激活并发布图像预设和查看器预设才能进行实时交付。

>



有关发布集或资产的详细信息，请参阅[发布资产](/help/assets/manage-digital-assets.md)。

## HTTP/2交付Dynamic Media资产 {#http-delivery-of-dynamic-media-assets}

Experience Manager现在支持通过HTTP/2交付所有Dynamic Media内容（图像和视频）。 即，图像或视频的已发布URL或嵌入代码可与接受托管资产的任何应用程序集成。 然后，将通过HTTP/2协议来交付已发布的资产。 这种交付方法改进了浏览器和服务器通信的方式，从而可以缩短所有Dynamic Media资产的响应和加载时间。

请参阅[HTTP/2内容交付常见问题解答](/help/assets/dynamic-media/http2faq.md)。

<!--this md file used to reside under sites-administering-->
