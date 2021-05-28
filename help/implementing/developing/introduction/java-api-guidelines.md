---
title: Java API准则
description: AEM构建于一个丰富的开源软件堆栈上，该堆栈会公开许多Java API以供使用。
exl-id: 0be33ec9-a4c3-4400-99d3-ed8366c5b5f9
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---

# Java API准则{#java-api-guidelines}

Adobe Experience Manager(AEM)构建于一个丰富的开源软件堆栈上，该堆栈会公开许多Java API，以供在开发过程中使用。

AEM基于以下四个主要Java API集以首选项的降序顺序构建。

1. **[Adobe Experience Manager(AEM)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service-javadoc/index.html)**  — 页面、资产、工作流等产品抽象概念。
1. **[Apache Sling Web Framework](https://sling.apache.org/apidocs/sling11/)**  - REST和基于资源的抽象概念，如资源、值映射和HTTP请求。
1. **[JCR(Apache Jackrabbit Oak)](http://jackrabbit.apache.org/oak/docs/oak_api/overview.html)**  — 数据和内容抽象，如节点、属性和会话。
1. **[OSGi(Apache Felix)](https://felix.apache.org)**  - OSGi应用程序容器抽象，如服务和(OSGi)组件。

如果AEM提供的API比Sling、JCR和OSGi更合适。 如果AEM不提供API，则首选使用Sling而不是JCR和OSGi。

有关这些准则的详细信息，请参阅文档[了解Java API最佳实践。](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/understand-java-api-best-practices.html)
