---
title: 命名约定
description: 存放庫中的節點須遵守Java內容存放庫的命名慣例
exl-id: 3c5c39dd-b209-488b-a93e-e840786fe224
source-git-commit: c08e442e58a4ff36e89a213aa7b297b538ae3bab
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 1%

---

# 命名约定{#naming-conventions}

存放庫中的節點會受到Java內容存放庫的命名慣例的約束。 不過，AEM對頁面節點名稱施加了進一步的慣例。

## 頁面的命名慣例 {#naming-conventions-for-pages}

這些命名慣例會在不同的層級實作：

* JcrUtil：的AEM實施 [JCR公用程式](#jcr-utilities).
* PageManager： [頁面管理員](#page-manager) 提供頁面層級作業的方法。
* 在AEM UI內 {#ui-behavior}

### JCR公用程式 {#jcr-utilities}

[JcrUtil](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/jcr/JcrUtil.html) 是JCR公用程式的AEM實作。 驗證名稱特別感興趣的是它控制的字元對應和以下驗證：

* `isValidName`
   * 檢查名稱是否非空白且僅包含有效字元。
   * 可用來檢查建議的名稱是否有效。
* `createValidName`
   * 這會以任意字串建立有效的標籤。
   * 它可用來從標題建立名稱。

### 頁面管理員 {#page-manager}

[PageManager](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/PageManager.html) 提供頁面層級作業的方法，根據 [JCRUtil](#jcr-utilities).

### AEM UI行為 {#ui-behavior}

管理內容時，AEM UI：

* 符合下列任一情況時，請根據PageManager的限制來驗證名稱：
   * 提供頁面標題，以轉換為節點名稱
   * 提供了明確的節點名稱
