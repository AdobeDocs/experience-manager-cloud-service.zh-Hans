---
title: Java API准则
description: AEM构建于一个丰富的开放源码软件堆栈上，该软件包提供许多可供使用的Java API。
translation-type: tm+mt
source-git-commit: b927992107d7e7e4df5511a366c71449ff73ec93
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 0%

---


# Java API准则{#java-api-guidelines}

Adobe Experience Manager(AEM)构建于一个丰富的开放源码软件堆栈上，该软件包提供许多Java API，供开发过程中使用。

AEM以以下四个主要Java API集为构建基础，按首选项的降序排列。

1. **Adobe Experience Manager(** AEM)-产品抽象，如页面、资产、工作流等。
1. **[Apache Sling Web Framework](https://sling.apache.org/apidocs/sling11/)**  - REST和基于资源的抽象，如资源、价值图和HTTP请求。
1. **[JCR(Apache Jackrabbit Oak)](http://jackrabbit.apache.org/oak/docs/oak_api/overview.html)** -数据和内容抽象，如节点、属性和会话。
1. **[OSGi(Apache Felix)](https://felix.apache.org)** - OSGi应用程序容器抽象，如服务和(OSGi)组件。

如果AEM提供API，则比Sling、JCR和OSGi更喜欢它。 如果AEM不提供API，则更喜欢Sling，而不是JCR和OSGi。

有关这些准则的详细信息，请参阅文档[了解Java API最佳实践。](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/understand-java-api-best-practices.html)
