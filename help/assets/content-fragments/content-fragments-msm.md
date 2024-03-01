---
title: 使用MSM和活动副本重用内容片段
description: 了解如何使用MSM的Live Copy功能在多个位置使用相同或相似的内容片段内容，同时与源内容同步。
source-git-commit: 3ce1a982055c2f9c900edbd88e079deb6d3a036a
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 10%

---

# 使用MSM重用内容片段 {#reuse-content-fragments-using-msm}

多站点管理器(MSM)和Live Copy功能允许您在多个位置使用相同的内容，同时与源内容同步。

* 使用MSM Live Copies ，您可以：
   * 创建内容一次，然后
   * 在同一站点或其他站点或应用程序的其他区域重复使用此内容。
* 之后，MSM 将维护您的源内容与其 Live Copy 之间的实时关系，以便：
   * 当您更改源内容时，源和活动副本将同步。
   * 可以通过断开各个子页面和/或组件的实时关系来仅对 Live Copy 的内容进行调整。

有关MSM概念的详细概述，请参阅 [重用内容：多站点管理器和Live Copy](/help/sites-cloud/administering/msm/overview.md).

>[!NOTE]
>
>[多站点管理器(MSM)](/help/sites-cloud/administering/msm/overview.md) 通过Adobe Experience Manager中的功能，用户可重复使用一次创作，然后跨多个Web位置重复使用的内容。

使用MSM获取内容片段，您可以：

* 创建内容片段一次，然后创建（链接）这些片段的副本以在站点或应用程序的其他区域重用。
* 通过更新一次源副本，然后将更改推送到（实时）副本来保持多个副本的同步。
* 通过暂时或永久挂起父片段和子片段之间的链接（无论是完全悬挂还是针对其变体或字段）进行本地更改。

MSM for Content Fragments与内容片段编辑器中的功能相结合，允许您在字段级别中断和恢复继承。

>[!CAUTION]
>
>MSM用于内容片段仅在通过使用内容片段时可用 **资产** 控制台。
>
>MSM功能为 *非* 使用时可用 **内容片段** 控制台。

## 操作方法 {#how-to}

有关将MSM用于内容片段（也适用于Assets）的详细信息，请参阅以下文档：

* 使用方法 [内容片段（和资产）的MSM](/help/assets/reuse-assets-using-msm.md)

* [创建Live Copy](/help/assets/reuse-assets-using-msm.md)

  >[!CAUTION]
  >
  >如果要使用MSM创建内容片段的副本)，则任意 **独特** 应从在各自中使用的所有数据类型中删除约束 [内容片段模型](/help/assets/content-fragments/content-fragments-models.md).

* [查看源和Live Copy的属性和状态](/help/assets/reuse-assets-using-msm.md#properties)
* [将修改从源传播到Live Copy](/help/assets/reuse-assets-using-msm.md#rollout-sync)
* 取消并恢复以下对象的继承：
   * 中的字段和变量 [内容片段编辑器](/help/assets/content-fragments/content-fragments-variations.md#inheritance)
   * [相关资源的元数据](/help/assets/content-fragments/content-fragments-variations.md#canceling-reenabling-inheritance-individual-items)
* [暂停和恢复关系](/help/assets/reuse-assets-using-msm.md#suspend-resume)
* [删除实时关系](/help/assets/reuse-assets-using-msm.md#detach)
* [比较内容片段（和资产）的MSM与站点的MSM](/help/assets/reuse-assets-using-msm.md#comparison)

## 限制 {#limitations}

* 对于内容片段，修改时触发器和关联的转出配置不存在。