---
title: 发布 Dynamic Media 资产
description: 了解如何发布Dynamic Media资产。
contentOwner: Rick Brough
feature: 资产管理
role: Business Practitioner
exl-id: 8ee759dc-cb8f-4e80-8175-2c3ba06da862
translation-type: tm+mt
source-git-commit: e94289bccc09ceed89a2f8b926817507eaa19968
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 10%

---

# 发布 Dynamic Media 资产 {#publishing-dynamic-media-assets}

您可以通过选择已上传的资产并点按&#x200B;**[!UICONTROL 发布]**&#x200B;或&#x200B;**[!UICONTROL 快速发布]**&#x200B;来发布Dynamic Media资产。 在发布Dynamic Media资产后，您便可以通过URL或在页面上嵌入代码的方式，将资产包含在网页中。

您还可以立即发布上传的资产，而无需任何用户干预。 或者，您也可以选择性发布这些资产。 请参阅[配置Dynamic Media](config-dm.md)。 或者，您也可以使用文件夹级别的&#x200B;**[!UICONTROL 选择性发布]**，选择性地将资产发布到Dynamic Media或Adobe Experience Manager，它们相互排斥。 请参阅[在Dynamic Media中使用选择性发布](/help/assets/dynamic-media/selective-publishing.md)。

在&#x200B;**[!UICONTROL 卡片视图]**&#x200B;中，资产名称正下方以及日期和时间左侧会显示一个小地球图标，指示资产已发布。 在&#x200B;**[!UICONTROL 列表视图]**&#x200B;中，**[!UICONTROL 已发布]**&#x200B;列显示已发布的资产和未发布的资产。

>[!NOTE]
>
>如果资产已经发布，则您会将资产移动到其他文件夹，并从新位置重新发布，此时原始发布的资产位置以及新重新发布的资产仍可用。 但是，原始已发布的资产会“丢失”到Experience Manager，无法取消发布。 因此，作为最佳实践，在将资产移到其他文件夹之前，请先取消发布资产。

如果您打算在对视频资产进行编码后立即发布这些资产，请确保编码已完成。 当对视频进行编码时，系统会通知您视频处理工作流正在进行中。 完成视频编码后，您可以预览视频演绎版。 此时，您便可以安全地发布视频，而不会出现任何发布错误。

另请参阅[将 URL 关联到您的 Web 应用程序](linking-urls-to-yourwebapplication.md)。

另请参阅[在网页上嵌入Dynamic Media Video查看器或图像查看器](embed-code.md)。

>[!NOTE]
>
>* 要使用URL，必须发布资产。 如果资产未发布，则复制URL并将其粘贴到Web浏览器将不起作用。
>* 必须为实时投放激活和发布图像预设和查看器预设。

>



有关发布集或资产的详细信息，请参阅[发布资产](/help/assets/manage-digital-assets.md)。

## HTTP/2投放Dynamic Media资源{#http-delivery-of-dynamic-media-assets}

Experience Manager现在支持通过HTTP/2投放所有Dynamic Media内容（图像和视频）。 即，图像或视频的已发布URL或嵌入代码可与接受托管资产的任何应用程序集成。 然后，通过HTTP/2协议传送已发布的资产。 此投放方法改进了浏览器和服务器通信的方式，使您的所有Dynamic Media资源都能得到更好的响应和加载时间。

请参阅[HTTP/2投放内容常见问题](/help/assets/dynamic-media/http2faq.md)。

<!--this md file used to reside under sites-administering-->
