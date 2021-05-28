---
title: AEM Dispatcher Converter 工具
description: AEM Dispatcher Converter 工具
exl-id: 97eb4f3f-dc03-461a-8d7e-164065bd1e4c
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 48%

---

# AEM Dispatcher Converter {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_dispconverter"
>title="AEM Dispatcher Converter"
>abstract="Adobe Experience Manager Dispatcher Converter将现有AEM Dispatcher配置转换为AEM as a Dispatcher配置。"

Adobe Experience Manager Dispatcher Converter将现有AEM Dispatcher配置转换为AEM as a Dispatcher配置。

## Dispatcher 简介 {#introduction-dispatcher}

Dispatcher 是 Adobe Experience Manager 的缓存和/或负载平衡工具。使用 AEM 的 Dispatcher 还有助于保护 AEM 服务器免受攻击。因此，您可以通过将 Dispatcher 与企业级 Web 服务器结合使用来提高 AEM 实例的安全性。

>[!NOTE]
>Dispatcher 最常见的用法是缓存来自 **AEM 发布实例**&#x200B;的响应，从而提高面向外部发布的网站的响应速度和安全性。

请参阅 [Dispatcher 概述](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=zh-Hans)，了解有关 Dispatcher 如何执行缓存，返回文档和执行负载平衡的信息。

### Apache 和 Dispatcher 配置和测试{#dispatcher-configurations-cloud}

您必须了解如何构建 AEM as a Cloud Service Apache 和 Dispatcher 配置，以及在部署到云环境之前，如何在本地验证和运行该配置。

有关更多信息，请参阅[云中的 Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html)。

## AEM Dispatcher Converter {#aem-dispatcher-converter}

AEM Dispatcher Converter提供了重构现有的内部部署或Adobe Managed Services Dispatcher配置作为与AEM兼容的Cloud Service配置到的功能。

## 使用 AEM Dispatcher Converter {#using-dispatcher-converter}

* 通过Adobe I/OCLI :建议通过`aio-cli-plugin-aem-cloud-service-migration`使用AEM Dispatcher Converter(AEM作为Adobe I/OCLI的Cloud Service代码重构插件)。

   请参阅&#x200B;**[Git资源：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** ，以了解如何安装和使用插件。

* 作为独立实用程序：AEM Dispatcher Converter工具也可以作为独立实用程序执行。

   请参阅&#x200B;**[Git资源：AEM Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)** ，了解有关此工具的使用和疑难解答的信息。

>[!IMPORTANT]
>AEM Dispatcher Converter是使用NodeJS开发的。 建议安装NodeJS 10.0+。
