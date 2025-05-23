---
title: 使用MSM和活动副本重用内容片段
description: 了解如何使用MSM的Live Copy功能在多个位置使用相同或相似的内容片段内容，同时与源内容同步。
exl-id: f050b2d1-856c-4cdb-ac74-bc78016f144a
feature: Content Fragments
role: User
solution: Experience Manager Sites
source-git-commit: f66ea281e6abc373e9704e14c97b77d82c55323b
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 10%

---

# 使用MSM重用内容片段 {#reuse-content-fragments-using-msm}

多站点管理器(MSM)和Live Copy功能允许您在多个位置使用相同的内容，同时与源内容同步。

* 使用MSM活动副本，您可以：
   * 创建内容一次，然后
   * 在同一站点或其他站点或应用程序的其他区域重复使用此内容。
* 之后，MSM 将维护您的源内容与其 Live Copy 之间的实时关系，以便：
   * 当您更改源内容时，源和活动副本将同步。
   * 可以通过断开各个子页面和/或组件的实时关系来仅对 Live Copy 的内容进行调整。

有关MSM概念的详细概述，请参阅[重用内容：多站点管理器和Live Copy](/help/sites-cloud/administering/msm/overview.md)。

>[!NOTE]
>
>Adobe Experience Manager中的[多站点管理器(MSM)](/help/sites-cloud/administering/msm/overview.md)功能使用户能够重复使用一次创作，然后跨多个Web位置重复使用的内容。

使用MSM获取内容片段，您可以：

* 创建内容片段一次，然后创建（链接）这些片段的副本以在站点或应用程序的其他区域重用。
* 通过将源副本更新一次，然后将更改推送到（实时）副本，来保持多个副本的同步。
* 通过暂时或永久暂停父片段与子片段之间的链接进行本地更改；完全暂停或暂停其变体或字段的链接。

MSM for Content Fragments与内容片段编辑器中的功能相结合，允许您在字段级别中断和恢复继承。

>[!CAUTION]
>
>只有在通过&#x200B;**Assets**&#x200B;控制台使用内容片段时，内容片段的MSM才可用。
>
>使用&#x200B;**内容片段**&#x200B;控制台时，MSM功能&#x200B;*不可用*。

## 操作方法 {#how-to}

有关将MSM用于内容片段(也适用于Assets)的详细信息，请参阅以下文档：

* 如何将[MSM用于内容片段(和Assets)](/help/assets/reuse-assets-using-msm.md)

* [创建Live Copy](/help/assets/reuse-assets-using-msm.md)

  >[!CAUTION]
  >
  >如果要使用MSM创建内容片段的副本)，则应该从各个[内容片段模型](/help/assets/content-fragments/content-fragments-models.md)中使用的任何数据类型中删除任何&#x200B;**唯一**&#x200B;约束。

* [查看源和Live Copy的属性和状态](/help/assets/reuse-assets-using-msm.md#properties)
* [将修改从源传播到Live Copy](/help/assets/reuse-assets-using-msm.md#rollout-sync)
* 取消并恢复以下项目的继承：
   * [内容片段编辑器](/help/assets/content-fragments/content-fragments-variations.md#inheritance)中的字段和变量
   * [相关资源的元数据](/help/assets/content-fragments/content-fragments-variations.md#canceling-reenabling-inheritance-individual-items)
* [暂停和恢复关系](/help/assets/reuse-assets-using-msm.md#suspend-resume)
* [删除实时关系](/help/assets/reuse-assets-using-msm.md#detach)
* [比较内容片段的MSM(和Assets)与站点的MSM](/help/assets/reuse-assets-using-msm.md#comparison)

## 限制 {#limitations}

* 对于内容片段，修改时触发器和关联的转出配置不存在。
