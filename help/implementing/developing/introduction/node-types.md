---
title: AEM 节点类型
description: AEM基于Sling，使用JCR存储库以及两者都提供的节点类型，但AEM也提供了一系列自己的节点类型。
exl-id: 82cc28ca-37e2-4ca3-b3e4-cc03bbc5bdf5
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 6%

---

# AEM 节点类型 {#aem-node-types}

由于AEM基于Sling并使用JCR存储库，因此这两种标准提供的节点类型都可以在AEM中使用：

* [JCR节点类型](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/3_Repository_Model.html#3.1.7-Node-Types)
* [Sling节点类型](https://cwiki.apache.org/confluence/display/SLING/Sling+Node+Types)

除此之外。 AEM提供了一系列自定义节点类型。 对于包含所有关联属性的最新列表， [使用CRXDE](/help/implementing/developing/tools/crxde.md) 浏览AEM存储库中的以下路径：

`/jcr:system/jcr:nodeTypes`
