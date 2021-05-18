---
title: Java API准则
description: AEM构建于一个丰富的开放源码软件堆栈上，它公开了许多可用的Java API。
exl-id: 0be33ec9-a4c3-4400-99d3-ed8366c5b5f9
source-git-commit: cbcc20e75e4a0cb6d0e060039f4945ff4a85ff5c
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---

# Java API准则{#java-api-guidelines}

Adobe Experience Manager(AEM)构建于一个丰富的开放源码软件堆栈上，它公开了许多在开发过程中使用的Java API。

AEM以以下四个主要Java API集为构建基础，按首选项的降序排列。

1. **[Adobe Experience Manager(AEM](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/index.html)** ) — 产品抽象，如页面、资产、工作流等。
1. **[Apache Sling Web Framework](https://sling.apache.org/apidocs/sling11/)**  - REST和基于资源的抽象，如资源、值映射和HTTP请求。
1. **[JCR(Apache Jackrabbit Oak)](http://jackrabbit.apache.org/oak/docs/oak_api/overview.html)**  — 数据和内容抽象，如节点、属性和会话。
1. **[OSGi(Apache Felix)](https://felix.apache.org)** - OSGi应用程序容器抽象，如服务和(OSGi)组件。

如果AEM提供API，则比Sling、JCR和OSGi更喜欢它。 如果AEM不提供API，则首选Sling，而非JCR和OSGi。

有关这些准则的详细信息，请参阅文档[了解Java API最佳实践。](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/understand-java-api-best-practices.html)
