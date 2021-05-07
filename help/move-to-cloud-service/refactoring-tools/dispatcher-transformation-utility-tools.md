---
title: AEM Dispatcher Converter 工具
description: AEM Dispatcher Converter 工具
exl-id: 97eb4f3f-dc03-461a-8d7e-164065bd1e4c
translation-type: tm+mt
source-git-commit: f6c700f82bc5a1a3edf05911a29a6e4d32dd3f72
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 51%

---

# AEM Dispatcher Converter {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_dispconverter"
>title="AEM Dispatcher Converter"
>abstract="Adobe Experience Manager Dispatcher Converter将现有的AEM Dispatcher配置转换为AEM作为Cloud Service Dispatcher配置。"

Adobe Experience Manager Dispatcher Converter将现有的AEM Dispatcher配置转换为AEM作为Cloud Service Dispatcher配置。

## Dispatcher 简介 {#introduction-dispatcher}

Dispatcher 是 Adobe Experience Manager 的缓存和/或负载平衡工具。使用 AEM 的 Dispatcher 还有助于保护 AEM 服务器免受攻击。因此，您可以通过将 Dispatcher 与企业级 Web 服务器结合使用来提高 AEM 实例的安全性。

>[!NOTE]
>Dispatcher 最常见的用法是缓存来自 **AEM 发布实例**&#x200B;的响应，从而提高面向外部发布的网站的响应速度和安全性。

请参阅 [Dispatcher 概述](https://docs.adobe.com/content/help/zh-Hans/experience-manager-dispatcher/using/dispatcher.html)，了解有关 Dispatcher 如何执行缓存，返回文档和执行负载平衡的信息。

### Apache 和 Dispatcher 配置和测试{#dispatcher-configurations-cloud}

您必须了解如何构建 AEM as a Cloud Service Apache 和 Dispatcher 配置，以及在部署到云环境之前，如何在本地验证和运行该配置。

有关更多信息，请参阅[云中的 Dispatcher](https://docs.adobe.com/content/help/zh-Hans/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html)。

## AEM Dispatcher Converter {#aem-dispatcher-converter}

AEM Dispatcher Converter提供将现有的内部部署或Adobe Managed Services Dispatcher配置重构到AEM的功能，作为与Cloud Service兼容的Dispatcher配置。

## 使用 AEM Dispatcher Converter {#using-dispatcher-converter}

* 通过Adobe I/O CLI :建议通过`aio-cli-plugin-aem-cloud-service-migration`使用AEM Dispatcher Converter(AEM作为Adobe I/O CLI的Cloud Service代码重构插件)。

   请参阅&#x200B;**[Git资源：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)**&#x200B;了解如何安装和使用插件。

* 作为独立的实用程序：AEM Dispatcher Converter工具也可以作为独立实用程序执行。

   请参阅&#x200B;**[Git资源：AEM Cloud Service Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)**&#x200B;以了解此工具的使用情况和疑难解答。

>[!IMPORTANT]
>AEM Dispatcher Converter是使用NodeJS开发的。 建议安装NodeJS 10.0+。
