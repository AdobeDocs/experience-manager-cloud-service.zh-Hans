---
title: 如何构建目标内容的多站点管理
description: 圖表顯示如何架構目標內容的多網站支援
exl-id: c6b05c2a-0897-4514-8937-e23bfcf757d5
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 39%

---

# 如何构建目标内容的多站点管理 {#how-multisite-management-for-targeted-content-is-structured}

下圖顯示如何架構目標內容的多網站支援。

**/content/campaigns/&lt;brand>** 下方显示了区域，默认情况下，每个品牌都有一个自动创建的主区域。每个区域都包含自身的一组活动、体验和选件。

![多站点结构](/help/sites-cloud/authoring/assets/multisite-structure.png)

若要查詢目標內容，頁面或網站可對應至某個區域。 如果沒有設定區域，AEM會退回此特定品牌的主區域。

下图是该逻辑如何为三个站点（名为 site1、site2 和 site3）工作的示例。

![跨站点的多站点结构](/help/sites-cloud/authoring/assets/multisite-structure-2.png)

* site1會根據區域對應來查詢myarea1以取得brand1，並查詢otherarea2以取得brand2。
* 網站2會查詢myarea1 for brand1和master area for brand2 ，因為只定義brand1的區域對應。
* 網站3會查詢brand1和brand2的主要區域，因為此網站完全沒有定義其他區域對應。
