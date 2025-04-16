---
title: API 参考材料
description: AEM具有广泛而强大的API，可用于您的数字体验项目。
exl-id: d4ef3040-5a0a-4149-9e99-09eda9605038
feature: Developing
role: Admin, Architect, Developer
source-git-commit: d9db32110e1e0aaa5bdc20bd6b4bff6da6a3a3a3
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 7%

---

# API 参考材料 {#api-reference-materials}

Adobe Experience Manager (AEM)提供了许多API用于开发应用程序和扩展AEM。 AEM基于多种开源技术而构建，这些技术也可以使用。

## AEM核心API {#core-aem-apis}

以下API是AEM的核心。

| API | 描述 |
|---|---|
| [Adobe Experience Manager as a Cloud Service](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html) | 产品抽象，如页面、资产、工作流等。 |
| [花岗岩UI](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html#) | Adobe的Open Web栈栈，提供各种基本组件（6.5 Granite材料适用于AEMaaCS） |
| [珊瑚UI](https://opensource.adobe.com/coral-spectrum/documentation/) | Adobe的云UI可视化样式，旨在提供一致的用户体验 |

<!---
|Editor core JavaScript API reference|Provides all the base objects and concepts to support authoring of content resources|
--->

>[!NOTE]
>
>有关 Experience Manager API 的最新信息，请访问 [Adobe Experience Manager as a Cloud Service APIs](https://developer.adobe.com/experience-cloud/experience-manager-apis/)。

## 其他框架 {#additional-apis}

AEM依赖于多个其他开源API。

| API | 描述 |
|---|---|
| [Apache Sling](https://sling.apache.org/apidocs/sling11/) | 使用Java内容存储库(JCR)存储和管理内容的Web框架 |
| [Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/oak_api/overview.html) | 实施可扩展的高性能分层式Java内容存储库(JCR)，以作为现代世界级网站的基础 |
| [Java内容存储库](https://www.adobe.io/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/index.html) | JCR版本2.0规范 |
| [Apache Felix](https://felix.apache.org) | Open Services Gateway Initiative (OSGi)框架和服务平台的实施 |

## API偏好设置准则 {#guidelines}

AEM基于以下四个主要Java API集构建，并按优先级降序排列。

| 优先级 | API | 描述 |
|---|---|---|
| 1 | [Adobe Experience Manager as a Cloud Service](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html) | 产品抽象，如页面、资产、工作流等。 |
| 2 | [Apache Sling](https://sling.apache.org/apidocs/sling11/) | REST和基于资源的抽象，如资源、值映射和HTTP请求。 |
| 3 | [Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/oak_api/overview.html) | 数据和内容抽象，如节点、属性和会话。 |
| 4 | [Apache Felix](https://felix.apache.org/) | OSGi应用程序容器抽象，如服务和(OSGi)组件。 |

如果API由AEM提供，则它比Sling、JCR和OSGi更受欢迎。 如果AEM不提供API，则首选使用Sling，而非JCR和OSGi。

>[!TIP]
>
>有关这些准则的详细信息，请参阅文档[了解Java API最佳实践](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/understand-java-api-best-practices.html)。

## AEM交付和内容管理服务及API {#delivery-apis}

AEM提供了可自定义的组件和内容交付选项。

| 功能 | 描述 |
|---|---|
| [核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-hans) | 适用于AEM的标准化网站内容管理(WCM)组件，可加快开发速度并降低网站的维护成本 |
| [JSON导出程序](/help/implementing/developing/components/json-exporter.md) | 以JSON数据模型格式交付任何AEM页面的内容 |
| [为组件启用 JSON 导出](/help/implementing/developing/components/enabling-json-exporter.md) | 基于建模器框架生成组件内容的JSON导出 |
| [内容片段和内容片段模型OpenAPI](/help/headless/content-fragment-openapis.md) | 内容片段和内容片段模型OpenAPI |
| [使用OpenAPI发送AEM内容片段](/help/headless/aem-content-fragment-delivery-with-openapi.md) | AEMEdge Delivery Services上的HTTP REST API，旨在从JSON格式的内容片段提供结构化内容。 |
| [内容片段GraphQL API](/help/headless/graphql-api/content-fragments.md) | 在Headless CMS实施中实现向JavaScript客户端高效投放内容片段 |
|  |  |
| [资源API](/help/assets/mac-api-assets.md) | 允许对资源执行创建 — 读取 — 更新 — 删除(CRUD)操作，包括二进制、元数据、演绎版和注释。 请参阅AEM Assets HTTP API |
| [内容片段HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md) | 通过CRUD操作直接通过HTTP API访问内容片段内容 |
| [内容片段Assets HTTP API](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/mac-api-assets.html) | 支持的HTTP资产请求的确切格式 |

>[!NOTE]
>
>有关可用的各种API的概述以及所涉及概念的比较，请参阅结构化内容交付和管理的[AEM API](/help/headless/apis-headless-and-content-fragments.md)。

## 特定于SPA的API {#spa-apis}

AEM单页应用程序(SPA)编辑器SDK框架提供了特定的JavaScript API参考。

| API | 描述 |
|---|---|
| [组件映射](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping) | 为单页应用程序提供一种将前端组件映射到Adobe Experience Manager资源类型(AEM组件)的方法 |
| [页面模型管理器](https://www.npmjs.com/package/@adobe/aem-spa-page-model-manager) | Adobe Experience Manager编辑器和Adobe Experience Manager单页应用程序(SPA)编辑器之间的解释器 |
| [React可编辑组件](https://www.npmjs.com/package/@adobe/aem-react-editable-components) | 提供React组件和集成层，以帮助您开始使用Adobe Experience Manager站点编辑器 |
| [Angular可编辑组件](https://www.npmjs.com/package/@adobe/aem-angular-editable-components) | 提供Angular组件和集成层，以开始使用Adobe Experience Manager站点编辑器 |

>[!TIP]
>
>有关单页应用程序的更多信息，请参阅[SPA简介和演练](/help/implementing/developing/hybrid/introduction.md)。
