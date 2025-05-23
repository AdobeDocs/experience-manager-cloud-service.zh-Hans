---
title: 命名约定
description: 存储库中的节点遵循Java内容存储库的命名约定
exl-id: 3c5c39dd-b209-488b-a93e-e840786fe224
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 1%

---

# 命名约定{#naming-conventions}

存储库中的节点遵循Java内容存储库的命名约定。 但是，AEM对页面节点名称施加进一步的约定。

## 页面的命名约定 {#naming-conventions-for-pages}

这些命名惯例在各级实施：

* JcrUtil： [JCR实用程序](#jcr-utilities)的AEM实现。
* PageManager： [页面管理器](#page-manager)提供页面级操作的方法。
* 在AEM UI {#ui-behavior}中

### JCR实用程序 {#jcr-utilities}

[JcrUtil](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/jcr/JcrUtil.html)是JCR实用程序的AEM实现。 验证名称特别感兴趣的是它控制的字符映射以及以下验证：

* `isValidName`
   * 检查名称是否不为空且仅包含有效字符。
   * 可用于检查建议的名称是否有效。
* `createValidName`
   * 这会根据任意字符串创建一个有效标签。
   * 它可用于从标题创建名称。

### 页面管理器 {#page-manager}

[PageManager](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/PageManager.html)提供了基于[JCRUtil](#jcr-utilities)的页面级操作方法。

### AEM UI行为 {#ui-behavior}

管理内容时，AEM UI会：

* 在执行以下任一操作时，根据PageManager施加的限制验证名称：
   * 提供了页面标题以转换为节点名称
   * 提供了显式节点名称
