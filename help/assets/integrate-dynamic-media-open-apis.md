---
title: 将 AEM Assets 与下游应用程序集成
description: 将 AEM Assets 与下游应用程序集成
role: User
exl-id: abd48b5d-2b43-453c-8eb6-31ff509245ca
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 33%

---

# 将 AEM Assets 与下游应用程序集成 {#integrate-dynamic-media-open-apis}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime和Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup><a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets与Edge Delivery Services的集成</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI可扩展性</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新建</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>启用Dynamic Media Prime和Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>搜索最佳实践</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>元数据最佳实践</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>具有 OpenAPI 功能的 Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 开发人员文档</b></a>
        </td>
    </tr>
</table>

>[!AVAILABILITY]
>
>具有 OpenAPI 功能的 Dynamic Media 指南现以 PDF 格式提供。下载完整指南并使用 Adobe Acrobat AI 助手来回答您的疑问。
>
>[!BADGE 具有 OpenAPI 功能的 Dynamic Media 指南 PDF]{type=Informative url="https://helpx.adobe.com/cn/content/dam/help/en/experience-manager/aem-assets/dynamic-media-with-openapi-capabilities.pdf"}

Experience Manager资源存储库中可用的所有[批准的资源](/help/assets/approve-assets.md)都可以交付给下游应用程序。

您可以使用搜索和交付API将您自己的自定义用户界面与Experience Manager Assets存储库集成，也可以使用Adobe的微前端资产选择器。

![与AEM Assets存储库集成](assets/asset-selector-integration.png)

这些API允许您从AEM Assets存储库中搜索批准的资源，然后使用投放URL将资源交付给下游应用程序。 有关详细信息，请参阅[搜索](/help/assets/search-assets-api.md)和[交付](/help/assets/deliver-assets-apis.md) API。

Adobe的微前端资产选择器提供了一个用户界面，可轻松与[!DNL Experience Manager Assets as a Cloud Service]存储库集成，以便您能够浏览或搜索存储库中可用的已批准数字资产，并在应用程序创作体验中使用这些资产。 有关详细信息，请参阅[微型前端资产选择器](/help/assets/overview-asset-selector.md)。

>[!MORELIKETHIS]
>
>* [将资产选择器与各种应用程序集成](/help/assets/integrate-asset-selector.md)
>* [资产选择器属性](/help/assets/asset-selector-properties.md)
>* [资产选择器自定义](/help/assets/asset-selector-customization.md)
