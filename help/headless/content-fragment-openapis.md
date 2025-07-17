---
title: Content Fragments 和 Content Fragment Models OpenAPIs
description: 了解 Content Fragments 和 Content Fragment Models OpenAPIs。
exl-id: 077eed73-a066-4273-b2f5-da4bf5cd900c
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: d683051387af5c0de45917a50003c2194d887bc4
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 47%

---

# 内容片段和内容片段模型管理OpenAPI {#content-fragments-and-content-fragment-models-management-openapis}

内容片段管理 API 的现代化 OpenAPI 实现允许开发人员以编程方式在 AEM 作者上执行创建、读取、更新和删除操作，以管理存储在 AEM 中的内容片段模型和内容片段。这些 API 支持多种用例。

内容片段的现有 [资产 HTTP API](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/assets/admin/mac-api-assets) 使用应迁移至新的 Content Fragment Management OpenAPI。有关完整文档，请参阅 [Content Fragment Management API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)。

>[!NOTE]
>
>当您未登录AEM时，需要授权才能访问OpenAPI；例如，当您从其他产品将OpenAPI用作集成的一部分时。
>
>有关授权您访问OpenAPI的详细信息，请参阅[基于OpenAPI的API](/help/implementing/developing/open-api-based-apis.md)。

>[!CAUTION]
>
>默认情况下，发布时禁用内容片段管理OpenAPI。 为此，对于面向投放的用例，我们建议使用[内容片段投放OpenAPI](/help/headless/aem-content-fragment-delivery-with-openapi.md)。

>[!NOTE]
>
>有关可用的各种API的概述以及所涉及概念的比较，请参阅结构化内容交付和管理的[AEM API](/help/headless/apis-headless-and-content-fragments.md)。