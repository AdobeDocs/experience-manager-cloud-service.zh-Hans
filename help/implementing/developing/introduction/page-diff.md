---
title: 開發和頁面差異
description: 瞭解頁面差異功能如何運作以及它如何影響開發人員
exl-id: 03c08616-2203-4b90-bed6-4836266e2507
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 1%

---

# 開發和頁面差異 {#developing-and-page-diff}

## 功能概述 {#feature-overview}

內容建立是一個反複的過程。 以效率撰寫需要能夠檢視反複專案之間有何變更。 檢視一個頁面版本然後檢視另一個頁面版本會效率低下，並容易出錯。 作者想要能夠並排比較目前頁面與先前版本，並醒目提示差異。

頁面差異可讓使用者將目前頁面與啟動、舊版等專案進行比較。 如需此使用者功能的詳細資訊，請參閱 [頁面差異](/help/sites-cloud/authoring/features/page-diff.md).

## 作業詳細資料 {#operation-details}

比較頁面的版本時，使用者想要比較的先前版本會由AEM在背景中重新建立，以方便差異分析。 這是為了能夠呈現內容 [用於並排比較](/help/sites-cloud/authoring/features/page-diff.md).

此重新建立操作由AEM內部完成，對使用者而言是透明的，不需要任何干涉。 不過，管理員檢視存放庫（例如CRX DE Lite）時，會在內容結構中看到這些重新建立的版本。

比較內容時，系統會在下列位置重新建立整個樹狀結構，一直到要比較的頁面：

`/tmp/versionhistory/`

清除工作會自動執行以清除此暫存內容。

## 限制 {#limitations}

差異會在使用者端透過DOM比較發生，讓差異流程變得簡單，但開發人員需要考慮許多限制。

* 此功能使用的CSS類別名稱與AEM產品沒有間隔。 如果頁面上包含其他自訂CSS類別或具有相同名稱的第三方CSS類別，則差異的顯示可能會受到影響。

   * `html-added`
   * `html-removed`
   * `cq-component-added`
   * `cq-component-removed`
   * `cq-component-moved`
   * `cq-component-changed`

* 由於diff是使用者端並在頁面載入時執行，在使用者端diff服務執行後對DOM所做的任何調整都不會計算在內。 這可能會影響

   * 使用AJAX來包含內容的元件
   * 单页面应用程序
   * 在使用者互動時操控DOM的Javascript型元件。
