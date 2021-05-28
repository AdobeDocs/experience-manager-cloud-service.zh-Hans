---
title: 数据保护和数据隐私法规 — Adobe Experience Manager作为Cloud Service就绪
description: 了解Adobe Experience Manager作为对各种数据保护和数据隐私法规的Cloud Service支持；包括欧盟《通用数据保护条例》(GDPR)、《加州消费者隐私法案》，以及在实施新的AEM as a Cloud Service项目时如何遵守这些规定。
exl-id: 5dfa353b-84c5-4b07-bfcd-b03c2d361553
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 2%

---

# Adobe Experience Manager作为数据保护和数据隐私法规的Cloud Service就绪{#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>本文档的内容不构成法律建议，也不会代替法律建议。
>
>请咨询贵公司的法律部门，以获取有关数据保护和数据隐私法规的建议。

>[!NOTE]
>
>有关Adobe对隐私问题的响应以及这对Adobe客户有何影响的更多信息，请参阅[Adobe的隐私中心](https://www.adobe.com/privacy.html)。

Adobe将提供文档和规程（如果有API），以便客户隐私管理员或AEM管理员处理数据保护和数据隐私请求，并帮助我们的客户遵守这些法规。 记录的过程将允许客户手动执行法规请求，或通过从外部门户或服务调用API（如果可用）来执行法规请求。

>[!CAUTION]
>
>此处记录的详细信息仅限于Adobe Experience Manager作为Cloud Service。
>
>来自其他Adobe点播服务的数据以及任何相关的隐私请求，将要求对该服务采取相应的操作。
>
>有关详细信息，请参阅[Adobe的隐私中心](https://www.adobe.com/privacy.html)。

## 简介 {#introduction}

作为Cloud Service的Adobe Experience Manager实例以及在其上运行的应用程序，都由我们的客户拥有和运行。

因此，数据保护法规（如GDPR、CCPA等）在很大程度上由客户负责。

作为非常简短的介绍，数据隐私和保护法规包括了新的规则，这些规则将遵循以下角色：

* 业务实体(CCPA)和/或数据控制者(GDPR)

* 服务提供商(CCPA)和/或数据处理者(GDPR)

这些条例的主要规定是：

1. 扩展了对个人数据的定义，以包含所有唯一ID;直接和间接可识别数据中。

2. 增强了同意要求。

3. 增加了对删除权限（数据擦除）的关注。

4. 选择退出数据销售。

对于Adobe Experience Manager作为Cloud Service:

* 这些实例以及在其上运行的应用程序都归客户所有和操作。

   * 这实际上意味着客户可以管理法规角色，包括业务实体和服务提供商、数据控制者和数据处理者等。

   * 如下图所示，Adobe Experience Platform Privacy Service将不属于AEM工作流的一部分。

* AEM包含有关客户隐私管理员和/或AEM管理员执行隐私法规请求的文档和程序；手动或通过API（如果可用）。

* 未添加新服务或UI。

   * 而是记录了过程和API，以供处理隐私法规请求的客户UI/门户使用。

* AEM将不包含任何用于支持隐私请求工作流的现成工具。

   * Adobe将为客户的隐私管理员和/或AEM管理员提供文档和程序，使他们能够手动执行与隐私法规相关的请求。

Adobe正在提供处理与Adobe Experience Manager as a Cloud Service的访问、删除和选择退出相关的隐私请求的过程。 在某些情况下，可以从客户开发的门户或脚本中调用一些可用的API，以帮助实现自动化。

下图说明了隐私请求工作流的外观(使用Adobe Experience Manager 6.5进行了说明):

![数据保护和隐私](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager as aCloud Service和法规就绪{#aem-as-a-cloud-service-and-regulatory-readiness}

有关AEM as a Cloud Service产品区域的法规文档，请参阅以下部分。

## Adobe Experience Manager as a Cloud Service 基础 {#aem-foundation}

请参阅[AEM数据保护和数据隐私法规的基础就绪](/help/onboarding/data-privacy-and-protection-readiness/foundation-readiness.md)。

## Adobe Experience Manager as a Cloud Service 站点 {#aem-sites}

请参阅[AEM Sites数据保护和数据隐私法规的就绪性。](/help/onboarding/data-privacy-and-protection-readiness/sites-readiness.md)

## Adobe Experience Manager as a Adobe Target与Adobe Analytics的Cloud Service集成{#aem-integration-with-adobe-target-adobe-analytics}

这些Adobe Experience Manager作为Cloud Service集成，提供了数据保护和隐私（例如GDPR）就绪服务。 AEM中不存储与集成相关的来自Adobe Target或Adobe Analytics的个人数据。
有关更多信息，请参阅：

* [Adobe Target — 隐私概述](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/privacy.html)

* [Adobe Analytics数据隐私工作流程](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-workflow.html)
