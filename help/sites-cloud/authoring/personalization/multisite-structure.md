---
title: 如何构建目标内容的多站点管理
description: 图表显示了如何构建目标内容的多站点支持
exl-id: c6b05c2a-0897-4514-8937-e23bfcf757d5
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 100%

---

# 如何构建目标内容的多站点管理 {#how-multisite-management-for-targeted-content-is-structured}

下图显示了如何构建目标内容的多站点支持。

**/content/campaigns/&lt;brand>** 下方显示了区域，默认情况下，每个品牌都有一个自动创建的主区域。每个区域都包含自身的一组活动、体验和选件。

![多站点结构](/help/sites-cloud/authoring/assets/multisite-structure.png)

要查找目标内容，可以将页面或站点映射到区域。如果未配置区域，AEM 将回退到此特定品牌的主区域。

下图是该逻辑如何为三个站点（名为 site1、site2 和 site3）工作的示例。

![跨站点的多站点结构](/help/sites-cloud/authoring/assets/multisite-structure-2.png)

* site1 根据区域映射查找 brand1 的 myarea1 和 brand2 的 otherarea2。
* site2 查找 brand1 的 myarea1 和 brand2 的主区域，因为仅定义了 brand1 的区域映射。
* site3 查找 brand1 和 brand2 的主区域，因为根本没有为该站点定义任何其他区域映射。
