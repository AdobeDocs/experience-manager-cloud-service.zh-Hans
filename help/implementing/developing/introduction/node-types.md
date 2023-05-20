---
title: AEM 节点类型
description: AEM以Sling為基礎，並使用JCR存放庫以及兩者都提供的節點型別，但AEM也提供自己的一系列節點型別。
exl-id: 82cc28ca-37e2-4ca3-b3e4-cc03bbc5bdf5
source-git-commit: 08559417c8047c592f2db54321afe68836b75bd1
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 5%

---

# AEM 节点类型 {#aem-node-types}

由於AEM以Sling為基礎，並使用JCR存放庫，因此這兩個標準提供的節點型別都可以在AEM中使用：

* [JCR節點型別](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/3_Repository_Model.html#3.1.7-Node-Types)
* [Sling節點型別](https://cwiki.apache.org/confluence/display/SLING/Sling+Node+Types)

除此之外， AEM提供一系列自訂節點型別。 對於具有所有關聯屬性的最新清單， [使用CRXDE](/help/implementing/developing/tools/crxde.md) 若要瀏覽AEM存放庫中的下列路徑：

`/jcr:system/jcr:nodeTypes`
