---
title: 命名约定
description: 存储库中的节点受Java内容存储库的命名约定的约束
exl-id: 3c5c39dd-b209-488b-a93e-e840786fe224
source-git-commit: c08e442e58a4ff36e89a213aa7b297b538ae3bab
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 10%

---

# 命名约定{#naming-conventions}

存储库中的节点须遵守 Java 内容存储库的命名约定。但是，AEM对页面节点的名称作了进一步的约定。

## 页面的命名约定 {#naming-conventions-for-pages}

这些命名约定在不同级别实施：

* JcrUtil:的AEM实施 [JCR实用程序](#jcr-utilities).
* PageManager:the [页面管理器](#page-manager) 提供页面级操作的方法。
* 在AEM UI中 {#ui-behavior}

### JCR实用程序 {#jcr-utilities}

[JcrUtil](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/jcr/JcrUtil.html) 是JCR实用程序的AEM实施。 验证名称时特别需要注意的是它所控制的字符映射和以下验证：

* `isValidName`
   * 检查名称是否不为空，并且只包含有效字符。
   * 可用于检查建议的名称是否有效。
* `createValidName`
   * 这会从任意字符串中创建有效标签。
   * 它可用于从标题创建名称。

### 页面管理器 {#page-manager}

[PageManager](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/PageManager.html) 提供页面级别操作的方法，具体依据 [JCRUtil](#jcr-utilities).

### AEM UI行为 {#ui-behavior}

管理内容时，AEM UI:

* 在以下任一情况下，根据PageManager施加的限制验证名称：
   * 提供页面标题以转换为节点名称
   * 提供了明确的节点名称
