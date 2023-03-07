---
title: AEM Screens as a Cloud Service 简介
description: 此页面用于介绍 AEM Screens as a Cloud Service。
exl-id: b1cc0a63-ecd3-4d89-ac49-f384cc610cdc
source-git-commit: 4b76fbbb1b58324065b39d6928027759b0897246
workflow-type: ht
source-wordcount: '382'
ht-degree: 100%

---

# AEM Screens as a Cloud Service 简介 {#introduction-screens-cloud}

借助 AEM Screens as a Cloud Service，您可以创建旨在公共场所使用的引人入胜的动态数字标牌体验。它是 AEM Screens 产品的下一个演进，代表了可用性和可扩展性的重大飞跃。

AEM Screens as a Cloud Service 是一种数字标牌解决方案，允许营销人员大规模创建和管理动态数字体验。此外，它还涉及不同类型的物理屏幕，而这是全面数字营销策略的一部分。它将 Adobe 的全渠道产品扩展到常见的网络和移动渠道之外，从而也将我们周围的数字标牌渠道包含在内。AEM Screens as a Cloud Service 通过深入了解面向任意公共场所内的所有消费者和访客的内容创建、内容汇编、已触发事件管理和媒体播放，实现更相关、上下文相关、更高效和更加可预见的用户体验。

## 了解 Screens as a Cloud Service 中的组件 {#understanding-components}

Screens as a Cloud Service 有两个主要组件，即：

* **[Content Provider](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/configure-screens-cloud/using-screens-content-provider.html?lang=en)**，它是在 AEM Cloud Service 或 Adobe Managed Services (AMS) 上运行的 Screens 加载项。Screens Content Provider 可让内容作者创建和管理渠道。内容作者可以添加新内容和编辑内容，而无需担心创建显示或播放器注册的细节。Content Provider 可以提取开发内容、显示或播放器注册的底层细节。

* **[Services Provider](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/configure-screens-cloud/navigating-to-screens-services-provider.html?lang=en)**，它是在 Adobe I/O Runtime 上运行的数字标牌管理服务。Screens Services Provider 可让内容作者、开发人员和管理员在内容被添加到渠道后管理内容播放的显示和播放器。此外，Screens Services Provider 会通知编排器在何处以及何时在高级别播放内容。


## 架构概述 {#architectural-overview}

作为 AEM Screens as a Cloud Service 用户，您可以从专为 Screens as a Cloud Service 设计的界面（即 **Screens Services Provider** 和 **Screens Content Provider**）添加和管理渠道中的内容、注册和管理显示和播放器。

![图像](/help/screens-cloud/assets/architecture-screenscloud.png)
