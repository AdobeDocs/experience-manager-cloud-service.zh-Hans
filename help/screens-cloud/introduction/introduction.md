---
title: AEM Screens as a Cloud Service
description: 本页介绍AEM Screensas a Cloud Service。
exl-id: b1cc0a63-ecd3-4d89-ac49-f384cc610cdc
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 1%

---

# AEM Screensas a Cloud Service简介 {#introduction-screens-cloud}

借助AEM Screensas a Cloud Service，您可以创建引人入胜的动态数字标牌体验，以便在公共空间中使用。 这是AEM Screens产品的下一个发展，在可用性和可扩展性方面实现了重大飞跃。

AEM Screensas a Cloud Service是一款数字标牌解决方案，允许营销人员大规模创建和管理动态数字体验。 此外，它还涉及不同类型的物理屏幕，作为全面数字营销策略的一部分。 它将Adobe的全渠道产品扩展到了通常的Web和移动渠道之外，还包括我们周围的数字标牌渠道。 AEM Screensas a Cloud Service通过深入了解内容创建、内容汇编、触发式事件管理以及任何公共空间中所有消费者和访客的媒体播放，提供了更相关、更符合情境、更高效且可预期的用户体验。

## 了解Screens中的组件as a Cloud Service {#understanding-components}

屏幕as a Cloud Service有两个主要组件，即：

* **[内容提供商](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/configure-screens-cloud/using-screens-content-provider.html?lang=en)**，在AEM Cloud Service或Adobe Managed Services(AMS)上运行的Screens加载项。 Screens内容提供商允许内容作者创建和管理渠道。 内容作者可以添加新内容、编辑内容，而不必担心创建显示屏或播放器注册的详细信息。 内容提供程序从开发内容、显示内容或播放器注册的基础详细信息中提供一个抽象。

* **[服务提供商](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/configure-screens-cloud/navigating-to-screens-services-provider.html?lang=en)**，在Adobe I/O运行时运行的数字标牌管理服务。 Screens服务提供程序允许内容作者、开发人员和管理员在将内容添加到渠道后，管理内容播放的显示屏和播放器。 此外， Screens Services Provider还会通知Orchestrator内容将在何处和何时在高级别播放。


## 架构概述 {#architectural-overview}

作为AEM Screensas a Cloud Service用户，您可以在渠道中添加和管理内容，从专为Screensas a Cloud Service而设计的界面(即， **Screens服务提供商** 和 **Screens内容提供商**.

![图像](/help/screens-cloud/assets/architecture-screenscloud.png)
