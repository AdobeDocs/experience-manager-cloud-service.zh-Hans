---
title: 为Publish层配置自定义域
description: 了解如何在AdobeCloud Manager中为发布层配置自定义域。
exl-id: cc71c8c5-cf42-4092-b0e0-646a2ed0ee54
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 11%

---

# 为发布层配置自定义域{#configure-custom-domain}

| [搜索最佳实践](/help/assets/search-best-practices.md) | [元数据最佳实践](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [具有 OpenAPI 功能的 Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 开发人员文档](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

>[!AVAILABILITY]
>
>Dynamic Media with OpenAPI功能指南现在以PDF格式提供。 下载整个指南，并使用Adobe Acrobat AI Assistant来回答您的疑问。
>
>[!BADGE 具有OpenAPI功能的Dynamic Media指南PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/dynamic-media-with-openapi-capabilities.pdf"}

在AdobeCloud Manager中，您可以通过添加自定义域让您的网站脱颖而出。 虽然AEM as a Cloud Service附带默认域，但您可以根据需要对其进行自定义。

## 开始之前

* 您必须具有多SAN（使用者替代名称）TLS或SSL证书。
* 对于为同一域中的发布层映射的证书，SSL证书应具有不同的SAN。
* 证书策略必须遵循扩展验证(EV)或组织验证(OV)，而不是域验证(DV)策略。


## 为发布层配置自定义域

1. 转到&#x200B;**[!UICONTROL AdobeCloud Manager]** > **[!UICONTROL 计划概述]** > **[!UICONTROL SSL证书]**，然后添加您的SSL证书。
   ![图像](/help/assets/assets/ssl-certificate.png)
了解如何在AdobeCloud Manager中添加[SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)。

1. 添加SSL证书后，添加自定义域。 单击&#x200B;**[!UICONTROL 域设置]**&#x200B;并针对&#x200B;**[!UICONTROL Publish服务]**选项指定自定义域。
了解有关[自定义域](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)的更多信息。

1. 在对应于发布域的DNS记录中添加两个[CNAME记录](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)。
由于 DNS 传播延迟，DNS 验证可能需要几个小时才能处理。

1. 记录支持案例以促进自定义域的配置，确保它定向到交付层。

>[!NOTE]
>
将自定义域添加到允许的重定向URL列表。 该列表位于资产选择器的IMS客户端中。<br>通过提供自定义域字符串与相应的Adobe团队协调以执行此任务。
