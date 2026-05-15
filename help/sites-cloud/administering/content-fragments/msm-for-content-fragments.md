---
title: 使用MSM和活动副本重用内容片段
description: 了解如何使用MSM的Live Copy功能在多个位置使用相同或相似的内容片段内容，同时与源内容同步。
badgeSaas: label="AEM Sites" type="Positive" tooltip="适用于AEM Sites)。"
feature: Content Fragments
role: User
solution: Experience Manager Sites
hide: true
hidefromtoc: true
index: false
exl-id: 5039cf92-21ff-4d6c-a684-72eab13b519d
source-git-commit: cc3cd74ad87f4213a200f36745ab3d335edca02d
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 4%

---

# 使用MSM重用内容片段 {#reuse-content-fragments-using-msm}

多站点管理器(MSM)和Live Copy功能允许您在多个位置使用相同的内容，同时与源内容同步。

<!-- CQDOC-23473 - feature is currently beta so page is hidden, see metadata -->
<!-- CQDOC-23473 - screenshots -->
<!-- CQDOC-23473 - only mentioned once in ToC, add entries -->
<!-- CQDOC-23473 - will work on folders -->

<!-- CQDOC-23473 - feature is currently beta remove Caution for GA -->

>[!CAUTION]
>
>内容片段控制台中的MSM目前是Beta功能，仅适用于特定客户。
>
>通过&#x200B;**Assets**&#x200B;控制台使用内容片段时，也可以使用MSM获取内容片段。

* 使用MSM活动副本，您可以：
   * 创建内容一次
   * 在同一站点的其他区域、其他站点或应用程序中重用此内容。
* 之后，MSM 将维护您的源内容与其 Live Copy 之间的实时关系，以便：
   * 当您更改源内容时，源和活动副本将同步。
   * 您可以通过断开单个子片段和/或组件的实时关系来仅调整实时副本的内容。

<!-- CQDOC-23473 - feature is currently beta remove Caution for GA -->

有关MSM概念的详细概述，请参阅重用内容：多站点管理器和Live Copy 。

<!--
For a detailed overview of MSM concepts see [Reusing Content: Multi Site Manager and Live Copy](/help/sites-cloud/administering/msm/overview.md).
-->

<!-- CQDOC-23473 - feature is currently beta remove Caution for GA -->

>[!NOTE]
>
>通过Adobe Experience Manager中的多站点管理器(MSM)功能，用户可以重复使用一次创作，然后跨多个Web位置重复使用的内容。

<!--
>[!NOTE]
>
>[Multi Site Manager (MSM)](/help/sites-cloud/administering/msm/overview.md) functionality in Adobe Experience Manager enables users to reuse content that is authored once and then reused across multiple web-locations. 
-->

使用MSM获取内容片段，您可以：

* 创建内容片段一次，然后创建（链接）这些片段的副本以在站点或应用程序的其他区域重用。
* 通过将源副本更新一次，然后将更改推送到（实时）副本，来保持多个副本的同步。
* 通过暂时或永久暂停父片段与子片段之间的链接进行本地更改；完全暂停或暂停其变体或字段的链接。

MSM for Content Fragments与内容片段编辑器中的功能相结合，允许您在字段级别中断和恢复继承。

<!-- CQDOC-23473 - feature is currently beta remove Caution for GA -->

>[!NOTE]
>
>本页介绍使用&#x200B;**内容片段**&#x200B;控制台时的MSM功能。
>
>通过&#x200B;**Assets**&#x200B;控制台使用内容片段时，也可以使用MSM获取内容片段。

<!--
>[!NOTE]
>
>This page covers MSM functionality when using the **Content Fragments** console.
>
>MSM for Content Fragments is also available when using [Content Fragments via the **Assets** console](/help/assets/content-fragments/content-fragments-msm.md). 
-->

## 创建 Live Copy {#create-a-live-copy}

<!-- CQDOC-23473 - exclude children or referenced content fragments? -->

要创建内容片段的Live Copy，请执行以下操作：

1. 在内容片段控制台导航到片段的位置。
1. 选择您的片段。
1. 从顶部工具栏中选择&#x200B;**创建Live Copy**。
1. 在打开的对话框中，指定目标并继续&#x200B;**下一步**。
1. 指定属性。 您可以指定标题、名称以及Live Copy是否应排除子项（嵌套片段）。
1. 继续&#x200B;**下一步**。
1. 选择是要立即创建Live Copy （**现在**），还是在&#x200B;**稍后**&#x200B;日期和时间创建Live Copy。
1. 通过&#x200B;**创建Live Copy**&#x200B;确认。

   <!-- CQDOC-23473 - feature is currently beta remove Caution for GA -->

   >[!CAUTION]
   >
   >如果要使用MSM创建内容片段的副本)，则应该从相应内容片段模型中使用的任何数据类型中删除任何&#x200B;**Unique**&#x200B;约束。

   <!--
   >[!CAUTION]
   >
   >If you want to use MSM to create copies of Content Fragments), then any **Unique** constraints should be removed from any Data Types used in the respective [Content Fragment Models](/help/assets/content-fragments/content-fragments-models.md).
   -->

## 查看属性和状态 {#view-properties-and-status}

要查看属性以及源和Live Copy的状态，请执行以下操作：

1. 在内容片段控制台导航到片段的位置。
1. 选择您的片段。
1. 选择片段的&#x200B;**标题**&#x200B;列中的“信息(i)”图标。
将打开右侧的信息面板。
1. 选择&#x200B;**Live Copy详细信息**&#x200B;的选项卡。

   ![有关Live Copy的信息](/help/sites-cloud/administering/content-fragments/assets/cf-msm-information.png)

## 传播修改 {#propagate-modifications}

在源和Live Copy之间传播修改。

### 同步 {#synchronize}

要触发将内容更新从Live Copy提取到源的同步，请执行以下操作：

1. 在内容片段控制台导航到片段源的位置。
1. 选择您的片段。
1. 从工具栏中选择&#x200B;**同步**。
1. 在对话框中确认&#x200B;**同步**。

### 转出 {#rollout}

要触发将源更新推送到Live Copy的转出，请执行以下操作：

1. 在内容片段控制台导航到片段Live Copy的位置。
1. 选择您的片段。
1. 从工具栏中选择&#x200B;**转出**。 此时将打开向导，引导您完成该过程。
1. 选择要包含在转出中的活动副本，然后&#x200B;**继续**。
1. 计划立即转出（**现在**）或&#x200B;**稍后**。
1. 根据需要&#x200B;**继续**。

<!-- CQDOC-23473 - feature is beta, is in authoring so remove here when GA -->

## 在编辑器中取消并还原继承 {#cancel-and-revert-to-inheritance-in-the-editor}

继承是一种机制，通过该机制，可以将内容从一个片段自动推送到另一个片段。 继承的字段和变体可以是多站点管理的产物。

您可以在内容片段编辑器中取消（然后还原到）继承。 根据上下文，这可用于变体，或者单个字段（如果片段是Live Copy的一部分）。

例如：

* 取消继承

  ![“取消继承”图标](/help/sites-cloud/administering/content-fragments/assets/cf-authoring-cancel-inheritance.png)

* 还原到继承（如果继承已取消）

  ![还原到继承图标](/help/sites-cloud/administering/content-fragments/assets/cf-authoring-revert-to-inheritance.png)

<!-- CQDOC-23473 - feature is currently beta reinstate Note for GA -->

<!--
## Cancel, and revert to, inheritance {#cancel-and-reinstate-inheritance}

Inheritance is the mechanism where content can be automatically pushed from one fragment to another. Inherited fields, and variations, can be the product of Multi-Site Management.

You can cancel (then revert) the inheritance. Depending on the context, this can be available for a variation, or an individual field, if the fragment is part of a live copy.
-->

<!--
>[!NOTE]
>
>For more details see [Cancel, and revert to, inheritance in the editor](/help/sites-cloud/administering/content-fragments/authoring.md#cancel-and-revert-to-inheritance).
-->

## 比较内容片段和站点页面的MSM {#compare-msm-for-content-fragments-and-sites-pages}

<!-- CQDOC-23473 - needs a detailed review -->

在大多数情况下，内容片段的MSM与MSM for Sites Pages功能的行为匹配。 需要注意的一些主要区别是：

* 在MSM中，站点页面的Blueprint称为内容片段的Live Copy源。
* 对于站点页面，您可以比较Blueprint及其Live Copy，但内容片段无法将源与其Live Copy进行比较。
* 您无法在内容片段控制台中编辑Live Copy。
* 站点页面通常具有子项，但内容片段没有，尽管它们可能具有引用的片段。 包含或排除子项的选项引用这些引用的片段。
* MSM for Content Fragments不支持删除创建站点向导中的章节步骤。
* 内容片段的MSM不支持在页面属性上配置MSM锁定。
* 对于内容片段的MSM，仅使用&#x200B;**标准转出配置**。 其他转出配置不适用于MSM的内容片段。

>[!NOTE]
>
>请记住，通过内容片段控制台访问的内容片段的MSM基于Assets功能；这是因为它们存储为Assets（虽然被认为是Sites功能）。

## 限制 {#limitations}

* 对于内容片段，修改时触发器和关联的转出配置不存在。
