---
title: AEM Dispatcher Converter 工具
description: 了解如何将AEM Dispatcher上的现有配置转换为AEM as a Cloud Service Dispatcher上的配置。
exl-id: 2e95ff7b-cc94-477d-99ab-816a58998287
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 28%

---

# AEM Dispatcher 转换器 {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_dispconverter"
>title="AEM Dispatcher 转换器"
>abstract="Adobe Experience Manager Dispatcher 转换器将现有 AEM Dispatcher 配置转换为 AEM as a Cloud Service Dispatcher 配置。"

Adobe Experience Manager Dispatcher 转换器将现有 AEM Dispatcher 配置转换为 AEM as a Cloud Service Dispatcher 配置。

## Dispatcher简介 {#introduction-dispatcher}

Dispatcher是Adobe Experience Manager的缓存或/和负载平衡工具。 使用 AEM 的 Dispatcher 还有助于保护 AEM 服务器免受攻击。因此，您可以通过将Dispatcher与企业级Web服务器结合使用来提高AEM实例的安全性。

>[!NOTE]
>Dispatcher 最常见的用法是缓存来自 **AEM 发布实例**&#x200B;的响应，从而提高面向外部发布的网站的响应速度和安全性。

请参阅[Dispatcher概述](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html)，了解Dispatcher如何执行缓存、返回文档和执行负载平衡。

### Apache和Dispatcher配置和测试 {#dispatcher-configurations-cloud}

了解如何构建AEM as a Cloud Service Apache和Dispatcher配置，以及如何在部署到云环境之前在本地验证和运行该配置。

有关详细信息，请参阅[云中的Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html)。

## AEM Dispatcher 转换器 {#aem-dispatcher-converter}

AEM Dispatcher Converter能够将现有的内部部署或Managed Services Dispatcher配置Adobe为与AEM as a Cloud Service兼容的Dispatcher配置。

## 使用AEM Dispatcher Converter {#using-dispatcher-converter}

* 通过Adobe Developer CLI ：Adobe建议您通过`aio-cli-plugin-aem-cloud-service-migration`使用AEM Dispatcher Converter (适用于Adobe Developer CLI的AEM as a Cloud Service代码重构插件)。

  请参阅&#x200B;**[Git资源：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)**，以便您了解如何安装和使用插件。

* 作为独立实用程序：AEM Dispatcher Converter工具也可以作为独立实用程序运行。

  请参阅&#x200B;**[Git资源：AEM Cloud Service Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)**，以了解此工具的使用和疑难解答。

>[!IMPORTANT]
>AEM Dispatcher Converter是使用NodeJS开发的。 Adobe建议您安装NodeJS 10.0+。
