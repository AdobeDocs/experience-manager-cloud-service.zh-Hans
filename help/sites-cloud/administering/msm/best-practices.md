---
title: MSM 最佳实践
description: 了解由 Adobe 工程和咨询团队编译的最佳实践，帮助启动和运行 AEM Multi Site Manager。
feature: Multi Site Manager
role: Admin
exl-id: 61b8ded8-3b9e-423f-85a9-7280e1a721cc
source-git-commit: 24a4a43cef9a579f9f2992a41c582f4a6c775bf3
workflow-type: ht
source-wordcount: '1433'
ht-degree: 100%

---

# MSM 最佳实践 {#msm-best-practices}

## 常规 {#general}

MSM 是用于自动化内容部署的可配置框架。实施通常涉及网站的主要部分，并且跨多个组织和地理区域。因此，强烈建议您像规划网站一样仔细规划 MSM 实施：

* 在开始实施之前，仔细&#x200B;**规划结构和内容流**。
* **进行所需数量的自定义，越少越好。**&#x200B;虽然 MSM 支持高度自定义（例如转出配置），但通常情况下，网站的性能、可靠性和可升级性的最佳实践旨在最大程度地减少自定义。
* 尽早建立&#x200B;**治理**&#x200B;模型，并相应地培训用户以确保成功。从治理的角度来看，最佳实践是&#x200B;**最大程度地减少本地内容制作者具有的授权**（需要此授权才能将内容分配/连接到其他本地用户及其各自的 Live Copy）。这是因为，不受控制的链式继承会大大增加 MSM 结构的复杂性并降低其性能和可靠性。
* 在针对您的结构、内容流、自动化和治理制定计划后，**为您的系统创建原型并进行彻底测试**，然后再开始实时实施。
* 请记住，**Adobe 咨询和领先的系统集成商**&#x200B;在使用 MSM 规划和实施内容自动化方面拥有丰富的经验，他们可以帮助您启动 MSM 项目并完成整个实施。

## Live Copy 源和 Blueprint 配置 {#live-copy-sources-and-blueprint-configurations}

请记住，可使用[常规页面](creating-live-copies.md#creating-a-live-copy-of-a-page)或 [Blueprint 配置](creating-live-copies.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)创建 Live Copy。二者都是有效的用例。

使用 Blueprint 配置的额外好处是：

* 允许作者对 Blueprint 使用&#x200B;**转出**&#x200B;信息，以便显式地将修改推送到从该 Blueprint 继承的 Live Copy。
* 允许作者使用&#x200B;**创建站点**，以便轻松地选择语言并配置 Live Copy 的结构。
* 为与 Blueprint 有关系的 Live Copy 定义默认转出配置。

如果未引用 Blueprint 配置，则只能从 Live Copy 本身启动部署，本质上是从源中提取内容。

使用 Live Copy 创建新站点时，创建 Blueprint 配置以确保完整 MSM 功能集的可用性是有利的。

>[!NOTE]
>
> 请注意，“权限”选项卡中的 CUG 无法从 Blueprint 转出到 Live Copy。请在配置 Live Copy 时对此进行规划。

## 组件和容器同步 {#components-and-container-synchronization}

通常，MSM 中关于组件同步的转出规则是：

* 组件转出时将与 Blueprint 中包含的任何资源同步。
* 容器仅同步当前资源。

这意味着组件将被视为聚合，并且在转出时，组件本身及其所有子组件都将替换为 Blueprint 中的组件。这意味着，如果本地将资源添加到此类组件中，它将在转出时移至 Blueprint 的内容中。

为了支持组件的嵌套，以便在转出中维护本地添加的组件，必须将组件声明为容器。

>[!NOTE]
>
>将属性 `cq:isContainer` 添加到组件中以将它指定为容器。

## 创建站点 {#create-site}

请注意，AEM 提供了两种创建 Live Copy 的主要方法：

* 在[创建 Live Copy](creating-live-copies.md#creating-a-live-copy-of-a-page) 时 – 这可以被视为更通用的方法，允许您从任何页面创建 Live Copy。Live Copy 的内容结构与源完全匹配。

* 在[创建站点](creating-live-copies.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)时 – 这是一种更专业的方法，主要用于创建具有多语言结构的网站。

以下是创建站点时要牢记的几个注意事项：

* 要创建新站点，您需要 [Blueprint 配置](creating-live-copies.md#managing-blueprint-configurations)。
* 要允许选择在新站点中创建的语言路径，相应的语言根必须存在于 Blueprint（源）中。
* 在[将新站点创建为 Live Copy](creating-live-copies.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)（依次使用&#x200B;**创建**&#x200B;和&#x200B;**站点**）后，此 Live Copy 的前两个级别&#x200B;*较低*。页面的子级不属于实时关系，但如果找到与触发器匹配的实时关系，则转出仍会下降。

这有助于避免：

* 在 Blueprint 中手动添加语言（第一个级别下方）。
* 直接在语言根下手动添加内容，因为这不会导致在转出时自动将此新内容传送到 Live Copy。

## MSM 和多语言网站 {#msm-and-multilingual-websites}

MSM 可通过两种方式来帮助创建多语言网站：

在创建语言母版时，请记住以下几点：

* 虽然 MSM 本身&#x200B;**不提供内容翻译**，但它可以与第三方翻译连接器集成。请注意：
   * MSM 允许您在页面和/或组件级别取消继承。这有助于防止在下一次转出时覆盖已翻译的内容（来自 Live Copy，以及来自 Blueprint 的尚未翻译的内容）。
      * 一些第三方翻译连接器会自动实施对 MSM 继承的管理。
      * 请与您的翻译服务提供商联系以获取更多信息。
      * 创建并翻译语言母版的另一种方法是将语言副本与 AEM 的现成的翻译集成框架结合使用。

有关更多信息，请参阅[翻译多语言站点的内容](/help/sites-cloud/administering/translation/overview.md)和[翻译最佳实践](/help/sites-cloud/administering/translation/best-practices.md)。

## 结构更改和转出 {#structure-changes-and-rollouts}

对 Blueprint/源树中内容结构的修改会以不同的方式在 Live Copy 中反映出来。这取决于修改类型：

* 在 Blueprint 中&#x200B;**创建**&#x200B;新页面将导致在使用标准转出配置进行转出后，在 Live Copy 中创建相应的页面。
* 在 Blueprint 中&#x200B;**删除**&#x200B;页面将导致在使用标准转出配置进行转出后，从 Live Copy 中删除相应的页面。
* 在 Blueprint 中&#x200B;**移动**&#x200B;页面将&#x200B;**不会**&#x200B;导致在使用标准转出配置进行转出后，在 Live Copy 中移动相应的页面：
   * 此行为的原因是页面移动隐式包含页面删除。这可能会导致发布时出现意外行为，因为删除创作实例上的页面会自动停用发布实例上的相应内容。这也可能对相关项目（如链接、书签等）产生其他影响。
      * 相应 Live Copy 页面中的内容继承已更新，以反映其源在 Blueprint 中的新位置。
      * 要完全实施从 Blueprint 到 Live Copy 的页面移动，请考虑[页面移动最佳实践。](#page-move)

### 页面移动最佳实践 {#page-move}

考虑在 Live Copy 中移动页面时，请考虑以下最佳实践。

>[!NOTE]
>
>以下内容仅适用于 [On Rollout 触发器](live-copy-sync-config.md#rollout-triggers)。

1. 创建自定义转出配置。
   * 此新配置必须包含操作 `PageMoveAction`。
   * 不要向此配置添加其他操作。
1. 定位新配置。
   * 要在 Live Copy 中的旧位置删除相应页面时完全转出页面移动，请执行以下操作：
      * 将新创建的配置放置在标准转出配置的前面。标准转出配置将负责删除旧位置的页面。
      * 要转出页面移动并将相应页面保留在 Live Copy 中的旧位置（实质上是复制内容），请执行以下操作：
         * 将新创建的配置放置在标准转出配置的后面。这将确保未在 Live Copy 中删除内容或从发布中停用内容。

## 自定义转出 {#customizing-rollouts}

MSM 转出配置是高度自定义的。您应意识到，自动化转出可能会产生深远的影响。作为最佳实践，您应在进行以下活动之前进行非常仔细的规划：

* 使用 [onModify 触发器](#onmodify)自动化转出
* 自定义[节点类型/属性](#node-types-properties)
* 启动后续工作流
* 在转出过程中激活内容

### onModify {#onmodify}

在使用[转出触发器](live-copy-sync-config.md#rollout-triggers) `onModify` 时，您应考虑：

* 使用 `onModify` 触发器自动化转出可能会对创作性能产生负面影响，因为它们会在每次修改页面后触发转出。
* 转出结果可能与预期结果不同：
   * 您不能指定生成的修改事件的顺序。
   * 基于事件的架构不能保证传递给 Rollout Manager 的事件的顺序。
* 如果对同一资源进行并发更新，则使用此转出配置可能会导致发生提交冲突。

因此，如果自动转出启动的好处多于任何潜在的性能问题，建议您仅使用 `onModify` 触发器。

### 节点类型/属性 {#node-types-properties}

除了自定义转出操作之外，MSM 还允许您自定义正在转出的节点属性。[MSM OSGi 配置允许您排除](live-copy-sync-config.md#excluding-properties-and-node-types-from-synchronization)从源复制到 Live Copy 的节点类型。

## 更多信息 {#further-information}

有关 MSM 和 Live Copy 的更多详细信息，请参阅以下文章。

* [创建并同步 Live Copy](creating-live-copies.md)
* [Live Copy 概述控制台](live-copy-overview.md)
* [配置 Live Copy 同步](live-copy-sync-config.md)
* [MSM 转出冲突](rollout-conflicts.md)
