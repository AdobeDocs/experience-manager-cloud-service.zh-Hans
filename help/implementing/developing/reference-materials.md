---
title: API参考资料
description: AEM具有广泛而功能强大的API，您可以将其用于数字体验项目。
source-git-commit: 4134d87ca40f7834605c7d3496f05ef80fbab554
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 4%

---

# API参考资料 {#api-reference-materials}

Adobe Experience Manager(AEM)提供了许多用于开发应用程序和扩展AEM的API。 AEM基于许多开源技术构建，这些技术也可以利用。

## AEM核心API {#core-aem-apis}

以下API是AEM的核心。

| API | 描述 |
|---|---|
| [Adobe Experience Manager as a Cloud Service](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/index.html) | 产品抽象概念，如页面、资产、工作流等。 |
| [Granite用户界面](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html#) | Adobe的开放式Web堆栈，提供各种基本组件（请注意，6.5 Granite材料适用于AEMaCS） |
| [Coral用户界面](https://opensource.adobe.com/coral-spectrum/documentation/) | Adobe的云UI可视样式，旨在提供用户体验的一致性 |

<!---
|Editor core JavaScript API reference|Provides all the base objects and concepts to support authoring of content resources|
--->

## 其他框架 {#additional-apis}

AEM依赖于许多其他开源API。

| API | 描述 |
|---|---|
| [Apache Sling](https://sling.apache.org/apidocs/sling11/) | 使用Java内容存储库(JCR)存储和管理内容的Web框架 |
| [Apache Jackrabbit Oak](http://jackrabbit.apache.org/oak/docs/oak_api/overview.html) | 实施可扩展且高性能的分层Java内容存储库(JCR)，以用作现代世界级网站的基础 |
| [Java内容存储库](https://docs.adobe.com/content/docs/en/spec/javax.jcr/javadocs/jcr-2.0/index.html) | JCR版本2.0的规范 |
| [Apache Felix](https://felix.apache.org) | 开放服务网关倡议框架和服务平台的实施 |

## API首选项准则 {#guidelines}

AEM基于以下四个主要Java API集以首选项的降序顺序构建。

| 优先级 | API | 描述 |
|---|---|---|
| 1 | [Adobe Experience Manager as aCloud Service](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/index.html) | 产品抽象概念，如页面、资产、工作流等。 |
| 2 | [Apache Sling](https://sling.apache.org/apidocs/sling11/) | REST和基于资源的抽象概念，如资源、值映射和HTTP请求。 |
| 3 | [Apache Jackrabbit Oak](http://jackrabbit.apache.org/oak/docs/oak_api/overview.html) | 数据和内容抽象，如节点、属性和会话。 |
| 4 | [Apache Felix](https://felix.apache.org/) | OSGi应用程序容器抽象，如服务和(OSGi)组件。 |

如果AEM提供的API比Sling、JCR和OSGi更合适。 如果AEM不提供API，则首选使用Sling而不是JCR和OSGi。

>[!TIP]
>
>有关这些准则的详细信息，请参阅文档[了解Java API最佳实践。](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/understand-java-api-best-practices.html)

## AEM交付和内容管理服务和API {#delivery-apis}

AEM提供了可自定义的组件和内容交付选项。

| API | 描述 |
|---|---|
| [核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans) | 针对AEM的标准化Web内容管理(WCM)组件，可加快开发时间并降低网站的维护成本 |
| [JSON导出程序](/help/implementing/developing/components/json-exporter.md) | 以JSON数据模型格式交付任何AEM页面的内容 |
| [为组件启用JSON导出](/help/implementing/developing/components/enabling-json-exporter.md) | 基于建模器框架生成组件内容的JSON导出 |
| [资产](/help/assets/mac-api-assets.md) | 允许对资产（包括二进制文件、元数据、演绎版和注释）执行创建 — 读取 — 更新 — 删除(CRUD)操作。 请参阅AEM Assets HTTP API |
| [内容片段HTTP](/help/assets/content-fragments/assets-api-content-fragments.md) | 通过CRUD操作直接通过HTTP API访问内容片段内容 |
| [内容片段GraphQL](/help/assets/content-fragments/graphql-api-content-fragments.md) | 在无头CMS实施中，支持将内容片段高效交付到JavaScript客户端 |
| [内容片段资产HTTP](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/mac-api-assets.html) | 支持的HTTP资产请求的确切格式 |

## SPA特定的API {#spa-apis}

AEM单页应用程序(SPA)编辑器SDK框架提供了特定的JavaScript API引用。

| API | 描述 |
|---|---|
| [组件映射](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping) | 为单页应用程序提供了一种将前端组件映射到Adobe Experience Manager资源类型(AEM组件)的方法 |
| [页面模型管理器](https://www.npmjs.com/package/@adobe/aem-spa-page-model-manager) | Adobe Experience Manager编辑器和Adobe Experience Manager单页应用程序(SPA)编辑器之间的解释程序 |
| [React可编辑的组件](https://www.npmjs.com/package/@adobe/aem-react-editable-components) | 提供React组件和集成层，以帮助您开始使用Adobe Experience Manager站点编辑器 |
| [Angular可编辑的组件](https://www.npmjs.com/package/@adobe/aem-angular-editable-components) | 提供Angular组件和集成层，以帮助您开始使用Adobe Experience Manager站点编辑器 |

>[!TIP]
>
>有关单页应用程序的更多信息，请参阅[SPA简介和演练](/help/implementing/developing/hybrid/introduction.md)。
