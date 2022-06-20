---
title: 重用内容 – 多站点管理器和 Live Copy
description: 了解如何通过 AEM 强大的 Live Copy 和多站点管理器功能重用内容。
feature: Multi Site Manager
role: Admin
exl-id: 22b4041f-1df9-4189-8a09-cbc0c89fbf2e
source-git-commit: 24a4a43cef9a579f9f2992a41c582f4a6c775bf3
workflow-type: ht
source-wordcount: '2682'
ht-degree: 100%

---

# 重用内容：多站点管理器和 Live Copy {#multi-site-manager-and-live-copy}

利用多站点管理器 (MSM)，您可以在多个位置使用相同的站点内容。MSM 使用其 Live Copy 功能来做到这一点。

* 利用 MSM，您可以：
   * 创建内容一次，然后
   * 在同一站点的其他区域内或其他站点上重用此内容（通过 [Live Copy](#live-copies)）。
* 之后，MSM 将维护您的源内容与其 Live Copy 之间的实时关系，以便：
   * 当您对源内容进行更改时，源和 Live Copy 将同步。
   * 可以通过断开各个子页面和/或组件的实时关系来仅对 Live Copy 的内容进行调整。

此页面概述了如何通过 MSM 重用内容。以下页面详细介绍了相关问题。

* [创建并同步 Live Copy](creating-live-copies.md)
* [Live Copy 概述控制台](live-copy-overview.md)
* [配置 Live Copy 同步](live-copy-sync-config.md)
* [MSM 转出冲突](rollout-conflicts.md)
* [MSM 最佳实践](best-practices.md)

## 可能的情况 {#possible-scenarios}

有许多针对 MSM 和 Live Copy 的用例。一些情况包括：

* **跨国 – 全球到本地公司**

   MSM 支持的一个典型用例是在多个采用同一语言的跨国站点中重用内容。这将允许重用核心内容，并允许国家变化。

   例如，[WKND 教程示例](/help/implementing/developing/introduction/develop-wknd-tutorial.md)的英语部分是为美国客户创建的。此站点的大部分内容也可用于其他为不同国家/地区和文化的说英语的客户服务的 WKND 站点。虽然所有站点的核心内容都相同，但可以进行区域调整。

   以下结构可用于美国和加拿大的站点。请记下 `language-masters` 节点如何维护英语以及其他语言内容的主副本。此内容可用作英语以及其他区域语言内容的基础。

   ```xml
   /content
       |- wknd
           |- language-masters
               |- en
               |- es
               |- fr
           |- us
               |- en
               |- es
           |- ca
               |- en
               |- fr
   ```

   >[!NOTE]
   >
   >MSM 不翻译内容。它用于创建所需的结构和部署内容。
   >
   >
   >有关此类示例，请参阅[为多语言站点翻译内容](/help/sites-cloud/administering/translation/overview.md)。

* **国内 – 总部到地区分支机构**

   或者，拥有经销商网络的公司可能希望为各个经销商提供单独的网站，每个网站均是总部提供的主站点的变体。这可能适用于拥有多个地区办事处的单一公司，或由中央特许专营授权公司和多个当地特许经营人构成的全国特许经营体系。

   总部可以提供核心信息，而区域实体可以添加本地信息，例如详细联系方式、营业时间和活动。

   ```xml
   /content
       |- head-office-berlin
       |- branch-hamburg
       |- branch-stuttgart
       |- branch-munich
       |- branch-frankfurt
   ```

* **多个版本**

   MSM 可以创建特定子分支的版本。例如，支持子站点可以保存特定产品的不同版本的详细信息，其中基本信息保持不变，只需更改已更新的功能：

   ```xml
   /content
       |- game-support
           |- polybius
               |- v5.0
               |- v4.0
               |- v3.0
               |- v2.0
               |- v1.0
   ```

   >[!TIP]
   >
   >在此类场景中，问题就变成了是直接复制还是使用 Live Copy，这需要以下方面达到平衡：
   >
   >* 需要在多个版本上更新的核心内容量。
   >
   >相较于：
   >
   >* 需要调整的单独副本数量。


## 从 UI 访问 MSM {#msm-from-the-ui}

可使用相应控制台中的各种选项直接通过 UI 访问 MSM。

* **创建站点**（**站点**）

   * MSM 可帮助您管理拥有相同内容的多个网站。例如，通常为国际受众提供网站，以便大多数内容在所有国家/地区都是相同的，仅一小部分内容特定于单个国家/地区。MSM 可让您[创建根据源站点自动更新一个或多个站点的 Live Copy](creating-live-copies.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)。这还可以帮助您实施通用的基础结构，跨多个站点使用共有内容，维护共有外观，并专注于管理各个站点之间实际不同的内容。通过此方式创建站点：
      * 需要预定义的 Blueprint 配置来指定源。
      * 创建（预定义的）源的 Live Copy。
      * 为用户提供&#x200B;**转出**&#x200B;按钮。

* **创建 Live Copy**（**站点**）

   * MSM 可让您[创建单个页面或网站子分支的临时（一次性）Live Copy。](creating-live-copies.md#creating-a-live-copy-of-a-page)例如，复制子分支可提供有关产品的新/更新版本的信息。通过此方式创建 Live Copy：
      * 创建临时 Live Copy（无需 Blueprint 配置）。
      * 可用于（立即）创建任何页面/分支的 Live Copy。
      * 需要&#x200B;**同步**（不提供&#x200B;**转出**&#x200B;按钮）。

* **查看属性**（**站点**）

   * 在适当时，此选项可提供相关 **Live Copy** 或 **Blueprint** 的信息来帮助您[监控 Live Copy](creating-live-copies.md#monitoring-your-live-copy)。

* **引用**（**站点**）

   * [引用](/help/sites-cloud/authoring/getting-started/basic-handling.md#references)边栏提供了有关 **Live Copy** 的信息以及对相应操作的访问权限。

* **Live Copy 概述**（**站点**）

   * 利用此控制台，您可以[查看和管理您的 Blueprint 及其 Live Copy。](live-copy-overview.md)

* **Blueprint**（**工具** – **站点**）

   * 利用此控制台，您可以[创建和管理您的 Blueprint 配置。](creating-live-copies.md#creating-a-blueprint-configuration)

>[!NOTE]
>
>MSM 功能的各个方面可用于其他几个 AEM 功能，例如启动项。在这些情况下，Live Copy 由该功能管理。

### 使用的术语 {#terms-used}

作为介绍，下表概述了用于 MSM 的主要术语。后续部分和页面中将更详细地介绍这些术语。

| 术语 | 定义 | 更多详细信息 |
|---|---|---|
| 源 | 用作 Live Copy 的基础的原始页面 | 与 Blueprint 和/或 Blueprint 页面同义 |
| Live Copy | （源的）副本，由转出配置定义的同步操作维护 |  |
| Live Copy 配置 | Live Copy 的配置详细信息的定义 |  |
| 实时关系 | 给定资源的继承的有效定义，即源和 Live Copy 之间的连接 | 确保对源所做的更改能够与 Live Copy 同步 |
| Blueprint | 与源同义 | 可由 Blueprint 配置定义 |
| Blueprint 配置 | 用于指定源路径的预定义的配置 | 在 Blueprint 配置中引用 Blueprint 页面时，“转出”命令将变为可用 |
| 章节 | 要包含在 Live Copy 中的 Blueprint 部分 | 这些通常是根的子页面 |
| 同步 | 源和 Live Copy 之间内容同步的通用术语（通过&#x200B;**转出**&#x200B;和&#x200B;**同步**&#x200B;选项） |  |
| 转出 | 从源同步到 Live Copy | 可以由作者（在 Blueprint 页面上）或系统事件（由转出配置定义）触发 |
| 转出配置 | 用于确定将同步的属性及其同步方式和时间的规则 |  |
| 同步 | 从 Live Copy 页面发出的手动同步请求 |  |
| 继承 | 发生同步时，Live Copy 页面/组件从其源页面/组件继承内容 |  |
| 暂停 | 临时删除 Live Copy 与其 Blueprint 页面之间的实时关系。 |  |
| 分离 | 永久删除 Live Copy 与其 Blueprint 页面之间的实时关系。 |  |
| 重置 | 重置 Live Copy 页面以删除所有继承取消，并使页面恢复到与源页面相同的状态 | 重置会影响您对页面属性、段落系统和组件所做的任何更改。 |
| 浅 | 单页面的 Live Copy |  |
| 深 | 页面的 Live Copy 及其子页面 |  |

<!--
>[!TIP]
>
>See [Overview of the Java API](/help/sites-developing/extending-msm.md#overview-of-the-java-api) for the object names.
-->

## Live Copy {#live-copies}

MSM Live Copy 是特定站点内容的副本，它保留了与原始源的实时关系：

* Live Copy 从其源继承内容。
* 在对源进行更改时，同步会执行实际内容传输。
* 可将 Live Copy 视为：
   * 浅：单页面
   * 深：页面及其子页面
* 同步规则（称为转出配置）可确定将同步的属性及其同步时间。

在上一个示例中，`/content/wknd/language-masters/en` 是英语版的全局主站点。为了重用本站点的内容，创建了 MSM Live Copy：

* `/content/wknd/language-masters/en` 下的内容为源。
* `/content/wknd/language-masters/en` 下的内容复制到 `/content/wknd/us/en/` 和 `/content/wknd/ca/en` 节点下。这些是 Live Copy。
* 作者对 `/content/wknd/language-masters/en` 下的页面进行了更改。
* 触发后，MSM 会将这些更改同步到 Live Copy。

### Live Copy – 构图 {#live-copies-composition}

>[!NOTE]
>
>此部分中的图表和描述代表潜在 Live Copy 的快照。虽然它们并不全面，但提供了概述以重点说明具体特征。

最初创建 Live Copy 时，选定的源页面会以 1:1 的比例反映在 Live Copy 中。之后，还可以直接在 Live Copy 中创建新资源（页面和/或段落），因此了解这些变体以及它们对同步产生的影响会很有用。可能的构图包括：

* [具有非 Live Copy 页面的 Live Copy](#live-copy-with-non-live-copy-pages)
* [嵌套式 Live Copy](#nested-live-copies)

Live Copy 的基本形式具有：

* 以 1:1 的比例反映所选源页面的 Live Copy 页面。
* 一个配置定义。
* 为每个资源定义的实时关系：
   * 将 Live Copy 资源与其 Blueprint/源链接。
   * 在实现继承和转出时使用。

可以根据要求[同步](creating-live-copies.md#synchronizing-your-live-copy)更改。

![Live Copy 构图概述](../assets/live-copy-composition.png)

#### 具有非 Live Copy 页面的 Live Copy {#live-copy-with-non-live-copy-pages}

在 AEM 中创建 Live Copy 时，您可以查看和浏览 Live Copy 分支，并在 Live Copy 分支上使用常规 AEM 功能。这意味着您（或流程）可以在 Live Copy 中创建新资源（页面和/或段落）。例如，面向特定地区或国家的产品。

* 此类资源与源/Blueprint 页面没有实时关系，并且不会同步。
* 可能会出现 MSM 作为特殊情况处理的场景。例如，当您（或流程）在源/Blueprint 和 Live Copy 分支中创建具有相同位置和名称的页面时。有关此类情况，请参阅 [MSM 转出冲突](rollout-conflicts.md)以了解更多信息。

![具有非 Live Copy 页面的 Live Copy](../assets/live-copy-with-non-live-copy-pages.png)

#### 嵌套式 Live Copy {#nested-live-copies}

当您（或流程）[在现有 Live Copy 中创建新页面](#live-copy-with-non-live-copy-pages)时，此新页面也可以设置为其他 Blueprint 的 Live Copy。这称作嵌套式 Live Copy。在嵌套式 Live Copy 中，第一个或外部 Live Copy 会对第二个或内部 Live Copy 的行为产生如下影响：

* 为顶级 Live Copy 触发的深转出可以继续在嵌套式 Live Copy 中执行。
* 源之间的任何链接都将在 Live Copy 中重写。

例如，从第二个 Blueprint 指向第一个 Blueprint 的链接将被重写为从嵌套式/第二个 Live Copy 指向第一个 Live Copy 的链接。

![嵌套式 Live Copy](../assets/live-copy-nested.png)

>[!NOTE]
>
>如果您在 Live Copy 分支中移动或重命名页面，这将被视为嵌套式 Live Copy，以使 AEM 能够跟踪关系。

#### 堆叠式 Live Copy {#stacked-live-copies}

Live Copy 在作为浅 Live Copy 的子级创建时称为堆叠式 Live Copy。其行为与[嵌套式 Live Copy](#nested-live-copies) 的行为相同。

### 源、Blueprint 和 Blueprint 配置 {#source-blueprints-and-blueprint-configurations}

任何页面或页面分支都可用作 Live Copy 的源。不过，MSM 还允许您定义指定源路径的 Blueprint 配置。使用 Blueprint 配置的好处是：

* 允许作者对 Blueprint 使用&#x200B;**转出**&#x200B;选项。即，显式地将修改推送到从该 Blueprint 继承的 Live Copy。
* 允许作者使用&#x200B;**创建站点**。这可让作者轻松选择语言并配置 Live Copy 的结构。
* 为与 Blueprint 有关系的 Live Copy 定义默认转出配置。

Live Copy 的源可以是常规页面，也可以是 Blueprint 配置包含的页面。二者都是有效的用例。

源构成了 Live Copy 的 Blueprint。在执行以下操作时定义 Blueprint：

* [创建 Blueprint 配置](creating-live-copies.md#creating-a-blueprint-configuration) – 配置预先定义了要用于创建 Live Copy 的页面。
* [创建页面的 Live Copy](creating-live-copies.md#creating-a-live-copy-of-a-page) – 用于创建 Live Copy 的页面（源页面）是 Blueprint 页面。Blueprint 配置可能引用源页面，也可能不引用源页面。

### 转出和同步 {#rollout-and-synchronize}

转出是将 Live Copy 与其源同步的中央 MSM 操作。您可以手动执行转出，也可以自动进行转出。

* 可以定义[转出配置](#rollout-configurations)，以便特定[事件](live-copy-sync-config.md#rollout-triggers)能够促使自动进行转出。
* 在创作 Blueprint 页面时，您可以使用&#x200B;**[转出](creating-live-copies.md#rolling-out-a-blueprint)**&#x200B;命令来将更改推送到 Live Copy。
   * **转出**&#x200B;命令适用于 Blueprint 配置引用的 Blueprint 页面。

   ![转出](../assets/live-copy-rollout.png)

* 在创作 Live Copy 页面时，您可以使用&#x200B;**[同步](creating-live-copies.md#synchronizing-a-live-copy)**&#x200B;命令来将更改从源拉入 Live Copy。
   * **同步**&#x200B;命令始终适用于 Live Copy 页面，无论源/Blueprint 页面是否由 Blueprint 配置包含。

   ![同步](../assets/live-copy-synchronize.png)

### 转出配置 {#rollout-configurations}

转出配置定义 Live Copy 与源内容同步的时间和方式。转出配置由一个触发器和一个或多个同步操作组成：

* **触发器** – 触发器是触发实时操作同步的事件，例如源页面的激活。MSM 定义您可以使用的触发器。
* **同步操作** – 对 Live Copy 执行同步操作可使其与源同步。示例操作包括复制内容、对子节点排序和激活 Live Copy 页面。MSM 提供了大量同步操作。

>[!NOTE]
>
>您可以使用 Java API 为实例创建自定义操作。

可以重用转出配置，以便多个 Live Copy 可以使用相同的转出配置。标准安装包含了多个[转出配置](live-copy-sync-config.md#installed-rollout-configurations)。

### 转出冲突 {#rollout-conflicts}

转出可能会变得复杂，尤其是当作者同时在源和 Live Copy 中编辑内容时。因此，了解 AEM 如何处理[转出期间可能发生的任何冲突](rollout-conflicts.md)会很有用。

### 暂停和取消继承与同步 {#suspending-and-cancelling-inheritance-and-synchronization}

Live Copy 中的每个页面和组件均通过实时关系与其源页面和组件关联。实时关系配置来自源的 Live Copy 内容的同步。

您可以&#x200B;**暂停** Live Copy 页面的 Live Copy 继承，以便更改页面属性和组件。当您暂停继承时，页面属性和组件不再与源同步。

在编辑单个页面时，作者可以为组件&#x200B;**取消继承**。取消继承后，实时关系将暂停，并且不会针对该组件进行同步。当需要自定义内容的子部分时，取消继承和同步会很有用。

### 分离 Live Copy {#detaching-a-live-copy}

您也可以从 Live Copy 的 Blueprint [分离 Live Copy](creating-live-copies.md#detaching-a-live-copy) 以删除所有连接。

>[!CAUTION]
>
>分离操作是永久性且不可逆的。

分离操作将永久删除 Live Copy 与其 Blueprint 页面之间的实时关系。将从 Live Copy 中删除所有与 MSM 相关的属性，并且 Live Copy 页面会成为独立副本。

>[!TIP]
>
>请参阅[分离 Live Copy](creating-live-copies.md#detaching-a-live-copy) 以了解所有详细信息，包括对子页面和父页面产生的相关影响。

## 使用 MSM 的标准步骤 {#standard-steps-for-using-msm}

以下步骤描述了通过 MSM 重用内容并将更改同步到 Live Copy 的标准过程。

1. 开发源站点的内容。
1. 决定要使用的转出配置。

   1. MSM [安装了多个转出配置](live-copy-sync-config.md#installed-rollout-configurations)，可满足大量用例的要求。
   1. （可选）如果需要，您可以[创建转出配置](live-copy-sync-config.md#creating-a-rollout-configuration)。

1. 决定需要[指定要使用的转出配置](live-copy-sync-config.md#specifying-the-rollout-configurations-to-use)并按需配置的情况。
1. 如果需要，可以[创建 Blueprint 配置](creating-live-copies.md#creating-a-blueprint-configuration)来标识 Live Copy 的源内容。
1. [创建 Live Copy。](creating-live-copies.md#creating-a-live-copy)
1. 根据需要更改源内容。您应采用您组织已制定的常规内容审查和审批流程。
1. [转出](creating-live-copies.md#rolling-out-a-blueprint) Blueprint，或[将 Live Copy 与更改同步](creating-live-copies.md#synchronizing-a-live-copy)。

## 自定义 MSM {#customizing-msm}

MSM 提供了一些工具，以便您的实施能够适应共享内容时可能存在的特殊复杂性。

* **自定义转出配置** – 当安装的转出配置不符合您的要求时，您可以[创建转出配置](live-copy-sync-config.md#creating-a-rollout-configuration)。您可以使用任何可用的转出触发器和同步操作。

<!--
* **Custom Synchronization Actions** - [Create a custom synchronization action](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action) when the installed actions do not meet your specific application requirements. MSM provides a Java API for creating custom synchronization actions.
-->

## 最佳实践 {#best-practices}

[MSM 最佳实践](best-practices.md)页面包含有关您的实施的重要信息。
