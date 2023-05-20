---
title: AEM Dispatcher Converter 工具
description: AEM Dispatcher Converter 工具
exl-id: 2e95ff7b-cc94-477d-99ab-816a58998287
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 61%

---

# AEM Dispatcher 转换器 {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_dispconverter"
>title="AEM Dispatcher 转换器"
>abstract="Adobe Experience Manager Dispatcher Converter 可以将现有 AEM Dispatcher 配置转换为 AEM as a Cloud Service Dispatcher 配置。"

Adobe Experience Manager Dispatcher Converter 可以将现有 AEM Dispatcher 配置转换为 AEM as a Cloud Service Dispatcher 配置。

## Dispatcher 简介 {#introduction-dispatcher}

Dispatcher 是 Adobe Experience Manager 的缓存和/或负载平衡工具。使用 AEM 的 Dispatcher 还有助于保护 AEM 服务器免受攻击。因此，您可以通过将 Dispatcher 与企业级 Web 服务器结合使用来提高 AEM 实例的安全性。

>[!NOTE]
>Dispatcher 最常见的用法是缓存来自 **AEM 发布实例**&#x200B;的响应，从而提高面向外部发布的网站的响应速度和安全性。

请参阅 [Dispatcher 概述](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html)，了解有关 Dispatcher 如何执行缓存，返回文档和执行负载平衡的信息。

### Apache 和 Dispatcher 配置和测试 {#dispatcher-configurations-cloud}

您必须了解如何构建 AEM as a Cloud Service Apache 和 Dispatcher 配置，以及在部署到云环境之前，如何在本地验证和运行该配置。

有关更多信息，请参阅[云中的 Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html)。

## AEM Dispatcher 转换器 {#aem-dispatcher-converter}

AEM Dispatcher Converter可將現有的內部部署或Adobe Managed Services Dispatcher設定重構成與AEMas a Cloud Service相容的Dispatcher設定。

## 使用 AEM Dispatcher Converter {#using-dispatcher-converter}

* 透過Adobe I/OCLI ：建議透過以下方式使用AEM Dispatcher Converter： `aio-cli-plugin-aem-cloud-service-migration` (Adobe I/OCLI的AEMas a Cloud Service程式碼重構外掛程式)。

   請參閱 **[Git資源： aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** 瞭解如何安裝及使用外掛程式。

* 作為獨立公用程式： AEM Dispatcher Converter工具也可以作為獨立公用程式執行。

   請參閱 **[Git資源： AEM Cloud Service Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)** 以瞭解此工具的使用和疑難排解。

>[!IMPORTANT]
>AEM Dispatcher Converter是使用NodeJS開發。 建議安裝NodeJS 10.0+。
