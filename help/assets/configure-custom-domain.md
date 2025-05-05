---
title: 为发布层配置自定义域
description: 了解如何在Adobe Cloud Manager中为发布层配置自定义域。
exl-id: cc71c8c5-cf42-4092-b0e0-646a2ed0ee54
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 20%

---

# 为发布层配置自定义域{#configure-custom-domain}

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

在Adobe Cloud Manager中，您可以通过添加自定义域让您的网站脱颖而出。 虽然AEM as a Cloud Service附带默认域，但您可以根据需要对其进行自定义。

## 开始之前

* 您必须具有多SAN（使用者替代名称）TLS或SSL证书。
* 对于为同一域中的发布层映射的证书，SSL证书应具有不同的SAN。
* 证书策略必须遵循扩展验证(EV)或组织验证(OV)，而不是域验证(DV)策略。


## 为发布层配置自定义域

1. 转到&#x200B;**[!UICONTROL Adobe Cloud Manager]** > **[!UICONTROL 计划概述]** > **[!UICONTROL SSL证书]**，然后添加您的SSL证书。
   ![图像](/help/assets/assets/ssl-certificate.png)
了解如何在Adobe Cloud Manager中添加[SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)。

1. 添加SSL证书后，添加自定义域。 单击&#x200B;**[!UICONTROL 域设置]**&#x200B;并针对&#x200B;**[!UICONTROL 发布服务]**&#x200B;选项指定自定义域。
了解有关[自定义域](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)的更多信息。

1. 在对应于发布域的DNS记录中添加两个[CNAME记录](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)。
由于 DNS 传播延迟，DNS 验证可能需要几个小时才能处理。

1. 记录支持案例以促进自定义域的配置，确保它定向到交付层。

>[!NOTE]
>
>将自定义域添加到允许的重定向URL列表。 该列表位于资产选择器的IMS客户端中。<br>通过提供自定义域字符串与相应的Adobe团队协调以执行此任务。
