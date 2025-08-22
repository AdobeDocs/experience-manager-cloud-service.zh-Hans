---
title: 在Adobe Journey Optimizer中使用内容片段
description: 了解内容片段如何与Adobe Journey Optimizer集成和使用。
feature: Content Fragments
role: User, Developer, Architect
solution: Experience Manager Sites
exl-id: 4090ee41-80f1-4389-8961-e4af891f01ff
source-git-commit: 0fd7b2633488ceb14d34b1978a91a3a830d8762a
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 10%

---

# 使用 Adobe Journey Optimizer 的内容片段 {#content-fragments-with-journey-optimizer}

[Adobe Journey Optimizer](https://experienceleague.adobe.com/zh-hans/docs/journey-optimizer/using/get-started/get-started)帮助您为客户提供互联、情境式和个性化的体验。 通过将Adobe Experience Manager (AEM) as a Cloud Service与Adobe Journey Optimizer (AJO)集成，您可以在AJO入站渠道和AJO出站渠道中重用AEM内容；包括Web、短信、电子邮件等。

例如，您可以：

* 将您的[AEM内容片段](/help/sites-cloud/administering/content-fragments/overview.md)无缝合并到[Journey Optimizer电子邮件](https://experienceleague.adobe.com/zh-hans/docs/journey-optimizer/using/channels/email/email-landing-page)内容中
* 直接从AEM预览AJO体验

内容片段和AJO之间的连接简化了访问和利用AEM内容的过程，从而能够创建个性化的动态营销活动和历程。

有关详细信息，请参阅AJO文档：

* [在AJO中使用内容片段](https://experienceleague.adobe.com/docs/journey-optimizer/using/integrations/aem-fragments.html?lang=zh-Hans#integrations)
* [将AJO选件与内容片段集成](https://experienceleague.adobe.com/zh-hans/docs/journey-optimizer/using/decisioning/offer-decisioning/managing-offers-in-the-offer-library/configure-offers/add-representations#urls)

## Dispatcher 配置 {#dispatcher-configuration}

要允许AJO通过[内容片段管理API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)访问AEM内容片段，您需要配置Dispatcher：

* 在`dispatcher/src/conf.dispatcher.d/filters/filters.any`内：

* 添加：

  ```xml
  # Allow Content Fragments API requests, required for integration with AJO 
  /200 {/type "allow" /url "/adobe/sites/cf/*" }
  ```

## 更多信息 {#further-information}

有关更多信息，请参阅：

* [AJO外部引用扩展](/help/sites-cloud/administering/content-fragments/extension-content-fragment-ajo-external-references.md)
