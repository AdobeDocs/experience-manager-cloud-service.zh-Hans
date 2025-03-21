---
title: Dynamic Media中的报表
description: 了解如何为Dynamic Media交付失败的URL请求错误报告。
contentOwner: Rick Brough
feature: Asset Management
role: User
hide: true
hidefromtoc: true
exl-id: 2488f813-df15-4dbb-8747-f827ee5925e1
source-git-commit: c82f84fe99d8a196adebe504fef78ed8f0b747a9
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 6%

---

# 为失败的Dynamic Media投放URL请求错误报告

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

您可以请求错误报告，以标识在交付时失败的Dynamic Media URL。 此报表是最多五天的数据汇总，并以CSV格式提供。 错误报告包含以下信息：

* 失败的Dynamic Media交付URL — 失败的URL是Dynamic Media生成的URL，无法在交付时生成任何内容。
* 反向链接URL — 从中调用失败投放URL的反向链接URL。
* 失败计数 — 导致失败的投放URL的加载次数。

当您请求错误报告时，Adobe Dynamic Media团队会以CSV格式向您发送该报告。 申请从提出请求之日起算起，有效期为五天。

您可以每月为给定公司请求一次错误报告。

**为失败的Dynamic Media投放URL请求错误报告：**

1. [向reports-dynamic-media@adobe.com](mailto:reports-dynamic-media@adobe.com)发送一封电子邮件，其中包含与您的Dynamic Media帐户关联的公司名称。

   如果您不知道公司名称，请参阅&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 工具]** > **[!UICONTROL 云服务]** > **[!UICONTROL Dynamic Media配置]**&#x200B;中的[Dynamic Media配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/config-dm.html?lang=zh-Hans#configuring-dynamic-media-cloud-services)页面。 在Dynamic Media配置浏览器页面上，单击&#x200B;**[!UICONTROL 全局]**，选中&#x200B;*[Dynamic_Media_folder_icon]*&#x200B;复选框，然后选择&#x200B;**[!UICONTROL 编辑]**。 您必须在AEM中拥有管理员权限才能访问“Dynamic Media配置”页面。

   ![正在访问Dynamic Media配置页。](/help/assets/dynamic-media/assets/reporting-accessdmconfig.png)
