---
title: 通过Dynamic Media Classic使CDN缓存失效
description: “了解如何使您的CDN(内容投放网络)缓存内容失效，以便您快速更新由Dynamic Media交付的资源，而不是等待缓存过期。”
feature: 资产管理，Dynamic Media Classic
topic: 业务从业者
translation-type: tm+mt
source-git-commit: 80a59a02067d478713aa7dcdb436ad1345d89c1a
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 14%

---


# 通过Dynamic Media Classic {#invalidating-your-cdn-cached-content}使CDN缓存失效

Dynamic Media资源由CDN(内容投放网络)缓存，以便快速投放。 但是，当您对资产进行更新时，您希望这些更改立即生效。 使CDN缓存内容失效后，您可以快速更新由Dynamic Media交付的资源，而无需等待缓存过期。

>[!NOTE]
>
>此功能要求您使用与Adobe Experience Manager Dynamic Media绑定的现成CDN。 此功能不支持任何其他自定义CDN。

>[!IMPORTANT]
>
>这些步骤仅适用于AEM 6.5、Service Pack 5或更早版本中的Dynamic Media。<!-- If you are using Dynamic Media in AEM as a Cloud Service, [use the new steps found here](/help/assets/invalidate-cdn-cache-dynamic-media.md). -->

另请参阅[Dynamic Media Classic](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html)中的缓存概述。

**要通过Dynamic Media Classic使CDN缓存失效，请执行以下操作：**

1. 打开[Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后登录到您的帐户。

   您的凭据和登录详细信息由Adobe在设置时提供。 如果您没有此信息，请与技术支持联系。

1. 单击&#x200B;**[!UICONTROL 设置 > 应用程序设置 > 常规设置]**。
1. 在“应用程序常规设置”页的“服务器”组标题下，找到&#x200B;**[!UICONTROL CDN失效模板]**&#x200B;文本框。

1. 指定用于使CDN(内容投放网络)缓存失效的模板。

   例如，假定您输入引用`<ID>`的图像URL（包括图像预设或修饰符），而不是像以下示例中那样输入特定的图像ID:

   `https://server.com/is/image/Company/<ID>?$product$`

   如果模板仅包含`<ID>`，则Dynamic Media将填入`https://<server>/is/image`，其中`<server>`是“常规设置”中定义的发布服务器名称，而&lt;ID>是选定无效的资产。

1. 在页面的右下角，点按&#x200B;**[!UICONTROL 关闭]**。
1. 在Dynamic Media Classic(Scene7)UI中，选择一个或多个资源，然后点按&#x200B;**[!UICONTROL “文件”>“使CDN失效”]**。 您会看到一个或多个URL的列表，这些URL是从您创建的模板以及您选择的资产中生成的。 它使用“应用程序常规设置”下“已发布服务器名称”下列出的服务器URL。

   例如，在上一步中设置了CDN失效模板后，假定您选择了名为`Backpack_B`的单个图像资源图像。 点按&#x200B;**[!UICONTROL “文件”>“使CDN]**&#x200B;失效”时，将在CDN Invalidation用户界面中生成以下URL:

   `https://server.com/is/image/Company/Backpack_B?$product$`

1. 在URL列表框中，点按&#x200B;**[!UICONTROL 继续]**&#x200B;以清除每个特定URL的缓存。 您可以编辑URL，也可以通过键入或粘贴URL到URL列表框来添加URL;您无需预先设置CDN Invalidate模板。

   点按&#x200B;**[!UICONTROL 继续]**&#x200B;后，将显示一个指示器，用于估计清除缓存所需的时间。

   如果您选择了多个资源，然后点按&#x200B;**[!UICONTROL 文件>使CDN]**&#x200B;失效，则每个资源都会在保存的&#x200B;**[!UICONTROL 模板URL]**&#x200B;中引用。 因此，您可以定义一个&#x200B;**[!UICONTROL CDN失效模板]**，引用网站上引用的每个URL图像预设，如产品详细信息和搜索结果。 然后，当您从缓存中选择一个或多个要失效的图像时，URL 会自动填充该界面。

   >[!NOTE]
   >
   >选择资源，然后点按&#x200B;**[!UICONTROL 文件> Invalidate CDN]**&#x200B;时，Dynamic Media会使用失效的CDN模板自动创建要从CDN失效的URL。 如果 **[!UICONTROL CDN 无效模板]**&#x200B;文本框中没有任何内容，则会显示空白 URL 列表。CDN 上的缓存不是基于资产，而是基于 URL。因此，必须了解您网站上的完整 URL。确定这些 URL 后，可以将其添加到步骤前面的&#x200B;**[!UICONTROL 无效 CDN 模板]**。然后，您可以选择这些资产，并在一个步骤中使 URL 失效。
   >
   >另一种方法是向&#x200B;**[!UICONTROL 使CDN]**&#x200B;列表添加完整的URL。 如果遵循此方法，则不必在Dynamic Media Classic中选择资源，然后再转到&#x200B;**[!UICONTROL “文件”>“使CDN]**&#x200B;失效”选项。

