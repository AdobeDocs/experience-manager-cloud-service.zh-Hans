---
title: 如何构建目标内容的多站点管理
description: 图表显示了如何构建目标内容的多站点支持
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# 如何构建目标内容的多站点管理 {#how-multisite-management-for-targeted-content-is-structured}

下图显示了如何构建目标内容的多站点支持。

Areas appear underneath **/content/campaigns/&lt;brand>** and by default each brand has a master area, which is created automatically. 每个区域都包含自身的一组活动、体验和选件。

![多站点结构](/help/sites-cloud/authoring/assets/multisite-structure.png)

要查找目标内容，可以将页面或站点映射到区域。如果未配置区域，AEM 将回退到此特定品牌的主区域。

下图是该逻辑如何为三个站点（名为 site1、site2 和 site3）工作的示例。

![跨站点的多站点结构](/help/sites-cloud/authoring/assets/multisite-structure-2.png)

* site1 根据区域映射查找 brand1 的 myarea1 和 brand2 的 otherarea2。
* site2 查找 brand1 的 myarea1 和 brand2 的主区域，因为仅定义了 brand1 的区域映射。
* site3 查找 brand1 和 brand2 的主区域，因为根本没有为该站点定义任何其他区域映射。
