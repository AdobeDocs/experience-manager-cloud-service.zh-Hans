---
title: Adobe Analytics与AEM Screens Cloud集成
description: 关注本页，了解AEM Screens与Adobe Analytics的现成集成，并为您提供播放证明。
contentOwner: trushton
content-type: reference
products: SG_EXPERIENCEMANAGER/Cloud/SCREENS
topic-tags: administering
docset: aem65
role: Admin, Developer
level: Intermediate
exl-id: e22242ce-e5ce-4486-bba4-e6a89ac4fb5e
source-git-commit: abe5f8a4b19473c3dddfb79674fb5f5ab7e52fbf
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# Adobe Analytics与AEM Screens Cloud集成 {#adobe-analytics-integration-with-aem-screens}

本节涵盖以下主题：

* **概述**
* **体系结构详细信息**

## 概述 {#overview}

***AEM Screens*** 利用Adobe Analytics，借助该功能，您可以实现市场上独一无二的功能 — 跨渠道分析，即帮助将位置中显示的内容与其他数据源相关联。

AEM Screens提供了与Adobe Analytics的现成集成，并为您提供了使用证明。

本节介绍以下与AEM Screens项目与Adobe Analytics的连接相关的功能：

* 允许按设备提供播放报告验证
* 允许按资产提供播放报表的证明
* 确保捕获所有播放器事件并为其添加时间戳
* 如果播放未连接到网络，请确保所有播放器事件都存储在本地
* 允许创建反馈循环，以跟踪一段时间内的播放事件
* 允许系统根据内容作者定义的成功标准修改内容和布局

因此，Adobe Analytics与AEM Screens的集成强制执行以下操作 *目标*：

* 实现数字标牌实施的ROI
* 集成Analytics作为未来支持收集和分析使用信息的基础

## 体系结构详细信息 {#architectural-details}

AEM Screens客户想要了解在哪个时间显示了哪些内容，以及显示时间长短（汇总）。 这是标牌解决方案的常见功能。 AEM Screens使用Adobe Analytics而不是构建我们自己的分析，通过它，您可以实现市场上独一无二的东西 — 跨渠道分析，它有助于将位置中显示的内容与其他数据源相关联。

以下架构图介绍了Adobe Analytics与AEM Screens的集成：

![与Adobe Analytics集成](/help/screens-cloud/assets/analytics-architecture.png)

## 在AEM Screens Cloud中启用Adobe Analytics {#enabling-adobe-analytics-in-aem-screens-cloud}

请联系您的Adobe关系经理，以在Screens Cloud中启用Adobe分析。

## 在AEM Screens Cloud中使用Adobe Analytics服务 {#using-adobe-analytics-service-in-aem-screens}

此场景通过固件和Instrument Screens核心组件中的Analytics服务中的REST调用调用Analytics API，以明确创建和发送特定于特定用例的事件，同时允许扩展，在这种情况下，任何自定义消息都可从自定义开发的渠道发送到Analytics。

Analytics事件离线存储在indexedDB中，稍后进行分块并发送到云。

>[!NOTE]
>要了解有关事件的顺序和标准数据模型的更多信息，请参阅 [为AEM Screens配置Adobe Analytics](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/administering/analytics-integration/configuring-adobe-analytics-aem-screens.html) 以了解详细信息。
