---
title: AEMDispatcher转换工具
description: AEMDispatcher转换工具
translation-type: tm+mt
source-git-commit: d3593edcfee660d5ce0b0a8774fe3c61025cbe36
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 12%

---


# AEMDispatcher转换器 {#introduction}

Adobe Experience ManagerDispatcher转换器将现有AMSDispatcher配置转换为AEM作为Cloud ServiceDispatcher配置。

## Dispatcher简介 {#introduction-dispatcher}

Dispatcher 是 Adobe Experience Manager 的缓存和/或负载平衡工具。使用 AEM 的 Dispatcher 还有助于保护 AEM 服务器免受攻击。因此，您可以通过将 Dispatcher 与企业级 Web 服务器结合使用来提高 AEM 实例的安全性。

>[!NOTE]
>The most common use of Dispatcher is to cache responses from an **AEM publish instance**, to increase the responsiveness and security of your externally facing published website.

请参阅 [Dispatcher概述](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/dispatcher.html) ，了解调度程序如何执行缓存、返回文档和执行负载平衡。

### Apache和Dispatcher配置与测试 {#dispatcher-configurations-cloud}

您必须了解如何将AEM构建为Cloud ServiceApache和Dispatcher配置，以及如何在部署到云环境之前在本地验证和运行它。

有关详 [细信息，请参阅](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/dispatcher/overview.html) “云”中的Dispatcher。

## AEMDispatcher转换器 {#aem-dispatcher-converter}

AEMDispatcher转换器是用于将现有AMSDispatcher配置转换为AEM的实用程序，作为Cloud ServiceDispatcher配置。 此实用程序用于AMS实例。

实现的转换器 **是AEMDispatcherConfigConverter** ，它遵循转换准则。

请参 [阅将AMS转换为Adobe Experience Manager作为Cloud ServiceDispatcher配置](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html#how-to-convert-an-ams-to-an-aem-as-a-cloud-service-dispatcher-configuration) ，以将AMS转换为Adobe Experience Manager作为Cloud ServiceDispatcher配置。

## 使用AEMDispatcher转换器 {#using-dispatcher-converter}

以下部分介绍使用AEMDispatcher转换器工具所需的资源和信息。

请参阅 **[Git资源： AEMCloud ServiceDispatcher转换器](https://github.com/adobe/aem-cloud-service-dispatcher-converter)**，了解此工具的用法、限制和疑难解答。

>[!IMPORTANT]
>AEMDispatcher转换器是使用Python 3.7.3开发的。建议安装Python 3.5或更高版本。

## 限制 {#limitations}

AEMDispatcher转换器工作的假设条件是提供的调度程序配置文件夹的结构与Cloud Manager调度程序配置中描述的结构相似。


