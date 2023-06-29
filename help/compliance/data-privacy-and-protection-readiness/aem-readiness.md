---
title: 数据保护和数据隐私条例 - Adobe Experience Manager as a Cloud Service 准备工作
description: 了解Adobe Experience Manager as a Cloud Service对各种数据保护和数据隐私条例的支持。 这些法规包括欧盟通用数据保护条例(GDPR)、加州消费者隐私法案，以及在实施新的AEMas a Cloud Service项目时如何实现合规性。
exl-id: 5dfa353b-84c5-4b07-bfcd-b03c2d361553
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 44%

---

# 针对数据保护和数据隐私条例的 Adobe Experience Manager as a Cloud Service 准备工作 {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>本文档的内容不构成法律建议，也不会代替法律建议。
>
>请咨询贵公司的法律部门，以获取有关数据保护和数据隐私条例的建议。

>[!NOTE]
>
>有关Adobe对隐私问题的响应以及此隐私对您这样的Adobe客户的意义的更多信息，请参阅 [Adobe隐私中心](https://www.adobe.com/cn/privacy.html).

Adobe为客户隐私管理员或AEM管理员提供文档和过程（如果可用，则使用API）。 本文档可帮助管理员处理数据保护和数据隐私请求，并帮助Adobe客户遵守这些法规。 记录的过程允许客户从外部门户或服务手动运行监管请求或调用API（如果可用）。

>[!CAUTION]
>
>此处所记录的详细信息仅限 Adobe Experience Manager as a Cloud Service。
>
>来自其他Adobe按需服务的数据以及任何相关的隐私请求要求对该服务执行操作。
>
>有关更多信息，请参阅 [Adobe隐私中心](https://www.adobe.com/cn/privacy.html).

## 简介 {#introduction}

Adobe Experience Manager as a Cloud Service的实例以及在其上运行的应用程序由Adobe客户负责和运营。

因此，GDPR、CCPA 及其他数据保护条例在很大程度上由客户负责。

作为简单介绍，数据隐私和保护法规包括以下角色需要遵守的新规则：

* 业务实体 (CCPA) 和/或数据控制方 (GDPR)

* 服务提供商 (CCPA) 和/或数据处理商 (GDPR)

此类条例中的主要条款：

1. 扩展了个人数据的定义，以包括唯一 ID（在可直接和间接识别身份的数据中）。

2. 强化了对同意书的要求。

3. 增加了对删除权利的关注（数据清除）。

4. 数据销售的选择退出。

对于 Adobe Experience Manager as a Cloud Service：

* 实例以及其上运行的应用程序由客户负责和运营。

   * 这种所有权实际上意味着客户管理管理管理法规角色，包括业务实体和服务提供商、数据控制方和数据处理商等。

   * Adobe Experience Platform Privacy Service不是AEM工作流的一部分，如下图所示。

* AEM 包括面向客户隐私管理员和/或 AEM 管理员的文档和过程，可手动或通过 API（在可用时）执行隐私监管请求。

* 未添加新的服务或 UI。

   * 而是记载了由处理隐私监管请求的客户 UI/门户使用的过程和 API。

* AEM不包括任何现成的工具来支持隐私请求工作流。

   * Adobe为客户隐私管理员和/或AEM管理员提供文档和过程，使他们能够手动运行与隐私法规相关的请求。

Adobe提供了处理与Adobe Experience Manager as a Cloud Service的访问、删除和选择退出相关的隐私请求的过程。 有时，可以从客户开发的门户或脚本中调用可用的API以帮助实现自动化。

下图说明了隐私请求工作流可能的样子（使用 Adobe Experience Manager 6.5 说明）：

![数据保护和隐私](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager as a Cloud Service 和监管准备工作 {#aem-as-a-cloud-service-and-regulatory-readiness}

有关AEMas a Cloud Service产品领域的监管文档，请参阅以下部分。

## Adobe Experience Manager as a Cloud Service 基础 {#aem-foundation}

请查看[数据保护和数据隐私条例的 AEM Foundation 准备工作](/help/compliance/data-privacy-and-protection-readiness/foundation-readiness.md)。

## Adobe Experience Manager as a Cloud Service Sites {#aem-sites}

参见 [用于数据保护和数据隐私法规的AEM Sites已准备就绪](/help/compliance/data-privacy-and-protection-readiness/sites-readiness.md)

## Adobe Experience Manager as a Cloud Service 与 Adobe Target 和 Adobe Analytics 的集成 {#aem-integration-with-adobe-target-adobe-analytics}

Adobe Experience Manager as a Cloud Service上的这些集成与支持数据保护和隐私（例如，GDPR）的服务配合使用。 Adobe Target 或 Adobe Analytics 中的任何个人数据都不会存储在与集成相关的 AEM 中。
有关更多信息，请参阅：

* [Adobe Target - 隐私概述](https://experienceleague.adobe.com/docs/target-dev/developer/implementation/privacy/cmp-privacy-and-general-data-protection-regulation.html)

* [Adobe Analytics 数据隐私工作流](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/an-gdpr-workflow.html)
