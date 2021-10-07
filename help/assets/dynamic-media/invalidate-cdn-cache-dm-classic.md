---
title: 通过Dynamic Media Classic使CDN（内容交付网络）缓存失效
description: 了解如何使CDN（内容分发网络）缓存内容失效，以便快速更新由Dynamic Media交付的资产，而无需等待缓存过期。
feature: Asset Management,Dynamic Media Classic
role: Admin,User
exl-id: 7e488699-5633-437f-9e2e-58c98aa13145
source-git-commit: 87306ae90f6411d2d4e48f3afdb66e5e848073fe
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 13%

---

# 通过Dynamic Media Classic使CDN缓存失效 {#invalidating-your-cdn-cached-content}

Dynamic Media资产由CDN（内容交付网络）缓存，以便快速交付。 但是，当您对资产进行更新时，您希望这些更改立即生效。 通过使CDN缓存内容失效，您可以快速更新由Dynamic Media交付的资产，而无需等待缓存过期。

>[!NOTE]
>
>此功能要求您使用与Adobe Experience Manager Dynamic Media捆绑在一起的现成CDN。 此功能不支持任何其他自定义CDN。

>[!IMPORTANT]
>
>这些步骤仅适用于Adobe Experience Manager 6.5 Service Pack 5或更早版本中的Dynamic Media。<!-- If you are using Dynamic Media in AEM as a Cloud Service, [use the new steps found here](/help/assets/invalidate-cdn-cache-dynamic-media.md). -->

另请参阅[Dynamic Media Classic](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html)中的缓存概述。

**要通过Dynamic Media Classic使CDN缓存失效，请执行以下操作：**

1. 打开[Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后登录到您的帐户。

   您的凭据和登录详细信息由Adobe在配置时提供。 如果您没有此信息，请联系客户支持。

1. 转到&#x200B;**[!UICONTROL 设置]** > **[!UICONTROL 应用程序设置]** > **[!UICONTROL 常规设置]**。
1. 在“应用程序常规设置”页面的“服务器”组标题下，找到&#x200B;**[!UICONTROL CDN失效模板]**&#x200B;文本框。

1. 指定用于使CDN（内容交付网络）缓存失效的模板。

   例如，假定您输入了引用`<ID>`的图像URL（包括图像预设或修饰符），而不是像以下示例中那样的特定图像ID:

   `https://server.com/is/image/Company/<ID>?$product$`

   如果模板仅包含`<ID>`，则Dynamic Media将填写`https://<server>/is/image` ，其中`<server>`是在“常规设置”中定义的发布服务器名称，&lt;ID>是选定要失效的资产。

1. 在页面的右下角，选择&#x200B;**[!UICONTROL 关闭]**。
1. 在Dynamic Media Classic(Scene7)UI中，选择一个或多个资产，然后转到&#x200B;**[!UICONTROL 文件]** > **[!UICONTROL 无效CDN]**。 您会看到从您创建的模板和您选择的资产生成的一个或多个URL的列表。 它使用“应用程序常规设置”下“已发布的服务器名称”下列出的服务器URL。

   例如，在上一步中设置CDN失效模板后，假设您选择了一个名为`Backpack_B`的图像资产图像。 当您转到&#x200B;**[!UICONTROL 文件]** > **[!UICONTROL 无效CDN]**&#x200B;时，它会在CDN失效用户界面中生成以下URL:

   `https://server.com/is/image/Company/Backpack_B?$product$`

1. 在URL列表框中，选择&#x200B;**[!UICONTROL 继续]**&#x200B;以清除每个特定URL的缓存。 您可以编辑URL，也可以通过键入或粘贴URL列表框来添加URL;您无需预先设置CDN无效模板。

   选择&#x200B;**[!UICONTROL 继续]**&#x200B;后，将显示一个指示器，用于估算清除缓存需要多长时间。

   如果您选择了多个资产，然后转到&#x200B;**[!UICONTROL 文件]** > **[!UICONTROL 无效CDN]**，则每个资产都会在保存的&#x200B;**[!UICONTROL 模板URL]**&#x200B;中引用。 因此，您可以定义&#x200B;**[!UICONTROL CDN无效模板]** ，以引用网站上引用的每个URL图像预设，如产品详细信息和搜索结果。 然后，当您从缓存中选择一个或多个要失效的图像时，URL 会自动填充该界面。

   >[!NOTE]
   >
   >当您选择资产，然后转到&#x200B;**[!UICONTROL 文件]** > **[!UICONTROL 无效CDN]**&#x200B;时，Dynamic Media会使用无效CDN模板从CDN自动创建URL。 如果 **[!UICONTROL CDN 无效模板]**&#x200B;文本框中没有任何内容，则会显示空白 URL 列表。CDN 上的缓存不是基于资产，而是基于 URL。因此，必须了解您网站上的完整 URL。确定这些 URL 后，可以将其添加到步骤前面的&#x200B;**[!UICONTROL 无效 CDN 模板]**。然后，您可以选择这些资产，并在一个步骤中使 URL 失效。
   >
   >另一个选项是向&#x200B;**[!UICONTROL 无效CDN]**&#x200B;列表添加完整的URL。 如果您遵循这种方法，则无需在转到&#x200B;**[!UICONTROL 文件]** > **[!UICONTROL 无效CDN]**&#x200B;选项之前，在Dynamic Media Classic中选择资产。
