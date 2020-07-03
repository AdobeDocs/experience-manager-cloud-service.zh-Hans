---
title: AEM Dispatcher Converter 工具
description: AEM Dispatcher Converter 工具
translation-type: tm+mt
source-git-commit: 66cf4fc7b5a336968dd3f8757cc56a11d6e4843e
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 94%

---


# AEM Dispatcher Converter {#introduction}

Adobe Experience Manager Dispatcher Converter 可以将现有 AMS Dispatcher 配置转换为 AEM 云服务 Dispatcher 配置。

## Dispatcher 简介 {#introduction-dispatcher}

Dispatcher 是 Adobe Experience Manager 的缓存和/或负载平衡工具。使用 AEM 的 Dispatcher 还有助于保护 AEM 服务器免受攻击。因此，您可以通过将 Dispatcher 与企业级 Web 服务器结合使用来提高 AEM 实例的安全性。

>[!NOTE]
>Dispatcher 最常见的用法是缓存来自 **AEM 发布实例**&#x200B;的响应，从而提高面向外部发布的网站的响应速度和安全性。

请参阅 [Dispatcher 概述](https://docs.adobe.com/content/help/zh-Hans/experience-manager-dispatcher/using/dispatcher.html)，了解有关 Dispatcher 如何执行缓存，返回文档和执行负载平衡的信息。

### Apache 和 Dispatcher 配置和测试{#dispatcher-configurations-cloud}

您必须了解如何构建 AEM 云服务 Apache 和 Dispatcher 配置，以及在部署到云环境之前，如何在本地验证和运行该配置。

有关更多信息，请参阅[云中的 Dispatcher](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html)。

## AEM Dispatcher Converter {#aem-dispatcher-converter}

AEM Dispatcher Converter 是一个实用程序，可用于将现有 AMS Dispatcher 配置转换为 AEM 云服务 Dispatcher 配置。此实用程序适用于 AMS 实例。

实施的转换器是 **AEMDispatcherConfigConverter**，它遵循转换准则。

请参阅[将 AMS 转换为 Adobe Experience Manager 云服务 Dispatcher 配置](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html#how-to-convert-an-ams-to-an-aem-as-a-cloud-service-dispatcher-configuration)，了解如何将 AMS 转换为 Adobe Experience Manager 云服务 Dispatcher。

## 使用 AEM Dispatcher Converter {#using-dispatcher-converter}

以下部分介绍了使用 AEM Dispatcher Converter 工具所需的资源和信息。

请参阅 **[Git 资源：AEM Cloud Service Dispatcher Converter](https://github.com/adobe/aem-cloud-service-dispatcher-converter)**，了解有关此工具的使用方法、限制和疑难解答的信息。

>[!IMPORTANT]
>AEM Dispatcher Converter 是使用 Python 3.7.3 开发的。建议安装 Python 3.5 或更高版本。

## 限制 {#limitations}

AEM Dispatcher Converter 的工作原理是假定提供的 Dispatcher 配置文件夹的结构与 Cloud Manager Dispatcher 配置中描述的结构相似。


