---
title: 数据保护和数据隐私法规- Adobe Experience Manager即云服务就绪性
description: '了解Adobe Experience Manager作为各种数据保护和数据隐私法规的云服务支持； 包括欧盟一般数据保护规定(GDPR)、加利福尼亚消费者隐私法以及在将新AEM作为云服务项目实施时如何遵守这些规定。 '
translation-type: tm+mt
source-git-commit: 2b7ee2b7b0ce351ed48aeb2f3135c947eafe7247
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 1%

---


# Adobe Experience Manager作为云服务就绪性，可用于数据保护和数据隐私法规 {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>本文档的内容不构成法律咨询，不能代替法律咨询。
>
>请咨询您的公司的法律部门，以获取有关数据保护和数据隐私法规的建议。

>[!NOTE]
>
>有关Adobe对隐私权问题的回应，以及这对您作为Adobe客户意味着什么的更多信息，请 [参阅Adobe隐私中心](https://www.adobe.com/privacy.html)。

Adobe将提供文档和过程（如果有API），供客户隐私管理员或AEM管理员处理数据保护和数据隐私请求，并帮助客户遵守这些规定。 记录的过程将允许客户手动或通过调用API（如果可用）从外部门户或服务执行法规要求。

>[!CAUTION]
>
>此处记录的详细信息仅限于Adobe Experience Manager作为云服务。
>
>来自其他Adobe按需服务的数据以及任何相关隐私请求将要求对该服务采取相应操作。
>
>有关详细信 [息，请参阅Adobe隐私中心](https://www.adobe.com/privacy.html)。

## 简介 {#introduction}

Adobe Experience Manager作为云服务的实例及其上运行的应用程序由我们的客户拥有和操作。

因此，GDPR、CCPA等数据保护法规在很大程度上是客户的责任。

作为非常简短的介绍，数据隐私和保护法规包括新规则，其后将遵循：

* 业务实体(CCPA)和／或数据控制者(GDPR)

* 服务提供商(CCPA)和／或数据处理者(GDPR)

本条例的主要规定是：

1. 扩展了个人数据的定义，以包含所有唯一ID; 直接和间接可识别数据。

2. 加强同意要求。

3. 增加了对删除权限（数据擦除）的关注。

4. 选择退出数据销售。

对于Adobe Experience Manager作为云服务：

* 客户拥有并操作在这些实例上运行的应用程序。

   * 这有效地意味着客户管理法规角色，包括业务实体和服务提供商、数据管理者和数据处理者等。

   * Adobe Experience Platform Privacy Service不属于AEM工作流程的一部分，如下图所示。

* AEM包括客户隐私管理员和／或AEM管理员执行隐私法规请求的文档和过程； 手动或通过API（如果可用）。

* 未添加新服务或UI。

   * 相反，过程和API已记录在案，供处理隐私法规请求的客户UI/门户使用。

* AEM将不包含任何现成的工具，以支持隐私请求工作流。

   * Adobe将为客户的隐私管理员和／或AEM管理员提供文档和过程，允许他们手动执行与隐私法规相关的请求。

Adobe将提供处理与Adobe Experience Manager作为云服务的访问、删除和选择退出相关的隐私请求的程序。 在某些情况下，可以从客户开发的门户或脚本中调用API来帮助实现自动化。

下图说明了隐私请求工作流程的外观（使用Adobe Experience Manager 6.5进行说明）:

![数据保护和隐私](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager作为云服务和法规准备 {#aem-as-a-cloud-service-and-regulatory-readiness}

有关AEM作为云服务的产品区域的法规文档，请参阅以下各节。

## Adobe Experience Manager作为云服务基础 {#aem-foundation}

See [AEM Foundation Readiness for Data Protection and Data Privacy Regulations](/help/onboarding/data-privacy-and-protection-readiness/foundation-readiness.md).

## Adobe Experience Manager 云服务站点 {#aem-sites}

See [AEM Sites Readiness for Data Protection and Data Privacy Regulations.](/help/onboarding/data-privacy-and-protection-readiness/sites-readiness.md)

## Adobe Experience Manager作为与Adobe目标和Adobe Analytics的云服务集成 {#aem-integration-with-adobe-target-adobe-analytics}

这些Adobe Experience Manager作为云服务集成，提供数据保护和隐私（例如GDPR）就绪服务。 在AEM中，与集成相关的Adobe目标或Adobe Analytics中不存储任何个人数据。
有关更多信息，请参阅：

* [Adobe目标-隐私概述](https://docs.adobe.com/content/help/en/target/using/implement-target/before-implement/privacy/privacy.html)

* [Adobe Analytics数据隐私工作流程](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-workflow.html)
