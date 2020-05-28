---
title: AEM Dispatcher Converter Tool
description: AEM Dispatcher Converter Tool
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 12%

---


# AEM Dispatcher Converter {#introduction}

Adobe Experience Manager Dispatcher Converter将现有AMS Dispatcher配置作为云服务Dispatcher配置转换为AEM。

## Dispatcher简介 {#introduction-dispatcher}

Dispatcher 是 Adobe Experience Manager 的缓存和/或负载平衡工具。使用 AEM 的 Dispatcher 还有助于保护 AEM 服务器免受攻击。因此，您可以通过将 Dispatcher 与企业级 Web 服务器结合使用来提高 AEM 实例的安全性。

>[!NOTE]
>The most common use of Dispatcher is to cache responses from an **AEM publish instance**, to increase the responsiveness and security of your externally facing published website.

请参阅调 [度程序概述](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/dispatcher.html) ，了解调度程序如何执行缓存、返回文档和执行负载平衡。

### Apache和Dispatcher配置和测试 {#dispatcher-configurations-cloud}

您必须了解如何将AEM构建为云服务Apache和Dispatcher配置，以及如何在部署到云环境之前在本地验证和运行它。

有关详 [细信息，请参阅](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/dispatcher/overview.html) Cloud中的Dispatcher。

## AEM Dispatcher Converter {#aem-dispatcher-converter}

AEM Dispatcher Converter是一个实用程序，用于将现有AMS Dispatcher配置转换为AEM作为云服务Dispatcher配置。 此实用程序用于AMS实例。

实现的转换器 **是AEMDispatcherConfigConverter** ，它遵循转换准则。

请参 [阅将AMS转换为Adobe Experience Manager作为云服务调度程序配置](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/dispatcher/overview.html#how-to-convert-an-ams-to-an-aem-as-a-cloud-service-dispatcher-configuration) ，以将AMS转换为Adobe Experience Manager作为云服务调度程序配置。

## 使用AEM Dispatcher Converter {#using-dispatcher-converter}

以下部分介绍使用AEM Dispatcher Converter工具所需的资源和信息。

请参阅 **[Git资源： AEM Cloud Service Dispatcher](https://github.com/adobe/aem-cloud-service-dispatcher-converter)**Converter以了解此工具的使用、限制和疑难解答。

>[!IMPORTANT]
>AEM Dispatcher Converter是使用Python 3.7.3开发的。建议安装Python 3.5或更高版本。

## 限制 {#limitations}

AEM Dispatcher Converter工作的假设条件是提供的调度程序配置文件夹的结构与Cloud Manager调度程序配置中描述的结构相似。


