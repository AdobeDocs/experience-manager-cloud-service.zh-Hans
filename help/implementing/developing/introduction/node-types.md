---
title: AEM节点类型
description: AEM基于Sling，并且使用JCR存储库，该存储库具有由二者提供的节点类型，但AEM还提供一系列其自己的节点类型。
translation-type: tm+mt
source-git-commit: 020cebfa714c098f032df963b7105503c741e748
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---


# AEM节点类型{#aem-node-types}

由于AEM基于Sling并使用JCR存储库，因此这两个标准提供的节点类型都可用于AEM::

* [JCR节点类型](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/3_Repository_Model.html#3.1.7-Node-Types)
* [Sling节点类型](https://cwiki.apache.org/confluence/display/SLING/Sling+Node+Types)

除了这些。 AEM提供一系列自定义节点类型。 对于具有所有关联属性的最新列表,[使用CRXDE](/help/implementing/developing/tools/crxde.md)浏览AEM存储库中的以下路径：

`/jcr:system/jcr:nodeTypes`
